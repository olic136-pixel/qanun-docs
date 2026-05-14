# Material Completeness Register — British Virgin Islands Financial Services Commission

**Jurisdiction code:** `BVI`  
**Regulator:** BVI Financial Services Commission (FSC)  
**Generated:** 2026-05-14T18:51:25.552158+00:00  
**Corpus DB:** `/Users/oliver/ADGM/adgm-corpus/corpus.db` (sha256 `c061d461e1ab68cd…`, opened read-only)  
**Authoritative inventory:** `/Users/oliver/ADGM/adgm-corpus/adgm_corpus/manifests/BVI_FSC.json` (12 expected documents)  
**Corpus source entities:** `BVI_FSC` (30 documents in corpus)  
**Primary source index:** https://www.bvifsc.vg — HTTP 200 (reachable)  

> **Template note.** The L9 session brief truncated before the MCR file template, and the plan file it referenced (`overnight_throughput_plan_2026-05-16.md`) does not exist. This structure was reconstructed from the `corpus_completeness` table schema and `adgm_corpus/manifests/MANIFEST_SCHEMA.json` (canonical status values: PRESENT / REGISTERED / PARTIAL / MISSING), styled after `dfsa_inventory_authoritative.md`. Adjust the shape if the intended template differs.

## Headline

- **Expected (authoritative):** 12
- **PRESENT** (current corpus doc matched): 11 (92%)
- **REGISTERED** (matched, but no `is_current=1` version): 0
- **PARTIAL** (matched by title heuristic only — verify): 1
- **MISSING** (no corpus document matched): 0
- **Critical gaps:** 0
- **Orphan corpus documents** (in corpus, not in authoritative inventory): 10

## Register

| Code | Authoritative document | Type | Tier | Status | Gap severity | Matched corpus doc | Match basis | Notes |
|---|---|---|---|---|---|---|---|---|
| `BVI-PIF` | Private Investment Funds Act 2019 | legislation | 1 | **PARTIAL** | MAJOR | #2576 Mutual Funds Act (`is_current=1`, `BVI-MFA`) | title | Not confirmed in Pinecone — verify in Phase 4 pre-flight |
| `BVI-AML` | AML and Terrorist Financing Code of Practice | legislation | 1 | **PRESENT** | CRITICAL | #2570 Anti Money Laundering And Terrorist Financing Code Of Practice (`is_current=1`, `BVI-AML`) | code+title | Confirmed in Pinecone — BVI-AML Part III verified |
| `BVI-AMLR` | Anti-Money Laundering Regulations | legislation | 1 | **PRESENT** | CRITICAL | #2571 Anti Money Laundering Regulations (`is_current=1`, `BVI-AMLR`) | code+title | Confirmed in Pinecone — BVI-AMLR Reg.2 verified |
| `BVI-BCA` | BVI Business Companies Act 2004 | legislation | 1 | **PRESENT** | CRITICAL | #2756 Bvi Business Companies Act Schedules (`is_current=1`, `BVI-BCA`) | code+title | CONFIRMED MISSING from corpus. Manual sourcing required. Open item — SOW Section 13. |
| `BVI-BCA-2022` | BVI Business Companies Act 2004 (2022 Amendments) | legislation | 1 | **PRESENT** | CRITICAL | #2739 Anti Money Laundering Amendment Regulations 2022 (`is_current=1`, `BVI-AML-AMD-2022`) | code | CONFIRMED MISSING from corpus. Manual sourcing required. Open item — SOW Section 13. |
| `BVI-MFA` | Mutual Funds Act | legislation | 1 | **PRESENT** | CRITICAL | #2576 Mutual Funds Act (`is_current=1`, `BVI-MFA`) | code+title | Confirmed in Pinecone — BVI-MFA Part IV verified |
| `BVI-RC` | Regulatory Code 2009 | legislation | 1 | **PRESENT** | CRITICAL | #2578 Regulatory Code 2009 (`is_current=1`, `BVI-RC`) | code+title | Confirmed in Pinecone — BVI-RC Schedule 6 verified |
| `BVI-SIBA` | Securities and Investment Business Act 2010 | legislation | 1 | **PRESENT** | CRITICAL | #2579 Securities And Investment Business Act 2010 (`is_current=1`, `BVI-SIBA`) | code+title | Confirmed in Pinecone — section_ref BVI-SIBA Part III verified |
| `BVI-FMSA` | Financing and Money Services Act 2009 | legislation | 1 | **PRESENT** | MAJOR | #2580 Financing And Money Services Act 2009 (`is_current=1`, `BVI-FMSA`) | code+title | Referenced in BVI-RC but not confirmed as standalone document in corpus |
| `BVI-REGS` | Investment Business (Approved Managers) Regulations 2012 | legislation | 1 | **PRESENT** | MAJOR | #2589 Investment Business (Approved Managers) Regulations 2012 (S.I. 2012 No. 54) (`is_current=1`, `BVI-REGS`) | code+title | Confirmed in Pinecone — BVI-REGS Reg.9 verified |
| `BVI-VASPA` | Virtual Assets Service Providers Act 2022 | legislation | 1 | **PRESENT** | MAJOR | #2737 Virtual Assets Service Providers Act 2022 (`is_current=1`, `BVI-VASPA`) | code+title | Confirmed in Pinecone — BVI-VASPA Part I verified |
| `BVI-BO-GUIDE` | BVIFSC Beneficial Ownership Guidance | guidance | 2 | **PRESENT** | MINOR | #2735 Bvifsc Beneficial Ownership Guidance (`is_current=1`, `BVI-BO-GUIDE`) | code+title | Confirmed in Pinecone |

## Gaps — action list (critical / major first)

_No MISSING or REGISTERED items — every authoritative document has a current corpus match._

## Orphan corpus documents

_Documents in corpus.db for this jurisdiction that did not match any authoritative inventory item. Either the inventory is incomplete, or these are superseded / mis-attributed._

| Corpus ID | Title | source_entity | rulebook_code | is_current | doc_type |
|---|---|---|---|---|---|
| 2734 | Vasp Travel Guidance | `BVI_FSC` | `BVI-VASP-TRAVEL` | 1 | guidance |
| 2740 | Proliferation Financing Prohibition Act | `BVI_FSC` | `BVI-PFA` | 1 | legislation |
| 2744 | Proceeds Of Criminal Conduct Act | `BVI_FSC` | `BVI-PCCA` | 1 | legislation |
| 2575 | Financial Services Commission Act | `BVI_FSC` | `BVI-FSCA` | 1 | legislation |
| 2745 | Economic Substance Companies And Ltd Partnerships Act | `BVI_FSC` | `BVI-ESA` | 1 | legislation |
| 2746 | Act No. 3 Of 2021 Data Protection Act, 2021 | `BVI_FSC` | `BVI-DPA` | 1 | legislation |
| 2736 | Counter Terrorism Act 2021 | `BVI_FSC` | `BVI-CTA` | 1 | legislation |
| 2574 | Company Management Act 1990 | `BVI_FSC` | `BVI-CMA` | 1 | legislation |
| 2572 | Banks And Trust Companies Act | `BVI_FSC` | `BVI-BTCA` | 1 | legislation |
| 2741 | Beneficial Ownership Secure Search System Act | `BVI_FSC` | `BVI-BOSS` | 1 | legislation |

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
