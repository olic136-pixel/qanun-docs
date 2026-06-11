# PANAMA — Activation Pack (MAX-5 K2)

**Prepared:** 2026-06-11 (MAX-5 K2, sprint/max5-jx-packs)
**For:** Oliver's human activation gate. Panama was tracked by **no J-item at all** (MAX-4 V5 register omission) — this pack and `docs/matrices/PANAMA_tier_matrix.md` close that hole; a register J-item should be minuted at the next register update.

## 1. Registry state

`TEMPLATE_REGISTRY` ← `services/panama_templates.py` @ sprint/max5-jx-templates: **14 `panama_*` templates**.

| Tier | Count | Note |
|---|---|---|
| 1 — Registration Pack | 4 | Casa de Valores application + shared plan/AML/F&P |
| 2 — Compliance Framework | 3 | manual, KYC/CDD, market conduct |
| 3 — Corporate Governance | 3 | board charter (Art.167), senior mgmt, whistleblowing |
| 4 — Operational Procedures | **2 (new)** | client asset & custody (crypto-conditional s3), books/records/registers |
| 5 — Filings & Monitoring | **2 (new)** | SMV periodic reporting, capital & liquidity monitoring |

Suite activation state: 0 suites (emit pipeline does not support PANAMA; same class as SV).

## 2. Matrix coverage

`docs/matrices/PANAMA_tier_matrix.md`: launch-priority rows **PAN-CASA-TRAD and PAN-CASA-CRYPTO are 14/14 filled-or-N/A (0 GAP)**; ADM/SI/ASESOR rows carry 3 groundable Tier-1 application gaps (deferred, refs verified) and 2 non-groundable gaps (SMV Acuerdos absent from corpus).

## 3. Corpus state

PAN-LMV 386 arts · PAN-LMV-67 169 · PAN-LSEG 336 · PAN-LEY32 96 (incl. Art.36 Registro de Acciones) · PAN-LEY52 22 · PAN-AML 7. All template refs LIKE-verified 2026-06-11. Gap: SMV Acuerdos (gobierno corporativo 5-2004, digital-asset rules) unindexed.

## 4. Questionnaire / UI (J18-equivalent)

Worst of the three jurisdictions: PANAMA is absent from the single-doc drafting page, has **no questionnaire at all** (router falls through to "No questionnaire defined"), wizard offers 2 of 5 licence types, and the suite page taxonomy is wrong (`sociedad_anonima`). Full list: `docs/tickets/MAX5_UI_punchlist_K6.md` §PANAMA (P1–P6) + cross-lane X1/X2.

## 5. Evidence

E2E: PAN-CASA-CRYPTO and PAN-CASA-TRAD cells pass with the fixed pipeline (one PAN coverage residual outstanding, tracked by the E2E lane).

## 6. RECOMMENDATION

**HOLD for UI + questionnaire reachability only.** Template/matrix/corpus structure is launch-shaped for both Casa de Valores tracks; the blocking set is P1–P6 + X1/X2 and the suite-emit gap — no Panama-side structural work remains.
