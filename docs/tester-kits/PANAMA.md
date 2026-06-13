# PANAMA — Tester Kit (L7 walkthrough skeleton)

**Prepared:** 2026-06-11 (MAX-6 N5, sprint/max6-k-drafts). Register L7 (deps: L6).
**Status:** skeleton — populated with entity shapes, smallest-template walkthrough, activation caveats and defect routes; golden links pending N1.
**Goldens: see overnight N1 results — populate links after N1 lands.**

## 1. Fictional entity shapes (from `scripts/e2e_validation.py` L6; L2 harness seeds the first match)

### Persona A — Istmo Digital Casa de Valores S.A. (primary; the L2 entity for PANAMA)
- `e2e-pan-casacrypto-0001` · **Casa de Valores** (`PAN-CASA-CRYPTO`)
- Calle 50, Ciudad de Panamá, Panama
- Activities: Securities brokerage; Digital asset exchange services · retail: yes
- Profile: crypto exchange desk + tokenised-securities brokerage; 11–25 staff; Panama/Colombia/Mexico; PEP exposure medium

### Persona B — Bahía Valores S.A.
- `e2e-pan-casatrad-0001` · **Casa de Valores** (`PAN-CASA-TRAD`)
- Costa del Este, Ciudad de Panamá, Panama
- Activities: Securities brokerage; Underwriting · retail: yes
- Profile: equities/bonds brokerage, public offerings; 26–50 staff; PEP exposure medium

> Both launch-priority rows of `docs/matrices/PANAMA_tier_matrix.md` are 14/14 filled-or-N/A.

## 2. Smallest-template walkthrough (warm-up run)

Smallest active Panama template: **`panama_board_charter_panama` — "Board Charter (Panama)", 3 sections, Tier 3** (registry survey 2026-06-11; grounded on PAN-LMV Art.167 class refs).

⚠ **Reachability first:** Panama has the worst UI surface of the six (activation pack §4): absent from the single-document page, **no questionnaire at all** (router falls through to "No questionnaire defined"), wizard offers 2 of 5 licence types with a wrong taxonomy label (`sociedad_anonima`). Expect the walkthrough to stall at reachability — **documenting where it stalls is the test** until punch-list P1–P6 + X1/X2 land.

1. Sign in; attempt onboarding as Persona A. Record exactly which licence-type options appear and which taxonomy labels are wrong.
2. If a drafting route to `panama_board_charter_panama` exists in your build, draft it; otherwise log the dead-end (screenshot + route).
3. If drafted: expect `[TO BE CONFIRMED]` placeholders throughout (no questionnaire); citations should be `PAN-LMV Art.N` / `PAN-LEY32 Art.N` shapes — all template refs LIKE-verified 2026-06-11.
4. Check the crypto-conditional content: `panama_client_asset_custody_procedures` s3 is crypto-conditional — Persona A (CRYPTO) should include it, Persona B (TRAD) should not.
5. Export DOCX; checklist §5.

## 3. Expected roughness (activation caveats — `docs/activation-packs/PANAMA.md`)

- Status: **HOLD for UI + questionnaire reachability only** — templates/matrix/corpus are launch-shaped for both Casa de Valores tracks; the blocking set is P1–P6 + X1/X2 (`docs/tickets/MAX5_UI_punchlist_K6.md` §PANAMA) + the suite-emit gap.
- No suites (emit pipeline doesn't support PANAMA — same class as SV).
- Corpus gap: **SMV Acuerdos unindexed** (gobierno corporativo 5-2004, digital-asset rules) — governance/digital-asset drafting cites primary laws only; missing Acuerdo citations are a known corpus gap, not hallucination cover.
- Tiers 4–5 are new (2+2 templates from MAX-5) — first tester pass on them.
- One PAN coverage residual outstanding in the E2E lane.

## 4. Reporting defects

- **Once live:** `POST /api/support/contact` (qanun-api `routers/support.py`, flag `enable_support_contact`, default OFF as of MAX-6) / in-app contact form.
- **Meanwhile:** **support@qanun.io** — subject `[TESTER][PANAMA] <template> — <one-line defect>`. Include persona, template id, section, verbatim text, expected vs actual, and reachability dead-ends with screenshots.

## 5. Verification checklist

- [ ] Reachability map recorded (what is/isn't selectable; wrong labels noted)
- [ ] Citations PAN-only (PAN-LMV / PAN-LMV-67 / PAN-LSEG / PAN-LEY32 / PAN-LEY52 / PAN-AML), resolve in Quick Lookup
- [ ] Crypto-conditional sections appear for CRYPTO and not for TRAD
- [ ] DOCX export clean (if reachable)
- [ ] Matches golden — **goldens: see overnight N1 results — populate links after N1 lands**
