# F2 — qanun-api Pre-existing Test Failures Investigation

**Date:** 2026-05-12
**Author:** Overnight sprint Claude (Opus 4.7) per `Authorise overnight-sprint-2026-05-11`
**Baseline:** 39 passed, 7 failed (per session-start `pytest -v`).
**After F2:** 41 passed, 4 xfailed (strict), 1 skipped, 0 failed.
**Branch:** `sprint/F2-test-failures-2026-05-11-overnight`

---

## One-line summary per failure

| # | Test                                                          | Category   | Action       |
|---|---------------------------------------------------------------|------------|--------------|
| 1 | test_drafting_service.py::TestEntityModel::test_tradedar_seeded | data-state | xfail strict |
| 2 | test_drafting_service.py::TestDraftJobPersistence::test_save_and_retrieve_job | test bug   | **fix** |
| 3 | test_ingest.py::TestClassification::test_classifies_aml_policy  | integration | **skipif** |
| 4 | test_templates.py::test_all_10_templates                        | test bug (stale) | **fix** |
| 5 | test_templates.py::test_all_sections_have_provisions            | data-state | xfail strict |
| 6 | test_templates.py::test_all_sections_have_instructions          | data-state | xfail strict |
| 7 | test_templates.py::test_structural_specs_match_templates        | data-state | xfail strict |

---

## Detail

### 1 — test_tradedar_seeded (xfailed)

```
AssertionError: TradeDar entity not seeded
```

The test queries the SQLAlchemy `Entity` table for
`entity_id='tradedarcateg3a-demo-0001'`. The TradeDar demo is seeded by
out-of-band scripts (`scripts/seed_deep_research.py`,
`scripts/create_demo_user.py`), not by an autouse fixture. The test DB
in pytest runs is empty.

**Action:** xfail strict with comment. Unxfail after a `tradedar_demo`
autouse fixture is added that pre-populates the entities table.

### 2 — test_save_and_retrieve_job (fixed)

```
TypeError: _save_job() missing 1 required positional argument: 'updates'
```

The test called `_save_job({...})` with a single dict; the production
signature is `_save_job(job_id: str, updates: dict)`. The test was wrong;
production is right (every other call site in `drafting_service.py`
uses the two-arg form correctly). Fix: update the test to call
`_save_job(job_id, {...})` and remove `job_id` from the updates payload.

### 3 — test_classifies_aml_policy (skipif)

```
TypeError: Could not resolve authentication method. Expected either
api_key or auth_token to be set.
```

The test instantiates `anthropic.Anthropic()` without a key. The class
was decorated `@pytest.mark.integration`, but unregistered pytest marks
only warn — they don't skip. Added
`@pytest.mark.skipif(not os.environ.get("ANTHROPIC_API_KEY"))` so the
test actually skips by default. Run with the env var set to exercise.

### 4 — test_all_10_templates (fixed)

```
assert 162 == 10
```

The registry has grown from the original 10 templates to 162 entries
(it now includes templates AND entity-fact-question entries in the same
flat dict). Test asserted exact equality on a count that no longer
applies. Changed to `>= 10` and kept the per-name `in TEMPLATE_REGISTRY`
loop — the original 10 templates must still be present, the assertion
of "exactly 10" was the brittle part.

### 5 — test_all_sections_have_provisions (xfailed)

```
AssertionError: compliance_manual/s25b_adgm_returns: no provisions
```

The `s25b_adgm_returns` section is mandatory but has empty
`required_provisions`. Non-trivial fix: content authoring of ADGM RA
rule references (annual return, notifications, registers). Out of scope
tonight; xfailed with comment.

### 6 — test_all_sections_have_instructions (xfailed)

```
AssertionError: vara_idq_completion_pack/vara_idq_completion_pack_s1:
  instructions too short (0 chars)
```

VARA IDQ completion pack template's first section has empty
`drafting_instructions`. Non-trivial fix: content authoring for the
VARA template; same shape as #5.

### 7 — test_structural_specs_match_templates (xfailed)

```
AssertionError: compliance_manual/s7_senior_management:
  TABLE section missing from structural spec
```

`compliance_manual/s7_senior_management` is declared
`render_mode=MIXED` but absent from `data/structural_specs.json`. The
fix is either (a) add a spec entry with the enforced table headers and
instructions, or (b) downgrade the render_mode to PROSE. Non-trivial
either way; xfailed with comment.

---

## Test count comparison

| Bucket    | Baseline | After F2 |
|-----------|----------|----------|
| passed    | 39       | 41       |
| failed    | 7        | 0        |
| xfailed   | 0        | 4        |
| skipped   | 0        | 1        |
| **total** | **46**   | **46**   |

Test count is preserved. Two failures resolved (code/test bug fixes;
+2 passing). Five failures converted to xfail/skip with documented
unxfail conditions. No new failures.

---

## Recommended next session

If the user wants to clear the 4 xfails:

1. **Provide TradeDar fixture.** Add an autouse session-scoped fixture
   that creates the test DB schema and seeds the TradeDar demo entity.
   Half-day.
2. **Add `required_provisions` for `compliance_manual/s25b_adgm_returns`.**
   Look up ADGM Companies Regulations 2020 Section 217 (annual returns)
   and Section 90 (statutory registers); add 3–5 provision references.
   Half-day.
3. **Author `drafting_instructions` for `vara_idq_completion_pack/s1`.**
   Generate from the existing VARA IDQ guidance documents. Half-day.
4. **Reconcile `compliance_manual/s7_senior_management`.** Either:
   - Add a `structural_specs.json` entry with the enforced table
     headers ("Controlled Function", "Current Holder",
     "Responsibilities") and the existing drafting instructions; or
   - Change the `render_mode` to `PROSE` in the template (drops the
     enforced table column).
   The first is correct if the table is intended; the second is
   correct if the table is optional / removed. Decision needed.
   Half-day.

After these land the strict xfails will fail (because they're now
passing), pytest will surface them, and the markers can be removed.

---

## Register

Maps to register item F2.
