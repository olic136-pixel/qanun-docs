# FSRA Truncation Root-Cause Investigation

**Generated:** 2026-05-15
**Source data:** `~/ADGM/adgm-corpus/audit/findings/truncation_candidates.csv` (6,499 total rows; 6,271 FSRA)
**Sweep heuristic:** `~/ADGM/adgm-corpus/audit/truncation_candidates.py` — `LENGTH(text) < 200 AND has_children AND text NOT ending in .?!:;)"`
**Investigation method:** five-sample diagnostic with corpus-internal cross-check; source-page comparison blocked at scale (83.7% of FSRA docs missing `source_url` — A5.C carry).

---

## Headline finding

**The 6,271 FSRA "truncation candidates" do not all represent ingestion truncation.** The sweep heuristic conflates two structurally distinct populations, both of which the heuristic flags. Honest decomposition: **~968 are parent-header structural artifacts (false positives); ~5,303 are short-rule rows that *may* be genuine mid-text truncation but cannot be confirmed at scale without source-page comparison.**

None of the brief's three original hypotheses (parser regex misfire / PDF extraction failure / source truncation) fits cleanly on its own. The pattern is a fourth hypothesis layered over the sweep heuristic's over-flagging.

## Length × children cross-tab (the decisive evidence)

| Bucket | Count | % of FSRA truncation rows | Pattern |
|---|---:|---:|---|
| `text_len ≤ 20` chars (heading-only) | 968 | 15.4% | **Parent-header artifact** — the row is just the chapter title (e.g., `"10.3 IRAP"`, `"2.10 Custody"`, `"5.2 General"`) |
| `text_len 21-100`, with children | 3,249 | 51.8% | **Ambiguous** — short rule bodies that introduce sub-paragraph children |
| `text_len 101-199`, with children | 2,054 | 32.8% | **Ambiguous** — mid-length rule bodies with sub-paragraph children |
| `text_len ≥ 200` | 0 | 0.0% | Excluded by the sweep heuristic (`MAX_LEN = 200`) |
| Any rows with `child_count = 0` | 0 | 0.0% | Excluded by heuristic (`AND EXISTS (SELECT 1 FROM sections c WHERE c.parent_ref = s.section_ref)`) |

The bottom two rows are the key: **the sweep cannot, by construction, flag the canonical signature of mid-text truncation** — a long-text rule with no children whose final sentence runs off mid-word. Every flagged row has children. So whatever "truncation" the sweep detects is constrained to short-text-with-children, which is a structurally ambiguous population.

## Five-sample diagnostic

| # | Rulebook | section_ref | text_len | child_count | text_tail | source_url | Interpretation |
|---|---|---|---:|---:|---|---|---|
| 1 | PRU | `PRU 10.3` | 9 | 4 | `'10.3 IRAP'` | (empty) | **Parent header** — "IRAP" is the chapter heading; substantive content lives in `PRU 10.3.1` / `10.3.2` / `10.3.3` |
| 2 | COBS | `COBS 5.2` | 11 | 4 | `'5.2 General'` | (empty) | **Parent header** — same shape |
| 3 | MIR | `MIR 2.10` | 12 | 2 | `'2.10 Custody'` | (empty) | **Parent header** — same shape |
| 4 | GPM | `GPM 3.4` | 12 | 4 | `'Introduction'` | https://en.adgm.thomsonreuters.com/rulebook/guidance-policies-manual-gpm-ver07311025 | **Parent header** — only sample with a URL, same shape |
| 5 | (PRU 10.3.2 — context comparison) | `PRU 10.3.2` | 196 | 6 | `…processes and ` | (empty) | **Possibly genuine** — text ends mid-word (`"processes and "`), suggests truncation of sub-paragraph (1) before sub-paragraph (2) begins |

Sample 5 is the ambiguous case. The PRU 10.3 children listing confirmed the children include `10.3.2(2)`, `10.3.2(3)`, ... `10.3.2(a)`, `10.3.2(b)` — i.e., the parser correctly identified the sub-paragraph break points, but the `(1)` body captured in the parent row ends mid-word. That MIGHT be (a) genuine mid-paragraph truncation, OR (b) the parser correctly captured everything up to the `(2)` marker on the source page and the `(1)` body really does end at "processes and " before the `(2)` marker on a new line. Without source comparison, indeterminate.

## Why source comparison can't decide it at scale

`documents.source_url` is empty for 550 of 657 FSRA current docs (**83.7%**). Of the 216 distinct docs containing the 6,271 truncation candidates, **only 1 has a populated source_url** (doc #2325 GPM ver07311025). The other 215 docs have no recorded ingestion provenance.

This is the **L-category A5.C source-URL backfill carry** (2,099 rows corpus-wide as of the 2026-05-12 audit). Remediation of FSRA truncations is **gated on A5.C** for the 215 docs.

## Per-rulebook breakdown (FSRA)

| Rulebook | Truncation rows | % of FSRA total |
|---|---:|---:|
| COBS | 2,747 | 43.8% |
| PRU | 789 | 12.6% |
| MKT | 605 | 9.6% |
| MIR | 446 | 7.1% |
| AML | 368 | 5.9% |
| FEES | 285 | 4.5% |
| PIN | 271 | 4.3% |
| GEN | 221 | 3.5% |
| IFR | 206 | 3.3% |
| FUNDS | 142 | 2.3% |
| CIB | 98 | 1.6% |
| GLO | 71 | 1.1% |
| (other: OTHER, GPM, PIN-AMEND, CIB-AMEND) | 22 | 0.4% |

COBS dominates at 43.8% — consistent with its being the largest FSRA rulebook.

## Recommended remediation (two-stage)

### Stage 1 — Refine the truncation sweep heuristic (fast)

The current sweep does not distinguish parent-headers from genuine truncation. Two changes will materially improve signal-to-noise:

1. **Exclude rows where `text_len ≤ 20` AND `child_count ≥ 1`** — these are parent-header artifacts. Removes ~968 FSRA false positives plus equivalent across other jurisdictions (estimated total ~1,200 false positives corpus-wide).
2. **Exclude rows where `text` ends with `:` followed by whitespace** — these are list-introducers (e.g., `"In addition to (2), the firm must conduct an IRAP assessment:"`) where the items live in the children. The sweep already excludes terminators but treats `:` as a terminator inconsistently with this pattern.

Sized as **half-day**: edit `audit/truncation_candidates.py`, re-run, regenerate `truncation_candidates.csv`, refresh `violation-matrix.md`. No corpus.db writes.

### Stage 2 — Genuine truncation investigation (blocked on A5.C)

After Stage 1, the remaining ~5,303 ambiguous rows need source-page comparison to confirm whether sample 5's pattern (text ending mid-word) is widespread. **This is blocked on A5.C** — 215 of 216 affected docs have no `source_url`. Per-rulebook session sized once A5.C lands provenance for the affected docs (Sprint sized after A5.C closes).

### What the brief's three hypotheses turned out to mean

- **H1 (parser regex misfire):** Plausible for the ~5,303 ambiguous rows (sample 5 shape) — but cannot be confirmed without source comparison. Likely a contributor, not the dominant signal.
- **H2 (PDF extraction failure):** No evidence. Page-boundary truncation signatures (text ending exactly at a page break) would require source-PDF re-extraction to test; deferred.
- **H3 (source truncation):** Cannot be tested without source URL access. Implausible for Thomson Reuters portal content (their rendering is structured HTML).

## Estimated remediation effort

| Stage | Scope | Effort | Dependencies |
|---|---|---|---|
| 1 — Sweep refinement | Refine heuristic, re-run, refresh matrix | 1 session (half-day) | None |
| 2 — Per-rulebook source comparison | 215 FSRA docs need source_url backfill, then ~5,303 rows compared | Multi-session, per-rulebook | A5.C completion (separate carry) |

## Register impact

This memo informs **M19 — FSRA structural_parser truncation systematic fix** (the proposed M-category entry). Status should reflect that Stage 1 is unblocked + sized; Stage 2 is blocked on A5.C. The original framing (6,271 sections each needing fix) over-counts the genuine integrity issue by an unknown but material amount.

## Open questions for follow-up sessions

1. **Will the heuristic refinement reveal a cleaner truncation signal?** Stage 1 + a second sweep will show whether the remaining count is small enough for source-comparison sampling without the full A5.C backfill.
2. **Does the same sweep over-flag pattern apply to the other jurisdictions' truncation rows?** VARA (41), DFSA (47), EL_SALVADOR (70), PANAMA_SMV (50), BVI_FSC (1) — small enough to manually inspect; likely the heuristic fix applies cleanly.
3. **Is `audit/violation-matrix.md`'s headline "20,567 violations" similarly inflated by this kind of heuristic over-counting?** A pass over the other 5 sweeps with the same lens would be worth a half-day.
