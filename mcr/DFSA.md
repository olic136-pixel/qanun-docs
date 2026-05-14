# Material Completeness Register — DIFC Dubai Financial Services Authority

**Jurisdiction code:** `DFSA`  
**Regulator:** Dubai Financial Services Authority (DFSA)  
**Generated:** 2026-05-14T18:51:23.121968+00:00  
**Corpus DB:** `/Users/oliver/ADGM/adgm-corpus/corpus.db` (sha256 `c061d461e1ab68cd…`, opened read-only)  
**Authoritative inventory:** `/Users/oliver/ADGM/adgm-corpus/adgm_corpus/manifests/DFSA.json` (22 expected documents)  
**Corpus source entities:** `DFSA` (43 documents in corpus)  
**Primary source index:** https://dfsaen.thomsonreuters.com/rulebook/dubai-financial-services-authority-dfsa — HTTP 200 (reachable)  

> **Template note.** The L9 session brief truncated before the MCR file template, and the plan file it referenced (`overnight_throughput_plan_2026-05-16.md`) does not exist. This structure was reconstructed from the `corpus_completeness` table schema and `adgm_corpus/manifests/MANIFEST_SCHEMA.json` (canonical status values: PRESENT / REGISTERED / PARTIAL / MISSING), styled after `dfsa_inventory_authoritative.md`. Adjust the shape if the intended template differs.

## Headline

- **Expected (authoritative):** 22
- **PRESENT** (current corpus doc matched): 21 (95%)
- **REGISTERED** (matched, but no `is_current=1` version): 0
- **PARTIAL** (matched by title heuristic only — verify): 1
- **MISSING** (no corpus document matched): 0
- **Critical gaps:** 0
- **Orphan corpus documents** (in corpus, not in authoritative inventory): 0

## Register

| Code | Authoritative document | Type | Tier | Status | Gap severity | Matched corpus doc | Match basis | Notes |
|---|---|---|---|---|---|---|---|---|
| `DFSA-CRYPTO-GUIDE` | Supervisory Guidelines on Assessing Suitability of Crypto Tokens | guidance | 2 | **PARTIAL** | MINOR | #2428 Supervisory Guidelines on Assessing the Suitability of Crypto Tokens (`is_current=1`) | title | EXISTS in SQLite (doc_id 2428) — 34k words |
| `DFSA-AML` | Anti-Money Laundering Module (AML) | rulebook | 1 | **PRESENT** | CRITICAL | #2814 DFSA AML Rulebook (`is_current=1`, `DFSA-AML`) | code+title | EXISTS in SQLite (doc_id 2441) |
| `DFSA-COB` | Conduct of Business Module (COB) | rulebook | 1 | **PRESENT** | MAJOR | #2818 DFSA COB Rulebook (`is_current=1`, `DFSA-COB`) | code+title | EXISTS in SQLite (doc_id 2448) |
| `DFSA-GEN` | General Module (GEN) | rulebook | 1 | **PRESENT** | MAJOR | #2821 DFSA GEN Rulebook (`is_current=1`, `DFSA-GEN`) | code+title | EXISTS in SQLite (doc_id 2421) |
| `DFSA-MKT` | Markets Rules (MKT) | rulebook | 1 | **PRESENT** | MAJOR | #2824 DFSA MKT Rulebook (`is_current=1`, `DFSA-MKT`) | code+title | EXISTS in SQLite (doc_id 2450) |
| `DFSA-PIB` | Prudential Investment Business Module (PIB) | rulebook | 1 | **PRESENT** | MAJOR | #2825 DFSA PIB Rulebook (`is_current=1`, `DFSA-PIB`) | code+title | EXISTS in SQLite (doc_id 2440) — 140k words |
| `DFSA-AFN` | Application Forms and Notices Module (AFN) | rulebook | 1 | **PRESENT** | MINOR | #2812 DFSA AFN Rulebook (`is_current=1`, `DFSA-AFN`) | code+title | EXISTS in SQLite (doc_id 2432) — no version metadata |
| `DFSA-AMI` | Authorised Market Institutions Module (AMI) | rulebook | 1 | **PRESENT** | MINOR | #2813 DFSA AMI Rulebook (`is_current=1`, `DFSA-AMI`) | code+title | EXISTS in SQLite (doc_id 2433) |
| `DFSA-AUD` | Auditor Module (AUD) | rulebook | 1 | **PRESENT** | MINOR | #2815 DFSA AUD Rulebook (`is_current=1`, `DFSA-AUD`) | code+title | EXISTS in SQLite (doc_id 2443) |
| `DFSA-CIR` | Collective Investment Rules (CIR) | rulebook | 1 | **PRESENT** | MINOR | #2816 DFSA CIR Rulebook (`is_current=1`, `DFSA-CIR`) | code+title | EXISTS in SQLite (doc_id 2447) |
| `DFSA-CMC` | CMC Module | rulebook | 1 | **PRESENT** | MINOR | #2817 DFSA CMC Rulebook (`is_current=1`, `DFSA-CMC`) | code+title | EXISTS in SQLite (doc_id 2449) |
| `DFSA-FER` | Fee Module (FER) | rulebook | 1 | **PRESENT** | MINOR | #2819 DFSA FER Rulebook (`is_current=1`, `DFSA-FER`) | code+title | EXISTS in SQLite (doc_id 2444) |
| `DFSA-FPR` | Fees and Penalties Rules (FPR) | rulebook | 1 | **PRESENT** | MINOR | #2820 DFSA FPR Rulebook (`is_current=1`, `DFSA-FPR`) | code+title | EXISTS in SQLite (doc_id 2445) |
| `DFSA-GLO` | Glossary Module (GLO) | rulebook | 1 | **PRESENT** | MINOR | #2822 DFSA GLO Rulebook (`is_current=1`, `DFSA-GLO`) | code+title | EXISTS in SQLite (doc_id 2438) |
| `DFSA-IFR` | Islamic Finance Rules (IFR) | rulebook | 1 | **PRESENT** | MINOR | #2823 DFSA IFR Rulebook (`is_current=1`, `DFSA-IFR`) | code+title | EXISTS in SQLite (doc_id 2436) |
| `DFSA-PIN` | Prudential Insurance Business Module (PIN) | rulebook | 1 | **PRESENT** | MINOR | #2826 DFSA PIN Rulebook (`is_current=1`, `DFSA-PIN`) | code+title | EXISTS in SQLite (doc_id 2434) |
| `DFSA-PRS` | Private Placements Rules (PRS) | rulebook | 1 | **PRESENT** | MINOR | #2827 DFSA PRS Rulebook (`is_current=1`, `DFSA-PRS`) | code+title | EXISTS in SQLite (doc_id 2435) |
| `DFSA-PRU` | Prudential Returns Module (PRU) | rulebook | 1 | **PRESENT** | MINOR | #2828 DFSA PRU Rulebook (`is_current=1`, `DFSA-PRU`) | code+title | EXISTS in SQLite (doc_id 2431) — 92k words |
| `DFSA-RAR` | Regulatory Appeals Rules (RAR) | rulebook | 1 | **PRESENT** | MINOR | #2829 DFSA RAR Rulebook (`is_current=1`, `DFSA-RAR`) | code+title | EXISTS in SQLite (doc_id 2437) |
| `DFSA-REC` | Recognised Bodies Module (REC) | rulebook | 1 | **PRESENT** | MINOR | #2830 DFSA REC Rulebook (`is_current=1`, `DFSA-REC`) | code+title | EXISTS in SQLite (doc_id 2439) |
| `DFSA-REP` | Reporting Module (REP) | rulebook | 1 | **PRESENT** | MINOR | #2831 DFSA REP Rulebook (`is_current=1`, `DFSA-REP`) | code+title | EXISTS in SQLite (doc_id 2442) |
| `DFSA-TKO` | Takeover Rules (TKO) | rulebook | 1 | **PRESENT** | MINOR | #2832 DFSA TKO Rulebook (`is_current=1`, `DFSA-TKO`) | code+title | EXISTS in SQLite (doc_id 2446) |

## Gaps — action list (critical / major first)

_No MISSING or REGISTERED items — every authoritative document has a current corpus match._

## Orphan corpus documents

_Documents in corpus.db for this jurisdiction that did not match any authoritative inventory item. Either the inventory is incomplete, or these are superseded / mis-attributed._

_None — every corpus document matched an inventory item._

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
