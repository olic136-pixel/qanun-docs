# BVI — Tester Kit (L7 walkthrough skeleton)

**Prepared:** 2026-06-11 (MAX-6 N5, sprint/max6-k-drafts). Register L7 (deps: L6).
**Status:** skeleton — populated with entity shapes, smallest-template walkthrough, activation caveats and defect routes; golden links pending N1.
**Goldens: see overnight N1 results — populate links after N1 lands.**

## 1. Fictional entity shapes (from `scripts/e2e_validation.py` L6; L2 harness seeds the first match)

### Persona A — Road Town Digital Custody Ltd (primary; the L2 entity for BVI)
- `e2e-bvi-vaspcust-0001` · **VASP** (`BVI-VASP-CUST`)
- Road Town, Tortola, British Virgin Islands
- Activities: Virtual asset custody services; Safekeeping of virtual assets
- Profile: institutional VA custody, multi-sig cold storage; 11–25 staff; no retail; PEP exposure low

### Persona B — Sage Mountain Asset Management Ltd
- `e2e-bvi-apprmgr-0001` · **Approved Manager** (`BVI-APPROVED-MGR`)
- Wickhams Cay II, Road Town, Tortola, BVI
- Activities: Investment Management; Investment Advice · fund manager: yes
- Profile: AUM USD 100m–250m; an incubator fund + segregated mandates; 1–10 staff

> These are the two launch-priority licence rows in `docs/matrices/BVI_J5_matrix.md` (both 100% filled-or-N/A).

## 2. Smallest-template walkthrough (warm-up run)

Smallest active BVI template: **`bvi_aml_audit_programme` — "AML/CFT Independent Audit Programme (BVI)", 3 sections, Tier 5** (registry survey 2026-06-11; one of the 8 templates added at MAX-5 when Tiers 4–5 went 0 → 4+4).

1. Sign in; onboard as Persona B (Approved Manager — selectable in the wizard; **VASP is not selectable yet**, so Persona A runs only via routes that accept an explicit template id).
2. **BVI is absent from the single-document drafting page** — templates are reachable only via the governance wizard (the inverse of DFSA). If you cannot reach a template, that's the known UI-reachability HOLD, not a new defect.
3. Draft `bvi_aml_audit_programme`; expect `[TO BE CONFIRMED]` placeholders (zero `entity_fact_questions` on all BVI templates; no FSC certificate number capture).
4. Citations: `BVI-RC Sec.N` / `BVI-REGS Reg.N` / BVI-BCA section shapes. The BCA fine re-parse landed (265 sections) and all 27 MAX-5 provisions are LIKE-verified — but historic grounding is thin (some templates carry very few required_provisions), so sparse citation density is expected; *wrong* citations are defects.
5. Export DOCX; checklist §5.
6. Scale-up: Persona B — `bvi_approved_manager_application`, `bvi_compliance_manual_bvi`, `bvi_regulatory_business_plan`; Persona A — `bvi_vasp_application`, `bvi_kyc_cdd_procedures` (the L6/E2E matrix cells).

## 3. Expected roughness (activation caveats — `docs/activation-packs/BVI.md` + MAX-5 K2 addendum)

- Status: **HOLD narrowed to UI-reachability + questionnaire** for the two launch-priority licence types; structure (matrix, tiers 4–5, corpus re-parse) landed at MAX-5.
- Wizard missing Restricted Manager, Business Companies and VASP; no Tier-0/J18 questionnaire content (punch-list B1–B5 in `docs/tickets/MAX5_UI_punchlist_K6.md`).
- Zero category tailoring (J19) — no Approved-vs-Restricted capital-adequacy framing inside documents.
- Suite-emit + suite endpoint doc_type derivation defect (X1) — no BVI suite drafting; single documents only.
- BVI_FSC corpus is comparatively small (~1,040 vectors post re-parse) — semantic retrieval thinner than VARA/ADGM.

## 4. Reporting defects

- **Once live:** `POST /api/support/contact` (qanun-api `routers/support.py`, flag `enable_support_contact`, default OFF as of MAX-6) / in-app contact form.
- **Meanwhile:** **support@qanun.io** — subject `[TESTER][BVI] <template> — <one-line defect>`. Include persona, template id, section, verbatim text, expected vs actual.

## 5. Verification checklist

- [ ] Citations BVI-only (BVI-RC / BVI-REGS / BVI-BCA), resolve in Quick Lookup
- [ ] Registers-maintenance content grounded on the re-parsed BCA (Sec.41/91/96/98/118/162/163 class)
- [ ] Annual-return content reflects BVI-REGS Reg.16 (31 January) where relevant
- [ ] DOCX export clean
- [ ] Matches golden — **goldens: see overnight N1 results — populate links after N1 lands**
