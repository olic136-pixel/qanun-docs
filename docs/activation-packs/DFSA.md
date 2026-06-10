# DFSA — Activation Pack (J4 / J16 / J18 / J19)

**Prepared:** 2026-06-10 (MAX-4 V5, sprint/max4-j-packs)
**For:** Oliver's J4 human activation gate
**Authoritative matrix:** **none exists.** Register J4/J16 (Open, "v1 scope expansion") require a per-licence-type (DFSA Cat 1–5) × tier matrix; `TemplateDiscoveryAgent` HALTs for DFSA. The 18 existing templates are a single-track 5-tier set in `services/dfsa_templates.py` with no per-category differentiation.

---

## 1. Registry state

`TEMPLATE_REGISTRY` ← `services/dfsa_templates.py`: **18 `dfsa_*` templates** of 162 total.

| Tier | Count | Templates |
|---|---|---|
| 1 — Registration Pack | 4 | dfsa_application_form, dfsa_regulatory_business_plan, dfsa_fit_proper_declarations, dfsa_technology_systems_description |
| 2 — Mandatory Compliance | 3 | dfsa_aml_cft_programme_difc, dfsa_compliance_manual_difc, dfsa_conflicts_policy |
| 3 — Corporate Governance | 3 | dfsa_board_charter, dfsa_senior_management_responsibilities, dfsa_whistleblowing_policy |
| 4 — Operational Procedures | 5 | dfsa_client_onboarding_procedure, dfsa_order_execution_policy, dfsa_incident_response, dfsa_bcp, dfsa_data_protection |
| 5 — Filings & Monitoring | 3 | dfsa_compliance_monitoring_programme, dfsa_annual_compliance_report, dfsa_mlro_annual_report |

**Suite activation state: 0 DFSA suites** in `SUITE_REGISTRY`.

## 2. Matrix coverage

**Not computable — no J4 matrix.** Structural punch-list against the 5-tier logical map (`cross-jurisdiction-document-map.md`):

| Jurisdiction | Licence type | Tier | Required doc (logical) | Template exists | Id / GAP |
|---|---|---|---|---|---|
| DFSA | Cat 1–5 (undifferentiated) | 1–5 | 18 single-track docs | Y | all 18 ids above |
| DFSA | per-category | any | per-category requirement lists (Cat 1 bank vs Cat 4 advisory etc.) | N | **GAP — J4 discovery not run; no category differentiation anywhere** |
| DFSA | all | 2 | KYC/CDD procedures (logical-map Tier 2 slot) | N | **GAP** (no dfsa_kyc_cdd; AML programme partially covers) |
| DFSA | all | 2 | Outsourcing policy (logical-map slot) | N | **GAP** |
| DFSA | all | 2 | Complaints handling (logical-map slot) | N | **GAP** |
| DFSA | dealing/custody cats | 4 | Client Money / Custody operations (COB) | N | **GAP** |

Indicative coverage vs the logical 5-tier map: **18 of ~24 logical slots ≈ 75% single-track; 0% per-licence-type** (no matrix, no tailoring).

## 3. Questionnaire gaps affecting DFSA (J18) — **blocking**

- **`GovernanceOnboardingWizard.tsx` has no DFSA group at all** — neither licence categories nor stages. The governance-suite path cannot create a DFSA profile; the 18 templates are reachable only via the single-document flow (`compliance/documents/new`, which does list DIFC/DFSA).
- **Zero `entity_fact_questions` on all 18 DFSA templates.**
- No DFSA category capture (Cat 1–5), no Authorised Individuals / SMR fields, no DFSA firm-reference number.
- `BusinessModelClassifier` is ADGM-only.

## 4. J19 category-tailoring spot-check

- Sampled `dfsa_compliance_manual_difc`: `category_tailoring` = {} — `grep -c category_tailoring services/dfsa_templates.py` = 0 → **J19 fully open for DFSA.**
- Provision spot-check (corpus.db, mode=ro): `DFSA-GEN 5.3` → EXACT (note: the LC7 "DFSA-GEN 5.3 class" dangling-ref family appears resolved for this ref post-MAX-3 DFSA prefixing); `DFSA-AML 4.1` → EXACT. 2/2 resolve.

## 5. Corpus caveats (from LAUNCH_VERDICT_20260610) — material here

- **DFSA-PRU is a stub:** doc 2828 re-scrape is on the park list and 334 held-back vectors await purge — **prudential/capital-adequacy drafting for DFSA-adjacent advice is degraded** until the re-scrape lands (register carry: task "(b) DFSA-PRU 2828 re-scrape design" is in progress in the swarm).
- LC7: 42 unique dangling template refs are characterised as "DFSA-GEN 5.3 class" — template-ref hygiene for DFSA needs a sweep even though the sampled refs resolve.
- DFSA corpus: 22 current docs — thin next to FSRA/VARA.

## 6. Evidence — L2 sample drafts

**PENDING E2E RUN** — placeholder for V1's L2 sample drafts (suggest dfsa_compliance_manual_difc + dfsa_aml_cft_programme_difc; avoid prudential content until DFSA-PRU re-scrape).

## 7. RECOMMENDATION

**HOLD** — no per-category matrix (J4 not run), no governance-wizard path at all (suites unreachable end-to-end), zero tailoring/questionnaires, and the DFSA-PRU corpus stub degrades prudential content; single-document drafting can remain quietly available, but do not present DFSA as an activated jurisdiction at the gate.
