# VARA — Tester Kit (L7 walkthrough skeleton)

**Prepared:** 2026-06-11 (MAX-6 N5, sprint/max6-k-drafts). Register L7 (deps: L6).
**Status:** skeleton — populated with entity shapes, smallest-template walkthrough, activation caveats and defect routes; golden links pending N1.
**Goldens: see overnight N1 results — populate links after N1 lands.**

## 1. Fictional entity shapes (from `scripts/e2e_validation.py` L6; L2 harness seeds the first match)

### Persona A — Burj Digital Exchange FZE (primary; the L2 entity for VARA)
- `e2e-vara-vaspex-0001` · **VASP-EX** (Exchange + Broker-Dealer Services)
- Dubai World Trade Centre, Dubai, UAE
- Retail clients: **yes** · AML obligations: yes
- Profile: spot virtual-asset trading, fiat on/off ramp; 51–100 staff; PEP exposure medium

### Persona B — Mina Custody Services LLC
- `e2e-vara-vaspcust-0001` · **VASP-CUST** (Custody Services)
- DWTC Free Zone, Dubai, UAE
- Profile: qualified custody, cold storage; 11–25 staff; institutional only; PEP exposure low

> Fallback `l2-vara-0001` ("L2 Acceptance VARA Ltd") only if no match — not a tester shape.

## 2. Smallest-template walkthrough (warm-up run)

Smallest active VARA template: **`vara_examination_prep_pack` — "Regulatory Examination Preparation Pack (VARA)", 3 sections, Tier 5** (registry survey 2026-06-11).
⚠ Known duplicate-concept hazard: this is the hand-authored key; the matrix-matched twin is `vara_regulatory_examination_preparation_pack`. If the UI offers both, that duplication is itself a logged defect (activation pack §2.3 — 7 such pairs).

1. Sign in; onboard as Persona A (VASP-EX, stage: Registered).
2. Wizard offers 5 of 8 VARA licence types — VASP-EX is selectable. Draft `vara_examination_prep_pack` (or the suite path below).
3. **Expect `[TO BE CONFIRMED]` everywhere**: all 47 VARA templates have zero `entity_fact_questions`, so MLRO name, board composition, custody arrangements render as placeholders. Verify the placeholders are well-formed; missing facts are a known gap, not a defect.
4. Check citations: VARA rulebook format `[RULEBOOK PART.SECTION.REF]` (e.g. VARA-CRM III). Part-level refs are acceptable (they resolve to child sections); non-VARA citations (ADGM/FSRA/COBS) are defects.
5. Export DOCX; checklist §5.
6. Suite run (the showcase): **`vara_vasp_bd_tier1` is the only approved suite slot (1/40)** — a VASP-BD Tier-1 suite, 7 documents. If testing suites, use VASP-BD Tier 1 and nothing else.

## 3. Expected roughness (activation caveats — `docs/activation-packs/VARA.md`)

- Strongest corpus of the launch set (fully re-parsed, 2,112/2,112 vector parity) — citation quality should be high; hold drafts to that.
- **39/40 suite slots unapproved** — only VASP-BD Tier 1 suite-drafts end-to-end.
- 7 duplicate doc_type pairs (hand-authored vs module keys) — same logical document reachable under two ids.
- Zero questionnaires and **zero category tailoring** (J19 open): documents differ by which apply, not by within-document licence-type content.
- Wizard missing VASP-LB, VASP-TRS, VASP-ISS — those tracks unreachable; don't test them.
- VARA-ISS: 40 NULLed citations pending re-extraction — issuance-document citation enrichment degraded (VASP-ISS lane only).

## 4. Reporting defects

- **Once live:** `POST /api/support/contact` (qanun-api `routers/support.py`, flag `enable_support_contact`, default OFF as of MAX-6) / the in-app contact form.
- **Meanwhile:** **support@qanun.io** — subject `[TESTER][VARA] <template> — <one-line defect>`. Include persona, template id, section, verbatim text, expected vs actual.

## 5. Verification checklist

- [ ] Citations are VARA-only, `[RULEBOOK PART.REF]` shaped; part-level refs resolve
- [ ] `[TO BE CONFIRMED]` placeholders well-formed and limited to genuinely unknown facts
- [ ] VASP-BD Tier-1 suite: 7 docs complete, tier ordering monotone, cross-tier context visible in later docs
- [ ] DOCX export clean
- [ ] Matches golden — **goldens: see overnight N1 results — populate links after N1 lands**
