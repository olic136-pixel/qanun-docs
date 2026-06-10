# VARA — Activation Pack (J2 / J10–J14 / J18 / J19)

**Prepared:** 2026-06-10 (MAX-4 V5, sprint/max4-j-packs)
**For:** Oliver's J2 human activation gate
**Authoritative matrix:** `VARA_PROPOSED_DOCUMENTS` in `~/ADGM/adgm-corpus/ucie/agents/template_discovery_agent.py` (37 documents, UCIE v2 SOW §6.1), 8 licence types (`VARA_LICENCE_TYPES`), 5-tier model (`TIER_NAMES`).

---

## 1. Registry state

`TEMPLATE_REGISTRY` (qanun-api `services/drafting_templates.py` ← `services/vara_templates.py` + 12 hand-authored Tier-3/4/5 overrides): **47 `vara_*` templates** of 162 total.

Per-tier (matrix-mapped): T1 = 7 · T2 = 11 · T3 = 8 · T4 = 6 · T5 = 5 (37 matrix docs) + 10 registry entries outside the matrix (see §2.3).

**Suite activation state (`SUITE_REGISTRY` via `template_discovery_loader`):** 1 of 40 licence-type × tier suite slots registered — `vara_vasp_bd_tier1` (`_review_status: "approved"`, 7 docs) at `ucie/jurisdictions/VARA/discovered_templates/vasp_bd/tier1.json`. **The other 39 slots have no emitted/approved suite JSON.**

## 2. Matrix coverage

**Doc-level coverage: 37/37 = 100%.** Every matrix document has a matching registry template (name-match score ≥ 0.5; majority exact).

### 2.1 Per-licence-type coverage

| Licence type | T1 | T2 | T3 | T4 | T5 | Total req | Templates exist | Coverage |
|---|---|---|---|---|---|---|---|---|
| VASP-BD | 7 | 11 | 8 | 6 | 5 | 37 | 37 | 100% |
| VASP-CUST | 7 | 11 | 8 | 5 | 5 | 36 | 36 | 100% |
| VASP-EX | 7 | 11 | 8 | 6 | 5 | 37 | 37 | 100% |
| VASP-ADV | 7 | 9 | 8 | 4 | 5 | 33 | 33 | 100% |
| VASP-MGMT | 7 | 10 | 8 | 5 | 5 | 35 | 35 | 100% |
| VASP-LB | 7 | 9 | 8 | 4 | 5 | 33 | 33 | 100% |
| VASP-TRS | 7 | 10 | 8 | 4 | 5 | 34 | 34 | 100% |
| VASP-ISS | 7 | 9 | 8 | 4 | 5 | 33 | 33 | 100% |

### 2.2 Punch-list (doc level — no gaps)

| Tier | Required document | Applies to | Template exists | Template id |
|---|---|---|---|---|
| 1 | AML/CFT Programme Summary | ALL | Y | `vara_amlcft_programme_summary` |
| 1 | Business Plan and Activity Description | ALL | Y | `vara_business_plan_and_activity_description` |
| 1 | Corporate Structure Chart and UBO Declarations | ALL | Y | `vara_corporate_structure_chart_and_ubo_declarations` |
| 1 | Fit and Proper Declarations — Senior Management | ALL | Y | `vara_fit_and_proper_declarations_senior_management` |
| 1 | IDQ Completion Pack | ALL | Y | `vara_idq_completion_pack` |
| 1 | Initial Capital Evidence Statement | ALL | Y | `vara_initial_capital_evidence_statement` |
| 1 | Technology Architecture Statement | ALL | Y | `vara_technology_architecture_statement` |
| 2 | AML/CFT Policy and Procedures Manual | ALL | Y | `vara_amlcft_policy_manual` |
| 2 | Complaints Policy and Procedure | ALL | Y | `vara_complaints_policy_and_procedure` |
| 2 | Conflicts of Interest Policy | ALL | Y | `vara_conflicts_of_interest_policy` |
| 2 | Consumer and Client Protection Policy | ALL | Y | `vara_consumer_and_client_protection_policy` |
| 2 | Custody and Safeguarding Policy | VASP-CUST, VASP-EX, VASP-BD, VASP-MGMT | Y | `vara_custody_and_safeguarding_policy` |
| 2 | Cybersecurity and Information Security Policy | ALL | Y | `vara_cybersecurity_and_information_security_policy` |
| 2 | KYC/CDD Procedures Manual | ALL | Y | `vara_kyccdd_procedures_manual` |
| 2 | Market Conduct Policy | ALL | Y | `vara_market_conduct_policy` |
| 2 | Marketing and Promotions Compliance Policy | ALL | Y | `vara_marketing_and_promotions_compliance_policy` |
| 2 | Outsourcing Policy | ALL | Y | `vara_outsourcing_policy` |
| 2 | Travel Rule Compliance Procedures | VASP-BD, VASP-EX, VASP-TRS, VASP-CUST | Y | `vara_travel_rule_compliance_procedures` |
| 3 | Audit Committee Terms of Reference | ALL | Y | `vara_audit_committee_terms_of_reference` |
| 3 | Board of Directors Charter | ALL | Y | `vara_board_of_directors_charter` |
| 3 | Delegation of Authority Matrix | ALL | Y | `vara_delegation_of_authority_matrix` |
| 3 | Related Party Transactions Policy | ALL | Y | `vara_related_party_transactions_policy` |
| 3 | Remuneration Policy | ALL | Y | `vara_remuneration_policy` |
| 3 | Risk Committee Terms of Reference | ALL | Y | `vara_risk_committee_terms_of_reference` |
| 3 | Senior Management Responsibilities Map | ALL | Y | `vara_senior_management_responsibilities_map` |
| 3 | Whistleblowing Policy | ALL | Y | `vara_whistleblowing_policy` |
| 4 | Business Continuity Plan | ALL | Y | `vara_business_continuity_plan` |
| 4 | Client Onboarding Procedure | ALL | Y | `vara_client_onboarding_procedure` |
| 4 | Custody Operations Manual | VASP-CUST, VASP-EX, VASP-BD | Y | `vara_custody_operations_manual` |
| 4 | Data Protection and Privacy Policy | ALL | Y | `vara_data_protection_and_privacy_policy` |
| 4 | Incident Response and Technology Recovery Procedure | ALL | Y | `vara_incident_response_and_technology_recovery_procedure` |
| 4 | Order Execution Policy | VASP-BD, VASP-EX, VASP-MGMT | Y | `vara_order_execution_policy` |
| 5 | Annual Compliance Report to Board | ALL | Y | `vara_annual_compliance_report_to_board` |
| 5 | Compliance Monitoring Programme | ALL | Y | `vara_compliance_monitoring_programme` |
| 5 | Internal Audit Plan Template | ALL | Y | `vara_internal_audit_plan_template` |
| 5 | MLRO Annual Report Template | ALL | Y | `vara_mlro_annual_report_template` |
| 5 | Regulatory Examination Preparation Pack | ALL | Y | `vara_regulatory_examination_preparation_pack` |

### 2.3 Registry entries outside the matrix — duplicate-concept hazard

10 `vara_*` registry templates are not matrix rows. 7 are **duplicate-concept pairs** with different `doc_type` keys (hand-authored "Tier 3 takes precedence" block at `drafting_templates.py:8144` vs `vara_templates.py` module versions) — the drafting flow can pick either key for the same logical document:

| Hand-authored key | Module key (matrix-matched) |
|---|---|
| `vara_board_charter` | `vara_board_of_directors_charter` |
| `vara_senior_management_responsibilities` | `vara_senior_management_responsibilities_map` |
| `vara_delegation_of_authority` | `vara_delegation_of_authority_matrix` |
| `vara_incident_response_procedure` | `vara_incident_response_and_technology_recovery_procedure` |
| `vara_data_protection_policy` | `vara_data_protection_and_privacy_policy` |
| `vara_mlro_annual_report` | `vara_mlro_annual_report_template` |
| `vara_examination_prep_pack` / `vara_annual_compliance_report` | `vara_regulatory_examination_preparation_pack` / `vara_annual_compliance_report_to_board` |

Genuinely additive (not in matrix, keep): `vara_quarterly_mis_report`, `vara_annual_regulatory_return`.

**Punch item:** deduplicate or alias the 7 pairs before suite activation so each suite slot binds one canonical `doc_type`.

## 3. Questionnaire gaps affecting VARA (J18)

- `GovernanceOnboardingWizard.tsx` offers only 5 of 8 VARA licence types: **VASP-LB, VASP-TRS, VASP-ISS are not selectable** — their suites are unreachable from the UI.
- Stage options exist (Registration Pending / Registered) — adequate.
- **Zero `entity_fact_questions` on all 47 VARA templates** (`_TEMPLATE_QUESTIONS` covers ADGM's 23 only) — every VARA draft proceeds with no pre-draft questionnaire, so MLRO name, board composition, custody arrangements etc. all render as `[TO BE CONFIRMED]`.
- No capture of: entity legal form, activity multi-select, VARA registration/IDQ number, Responsible Individuals.
- `BusinessModelClassifier` is FSRA/ADGM-only (hard rules and categories hardcoded); no VARA classification path.

## 4. J19 category-tailoring spot-check

- Sampled `vara_custody_and_safeguarding_policy`: **`category_tailoring` = {} — no per-licence-type conditional content.** `grep -c category_tailoring services/vara_templates.py` = 0 → true for all 47 VARA templates. Licence-type differentiation currently comes only from the suite doc-list (which docs apply), not from within-document tailoring. **J19 remains fully open for VARA.**
- Provision spot-check (corpus.db, mode=ro): `VARA-CUST III` and `VARA-CRM V` are part-level refs — no exact section row, but resolve to 36 and 27 child sections respectively (consistent with LC7's "VARA part refs verified 25/25"). Verdict: refs sound at part level; acceptable.

## 5. Corpus caveats (from LAUNCH_VERDICT_20260610)

- **VARA fully re-parsed:** 2,112/2,112 vector parity local↔Pinecone; part refs verified 25/25 against the re-parsed corpus. Strongest corpus of the five.
- Park-list residual: **VARA-ISS 40 NULLed citations re-extraction** — affects citation enrichment for VASP-ISS issuance documents only.
- Overall verdict CONDITIONAL-GO; no VARA-specific data-integrity blocker.

## 6. Evidence — L2 sample drafts

**PENDING E2E RUN** — placeholder for V1's L2 sample drafts (VASP-BD Tier 1 suite is the natural smoke target; suite `vara_vasp_bd_tier1` already approved + loaded, 7 docs).

## 7. RECOMMENDATION

**ACTIVATE-WITH-CAVEATS** — 100% matrix coverage on a re-parsed, parity-verified corpus and one approved suite already loading end-to-end; caveats: only 1/40 suite slots approved (emit + approve the remaining 39), 7 duplicate doc_type pairs to dedupe, no entity-fact questionnaires, no category tailoring (J19), and 3 licence types missing from the wizard.
