# DFSA — Activation Pack (J4 / J16 / J18 / J19)

**Prepared:** 2026-06-11 (MAX-5 K1/W3, sprint/max5-dfsa-pack — supersedes the MAX-4 V5 HOLD pack)
**For:** Oliver's J4 human activation gate. DIFC is a LAUNCH jurisdiction (MAX-5 charter ruling 1).
**Authoritative matrix:** `docs/matrices/DFSA_tier_matrix.md` (NEW, this sprint) —
per-licence-type (Cat 2-MP/3A dealer, Cat 3C asset/fund manager, Cat 4 adviser/arranger)
× T0–T5. Proposed, pending Oliver approval; once approved it unblocks
`TemplateDiscoveryAgent` (currently HALT — `ucie/jurisdictions/DFSA/manifest.json`
still has `licence_types: ["TBD"]`).

---

## 1. Registry state (verified 2026-06-11)

`TEMPLATE_REGISTRY` ← `services/dfsa_templates.py`: **18 `dfsa_*` templates** of 162 total.
All single-track (`applicable_entity_types=["Authorised Firm"]`, zero `category_tailoring`,
zero `entity_fact_questions`).

| Tier | Count | Templates |
|---|---|---|
| 1 — Registration Pack | 4 | dfsa_application_form, dfsa_regulatory_business_plan, dfsa_fit_proper_declarations, dfsa_technology_systems_description |
| 2 — Mandatory Compliance | 3 | dfsa_aml_cft_programme_difc, dfsa_compliance_manual_difc, dfsa_conflicts_policy |
| 3 — Corporate Governance | 3 | dfsa_board_charter, dfsa_senior_management_responsibilities, dfsa_whistleblowing_policy |
| 4 — Operational Procedures | 5 | dfsa_client_onboarding_procedure, dfsa_order_execution_policy, dfsa_incident_response, dfsa_bcp, dfsa_data_protection |
| 5 — Filings & Monitoring | 3 | dfsa_compliance_monitoring_programme, dfsa_annual_compliance_report, dfsa_mlro_annual_report |

**Suite activation state: 0 DFSA suites** in `SUITE_REGISTRY` (loader registers only
`vara_vasp_bd_tier1`). Single-document flow IS live: `compliance/documents/new` lists
DIFC/DFSA as active and filters templates by `coverage_rulebooks` prefix `DFSA-`.

## 2. Matrix coverage (NEW — J4 discovery now run)

Full matrix: `docs/matrices/DFSA_tier_matrix.md`. Summary:

| Licence type | Slots (T1–T5) | Filled | GAP |
|---|---|---|---|
| Cat 2-MP / 3A dealer | 21 | 16 | 5 (+1 conditional) |
| Cat 3C asset/fund manager | 24 | 16 | 8 |
| Cat 4 adviser/arranger | 18 | 15 | 3 (+1) |
| Tier 0 (all — K4 DIFC company-law lane) | 3 | 0 | 3 |

Deduped new-template gap list (10 items, priority order): `dfsa_kyc_cdd_procedures`,
`dfsa_outsourcing_policy`, `dfsa_complaints_handling`, `dfsa_client_money_procedures`,
`dfsa_suitability_advice_procedure`, `dfsa_fund_manager_cir_compliance`,
`dfsa_fund_valuation_policy`, `dfsa_investment_management_agreement`,
`dfsa_prudential_returns_procedure` (**corpus-blocked**, see §5), Tier-0 DIFC formation
pack (3 docs, **K4 lane**). Items 1–8 are corpus-unblocked today (COB 1,376 sections,
CIR 1,000, AML 405 all current).

**Naming caution:** ADGM "Cat 3A matched principal" ≠ DFSA Cat 3A. DFSA: matched
principal = Cat 2-MP (US $500k base capital, PIB 3.6.2); Cat 3A = dealing as agent
(US $200k). The matrix uses DFSA-correct vocabulary.

## 3. J18-DFSA — wizard/questionnaire path spec (build in K6's UI lane)

Current state, file by file (read 2026-06-11):

| Surface | File | State |
|---|---|---|
| Governance wizard | `~/qanun/app/(dashboard)/compliance/governance/GovernanceOnboardingWizard.tsx` (456 lines) | **No DIFC/DFSA group** in `CATEGORY_GROUPS` (has ADGM, VARA, SV, BVI, Panama) or `STAGE_GROUPS` |
| Questionnaire data | `~/qanun/lib/questionnaires/jurisdiction-questions.ts` | `DFSA_QUESTIONS` EXISTS — 5 minimal questions (free-text category, activities multi, SEO, FO, CO/MLRO) |
| Questionnaire router | `~/qanun/components/qanun/JurisdictionQuestionnaireRouter.tsx` | DFSA already wired ("DFSA Governance Questionnaire") — no change |
| Single-doc page | `~/qanun/app/(dashboard)/compliance/documents/new/page.tsx` | DFSA active; prefix filter `DFSA-` in `lib/api/drafting.ts` — no change |
| Profile endpoint | `~/ADGM/qanun-api/routers/governance.py` | **Hard blocker:** `VALID_FSRA_CATEGORIES = {"cat_1","cat_2","cat_3a","cat_3c"}` (line 26) — any `dfsa_*` category 400s. `VALID_REGULATORY_STAGES` likewise ADGM-only |
| Register seeding | `document_register` (server-only raw SQL table) | Applicability via `applicable_categories` JSON per row — **no DFSA rows / no `dfsa_*` category values** → even with the enum widened, profile creation maps 0 documents |
| Suite start | `routers/drafting.py /drafting/suite` | Works for DFSA **only with explicit `doc_types`**; auto-derive uses `getattr(t,'jurisdictions',['ADGM'])` — attribute doesn't exist on any template, so `jurisdiction="DFSA"` derives an empty/wrong set |
| Classifier | `services/business_classifier.py` + `data/submission_manifest.json` | ADGM/FSRA-only (FSRA hard rules + manifest categories baked into prompt); valid outputs `category_1…category_4, representative_office` |

Exact change list (J18-DFSA):

1. **Wizard enums** (`GovernanceOnboardingWizard.tsx`): add `CATEGORY_GROUPS` entry
   "DIFC / DFSA" with `dfsa_cat_2mp`, `dfsa_cat_3a`, `dfsa_cat_3c`, `dfsa_cat_4`
   (+descriptions); add `STAGE_GROUPS` entry (`dfsa_pre_application`,
   `dfsa_authorised`); optional `APPROXIMATE_COUNTS`. **~30 lines.**
2. **Questionnaire upgrade** (`jurisdiction-questions.ts`): make
   `dfsa_licence_category` a structured select (Cat 1/2/2-MP/3A/3B/3C/3D/4/5), add
   client-type multi (Retail/Professional/Market Counterparty), endorsements
   (Retail, Client Money/Assets, Crypto Token), DFSA firm reference no., MLRO split
   from CO, fund-manager conditional block (fund types, AUM band). **~60–80 lines.**
3. **Backend enum + stages** (`routers/governance.py`): widen
   `VALID_FSRA_CATEGORIES`/`VALID_REGULATORY_STAGES` (or per-jurisdiction validation
   keyed off category prefix). **~10 lines + tests.**
4. **Register migration** (server `document_register`): seed 18+ DFSA rows with
   `applicable_categories` = matrix §3 mapping (e.g. order_execution_policy excludes
   `dfsa_cat_4`). Idempotent migration per qanun-api rules. **~120 lines migration.**
5. **Suite derivation fix** (`routers/drafting.py`): replace the phantom
   `jurisdictions` attr with the `coverage_rulebooks` prefix convention the frontend
   already uses (or add `jurisdictions` to `DocumentTemplate`). **~10 lines.**
6. **(Optional, post-gate) classifier**: parameterise `BusinessModelClassifier` by
   jurisdiction with a DFSA manifest (PIB 1.3 hard rules). **~150 lines + manifest
   JSON.** Not required for wizard reachability.

**Size estimate: ~230–250 lines core (items 1–5) + ~150 optional (item 6); 2 files
frontend, 2 files + 1 migration backend. No new components — existing renderer/router
already dispatch DFSA.**

## 4. E2E design — 8 DFSA cells (extends the 40-cell MAX-4 matrix conventions)

Convention: `JURISDICTION.LICENCE-CODE.doc_type`, 2 licence types × 4 templates,
smallest templates for cost (all chosen cells are 3–4-section, 1,200–1,600 min-word
templates; suite start via explicit `doc_types` so no backend change needed).

**Fictional DIFC entity shapes** (DIFC private companies limited by shares under
DIFC Companies Law No. 5 of 2018 — corpus doc 2656):

- **Khalij Asset Management (DIFC) Ltd** — Cat 3C; Managing Assets + Managing a
  Collective Investment Fund (Exempt Funds, professional clients only); base capital
  US $140k; SEO/FO/CO+MLRO named; no client money (fund custodian model).
- **Meydan Advisory Partners (DIFC) Ltd** — Cat 4; Advising on Financial Products +
  Arranging Deals in Investments; professional clients; US $30k base capital;
  no client assets; outsourced internal audit.

| # | Cell | Tier | Min words |
|---|---|---|---|
| 1 | `DFSA.DFSA-CAT3C.dfsa_fit_proper_declarations` | T1 | 1,200 |
| 2 | `DFSA.DFSA-CAT3C.dfsa_conflicts_policy` | T2 | 1,200 |
| 3 | `DFSA.DFSA-CAT3C.dfsa_senior_management_responsibilities` | T3 | 1,200 |
| 4 | `DFSA.DFSA-CAT3C.dfsa_compliance_monitoring_programme` | T5 | 1,200 |
| 5 | `DFSA.DFSA-CAT4.dfsa_fit_proper_declarations` | T1 | 1,200 |
| 6 | `DFSA.DFSA-CAT4.dfsa_whistleblowing_policy` | T3 | 1,200 |
| 7 | `DFSA.DFSA-CAT4.dfsa_data_protection` | T4 | 1,200 |
| 8 | `DFSA.DFSA-CAT4.dfsa_mlro_annual_report` | T5 | 1,600 |

Tiers 1/2/3/4/5 all covered; one shared template (fit & proper) across both licence
types for a same-template/different-entity comparison, matching BVI's reuse pattern.
**Deliberately excluded:** anything PIB/PRU-heavy (`dfsa_application_form` s4 cites
PIB 1.1; capital-adequacy drafting degraded per §5) and `dfsa_order_execution_policy`
for Cat 4 (not applicable per matrix). Expected scorer profile: citation verification
should run clean — all template refs resolve exactly (§5a) and DFSA ref shape
(`DFSA-MODULE C.S.R`) is regex-friendly, unlike the VARA Roman-numeral shapes that
drove VARA to 0/8.

## 5. Corpus verification (run 2026-06-11, corpus.db mode=ro)

**(a) Template ref check (LC7-style, DFSA-scoped):** 18 templates → 75 provision-ref
entries, 17 unique refs → **17/17 resolve as exact `section_ref` rows on is_current=1
docs; 0 dangling.** (The MAX-4 "DFSA-GEN 5.3 class" worry is fully retired post-MAX-3
prefixing + LC7.)

**(b) PL-03-class sweep (stub/truncation candidates):** DFSA = 22 current docs,
9,271 sections. 6,121 DFSA-targeted citation rows; 3,109 distinct targets; **201
cited-but-missing** (no exact or child section), concentrated:

| Doc | Sections | Finding |
|---|---|---|
| DFSA-PIB (2825) | 1,174 | **Truncated parse: chapters 1–7 only (ch. 7 = 10 sections) + App C; 93 cited-but-missing refs across ch. 7.3–14** (capital adequacy, liquidity, reporting). Worst current DFSA defect |
| DFSA-PIN (2826) | 501 | 104 cited-but-missing; chapters >10 nearly absent (insurance — out of launch scope) |
| DFSA-PRU (2828) | 73 | Revived but partial: ch. 1, 2, 6 only (587k chars in 73 sections — coarse). Re-scrape still parked |
| DFSA-GLO (2822) | 17 | Glossary in 17 sections / 92k chars — defined-term lookup degraded |
| DFSA-CMC (2817) | 44 | ch. 2, 6, 7 missing (3 cited-but-missing) — minor |
| doc 2428 (Crypto Token guidance) | 0 | 34k words, zero sections — unsectioned |

**(c) DIFC company-law state (Tier-0 row, K4's lane):** **DIFC-CL doc 2656 — "DIFC
Companies Law No. 5 of 2018 (Consolidated March 2022)", 154 sections (`DIFC-CL s.N`),
is_current=1 — present and usable** for Tier-0 grounding. The remaining DIFC
legislation is stub-parsed: Collective Investment Law **0 sections**, Investment
Trust Law **0 sections**, Islamic Financial Business Law 1, Markets Law 7, Regulatory
Law 9. The CIL stub matters for Cat 3C fund managers (fund-law citations) — flag to
K4 alongside the Tier-0 template work.

## 6. J19 category tailoring

Unchanged from MAX-4: `category_tailoring` = {} on all 18 templates (`grep -c
category_tailoring services/dfsa_templates.py` = 0). With the §2 matrix approved,
differentiation is delivered matrix-level (doc applicability) first; within-document
tailoring (J19) remains open and is NOT a gate blocker for the §4 E2E run.

## 7. RECOMMENDATION

**GO-PENDING-MATRIX-APPROVAL** (was: HOLD). The two structural blockers behind the
MAX-4 HOLD are resolved or reduced to enumerated work:

1. ~~No matrix~~ → `docs/matrices/DFSA_tier_matrix.md` exists, corpus-grounded —
   **needs Oliver's J4 approval**, then propagate `licence_types` into
   `ucie/jurisdictions/DFSA/manifest.json` to un-HALT TemplateDiscoveryAgent.
2. ~~No wizard path~~ → J18-DFSA fully specified (§3): ~230–250 core lines across 4
   files + 1 register migration; build in K6's UI lane. The real blocker was never
   only the wizard — `VALID_FSRA_CATEGORIES` and the empty DFSA register rows are
   called out explicitly.
3. Corpus: refs 17/17 clean; remaining defects are scoped (PIB ch. 8–14 truncation,
   PRU partial, GLO coarse, DIFC CIL/ITL stubs) and avoidable by the §4 cell design.
   Keep prudential-content templates HOLD until the PIB/PRU re-scrape lands.
4. E2E: run the §4 8-cell pack after J18 items 3–5 (or with explicit doc_types
   immediately) — no DFSA-specific scorer risk identified.

Single-document drafting remains quietly available throughout.
