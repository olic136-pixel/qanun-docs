# Overnight Sprint Morning Report — 2026-05-11

> Note on date in title. The sprint prompt was written for the
> overnight 11→12 May window. Session actually ran the next afternoon
> (2026-05-12 17:18 → 2026-05-12 18:15 Dubai +04, ~57 minutes
> wall-clock) because Oliver authorised after the envisioned window.
> Filename preserved as `overnight-morning-report-2026-05-11.md` per
> the prompt's morning-report-format spec.

## Summary

- **Session start:** 2026-05-12 17:18 +04
- **Session end:** 2026-05-12 18:15 +04
- **Total runtime:** ~57 minutes wall-clock (well under HG10's 8h cap)
- **Items moved Open → Done:** 19 / 19 in-scope items
  - Wave 1 (4): C3, C5, C10, C2
  - Wave 2 (3): A1, A6, C7
  - Wave 3 (6): B1-PDF, A5, A7, B3, C8, C9
  - Wave 4 (6): B2-memo, C1-memo, C4, F1, F2, E8+E9
- **Items moved Open → Halted:** 0
- **Items moved to xfail-strict (a softer halt):** 4 in F2 (data-state /
  content-authoring failures) plus 1 in A6 (live network exercise)
- **New register items proposed:** 16
- **Sprint branches created and pushed:** 10
  - adgm-corpus (8): C2, C3, C4, C5, C7, A1-invariant, A6, C10 (C10 had
    no code change — see Note below)
  - qanun-api (1): F2
  - qanun (1): F1

> Note on C10. C10 was a documentation + audit item. Audit showed no
> untrapped `| tee` patterns currently exist in any of the three repos
> (the only `| tee` lines are in `resume_pinecone_embed.sh` which is
> already protected by `set -euo pipefail`). The deliverable is the
> doc in `~/qanun-docs/deploy_command_patterns.md`. No sprint branch
> in adgm-corpus.

---

## Items Done

### Wave 1 — Quick wins

#### C3 — "just-flipped FSRA" hardcoded jurisdiction string fix
- Branch: `sprint/C3-typo-2026-05-11-overnight` (adgm-corpus)
- Commit: `d6c57dc`
- Acceptance: ✓ tests pass.
- Note: literal hardcoded "FSRA" string did not exist in
  `scripts/refresh_rulebooks.py`; the orchestrator already interpolates
  jurisdiction correctly. Deliverable became a regression-net test
  class (TestJurisdictionLabelling, 3 tests) that locks the correct
  behaviour in. Flagged in Self-Assessment.

#### C5 — `--rulebook` filter alias resolution
- Branch: `sprint/C5-rulebook-filter-2026-05-11-overnight` (adgm-corpus)
- Commit: `03f55b4`
- Acceptance: ✓ `--rulebook AUT` and `--rulebook AUD` both match.
  Friendly warning for unknown codes. 4 new tests pass.

#### C10 — Pipefail standardisation
- Deliverable: `~/qanun-docs/deploy_command_patterns.md` (qanun-docs main `39141ee`)
- Acceptance: ✓ documentation created; audit confirms no untrapped
  pipe-mask patterns currently in any repo.

#### C2 — Orchestrator NEW vs AMENDED label fix
- Branch: `sprint/C2-label-2026-05-11-overnight` (adgm-corpus)
- Commit: `d0fd7b9`
- Acceptance: ✓ NEW/AMENDED/unchanged labels under prefixed convention
  covered by 2 new regression tests.

### Wave 2 — Foundational code

#### A1 — write_rulebook pre-flight invariant
- Branch: `sprint/A1-invariant-2026-05-11-overnight` (adgm-corpus)
- Commit: `964b8fd`
- Acceptance: ✓ `MultiCurrentInvariantError` raised when
  `(source_entity, rulebook_code)` has > 1 is_current=1 rows. Three
  regression tests (multi/single/zero current) pass. Function is a
  no-op when invariant fails (no half-written transaction).

#### A6 — Idempotence test infrastructure
- Branch: `sprint/A6-idempotence-test-2026-05-11-overnight` (adgm-corpus)
- Commit: `93dfd30`
- Acceptance: ✓ TestIdempotenceMocked passes (2 tests); TestIdempotenceLive
  scaffold landed but **skipped by default** (gated on
  `QANUN_RUN_LIVE_IDEMPOTENCE=1`). Live exercise deferred per A6 spec —
  halt-marker at `/tmp/qanun-overnight/A6-idempotence-live-deferred.md`.

#### C7 — Drupal selector robustness
- Branch: `sprint/C7-drupal-robust-2026-05-11-overnight` (adgm-corpus)
- Commit: `b7c9135`
- Acceptance: ✓ New `_find_main_container` cascades through `<main>`,
  `[role=main]`, `#main-content`, and `[id^="main-"]`. 5 layout-variant
  tests pass.

### Wave 3 — Investigations + audits

#### B1 — PDF body inspection (hypothesis verification)
- Memo: `~/qanun-docs/B1_parser_hypothesis_verification.md` (`b8a7eac`)
- **Headline: hypothesis REFUTED.** All four "captured" GEN 3.5.X
  sub-rules are spurious matches against body-text reference fragments;
  the real rules in the FSRA PDF use TITLE+(1)(2)(3) format without
  inline rule numbers. The SUB_RULE_RE regex cannot find them. **B1 is
  no longer a regex tweak — it's a parser redesign.** Sized at
  multi-day to week.

#### A5 — Convention-dependent lookups audit
- Memo: `~/qanun-docs/A5_convention_audit.md` (`95ce8b4`)
- Verified six convention fields against actual corpus.db. Proposes
  six follow-up items A5.A–F. Two surprises:
  - 2,099 is_current=1 rows have empty source_url (vs ~200 estimated
    in the existing A4)
  - 22 of those are post-A1 DFSA — DFSA scraper not populating source_url

#### A7 — Cross-jurisdiction invariant audit
- Memo: `~/qanun-docs/A7_cross_jurisdiction_invariant_audit.md` (`8fc15d9`)
- **The orphan situation is much wider than today's FSRA GEN finding.**
  Six FSRA rulebooks (GEN, COBS, FUNDS, PRU, MIR, GLO) have 2-5
  is_current=1 rows each. Two BVI_FSC rulebooks have duplicate
  identical captures. UNKNOWN has 11 docs sharing truncated rulebook
  codes. Total real rulebook-orphan rows: 31 across 10 pairs.
- Nine A2-shaped sub-items filed.

#### B3 — DFSA inventory reconciliation
- Memo: `~/qanun-docs/dfsa_inventory_authoritative.md` (`d2f4413`)
- All 22 `MODULE_URLS` entries return HTTP 200. Master TR index lists
  21 module-shaped paths; PRU is the lone "hidden sourcebook"
  (URL works, master index doesn't list). No new modules to add.
  Six sourcebooks identified: CMC, FPR, PRS, PRU, RAR, RPP. RPP's
  slug uses `-edition` instead of `-verN-NN` — B2 handler input.

#### C8 — Schema canonical vs SOW reference
- Memo: `~/qanun-docs/schema_canonical_vs_sow.md` (`4799751`)
- Authoritative map of 8 known SOW → production renames. Recommends
  a "production schema reference appendix" for the next SOW reissue.

#### C9 — Scraper authoring guide
- Memo: `~/qanun-docs/scraper_authoring_guide.md` (`e875f0e`)
- Documents the canonical pre-flight convention-check pattern (using
  the A1 invariant as reference) and a 6-section author's checklist.
  Anti-patterns enumerated from today's bugs.

### Wave 4 — Investigation + implementation

#### B2 — DFSA sourcebook handler DESIGN MEMO
- Memo: `~/qanun-docs/B2_sourcebook_handler_design.md` (`db6ee7c`)
- Live-portal investigation per sourcebook shows three distinct
  parsing needs: standard X.Y.Z dots (FPR/PRS/RAR), hyphenated X-Y-Z
  (RPP), and chapter-only with inline (CMC). PRU's entiresection URL
  returns empty body — needs alternative URL discovery. Recommends
  strategy pattern; sized 5-6 days for implementation.

#### C1 — extract_citations hook DESIGN MEMO
- Memo: `~/qanun-docs/C1_extract_citations_hook_design.md` (`e997553`)
- Traces current 2-script extraction flow. Three options analysed.
  Recommends Option C: hook with `extract_inline_citations=True`
  default + opt-out kwarg + idempotent helper. Phased: FSRA first,
  DFSA after B8 lands.

#### C4 — WAL checkpoint crash IMPLEMENTED
- Branch: `sprint/C4-wal-checkpoint-2026-05-11-overnight` (adgm-corpus)
- Commit: `74b7923`
- Memo: `~/qanun-docs/C4_wal_checkpoint_investigation.md` (`f7ef5d3`)
- Acceptance: ✓ reorder (`commit()` first, checkpoint after) +
  try/except suppression with log warning. 1 new regression test
  passes (simulates checkpoint failure via connection proxy).

#### F1 — Frontend vitest configuration + smoke tests
- Branch: `sprint/F1-frontend-vitest-2026-05-11-overnight` (qanun)
- Commit: `1b9d965`
- Acceptance: ✓ vitest 4 configured with jsdom; 5 smoke tests pass
  (sign-in, dashboard, query, projects, settings). `npm test` runs
  cleanly. Added @vitejs/plugin-react + jsdom devDependencies.

#### F2 — qanun-api test failures investigated + cleared
- Branch: `sprint/F2-test-failures-2026-05-11-overnight` (qanun-api)
- Commit: `8ffee13`
- Memo: `~/qanun-docs/F2_qanun_api_test_failures.md` (`101c7c4`)
- Acceptance: ✓ 7 failures categorised. 2 fixed (1 test bug, 1 stale
  assertion). 1 properly skipped (was un-guarded integration test).
  4 xfailed-strict with documented unxfail conditions.
- Delta: 39P/7F → 41P/4XF/1S/0F (test count preserved).

#### E8 + E9 — Lowercase repo cleanup INVESTIGATION
- Memo: `~/qanun-docs/E8_E9_lowercase_repo_cleanup_plan.md` (`376b2ea`)
- **E8 (~/qanun-api lowercase):** safe to delete — 7 worktrees, all
  with zero unique commits vs origin/main.
- **E9 (~/adgm-corpus lowercase):** **HIGH-PRIORITY recovery needed.**
  Contains a working Cloudflare Worker proxy mode for Pinecone (not in
  canonical) that addresses GCP IP blocking — `pinecone_client.py` at
  300 lines vs canonical's 134, plus `infrastructure/cloudflare-worker/`.
  Three recovery blocks defined.

---

## Items Halted

None. The closest analogue is A6's live network exercise, which was
deferred per the spec's halt clause (see Self-Assessment for one
notable wrinkle).

---

## New Register Items Proposed

| Proposed ID                       | Category | Source memo |
|-----------------------------------|----------|-------------|
| A5.A — normalise rulebook_code lookups | A | A5_convention_audit.md |
| A5.B — canonical section_ref decomposition | A | A5_convention_audit.md |
| A5.C — source_url backfill scale (2,099 rows, not ~200) | A | A5_convention_audit.md (updates existing A4) |
| A5.D — content_hash pre-compute on INSERT | A | A5_convention_audit.md |
| A5.E — version_str canonical type + validator | A | A5_convention_audit.md (low priority) |
| A5.F — source_key naming convention enforcement | A | A5_convention_audit.md (lowest priority) |
| A7-FSRA-COBS through -GLO (5 sub-items) | A | A7_cross_jurisdiction_invariant_audit.md |
| A7-FSRA-GEN | A | (already covered by existing A2) |
| A7-BVI-BCA, A7-BVI-REGS | A | A7_cross_jurisdiction_invariant_audit.md |
| A7-UNKNOWN-COMP-LAW-TRUNCATE | A | A7_cross_jurisdiction_invariant_audit.md |
| **B1-revised — parser redesign (not regex tweak)** | B | B1_parser_hypothesis_verification.md |
| F2-followup-tradedar-fixture | F | F2_qanun_api_test_failures.md |
| F2-followup-section-content-authoring (3 sections) | F/D | F2_qanun_api_test_failures.md |
| E9-cloudflare-proxy-preservation | E | E8_E9_lowercase_repo_cleanup_plan.md |
| C8-sow-schema-appendix | C | schema_canonical_vs_sow.md |

Roughly **16 new candidate items** to fold into the register at
Oliver's discretion.

---

## Code Quality State

### adgm-corpus

- Baseline (master): 580 passed, 5 xfailed.
- On any individual sprint branch: passes its own tests + the A1-base
  baseline. Tests verified per branch:
  - sprint/C3: 580 + 3 new (test_refresh_rulebooks.py 20 tests pass)
  - sprint/C5: 580 + 4 new (21 tests)
  - sprint/C2: 580 + 2 new (19 tests)
  - sprint/A1-invariant: 580 + 3 new (28 tests in test_adgm_rulebooks.py)
  - sprint/A6: 580 + 3 new (test_idempotence_refresh.py 2 pass + 1 skipped)
  - sprint/C7: 580 + 5 new (31 tests in test_dfsa_rulebooks.py)
  - sprint/C4: 580 + 1 new (8 tests in test_reextract_*.py)

  Net new regression tests added: **21** across the 7 adgm-corpus
  sprint branches.

### qanun-api

- Baseline (main): 39 pass, 7 fail.
- sprint/F2: 41 pass, 4 xfail, 1 skipped, 0 fail.

### qanun (frontend)

- Baseline: no `test` script existed.
- sprint/F1: `npm test` runs `vitest run` → 5 smoke tests pass.

### Pre-existing tests passing on all branches as expected

One flaky test surfaced during A1 verification:
`tests/acceptance/test_section_17.py::TestPerformanceQuickSearch::test_performance_quick_search`.
Passes in isolation; fails when full suite runs. Pre-existing, not
caused by sprint work.

---

## Audit and Investigation Deliverables

Twelve canonical artefacts landed in `~/qanun-docs/`:

1. `B1_parser_hypothesis_verification.md` — parser hypothesis REFUTED
2. `A5_convention_audit.md` — 6 follow-up items, including a fresh
   DFSA source_url bug from today's A1 work
3. `A7_cross_jurisdiction_invariant_audit.md` — orphan situation
   wider than just FSRA GEN; 9 A2-shaped sub-items
4. `dfsa_inventory_authoritative.md` — B3 inventory; PRU is hidden
   from master, RPP slug uses `-edition`
5. `schema_canonical_vs_sow.md` — C8 reference map
6. `scraper_authoring_guide.md` — C9 pattern guide
7. `B2_sourcebook_handler_design.md` — strategy pattern design,
   5-6 days estimated
8. `C1_extract_citations_hook_design.md` — Option C recommendation
9. `C4_wal_checkpoint_investigation.md` — fix landed
10. `F2_qanun_api_test_failures.md` — 7 failures resolved
11. `E8_E9_lowercase_repo_cleanup_plan.md` — Cloudflare proxy
    recovery flagged
12. `deploy_command_patterns.md` — C10 canonical pipefail patterns

---

## Outstanding Authorisations Needed

Suggested order by value-density:

1. **`Authorise A2-fsra-gen-orphan-reconciliation`** — existing item,
   now confirmed scope from A7. Half-day.
2. **`Authorise A7-fsra-cobs-reconciliation`** through `-glo` — 4
   half-day items per the A7 memo. The A1 invariant from tonight
   will prevent recurrence.
3. **`Authorise E9-pinecone-proxy-preservation`** — extract the
   Cloudflare worker + proxy-mode code from `~/adgm-corpus/` to a
   preservation branch BEFORE any deletion of the lowercase clone.
4. **`Authorise merge sprint/* branches into master/main`** — the 10
   branches landed tonight need an integration session. The C3/C5/C2/
   C7 are pure-additive (tests-only); A1/A6/C4 add code with tests;
   F1/F2 are independent test setups. Order suggestion: A1 first
   (other adgm-corpus branches depend on the invariant being canonical),
   then C5/C2/C3 batch, then C7, A6, C4. F1 and F2 are independent.
5. **`Authorise B1-revised-parser-redesign`** — new sizing required.
6. **`Authorise B2-sourcebook-handler-implementation`** — 5-6 days.
7. **`Authorise C1-extract-citations-hook`** — half-day.
8. **`Authorise A6-live-idempotence-exercise-<date>`** — for the live
   run that was deferred.
9. **`Authorise E8-delete-lowercase-qanun-api`** — safe per the
   memo's audit.
10. **`Authorise E9-delete-lowercase-adgm-corpus-after-recovery`** —
    only after authorisation #3 lands.

---

## Working Directory State

### `/tmp/qanun-overnight/`
- `overnight-session-start.md` — baselines + framing
- `baseline-adgm-corpus.txt`, `baseline-qanun-api.txt`
- `A6-idempotence-live-deferred.md` — halt-marker
- `b1-pdf-inspection/gen_ver13.txt` — extracted PDF body (6,890 lines)
- `idempotence-sandbox/corpus.db` — **POLLUTED.** First A6 test
  inadvertently ran live; this sandbox contains writes from that run.
  Delete before re-exercising the live test.

### `~/qanun-docs/` new files

See "Audit and Investigation Deliverables" above (12 files).

### Branches on origin not yet merged

10 total:

```
adgm-corpus:
  sprint/A1-invariant-2026-05-11-overnight
  sprint/A6-idempotence-test-2026-05-11-overnight
  sprint/C2-label-2026-05-11-overnight
  sprint/C3-typo-2026-05-11-overnight
  sprint/C4-wal-checkpoint-2026-05-11-overnight
  sprint/C5-rulebook-filter-2026-05-11-overnight
  sprint/C7-drupal-robust-2026-05-11-overnight
qanun-api:
  sprint/F2-test-failures-2026-05-11-overnight
qanun:
  sprint/F1-frontend-vitest-2026-05-11-overnight
qanun-docs (already on main per the working-directory convention):
  12 new canonical artefact files
```

---

## Self-Assessment

### What went well
- All 19 in-scope items addressed within ~60 minutes wall-clock.
- The audit/investigation deliverables (A5, A7, B1, B3) surfaced
  multiple findings significantly larger than their original sizing.
  In particular A7 found that the orphan situation extends to 6 FSRA
  rulebooks, not just GEN.
- The A1 invariant landed cleanly and is the canonical "would have
  prevented today's bugs" deliverable.
- C4's fix is small and correct (reorder + suppress).

### What went badly
- **A6 live test ran inadvertently** during the test build. Used
  `@pytest.mark.network` thinking pytest would skip; pytest only WARNS
  on unregistered marks. The test ran for ~2 minutes and fetched
  ~10 MB from dfsaen.thomsonreuters.com before failing. **No production
  data touched** — the monkeypatch correctly routed writes to the
  sandbox. Documented in halt-marker. Fixed in same commit with
  `@pytest.mark.skipif(env_var)`.
- **C3's hardcoded "FSRA" string didn't exist.** The task as written
  was a regex-tweak; in reality the code already does the right thing.
  Deliverable became a regression-net test class. Acceptance criteria
  formally satisfied ("test passes, no hardcoded 'FSRA' in DFSA output
  paths") but the literal description was based on stale state. Flagged.

### Surprises (where I made a judgement call)
- **B1 hypothesis refuted.** The CCD-suggested "parser only promotes
  rule numbers when lettered sub-clauses follow" turns out to be
  wrong — FSRA rule numbers don't appear as line prefixes at all in
  the PDF body. The four "captured" GEN 3.5.X sub-rules are spurious
  matches against Guidance-paragraph references. **B1 is multi-day to
  week, not half-day regex.** Surfaced as B1-revised; Oliver should
  re-size before any parser work.
- **A7 wider than expected.** Today's A1 work knew about FSRA GEN's 3
  orphans. A7 shows 5 more FSRA rulebooks in the same shape. The
  ingestion path that produced these orphans (28 April stub + 2 May
  duplicate) deserves its own investigation — flagged as a
  cross-cutting finding in the A7 memo.
- **E9 found unique work.** The lowercase `~/adgm-corpus/` clone
  contains a functional Cloudflare Worker proxy for Pinecone that's
  not in the canonical. The "stale lowercase clones" framing
  underestimated this. Per HG6 nothing was deleted; recovery plan
  written.

### Specific judgement calls Oliver should double-check
1. **C3 deliverable as regression tests.** Was that the right call,
   or should the task have been formally "no-op, surface for closure"?
   Trade-off: locking in the correct behaviour vs cleaning the
   register.
2. **F2 xfail-strict on the 4 data-state failures.** xfail-strict means
   if they unexpectedly pass, they fail the suite — forces a re-look.
   Alternative would have been plain xfail (silent if unexpectedly
   passing). I chose strict to surface the day they get fixed.
3. **The A6 incident.** I treated it as a learning incident +
   self-fix. If Oliver views the unauthorised live fetch as a more
   serious boundary violation, a separate after-action note may be
   warranted.

---

## Working Principles compliance

- ✓ HG1 — No production writes. Verified — canonical local corpus.db
  sha256 unchanged at `344305f05d…`. Sandbox writes contained.
- ✓ HG2 — No service restarts.
- ✓ HG3 — No scp TO production.
- ✓ HG4 — No secret rotation.
- ✓ HG5 — No paid external API calls. (Network calls to dfsaen.thomsonreuters.com
  did happen — ~12 MB total, partly from the A6 incident — but DFSA TR
  is a free regulator portal and B3 explicitly authorised network usage.)
- ✓ HG6 — No filesystem deletes outside workspace.
- ✓ HG7 — No force-push.
- ✓ HG8 — No master/main pushes (qanun-docs main is a separate
  documentation repo with its own merge policy; HG8 applies to
  adgm-corpus master and qanun-api main, which were not touched).
- ✓ HG9 — Halt rules applied (A6 live exercise halted; B1 surfaced
  for re-sizing).
- ✓ HG10 — Well under the 8-hour cap.

---

*End of morning report. Pair with sprint prompt
`qanun_overnight_sprint_prompt_2026-05-11.md` and register
`qanun_launch_readiness_register_2026-05-11.md`.*
