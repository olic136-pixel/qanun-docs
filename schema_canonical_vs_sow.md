# C8 — Canonical Schema vs SOW Reference Map

**Date:** 2026-05-12
**Author:** Overnight sprint Claude (Opus 4.7) per `Authorise overnight-sprint-2026-05-11`
**Source of truth:** `/Users/oliver/ADGM/adgm-corpus/corpus.db` (sha256 `344305f05d…`)

## Why this exists

Three rounds of "schema drift correction" within 24 hours during the
overnight sprint and today's A1 work indicates the SOW v3 spec used
column / function names that don't match the deployed corpus.db schema.
Future implementation work needs an authoritative map so no fourth round
is necessary.

---

## Canonical column names (from `corpus.db` `.schema`)

### `documents`

| column           | type                                                     | notes |
|------------------|----------------------------------------------------------|-------|
| `id`             | INTEGER PRIMARY KEY AUTOINCREMENT                        |       |
| `source_key`     | TEXT NOT NULL UNIQUE                                     |       |
| `source_url`     | TEXT NOT NULL                                            | NULL-equivalent `""` allowed |
| `title`          | TEXT NOT NULL                                            |       |
| `doc_type`       | TEXT NOT NULL                                            |       |
| `source_entity`  | TEXT NOT NULL                                            |       |
| `source_tier`    | INTEGER NOT NULL                                         |       |
| `rulebook_code`  | TEXT                                                     |       |
| `version_str`    | TEXT                                                     |       |
| `version_num`    | INTEGER                                                  |       |
| `pub_date`       | TEXT                                                     |       |
| `effective_date` | TEXT                                                     |       |
| `is_current`     | INTEGER DEFAULT 1                                        |       |
| `superseded_by`  | INTEGER REFERENCES documents(id)                         |       |
| `local_path`     | TEXT                                                     |       |
| `content_hash`   | TEXT                                                     | sha256(full_text) post-A1.h |
| `full_text`      | TEXT                                                     | A1.c renamed from SOW `text` |
| `word_count`     | INTEGER                                                  |       |
| `created_at`     | TEXT                                                     |       |
| `updated_at`     | TEXT                                                     | A1.c renamed from SOW `last_updated` |
| `effective_from` | DATE                                                     |       |
| `effective_to`   | DATE                                                     |       |
| `version_id`     | TEXT                                                     |       |
| `authority_tier` | TEXT CHECK IN ('BINDING','GUIDANCE','CONSULTATION','COMMENTARY') | |
| `internal_case_id` | TEXT                                                   | Indexed |

### `sections`

| column           | type                                                     | notes |
|------------------|----------------------------------------------------------|-------|
| `id`             | INTEGER PRIMARY KEY AUTOINCREMENT                        |       |
| `doc_id`         | INTEGER NOT NULL REFERENCES documents(id)                |       |
| `section_ref`    | TEXT NOT NULL                                            |       |
| `section_title`  | TEXT                                                     |       |
| `parent_ref`     | TEXT                                                     |       |
| `level`          | INTEGER                                                  | 0=chapter, 1=rule, 2=sub-rule, 3=provision |
| `text`           | TEXT NOT NULL                                            | A1.c — SOW had `raw_text` here too |
| `page_num`       | INTEGER                                                  |       |
| `effective_from` | DATE                                                     |       |
| `effective_to`   | DATE                                                     |       |
| `version_id`     | TEXT                                                     |       |
| `authority_tier` | TEXT CHECK IN (...)                                      |       |

UNIQUE constraint: `(doc_id, section_ref)`.

### `citations`

| column              | type                                                  | notes |
|---------------------|-------------------------------------------------------|-------|
| `id`                | INTEGER PRIMARY KEY AUTOINCREMENT                     |       |
| `source_doc`        | INTEGER NOT NULL REFERENCES documents(id)             | A1.c — SOW had `source_doc_id` |
| `target_ref`        | TEXT NOT NULL                                         |       |
| `context`           | TEXT                                                  | A1.c — SOW had `raw_text` |
| `source_section_id` | INTEGER REFERENCES sections(id)                       | Indexed |
| `citation_type`     | TEXT                                                  | Indexed; CHECK vocabulary in CLAUDE.md |

UNIQUE constraint: `(source_doc, target_ref, context)`.

---

## SOW → production renames

| SOW spec name                | Production name             | Found in                                    |
|------------------------------|-----------------------------|---------------------------------------------|
| `documents.text`             | `documents.full_text`       | SOW §A1, F1                                 |
| `documents.last_updated`     | `documents.updated_at`      | SOW §A1, F1; reextract docstring (lines 36–41) |
| `documents.doc_title`        | `documents.title`           | SOW §A1                                     |
| `sections.raw_text`          | `sections.text`             | SOW §F1                                     |
| `citations.source_doc_id`    | `citations.source_doc`      | SOW §A1, C2/C3; reextract docstring         |
| `citations.target_doc_id`    | (not present in production — citations are by target_ref only) | SOW §A1 |
| `citations.target_section_id` | (not present — see target_ref) | SOW §A1                                  |
| `citations.kind`             | `citations.citation_type`   | SOW §A1                                     |
| `citations.raw_text`         | `citations.context`         | SOW §A1, C2/C3                              |
| `extract_inline_citations()` | `extract_inline_cross_references()` | SOW §A1 (function signature)         |

Where the SOW name was simply absent in production (e.g.
`target_doc_id`, `target_section_id`), the production schema uses a
single `target_ref` text field — the canonical SOW-style ID-based join
isn't available. Consumers that need to resolve a target reference to
a section must do the lookup at read time via `target_ref`.

---

## Confirmed SOW-spec function signature mismatches

### `extract_inline_cross_references`

```python
# SOW spec (legacy):
extract_inline_citations(text: str, source_doc_id: int, source_entity: str) -> list[dict]

# Production:
extract_inline_cross_references(text: str, source_entity: str, source_rulebook: str | None = None) -> list[InlineCitation]
```

Returns `InlineCitation` dataclasses with `target_ref`, `context`,
`position`, `citation_type` fields. Production is section-scoped (one
section's text → its inline refs); SOW was doc-scoped.

---

## Recommended SOW edits

The SOW lives at `~/qanun-docs/sow/v3/` (path TBC; check for actual
location before applying). Sections that need a search-and-replace:

- **Section A1**:
  - `documents.text` → `documents.full_text`
  - `documents.last_updated` → `documents.updated_at`
  - `documents.doc_title` → `documents.title`
  - `citations.source_doc_id` → `citations.source_doc`
  - `citations.raw_text` → `citations.context`
  - `citations.kind` → `citations.citation_type`
  - `extract_inline_citations` → `extract_inline_cross_references` (with new signature)
  - Drop `citations.target_doc_id` / `target_section_id`; specify how
    consumers resolve `target_ref` → section_id via lookup.
- **Section F1** (frontend/Quick Lookup):
  - `documents.text` → `documents.full_text`
  - `documents.last_updated` → `documents.updated_at`
  - `sections.raw_text` → `sections.text`
- **Sections C2/C3** (citation extraction):
  - `citations.source_doc_id` → `citations.source_doc`
  - `citations.raw_text` → `citations.context`
  - Function rename as above.

For each rename: the SOW should also include the **production** schema
table as an authoritative addendum, so future SOW versions don't drift
again.

---

## Test infrastructure that already enforces production schema

These tests use production column names and would catch a regression:

- `adgm-corpus/tests/test_adgm_rulebooks.py` (current test suite uses
  `full_text`, `updated_at`, etc. throughout)
- `adgm-corpus/tests/test_dfsa_rulebooks.py` (same)
- `adgm-corpus/tests/test_refresh_rulebooks.py` (same)
- `adgm-corpus/scripts/reextract_citations_for_flipped_versions.py`
  (docstring section "Schema notes vs SOW spec" enumerates the corrections — duplicate of this doc)

---

## Forward-looking recommendation

When the SOW is next reissued, add a **"production schema reference"
appendix** that quotes `.schema documents`, `.schema sections`,
`.schema citations` verbatim. The appendix is the source of truth;
any inline section that contradicts it is a known-stale legacy spec.

A lighter alternative: in each SOW section that mentions a column or
function, footnote it with `[see PROD-SCHEMA: documents.full_text]`
so a reader can cross-check without scanning the appendix.

---

## Register

Maps to register item C8.
