# MALIS Phase 1b Report — Claim Registry + Budget Architecture

**Date:** 2026-03-21
**Phase:** 1b (Claim Registry + Budget Architecture)
**Operator:** Claude (automated), supervised by Oliver Cook KC

---

## 1. Components Built

| File | Component | SOW Section |
|------|-----------|-------------|
| `intelligence_pkg/__init__.py` | Package init | — |
| `intelligence_pkg/agents/__init__.py` | Agents sub-package | — |
| `intelligence_pkg/state.py` | MALISState TypedDict | 4.1 |
| `intelligence_pkg/claims.py` | ClaimModel + ClaimRegistry | 5.1–5.3 |
| `intelligence_pkg/budget.py` | BudgetManager + Compaction + A-RAG Router + Cost Estimator | 6.1–6.4 |
| `intelligence_pkg/grounding.py` | Grounding Validator | 10.1–10.2 |
| `intelligence_pkg/degradation.py` | DegradationHandler (all 10 failure modes) | 6.5 |
| `governance_pkg/__init__.py` | Package init | — |
| `governance_pkg/audit.py` | AuditLogger (hash-chained, immutable) | 7.3 |
| `governance_pkg/confidence_calibration.py` | CalibrationService | 5.4 |

### Test Files

| File | Tests |
|------|-------|
| `tests/intelligence/test_claims.py` | 7 |
| `tests/intelligence/test_budget.py` | 13 |
| `tests/intelligence/test_grounding.py` | 4 |
| `tests/intelligence/test_degradation.py` | 11 |
| `tests/governance/test_audit.py` | 6 |
| `tests/governance/test_calibration.py` | 4 |
| `tests/integration/test_phase1b_integration.py` | 1 |
| `tests/corpus/test_temporal.py` (Phase 1) | 20 |

---

## 2. Test Results

**Total tests written:** 66
**Total passing:** 66
**Total failing:** 0

All tests run against in-memory or temporary SQLite databases — no mocking of the storage layer.

---

## 3. SQLite Tables in corpus.db

| Table | Status | Phase |
|-------|--------|-------|
| documents | Existing (Phase 1 enhanced) | 1 |
| sections | Existing (Phase 1 enhanced) | 1 |
| citations | Existing | Pre-MALIS |
| document_versions | Existing | Pre-MALIS |
| manifest | Existing | Pre-MALIS |
| changes | Existing | Pre-MALIS |
| **claims** | **Rebuilt** — full MALIS schema with 8-tier CHECK, 6 new columns | 1b |
| **session_cache** | Enhanced — added matter_id, owner_id | 1b |
| **entity_profiles** | Enhanced — added confidence, owner_id | 1b |
| **matter_logs** | Enhanced — added owner_id | 1b |
| **relations** | Existing (compatible) | Pre-MALIS |
| **reasoning_archives** | Enhanced — added grounding_result, output_status, owner_id, matter_id | 1b |
| **embedding_cache** | Existing (compatible) | Pre-MALIS |
| **audit_log** | **New** — entry_id, timestamp, session_id, user_id, event_type, event_data, prev_hash, entry_hash | 1b |
| **confidence_feedback** | **New** — feedback_id, claim_id, reviewer_id, rating, notes, created_at | 1b |
| documents_fts / sections_fts | FTS5 virtual tables | Pre-MALIS |

---

## 4. Deviations from SOW Spec

| Item | SOW Spec | Implementation | Rationale |
|------|----------|----------------|-----------|
| Package names | `corpus_pkg`, `intelligence_pkg`, `governance_pkg` | `adgm_corpus` (existing), `intelligence_pkg`, `governance_pkg` | `adgm_corpus` is the established package name; renaming would break existing imports |
| Claim write serialiser | asyncio.Queue | asyncio.Lock (fallback to None in sync) | Queue adds complexity without benefit in single-writer SQLite WAL mode; Lock provides equivalent serialisation |
| A-RAG deep classification | Haiku API call | Regex heuristics | Avoids API dependency in routing; Haiku classification can be added when agents pipeline is built in Phase 2 |
| Compaction Level 1 | Anthropic Compaction API | Haiku summarisation | Compaction API not yet available; Haiku summarisation is the documented fallback |
| `relations` table columns | source_entity_id, target_entity_id | entity_a, entity_b | Kept LEXIS column names to avoid breaking existing code; functionally equivalent |
| `embedding_cache` columns | cache_key, vector, model_name | query_hash, embedding, model | Kept LEXIS column names; functionally equivalent |

---

## 5. Known Limitations / Deferred Items

| Item | Status | Notes |
|------|--------|-------|
| Grounding sentence splitting | Basic regex | SOW mentions nltk.sent_tokenize; current regex handles legal text well. Can upgrade if edge cases appear |
| Compaction Level 1 (Haiku) | Falls through to Level 2 without API key | Works correctly when ANTHROPIC_API_KEY is set |
| A-RAG deep tier | Heuristic only | Full Haiku classification deferred to Phase 2 agent pipeline |
| `owner_id` / `matter_id` | Columns present, not populated | Single-user for now; columns ready for multi-tenancy |
| `datetime.utcnow()` deprecation | Pydantic warning | ClaimModel uses `utcnow()` which is deprecated in Python 3.12+; AuditLogger already uses timezone-aware `datetime.now(UTC)` |

---

## 6. Phase 2 Readiness Confirmation

| Component | Operational | Tests |
|-----------|-------------|-------|
| Claim Registry | YES | 7/7 |
| Budget Manager | YES | 13/13 |
| Grounding Validator | YES | 4/4 |
| Degradation Handler | YES | 11/11 |
| Audit Logger | YES | 6/6 |
| Confidence Calibration | YES | 4/4 |
| Integration (all components) | YES | 1/1 |
| Temporal Filter (Phase 1) | YES | 20/20 |

**All Phase 1b infrastructure is operational. Phase 2 (Core Agent Pipeline) can begin.**
