# MALIS Phase 6 Report — Regulatory Digital Twin

**Date:** 2026-03-21
**Phase:** 6 (Digital Twin: Creation, Monitoring, Alerts, Impact Assessment)
**Operator:** Claude (automated), supervised by Oliver Cook KC

---

## 1. Components Built

| File | Component |
|------|-----------|
| `intelligence_pkg/twin/twin_manager.py` | TwinManager: CRUD, alerts, assessments, diff |
| `intelligence_pkg/twin/change_detector.py` | ChangeDetector: 6-type deterministic classification |
| `intelligence_pkg/twin/impact_assessor.py` | 4-stage impact assessment pipeline |
| `intelligence_pkg/agents/twin_monitor.py` | Twin monitor agent (Sonnet/Opus adaptive) |
| `intelligence_pkg/twin/scheduler.py` | APScheduler monitoring cycle |
| `config/prompts/twin_monitor.yaml` | Twin monitor system prompt |
| `intelligence_pkg/mcp_server.py` | +9 twin MCP tools (31 total) |

### Test Files (6 files, 57 tests)

| File | Tests |
|------|-------|
| `tests/intelligence/twin/test_twin_manager.py` | 14 |
| `tests/intelligence/twin/test_change_detector.py` | 10 |
| `tests/intelligence/twin/test_impact_assessor.py` | 8 |
| `tests/intelligence/twin/test_twin_monitor.py` | 8 |
| `tests/intelligence/twin/test_scheduler.py` | 6 |
| `tests/intelligence/twin/test_mcp_twin_tools.py` | 8 |
| `tests/integration/test_phase6_integration.py` | 3 |

---

## 2. Test Results

**Total tests (all phases):** 345
**Passing:** 344
**xfail:** 1 (confidence calibration — requires human review)
**Failing:** 0
**Regressions from prior phases:** 0

---

## 3. MCP Tool Inventory (31 tools)

| # | Tool | Domain | Status |
|---|------|--------|--------|
| 1 | stress_test_product | Stress | Operational |
| 2 | simulate_regulator | Stress | Operational |
| 3 | regulatory_heat_map | Stress | Operational |
| 4 | test_scenario | Stress | Operational |
| 5 | mcp_memory_search | Memory | Operational |
| 6 | mcp_graph_query | Memory | Operational |
| 7 | mcp_query | Core | Operational |
| 8 | mcp_quick_search | Core | Operational |
| 9 | mcp_claim_lookup | Claims | Operational |
| 10 | mcp_session_info | Claims | Operational |
| 11 | mcp_solve_regulatory | Feature A | Operational |
| 12 | mcp_export_memo | Export | Operational |
| 13 | mcp_status | System | Operational |
| 14 | mcp_provenance_check | Governance | Operational |
| 15 | mcp_create_twin | Twin | Operational |
| 16 | mcp_assess_twin | Twin | Operational |
| 17 | mcp_get_twin_alerts | Twin | Operational |
| 18 | mcp_update_twin | Twin | Operational |
| 19 | mcp_twin_status | Twin | Operational |
| 20 | mcp_twin_diff | Twin | Operational |
| 21 | mcp_foreshadow_report | Twin | Preview (Phase 7) |
| 22 | mcp_resolve_alert | Twin | Operational |
| 23 | mcp_archive_twin | Twin | Operational |
| 24-31 | Corpus MCP (8 tools) | Corpus | Operational |

---

## 4. Digital Twin Lifecycle

1. **Create** → TwinManager.create() with product schema, jurisdictions, licence references
2. **Initial Assessment** → run_twin_monitor() maps regulatory provisions to product features
3. **Continuous Monitoring** → APScheduler scans corpus every hour for changes
4. **Change Detection** → ChangeDetector classifies new/modified documents
5. **Impact Assessment** → 4-stage pipeline: semantic similarity → provision overlap → keyword → citation chain
6. **Alert Generation** → CRITICAL/HIGH/MEDIUM/LOW based on overlap type and change severity
7. **Alert Resolution** → Human reviews and resolves with actions_taken
8. **Regulatory Diff** → Compare twin state between two assessment dates

---

## 5. Change Detection (6 types)

| Type | Classification Logic |
|------|---------------------|
| new_instrument | legislation/rulebook with no prior version in document_versions |
| amendment | legislation/rulebook WITH prior version |
| consultation | doc_type contains 'consultation' or title contains 'Consultation Paper' |
| guidance | doc_type in guidance/circular/policy_statement |
| enforcement | doc_type is enforcement_notice |
| soft_signal | Everything else (speeches, blogs, press releases) |

---

## 6. Impact Assessment (4 stages)

| Stage | Method | Alert Level if Hit |
|-------|--------|--------------------|
| 1. Semantic Similarity | Pinecone cosine (≥0.7 threshold) | LOW |
| 2. Provision Overlap | Section_ref match against twin regulatory_map | HIGH (CRITICAL if amendment) |
| 3. Keyword Cross-Reference | Change terms in product_schema | MEDIUM |
| 4. Citation Chain | Citations table traversal | MEDIUM |

---

## 7. APScheduler Configuration

| Job | Interval | Description |
|-----|----------|-------------|
| corpus_change_scan | Every 1 hour | Detects new/modified documents, runs impact assessment |
| twin_assessment_cycle | Every 24 hours | Full reassessment for up to 10 ACTIVE twins |

Throttling: max 10 twins per cycle. Priority: unresolved alerts first, oldest assessment second.

---

## 8. Known Limitations

| Item | Notes |
|------|-------|
| Foreshadowing | Preview only — stub returns pending signal count. Full engine in Phase 7 |
| Semantic similarity (Stage 1) | Requires Pinecone + Voyage AI; falls back to 0.0 without embedder |
| Cross-border twin | Single jurisdiction per assessment cycle; multi-jurisdiction requires separate twins |
| Alert escalation | No email/webhook notification — alerts stored in SQLite only |

---

## 9. Phase 7 Readiness

| Component | Operational |
|-----------|-------------|
| Twin lifecycle (create/assess/alert/resolve) | YES |
| Change detector (all 6 types) | YES |
| Impact assessor (4 stages) | YES |
| Twin monitor agent (Sonnet/Opus adaptive) | YES |
| APScheduler monitoring cycle | YES |
| All 31 MCP tools | YES (1 preview) |
| foreshadow_signals table | YES (created, empty) |
| Integration tests | YES (3/3) |
| Zero regressions | YES (344/344 + 1 xfail) |
