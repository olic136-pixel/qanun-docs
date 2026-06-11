# BVI — J5 Per-Licence-Type × Tier Matrix (MAX-5 K2)

**Prepared:** 2026-06-11 (MAX-5 K2, sprint/max5-jx-packs)
**Closes:** launch-readiness register J5 (matrix) and the J17 Tier-4/5 template gap for the two launch-priority licence types.
**Template source:** `qanun-api services/bvi_templates.py` @ sprint/max5-jx-templates (**20 `bvi_*` templates** — 12 pre-existing Tier 1–3 + 8 new Tier 4–5).
**Corpus basis (all refs LIKE-verified, is_current=1, 2026-06-11):** BVI-SIBA (133 sections incl. Schedule 2 investment activities), BVI-BCA (265 fine sections, post re-parse), BVI-REGS (Approved Managers Regulations, Reg.1–18), BVI-RC (Sec.19/36/37/39/57/61/69, Schedules 1–6), BVI-AML (76), BVI-AMLR (21), BVI-VASP-AML-GUIDE (27), BVI-VASPA (Parts I–VI), BVI-MFA (8), BVI-MFR (4).

## 1. Licence-type taxonomy (rows)

| Code | Licence type | Source of regime | Launch priority |
|---|---|---|---|
| BVI-APPROVED-MGR | Approved Manager | Investment Business (Approved Managers) Regulations (BVI-REGS Reg.4–18) | **YES** (E2E cell `BVI-APPROVED-MGR`) |
| BVI-VASP-CUST | VASP — custody service | BVI-VASPA Part III registration; BVI-VASP-AML-GUIDE | **YES** (E2E cell `BVI-VASP-CUST`) |
| BVI-VASP-EX | VASP — exchange service | BVI-VASPA Parts II–III | no |
| BVI-SIBA-IB | Investment Business licensee (SIBA Schedule 2 activity categories: dealing, arranging, managing, advising, custody, administration, operating an exchange) | BVI-SIBA Part III + Schedule 2 | no |
| BVI-MF | Mutual fund (private / professional / public) and fund manager/administrator | BVI-MFA, BVI-MFR, BVI-SIBA | no |
| BVI-BC | Business company (unregulated — company-law obligations only) | BVI-BCA | no |

## 2. Matrix (template ids per tier; **bold** = added in MAX-5 K2)

Legend: ✓ = template exists and applies · GAP = required, no template · N/A = not required for this licence type (with reason).

### 2.1 BVI-APPROVED-MGR (launch priority — 19/19 slots filled, 0 GAP)

| Tier | Slot | Template |
|---|---|---|
| 1 | Application | bvi_approved_manager_application |
| 1 | Business plan | bvi_regulatory_business_plan |
| 1 | AML/CFT programme | bvi_aml_cft_programme_bvi |
| 1 | Fit & proper | bvi_fit_proper_declaration |
| 1 | VASP application | N/A — not a VASP |
| 2 | Compliance manual | bvi_compliance_manual_bvi |
| 2 | KYC/CDD | bvi_kyc_cdd_procedures |
| 2 | Conflicts | bvi_conflicts_policy_bvi |
| 2 | Outsourcing | bvi_outsourcing_policy_bvi |
| 3 | Board charter | bvi_board_charter_bvi |
| 3 | Senior management map | bvi_senior_management_map |
| 3 | Whistleblowing | bvi_whistleblowing_bvi |
| 4 | Client onboarding | **bvi_client_onboarding_procedures** |
| 4 | Registers & records maintenance | **bvi_registers_maintenance_procedures** (BVI-BCA Sec.41/91/96/98/118/162/163) |
| 4 | Transaction monitoring + SAR | **bvi_transaction_monitoring_sar_procedures** |
| 4 | Incident response / BCP | **bvi_incident_response_bcp** (BVI-RC Schedule 3 notification limits) |
| 5 | Periodic returns & financial filings | **bvi_periodic_returns_procedures** (BVI-REGS Reg.14/16 — annual return by 31 Jan; SIBA Reg.68–76) |
| 5 | AML independent audit | **bvi_aml_audit_programme** |
| 5 | FSC notifications & approvals | **bvi_fsc_notification_filings** (BVI-SIBA Reg.10/14/66; BVI-REGS Reg.13 14-day changes) |
| 5 | Compliance monitoring programme | **bvi_compliance_monitoring_programme** (BVI-REGS Reg.15 compliance officer) |

### 2.2 BVI-VASP-CUST (launch priority — 19/19 slots filled, 0 GAP)

Identical to §2.1 except: Tier 1 application slot = **bvi_vasp_application** (bvi_approved_manager_application = N/A); VASP-conditional sections activate in **bvi_client_onboarding_procedures** (s3, BVI-VASP-AML-GUIDE 7.2.1/7.5.1) and **bvi_transaction_monitoring_sar_procedures** (s2, BVI-VASP-AML-GUIDE 7.6.2/7.6.5). Custody-asset segregation is covered at Tier 1 by bvi_vasp_application s3 (technology, custody and cybersecurity controls). Remaining custody-specific operational manual (wallet operations runbook) is **deliberately N/A at v1**: VASPA resolves at Part level only in the corpus — a dedicated template would be ungroundable below Part granularity (park to post-launch corpus work).

### 2.3 BVI-VASP-EX (not launch priority)

As §2.2, plus two slots that stay **GAP — not corpus-groundable**: Tier 2 market-surveillance/listing policy and Tier 4 matching-engine operations (no exchange-conduct provisions below BVI-VASPA Part level in corpus). All other slots ✓ via the shared VASP set.

### 2.4 BVI-SIBA-IB

| Tier | State |
|---|---|
| 1 | **GAP** — Investment Business licence application variant (groundable: BVI-SIBA Part III + Schedule 2 + SIBA Reg.* fine rows exist; deferred — not launch priority); business plan / AML programme / F&P ✓ (shared) |
| 2–3 | ✓ shared set; NOTE: `applicable_entity_types` on the shared templates lists Approved Manager / Authorised Fund Manager / Registered Fund / VASP — add "Investment Business" when this row activates |
| 4–5 | ✓ shared Tier 4/5 set applies (SIBA Reg.68–76 grounding is licensee-generic); custody-of-client-assets procedure for Cat-custody firms = **GAP** (deferred with the row) |

### 2.5 BVI-MF

Tier 1 fund application/recognition variant = **GAP** (BVI-MFA/BVI-MFR are Part-level; groundable only coarsely — deferred). Tiers 2–5: ✓ shared set ("Registered Fund" is in applicable_entity_types); fund-specific NAV/valuation procedures = **GAP — not corpus-groundable** (no MFR fine sections).

### 2.6 BVI-BC (company formation track)

Tier 4 registers & records maintenance ✓ (**bvi_registers_maintenance_procedures** — the BVI-BCA re-parse consumer). All FSC tiers 1–3 and 5 = **N/A — unregulated entity, no FSC licence obligations**.

## 3. Summary

- **Launch-priority coverage: 100%** — every matrix slot for BVI-APPROVED-MGR and BVI-VASP-CUST is filled or explicitly N/A; Tier 4 = 4 templates, Tier 5 = 4 templates (was 0/0 at MAX-4 V5).
- New templates carry 27 required_provision entries, all LIKE-verified pre-commit; the previously thin grounding (2 refs on the sampled AML programme) does not recur — grounding floor ≥3 refs/template is test-pinned (`tests/test_max5_jx_templates.py`).
- Open GAPs are confined to non-launch rows (SIBA-IB application, MF application, exchange-conduct, NAV procedures) and are gap-listed above with groundability verdicts.
