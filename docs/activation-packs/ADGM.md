# ADGM — Activation Pack (J1 / J6–J9 / J18 / J19)

**Prepared:** 2026-06-10 (MAX-4 V5, sprint/max4-j-packs)
**For:** Oliver's J1 human activation gate
**Authoritative matrix:** **none exists yet.** Register J1 (Open) requires a TemplateDiscoveryAgent run for ADGM producing a per-licence-type set (Cat 1, 2, 3A, 3B, 3C, 4, 5); `TemplateDiscoveryAgent.run()` currently HALTs for any jurisdiction other than VARA and EL_SALVADOR. The de-facto inventory is the original Qanun template set (`sprint-6-prep/adgm-template-inventory.md`) plus the cross-jurisdiction logical map (`sprint-6-prep/cross-jurisdiction-document-map.md`).

---

## 1. Registry state

`TEMPLATE_REGISTRY` core block (`services/drafting_templates.py:8092`): **23 ADGM templates** of 162 total. These are the most mature templates in the system — the only ones with `category_tailoring`, `entity_fact_questions`, Stark exemplars and appendices.

Indicative tier mapping (no formal tier field; classified against the 5-tier model):

| Tier | Count | Templates |
|---|---|---|
| 1 — Registration Pack | **0** | — (no application form, regulatory business plan, F&P declarations, capital evidence) |
| 2 — Mandatory Compliance | 10 | aml_cft_policy, compliance_manual (31 sections + 6 appendices), kyc_cdd_procedures, business_risk_assessment, conflicts_policy, cyber_risk_framework, outsourcing_policy, customer_verification_procedures, suitability_policy, risk_management_policy |
| 3 — Corporate Governance | 4 | board_governance_charter, whistleblowing_policy, terms_of_reference_committees, succession_plan |
| 4 — Operational Procedures | 6 | business_continuity_plan, trading_procedures_manual, margin_financing_policy, client_agreement_tob, custody_agreement, margin_terms_of_business |
| 5 — Filings & Monitoring | 3 | compliance_monitoring_programme, icaap, recovery_resolution_plan |

**Suite activation state: 0 ADGM suites** in `SUITE_REGISTRY` (no discovery run, no emitted JSON).

## 2. Matrix coverage

**Not computable — the J1 per-licence-type × tier matrix has not been produced.** Punch-list therefore reduces to structural gaps against the 5-tier model:

| Jurisdiction | Licence type | Tier | Required doc | Template exists | Id / GAP |
|---|---|---|---|---|---|
| ADGM | all (Cat 1–5) | 1 | FSRA application / regulatory business plan / F&P / capital evidence pack | N | **GAP — entire Tier 1 absent** |
| ADGM | all | 2–5 | (per J1 matrix, TBD) | partially | 23 templates exist; mapping to per-category requirement lists awaits the J1 discovery run |
| ADGM | Cat 3A/3C etc. | 2 | s25b ADGM Returns / s27b FATCA-CRS / s27c Economic Substance sections in compliance manual | N | **GAP — J6/J7/J8 Open** |
| ADGM | all | — | 6 Stark appendices (sA, sB, sF1, sF2, sG, sH) | partial | compliance_manual carries 6 appendices; verify against J9 spec at gate |

Per-category differentiation **does** exist through `category_tailoring` (all 23 templates carry keys `category_1, category_2, category_3a, category_3b, category_3c, category_4, category_5, default`) — ADGM is the only jurisdiction where J19 is substantively done.

**Coverage %: N/A (matrix missing).** Against the indicative 5-tier shape: 4/5 tiers populated; Tier 1 = 0%.

## 3. Questionnaire gaps affecting ADGM (J18)

- Wizard offers Cat 3C, 3A, 2, 1 — **missing Cat 3B, Cat 4, Cat 5** (J1 acceptance names all seven).
- Stage options (pre-application / IPA / authorised / compliance audit) — the most complete of the five jurisdictions.
- `entity_fact_questions` present on **23/23 templates** (MLRO, SEO, AUM, PEP exposure, prime broker, custodian etc.) — the only jurisdiction with pre-draft questionnaires.
- `BusinessModelClassifier` works for ADGM only (hard rules: retail→Cat 2 minimum, principal dealing→3B, etc.) — functioning as designed here.
- Missing: ADGM/FSRA registration number capture, entity legal form (LTD/branch/SPV), Islamic-finance flag follow-through to template selection.

## 4. J19 category-tailoring spot-check

- Sampled `aml_cft_policy`: 8 tailoring keys with substantive per-category drafting guidance (e.g. category_3a counterparty-DD focus vs category_1 full-bank programme). **J19 satisfied for ADGM's 23.**
- Provision spot-check (corpus.db, mode=ro): `AML 4.1` → EXACT; `AML 12.1.1` → EXACT. 2/2 resolve.

## 5. Corpus caveats (from LAUNCH_VERDICT_20260610)

- FSRA corpus is the deepest (629 current docs) and LC1–LC5 are 🟢, but the residual quality tail concentrates here: **~1,900 genuine dangling citation targets** (led by IFR 6/7/8 chapter-row parser gaps) — quality tail, not integrity debt.
- **LC7 open items are ADGM-specific:** `compliance_manual` has 21 stale section-ids; 42 unique dangling template refs ("DFSA-GEN 5.3 class") across the registry. The compliance_manual items should be fixed before an ADGM gate sign-off since it is the flagship template.
- J7 (FATCA/CRS) is blocked on B1 parser redesign (COBS 17.4.1 resolution) per the register.

## 6. Evidence — L2 sample drafts

**PENDING E2E RUN** — placeholder for V1's L2 sample drafts (suggest aml_cft_policy + compliance_manual for Cat 3C — exercises tailoring, questionnaires and appendices in one pass).

## 7. RECOMMENDATION

**ACTIVATE-WITH-CAVEATS** — the 23 templates are the system's most production-ready (tailoring + questionnaires + exemplars + deep corpus) and are already live in the single-document drafting flow; caveats: no J1 per-licence matrix or suites yet (Tier 1 registration pack entirely absent — fine for already-authorised firms, blocking for pre-application clients), J6–J9 manual sections open, compliance_manual 21 stale section-ids to patch.
