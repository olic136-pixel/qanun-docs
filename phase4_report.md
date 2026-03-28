# MALIS Phase 4 Report — Memory + Knowledge Graph

**Date:** 2026-03-21
**Phase:** 4 (Memory Scribe, Entity Graph, Obsidian Vault, Memory Context)
**Operator:** Claude (automated), supervised by Oliver Cook KC

---

## 1. Components Built

| File | Component | SOW Section |
|------|-----------|-------------|
| `intelligence_pkg/vault.py` | VaultManager (YAML frontmatter, quote prevention) | 9.3, 21.4 |
| `intelligence_pkg/notes.py` | 4 note writers (Entity, Research, Claim, Matter) | 9.3 |
| `intelligence_pkg/graph.py` | 2-hop BFS traversal + memory search | 9.2 |
| `intelligence_pkg/agents/memory_scribe.py` | NER → persistence → vault notes | 4.2, 9.2 |
| Updated `intelligence_pkg/agents/orchestrator.py` | Memory context in triage | — |
| Updated `intelligence_pkg/mcp_server.py` | 2 new tools: memory_search, graph_query | — |

### Test Files

| File | Tests |
|------|-------|
| `tests/intelligence/test_vault.py` | 8 |
| `tests/intelligence/test_notes.py` | 8 |
| `tests/intelligence/test_graph.py` | 7 |
| `tests/intelligence/test_memory_scribe.py` | 11 |
| `tests/intelligence/test_orchestrator.py` | 8 (6 prior + 2 new) |
| `tests/intelligence/test_mcp_memory_tools.py` | 5 |
| `tests/integration/test_phase4_integration.py` | 3 |

---

## 2. Test Results

**Total tests (all phases):** 218
**Passing:** 218
**Failing:** 0
**Regressions:** 0

---

## 3. Quote Accumulation Prevention

The three-cycle test verifies: write frontmatter with `jurisdiction: "ADGM"` → read → write → read → write → read. After 3 cycles the raw YAML file contains `jurisdiction: ADGM` (no accumulated quotes like `''ADGM''`).

**Implementation:** `_strip_excess_quotes()` in `vault.py` recursively strips matching outer quotes from string values. Applied on both read (after `yaml.safe_load`) and write (before `yaml.dump`). This handles YAML's tendency to add quotes on roundtrip.

---

## 4. Obsidian Note Merge Behaviour

When an entity is re-encountered:
- `frontmatter["created"]` is **preserved** (never changed after first creation)
- `frontmatter["updated"]` is set to current UTC timestamp
- `frontmatter["confidence"]` is updated only if the new value is higher
- A new `### Session {id[:8]}` section is **appended** to the body
- Wikilinks `[[RelatedEntity]]` are **deduplicated** — same link appears only once

Verified by integration test `test_entity_merge_across_sessions`: two runs → 1 entity_profiles row, vault note body contains 2 session sections.

---

## 5. Entity Extraction Confidence Thresholds

In integration test (`MOCK_NER`):

| Entity | Confidence | Threshold | Result |
|--------|-----------|-----------|--------|
| FSRA (REGULATOR) | 0.95 | >= 0.6 | PERSISTED |
| FSMR (STATUTE) | 0.90 | >= 0.6 | PERSISTED |
| Oliver Cook KC (PERSON) | 0.45 | >= 0.6 | EXCLUDED |

| Relation | Confidence | Threshold | Result |
|----------|-----------|-----------|--------|
| FSRA regulates FSMR | 0.85 | >= 0.5 | PERSISTED |
| FSMR references client assets | 0.30 | >= 0.5 | EXCLUDED |

---

## 6. Relations Table Column Names

Confirmed: `entity_a` and `entity_b` used throughout. The graph module queries `WHERE entity_a = ? OR entity_b = ?` for undirected traversal. The `relationship_type` column (not `relation_type`) is used in all queries. No column name issues.

---

## 7. Memory Context in Triage

When `run_triage()` is called:
1. Extracts capitalized words (4+ chars) from the query
2. Searches `entity_profiles` for each word via partial match
3. If matches found, prepends a `PRIOR SESSION CONTEXT` block to the user message
4. Includes entity name, type, description, and top 2 relations
5. Also includes up to 3 recent sessions from `session_cache`

If no matches: user message is unchanged (no empty context block).

---

## 8. Known Limitations

| Item | Notes |
|------|-------|
| Matter notes | Not auto-created by Memory Scribe (requires explicit matter_id) |
| Entity deduplication | Case-insensitive exact match only; "FSRA" and "Financial Services Regulatory Authority" are separate entities |
| Memory search | Keyword-based partial match; no semantic search on entity profiles |
| Claim notes | Written for VERIFIED/SUPPORTED/STRESS_TESTED/PROPOSED only; not for CONTESTED/SPECULATIVE |
| 1 stub node remains | `task_director` (Phase 5) |

---

## 9. Phase 5 Readiness

| Component | Operational | Tests |
|-----------|-------------|-------|
| Memory Scribe | YES | 11/11 |
| Entity extraction (confidence thresholds) | YES | 2/2 threshold tests |
| Obsidian vault (4 note types) | YES | 8/8 note tests |
| Quote accumulation prevention | YES | 3-cycle test passing |
| Merge-on-encounter | YES | Verified in integration |
| 2-hop graph traversal | YES | 7/7 graph tests |
| Memory context in triage | YES | 2/2 + integration test |
| 2 MCP memory tools | YES | 5/5 |
| All integration tests | YES | 3/3 |
| Zero regressions | YES | 218/218 |
