# DFSA — Per-Licence-Type × Tier Matrix (J-discovery, MAX-5 W3)

**Prepared:** 2026-06-11 (K1, sprint/max5-dfsa-pack)
**Status:** PROPOSED — pending Oliver matrix approval (J4 gate). This document is the
J-discovery output that `ucie/jurisdictions/DFSA/manifest.json` (`licence_types: ["TBD"]`)
and `TemplateDiscoveryAgent` (HALT on missing matrix) have been waiting on.
**Derivation:** the Studio Addendum spec is not locatable; licence categories are derived
from the repo (TEMPLATE_REGISTRY 18 `dfsa_*` templates, `business_classifier.py`,
GovernanceOnboardingWizard) + the DFSA corpus (DFSA-PIB 1.3 category rules,
DFSA-PIB 3.6.2 base capital table, DFSA-GEN 7 licensing chapter, DFSA-COB, DFSA-CIR).

---

## 1. DFSA licence-category framework (corpus-grounded)

Categories per **DFSA-PIB 1.3** (all refs verified in corpus.db, doc 2825, is_current=1):

| Category | Determinative Financial Service (PIB 1.3) | Base Capital (PIB 3.6.2) |
|---|---|---|
| Cat 1 | Accepting Deposits / Managing a PSIAu | US $10m |
| Cat 2 | Dealing in Investments as Principal; Providing Credit | US $2m (**US $500k if Matched Principal only**) |
| Cat 3A | Dealing in Investments as Agent | US $200k |
| Cat 3B | Custody for a Fund / fund trustee / EMPS (PIB 1.3.4) | US $1m (crypto custody) and variants |
| Cat 3C | Managing Assets; Managing a Collective Investment Fund; Custody (non-fund); PSIAr (PIB 1.3.5) | US $140k (Public/Credit Fund or Managing Assets) / US $40k (other) |
| Cat 3D | Money Services (Stored Value issuance class) | US $200k |
| Cat 4 | Arranging Deals, Advising on Financial Products, Arranging Custody, Insurance Intermediation, Fund Administration etc. (PIB 1.3.6) | US $30k (US $140k crowdfunding / money transmission) |
| Cat 5 | Islamic financial institution managing PSIAu | US $10m |

**Naming caution (cross-jurisdiction):** ADGM "Cat 3A = matched principal dealer" does
NOT map to DFSA Cat 3A. In DFSA terms a matched-principal dealer is **Category 2
(Matched Principal)** at US $500k base capital (PIB 3.6.2); DFSA Cat 3A is
dealing **as agent**. The matrix below carries the dealer track as
**"Cat 2-MP / 3A dealer"** to keep the charter's intent honest in DFSA vocabulary.

Mandatory appointments all categories: SEO, Finance Officer, Compliance Officer, MLRO
(DFSA-GEN 7.5, verified; CO+MLRO combinable, GEN 7.5 guidance).

## 2. Tier model

Same five-tier model as ADGM/VARA (`cross-jurisdiction-document-map.md`) plus the
Tier-0 entity-formation row:

- **T0** — DIFC entity formation (company-law lane, K4)
- **T1** — Registration pack (authorisation application set)
- **T2** — Mandatory compliance (AML/CFT, compliance manual, conflicts)
- **T3** — Corporate governance
- **T4** — Operational procedures
- **T5** — Filings & monitoring

## 3. Matrix — required doc | template | GAP

Legend: ✓ = required for this licence type; (✓) = required only if the relevant
activity/endorsement is held; — = not required. Template column gives the
`TEMPLATE_REGISTRY` id or **GAP**.

### Tier 0 — DIFC entity formation (K4 lane; see §5 for corpus state)

| Required doc (logical) | 2-MP/3A | 3C | 4 | Template | Corpus anchor |
|---|---|---|---|---|---|
| DIFC incorporation pack (Articles of Association, incorporation resolutions) | ✓ | ✓ | ✓ | **GAP** (no dfsa/difc T0 templates) | DIFC-CL (doc 2656, 154 sections, current) |
| Registered office + officers register set | ✓ | ✓ | ✓ | **GAP** | DIFC-CL s.* |
| Shareholder / UBO register | ✓ | ✓ | ✓ | **GAP** | DIFC-CL s.* |

### Tier 1 — Registration pack

| Required doc | 2-MP/3A | 3C | 4 | Template |
|---|---|---|---|---|
| Authorisation application (GEN 7.2) | ✓ | ✓ | ✓ | `dfsa_application_form` |
| Regulatory business plan | ✓ | ✓ | ✓ | `dfsa_regulatory_business_plan` |
| Fit & proper declarations / Authorised Individuals (GEN 7.6) | ✓ | ✓ | ✓ | `dfsa_fit_proper_declarations` |
| Technology & systems description (GEN 5.3) | ✓ | ✓ | ✓ | `dfsa_technology_systems_description` |
| Prudential returns setup / ICAAP-lite (PIB 10, EPRS) | ✓ | ✓ | (✓) | **GAP** — also corpus-blocked: PIB ch. 8–14 absent (§5) |
| Fund-platform addendum: CIR fund manager statement (CIR 13) | — | (✓) Fund Manager | — | **GAP** |

### Tier 2 — Mandatory compliance

| Required doc | 2-MP/3A | 3C | 4 | Template |
|---|---|---|---|---|
| AML/CFT programme (AML 4–7) | ✓ | ✓ | ✓ | `dfsa_aml_cft_programme_difc` |
| Compliance manual (GEN 5.3) | ✓ | ✓ | ✓ | `dfsa_compliance_manual_difc` |
| Conflicts of interest policy (COB 3.5) | ✓ | ✓ | ✓ | `dfsa_conflicts_policy` |
| KYC/CDD procedures (AML 7) — standalone slot in logical map | ✓ | ✓ | ✓ | **GAP** (partially covered inside AML programme + client onboarding) |
| Outsourcing policy (GEN 5.3.21-class) | ✓ | ✓ | ✓ | **GAP** (one section inside `dfsa_technology_systems_description` only) |
| Complaints handling (COB 2 / GEN 9-class) | ✓ | ✓ | ✓ | **GAP** |

### Tier 3 — Corporate governance

| Required doc | 2-MP/3A | 3C | 4 | Template |
|---|---|---|---|---|
| Board charter (GEN 2.1/5.3) | ✓ | ✓ | ✓ | `dfsa_board_charter` |
| Senior management responsibilities map (GEN 7.4/7.5) | ✓ | ✓ | ✓ | `dfsa_senior_management_responsibilities` |
| Whistleblowing policy (GEN 5.3) | ✓ | ✓ | ✓ | `dfsa_whistleblowing_policy` |
| Remuneration / governance policy (GEN 5.3 structure class) | ✓ | ✓ | (✓) | **GAP** (logical-map optional slot) |

### Tier 4 — Operational procedures

| Required doc | 2-MP/3A | 3C | 4 | Template |
|---|---|---|---|---|
| Client onboarding & classification (COB 2.2) | ✓ | ✓ | ✓ | `dfsa_client_onboarding_procedure` |
| Order execution / best execution policy (COB 6.12) | ✓ | ✓ (executes orders) | — | `dfsa_order_execution_policy` |
| Incident response (GEN 5.3) | ✓ | ✓ | ✓ | `dfsa_incident_response` |
| BCP (GEN 5.3) | ✓ | ✓ | ✓ | `dfsa_bcp` |
| Data protection policy (DIFC DP Law alignment) | ✓ | ✓ | ✓ | `dfsa_data_protection` |
| Client Money / Client Asset procedures (COB 6.11–6.14, App5/App6) | ✓ holds client money | (✓) | — (Cat 4 typically no client assets) | **GAP** |
| Custody operations / safe custody (COB 6.13-class) | (✓) | (✓ non-fund custody) | — | **GAP** |
| Fund valuation & pricing policy (CIR class) | — | (✓) Fund Manager | — | **GAP** |
| Investment mandate / discretionary management agreement pack | — | ✓ | — | **GAP** |
| Suitability / advice-process procedure (COB 3.4-class) | — | (✓) | ✓ | **GAP** |

### Tier 5 — Filings & monitoring

| Required doc | 2-MP/3A | 3C | 4 | Template |
|---|---|---|---|---|
| Compliance monitoring programme | ✓ | ✓ | ✓ | `dfsa_compliance_monitoring_programme` |
| Annual compliance report to board | ✓ | ✓ | ✓ | `dfsa_annual_compliance_report` |
| MLRO annual report (AML 12-class) | ✓ | ✓ | ✓ | `dfsa_mlro_annual_report` |
| Prudential / EPRS return procedures (PIB/REP) | ✓ | ✓ | (✓) | **GAP** — corpus-blocked (PIB ch. 8–14, PRU partial) |
| Fund annual/periodic reports (CIR class) | — | (✓) Fund Manager | — | **GAP** |

## 4. Coverage summary

All 18 templates are single-track (`applicable_entity_types=["Authorised Firm"]`,
`category_tailoring` absent) — they apply to every category; differentiation today is
matrix-level (which docs apply), not within-document.

| Licence type | Slots (T1–T5, incl. conditionals) | Filled by existing template | GAP |
|---|---|---|---|
| Cat 2-MP / 3A dealer | 21 | 16 | 5 (prudential setup, KYC/CDD standalone, outsourcing, complaints, client money) + 1 conditional (custody ops) |
| Cat 3C asset/fund manager | 24 | 16 | 8 (above 5 + fund-manager CIR set: CIR statement, valuation policy, mandate pack, fund reports — suitability conditional) |
| Cat 4 adviser/arranger | 18 | 15 | 3 firm (KYC/CDD standalone, outsourcing, complaints) + suitability/advice-process; client-money/custody/execution slots drop out |
| Tier 0 (all) | 3 | 0 | 3 (K4 DIFC company-law lane) |

Unique **new-template gap list** (deduped across categories, priority order):

1. `dfsa_kyc_cdd_procedures` (T2, all cats) — AML 7 standalone
2. `dfsa_outsourcing_policy` (T2, all cats) — GEN 5.3
3. `dfsa_complaints_handling` (T2, all cats) — COB/GEN
4. `dfsa_client_money_procedures` (T4, dealer/3C) — COB 6.11–6.14 — **blocked on nothing; COB fully present (1,376 sections)**
5. `dfsa_suitability_advice_procedure` (T4, Cat 4 + 3C) — COB 3.4
6. `dfsa_fund_manager_cir_compliance` (T1/T4, 3C-FM) — CIR 13 present (CIR: 1,000 sections)
7. `dfsa_fund_valuation_policy` (T4, 3C-FM) — CIR
8. `dfsa_investment_management_agreement` (T4, 3C) — COB
9. `dfsa_prudential_returns_procedure` (T1/T5) — **HOLD: corpus-blocked** until PIB ch. 8–14 / PRU re-scrape lands
10. Tier-0 DIFC formation pack (3 docs) — **K4 lane**, DIFC-CL present in corpus

## 5. Corpus state feeding this matrix (verified 2026-06-11, corpus.db mode=ro)

- DFSA: 22 current docs, **9,271 sections** (incl. DFSA-PRU 73). All 17 unique template
  refs resolve exactly (75 entries, 0 dangling).
- **DFSA-PIB truncated:** chapters present 1–7 (ch. 7 only 10 sections) + App C; 93
  PIB refs are cited-in-corpus-but-missing (whole of ch. 7.3+, 8, 10, 11, 12, 13, 14) —
  capital-requirement calculations beyond base capital are not draftable from corpus.
- **DFSA-PIN:** 104 cited-but-missing (chapters >10 essentially absent) — insurance
  categories out of scope for this matrix anyway.
- **DFSA-PRU:** 73 sections covering ch. 1, 2, 6 only — partial revival, still on the
  re-scrape park list.
- **DFSA-GLO:** 17 sections for a 92k-char glossary — coarse parse, defined-term
  lookups degraded.
- **Tier 0 / DIFC company law:** `DIFC-CL` doc 2656 ("DIFC Companies Law No. 5 of 2018,
  Consolidated March 2022"), **154 sections (s.1–s.154+), is_current=1 — present and
  usable.** But the other DIFC legislation is stub-parsed: Collective Investment Law
  **0 sections**, Investment Trust Law **0 sections**, Islamic Financial Business Law
  1, Markets Law 7, Regulatory Law 9, Crypto Token suitability guidance (doc 2428)
  0 sections / 34k words. Tier-0 row is honestly **DIFC-CL-only** until K4's lane
  re-parses the rest (Collective Investment Law matters for 3C fund managers).
