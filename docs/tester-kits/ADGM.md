# ADGM — Tester Kit (L7 walkthrough skeleton)

**Prepared:** 2026-06-11 (MAX-6 N5, sprint/max6-k-drafts). Register L7 (deps: L6).
**Status:** skeleton — populated with entity shapes, smallest-template walkthrough, activation caveats and defect routes; golden links pending N1.
**Goldens: see overnight N1 results — populate links after N1 lands.**

## 1. Who you are pretending to be (fictional entity shapes)

Use these personas exactly — they are the L6 fictional customers from `qanun-api/scripts/e2e_validation.py` (`FICTIONAL_ENTITIES`), and the L2 suite-acceptance harness (`scripts/l2_suite_acceptance.py::seed_entity`) seeds the same first-match persona, so tester runs and harness runs draft for identical shapes.

### Persona A — Almahra Capital Partners Ltd (primary; also the L2 entity for ADGM)
- `entity_id` convention: `e2e-adgm-cat3c-0001` · **Category 3C** (`ADGM-CAT3C`)
- Al Maryah Island, ADGM, Abu Dhabi, UAE
- Activities: Managing Assets; Managing a Collective Investment Fund; Advising on Investments
- Fund manager: yes · Retail clients: no · AML obligations: yes
- Profile: AUM USD 250m–500m; 11–25 staff; discretionary managed accounts + a Qualified Investor Fund; institutional/professional clients only; PEP exposure low

### Persona B — Khaleej Markets Trading Ltd
- `e2e-adgm-cat3a-0001` · **Category 3A** (`ADGM-CAT3A`)
- ADGM Square, Abu Dhabi, UAE
- Activities: Dealing in Investments as Principal; Dealing in Investments as Agent
- Profile: listed equities, FX forwards, fixed income; 26–50 staff; PEP exposure low

> Fallback note: if the harness finds no jurisdiction match it seeds `l2-adgm-0001` ("L2 Acceptance ADGM Ltd", category_3c) — testers should not normally see this shape.

## 2. Smallest-template walkthrough (warm-up run)

Smallest active ADGM template by section count: **`terms_of_reference_committees` — "Terms of Reference — Board and Committees", 6 sections, Tier 3** (registry survey 2026-06-11).

1. Sign in; complete onboarding as Persona A (Cat 3C, post-authorisation stage).
2. ADGM **is** live in the single-document flow (`compliance/documents/new`): select ADGM → `terms_of_reference_committees`.
3. Answer the pre-draft questionnaire — ADGM is the only jurisdiction with `entity_fact_questions` (MLRO, SEO, AUM, PEP exposure…). Note any question that doesn't fit the persona: that's a finding, not your error.
4. Draft → review each section: check every citation cites FSRA/ADGM sources only, headings match the ToR scope, committee structure is consistent with an 11–25-staff Cat 3C.
5. Export DOCX; confirm no `[[Placeholder]]` tokens survive except deliberate `[TO BE CONFIRMED]` facts you declined to provide.
6. Compare against the golden output — **goldens: see overnight N1 results — populate links after N1 lands.**
7. Scale-up runs (after warm-up): `aml_cft_policy` and `business_risk_assessment` (the L6/E2E matrix cells for Persona A).

## 3. What is expected to be rough (activation caveats — from `docs/activation-packs/ADGM.md`)

- **No Tier-1 registration pack exists** (0 templates) — do not test pre-application/application scenarios; ADGM is currently for already-authorised firms.
- No J1 per-licence matrix and **0 ADGM suites** — full-suite drafting is not testable; single documents only.
- `compliance_manual` (the flagship 31-section template) carries **21 stale section-ids** — expect citation defects there; log them, they are known.
- Wizard licence list missing Cat 3B, Cat 4, Cat 5.
- FSRA corpus quality tail: ~1,900 dangling citation targets (IFR 6/7/8 parser gaps) — a wrong-looking IFR citation may be a corpus gap rather than a drafting hallucination; report it either way.
- J6–J8 sections (ADGM Returns, FATCA-CRS, Economic Substance) absent from the compliance manual — known gaps.

## 4. Reporting defects

- **Once the support endpoint is live:** `POST /api/support/contact` (qanun-api `routers/support.py`, behind `enable_support_contact` — default OFF as of MAX-6) / the in-app contact form that fronts it.
- **Meanwhile (K7 mailbox pattern):** email **support@qanun.io** — subject `[TESTER][ADGM] <template> — <one-line defect>`.
- Include: persona used, template id, section number, the offending citation/text verbatim, expected vs actual, export file if relevant.

## 5. Verification checklist (what good looks like)

- [ ] Every citation resolves in Quick Lookup to a current FSRA/ADGM provision
- [ ] No non-ADGM rulebooks cited (no DFSA/VARA bleed-through)
- [ ] Entity facts from the questionnaire appear correctly in the draft
- [ ] DOCX export opens clean; styles intact; no scrubber survivors
- [ ] Draft matches golden within reasonable variation — **goldens: see overnight N1 results — populate links after N1 lands**
