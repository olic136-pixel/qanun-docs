# Material Completeness Register — El Salvador CNAD Digital Asset Services

**Jurisdiction code:** `EL_SALVADOR`  
**Regulator:** Comisión Nacional de Activos Digitales (CNAD), El Salvador  
**Generated:** 2026-05-14T18:51:52.790183+00:00  
**Corpus DB:** `/Users/oliver/ADGM/adgm-corpus/corpus.db` (sha256 `c061d461e1ab68cd…`, opened read-only)  
**Authoritative inventory:** `/Users/oliver/ADGM/adgm-corpus/adgm_corpus/manifests/EL_SALVADOR.json` (24 expected documents)  
**Corpus source entities:** `EL_SALVADOR` (28 documents in corpus)  
**Primary source index:** https://cnad.gob.sv — HTTP 200 (reachable)  

> **Template note.** The L9 session brief truncated before the MCR file template, and the plan file it referenced (`overnight_throughput_plan_2026-05-16.md`) does not exist. This structure was reconstructed from the `corpus_completeness` table schema and `adgm_corpus/manifests/MANIFEST_SCHEMA.json` (canonical status values: PRESENT / REGISTERED / PARTIAL / MISSING), styled after `dfsa_inventory_authoritative.md`. Adjust the shape if the intended template differs.

## Headline

- **Expected (authoritative):** 24
- **PRESENT** (current corpus doc matched): 12 (50%)
- **REGISTERED** (matched, but no `is_current=1` version): 8
- **PARTIAL** (matched by title heuristic only — verify): 2
- **MISSING** (no corpus document matched): 2
- **Critical gaps:** 0
- **Orphan corpus documents** (in corpus, not in authoritative inventory): 5

## Register

| Code | Authoritative document | Type | Tier | Status | Gap severity | Matched corpus doc | Match basis | Notes |
|---|---|---|---|---|---|---|---|---|
| `SV-DASP-ES` | Reglamento DASP CNAD [Español] | rulebook | 1 | **MISSING** | MAJOR | — | — | MISSING — Spanish original not ingested |
| `SV-UIF` | UIF Instructions applicable to DASPs | guidance | 2 | **MISSING** | MAJOR | — | — | MISSING — UIF financial intelligence unit instructions not ingested |
| `SV-BTC-2025` | Reforma a la Ley Bitcoin (Decreto 918, 2025) | legislation | 1 | **REGISTERED** | MAJOR | #2380 Reforma a la Ley Bitcoin (Decreto 918, 2025) (`is_current=0`, `SV-MISC`) | title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-AML-OLD` | Ley Contra el Lavado de Dinero y de Activos (previous law) | legislation | 1 | **REGISTERED** | MINOR | #2375 Ley Contra el Lavado de Dinero y de Activos (`is_current=0`, `SV-AML`) | title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-BCR-LPB` | Lineamientos para Plataforma Tecnológica Bitcoin/Dólares (BCR) | rulebook | 1 | **REGISTERED** | MINOR | #2383 Lineamientos para Plataforma Tecnológica Bitcoin/Dólares (BCR) (`is_current=0`, `SV-BTC`) | title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-BCR-NRP29` | NRP-29: Participación de PSAV en Sistemas de Pago (BCR) | rulebook | 1 | **REGISTERED** | MINOR | #2382 NRP-29: Participación de PSAV en Sistemas de Pago (BCR) (`is_current=0`, `SV-DASP`) | title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-BCR-NT` | Normas Técnicas para Facilitar la Aplicación de la Ley Bitcoin (BCR) | rulebook | 1 | **REGISTERED** | MINOR | #2343 Normas Técnicas para Facilitar la Aplicación de la Ley Bitcoin (BCR) (`is_current=0`, `SV-BTC`) | title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-BTC-REG` | Reglamento de la Ley Bitcoin (Decreto Ejecutivo 27, 2021) | rulebook | 1 | **REGISTERED** | MINOR | #2384 Reglamento de la Ley Bitcoin (Decreto Ejecutivo 27, 2021) (`is_current=0`, `SV-BTC`) | title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-BTC-TRUST` | Ley del Fideicomiso Bitcoin (Decreto 137, 2022) | legislation | 1 | **REGISTERED** | MINOR | #2340 Ley del Fideicomiso Bitcoin (Decreto 137, 2022) (`is_current=0`, `SV-BTC`) | title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-LOC-ANALYSIS` | Library of Congress: El Salvador Bitcoin Law Analysis [English] | guidance | 2 | **REGISTERED** | MINOR | #2379 Library of Congress: El Salvador Bitcoin Law Analysis [English] (`is_current=0`, `SV-BTC`) | title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-LEAD-ES` | Ley de Emisión de Activos Digitales (Decreto 643, 2023) [Español] | legislation | 1 | **PARTIAL** | MAJOR | #2341 Reformas a la Ley de Emisión de Activos Digitales (2024) (`is_current=1`, `SV-LEAD24`) | title | MISSING — Spanish authoritative version not ingested |
| `SV-LBAN-COOP` | Ley de Bancos Cooperativos y Sociedades de Ahorro y Crédito | legislation | 1 | **PARTIAL** | MINOR | #2373 Ley de Bancos Cooperativos y Sociedades de Ahorro y Crédito (`is_current=1`, `SV-LBAN`) | title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-AML` | Ley Especial para la Prevención del Lavado de Dinero (Decreto 426, 2025) | legislation | 1 | **PRESENT** | CRITICAL | #2381 Ley Especial para la Prevención del Lavado de Dinero (Decreto 426, 2025) (`is_current=1`, `SV-AML`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-BTC` | Ley Bitcoin (Decreto Legislativo No. 57, 2021) | legislation | 1 | **PRESENT** | CRITICAL | #2342 Ley Bitcoin (Decreto Legislativo No. 57, 2021) (`is_current=1`, `SV-BTC`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-DASP` | CNAD DASP Regulation [English] | rulebook | 1 | **PRESENT** | CRITICAL | #2389 CNAD DASP Regulation [English] (`is_current=1`, `SV-DASP`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-LEAD` | Digital Asset Issuance Law (Decreto 643, 2023) [English] | legislation | 1 | **PRESENT** | CRITICAL | #2378 Digital Asset Issuance Law (Decreto 643, 2023) [English] (`is_current=1`, `SV-LEAD`) | code+title | EXISTS in SQLite (doc_id 2378) — rulebook_code=null. Fix in Phase 5. |
| `SV-LEAD24` | Reformas a la Ley de Emisión de Activos Digitales (2024) | legislation | 1 | **PRESENT** | CRITICAL | #2341 Reformas a la Ley de Emisión de Activos Digitales (2024) (`is_current=1`, `SV-LEAD24`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-AML-GUIDE` | CNAD AML/CFT Compliance Guide [English] | guidance | 2 | **PRESENT** | MAJOR | #2385 CNAD AML/CFT Compliance Guide [English] (`is_current=1`, `SV-AML-GUIDE`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-ISS` | CNAD Issuer Registration Regulation [English] | rulebook | 1 | **PRESENT** | MAJOR | #2388 CNAD Issuer Registration Regulation [English] (`is_current=1`, `SV-ISS`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-LBAN` | Ley de Bancos | legislation | 1 | **PRESENT** | MAJOR | #2373 Ley de Bancos Cooperativos y Sociedades de Ahorro y Crédito (`is_current=1`, `SV-LBAN`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-LSSF` | Ley de Supervisión y Regulación del Sistema Financiero | legislation | 1 | **PRESENT** | MAJOR | #2372 Ley de Supervisión y Regulación del Sistema Financiero (`is_current=1`, `SV-LSSF`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-STBL` | CNAD Stablecoin Regulation [English] | rulebook | 1 | **PRESENT** | MAJOR | #2387 CNAD Stablecoin Regulation [English] (`is_current=1`, `SV-STBL`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-ANNUAL` | CNAD Annual Report 2023-2024 | guidance | 2 | **PRESENT** | MINOR | #2386 CNAD Annual Report 2023-2024 (`is_current=1`, `SV-ANNUAL`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |
| `SV-LMV` | Ley del Mercado de Valores | legislation | 1 | **PRESENT** | MINOR | #2374 Ley del Mercado de Valores (`is_current=1`, `SV-LMV`) | code+title | EXISTS in SQLite — rulebook_code=null. Fix in Phase 5. |

## Gaps — action list (critical / major first)

- **[MAJOR] REGISTERED** — `SV-BTC-2025` Reforma a la Ley Bitcoin (Decreto 918, 2025) — EXISTS in SQLite — rulebook_code=null. Fix in Phase 5.
- **[MAJOR] MISSING** — `SV-DASP-ES` Reglamento DASP CNAD [Español] — MISSING — Spanish original not ingested
- **[MAJOR] MISSING** — `SV-UIF` UIF Instructions applicable to DASPs — MISSING — UIF financial intelligence unit instructions not ingested
- **[MINOR] REGISTERED** — `SV-AML-OLD` Ley Contra el Lavado de Dinero y de Activos (previous law) — EXISTS in SQLite — rulebook_code=null. Fix in Phase 5.
- **[MINOR] REGISTERED** — `SV-BTC-TRUST` Ley del Fideicomiso Bitcoin (Decreto 137, 2022) — EXISTS in SQLite — rulebook_code=null. Fix in Phase 5.
- **[MINOR] REGISTERED** — `SV-BCR-NRP29` NRP-29: Participación de PSAV en Sistemas de Pago (BCR) — EXISTS in SQLite — rulebook_code=null. Fix in Phase 5.
- **[MINOR] REGISTERED** — `SV-BCR-LPB` Lineamientos para Plataforma Tecnológica Bitcoin/Dólares (BCR) — EXISTS in SQLite — rulebook_code=null. Fix in Phase 5.
- **[MINOR] REGISTERED** — `SV-BCR-NT` Normas Técnicas para Facilitar la Aplicación de la Ley Bitcoin (BCR) — EXISTS in SQLite — rulebook_code=null. Fix in Phase 5.
- **[MINOR] REGISTERED** — `SV-BTC-REG` Reglamento de la Ley Bitcoin (Decreto Ejecutivo 27, 2021) — EXISTS in SQLite — rulebook_code=null. Fix in Phase 5.
- **[MINOR] REGISTERED** — `SV-LOC-ANALYSIS` Library of Congress: El Salvador Bitcoin Law Analysis [English] — EXISTS in SQLite — rulebook_code=null. Fix in Phase 5.

## Orphan corpus documents

_Documents in corpus.db for this jurisdiction that did not match any authoritative inventory item. Either the inventory is incomplete, or these are superseded / mis-attributed._

| Corpus ID | Title | source_entity | rulebook_code | is_current | doc_type |
|---|---|---|---|---|---|
| 2710 | Cnad Download | `EL_SALVADOR` | `SV-MISC` | 1 | rulebook |
| 2568 | CNAD Legal Framework — Reference Page | `EL_SALVADOR` | `SV-CNAD-FRAMEWORK` | 1 | guidance |
| 2569 | CNAD Documentation Library — Reference Page | `EL_SALVADOR` | `SV-CNAD-DOCS` | 1 | guidance |
| 2591 | Código de Comercio de El Salvador (Decreto 671, 1970 — ed. 2008) | `EL_SALVADOR` | `SV-CC` | 1 | company_law |
| 2732 | Cnad Documentation Library | `EL_SALVADOR` | `SV-MISC` | 0 | guidance |

## Method

1. **Authoritative inventory** — `expected_documents` from the jurisdiction manifest. Manifests are the curated source of truth; the regulator's published URL is HEAD-checked only for reachability (header line above).
2. **Corpus enumeration** — `documents` rows whose `source_entity` is in the configured set, read-only.
3. **Matching**, strongest basis wins:
   - `code` — manifest `corpus_code` vs corpus `rulebook_code`, compared on the trailing dash-segment (strong).
   - `source_url` — manifest `source_url` vs corpus `source_url`, scheme-stripped, substring-tolerant (strong).
   - `title` — token-set overlap coefficient ≥ 0.6 after lowercasing and version/punctuation stripping (weak).
4. **Status**:
   - `PRESENT` — a strong match to an `is_current=1` corpus doc.
   - `PARTIAL` — only a weak (title-only) match to a current doc; needs human verification.
   - `REGISTERED` — matched corpus doc(s), but none flagged `is_current=1` (older version ingested, current not marked).
   - `MISSING` — no corpus document matched.
