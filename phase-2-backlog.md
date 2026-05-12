# Phase 2 Backlog

Items surfaced during the post-overnight integration session and other
sources that are NOT actioned immediately but should land in a future
session.

---

## Process items

### Integration prompt drafting checklist — verify symbol locations

**Source:** A1 master integration merge, 2026-05-12.

Verify symbol locations before specifying import paths in smoke checks.
The A1 master integration prompt assumed
`MultiCurrentInvariantError` would live in `adgm_corpus.storage.db`
(conceptually a storage invariant); the actual location is
`adgm_corpus.collection.scrapers.adgm_rulebooks` (next to
`write_rulebook`). Future integration prompts should grep for the
symbol on the source branch before specifying its import path, rather
than guessing based on conceptual placement.

Suggested checklist for the next integration prompt:

```
# Before specifying any "from X import Y" smoke check:
git checkout <sprint-branch>
grep -rn "class Y\b\|^def Y\|^Y =" <package>/ | head
# Use the discovered path in the prompt.
```

---

## Test infrastructure

### Pre-existing flake — `TestPerformanceQuickSearch::test_performance_quick_search`

**Source:** Overnight morning report 2026-05-11; reconfirmed during
C5 master integration on 2026-05-12.

The test `tests/acceptance/test_section_17.py::TestPerformanceQuickSearch::test_performance_quick_search`
fails when run as part of the full suite but passes reliably in
isolation. Behaviour during C5 integration:

- Full-suite run #1: failed.
- Isolated runs (×2): both passed in ~3.5 s.
- Full-suite run #2: passed.

Likely causes:

- Timing assumption with insufficient wall-clock leeway (the test
  asserts a latency budget that the full suite's preceding resource
  contention pushes past).
- Shared resource contention (DB connections, file handles).
- Test-order dependency (a preceding test leaves state that the
  performance assertion is sensitive to).

**Phase 2 investigation plan:**

1. Run `pytest --durations=20 tests/acceptance/` to find what runs
  immediately before the perf test in the failing case.
2. Profile the perf test's runtime characteristics in both modes
  (isolated vs full-suite-position) to identify the deterministic
  trigger.
3. Fix the deterministic trigger if surfaced (likely cleanup in a
  preceding test fixture, or a hardcoded latency threshold that
  needs widening with documented justification).
4. Failing fix: mark `@pytest.mark.flaky` or xfail-strict with a
  documented unxfail condition.

**Not blocking any specific feature work.** Contaminates every
full-suite run including future integration sessions, requiring
re-run-once discipline per the C5 decision pattern.

---

## Integration prompt drafting checklist — sprint-branch arithmetic

**Source:** C5 master integration merge, 2026-05-12.

When sprint branches are all cut from a common base that isn't the
current master, the prompt's expected on-branch test count must be
"base-baseline + own-delta", not "current-master + own-delta". The
post-merge count on master IS "current-master + own-delta". Both
numbers should appear in the prompt's verification matrix.

The A1 master integration prompt conflated these for C5 (specified
662 as the on-branch count when it should have been 659; 662 is the
post-merge count).

Future integration prompts that involve sprint branches with a
common pre-master base should construct the verification table the
way the corrected C5-through-C4 table is constructed: one column for
on-branch (constant base-baseline + own delta), one column for
post-merge (running cumulative).

Example table shape:

```
  Step  Branch  On-branch         Post-merge        Cumulative on master
  ────  ──────  ─────────────     ──────────────    ────────────────────
  C5    sha     base + own_delta  master + own_delta  …
  C2    sha     base + own_delta  master + own_delta  …
  ...
```

Both gates run; both matter; both have specific expected values.
A failure at either is a halt-and-surface.
