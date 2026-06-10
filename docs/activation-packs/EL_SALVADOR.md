# EL SALVADOR — Activation Pack (J3 / J15 / J18 / J19)

**Prepared:** 2026-06-10 (MAX-4 V5, sprint/max4-j-packs)
**For:** Oliver's J3 human activation gate
**Authoritative matrix:** `SV_DOCUMENTS` in `~/ADGM/adgm-corpus/ucie/agents/template_discovery_agent.py::_run_el_salvador` — the suite **Oliver-approved 29 March 2026** (review memo `~/ADGM/adgm-corpus/output/EL_SALVADOR_template_review.md`). Note: the approval memo says "APPROVED — 53 documents" but the code list, coverage CSV and registry all carry **52** — the count in the memo is off by one (post-amendment consolidation); the 52-row list is the operative set.

---

## 1. Registry state

`TEMPLATE_REGISTRY` ← `services/sv_templates.py`: **52 `sv_*` templates** of 162 total.

Per-tier: T1 = 13 (incl. BSP BCR pack + Certifier framework) · T2 = 13 · T3 = 7 · T4 = 9 · T5 = 10.

**Suite activation state: 0 suites.** `emit_suite_json()` in the TemplateDiscoveryAgent **does not support EL_SALVADOR** — `_normalised_documents()` returns `[]` for SV ("VARA is the Option-C smoke target; SV emit is a follow-up"). No `ucie/jurisdictions/EL_SALVADOR/discovered_templates/` directory exists, so `SUITE_REGISTRY` carries no SV suites and tier-ordered suite drafting (cross-tier context propagation, I3) is unavailable for SV.

## 2. Matrix coverage

**Doc-level coverage: 52/52 = 100%.** Every approved matrix document has a matching registry template; zero registry extras (1:1 reconciliation).

### 2.1 Per-licence-type coverage (10 SV categories)

| Licence type | T1 | T2 | T3 | T4 | T5 | Total req | Templates exist | Coverage |
|---|---|---|---|---|---|---|---|---|
| SV-DASP-EX | 9 | 12 | 7 | 8 | 7 | 43 | 43 | 100% |
| SV-DASP-CUST | 9 | 11 | 7 | 5 | 7 | 39 | 39 | 100% |
| SV-DASP-PLAT | 9 | 11 | 7 | 6 | 7 | 40 | 40 | 100% |
| SV-DASP-STR | 8 | 10 | 7 | 5 | 7 | 37 | 37 | 100% |
| SV-DASP-XFER | 9 | 11 | 7 | 5 | 7 | 39 | 39 | 100% |
| SV-DASP-INV | 8 | 10 | 7 | 5 | 7 | 37 | 37 | 100% |
| SV-BSP | 9 | 10 | 7 | 4 | 7 | 37 | 37 | 100% |
| SV-DASP-ISS | 10 | 11 | 7 | 4 | 7 | 39 | 39 | 100% |
| SV-STBL-ISS | 9 | 11 | 7 | 4 | 10 | 41 | 41 | 100% |
| SV-CERT | 8 | 10 | 7 | 4 | 7 | 36 | 36 | 100% |

### 2.2 Punch-list extract (track-specific rows; ALL-rows omitted — all Y)

All 52 rows reconcile Y. Track-specific highlights:

| Tier | Required document | Applies to | Exists | Template id |
|---|---|---|---|---|
| 1 | BSP BCR Registration Pack | SV-BSP | Y | `sv_bsp_bcr_registration_pack` |
| 1 | Certifier Appointment Framework | SV-DASP-ISS | Y | `sv_certifier_appointment_framework` |
| 1 | Digital Asset List w/ Commercial & Financial Restrictions | EX, PLAT, XFER, CUST | Y | `sv_digital_asset_list` |
| 1 | RID — Issuance Prospectus | SV-DASP-ISS | Y | `sv_rid_issuance_prospectus_full` |
| 1 | Stablecoin Issuance Notification | SV-STBL-ISS | Y | `sv_stablecoin_issuance_notification` |
| 2 | FATF Travel Rule Compliance Procedure | EX, XFER, CUST | Y | `sv_travel_rule_procedure` |
| 2 | Market Abuse and Insider Trading Policy | EX, PLAT, ISS | Y | `sv_market_abuse_policy` |
| 2 | Reserve Asset Management Policy | SV-STBL-ISS | Y | `sv_reserve_asset_management_policy` |
| 4 | Custody and Wallet Operations Manual | CUST, EX | Y | `sv_custody_wallet_operations` |
| 4 | Investment Product Management Manual | INV, STR | Y | `sv_investment_product_manual` |
| 5 | Stablecoin Monthly Reserve Affidavit | SV-STBL-ISS | Y | `sv_stablecoin_monthly_affidavit` |
| 5 | Stablecoin Quarterly Reserve Attestation | SV-STBL-ISS | Y | `sv_stablecoin_quarterly_attestation` |
| 5 | Stablecoin API Issuance/Destruction Report Spec | SV-STBL-ISS | Y | `sv_stablecoin_api_report` |

(Full 52-row table reproducible from `/tmp/sv_recon.json` script in the evidence pack; doc-level table held to highlights for brevity since coverage is 100%.)

## 3. Questionnaire gaps affecting EL_SALVADOR (J18)

- `GovernanceOnboardingWizard.tsx` offers only **4 of 10** SV categories (DASP-EX, DASP-CUST, DASP-PLAT, DASP-XFER). **Missing: SV-DASP-STR, SV-DASP-INV, SV-BSP, SV-DASP-ISS, SV-STBL-ISS, SV-CERT** — the entire stablecoin, BSP/BCR and issuance tracks (14 track-specific templates) are unreachable from the UI.
- Stage options: only "Registered — CNAD". **No pre-registration stage**, despite Tier 1 being a Registration Pack — pre-application firms cannot represent their state.
- **Zero `entity_fact_questions` on all 52 SV templates** — no capture of UIF-registered MLRO/Oficial de Cumplimiento details (J15 calls this out explicitly), CNAD registration number, or reserve-asset banking partners for STBL-ISS.
- No bilingual/Spanish-language preference field (J15: LEAD is operative legislation; key documents need bilingual support consideration).
- `BusinessModelClassifier` is ADGM-only; no SV classification path.

## 4. J19 category-tailoring spot-check

- Sampled `sv_reserve_asset_management_policy`: `category_tailoring` = {} — and `grep -c category_tailoring services/sv_templates.py` = 0 → **no SV template has category-conditional content**. Track differentiation exists only via the applies-to doc lists. **J19 fully open for SV.**
- Provision spot-check (corpus.db, mode=ro): `SV-STBL Art.4` → EXACT section row; `SV-STBL Art.11` → EXACT. Refs are correctly formed against the SV corpus (16 current EL_SALVADOR documents).

## 5. Corpus caveats (from LAUNCH_VERDICT_20260610)

- ES rulebook-code issues resolved at LC2 (🟢); no SV-specific items on the park list.
- Spanish-primary citation convention applies (SV-*-ES primary, EN secondary) per the approved review memo — drafting outputs cite the Spanish authoritative texts.
- Corpus footprint is comparatively small (16 current docs) — adequate for the approved matrix (52/52 READY at discovery time, CSV on file) but thinner than VARA/ADGM for semantic retrieval.

## 6. Evidence — L2 sample drafts

**PENDING E2E RUN** — placeholder for V1's L2 sample drafts (suggest SV-DASP-EX Tier 1–2 and one SV-STBL-ISS Tier 5 filing template to exercise the stablecoin track).

## 7. RECOMMENDATION

**ACTIVATE-WITH-CAVEATS (DASP-EX/CUST/PLAT/XFER tracks only); HOLD the STBL-ISS / BSP / ISS / CERT tracks** — matrix is human-approved and 100% template-covered, but the suite-emit pipeline doesn't support SV yet, six categories (including all stablecoin/issuance tracks) are unreachable from the questionnaire, and no entity-fact questions or tailoring exist.
