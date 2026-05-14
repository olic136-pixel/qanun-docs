# LMCR Consolidation — Cross-Jurisdiction Launch-Readiness Summary

**Session:** `016-LMCR-consolidation`
**Generated:** 2026-05-14
**Inputs:** `ADGM.md`, `VARA.md`, `DFSA.md`, `BVI.md`, `EL_SALVADOR.md`, `PANAMA.md` (all 6 present — pre-flight passed)
**Corpus DB:** `/Users/oliver/ADGM/adgm-corpus/corpus.db` (sha256 `c061d461e1ab68cd…`)

> ## ⚠️ Surface — schema discrepancy (halt_strategy: surface)
>
> The 016 session brief assumes a per-jurisdiction MCR template with **`Total Required` / `In Corpus` / `Gap Count` / `Priority Gap`** columns, severity scale **CRITICAL / HIGH / MEDIUM / LOW**, and per-gap **`source_url`** + **`estimated_effort_session_count`** fields.
>
> The actual MCR files (009–014) do **not** carry that schema. As each upstream session noted, *"the L9 session brief truncated before the MCR file template"* — so all six were reconstructed from the `corpus_completeness` table schema instead. They provide:
> - Headline counts: `Expected / PRESENT / REGISTERED / PARTIAL / MISSING / Critical gaps / Orphans`
> - A per-document **Gap severity** of `CRITICAL / MAJOR / MINOR` (a property of the document's importance, not of the gap)
> - **No** `source_url` for gaps, **no** `estimated_effort_session_count`, **no** template-citation or Quick-Lookup signal
>
> This consolidation is therefore built on a **best-effort mapping** (documented under each section). The brief's prescribed sort key — *"cited by templates × surfaced in user Quick Lookups"* — **cannot be computed** from current MCR data and is approximated by the MCR gap-severity proxy. **Recommended follow-up:** either (a) re-run 009–014 once the real MCR template is recovered, or (b) extend `mcr_generator.py` to emit citation/effort metadata, then re-run this consolidation.
>
> Also surfaced: **no `--consolidate` flag and no separate consolidation script exists** in the L9 toolkit (`/Users/oliver/ADGM/adgm-corpus/mcr/mcr_generator.py`). This file was aggregated manually.

---

## Per-jurisdiction summary

Column mapping: **Total Required** = MCR `Expected (authoritative)`; **In Corpus** = MCR `PRESENT`; **Gap Count** = `REGISTERED + PARTIAL + MISSING`; **Priority Gap** = highest-severity non-PRESENT item (severity, then MISSING > PARTIAL > REGISTERED).

| Jurisdiction | Total Required | In Corpus | Gap Count | Priority Gap (highest) |
|---|---|---|---|---|
| ADGM | 14 | 14 | 0 | — (none) |
| VARA | 12 | 12 | 0 | — (none) |
| DFSA | 22 | 21 | 1 | `DFSA-CRYPTO-GUIDE` — PARTIAL, MINOR |
| BVI | 12 | 11 | 1 | `BVI-PIF` — PARTIAL, MAJOR |
| EL_SALVADOR | 24 | 12 | 12 | `SV-DASP-ES` — MISSING, MAJOR |
| PANAMA | 8 | 5 | 3 | `PAN-SMV-GESTORAS` — MISSING, CRITICAL |
| **Total** | **92** | **75** | **17** | — |

Gap-count breakdown across all jurisdictions: **REGISTERED 8**, **PARTIAL 4**, **MISSING 5** (= 17).
Corpus coverage (PRESENT / Required): **75 / 92 = 81.5%**.

---

## Gap acquisition queue

All 17 non-PRESENT items, flattened and sorted by severity then status (MISSING > PARTIAL > REGISTERED).

**Severity mapping (best-effort):** MCR `CRITICAL` → CRITICAL; MCR `MAJOR` → HIGH; MCR `MINOR` → MEDIUM. No items fell to LOW. The brief's CRITICAL-vs-HIGH split ("cited by templates × surfaced in Quick Lookups") could not be applied — see surface note above.

**`source_url`:** not carried by the MCR files — shown as `n/a (not in MCR)`. **Est. effort:** derived heuristic — MISSING = 1.0 session (needs external sourcing); PARTIAL = 0.5 (verify/re-match); REGISTERED = 0.25 (metadata fix, batchable). Phase column is taken from MCR Notes where stated.

| # | Severity | Jurisdiction | Item | Status | source_url | Est. effort (sessions) | Remediation phase / note |
|---|---|---|---|---|---|---|---|
| 1 | CRITICAL | PANAMA | `PAN-SMV-GESTORAS` — Acuerdo SMV, Gestoras de Inversión | MISSING | n/a (not in MCR) | 1.0 | Open item — SOW Section 13. SMV decree for fund managers. |
| 2 | HIGH | EL_SALVADOR | `SV-DASP-ES` — Reglamento DASP CNAD [Español] | MISSING | n/a (not in MCR) | 1.0 | Spanish original not ingested. |
| 3 | HIGH | EL_SALVADOR | `SV-UIF` — UIF Instructions applicable to DASPs | MISSING | n/a (not in MCR) | 1.0 | UIF financial-intelligence-unit instructions not ingested. |
| 4 | HIGH | PANAMA | `PAN-UAF` — Instrucciones UAF, Sujetos Obligados Financieros | MISSING | n/a (not in MCR) | 1.0 | UAF financial-intelligence-unit instructions. |
| 5 | HIGH | PANAMA | `PAN-UBO` — Ley 129 de 2020, Registro Único de Beneficiarios Finales | MISSING | n/a (not in MCR) | 1.0 | Referenced in PAN-LEY32 but not ingested standalone. |
| 6 | HIGH | BVI | `BVI-PIF` — Private Investment Funds Act 2019 | PARTIAL | n/a (not in MCR) | 0.5 | Title-only match to Mutual Funds Act; verify in Phase 4 pre-flight. |
| 7 | HIGH | EL_SALVADOR | `SV-LEAD-ES` — Ley de Emisión de Activos Digitales (Decreto 643, 2023) [Español] | PARTIAL | n/a (not in MCR) | 0.5 | Spanish authoritative version not ingested; matched to 2024 reform. |
| 8 | HIGH | EL_SALVADOR | `SV-BTC-2025` — Reforma a la Ley Bitcoin (Decreto 918, 2025) | REGISTERED | n/a (not in MCR) | 0.25 | Exists in SQLite, `rulebook_code=null`. Fix in Phase 5. |
| 9 | MEDIUM | DFSA | `DFSA-CRYPTO-GUIDE` — Supervisory Guidelines on Suitability of Crypto Tokens | PARTIAL | n/a (not in MCR) | 0.5 | Exists in SQLite (doc_id 2428, 34k words); confirm match. |
| 10 | MEDIUM | EL_SALVADOR | `SV-LBAN-COOP` — Ley de Bancos Cooperativos y Sociedades de Ahorro y Crédito | PARTIAL | n/a (not in MCR) | 0.5 | Exists in SQLite, `rulebook_code=null`. Fix in Phase 5. |
| 11 | MEDIUM | EL_SALVADOR | `SV-AML-OLD` — Ley Contra el Lavado de Dinero y de Activos (previous law) | REGISTERED | n/a (not in MCR) | 0.25 | Exists in SQLite, `rulebook_code=null`. Fix in Phase 5. |
| 12 | MEDIUM | EL_SALVADOR | `SV-BTC-TRUST` — Ley del Fideicomiso Bitcoin (Decreto 137, 2022) | REGISTERED | n/a (not in MCR) | 0.25 | Exists in SQLite, `rulebook_code=null`. Fix in Phase 5. |
| 13 | MEDIUM | EL_SALVADOR | `SV-BCR-NRP29` — NRP-29: Participación de PSAV en Sistemas de Pago (BCR) | REGISTERED | n/a (not in MCR) | 0.25 | Exists in SQLite, `rulebook_code=null`. Fix in Phase 5. |
| 14 | MEDIUM | EL_SALVADOR | `SV-BCR-LPB` — Lineamientos para Plataforma Tecnológica Bitcoin/Dólares (BCR) | REGISTERED | n/a (not in MCR) | 0.25 | Exists in SQLite, `rulebook_code=null`. Fix in Phase 5. |
| 15 | MEDIUM | EL_SALVADOR | `SV-BCR-NT` — Normas Técnicas para Facilitar la Aplicación de la Ley Bitcoin (BCR) | REGISTERED | n/a (not in MCR) | 0.25 | Exists in SQLite, `rulebook_code=null`. Fix in Phase 5. |
| 16 | MEDIUM | EL_SALVADOR | `SV-BTC-REG` — Reglamento de la Ley Bitcoin (Decreto Ejecutivo 27, 2021) | REGISTERED | n/a (not in MCR) | 0.25 | Exists in SQLite, `rulebook_code=null`. Fix in Phase 5. |
| 17 | MEDIUM | EL_SALVADOR | `SV-LOC-ANALYSIS` — Library of Congress: El Salvador Bitcoin Law Analysis [English] | REGISTERED | n/a (not in MCR) | 0.25 | Exists in SQLite, `rulebook_code=null`. Fix in Phase 5. |

**Queue totals:** 1 CRITICAL · 7 HIGH · 9 MEDIUM · 0 LOW. Aggregate derived effort ≈ **8.5 sessions** (CRITICAL 1.0 + HIGH 5.25 + MEDIUM 2.25).

**Observation:** 8 of the 9 MEDIUM items and 1 HIGH item are EL_SALVADOR `REGISTERED`/`PARTIAL` rows all flagged *"Fix in Phase 5"* — they are metadata fixes (`rulebook_code=null`, `is_current=0`) on documents already in SQLite, not external sourcing. They can be remediated as a single batched Phase 5 task rather than 9 separate acquisitions.

---

## Launch readiness gate

**L18 acceptance criterion:** zero CRITICAL gaps **and** zero HIGH gaps before launch.

| Gate check | Count | Status |
|---|---|---|
| CRITICAL gaps | 1 (`PAN-SMV-GESTORAS`) | ❌ FAIL |
| HIGH gaps | 7 | ❌ FAIL |
| MEDIUM gaps | 9 | ⚠️ launch-with-acknowledgement permitted |
| LOW gaps | 0 | ✅ |

**Gate verdict: ❌ NOT READY FOR LAUNCH.**

Blocking items (must clear before L18 sign-off):
- **1 CRITICAL** — `PAN-SMV-GESTORAS` (Panama).
- **7 HIGH** — 4 MISSING (`SV-DASP-ES`, `SV-UIF`, `PAN-UAF`, `PAN-UBO`), 2 PARTIAL (`BVI-PIF`, `SV-LEAD-ES`), 1 REGISTERED (`SV-BTC-2025`).

All 8 blockers are concentrated in **EL_SALVADOR (4)** and **PANAMA (3)** plus **BVI (1)**. ADGM, VARA, and DFSA are launch-clear (DFSA's single gap is MEDIUM).

Non-blocking:
- **9 MEDIUM** gaps may launch with acknowledgement; 8 are batchable EL_SALVADOR Phase 5 metadata fixes.

**Post-launch:** MCR re-runs scheduled quarterly.

---

## Method & caveats

1. **Pre-flight:** all 6 MCR files confirmed present in `~/qanun-docs/mcr/`. No HALT.
2. **L9 toolkit:** `mcr_generator.py` inspected — supports `--jurisdiction {NAME|ALL}` only; **no `--consolidate` flag**, and no standalone consolidation script exists. This file was aggregated manually by reading the six MCRs.
3. **Severity:** the MCR `Gap severity` field (`CRITICAL/MAJOR/MINOR`) is a per-document importance attribute, present even on PRESENT rows. The "gap" itself is determined by `Status ∈ {REGISTERED, PARTIAL, MISSING}`. Queue severity = MCR severity of non-PRESENT rows, mapped CRITICAL→CRITICAL, MAJOR→HIGH, MINOR→MEDIUM.
4. **Unavailable data:** `source_url` and `estimated_effort_session_count` are not emitted by the current MCRs; effort is a documented heuristic, not source data. The brief's template-citation/Quick-Lookup sort signal does not exist in the inputs.
5. **Orphan documents** (in corpus, not in authoritative inventory) were noted by the MCRs — ADGM 728, BVI 10, EL_SALVADOR 5, PANAMA 2 — but are out of scope for the launch gap queue and not consolidated here.
