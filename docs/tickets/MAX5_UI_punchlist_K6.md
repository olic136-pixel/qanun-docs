# MAX-5 K2 → K6 — Per-Jurisdiction UI Reachability Punch-List

**Prepared:** 2026-06-11 (MAX-5 K2, sprint/max5-jx-packs). Exact reachability gaps for the UI lane. Repo: `~/qanun`. Backend registry state: qanun-api @ sprint/max5-jx-templates (BVI 20, Panama 14, SV 52 templates).

Surfaces audited: `GovernanceOnboardingWizard.tsx` (wizard), `compliance/documents/new/page.tsx` (single-doc drafting), `compliance/governance-suite/page.tsx` (suite builder), `components/qanun/JurisdictionQuestionnaireRouter.tsx` + `lib/questionnaires/jurisdiction-questions.ts` (questionnaires), `components/qanun/cee/JurisdictionSelector.tsx` (CEE).

## BVI

| # | Gap | File / lines | Fix |
|---|---|---|---|
| B1 | VASP not selectable in wizard although `bvi_vasp_application` exists (MAX-4 carryover) | `GovernanceOnboardingWizard.tsx` 52–59 | Add `bvi_vasp_cust` + `bvi_vasp_ex` options (launch priority is VASP-CUST per E2E) |
| B2 | Single-doc drafting page omits BVI entirely | `documents/new/page.tsx` 31–36 (`JURISDICTIONS`) | Add `{ code: 'BVI', label: 'BVI — FSC', active: true }` |
| B3 | Suite page licence codes don't cover VASP; `company_formation` has no Tier 1–3/5 backing (registers template only) | `governance-suite/page.tsx` 50–54 | Replace with: `approved_manager` (live), `vasp_cust` (live), `vasp_ex`, `investment_business`, `mutual_fund`, `company_formation` (registers-only, label accordingly) — align codes to BVI_J5_matrix.md rows |
| B4 | `DOC_COUNTS.BVI` `[0,7,9,6,5,4]` (=31) is fiction; registry is 20 | `governance-suite/page.tsx` 73 | Set `[0, 4, 5, 3, 4, 4]` (pack tier convention: T1=4 + VASP-variant, T2=5, T3=3, T4=4, T5=4) |
| B5 | BVI questionnaire content thin: no FSC certificate number, no Approved-vs-Restricted capital framing, zero entity_fact_questions backend-side | `lib/questionnaires/jurisdiction-questions.ts` (BVI block) | J18 content work — add licence-category select sourced from BVI_J5_matrix rows + FSC cert number + AM 31-Jan annual-return acknowledgement |
| B6 | Wizard BVI stages adequate (`bvi_pre_application`/`bvi_registered`) | — | No change |

## PANAMA

| # | Gap | File / lines | Fix |
|---|---|---|---|
| P1 | Single-doc drafting page omits PANAMA | `documents/new/page.tsx` 31–36 | Add `{ code: 'PANAMA', label: 'Panama — SMV', active: true }` |
| P2 | Wizard offers only Casa de Valores + Asesor; Administradora/Sociedad de Inversión absent | `GovernanceOnboardingWizard.tsx` 60–66 | Add `pan_administradora`, `pan_sociedad_inversion`; add a crypto/traditional toggle (or paired options `pan_casa_valores_trad` / `pan_casa_valores_crypto`) to match E2E cells PAN-CASA-TRAD/CRYPTO |
| P3 | Suite page: `sociedad_anonima` is a corporate form, not an SMV licence; no crypto/trad distinction; ADM/SI missing | `governance-suite/page.tsx` 55–59 | Replace per PANAMA_tier_matrix.md §1 taxonomy |
| P4 | `DOC_COUNTS.PANAMA` `[0,6,8,5,4,3]` (=26) vs registry 14 | `governance-suite/page.tsx` 74 | Set `[0, 4, 3, 3, 2, 2]` |
| P5 | No Panama questionnaire at all: `JURISDICTION_LABELS` lacks PANAMA and `jurisdiction-questions.ts` has no PAN question set → router renders "No questionnaire defined" | `JurisdictionQuestionnaireRouter.tsx` 25–30; `lib/questionnaires/jurisdiction-questions.ts` | Add PANAMA label + PAN_QUESTIONS (licence type incl. crypto/trad, Registro Público folio, agente residente, Ejecutivo Principal, capital neto Art.55 ack, Spanish/bilingual output preference) |
| P6 | Spanish-language preference field absent (drafting cites Spanish LMV articles) | same as P5 | Include in PAN_QUESTIONS |

## EL SALVADOR (ES)

Full change set in `docs/specs/ES_J18_split_spec.md` — headline items:

| # | Gap | File / lines | Fix |
|---|---|---|---|
| S1 | Wizard exposes 4/10 categories; held tracks absent rather than gated | `GovernanceOnboardingWizard.tsx` 43–51 | All 10 from `lib/constants/sv-categories.ts`; 6 gated "Coming soon" |
| S2 | Suite page SV list drift: 9 entries, missing `dasp_str`, `issu` ≠ matrix code | `governance-suite/page.tsx` 38–48 | Source from sv-categories constant |
| S3 | No pre-registration stage | `GovernanceOnboardingWizard.tsx` 100–105 | Add `sv_pre_registration` |
| S4 | `sv_licence_category` is free text | `jurisdiction-questions.ts` 46–49 | Enumerated select, gated options disabled |
| S5 | `APPROXIMATE_COUNTS` ADGM-only → SV confirm step shows "—" | `GovernanceOnboardingWizard.tsx` 125–130 | Add live-track docCounts 43/39/40/39 |

## CROSS-JURISDICTION (blocking for all three)

| # | Issue | Where | Note |
|---|---|---|---|
| X1 | **Suite endpoint ignores licence_type/tiers; `jurisdictions` attr doesn't exist on DocumentTemplate** — non-ADGM suites mis-derive doc_types | qanun-api `routers/drafting.py:568–575` | API-lane fix required before any non-ADGM suite activation; UI gating cannot compensate |
| X2 | Zero `entity_fact_questions` on all BVI (20), Panama (14) and SV (52) templates | qanun-api template modules | J18 backend content half of the questionnaire work |
| X3 | `BusinessModelClassifier` is ADGM-only | `~/qanun` + api | Park; not launch-blocking if licence type is explicitly selected |
| X4 | Wizard payload key is `fsra_category` for every jurisdiction | `lib/api/governance.ts` 8/44/107/114 | Cosmetic-but-confusing contract; rename to `licence_category` only with a coordinated API migration (do NOT rename unilaterally — K12 lesson) |
