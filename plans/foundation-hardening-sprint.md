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
