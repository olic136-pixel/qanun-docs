# Material Completeness Register — Panama Superintendencia del Mercado de Valores

**Jurisdiction code:** `PANAMA`  
**Regulator:** Superintendencia del Mercado de Valores (SMV), Panama  
**Generated:** 2026-05-14T18:51:33.488613+00:00  
**Corpus DB:** `/Users/oliver/ADGM/adgm-corpus/corpus.db` (sha256 `c061d461e1ab68cd…`, opened read-only)  
**Authoritative inventory:** `/Users/oliver/ADGM/adgm-corpus/adgm_corpus/manifests/PANAMA_SMV.json` (8 expected documents)  
**Corpus source entities:** `PANAMA_SMV`, `PANAMA` (7 documents in corpus)  
**Primary source index:** https://supervalores.gob.pa — HTTP 200 (reachable)  

> **Template note.** The L9 session brief truncated before the MCR file template, and the plan file it referenced (`overnight_throughput_plan_2026-05-16.md`) does not exist. This structure was reconstructed from the `corpus_completeness` table schema and `adgm_corpus/manifests/MANIFEST_SCHEMA.json` (canonical status values: PRESENT / REGISTERED / PARTIAL / MISSING), styled after `dfsa_inventory_authoritative.md`. Adjust the shape if the intended template differs.

## Headline

- **Expected (authoritative):** 8
- **PRESENT** (current corpus doc matched): 5 (62%)
- **REGISTERED** (matched, but no `is_current=1` version): 0
- **PARTIAL** (matched by title heuristic only — verify): 0
- **MISSING** (no corpus document matched): 3
- **Critical gaps:** 1: `PAN-SMV-GESTORAS`
- **Orphan corpus documents** (in corpus, not in authoritative inventory): 2

## Register

| Code | Authoritative document | Type | Tier | Status | Gap severity | Matched corpus doc | Match basis | Notes |
|---|---|---|---|---|---|---|---|---|
| `PAN-SMV-GESTORAS` | Acuerdo SMV — Gestoras de Inversión | rulebook | 1 | **MISSING** | CRITICAL | — | — | CONFIRMED MISSING. SMV regulatory decree for fund managers. Open item — SOW Section 13. |
| `PAN-UAF` | Instrucciones UAF — Sujetos Obligados Financieros | guidance | 2 | **MISSING** | MAJOR | — | — | CONFIRMED MISSING. UAF financial intelligence unit instructions. |
| `PAN-UBO` | Ley 129 de 2020 — Registro Único de Beneficiarios Finales | legislation | 1 | **MISSING** | MAJOR | — | — | Referenced in PAN-LEY32 text but not ingested as standalone document |
| `PAN-AML` | Ley 23 de 2015 — Medidas para Prevenir el Blanqueo de Capitales | legislation | 1 | **PRESENT** | CRITICAL | #2582 Ley 23 De 2015 Blanqueo Seccion Valores (`is_current=1`, `PAN-AML`) | code+title | CONFIRMED MISSING. Priority gap. Open item — SOW Section 13. |
| `PAN-LMV` | Ley de Valores (Texto Único Decreto Ley 1 de 1999) | legislation | 1 | **PRESENT** | CRITICAL | #2585 Texto Unico Dl1 1999 Ley De Valores (`is_current=1`, `PAN-LMV`) | code+title | Confirmed in Pinecone under PANAMA_SMV — no SQLite row yet. Phase 4. |
| `PAN-LMV-67` | Ley 67 de 2011 (Reforma Ley de Valores) | legislation | 1 | **PRESENT** | CRITICAL | #2584 Ley 67 De 2011 (`is_current=1`, `PAN-LMV-67`) | code+title | Confirmed in Pinecone under PANAMA_SMV — no SQLite row yet. Phase 4. |
| `PAN-LEY32` | Ley 32 de 1927 — Sociedades Anónimas | legislation | 1 | **PRESENT** | MAJOR | #2590 Ley 32 de 1927 — Sobre Sociedades Anónimas (Panamá) (`is_current=1`, `PAN-LEY32`) | code+title | Confirmed in Pinecone under PANAMA entity — consolidate to PANAMA_SMV in Phase 4 |
| `PAN-LEY52` | Ley 52 de 2016 — Registros Contables de Personas Jurídicas | legislation | 1 | **PRESENT** | MAJOR | #2663 Pan Ley52 (`is_current=1`, `PAN-LEY52`) | code | Confirmed in Pinecone under PANAMA entity — consolidate to PANAMA_SMV in Phase 4 |

## Gaps — action list (critical / major first)

- **[CRITICAL] MISSING** — `PAN-SMV-GESTORAS` Acuerdo SMV — Gestoras de Inversión — CONFIRMED MISSING. SMV regulatory decree for fund managers. Open item — SOW Section 13.
- **[MAJOR] MISSING** — `PAN-UBO` Ley 129 de 2020 — Registro Único de Beneficiarios Finales — Referenced in PAN-LEY32 text but not ingested as standalone document
- **[MAJOR] MISSING** — `PAN-UAF` Instrucciones UAF — Sujetos Obligados Financieros — CONFIRMED MISSING. UAF financial intelligence unit instructions.

## Orphan corpus documents

_Documents in corpus.db for this jurisdiction that did not match any authoritative inventory item. Either the inventory is incomplete, or these are superseded / mis-attributed._

| Corpus ID | Title | source_entity | rulebook_code | is_current | doc_type |
|---|---|---|---|---|---|
| 2581 | Ley 12 De 2012 Seguros | `PANAMA_SMV` | `PAN-LSEG` | 1 | legislation |
| 2583 | Ley 56 De 2012 | `PANAMA_SMV` | `PAN-LMV-56` | 1 | legislation |

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
