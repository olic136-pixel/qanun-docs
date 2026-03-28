# MALIS — Build Complete

**Multi-Agent Legal Intelligence System**
**Build Date:** 2026-03-21
**Total Tests:** 392 (391 passing, 1 xfail)
**Phases:** 7 (1, 1b, 2, 3, 3+, 4, 5, 6, 7)

---

## 1. System Overview

MALIS is a multi-agent legal intelligence system built on the ADGM regulatory corpus. It transforms raw regulatory text into structured, traceable legal research output with confidence labels, provenance chains, and an immutable audit trail.

The system supports 5 query types (RESEARCH, SOLUTION_SEEKING, LICENCE_DESIGN, STRESS_TEST, REGULATOR_SIMULATION), 12 pipeline agents, 31 MCP tools, 4 enterprise export formats, an Obsidian knowledge vault, a Digital Twin with continuous monitoring, and a Foreshadowing Engine for anticipating regulatory change.

---

## 2. Build Summary

| Phase | Deliverable | Tests Added |
|-------|-------------|-------------|
| 1 | Metadata migration (SQLite + Pinecone), TemporalFilter | 20 |
| 1b | Claim Registry, Budget Manager, Grounding Validator, Degradation Handler, Audit Logger | 46 |
| 2 | LangGraph pipeline, Orchestrator, Retriever, Analyst | 38 |
| 3 | Devil's Advocate, Blue Sky, RSA, UX Advocate, Guardrail Compiler | 35 |
| 3+ | Stress Tester, RegToTests, Artefacts, 4 MCP tools | 35 |
| 4 | Memory Scribe, Entity Graph, Obsidian Vault, Memory Context | 44 |
| 5 | Task Director, Enterprise Exporters, Complete MCP, Documentation, Acceptance Tests | 69 |
| 6 | Digital Twin, Change Detector, Impact Assessor, Twin Monitor, Scheduler | 57 |
| 7 | Foreshadowing Engine (4 signal types), Quarterly Briefing | 48 |

---

## 3. Complete Component Inventory

### Pipeline Agents (12)
| Agent | Model | Phase |
|-------|-------|-------|
| Orchestrator (triage) | Sonnet | 2 |
| Corpus Retriever | Haiku (reranking) | 2 |
| Legal Analyst | Opus (tool use) | 2 |
| Devil's Advocate | Opus (hard termination: 2 iter / 80k tokens) | 3 |
| Blue Sky Strategist | Opus (SPECULATIVE) | 3 |
| RSA | Opus (extended thinking) | 3 |
| UX/Marketability Advocate | Sonnet | 3 |
| Stress Tester | Opus (extended thinking, 3 dimensions) | 3+ |
| Orchestrator (synthesis) | Opus | 2 |
| Grounding Validator | Deterministic | 1b |
| Memory Scribe | Haiku (NER) | 4 |
| Task Director | Haiku (action items) | 5 |

### MCP Tools (31)
4 stress + 2 memory + 8 core/claims/export/system + 9 twin + 8 corpus = 31

### Enterprise Exports (4)
Word memo, Excel control matrix, Q&A pack, Provenance trace

### Deterministic Tools (3)
Guardrail Compiler, RegToTests Compiler, Artefact Generator

### SQLite Tables (25+)
documents, sections, claims, audit_log, confidence_feedback, session_cache, entity_profiles, relations, reasoning_archives, embedding_cache, matter_logs, product_twins, twin_alerts, twin_assessments, regulatory_changes, foreshadow_signals, + FTS5 virtual tables

---

## 4. Key Architecture Decisions

| Decision | Rationale |
|----------|-----------|
| Direct Anthropic SDK (not LangChain) | Reliable structured output via tool_use; avoids wrapper instability |
| Synchronous pipeline nodes | LangGraph invokes synchronously; async would require ainvoke() throughout |
| Extended thinking two-step pattern | tool_choice incompatible with thinking; Step A thinks, Step B extracts |
| Claims as inter-agent protocol | Prevents hallucination amplification between agents (SOW Section 21.10) |
| DA hard termination (2 iter / 80k tokens) | Unbounded adversarial loops are the most dangerous failure mode |
| Server-side composite scoring for RSA | LLM should not self-score; risk of self-serving bias |
| Heuristic foreshadowing (not ML) | No training corpus available; base rates + adjusters are transparent and auditable |
| Authority tier is jurisdiction-relative | ADGM courts BINDING in ADGM, GUIDANCE in DIFC, and vice versa |
| Quote accumulation prevention | YAML frontmatter compounds quotes on read/write cycles; strip on every operation |

---

## 5. Acceptance Criteria (Section 17)

| Criterion | Status |
|-----------|--------|
| Temporal retrieval accuracy | PASS |
| Authority tiering | PASS |
| Claim traceability | PASS |
| Adversarial termination | PASS |
| Schema enforcement | PASS |
| Audit trail integrity | PASS |
| Degradation handling | PASS |
| Enterprise exports | PASS |
| Performance (quick_search < 2s) | PASS |
| Confidence calibration | XFAIL (requires human review period) |

---

## 6. Known Limitations

| Item | Notes |
|------|-------|
| Confidence calibration | Requires human review period; automated test marked xfail |
| Foreshadowing probabilities | Heuristic only — no trained predictive model |
| Enforcement trends | INSUFFICIENT_DATA with < 3 enforcement actions |
| Quick search | Requires Pinecone API key; returns empty without it |
| Export artefacts | Local disk only; no S3/cloud integration |
| Task Director | No external PM integration (Asana/Linear) |
| Alert escalation | SQLite-only; no email/webhook notifications |
| RBAC | owner_id/matter_id columns present but not enforced |
| Horizon Oracle | Section 15.3 Blue Sky; requires training corpus |

---

## 7. Recommended First Operational Steps

1. Set environment variables: `ANTHROPIC_API_KEY`, `PINECONE_API_KEY`, `VOYAGE_API_KEY`
2. Verify corpus: `sqlite3 corpus.db "SELECT COUNT(*) FROM documents;"`
3. Start MCP servers (intelligence + corpus)
4. Connect Claude Desktop via MCP configuration
5. Run `corpus_status` tool to verify connectivity
6. Run a test query: `mcp_query("What are the custody requirements under ADGM FSMR?")`
7. Create your first product twin: `mcp_create_twin("My Product", "description", {...}, ["ADGM"], ["3A"])`
8. Start the monitoring scheduler for continuous twin monitoring
9. Run `mcp_foreshadow_report(report_type="summary")` to check for signals

---

## 8. Blue Sky Roadmap (Section 15 — Not Built)

| Capability | Difficulty | Prerequisite |
|-----------|-----------|--------------|
| Horizon Oracle (fine-tuned classifier) | HIGH | Training corpus of regulatory outcomes |
| Probabilistic forecasts | HIGH | Horizon Oracle model |
| Interactive foreshadowing dashboard | MEDIUM | Frontend framework |
| Real-time corpus change webhooks | MEDIUM | External notification service |
| Multi-language corpus support | HIGH | Translation pipeline |
| Cross-border twin federation | HIGH | Multi-instance architecture |
| Automated compliance testing (CI/CD) | MEDIUM | Test framework integration |
