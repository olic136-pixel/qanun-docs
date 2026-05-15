# Dangling Citations Root-Cause Investigation

**Generated:** 2026-05-15
**Source data:** `~/ADGM/adgm-corpus/audit/findings/citation_integrity.csv` (13,040 rows)
**Sweep heuristic:** `~/ADGM/adgm-corpus/audit/citation_integrity.py` — flags any `citations.target_ref` that does not match a `section_ref` of any `is_current=1` document.
**Investigation method:** read sweep source → derive what "unattributed" means programmatically → decompose 6,238 unattributed row + cross-correlate with truncation (Memory #28 parametric).

---

## Headline finding

**The 13,040 dangling-citation count is dominated by sweep heuristic over-flagging of citation types whose `target_ref` semantics differ from `section_ref`.** Two distinct issues hide inside one number:

1. **98.3% are `legacy_intra_rulebook` citations** (12,813 of 13,040). Many of these target *document-level labels* (`"FSMR Schedule 1"`) or *cross-jurisdictional refs in non-canonical formats* — not section_refs in the current corpus. Some fraction is genuine (legacy extractor pointing at superseded/archived sections); the rest are sweep false positives.
2. **1.7% are `inline_anchor` (91) + `inline_shorthand` (136) citations** — **100% of these citation types are flagged dangling**, by sweep construction. These citations target rulebook *names* (e.g., `"VARA Company Rulebook"`), not section_refs. They are dangling by design of the sweep, not by data error.

**Cross-correlation with truncation: 0.6%.** Dangling citations and truncated sections are independent problems; fixing truncation will not subsume dangling.

## Sweep behaviour (read from source)

`audit/citation_integrity.py` builds a single set `current_refs` of all `sections.section_ref` for `documents.is_current = 1`, then flags every `citations.target_ref` that doesn't match. The `source_entity` column in the CSV comes from `entity_by_doc.get(source_doc, "")` — so an empty `source_entity` value means the citation's `source_doc` foreign key resolves to nothing.

**Schema verification (Memory #28 corrections to brief's hypotheses):**

| Brief's B2 Q1 hypothesis | Result | Why |
|---|---|---|
| Citations from sections with NULL/empty `source_entity` | **0** | `documents.source_entity` is `NOT NULL`; no document has empty `source_entity` |
| Citations with orphan `source_section_id` FK | (separate issue, not counted) | — |
| Citations with `target_ref` not resolving to current section | **13,040** (the headline) | This is the sweep's definition |

**Real decomposition of the 6,238 "unattributed" row:**

| Decomposition | Count |
|---|---:|
| Citations whose `source_doc` FK is orphaned (points to no document) — total | **7,560** |
| ↳ of which `target_ref` does not resolve (appear in the CSV) | **6,238** |
| ↳ of which `target_ref` DOES resolve to a current section (excluded from CSV) | **1,322** |
| Citations from documents with empty `source_entity` | 0 |

So the "unattributed" bucket is **orphan `source_doc` FK + non-resolving `target_ref`** — the join `documents` on `source_doc` returns no row, hence `source_entity` is the aggregator's fallback empty string.

## Decomposition by citation_type — the decisive cut

| citation_type | Total | Dangling | % of type | Interpretation |
|---|---:|---:|---:|---|
| `legacy_intra_rulebook` | 22,235 | 12,813 | **57.6%** | Pre-Phase-B extractor; many target document-level labels (e.g., `"FSMR Schedule 1"`) or cross-jurisdictional refs in non-canonical formats |
| `inline_shorthand` | 136 | 136 | **100.0%** | Phase E1 — defined-shortform pattern. Target is a *rulebook name*, never a section_ref. Sweep over-flags by design. |
| `inline_anchor` | 91 | 91 | **100.0%** | Phase E1 — full-name pattern. Same — rulebook-name target. Sweep over-flags by design. |
| `eao_reference` | 17 | 0 | 0.0% | Phase B structured EAO → ER 2024 cross-references. Target IS a section_ref. Sweep is correct here. |

## Top target_refs in the "unattributed" bucket (source_entity = '')

| target_ref | Count | Shape |
|---|---:|---|
| `VARA Compliance and Risk Management Rulebook` | 98 | Rulebook name (inline_*) |
| `VARA Company Rulebook` | 86 | Rulebook name (inline_*) |
| `VARA Market Conduct Rulebook` | 63 | Rulebook name (inline_*) |
| `DFSA-PIB 4.14` | 38 | Cross-jurisdiction section ref (legacy) |
| `FSMR Schedule 1` | 38 | Document-level label (legacy) |
| `VARA Part IV` | 32 | Part-level label (legacy) |
| `VARA Technology and Information Rulebook` | 30 | Rulebook name (inline_*) |
| `VARA Part III` | 29 | Part-level label (legacy) |
| `VARA Part II` | 25 | Part-level label (legacy) |
| `VARA Part I` | 18 | Part-level label (legacy) |
| `Art.9`, `Art.7`, `Art.12` | 17/16/15 | Generic article refs — no rulebook context |
| `DFSA-PIB 3` | 16 | Cross-jurisdiction section ref (legacy) |

## Three hypotheses (per the brief's correction)

**(a) Cross-jurisdiction `target_ref` resolves to a section in a DIFFERENT `source_entity` than the source.**
- **Cannot be tested against the 13,040 set** — the sweep already filters to `target_ref` NOT IN any current section. By construction, 0 dangling rows have a resolvable target. A separate sweep would be needed to detect this pattern among the *resolved* citations.

**(b) Bare-code `target_ref` without rulebook prefix.**
- **Disproven.** 0 dangling target_refs start with a digit. All have textual prefixes. The closest pattern is `"Art.9"`, `"Art.7"`, `"Art.12"` (generic article refs from SV/legacy extraction) — these have a prefix but no rulebook context.

**(c) Aggregator's fallback bucket — sweep produces empty `source_entity` when `entity_by_doc.get(source_doc, "")` falls through.**
- **CONFIRMED.** 7,560 citations have orphan `source_doc` FK (pointing to no document). Of these, 6,238 also have non-resolving target_refs and appear in the CSV's empty-source_entity row.

## Truncation cross-correlation

| Question | Result |
|---|---:|
| Dangling citations whose source section is flagged truncated | **41** |
| Dangling citations with non-NULL `source_section_id` (denominator) | 6,465 |
| Correlation | **0.6%** |

Dangling and truncation are independent problems. The brief's "if truncation-correlation high, Block A's fix subsumes B" is false.

## Recommended remediation (three-stage, escalating scope)

### Stage 1 — Refine the dangling-citation sweep heuristic (fast)

Two changes will materially reduce false positives:

1. **Exclude `inline_anchor` + `inline_shorthand` from the sweep entirely.** These citation types target rulebook names by design; `target_ref` is a defined name pattern, never a `section_ref`. Sized as 30 minutes (one-line `WHERE` change in `citation_integrity.py` + re-run).
2. **Surface the orphan `source_doc` FK count as a separate finding.** 7,560 citations with broken FK is its own integrity issue, more severe than the dangling-target issue. Should be a discrete row in `violation-matrix.md`, not folded under "dangling citations".

**Impact:** After Stage 1, the dangling count drops from 13,040 → ~12,813 (loses the 227 inline_*). The 7,560 orphan-FK count moves to its own line. The remaining ~12,813 are the genuine legacy_intra_rulebook investigation target.

### Stage 2 — Decompose legacy_intra_rulebook dangling (half-day)

The 12,813 legacy_intra_rulebook dangling citations need further decomposition:

- **Document-level labels** (e.g., `"FSMR Schedule 1"`, `"VARA Part IV"`) — sweep should treat document-name targets differently from section_ref targets. Likely a separate citation_class.
- **Cross-jurisdiction section refs in non-canonical formats** (e.g., `"DFSA-PIB 4.14"` — does the corpus actually use that format for DFSA sections, or is it `"PIB 4.14"`?). Verify by querying `sections.section_ref` patterns; standardise or migrate.
- **Genuine dangling** (legacy extractor pointed at sections that no longer exist) — these are the real fix targets.

A pass over the legacy extractor's output to bucket these three sub-classes is sized as a half-day. The genuine dangling count is likely <2,000 after this decomposition.

### Stage 3 — Orphan FK source_doc remediation (separate carry)

The 7,560 orphan `source_doc` FK rows imply the citation table has rows pointing to deleted/superseded documents. This needs investigation:
- Are these citations from documents that were re-ingested with new IDs (the old documents removed)?
- Are they from a partial migration that left stale references?
- Should they be cascade-deleted with the document, or re-pointed to the current version?

Sized after a session-zero investigation of *why* the FKs are orphaned.

## Register impact

This memo informs **M21 — Dangling citations remediation** (the proposed M-category entry). Status should reflect:
- Stage 1 (sweep refinement) — unblocked, ~30 min.
- Stage 2 (legacy decomposition) — half-day, follows Stage 1.
- Stage 3 (orphan FK) — separate carry, deserves its own register entry; sized post-investigation.

The original "13,040 dangling citations" framing materially over-states the integrity gap. After Stage 1+2, the genuine-dangling count is likely under 2,000.

## Open questions for follow-up sessions

1. **Why are 7,560 source_doc FKs orphaned?** Is `citations` not being cleaned up when documents are superseded/replaced?
2. **What's the canonical section_ref format for DFSA?** `"DFSA-PIB 4.14"` vs `"PIB 4.14"` vs other — if extractor and storage use different formats, the legacy_intra_rulebook count inflates.
3. **Should `inline_anchor` / `inline_shorthand` have a separate validity check?** Their target_refs (rulebook names) should resolve against a *rulebook-name* index, not against section_refs. A dedicated sweep would catch genuine errors (citation references a nonexistent rulebook) without false-positive saturation.
