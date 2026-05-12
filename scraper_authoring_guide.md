# Scraper authoring guide — Qanun corpus

**Status:** Authoritative pattern guide for `adgm_corpus/collection/scrapers/*`.
Last update: 2026-05-12 (C9 deliverable).

---

## Why this guide exists

Today's A1.b/A1.f/A1.g/A1.h bugs all shared a shape: a scraper assumed
a corpus convention that wasn't actually enforced by the schema. The
production data had drifted from the assumed convention, and the
scraper silently produced data that matched the *old* convention. The
result: silent corruption, surfaced only when downstream consumers
broke or invariants tripped.

This guide encodes the patterns those bugs taught us, so future scraper
authors don't repeat them.

---

## The core pattern — pre-flight convention check

**Rule.** Before inserting rows with TEXT fields where the "right
value" is a convention encoded in data rather than enforced by schema
(e.g., prefixed/bare rulebook codes, section_ref shapes, version_str
formats), the scraper MUST:

1. Query the existing distinct values for the field, scoped to its
   target slice (e.g., `source_entity = ?`).
2. Confirm the new value matches the dominant convention OR is a
   deliberate, documented extension.
3. If neither, halt and raise a descriptive error — the convention
   has drifted and a human needs to decide.

### Reference implementation — `write_rulebook` invariant

The A1 invariant landed today (`sprint/A1-invariant-2026-05-11-overnight`)
is the canonical example for the **single-current** convention:

```python
def write_rulebook(conn, doc: dict, diff: dict | None = None) -> int:
    # A1 pre-flight invariant. Done BEFORE any UPDATE/INSERT — the
    # function must be a no-op when the invariant fails so the operator
    # can audit without a half-written transaction in the WAL.
    current_rows = conn.execute(
        "SELECT id, version_str, source_url FROM documents "
        "WHERE source_entity = ? AND rulebook_code = ? AND is_current = 1",
        (doc["source_entity"], doc["rulebook_code"]),
    ).fetchall()
    if len(current_rows) > 1:
        offending = ", ".join(
            f"id={r[0]} (version_str={r[1]!r}, source_url={r[2]!r})"
            for r in current_rows
        )
        raise MultiCurrentInvariantError(
            f"write_rulebook pre-flight invariant violated for "
            f"source_entity={doc['source_entity']!r} "
            f"rulebook_code={doc['rulebook_code']!r}: "
            f"expected 0 or 1 is_current=1 rows, found {len(current_rows)}. "
            f"Offending rows: {offending}. "
            f"Refusing to write — upstream corpus state needs reconciliation."
        )
    # … rest of write …
```

Why this works:
- **Done first**, before any state mutation. A failure leaves the DB
  unchanged.
- **Descriptive error**. The operator gets the offending IDs, their
  version_str, and their source_url — enough to start reconciling
  without re-running.
- **Source-entity scoped**. Doesn't trip on unrelated rows in the
  same table.

### Where else this pattern should live

Apply the same shape for:

- **rulebook_code convention** — before inserting a doc, check whether
  the new value matches the dominant prefix convention for the
  `source_entity` (per A5.A proposal). DFSA → prefixed `DFSA-COB`;
  FSRA → bare `COB`. Halt if a new entity introduces a third convention.
- **section_ref shape** — before bulk-inserting sections, verify the
  shape matches the existing convention for the doc's `(source_entity,
  rulebook_code)`. Halt if any section_ref shape differs.
- **version_str format** — before INSERT, verify `version_str` matches
  the entity's known regex (`VER\d+\.\d+` for FSRA, `VER\d+-\d+` for
  DFSA). Halt on mismatch.
- **content_hash** — verify `content_hash == sha256(full_text)` at
  INSERT time (A1.h fix). Halt on mismatch (would catch a scraper
  that hashes raw bytes again).

---

## Scraper-author checklist

When writing or reviewing a new scraper (FSRA, DFSA, BVI, El Salvador,
Panama, future jurisdictions), confirm each item:

### A. Field convention

- [ ] What is the existing convention for **rulebook_code** in this
  source_entity? `SELECT DISTINCT rulebook_code FROM documents WHERE source_entity = '<entity>'`.
  Bare or prefixed? Document the choice.
- [ ] Same for **section_ref**: does the existing data use
  `<CODE> X.Y` or `<CODE>-X.Y` or `<CODE> Section X`?
- [ ] **source_url**: does the scraper capture a non-empty URL for
  every is_current=1 doc it emits?
- [ ] **content_hash**: is it computed from `full_text` (not raw HTML
  bytes — see A1.h)?
- [ ] **version_str**: does it match the entity's known format
  regex?
- [ ] **source_key**: lowercase snake_case, version-stamped, UNIQUE.

### B. Invariants

- [ ] The scraper's `upsert_rulebook` (or equivalent) routes through
  `write_rulebook` so the A1 single-current invariant applies.
- [ ] If the scraper writes other tables (e.g., citations, sections),
  the same pre-flight pattern is applied for those tables' implicit
  conventions.

### C. State assumptions

- [ ] The scraper does NOT assume a fixed corpus state (e.g., "the
  prior doc must exist", "the rulebook must be in MODULE_URLS"). It
  branches on actual lookup results and halts cleanly when assumptions
  fail. (A1.g was exactly this class of bug — the existence check used
  the wrong key and silently routed to NEW.)
- [ ] The scraper is idempotent: running twice against unchanged
  upstream produces zero DB writes. (A6 test infrastructure exists for
  this — `tests/test_idempotence_refresh.py::TestIdempotenceMocked`.)

### D. Error handling

- [ ] Network failures, parse failures, and small full_text results
  are HARD failures. The scraper does NOT commit a stub row with
  empty `version_str` and tiny `full_text` and `is_current=1`.
  (A7 found 6 cases of this pattern in FSRA from a 28-April + 2-May
  re-run.)
- [ ] On a failed extraction (e.g., `full_text` under N KB for what
  should be a substantial rulebook), the scraper logs the failure
  and exits, leaving the prior is_current=1 row untouched.

### E. Tests

- [ ] Three regression tests per branch: NEW path, AMENDED path,
  unchanged path. The unchanged path asserts ZERO writes.
- [ ] One regression test per convention assumption: e.g., "AMENDED
  with prefixed convention" (per C2), "filter resolves alias both
  pre- and post-resolve" (per C5), "Drupal layout drift resilient"
  (per C7).
- [ ] If the scraper uses an external service, the network test is
  guarded by an env var (e.g., `QANUN_RUN_LIVE_FOO=1`) and **skipped
  by default**. `@pytest.mark.network` alone is documentation, not a
  skip; pytest only warns on unregistered marks. See
  `tests/test_idempotence_refresh.py::TestIdempotenceLive` for the
  pattern.

### F. Logging + observability

- [ ] Log every fetch with the URL, response size, and parse result
  count. (Helps post-hoc audit of "did this rulebook actually get
  data?".)
- [ ] When upserting, log the (source_entity, rulebook_code,
  rows_affected) tuple. (Helps audit-trail of "what changed in this
  refresh run?".)

---

## What NOT to do — anti-patterns from today's bugs

1. **Don't assume a convention based on what the SOW says.** The SOW
   may be out of date. The corpus.db schema (`.schema documents`) is
   the source of truth for fields and types; the data itself
   (`SELECT DISTINCT …`) is the source of truth for value conventions.
2. **Don't lookup with a bare code when the data uses a prefixed code**
   (or vice versa). The A1.g bug. Always normalise before lookup, or
   build the lookup key from the same source that produced the data.
3. **Don't hash raw HTML bytes when Drupal-style framing markup will
   differ per request.** A1.h. Hash the extracted `full_text` instead.
4. **Don't filter on the literal SOW code when an alias map exists.**
   C5. Match against both the SOW code and the post-alias form so
   `--rulebook AUT` and `--rulebook AUD` both work.
5. **Don't commit a stub row with empty version_str and tiny
   full_text.** A7. Treat short extractions as failures.
6. **Don't trust `pytest.mark.<custom>` to skip tests.** Use
   `@pytest.mark.skipif(env_check, reason=…)` to actually guard
   tests that need authorisation.

---

## Latent-convention search — quick check before writing

When picking up an existing scraper to extend, run this query first to
see what conventions you'll be perpetuating:

```sql
SELECT
  source_entity,
  rulebook_code,
  COUNT(*) AS docs,
  GROUP_CONCAT(DISTINCT version_str) AS version_str_samples,
  COUNT(CASE WHEN source_url = '' OR source_url IS NULL THEN 1 END) AS empty_url
FROM documents
WHERE source_entity = '<your-entity>'
GROUP BY source_entity, rulebook_code
ORDER BY docs DESC
LIMIT 20;
```

The output tells you:
- Which `rulebook_code` shape the entity uses
- The `version_str` formats already present (canonical + outliers)
- How many docs lack a source_url (informs whether the scraper needs
  to capture URLs more aggressively)

---

## Related register items

- **A1** — write_rulebook invariant (the reference implementation here).
- **A5.A / A5.B** — normalise rulebook_code + section_ref lookups.
- **A5.C** — source_url backfill.
- **A5.D** — content_hash assertion on INSERT.
- **A6** — idempotence test infrastructure.
- **A7** — cross-jurisdiction invariant audit (where multi-current
  orphans hide).
- **C7** — Drupal selector robustness pattern.

---

## Register

Maps to register item C9.
