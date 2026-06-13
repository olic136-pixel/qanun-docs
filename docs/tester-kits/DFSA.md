# DFSA (DIFC) — Tester Kit (L7 walkthrough skeleton)

**Prepared:** 2026-06-11 (MAX-6 N5, sprint/max6-k-drafts). Register L7 (deps: L6).
**Status:** skeleton — populated with entity shapes, smallest-template walkthrough, activation caveats and defect routes; golden links pending N1.
**Goldens: see overnight N1 results — populate links after N1 lands.**

## 1. Fictional entity shapes (MAX5-E2E Phase 2 DFSA cells, `scripts/e2e_validation.py`; L2 harness seeds the first match)

### Persona A — Khalij Asset Management (DIFC) Ltd (primary; the L2 entity for DFSA)
- `e2e-dfsa-cat3c-0001` · **Cat 3C** (`DFSA-CAT3C`), Authorised Firm
- Gate Village 4, DIFC, Dubai, UAE
- Activities: Managing Assets; Managing a Collective Investment Fund; Advising on Financial Products
- Fund manager: yes · Professional Clients only · base capital US $140k; no client money (fund-custodian model)
- Profile: AUM USD 150m–300m; 11–25 staff; discretionary portfolio management + an Exempt Fund

### Persona B — Meydan Advisory Partners (DIFC) Ltd
- `e2e-dfsa-cat4-0001` · **Cat 4** (`DFSA-CAT4`), Authorised Firm
- Index Tower, DIFC, Dubai, UAE
- Activities: Advising on Financial Products; Arranging Deals in Investments
- Profile: corporate-finance advisory, private placements; 1–10 staff; US $30k base capital; no client assets; outsourced internal audit

> Vocabulary caution (activation pack §2): ADGM "Cat 3A matched principal" ≠ DFSA Cat 3A. DFSA matched principal = Cat 2-MP; DFSA Cat 3A = dealing as agent.

## 2. Smallest-template walkthrough (warm-up run)

Smallest active DFSA template: **`dfsa_bcp` — "Business Continuity Plan (DIFC)", 3 sections, Tier 4** (registry survey 2026-06-11).

1. Sign in. **Use the single-document flow** (`compliance/documents/new`) — DIFC/DFSA is live there; the governance wizard has **no DIFC/DFSA group yet** (J18-DFSA build pending in K6's UI lane).
2. Select DIFC/DFSA → `dfsa_bcp`; persona A facts entered manually (DFSA templates have zero `entity_fact_questions` — expect `[TO BE CONFIRMED]` for unprompted facts).
3. Review citations: DFSA ref shape `DFSA-MODULE C.S.R` — all 17 unique template refs verified 17/17 exact against the corpus, so dangling template citations are real defects here, not corpus noise.
4. Export DOCX; checklist §5.
5. Scale-up: the 8-cell E2E pack (activation pack §4) — Cat 3C: fit & proper, conflicts, senior-management responsibilities, compliance monitoring; Cat 4: fit & proper, whistleblowing, data protection, MLRO annual report.

## 3. Expected roughness (activation caveats — `docs/activation-packs/DFSA.md`, GO-PENDING-MATRIX-APPROVAL)

- **No wizard/questionnaire path**: backend `VALID_FSRA_CATEGORIES` rejects `dfsa_*` categories; suites only work with explicit `doc_types` (derivation defect). Single-doc flow is the tester surface.
- **Avoid prudential/capital-adequacy content**: DFSA-PIB parsed chapters 1–7 only (93 cited-but-missing refs in ch. 7.3–14); PRU partial; GLO glossary coarse. `dfsa_application_form` cites PIB — expect degraded grounding there.
- DIFC company law: DIFC-CL (154 sections) usable; Collective Investment Law / Investment Trust Law are 0-section stubs — fund-law citations for Cat 3C may misground; report them, they are known-class.
- Zero category tailoring (J19 open) — Cat 3C and Cat 4 get the same within-document content.
- 10 known template gaps (KYC/CDD, outsourcing, complaints, client money…) — absence of these from the catalogue is known, not a defect.

## 4. Reporting defects

- **Once live:** `POST /api/support/contact` (qanun-api `routers/support.py`, flag `enable_support_contact`, default OFF as of MAX-6) / in-app contact form.
- **Meanwhile:** **support@qanun.io** — subject `[TESTER][DFSA] <template> — <one-line defect>`. Include persona, template id, section, verbatim text, expected vs actual.

## 5. Verification checklist

- [ ] Citations DFSA-only, `DFSA-MODULE C.S.R` shape, resolve in Quick Lookup
- [ ] No ADGM/FSRA vocabulary bleed (especially category naming, §1 caution)
- [ ] No PIB ch. 8–14 citations presented as verified
- [ ] DOCX export clean
- [ ] Matches golden — **goldens: see overnight N1 results — populate links after N1 lands**
