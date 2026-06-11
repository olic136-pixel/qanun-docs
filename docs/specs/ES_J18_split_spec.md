# El Salvador — J18 Split Spec: 4 DASP Tracks Live, 6 Tracks Visible-but-Gated (MAX-5 K2)

**Prepared:** 2026-06-11 (MAX-5 K2, sprint/max5-jx-packs). **Feeds the UI lane (K6) — spec only, no frontend built.**
**Decision implemented:** MAX-4 V5 split decision — activate SV-DASP-EX / CUST / PLAT / XFER; hold SV-DASP-STR / SV-DASP-INV / SV-BSP / SV-DASP-ISS / SV-STBL-ISS / SV-CERT. Held tracks must be **visible and gated ("Coming soon"), not absent** — absence reads as a product gap; gating reads as a roadmap.
**Repo:** `~/qanun` (Next.js, read-only for this spec). All paths below are relative to repo root.

## 1. Single source of truth (new file)

**`lib/constants/sv-categories.ts`** (NEW, ~60 lines) — one exported list consumed by every surface below; today each surface hard-codes its own divergent subset (4 in the wizard, 9 in the suite page, free-text in the questionnaire).

```ts
export type SvCategoryStatus = 'live' | 'gated'
export interface SvCategory {
  code: string          // canonical UI code, e.g. 'dasp_ex'
  wizardValue: string   // legacy wizard value, e.g. 'sv_dasp_ex'
  matrixCode: string    // J3 matrix code, e.g. 'SV-DASP-EX'
  label: string
  description: string
  status: SvCategoryStatus
  docCount: number      // from the Oliver-approved 52-doc matrix
}
export const SV_CATEGORIES: SvCategory[] = [
  { code: 'dasp_ex',   wizardValue: 'sv_dasp_ex',   matrixCode: 'SV-DASP-EX',   label: 'DASP-EX — Exchange',  status: 'live',  docCount: 43, ... },
  { code: 'dasp_cust', wizardValue: 'sv_dasp_cust', matrixCode: 'SV-DASP-CUST', label: 'DASP-CUST — Custody', status: 'live',  docCount: 39, ... },
  { code: 'dasp_plat', wizardValue: 'sv_dasp_plat', matrixCode: 'SV-DASP-PLAT', label: 'DASP-PLAT — Platform',status: 'live',  docCount: 40, ... },
  { code: 'dasp_xfer', wizardValue: 'sv_dasp_xfer', matrixCode: 'SV-DASP-XFER', label: 'DASP-XFER — Transfer',status: 'live',  docCount: 39, ... },
  { code: 'dasp_str',  wizardValue: 'sv_dasp_str',  matrixCode: 'SV-DASP-STR',  label: 'DASP-STR — Staking',  status: 'gated', docCount: 37, ... },
  { code: 'dasp_inv',  wizardValue: 'sv_dasp_inv',  matrixCode: 'SV-DASP-INV',  label: 'DASP-INV — Investment',status: 'gated', docCount: 37, ... },
  { code: 'bsp',       wizardValue: 'sv_bsp',       matrixCode: 'SV-BSP',       label: 'BSP — Bitcoin Service Provider', status: 'gated', docCount: 37, ... },
  { code: 'dasp_iss',  wizardValue: 'sv_dasp_iss',  matrixCode: 'SV-DASP-ISS',  label: 'ISS — Issuance',      status: 'gated', docCount: 39, ... },
  { code: 'stbl_iss',  wizardValue: 'sv_stbl_iss',  matrixCode: 'SV-STBL-ISS',  label: 'STBL-ISS — Stablecoin Issuer', status: 'gated', docCount: 41, ... },
  { code: 'cert',      wizardValue: 'sv_cert',      matrixCode: 'SV-CERT',      label: 'CERT — Certifier',    status: 'gated', docCount: 36, ... },
]
```

## 2. Change set per file/component

### 2.1 `app/(dashboard)/compliance/governance/GovernanceOnboardingWizard.tsx` (456 lines)
- **`CATEGORY_GROUPS`** (lines 23–67), El Salvador group (lines 43–51): replace the 4 hard-coded options with `SV_CATEGORIES` (all 10). Extend `CategoryOption` (line 12) with `gated?: boolean`.
- **`SelectableCard`** (lines 423–447): add `gated` prop → render a right-aligned "Coming soon" pill (design system: gold #C4922A text on 10% tint, 10px uppercase tracking), `disabled` button, `cursor-not-allowed`, opacity 60%, `onClick` no-op, `aria-disabled`.
- **Step-1 validation** (line 393–401 `disabled` logic): unchanged — gated cards can never set `fsraCategory`.
- **`STAGE_GROUPS`** El Salvador (lines 100–105): add `{ value: 'sv_pre_registration', label: 'Pre-registration', description: 'Preparing CNAD registration application' }` ahead of `sv_registered` (Tier 1 is a Registration Pack; pre-application firms currently cannot represent their state).
- **`APPROXIMATE_COUNTS`** (lines 125–130): currently ADGM-only — add the four live SV values from `SV_CATEGORIES.docCount` (43/39/40/39) so step 3 stops rendering "—" for SV.

### 2.2 `app/(dashboard)/compliance/governance-suite/page.tsx` (≈600 lines)
- **`LICENCE_TYPES.EL_SALVADOR`** (lines 38–48): currently 9 entries — drift from matrix: missing `dasp_str`; `issu` mislabels the matrix code SV-DASP-ISS. Replace with `SV_CATEGORIES` (10 entries, `gated` carried through). Render gated entries with the same "Coming soon" treatment, non-selectable (step-2 `canProceed` at line ~81 already requires a selection; blocked selection suffices).
- **`DOC_COUNTS.EL_SALVADOR`** (line 72): `[0, 11, 13, 7, 9, 10]` = 52 — correct, keep.
- Selection chip on step 4 review should show the matrix code (`SV-DASP-EX`) alongside the label for support-ticket parity with the J3 matrix.

### 2.3 `lib/questionnaires/jurisdiction-questions.ts`
- **`SV_QUESTIONS`** `sv_licence_category` (line 46): free-text → `select` sourced from `SV_CATEGORIES`; live options enabled, gated options present with "(coming soon)" suffix and disabled. Keeps the answer enumerable for J19 tailoring instead of free text.
- Add (J15/J18 content, distinct items): `sv_uif_mlro_details` capture is already present (lines 82–88) — no change; add `sv_reserve_bank_partner` (text) shown only when category = `stbl_iss` (gated today, ships dormant behind the gate).

### 2.4 `components/qanun/cee/JurisdictionSelector.tsx` (91 lines)
- No change — jurisdiction-level only; EL_SALVADOR stays selectable.

### 2.5 `components/qanun/cee/ConversationEngine.tsx`
- VERIFY item for K6: if the CEE flow prompts for an SV category, source from `SV_CATEGORIES` and enforce the same gate (do not let conversation flow reach a held track).

### 2.6 `components/qanun/JurisdictionQuestionnaireRouter.tsx` (68 lines)
- No structural change (EL_SALVADOR already routed, line 29); inherits the 2.3 select change via `getJurisdictionQuestions`.

### 2.7 Tests
- `__tests__/jurisdiction-questionnaires.test.tsx`: extend — (a) all 10 SV categories render in wizard step 1; (b) exactly 6 carry the gated affordance and are not selectable; (c) `sv_pre_registration` stage present; (d) suite page SV licence list === `SV_CATEGORIES` (no drift); (e) snapshot of the "Coming soon" pill.

**Estimated size:** 1 new file (~60 lines) + 4 edited files, net ≈ +220 / −60 lines, plus tests ≈ +120 lines. Half-day build, consistent with the register's J18 sizing.

## 3. Template-side reachability map (registry @ sprint/max5-jx-templates)

All 52 `sv_*` templates exist in `TEMPLATE_REGISTRY` (T1=13, T2=13, T3=7, T4=9, T5=10) — reachability is entirely a UI/gating property:

| Track | Status | Docs in matrix | Reachable today | After this spec |
|---|---|---|---|---|
| SV-DASP-EX | live | 43 | YES (wizard) | YES |
| SV-DASP-CUST | live | 39 | YES | YES |
| SV-DASP-PLAT | live | 40 | YES | YES |
| SV-DASP-XFER | live | 39 | YES | YES |
| SV-DASP-STR | gated | 37 | NO — absent everywhere (incl. suite page) | visible, gated |
| SV-DASP-INV | gated | 37 | suite page only (inconsistent) | visible, gated |
| SV-BSP | gated | 37 | suite page only | visible, gated |
| SV-DASP-ISS | gated | 39 | suite page only (as `issu`) | visible, gated |
| SV-STBL-ISS | gated | 41 | suite page only | visible, gated |
| SV-CERT | gated | 36 | suite page only | visible, gated |

The 14 track-specific templates of the held tracks (BSP BCR pack, certifier framework, RID prospectus, stablecoin notification/affidavit/attestation/API-report, reserve management, market abuse, investment product manual, etc.) remain registry-resident and drafting-capable; the gate is presentational only.

## 4. Backend cross-lane caveat (NOT a UI fix — flagged for the API lane)

`POST /api/drafting/suite` (qanun-api `routers/drafting.py:568–575`) derives `doc_types` ignoring `licence_type` and `tiers` when `doc_types` is empty: the filter tests `request.jurisdiction in getattr(t, 'jurisdictions', ['ADGM'])` — `DocumentTemplate` has **no `jurisdictions` attribute**, so non-ADGM suites resolve to templates with empty `applicable_entity_types` only. UI gating alone therefore cannot scope an SV suite correctly; the API lane must filter by doc_type prefix (`sv_`) + tier + track applicability before SV suites activate. (Same defect affects BVI/PANAMA suites.)
