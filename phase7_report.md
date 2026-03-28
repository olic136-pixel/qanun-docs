# MALIS Phase 7 Report — Foreshadowing Engine

**Date:** 2026-03-21
**Phase:** 7 (Final Phase — Foreshadowing Engine)
**Operator:** Claude (automated), supervised by Oliver Cook KC

---

## 1. Components Built

| File | Component |
|------|-----------|
| `intelligence_pkg/twin/foreshadowing/consultation_analyser.py` | Consultation paper impact analysis with adoption probability |
| `intelligence_pkg/twin/foreshadowing/enforcement_detector.py` | Enforcement trend detection via keyword themes |
| `intelligence_pkg/twin/foreshadowing/soft_signal_analyser.py` | Regulatory speech/publication language analysis |
| `intelligence_pkg/twin/foreshadowing/contagion_analyser.py` | Cross-jurisdictional contagion probability |
| `intelligence_pkg/twin/foreshadowing/orchestrator.py` | Coordinator + quarterly briefing generator |
| Updated `intelligence_pkg/twin/scheduler.py` | Weekly foreshadowing scan job |
| Updated `intelligence_pkg/mcp_server.py` | Real foreshadow_report (replaced stub) |

### Tests: 46 new tests across 5 analyser test files + 4 integration tests

---

## 2. Test Results

**Total tests (all 7 phases):** 392
**Passing:** 391
**xfail:** 1 (confidence calibration — requires human review)
**Failing:** 0
**Regressions from prior phases:** 0

---

## 3. Foreshadowing Signal Types

| Type | Detection Method | Probability Heuristic | Alert Level |
|------|-----------------|----------------------|-------------|
| Consultation | CONSULTATION docs + Sonnet impact assessment | Base 0.65 ± adjusters (mandatory +0.15, FSRA +0.10, intl standards +0.10, discussion -0.15) | FORESHADOW (HIGH impact) |
| Enforcement | Keyword theme grouping + trend detection | Trend analysis (INCREASING/STABLE/DECREASING/INSUFFICIENT_DATA) | FORESHADOW (HIGH exposure) |
| Soft Signal | COMMENTARY docs + Haiku intent analysis (STRONG/MODERATE/WEAK) | Language pattern matching (will/intend→STRONG, considering→MODERATE, noted→WEAK) | FORESHADOW (STRONG match) |
| Contagion | Cross-jurisdiction change detection + keyword matching | Base rates by jurisdiction pair (DIFC→ADGM 0.55, EU 0.40, UK 0.45, US 0.25) | FORESHADOW (HIGH probability + match) |

---

## 4. Probability Heuristics

**All probability estimates are heuristic approximations. They are NOT based on trained ML models.**

### Consultation Adoption
- Base: 0.65
- +0.15: "mandatory"/"required"/"obligation" in title
- +0.10: FSRA source
- +0.10: FATF/IOSCO/BIS/Basel reference
- -0.15: "discussion"/"options paper"
- -0.10: "no action"/"industry-led"
- Capped: 0.10–0.95

### Cross-Jurisdictional Contagion
- DIFC→ADGM: 0.55 | EU→ADGM: 0.40 | UK→ADGM: 0.45 | US→ADGM: 0.25 | EL_SALVADOR→ADGM: 0.10
- +0.20: international standards reference | +0.10: amendment (enacted) | -0.10: consultation (proposed)
- Capped: 0.05–0.90

---

## 5. Phase 7 vs Section 15.3 (Blue Sky) Boundary

| This Phase Delivers | Section 15.3 Describes (NOT built) |
|--------------------|------------------------------------|
| Heuristic probability estimates (base rates + adjusters) | Fine-tuned classification model (Horizon Oracle) |
| Keyword-based trend detection | ML-trained enforcement trend predictor |
| Pattern matching signal strength (STRONG/MODERATE/WEAK) | Probabilistic forecasts ("73% likelihood...") |
| Quarterly Word document briefing | Interactive dashboard with confidence intervals |

---

## 6. Known Limitations

| Item | Notes |
|------|-------|
| Probability accuracy | Heuristic only — no training data or validation corpus |
| Enforcement trends | INSUFFICIENT_DATA when < 3 actions (most jurisdictions) |
| Soft signals | Haiku-based intent analysis; may miss subtle signals |
| Contagion | Jurisdiction pair base rates are estimates, not empirical |
| Quarterly briefing | Opus-generated; requires API key |
