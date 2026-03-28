# MALIS Phase 2 Report — Core Agent Pipeline

**Date:** 2026-03-21
**Phase:** 2 (Core Agent Pipeline: Orchestrator, Corpus Retriever, Legal Analyst)
**Operator:** Claude (automated), supervised by Oliver Cook KC

---

## 1. Components Built

### New Files

| File | Component | SOW Section |
|------|-----------|-------------|
| `intelligence_pkg/pipeline.py` | LangGraph StateGraph with full topology | 4.3 |
| `intelligence_pkg/prompts.py` | PromptLoader (YAML-based, jurisdiction-aware) | — |
| `intelligence_pkg/agents/orchestrator.py` | run_triage (Sonnet) + run_synthesis (Opus) | 4.2 |
| `intelligence_pkg/agents/retriever.py` | 3-tier retrieval (FTS5/Pinecone/Deep) | 4.2, 6.2 |
| `intelligence_pkg/agents/analyst.py` | Legal analysis with claim registration | 4.2, 5.1 |
| `config/prompts/orchestrator_triage.yaml` | Triage system prompt | 4.2 |
| `config/prompts/orchestrator_synthesis.yaml` | Synthesis system prompt | 4.2 |
| `config/prompts/analyst.yaml` | Legal Analyst system prompt | 4.2 |
| `config/prompts/retriever.yaml` | Reranking system prompt | 4.2 |
| `tests/corpus/golden_questions/adgm.json` | 5 golden questions (1 negative control) | 10.3 |

### Modified Files

| File | Change |
|------|--------|
| `intelligence_pkg/claims.py` | Fixed `datetime.utcnow()` → `datetime.now(timezone.utc)` |
| `intelligence_pkg/pipeline.py` | Wired real agents for triage/retriever/analyst/synthesizer nodes |

### Test Files

| File | Tests |
|------|-------|
| `tests/intelligence/test_pipeline_topology.py` | 8 |
| `tests/intelligence/test_prompts.py` | 5 |
| `tests/intelligence/test_orchestrator.py` | 6 |
| `tests/intelligence/test_retriever.py` | 6 |
| `tests/intelligence/test_analyst.py` | 5 |
| `tests/intelligence/test_golden_questions.py` | 7 |
| `tests/integration/test_phase2_integration.py` | 1 |

---

## 2. Test Results

**Total tests (all phases):** 104
**Passing:** 104
**Failing:** 0

---

## 3. Deviations from SOW Spec

| Item | SOW Spec | Implementation | Rationale |
|------|----------|----------------|-----------|
| Anthropic SDK | Not specified | Direct SDK (not LangChain wrappers) | More reliable structured output via tool use; SOW Section 21.8 warns about Settings bugs |
| A-RAG deep reranking | Haiku LLM reranking call | Deduplication + score-based ordering | LLM reranking deferred to when full Pinecone is available in tests; infrastructure ready |
| FTS5 query cleaning | Not specified | Stop word removal + OR joining | FTS5 requires content words only; question phrases ("What are the...") fail without cleaning |
| Pipeline stubs_only mode | Not specified | Added `stubs_only` parameter to `build_graph()` | Enables topology testing without API dependencies (SOW Section 21.17) |
| Async agents | SOW mentions `async def` | Sync `def` (no `await`) | LangGraph invokes nodes synchronously; async would require `ainvoke()` throughout. Can be upgraded in Phase 3 if needed |

---

## 4. System Prompt Design Decisions

**Orchestrator Triage:**
- Strict JSON-only output via tool use enforcement — no freeform text allowed
- Query type taxonomy exactly matches SOW: RESEARCH, SOLUTION_SEEKING, LICENCE_DESIGN, STRESS_TEST, REGULATOR_SIMULATION
- As-of date detection included per SOW Section 4.1

**Legal Analyst:**
- Strongest constraint: "There are no unregistered assertions" — forces every claim through the registry
- Three-tier confidence (VERIFIED/SUPPORTED/INFERRED) — analyst cannot assign CONTESTED/SPECULATIVE/PROPOSED
- Cross-reference and temporal duties explicitly required
- Negative assertion duty: must say "I cannot find" rather than fabricate

**Corpus Retriever:**
- Reranking prompt focuses on relevance assessment only — no legal analysis
- Jurisdiction-specific priority: FSRA rulebooks > comparator materials

---

## 5. Known Limitations

| Item | Notes |
|------|-------|
| Deep tier LLM reranking | Infrastructure ready but uses score-based ordering without Haiku call in current tests |
| Async execution | Nodes are synchronous; can upgrade to async in Phase 3 |
| 8 stub nodes | devils_advocate, blue_sky, rsa, ux_advocate, stress_tester, grounding_validator_node, memory_scribe, task_director remain stubs |
| Golden questions | 5 of target 20 implemented; remaining 15 for Phase 3 |
| Voyage embedder | Passed as dependency injection; not auto-initialized from settings |

---

## 6. Phase 3 Readiness Confirmation

| Component | Operational | Tests |
|-----------|-------------|-------|
| LangGraph graph compiles | YES | 8/8 topology tests |
| Orchestrator (triage + synthesis) | YES | 6/6 |
| Corpus Retriever (3-tier) | YES | 6/6 |
| Legal Analyst (claim registration) | YES | 5/5 |
| Golden question smoke tests | YES | 7/7 |
| End-to-end mocked pipeline test | YES | 1/1 |
| **All Phase 1+1b+2 tests** | **YES** | **104/104** |

**Phase 3 (Devil's Advocate + Blue Sky + RSA + remaining agents) can begin.**
