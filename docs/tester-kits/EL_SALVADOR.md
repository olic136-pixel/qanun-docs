# EL SALVADOR — Tester Kit (L7 walkthrough skeleton)

**Prepared:** 2026-06-11 (MAX-6 N5, sprint/max6-k-drafts). Register L7 (deps: L6).
**Status:** skeleton — populated with entity shapes, smallest-template walkthrough, activation caveats and defect routes; golden links pending N1.
**Goldens: see overnight N1 results — populate links after N1 lands.**

## 1. Fictional entity shapes (from `scripts/e2e_validation.py` L6; L2 harness seeds the first match)

### Persona A — Pacífico Digital S.A. de C.V. (primary; the L2 entity for EL_SALVADOR)
- `e2e-sv-daspex-0001` · **SV-DASP-EX** (digital-asset exchange)
- San Salvador, El Salvador
- Activities: Exchange of digital assets; Order book operation · retail: yes
- Profile: BTC/USD spot exchange, stablecoin pairs; 26–50 staff; jurisdictions El Salvador/Guatemala/US; PEP exposure medium

### Persona B — Cuscatlán Token Issuance S.A.
- `e2e-sv-daspiss-0001` · **SV-DASP-ISS** (issuance)
- Antiguo Cuscatlán, La Libertad, El Salvador
- Activities: Public offering of digital assets; Issuance services
- Profile: tokenised real-estate certificates (RID issuances); 1–10 staff; PEP exposure low
- ⚠ The ISS track is **HOLD** (unreachable from the wizard) — Persona B is for explicit-template runs and for verifying the hold, not for full walkthroughs.

> Fallback `l2-el_salvador-0001` only if no match — not a tester shape.

## 2. Smallest-template walkthrough (warm-up run)

Smallest active SV template: **`sv_declaraciones_idoneidad` — "Declaraciones de Idoneidad — Directores y Oficial de Cumplimiento (Fit and Proper Declarations)", 1 section, Tier 0/1** (registry survey 2026-06-11) — also the natural bilingual smoke test.

1. Sign in; onboard as Persona A. Wizard offers 4 of 10 SV categories — **DASP-EX is selectable**. Stage: only "Registered — CNAD" exists (no pre-registration stage — known gap; Tier-1 registration-pack scenarios can't represent their true stage).
2. Draft `sv_declaraciones_idoneidad`. Expect `[TO BE CONFIRMED]` for the Oficial de Cumplimiento / UIF registration details (zero `entity_fact_questions` on all 52 SV templates — J15 flags exactly this).
3. **Citations are Spanish-primary** (SV-*-ES authoritative, EN secondary) per the approved review memo — Spanish citations are correct behaviour, not a defect. Check `SV-LEAD Art.N` / `SV-STBL Art.N` shapes resolve.
4. Review bilingual quality: the document is a Spanish-deliverable class; note any anglicism/terminology friction for the J15 bilingual consideration.
5. Export DOCX; checklist §5.
6. Scale-up: Persona A matrix cells — `sv_bsp_bcr_registration_pack` (stage caveat above), `sv_amlcft_programme`, `sv_kyc_cdd_manual`, `sv_exchange_trading_operations_manual`.

## 3. Expected roughness (activation caveats — `docs/activation-packs/EL_SALVADOR.md`)

- Status: **ACTIVATE-WITH-CAVEATS for DASP-EX/CUST/PLAT/XFER only; STBL-ISS / BSP / ISS / CERT tracks HOLD** (six categories, including all stablecoin/issuance tracks, unreachable from the questionnaire).
- **No SV suites** — `emit_suite_json()` doesn't support EL_SALVADOR; tier-ordered suite drafting (cross-tier context) unavailable. Single documents only.
- Zero entity-fact questions; no CNAD registration number, UIF-MLRO or reserve-bank capture.
- No Spanish-language preference field in onboarding (J15).
- Corpus footprint small (16 current docs) — adequate for the approved 52-doc matrix but semantic retrieval is thinner than VARA/ADGM.

## 4. Reporting defects

- **Once live:** `POST /api/support/contact` (qanun-api `routers/support.py`, flag `enable_support_contact`, default OFF as of MAX-6) / in-app contact form.
- **Meanwhile:** **support@qanun.io** — subject `[TESTER][SV] <template> — <one-line defect>`. Include persona, template id, section, verbatim text (Spanish or English), expected vs actual.

## 5. Verification checklist

- [ ] Citations SV-only, Spanish-primary, `Art.`-shaped, resolve in Quick Lookup
- [ ] Spanish drafting quality acceptable for a CNAD-facing document
- [ ] `[TO BE CONFIRMED]` limited to genuinely uncaptured facts
- [ ] DOCX export clean
- [ ] Matches golden — **goldens: see overnight N1 results — populate links after N1 lands**
