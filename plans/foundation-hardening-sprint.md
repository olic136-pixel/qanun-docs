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
