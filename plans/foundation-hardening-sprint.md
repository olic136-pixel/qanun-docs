# Foundation Hardening Sprint

**Date:** 15 May 2026
**Decision:** Path A (Foundation Hardening before scope expansion) over Path B (ADGM-only-v1 scope cut)
**Rationale:** 15 May 2026 audit established write-side integrity gates are 1 of 8 layers built; output-side anti-fabrication is the only fully-robust layer. Gates once built are permanent infrastructure; not re-done per jurisdiction. Reversible if sprint exceeds 3 weeks.

## Acceptance gate

No scope expansion until all Waves A–E close. Specifically deferred:

- M23, M24
- J-category (templates), K-category (commercial), L-category (E2E validation)

Parallel-OK during sprint:

- F6 (TemplateDiscoveryAgent test isolation)
- Frontend UI work not depending on corpus shape changes

## Waves

| Wave | Sessions | Existing register items |
|---|---|---|
| A — Write-path gates | 5 | A1-content-hash-aware-invariant, A7-FSRA-source-URL-dedup, A7-FSRA-cross-entry-point-dedup, A7-FSRA-content-sniff-classifier, A7-FSRA-pipeline-size-sanity |
| B — Parser consistency | 4 | A5.A, A5.B, A5.D, A5.E |
| C — source_url backfill | 2–3 | A5.C, A5.C.1 |
| D — Citation integrity | 4–5 | M22, M21 (Stage 1 + Stage 2), C1 |
| E — Parser determinism | 2–3 | B1 (determinism sub-concern) |

**Total: 17–22 bounded sessions, ~2–3 weeks.**

## Sequencing

- A ‖ B (different files, different concerns)
- C after A (source_url dedup gate before backfill)
- D after B (section_ref decomposition feeds citation target resolution)
- E independent

## Tracking

Per-wave status updates land in the register against each item's `Status:` field. This memo establishes scope and the acceptance gate only; the register is the source of truth. First Wave A session opens with a `corpus_status()` check and a register read-through.

## Lessons during the sprint

Lessons surfaced during Wave A sessions. Captured here rather than as separate
register entries because they apply to remaining-wave session discipline,
not to register-tracked deliverables.

### Pre-flight pytest baselines on pollution-prone code

Session 2 surfaced a process trap: running the pytest baseline at Step 2(e)
*before* fixing F6 polluted the working tree with the very artefacts that
F6's fix prevents. Subsequent post-fix verification then saw the leftover
pollution and chased it as an apparent regression. The fix had worked from
iteration 1; the appearance of failure was a baseline artefact.

Mitigation for remaining Wave A/B/C/D/E sessions: when the session work is
a bug fix whose test gate is the bug itself (the F6 family — bugs that
contaminate working state during pytest), either (a) clean the working tree
between baseline and verification with `git checkout -- .` and a
targeted `rm -rf` of known-polluted paths, or (b) skip the pre-fix
baseline and treat the post-fix run as authoritative. Document which
approach was taken in the session paste-back.

### Memory #21 caught a near-miss commit

During Session 2's diagnostic detour, an over-broad `find … | xargs rm -rf`
deleted test files that had been recovered by `git checkout -- tests/ ucie/`
— but the recovery also wiped Part A edits. After re-applying, the first
commit attempt staged the deletions of `lexis/tests/*` alongside the
intended Part A files. Caught by `git status` review before the commit
landed, recovered with `git reset --soft HEAD~1` + `git restore --staged`
+ `git checkout --`. Published master is clean.

The discipline that prevented bad code reaching origin: explicit-path
`git add` (Memory #21 in operational hygiene), never `git add -A` in
adgm-corpus. Future Wave sessions retain this discipline.

## Wave A — complete (15 May 2026)

Wave A closed in 5 register items + parallel-OK F6 across one extended CCD
day (Sessions 1, 2, 3a, 3b, 4 plus register touches 1.5, 2.5, 3b.5, 4.5):

| Item | Code session |
|---|---|
| A1-content-hash-aware-invariant | Session 1 |
| A7-FSRA-cross-entry-point-dedup | Session 1 (subsumed into data-layer gate) |
| A7-FSRA-source-URL-dedup | Session 1 (scope broadened to universal write-path) |
| A7-FSRA-pipeline-size-sanity | Session 2 Part B |
| A7-FSRA-content-sniff-classifier | Session 3b |
| A8-WRITE-PATH-COVERAGE | Session 4 |
| F6 (parallel-OK) | Session 2 Part A |

Structural shape post-Wave-A: all corpus write operations route through
`insert_document` → `assert_write_invariants` → Gates 1, 2, 4 (Gate 3
size-floor in `write_rulebook`). AST-scan meta-test prevents future
bypass; `add_jurisdiction.py` Step 16 validates signature registration
per jurisdiction.

Status-at-a-Glance table refresh + per-family aggregation methodology
documentation: separate housekeeping session immediately following Wave A
closure.

Wave B opens next: combined A5.A + A5.D + A5.E session, then standalone
A5.B (canonical `section_ref` decomposition).

## Wave B — complete (15-17 May 2026)

Wave B closed in 4 register items across 2 code sessions + 2 register
touches (Sessions 1, 2 plus 1.5, 2.5):

| Item | Code session |
|---|---|
| A5.A — normalise_rulebook_code helper | Session 1 |
| A5.D — content_hash compute in write_rulebook | Session 1 |
| A5.E — version_str per-entity validator | Session 1 |
| A5.B — canonical section_ref decomposition | Session 2 |

Structural shape post-Wave-B: parser-side write path now has consistent
canonicalisation. `insert_document` routes rulebook_code through
`normalise_rulebook_code` before invariant gates fire. `write_rulebook`
derives `content_hash` from `full_text` (canonical going forward).
`assert_write_invariants` Gate 5 validates `version_str` against
per-entity regex patterns. The new `adgm_corpus.storage._section_ref`
module provides single-source-of-truth decomposition of section_ref
strings across 11 format shapes coexisting in the corpus.

Three xfail-strict global tests now sit on the test suite tracking
calibration gaps from Wave A and B (Memory #25 pattern, three instances):
content_hash collisions (8 rows), content-sniff signature gaps (15
ADGM_RA-F rows), version_str outlier (1 FSRA row — `VER10311025`,
appears to be malformed `VER10.311025` missing the dot). Worth a future
Wave A+ refinement session addressing all three in one pass.

Wave B sprint pacing came in well under the memo's "4 sessions" estimate
— A5.A/D/E combined into one Session 1 (small, mechanical, all in
`storage/db.py`); A5.B as standalone Session 2 (architectural, expanded
from 5 to 11 formats after Step 2 discovery surfaced legacy shapes).

Carries surfaced during Wave B:
- qanun-api consumer refactor (2 sites at `services/change_detection_service.py:54, 200`)
  pending a cross-repo Python sharing decision
- A5.B unknown-sample pattern refinement candidates (DFSA `CMC 1`, BVI
  multi-word) — global coverage is ≥95% but not 100%

Wave C opens next: source_url backfill (A5.C + A5.C.1). 2-3 interactive
sessions per the memo. Wave D drafting (queue-format pilot via O1 V1)
can begin in parallel; Wave D execution waits on Wave C closure.
