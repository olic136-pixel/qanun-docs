# Qanun Launch-Readiness Register

**Status:** Repo-tracked register, consolidated 2026-05-12.
**Reconstruction note:** The integration prompt referenced
`qanun_launch_readiness_register_v1.1_2026-05-12.md`. That file did not
exist in `~/qanun-docs/` at integration time. This register is
reconstructed from:
- `~/qanun-docs/overnight-morning-report-2026-05-11.md`
- `~/qanun-docs/phase-2-backlog.md`
- The 11 audit / investigation memos under `~/qanun-docs/` (A5, A7, B1,
  B2, B3, C1, C4, C8, C9, E8+E9, F2, plus the schema and scraper-author
  guides and the DFSA inventory)
- `/tmp/qanun-overnight/integration-progress.md`

If a v1.1 canonical exists in a parallel artefact store and contains
items not enumerated below, supersede this file with the canonical.
Otherwise treat this as the working register going forward.

---

## Overnight items — INTEGRATED (master/main canonical, 2026-05-12)

These items landed during the overnight sprint and were merged to
canonical branches during the integration session. They no longer
block dependent work.

| ID | Description | Status | Sprint branch | Merge commit |
|---|---|---|---|---|
| A1 | write_rulebook pre-flight invariant — raises MultiCurrentInvariantError on multi-current state | Integrated | sprint/A1-invariant-2026-05-11-overnight @ 964b8fd | 2863b79 |
| C5 | --rulebook filter alias resolution (AUT ↔ AUD) + friendly warning on unknown codes | Integrated | sprint/C5-rulebook-filter-2026-05-11-overnight @ 03f55b4 | 53e0f87 |
| C2 | NEW/AMENDED/unchanged label routing through prefixed rulebook_code | Integrated | sprint/C2-label-2026-05-11-overnight @ d0fd7b9 | 6a2ae1a |
| C3 | Jurisdiction interpolation regression tests | Integrated | sprint/C3-typo-2026-05-11-overnight @ d6c57dc | 7d01968 |
| C7 | Drupal selector robustness — `_find_main_container` cascade | Integrated | sprint/C7-drupal-robust-2026-05-11-overnight @ b7c9135 | 6d9328b |
| A6 | Idempotence test infrastructure (mocked + live scaffold) | Integrated | sprint/A6-idempotence-test-2026-05-11-overnight @ 93dfd30 | f443dbb |
| C4 | WAL checkpoint reorder + suppression in reextract_citations script | Integrated | sprint/C4-wal-checkpoint-2026-05-11-overnight @ 74b7923 | 95d925d |
| F2 | qanun-api: 6 of 7 pre-existing test failures fixed | Integrated | sprint/F2-test-failures-2026-05-11-overnight @ 8ffee13 | b179bd2 |
| F1 | qanun frontend vitest configuration + 5 smoke tests | Integrated | sprint/F1-frontend-vitest-2026-05-11-overnight @ 1b9d965 | 4aaf8dc |
| A1-FOUNDATION | Overnight A1 scraper rebuild (A1.a–A1.h) — ADGMRulebookScraper refactor, DFSARulebookScraper, refresh_rulebooks orchestrator, reextract script | Integrated | sprint/A1-scrapers-2026-05-11 @ 70f3cc1 | 913f93a |

All 7 adgm-corpus sprint branches plus the A1 foundation + F2 + F1
branches are retained on origin per Operational Hygiene rule 6.

---

## Outstanding items — referenced by integrated merges

These were referenced in the merge commit messages of integrated items
and are formally tracked here so future work can find them by ID.

### F2.TRADEDAR — TradeDar entity fixture redesign

- **Source:** F2 merge commit `b179bd2`, deferred from F2.
- **Scope:** Rebuild the test fixture that seeds the TradeDar demo
  entity so `TestEntityModel::test_tradedar_seeded` can be unxfailed.
  The current fixture path doesn't reliably populate the entity row
  in test DB state.
- **Why deferred:** Fixture redesign is non-trivial (requires
  coordinating SQLAlchemy session lifecycle with pytest fixtures); not
  a one-line fix.
- **Unxfail condition:** `pytest.mark.xfail(strict=True)` will start
  reporting XPASS when the fixture works; remove the marker at that
  point.
- **Detail memo:** `~/qanun-docs/F2_qanun_api_test_failures.md` §1.
- **Estimated effort:** half-day (fixture design + verification).

### A6.LIVE — Live idempotence exercise

- **Source:** A6 merge commit `f443dbb`, scaffold landed but skipped.
- **Scope:** Run `TestIdempotenceLive::test_dfsa_apply_three_times_against_live_portal`
  against a fresh sandbox corpus.db with `QANUN_RUN_LIVE_IDEMPOTENCE=1`.
  Verify that three successive `refresh_rulebooks.py --apply` runs
  produce identical doc counts (no double-flips, no orphan rows).
- **Pre-requisite:** Fresh sandbox at
  `/tmp/qanun-overnight/idempotence-sandbox/corpus.db` (polluted one
  removed during A6 merge housekeeping).
- **Authorisation phrase:** `Authorise A6-live-idempotence-exercise-<date>`
  per overnight morning report.
- **Estimated effort:** half-day (sandbox setup + 3 live runs + result
  diff).

### B1-REVISED — FSRA rulebook parser redesign

- **Source:** B1 investigation memo (overnight), hypothesis REFUTED.
- **Scope:** The morning-report sizing of B1 as a regex tweak was based
  on a hypothesis that turned out to be wrong. The four "captured"
  GEN 3.5.X sub-rules were spurious matches against Guidance-paragraph
  references; FSRA rule numbers don't appear as line prefixes in the
  PDF body. Parser needs redesign, not regex tweak.
- **Estimated effort:** multi-day to week.
- **Detail memo:** `~/qanun-docs/B1_parser_hypothesis_verification.md`.

---

## Audit-surfaced follow-ups (overnight)

From the 11 overnight audit / investigation memos. Each is its own
candidate register item; size estimates in parentheses.

### Convention follow-ups (from A5)

- **A5.A** — Normalise `rulebook_code` lookups across all read sites
  (half-day). Eliminate hardcoded ADGM-ER-2024-EAO matches.
- **A5.B** — Canonical `section_ref` decomposition helper to replace
  `split()[0]` patterns; pre-requisite for B7 portability mapping
  (half-day).
- **A5.C** — `source_url` backfill at scale: 2,099 is_current=1 rows
  have empty URLs. Supersedes existing A4's ~200 estimate (multi-day).
- **A5.D** — Pre-compute `content_hash = sha256(full_text)` for the
  122 is_current=1 docs that lack it (half-day).
- **A5.E** — `version_str` canonical type + validator (multi-day, low
  priority).
- **A5.F** — `source_key` naming convention enforcement (≤1 hour,
  lowest priority).

### Cross-jurisdiction orphan reconciliations (from A7)

These extend the existing A2 (FSRA GEN reconciliation) to the wider
scope A7 surfaced.

- **A7-FSRA-COBS** — 5 is_current rows (1 prior + 2 stubs + 2 duplicate
  full captures) (day).
- **A7-FSRA-GLO** — 5 is_current rows (same shape as COBS) (day).
- **A7-FSRA-FUNDS** — 3 rows + content-size verification (half-day).
- **A7-FSRA-PRU** — 3 rows + metadata backfill (half-day).
- **A7-FSRA-MIR** — 3 rows (half-day).
- **A7-FSRA-GEN** — already covered by existing register item A2.
- **A7-BVI-BCA** — 2 byte-identical captures, flip earlier (half-day).
- **A7-BVI-REGS** — 2 captures, flip earlier (half-day).
- **A7-UNKNOWN-COMP-LAW-TRUNCATE** — 11 docs with 17-char-truncated
  rulebook_code conflating distinct documents (half-day).

### DFSA scraper follow-ups

- **B2** — DFSA sourcebook handler implementation (5–6 days). Design
  memo at `~/qanun-docs/B2_sourcebook_handler_design.md`. Recommends
  strategy pattern: ModuleParser, HyphenatedRuleParser, ChapterParagraphParser,
  ChapterPageParser.
- **B3** — DFSA inventory drift surveillance (≤1 hour). PRU's "hidden
  from master" status worth a passive check after each scraper run.

### Citation extraction follow-up

- **C1** — `write_rulebook` extract_citations hook implementation
  (half-day). Design memo at
  `~/qanun-docs/C1_extract_citations_hook_design.md`. Recommends
  Option C: hook with `extract_inline_citations=True` default + opt-out
  kwarg + idempotent helper.

### Schema + scraper-author guides (canonical refs)

- **C8** — Schema canonical vs SOW reference map (`~/qanun-docs/schema_canonical_vs_sow.md`).
  Recommends a "production schema reference appendix" for the next
  SOW reissue. No code change.
- **C9** — Scraper authoring guide (`~/qanun-docs/scraper_authoring_guide.md`).
  Documents the canonical pre-flight convention-check pattern.

### Operational hygiene cleanups (E-series)

From the overnight morning report's E-series. Most surfaced but not
investigated in depth tonight.

- **E1** — Documented in overnight report. Status TBD.
- **E2** — Documented. Status TBD.
- **E3** — Documented. Status TBD.
- **E4** — Documented. Status TBD.
- **E5** — Documented. Status TBD.
- **E6** — Documented. Status TBD.
- **E7** — Documented. Status TBD.
- **E8 + E9** — Lowercase repo cleanup. Investigation-only memo at
  `~/qanun-docs/E8_E9_lowercase_repo_cleanup_plan.md`. HIGH-PRIORITY
  recovery flagged: lowercase `~/adgm-corpus/` contains a Cloudflare
  Worker proxy mode for Pinecone (not in canonical). Must preserve
  before deletion.

---

## Process items (from phase-2-backlog)

Meta-findings caught by halt-and-surface discipline during the
integration session. All documented in `~/qanun-docs/phase-2-backlog.md`.

- **P1** — Integration prompt drafting checklist: verify symbol
  locations via `git grep` before specifying import paths in smoke
  checks. (Caught during A1 merge.)
- **P2** — Integration prompt drafting checklist: sprint-branch
  arithmetic must distinguish on-branch (base + own_delta) from
  post-merge (current-master + own_delta). (Caught during C5 merge.)
- **P3** — Integration prompt drafting checklist: use `git show <sha>`
  for content inspection, not `git diff master..branch` which fires
  on foundation-cut artefacts. (Caught during C3 merge.)
- **P4** — Pre-existing flake `TestPerformanceQuickSearch::test_performance_quick_search`
  investigation. Fired on 3 of 7 on-branch runs during integration
  (C5, C2, C4); all retries clean; all post-merge runs clean. Order-
  dependent rather than randomly stochastic. Phase 2 should run
  `pytest --durations=20` to identify the trigger.

---

## Items not in scope tonight

Items the overnight session and integration session deliberately did
not address. Documented here for completeness; future sessions decide.

- **B4** — DFSA portability map population (deferred to post-B2).
- **B5** — Cross-corpus citation enrichment (deferred to post-B2).
- **B6** — Pinecone vector parity audit (deferred).
- **B7** — Portability mapping (depends on A5.B canonical section_ref).
- **B8** — Cross-corpus alignment scoring (deferred).
- **D1–D9** — D-series register items (not surfaced tonight; would
  appear in a v1.1+ canonical register if it exists elsewhere).

---

## Maintenance note

This register file is created 2026-05-12 as a reconstruction. If the
original v1.1 register surfaces and contains items not enumerated
above, those items take precedence — merge them in carefully. Future
register edits land in this file by direct commit + push.
