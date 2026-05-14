# Material Completeness Register — Dubai Virtual Assets Regulatory Authority

**Jurisdiction code:** `VARA`  
**Regulator:** Dubai Virtual Assets Regulatory Authority (VARA)  
**Generated:** 2026-05-14T18:51:17.765830+00:00  
**Corpus DB:** `/Users/oliver/ADGM/adgm-corpus/corpus.db` (sha256 `c061d461e1ab68cd…`, opened read-only)  
**Authoritative inventory:** `/Users/oliver/ADGM/adgm-corpus/adgm_corpus/manifests/VARA.json` (12 expected documents)  
**Corpus source entities:** `VARA` (28 documents in corpus)  
**Primary source index:** https://rulebooks.vara.ae — HTTP 200 (reachable)  

> **Template note.** The L9 session brief truncated before the MCR file template, and the plan file it referenced (`overnight_throughput_plan_2026-05-16.md`) does not exist. This structure was reconstructed from the `corpus_completeness` table schema and `adgm_corpus/manifests/MANIFEST_SCHEMA.json` (canonical status values: PRESENT / REGISTERED / PARTIAL / MISSING), styled after `dfsa_inventory_authoritative.md`. Adjust the shape if the intended template differs.

## Headline

- **Expected (authoritative):** 12
- **PRESENT** (current corpus doc matched): 12 (100%)
- **REGISTERED** (matched, but no `is_current=1` version): 0
- **PARTIAL** (matched by title heuristic only — verify): 0
- **MISSING** (no corpus document matched): 0
- **Critical gaps:** 0
- **Orphan corpus documents** (in corpus, not in authoritative inventory): 0

## Register

| Code | Authoritative document | Type | Tier | Status | Gap severity | Matched corpus doc | Match basis | Notes |
|---|---|---|---|---|---|---|---|---|
| `VARA-COMP` | Company Rulebook V2.0 | rulebook | 1 | **PRESENT** | CRITICAL | #2800 Company Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-COMP`) | code+title | V1+V2 both in Pinecone with is_current=true — V2 is authoritative. Fix in Phase 3. |
| `VARA-CRM` | Compliance and Risk Management Rulebook | rulebook | 1 | **PRESENT** | CRITICAL | #2801 Compliance and Risk Management Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-CRM`) | code+title |  |
| `VARA-MC` | Market Conduct Rulebook | rulebook | 1 | **PRESENT** | CRITICAL | #2803 Market Conduct Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-MC`) | code+title | Confirmed in Pinecone — section_ref VARA-MC VII.A.3 verified |
| `VARA-TI` | Technology and Information Rulebook | rulebook | 1 | **PRESENT** | CRITICAL | #2802 Technology and Information Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-TI`) | code+title | Confirmed in Pinecone — section_ref VARA-TI I.A.6 verified |
| `VARA-ADV` | Advisory Services Rulebook | rulebook | 1 | **PRESENT** | MAJOR | #2811 Advisory Services Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-ADV`) | code+title | Confirmed in Pinecone — VARA-ADV Schedule 1 verified |
| `VARA-BD` | Broker-Dealer Services Rulebook V2.0 | rulebook | 1 | **PRESENT** | MAJOR | #2804 Broker-Dealer Services Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-BD`) | code+title | V1+V2 duplicate in Pinecone — fix in Phase 3 |
| `VARA-CUST` | Custody Services Rulebook V2.0 | rulebook | 1 | **PRESENT** | MAJOR | #2806 Custody Services Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-CUST`) | code+title | V1+V2 duplicate in Pinecone — fix in Phase 3 |
| `VARA-EX` | Exchange Services Rulebook V2.0 | rulebook | 1 | **PRESENT** | MAJOR | #2805 Exchange Services Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-EX`) | code+title | V1+V2 duplicate in Pinecone — fix in Phase 3 |
| `VARA-ISS` | Virtual Asset Issuance Rulebook | rulebook | 1 | **PRESENT** | MAJOR | #2810 Virtual Asset Issuance Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-ISS`) | code+title |  |
| `VARA-LB` | Lending and Borrowing Services Rulebook | rulebook | 1 | **PRESENT** | MAJOR | #2808 Lending and Borrowing Services Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-LB`) | code+title | UNCONFIRMED in Pinecone — verify in Phase 3 pre-flight |
| `VARA-MGMT` | VA Management and Investment Services Rulebook | rulebook | 1 | **PRESENT** | MAJOR | #2807 VA Management and Investment Services Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-MGMT`) | code+title | UNCONFIRMED in Pinecone — verify in Phase 3 pre-flight |
| `VARA-TRS` | VA Transfer and Settlement Services Rulebook V2.0 | rulebook | 1 | **PRESENT** | MAJOR | #2809 VA Transfer and Settlement Services Rulebook \| Virtual Assets Regulatory Authority (VARA) (`is_current=1`, `VARA-TRS`) | code+title | V1+V2 duplicate in Pinecone — fix in Phase 3 |

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
