# BVI — Activation Pack (J5 / J17 / J18 / J19)

**Prepared:** 2026-06-10 (MAX-4 V5, sprint/max4-j-packs)
**For:** Oliver's J5 human activation gate
**Authoritative matrix:** **none exists.** Register J5/J17 (Open, "v1 scope expansion") require per-licence-type (Approved Manager, Restricted Manager, Business Companies, Mutual Fund Manager, Investment Business, VASP) × tier matrices; `TemplateDiscoveryAgent` HALTs for BVI. The 12 existing templates in `services/bvi_templates.py` are a single-track partial set.

---

## 1. Registry state

`TEMPLATE_REGISTRY` ← `services/bvi_templates.py`: **12 `bvi_*` templates** of 162 total.

| Tier | Count | Templates |
|---|---|---|
| 1 — Registration Pack | 4 | bvi_approved_manager_application, bvi_vasp_application, bvi_regulatory_business_plan, bvi_fit_proper_declaration |
| 2 — Mandatory Compliance | 5 | bvi_aml_cft_programme_bvi, bvi_compliance_manual_bvi, bvi_kyc_cdd_procedures, bvi_conflicts_policy_bvi, bvi_outsourcing_policy_bvi |
| 3 — Corporate Governance | 3 | bvi_board_charter_bvi, bvi_senior_management_map, bvi_whistleblowing_bvi |
| 4 — Operational Procedures | **0** | — |
| 5 — Filings & Monitoring | **0** | — |

**Suite activation state: 0 BVI suites** in `SUITE_REGISTRY`.

## 2. Matrix coverage

**Not computable — no J5 matrix.** Structural punch-list against the 5-tier logical map:

| Jurisdiction | Licence type | Tier | Required doc (logical) | Template exists | Id / GAP |
|---|---|---|---|---|---|
| BVI | Approved Manager / VASP | 1 | application + business plan + F&P | Y | 4 ids above (two licence tracks share T1 docs) |
| BVI | Restricted Manager | 1 | application variant | N | **GAP — licence type not represented** |
| BVI | Mutual Fund Manager / Business Companies | 1 | application variants | N | **GAP** |
| BVI | all | 2 | complaints procedure (logical-map slot) | N | **GAP** |
| BVI | all | 2 | client asset protection (logical-map slot) | N | **GAP** |
| BVI | all | 4 | **entire tier** — onboarding, incident response, BCP, transaction monitoring, SAR procedure | N | **GAP — Tier 4 = 0 templates** |
| BVI | all | 5 | **entire tier** — compliance monitoring programme, MLRO annual report, FSC filings | N | **GAP — Tier 5 = 0 templates** |

Indicative coverage vs the logical 5-tier map: tiers 1–3 partially covered (~60–70% single-track), **tiers 4–5 at 0%**; per-licence-type coverage 0% (no matrix, two of ~5 licence types have any Tier-1 doc).

## 3. Questionnaire gaps affecting BVI (J18)

- Wizard offers Approved Manager, Investment Business, Mutual Fund — **missing Restricted Manager, Business Companies, VASP** (ironically `bvi_vasp_application` exists but VASP isn't selectable).
- Stage options (pre-application / registered) exist — adequate but minimal.
- **Zero `entity_fact_questions` on all 12 BVI templates;** no capital-adequacy framing per Approved vs Restricted Manager (J19 register example), no FSC certificate number capture.
- BVI is absent from the single-document drafting page's jurisdiction list (`compliance/documents/new` offers ADGM/VARA/DFSA/EL_SALVADOR only) — BVI templates reachable only via the governance wizard, the inverse of the DFSA situation.
- `BusinessModelClassifier` is ADGM-only.

## 4. J19 category-tailoring spot-check

- Sampled `bvi_aml_cft_programme_bvi`: `category_tailoring` = {} — `grep -c category_tailoring services/bvi_templates.py` = 0 → **J19 fully open for BVI.** (The register's own J19 example — capital adequacy framing Approved vs Restricted Manager — has no code expression.)
- Provision spot-check (corpus.db, mode=ro): `BVI-RC Sec.69` → EXACT; `BVI-RC Sec.39` → EXACT. 2/2 resolve. Note the sampled template's 5 sections carry only 2 required_provisions total — thin grounding relative to other jurisdictions.

## 5. Corpus caveats (from LAUNCH_VERDICT_20260610)

- **BVI-BCA doc 2756 fine re-parse** is on the park list (register carry "(c)") — Business Companies Act granularity is coarse until it lands; affects company-law-grounded sections (corporate documentation, board charters).
- BVI_FSC corpus: 27 current docs — thin; template grounding already sparse (see §4).

## 6. Evidence — L2 sample drafts

**PENDING E2E RUN** — placeholder for V1's L2 sample drafts (suggest bvi_approved_manager_application + bvi_aml_cft_programme_bvi if sampled at all; expect thin provision grounding).

## 7. RECOMMENDATION

**HOLD** — tiers 4–5 have zero templates (a firm cannot get an operating-state document set), no per-licence matrix (J5 not run), no tailoring/questionnaires, VASP track unreachable from the wizard, and the BCA fine re-parse is pending; tiers 1–3 single-track content is a useful seed for the J5 discovery run, not an activatable suite.

---

## 8. MAX-5 K2 ADDENDUM (2026-06-11, sprint/max5-jx-packs)

Supersedes §§1–2 and revises §7:

- **J5 matrix now exists:** `docs/matrices/BVI_J5_matrix.md` — 6 licence-type rows × 5 tiers; both launch-priority rows (BVI-APPROVED-MGR, BVI-VASP-CUST per the E2E cells) are 100% filled-or-N/A.
- **Registry 12 → 20 templates** (qanun-api sprint/max5-jx-templates): Tier 4 = 4 (client onboarding, registers maintenance on the BVI-BCA fine re-parse — Sec.41/91/96/98/118/162/163, transaction monitoring + SAR, incident response/BCP) and Tier 5 = 4 (periodic returns incl. BVI-REGS Reg.16 31-Jan annual return, AML independent audit, FSC notification filings on RC Schedule 3 time limits, compliance monitoring). Tiers 4–5 were 0/0 at V5.
- **Corpus caveat §5 cleared:** the BVI-BCA fine re-parse landed (265 sections); BVI corpus now 1,040 vectors. All 27 new required_provisions LIKE-verified; grounding floor test-pinned.
- **Still open before activation:** J18 questionnaire content (punch-list B1–B5 in `docs/tickets/MAX5_UI_punchlist_K6.md`), J19 tailoring, suite-emit + the suite endpoint doc_type derivation defect (X1), and E2E L2 sample-draft evidence (BVI cells now pass the fixed pipeline per MAX-5 E2E baseline).
- **Revised recommendation:** HOLD narrows from "structural" to **UI-reachability + questionnaire only** for the two launch-priority licence types.
