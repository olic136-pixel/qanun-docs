# Panama — Tier Matrix and Template Mapping (MAX-5 K2)

**Prepared:** 2026-06-11 (MAX-5 K2, sprint/max5-jx-packs)
**Closes:** the MAX-4 V5 register omission — Panama previously had **no J-item and no matrix at all**. This document is the Panama equivalent of the J5-class matrices.
**Template source:** `qanun-api services/panama_templates.py` @ sprint/max5-jx-templates (**14 `panama_*` templates** — 10 pre-existing Tier 1–3 + 4 new Tier 4–5).
**Corpus basis (all refs LIKE-verified, is_current=1, 2026-06-11):** PAN-LMV (386 articles), PAN-LMV-67 (169), PAN-LEY32 (96 — Sociedades Anónimas, incl. Art.36 Registro de Acciones), PAN-LEY52 (22), PAN-AML (7), PAN-LSEG (336). SMV Acuerdos remain unindexed — anything Acuerdo-grounded is gap-listed, not authored.

## 1. Licence-type taxonomy (rows — per E2E conventions, `scripts/e2e_validation.py`)

| Code | Licence type | Launch priority |
|---|---|---|
| PAN-CASA-TRAD | Casa de Valores — traditional securities | **YES** (E2E cell `PAN-CASA-TRAD`) |
| PAN-CASA-CRYPTO | Casa de Valores — digital-asset business line | **YES** (E2E cell `PAN-CASA-CRYPTO`) |
| PAN-ADM | Administradora de Inversión | no |
| PAN-SI | Sociedad de Inversión | no |
| PAN-ASESOR | Asesor de Inversión | no |

The crypto and traditional Casa de Valores tracks share one licence (PAN-LMV Art.50); the crypto track differs by conditional sections, not by separate templates (mirrors the SV-DASP conditional-section pattern).

## 2. Template → tier mapping (all 14; **bold** = added in MAX-5 K2)

| Tier | Template | CASA-TRAD | CASA-CRYPTO | ADM | SI | ASESOR |
|---|---|---|---|---|---|---|
| 1 | panama_casa_valores_application (PAN-LMV Art.50) | ✓ | ✓ | N/A¹ | N/A¹ | N/A¹ |
| 1 | panama_regulatory_business_plan | ✓ | ✓ | ✓ | ✓ | ✓ |
| 1 | panama_aml_cft_programme_panama (PAN-LMV Art.70) | ✓ | ✓ | ✓ | ✓ | ✓ |
| 1 | panama_fit_proper_declaration (Art.78/79) | ✓ | ✓ | ✓ | ✓ | ✓ |
| 2 | panama_compliance_manual_panama | ✓ | ✓ | ✓ | ✓ | ✓ |
| 2 | panama_kyc_cdd_procedures_panama | ✓ | ✓ | ✓ | ✓ | ✓ |
| 2 | panama_market_conduct_policy (Art.100/101) | ✓ | ✓ | ✓ | ✓ | ✓ |
| 3 | panama_board_charter_panama (Art.167) | ✓ | ✓ | ✓ | ✓ | ✓ |
| 3 | panama_senior_management_panama | ✓ | ✓ | ✓ | ✓ | ✓ |
| 3 | panama_whistleblowing_panama | ✓ | ✓ | ✓ | ✓ | ✓ |
| 4 | **panama_client_asset_custody_procedures** (Art.64/228/236/237/63; crypto-conditional s3) | ✓ | ✓ (s3 active) | ✓ | ✓ | N/A² |
| 4 | **panama_books_records_procedures** (Art.60/175; PAN-LEY32 Art.36) | ✓ | ✓ | ✓ | ✓ | ✓ |
| 5 | **panama_smv_periodic_reporting** (Art.61/177/189/171) | ✓ | ✓ | ✓ | ✓ | ✓ |
| 5 | **panama_capital_liquidity_monitoring** (Art.55/60/61) | ✓ | ✓ | ✓ | N/A³ | N/A³ |

¹ Application variants for ADM (Art.184/185), SI (Art.152/158/159) and Asesor (Art.50) are gap-listed below.
² Asesor does not hold client assets (advisory only).
³ Art.55 capital neto applies to casas de valores; ADM kept in scope for group prudential monitoring; SI/Asesor excluded at v1.

**Launch-priority coverage: 14/14 slots filled or explicitly N/A for both PAN-CASA-TRAD and PAN-CASA-CRYPTO (0 GAP).** Tier 4 = 2, Tier 5 = 2 (was 0/0).

## 3. Gap list (not authored — over the ≤4 budget or not corpus-groundable)

| Gap | Tier | Groundable? | Verdict |
|---|---|---|---|
| Administradora de Inversión licence application | 1 | YES (PAN-LMV Art.184/185 verified) | Author when ADM row activates |
| Sociedad de Inversión registration | 1 | YES (Art.152/158/159 verified) | Author when SI row activates |
| Asesor de Inversión application variant | 1 | YES (Art.50) | Author when ASESOR row activates |
| Crypto market-conduct / travel-rule supplement | 2 | **NO** — SMV digital-asset Acuerdos not in corpus | Park pending corpus ingest; crypto track relies on conditional s3 of the custody template + generic market conduct |
| Complaints-handling procedure | 4 | **NO** — no verified LMV complaints article; Acuerdo-level | Park pending corpus ingest |
| E2E PAN coverage residual (one cell) | — | — | Tracked by E2E lane; not a template gap |

## 4. Cross-lane notes

- `applicable_entity_types` uses the Spanish entity-type strings ("Casa de Valores", "Administradora de Inversión", "Sociedad de Inversión", "Asesor de Inversión") — the UI licence codes (`casa_de_valores`, `asesor_de_inversion`, `sociedad_anonima`) and E2E codes (PAN-CASA-CRYPTO/TRAD) must map onto these (see MAX5_UI_punchlist_K6.md).
- `sociedad_anonima` in the governance-suite UI is a corporate form, not an SMV licence type — recommend replacing with `administradora_de_inversion` + `sociedad_de_inversion` and adding a crypto/traditional toggle on `casa_de_valores`.
