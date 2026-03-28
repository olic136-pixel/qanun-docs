# MALIS Phase 1 Migration Report

**Date:** 2026-03-21
**Migration:** LEXIS → MALIS Phase 1 (Metadata Migration & Gap Close)
**Operator:** Claude (automated), supervised by Oliver Cook KC

---

## 1. Pre-Migration State (Audit Baseline)

### SQLite corpus.db (184 MB)
| Table | Rows |
|-------|------|
| documents | 2,484 |
| sections | 63,397 |
| citations | 13,337 |
| document_versions | 80 |

### Pinecone "lexis-corpus" Index
- **Vectors:** 58,984 (namespace: `default`)
- **Dimension:** 1024 (voyage-law-2)
- **Metric:** Cosine, Serverless AWS us-east-1

### Missing MALIS Fields (Pre-Migration)
| Field | Status |
|-------|--------|
| `effective_from` | MISSING |
| `effective_to` | MISSING |
| `version_id` | MISSING |
| `authority_tier` | MISSING |
| `content_hash` | Present (documents, document_versions) |
| `source_tier` | Present (1/2/3 numeric) |

---

## 2. Changes Made

### Step 1 — Authority Tier Mapping (confirmed)

Mapping from `source_tier` + `source_entity` to MALIS `authority_tier`, ADGM perspective:

| source_tier | source_entity | authority_tier | Count |
|-------------|---------------|----------------|-------|
| 1 | FSRA | BINDING | 333 |
| 1 | ADGM_COURTS | BINDING | 261 |
| 1 | DFSA | BINDING | 21 |
| 1 | DIFC | BINDING | 5 |
| 1 | EL_SALVADOR | COMMENTARY | 18 |
| 2 | FSRA | GUIDANCE | 643 |
| 2 | EL_SALVADOR | COMMENTARY | 3 |
| 2 | DFSA | COMMENTARY | 3 |
| 3 | DIFC_COURTS | GUIDANCE | 1,188 |
| 3 | CLIFFORD_CHANCE | COMMENTARY | 4 |
| 3 | NORTON_ROSE | COMMENTARY | 3 |
| 3 | MONDAQ | COMMENTARY | 2 |

**Key design decision:** Authority tier is jurisdiction-relative. ADGM courts are BINDING in ADGM but GUIDANCE in DIFC, and vice versa. El Salvador has no bearing on ADGM/DIFC. The static column stores the ADGM perspective; runtime queries can flip tiers via the `TemporalFilter.jurisdiction` parameter.

### Step 2 — Schema Migration (additive only)

Added 4 columns to each of `documents` and `sections`:

```sql
ALTER TABLE documents ADD COLUMN effective_from DATE;
ALTER TABLE documents ADD COLUMN effective_to DATE;
ALTER TABLE documents ADD COLUMN version_id TEXT;
ALTER TABLE documents ADD COLUMN authority_tier TEXT CHECK(authority_tier IN ('BINDING','GUIDANCE','CONSULTATION','COMMENTARY'));
-- (same 4 columns on sections)
```

No columns dropped, no data truncated.

### Step 3 — Backfill Current Documents

| Sub-step | Field | Documents Updated | Sections Updated |
|----------|-------|-------------------|------------------|
| 3A | effective_from | 2,484 | 63,397 |
| 3B | effective_to | 2,484 (set NULL) | 63,397 (set NULL) |
| 3C | version_id (UUID v5) | 2,484 | 63,397 |
| 3D | authority_tier | 2,484 | 63,397 |

**Anomaly:** Only 2 of 2,484 documents had `effective_date` populated. For the remaining 2,482, `effective_from` was set from `created_at` (corpus ingest date: 2026-03-15 to 2026-03-21). This is a known approximation — true legislative effective dates should be backfilled when available.

### Step 4 — Historical Versions (Bi-Temporal)

**No-op.** All 2,484 documents have `is_current = 1`. The 80 `document_versions` rows are single-capture snapshots from the same ingest date with no actual version chains. Zero superseded documents exist.

### Step 5 — Pinecone Metadata Upsert

Two-pass approach (no re-embedding):

| Pass | Strategy | Vectors Updated | Failures | Time |
|------|----------|-----------------|----------|------|
| Pass 1 | Section-based chunk_index matching | 24,329 | 0 | 324s |
| Pass 2 | doc_id-based lookup (all vectors) | 58,984 | 0 | 776s |

All 58,984 vectors now carry: `effective_from`, `effective_to`, `authority_tier`, `version_id`.

### Step 6 — Chunk Gap Analysis

**No gap.** All 2,484 documents are represented in Pinecone (58,984 vectors). The difference between 58,984 Pinecone vectors and 63,397 SQLite sections is because the ingestion pipeline uses `chunk_legal_document()` which produces different-sized chunks than the section parser. These are different granularities, not missing data.

### Step 7 — Historical Version Indexing

**No-op.** Zero `is_current=0` documents exist. The `adgm-historical` Pinecone namespace was not created (it will be created automatically when superseded documents are ingested in future).

### Step 9 — MALIS Temporal Filter Module

Created `adgm_corpus/temporal.py` implementing `TemporalFilter` class:

- Current mode + as-of-date mode
- Pinecone filter generation (namespace-aware)
- SQLite WHERE clause generation (FTS5 fallback)
- Authority tier filtering (combinable with temporal)
- Jurisdiction-aware tier resolution (ADGM/DIFC perspectives)

**Tests:** 20 tests in `tests/corpus/test_temporal.py` — all passing.

---

## 3. Final State

### SQLite Field Coverage

| Table | Total | effective_from | effective_to | version_id | authority_tier |
|-------|-------|----------------|--------------|------------|----------------|
| documents | 2,484 | 2,484 (100%) | 0* | 2,484 (100%) | 2,484 (100%) |
| sections | 63,397 | 63,397 (100%) | 0* | 63,397 (100%) | 63,397 (100%) |

*`effective_to = NULL` for all records — correct, as all are currently in force.

### Authority Tier Distribution (Documents)

| Tier | Count |
|------|-------|
| BINDING | 620 |
| GUIDANCE | 1,831 |
| COMMENTARY | 33 |

### Pinecone Vector Counts

| Namespace | Vectors |
|-----------|---------|
| default | 58,984 |
| adgm-historical | 0 (not yet created) |
| **Total** | **58,984** |

### Temporal Logic Verification

- is_current=1 records with effective_to set: **0** (correct)
- is_current=0 records missing effective_to: **0** (correct)

---

## 4. Anomalies & Known Limitations

1. **effective_from approximation:** 2,482 of 2,484 documents use `created_at` (ingest date) as `effective_from` because `effective_date` was not populated at ingest time. True legislative effective dates should be backfilled from source metadata.

2. **No historical versions:** The corpus currently has zero superseded documents. Bi-temporal queries will become functional once the ingestion pipeline captures version transitions.

3. **Pinecone chunks ≠ SQLite sections:** The ingestion pipeline re-chunks documents using `chunk_legal_document()`, producing 58,984 chunks from 63,397 sections. This is by design — the chunker optimises for embedding quality. Both data sources are complete.

4. **Pinecone NULL handling:** Pinecone cannot filter on NULL values. For `effective_to`, empty string `""` represents "currently in force". The `TemporalFilter` class handles this by using namespace separation (default = current, adgm-historical = superseded) rather than NULL filtering.

---

## 5. Outstanding Items

| Item | Status | Action Required |
|------|--------|-----------------|
| True effective dates | Pending | Backfill from ADGM source metadata when available |
| Historical versions | N/A | Will populate as documents are updated over time |
| CONSULTATION tier | Unused | No consultation papers currently in corpus; tier is reserved |
| adgm-historical namespace | Not created | Auto-creates when first superseded doc is indexed |

---

## 6. Files Created/Modified

| File | Action |
|------|--------|
| `adgm-corpus/corpus.db` | 4 columns added to `documents`, 4 to `sections`; all rows backfilled |
| `adgm_corpus/temporal.py` | NEW — TemporalFilter class |
| `tests/corpus/test_temporal.py` | NEW — 20 unit tests |
| `scripts/generate_version_ids.py` | NEW — UUID v5 generation |
| `scripts/migrate_pinecone_metadata.py` | NEW — Pinecone metadata patcher (pass 1) |
| `scripts/migrate_pinecone_pass2.py` | NEW — Pinecone metadata patcher (pass 2, doc_id-based) |
| `scripts/find_missing_docs.py` | NEW — Gap analysis script |
| `scripts/check_pinecone_final.py` | NEW — Final verification script |
| `docs/migration_report.md` | NEW — This report |

---

## 7. Confirmation

The ADGM regulatory corpus is now **MALIS Phase 1 compliant**:

- All documents and sections carry `effective_from`, `effective_to`, `version_id`, and `authority_tier`
- All 58,984 Pinecone vectors carry the same 4 MALIS metadata fields
- The `TemporalFilter` module supports current-state and as-of-date queries with authority tier and jurisdiction filtering
- Bi-temporal infrastructure is in place and will activate when historical versions are captured

**Phase 1b (Claim Registry + Budget Architecture) can begin.**
