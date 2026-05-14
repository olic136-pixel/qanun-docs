# Material Completeness Register — ADGM Financial Services Regulatory Authority

**Jurisdiction code:** `ADGM`  
**Regulator:** ADGM Financial Services Regulatory Authority (FSRA)  
**Generated:** 2026-05-14T18:51:20.145163+00:00  
**Corpus DB:** `/Users/oliver/ADGM/adgm-corpus/corpus.db` (sha256 `c061d461e1ab68cd…`, opened read-only)  
**Authoritative inventory:** `/Users/oliver/ADGM/adgm-corpus/adgm_corpus/manifests/FSRA.json` (14 expected documents)  
**Corpus source entities:** `FSRA`, `ADGM FSRA`, `ADGM_RA`, `ADGM` (1115 documents in corpus)  
**Primary source index:** https://en.adgm.thomsonreuters.com/rulebook/fsra-legislation — HTTP 403 (error)  

> **Template note.** The L9 session brief truncated before the MCR file template, and the plan file it referenced (`overnight_throughput_plan_2026-05-16.md`) does not exist. This structure was reconstructed from the `corpus_completeness` table schema and `adgm_corpus/manifests/MANIFEST_SCHEMA.json` (canonical status values: PRESENT / REGISTERED / PARTIAL / MISSING), styled after `dfsa_inventory_authoritative.md`. Adjust the shape if the intended template differs.

## Headline

- **Expected (authoritative):** 14
- **PRESENT** (current corpus doc matched): 14 (100%)
- **REGISTERED** (matched, but no `is_current=1` version): 0
- **PARTIAL** (matched by title heuristic only — verify): 0
- **MISSING** (no corpus document matched): 0
- **Critical gaps:** 0
- **Orphan corpus documents** (in corpus, not in authoritative inventory): 728

## Register

| Code | Authoritative document | Type | Tier | Status | Gap severity | Matched corpus doc | Match basis | Notes |
|---|---|---|---|---|---|---|---|---|
| `AML` | AML/CFT Rulebook VER10.020125 | rulebook | 1 | **PRESENT** | CRITICAL | #200 Adgm1547 5692 Ver10020125 (`is_current=1`, `AML`) | code |  |
| `COBS` | Conduct of Business Rulebook VER21.010126 | rulebook | 1 | **PRESENT** | CRITICAL | #2788 Cobs Ver23.290426 (`is_current=1`, `COBS`) | code |  |
| `GEN` | General Rulebook VER12.311025 | rulebook | 1 | **PRESENT** | CRITICAL | #2790 Gen Ver13.270426 (`is_current=1`, `GEN`) | code |  |
| `MKT` | Markets Rulebook VER08.181223 | rulebook | 1 | **PRESENT** | CRITICAL | #2833 FSRA MKT Rulebook (`is_current=1`, `MKT`) | code | Full consolidated rulebook VER10.311025 ingested in Phase 6. |
| `PRU` | Prudential Rulebook VER13.181223 | rulebook | 1 | **PRESENT** | CRITICAL | #2795 Pru Ver20.270426 (`is_current=1`, `PRU`) | code | VER13 from Dec 2023 — check portal for newer version |
| `FSMR` | Financial Services and Markets Regulations 2015 Consolidated | legislation | 1 | **PRESENT** | MAJOR | #99 Adgm1547 12483 Ver28311025 (`is_current=1`, `FSMR`) | code |  |
| `FUNDS` | Funds Rulebook VER19.010126 | rulebook | 1 | **PRESENT** | MAJOR | #2789 Funds Ver12.290426 (`is_current=1`, `FUNDS`) | code+title |  |
| `GLO` | Glossary VER25.010126 | rulebook | 1 | **PRESENT** | MAJOR | #2792 Glo Ver27.290426 (`is_current=1`, `GLO`) | code |  |
| `REP` | Regulatory Returns Module | rulebook | 1 | **PRESENT** | MAJOR | #304 Adgm Courts Guidelines For Self Represented Litigants (English)04042025 (`is_current=1`, `REP`) | code | REP not confirmed as a standalone FSRA module on TR portal. Possible data dispersal artefact. Gap retained as MISSING pending practitioner confirmation. |
| `CIB` | Covered Investment Business Rulebook VER06.290725 | rulebook | 1 | **PRESENT** | MINOR | #62 Adgm1547 9385 Ver06290725 (`is_current=1`, `CIB`) | code |  |
| `FEES` | Fees Rulebook VER20.010126 | rulebook | 1 | **PRESENT** | MINOR | #87 Adgm1547 7504 Ver20010126 (`is_current=1`, `FEES`) | code |  |
| `IFR` | Islamic Finance Rulebook VER08.020125 | rulebook | 1 | **PRESENT** | MINOR | #117 Adgm1547 5911 Ver08020125 (`is_current=1`, `IFR`) | code |  |
| `MIR` | Market Infrastructure Rulebook VER08.100724 | rulebook | 1 | **PRESENT** | MINOR | #2793 Mir Ver12.270426 (`is_current=1`, `MIR`) | code | Re-scraped and ingested in Phase 6. |
| `PIN` | Professional Indemnity Rulebook VER11.250925 | rulebook | 1 | **PRESENT** | MINOR | #91 Adgm1547 9602 Ver11250925 (`is_current=1`, `PIN`) | code |  |

## Gaps — action list (critical / major first)

_No MISSING or REGISTERED items — every authoritative document has a current corpus match._

## Orphan corpus documents

_Documents in corpus.db for this jurisdiction that did not match any authoritative inventory item. Either the inventory is incomplete, or these are superseded / mis-attributed._

| Corpus ID | Title | source_entity | rulebook_code | is_current | doc_type |
|---|---|---|---|---|---|
| 78 | Wm54 2020 Class Modification Notice Operating A Multilateral Trading Facility In Relation To Virtual Assets | `FSRA` | `WAIVERS` | 1 | rulebook |
| 102 | Wm52 2020 Class Modification Notice Digital Investment Managers Withdrawn 6Nov2020 | `FSRA` | `WAIVERS` | 1 | rulebook |
| 2771 | Amendments To Pin | `FSRA` | `PIN-AMEND` | 1 | rulebook |
| 65 | Notice Of Publication Rules Made By The Registrar File 1 | `ADGM` | `NOTICES` | 1 | rulebook |
| 154 | Adgm1547 25730 Ver12023 | `ADGM` | `NOTICES` | 1 | rulebook |
| 210 | Notice Of Publication Rules Made By The Board File 2 | `ADGM` | `NOTICES` | 1 | rulebook |
| 2325 | Guidance & Policies Manual (GPM) | `FSRA` | `GPM` | 1 | guidance |
| 2555 | FSRA Application Forms and Guidance | `FSRA` | `FORMS` | 1 | guidance |
| 2667 | Private Ltd Rsc Non Financial | `ADGM_RA` | `COMP-LAW-PRIV_LTD_RSC_NF` | 1 | company_law |
| 2673 | Private Ltd Retail | `ADGM_RA` | `COMP-LAW-PRIV_LTD_RETAIL` | 1 | company_law |
| 2666 | Private Ltd Non Financial | `ADGM_RA` | `COMP-LAW-PRIV_LTD_NF` | 1 | company_law |
| 2730 | Model Articles Rules 2015 | `ADGM_RA` | `COMP-LAW-MODEL_ARTICLES` | 1 | company_law |
| 2674 | Lp Financial And Non Financial | `ADGM_RA` | `COMP-LAW-LP_FN` | 1 | company_law |
| 2671 | Llp Financial And Non Financial | `ADGM_RA` | `COMP-LAW-LLP_FN` | 1 | company_law |
| 2672 | Guidance Continuance Into Adgm | `ADGM_RA` | `COMP-LAW-GUIDANCE_CONT_ADGM` | 1 | company_law |
| 2668 | Foundation Registration | `ADGM_RA` | `COMP-LAW-FOUNDATION_REG` | 1 | company_law |
| 2669 | Foundation Continuance | `ADGM_RA` | `COMP-LAW-FOUNDATION_CONT` | 1 | company_law |
| 2670 | Branch Financial And Non Financial Services | `ADGM_RA` | `COMP-LAW-BRANCH_FN` | 1 | company_law |
| 2766 | Amendments To Cib | `FSRA` | `CIB-AMEND` | 1 | rulebook |
| 116 | Bank Recovery And Resolution Regulation 2018 20 | `FSRA` | `BRR` | 1 | rulebook |
| 2798 | ADGM Whistleblower Protection Regulations 2024 | `ADGM_RA` | `ADGM-WB-2024` | 1 | legislation |
| 72 | Commercial Licensing Regulations 2015 (Controlled Activities) Rules 2021 | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 82 | Commercial Licensing Regulations 2015 (Conditions Of Licence) Rules 2021 | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 88 | (10) Editorial   Exemption Order | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 142 | (06) Limited Liability Partnerships Rules 2021(Editorial) | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 153 | (2) Editorial   Insolvency Regulations 2022 | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 160 | (3) Companies Regulations (Auditors) Rules 2022   Editorial Version 0 | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 166 | (6) Editorial   Conditions Of Licence Rules | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 179 | Business And Company Names Rules 2021 | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 187 | (04) Commercial Licensing Regulations (Controlled Activities) Rules 2021 (Editorial) | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 195 | (6) Companies Regulations (Names Adjudication) Rules 2022   Editorial Version | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 214 | (8) Editorial   Controlled Activities Rules | `ADGM_RA` | `ADGM-RA-RULES` | 1 | rulebook |
| 2592 | Branch – Financial and Non-Financial Services Registration Guide | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2593 | Guidance on Continuance into ADGM | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2594 | Limited Liability Partnership – Financial and Non-Financial Registration Guide | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2595 | Limited Partnership – Financial and Non-Financial Services Registration Guide | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2596 | Private Company Limited by Shares – Non-Financial Services Registration Guide | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2597 | Private Company Limited by Shares (RSC) – Non-Financial Services Registration Guide | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2598 | Private Company Limited by Shares – Retail Registration Guide | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2599 | Foundation Registration Guide | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2600 | Foundation Continuance to ADGM Guide | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2601 | Nominee Arrangement Confirmation Form | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2602 | Nominee Arrangement Confirmation – Role Holder Nominee Company | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2603 | Nominee Arrangement Confirmation – Role Holder Nominee Foundation | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2604 | Nominee Arrangement Confirmation – Role Holder Nominee Partnership | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2605 | Tax Services Controlled Activity Form | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2607 | ADGM Model Articles – Private Company Limited by Shares | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2608 | ADGM Model Articles – Private Company Limited by Guarantee | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2609 | ADGM Model Articles – Public Company | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2610 | Resolution Template – Single Individual Shareholder for PLC Incorporation | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2611 | Resolution Template – Multiple Individual Shareholders for PLC Incorporation | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2612 | Resolution Template – Corporate Shareholder for PLC Incorporation | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2613 | Resolution Template – Registration of Branch | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2614 | Resolution Template – Registration of Branch by Management Board | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2615 | Resolution Template – Incorporation by Body Corporate | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2616 | Resolution Template – Incorporation by Individual | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2617 | Confirmation – Updated Documents | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2618 | Confirmation – Valid Current Documents | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2657 | ADGM-RA Director Consent to Act | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2658 | ADGM-RA Authorised Signatory Consent | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2659 | ADGM-RA Registered Office Consent Letter | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2660 | ADGM-RA CSP Appointment — DLT Foundations | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2661 | ADGM-RA CSP Appointment — Foundations 2017 | `ADGM_RA` | `ADGM-RA-F` | 1 | company_law |
| 2750 | Insolvency Regulations 2022 | `ADGM_RA` | `ADGM-IR` | 1 | legislation |
| 2619 | Restriction Agreement (MKT Form 9-1) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2620 | Reporting Entities – Quarterly Cash Report (MKT Form 10-1) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2621 | Mining Reporting Entities (MKT Form 11-1) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2622 | Petroleum Reporting Entities (MKT Form 12-1) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2623 | Application for Admission of Securities to the Official List (MKT Form 2-4) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2624 | Application for Approval of a Prospectus (MKT Form 4.6-1) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2625 | Application for Approval of an Offer Document (MKT Form 4-7) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2626 | Payment Form (MKT Form 4.6-2) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2627 | Waiver Modification Request (MKT Form 1-1) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2629 | Venture Capital Fund Manager (VCFM) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2630 | Virtual Assets Application (VAS) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2631 | Notification of Virtual Asset for Accepted Virtual Asset Status | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2632 | Principal Representative Status-1 (PRS-1) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2633 | Approved Person Status (APS) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2634 | Withdrawal of Approved Person Status (APS-2) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2635 | Change in Approved Person Status (APS-3) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2636 | Key Individuals Application-1 (RBK-1) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2637 | Public Fund Registration (FPR) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2638 | Exempt Fund or Qualified Investor Fund Notification (FEQN) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2639 | Foreign Fund Manager (FFM) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2640 | Foreign Fund Notification (FFN) | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2643 | Asset Management Supplement (AMS) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2644 | Banking Business Supplement (BBS) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2645 | Captive Insurer Business (CIBF) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2646 | Change in Control (CIC) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2647 | Credit Rating Agency (CRA) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2648 | Dealing and Advisory Supplement (DAS) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2649 | Islamic Financial Business Supplement (IFBS) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2650 | Insurance Business Supplement (IBS) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2651 | Private Financing Platform Supplement (PFP) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2652 | Representative Office (RO) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2653 | Cancel a Financial Services Permission (FSPC) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2654 | Remote Member Recognition Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2655 | Waivers or Modifications (WM) Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | guidance |
| 2675 | Mkt 10 1 Quarterly Cash Report | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2676 | Ffn Foreign Fund Notification | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2677 | Das Dealing Advisory Supplement | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2678 | Ffm Foreign Fund Manager | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2679 | Cibf Captive Insurance Business | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2680 | Ibs Insurance Business Supplement | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2681 | Cra Credit Rating Agency | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2682 | Cic Change In Control | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2683 | Mkt 11 1 Mining Reporting Entities | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2684 | Mkt 9 1 Restriction Agreement | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2685 | Remote Member Recognition | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2686 | Mkt 12 1 Petroleum Reporting Entities | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2687 | Prs 1 Principal Representative Status | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2688 | Wm Waivers Modifications | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2689 | Mkt 2 4 Admission Securities Official List | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2690 | Mkt 1 1 Waiver Modification Request | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2691 | Vcfm Venture Capital Fund Manager | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2692 | Mkt 4.6 1 Approval Prospectus | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2693 | Pfp Private Financing Platform | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2694 | Fspc Cancel Financial Services Permission | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2695 | Ro Representative Office | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2696 | Fpr Public Fund Registration | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2697 | Va Notification Accepted Status | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2699 | Mkt 4.6 2 Payment Form | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2701 | Mkt 4 7 Approval Offer Document | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2703 | Bbs Banking Business Supplement | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2704 | Rbk 1 Key Individuals Application | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2705 | Ams Asset Management Supplement | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2706 | Vas Virtual Assets Application | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2707 | Ifbs Islamic Financial Business | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 2708 | Feqn Exempt Qualified Fund Notification | `ADGM FSRA` | `ADGM-FSRA-F` | 1 | other |
| 216 | Adgm1547 24944 Ver012022 | `ADGM` | `ADGM-FATCA` | 1 | rulebook |
| 2799 | ADGM EAO Guidance on ER 2024 (Feb 2025) | `ADGM_RA` | `ADGM-ER-2024-EAO` | 1 | guidance |
| 2797 | ADGM Employment Regulations 2024 | `ADGM_RA` | `ADGM-ER-2024` | 1 | legislation |
| 208 | Adgm1547 22829 Ver1032020 | `ADGM_RA` | `ADGM-DPR` | 1 | rulebook |
| 2749 | Data Protection Regulations 2021 | `ADGM_RA` | `ADGM-DPR` | 1 | legislation |
| 159 | Adgm1547 19312 Ver142023 | `ADGM` | `ADGM-CRS` | 1 | rulebook |
| 2588 | ADGM Companies Regulations (Model Articles) Rules 2015 | `ADGM` | `ADGM-CR-MAR` | 1 | company_law |
| 2587 | ADGM Companies Regulations 2020 | `ADGM` | `ADGM-CR` | 1 | company_law |
| 2747 | Commercial Licensing Regulations 2015 | `ADGM_RA` | `ADGM-CLR` | 1 | legislation |
| 1778 | 11 Appendix 9 Mkt Misc Amendments | `FSRA` | — | 1 | consultation |
| 1780 | 01 Cp 4 Of 2019 Misc Amendments 2019 | `FSRA` | — | 1 | consultation |
| 1781 | Adgm1547 22726 Ver2007 | `FSRA` | — | 1 | consultation |
| 1782 | Appendix 1   Commercial Licensing Regulations (Controlled Activities) Rules 2024 (Editorial) | `FSRA` | — | 1 | consultation |
| 1783 | Annex A %E2%80%94 Distributed Ledger Technology Foundations Regulations 2023 | `FSRA` | — | 1 | consultation |
| 1785 | Consultation Paper No 3 Of 2015 Operating Regulations | `FSRA` | — | 1 | consultation |
| 1786 | Appendix 1   Companies Regulations 2020 (Auditors) Rules 2020 | `FSRA` | — | 1 | consultation |
| 1787 | Consultation Paper No 3 Of 2021 Proposals On Digital Verification Of Identity(Ekyc) | `FSRA` | — | 1 | consultation |
| 1788 | Annex A   Administrative Regulations | `FSRA` | — | 1 | consultation |
| 1791 | Annex A Brr Regulations | `FSRA` | — | 1 | consultation |
| 1792 | Cp No2 Of 2017 Data Protection Regulations Amendments | `FSRA` | — | 1 | consultation |
| 1793 | (05) Appendix 3 Privatecreditfunds Iframendments | `FSRA` | — | 1 | consultation |
| 1794 | Annex B   Proposed Companies Regulations 2022 | `FSRA` | — | 1 | consultation |
| 1795 | Annex A Insolvency Regulations Consultation Paper No 4 Of 2015 | `FSRA` | — | 1 | consultation |
| 1797 | (03) Appendix 1(Cobsamendments) | `FSRA` | — | 1 | consultation |
| 1798 | Annex A   Companies Regulations (Amendment No 2) 2020   Showing Effect Of Proposed Amendments | `FSRA` | — | 1 | consultation |
| 1800 | Annex A   Adgm Companies Amendment No. 5 Regulations 2019 | `FSRA` | — | 1 | consultation |
| 1801 | Annex A (Proposed Amendments To Fsmr) | `FSRA` | — | 1 | consultation |
| 1802 | (04) Appendix 2 Privatecreditfunds Gloamendments | `FSRA` | — | 1 | consultation |
| 1805 | Annex B To Consultation Paper   Fintech Reglab Guidance | `FSRA` | — | 1 | consultation |
| 1806 | Annex B    Foundations Regulations (Amendment No 2) 2020 | `FSRA` | — | 1 | consultation |
| 1807 | Annex B Draft Fsmr Amendments Passporting | `FSRA` | — | 1 | consultation |
| 1808 | Appendix 1  Commercial Licensing Regulations 2015 (Controlled Activities) Rules | `FSRA` | — | 1 | consultation |
| 1809 | Annex E Commerical Licensing Amendment Regulations 2018 | `FSRA` | — | 1 | consultation |
| 1810 | Annexure A   Adgm Courts   Draft Litigation Funding Rules | `FSRA` | — | 1 | consultation |
| 1811 | (03) Appendix 2 Otclps Pru Amendments | `FSRA` | — | 1 | consultation |
| 1812 | Consultation Paper No 8 Of 2015 Limited Liability Partnerships Regulations | `FSRA` | — | 1 | consultation |
| 1813 | Consultation Paper No8 Of 2018 Accountsfinespolicy | `FSRA` | — | 1 | consultation |
| 1815 | Annex A Adgm Courts Civil Evidence Judgments Enforcement And Judicial Appointments Regulations Consultation Paper No 11 | `FSRA` | — | 1 | consultation |
| 1816 | Consultation Paper No 1 Of 2015 Application Of English Law Regulations | `FSRA` | — | 1 | consultation |
| 1817 | Appendix 5   Draft Amendments To The Anti Money Laundering And Sanctions Rules And Guidance (Aml) | `FSRA` | — | 1 | consultation |
| 1818 | 09 Appendix 7 Ifr Misc Amendments | `FSRA` | — | 1 | consultation |
| 1819 | Appendix 1   Amendments To Cobs 2 | `FSRA` | — | 1 | consultation |
| 1820 | 07 Appendix 5 Aml Misc Amendments | `FSRA` | — | 1 | consultation |
| 1822 | Adgm1547 3268 Ver021113.10 | `FSRA` | — | 1 | consultation |
| 1823 | Appendix 1   Amendments To Cobs 3 | `FSRA` | — | 1 | consultation |
| 1824 | (08) Attachment 1   Environmental%2C Social And Governanve Disclosures Guidance(1) | `FSRA` | — | 1 | consultation |
| 1826 | Annex B Companies Amendment Regulations 2018 | `FSRA` | — | 1 | consultation |
| 1829 | Appendix 1   Data Protection Regulations (Substantial Publicinterest) Rules 2025 | `FSRA` | — | 1 | consultation |
| 1831 | Annex B Mapping Table | `FSRA` | — | 1 | consultation |
| 1832 | Appendix 5 Glo | `FSRA` | — | 1 | consultation |
| 1833 | Appendix 1   Proposed Amendments To Aml | `FSRA` | — | 1 | consultation |
| 1835 | Appendix 10   Proposed Amendments To Pin | `FSRA` | — | 1 | consultation |
| 1836 | Annex A App 5 Aml Misc Amendments | `FSRA` | — | 1 | consultation |
| 1837 | Annex B   Proposed Interpretation (Amendment No. 1) Regulations 2020 | `FSRA` | — | 1 | consultation |
| 1838 | (01) Consultation Paper No 2 Of 2023   Proposed Enhancements To Client Classification%2C Client Assets And Conduct Requirements | `FSRA` | — | 1 | consultation |
| 1839 | Consultation Paper No 2 Of 2015 Companies Regulations | `FSRA` | — | 1 | consultation |
| 1841 | Annex A Late Filing Penalty Guide Annual Accounts | `FSRA` | — | 1 | consultation |
| 1842 | Appendix 1   Amendments To Cobs 1 | `FSRA` | — | 1 | consultation |
| 1843 | Appendix 2   Commercial Licensing Regulations (Conditions Of Licence And Branch Registration) Rules 2024 (Editorial) | `FSRA` | — | 1 | consultation |
| 1844 | Annex A Arbitration Regulations Consultation Paper No 12 | `FSRA` | — | 1 | consultation |
| 1845 | Appendix 1   Amendments To Cobs 0 | `FSRA` | — | 1 | consultation |
| 1846 | Appendix 2 (Proposed Amendments To Aml) | `FSRA` | — | 1 | consultation |
| 1847 | Consultation Paper No 3 Of 2018 Registration Authority Decision Procedures And Enforcement Manual | `FSRA` | — | 1 | consultation |
| 1849 | Appendix 1   Insolvency Regulations (Insolvency Practitioners) Rules 2022 | `FSRA` | — | 1 | consultation |
| 1850 | Appendix A To Annex B   Reglab Application Form | `FSRA` | — | 1 | consultation |
| 1851 | Annex A Application Of English Law Regulations Consultation Paper No 1 Of 2015 | `FSRA` | — | 1 | consultation |
| 1853 | Annex C   Beneficial Ownership And Control Regulations Amendment No. 2 Regulations 2019 | `FSRA` | — | 1 | consultation |
| 1854 | Annex B App 2 Companies Regulations Register Of Auditors Rules 2017 | `FSRA` | — | 1 | consultation |
| 1855 | Appendix 1   Proposed Amendments To Cib | `FSRA` | — | 1 | consultation |
| 1856 | Annex B   Foundations Regulations (Amendment No 2) 2020   Showing Effect Of Proposed Amendments | `FSRA` | — | 1 | consultation |
| 1857 | Appendix 2   Commercial Licensing Regulations 2015 (Controlled Activities) Rules 2018 | `FSRA` | — | 1 | consultation |
| 1858 | Appendix%201 Aml Ekyc Digitalverification | `FSRA` | — | 1 | consultation |
| 1859 | (04) Appendix 1 Susfin Cobsamendments | `FSRA` | — | 1 | consultation |
| 1860 | Annex A   Proposed Beneficial Ownership And Control Regulations (Amendment No. 2) 2024 | `FSRA` | — | 1 | consultation |
| 1861 | Annex A   Amendments To Fsmr 0 | `FSRA` | — | 1 | consultation |
| 1863 | Annex A   Amendments To Fsmr 1 | `FSRA` | — | 1 | consultation |
| 1866 | (04) Appendix 2(Amendments To Glo) | `FSRA` | — | 1 | consultation |
| 1867 | Appendix 1   Commercial Licensing Regulations (Conditions Oflicence And Branch Registratiion) Rules (Editorial Blackline) | `FSRA` | — | 1 | consultation |
| 1869 | Annex A Beneficial Ownership And Control Regulations 2018 | `FSRA` | — | 1 | consultation |
| 1872 | Appendix 4 Takeover Regulations  Takeover Code  Rules 2015 | `FSRA` | — | 1 | consultation |
| 1873 | Annex A   Insolvency Regulations 2022   Editorial Version | `FSRA` | — | 1 | consultation |
| 1874 | Annex A Judicial Conduct Judicial Office Holders Rules 20102015 | `FSRA` | — | 1 | consultation |
| 1875 | Annex E Retention Of Knives Guns And Other Articles Rules Consultation Paper No 11 | `FSRA` | — | 1 | consultation |
| 1877 | Annex B Guidance Regulatory Framework For Private Financing Platforms | `FSRA` | — | 1 | consultation |
| 1878 | Appendix 4 Draft Amendments To The Rules Of Market Conduct | `FSRA` | — | 1 | consultation |
| 1879 | Consultation Paper No 13 Adgm Courts Rules  Supplementary Rules | `FSRA` | — | 1 | consultation |
| 1880 | Annex A App 2 Cobs Misc Amendments | `FSRA` | — | 1 | consultation |
| 1881 | Appendix 1   Proposed Amendments To Pru | `FSRA` | — | 1 | consultation |
| 1882 | Appendix 2 Proposed Amendments To Glo | `FSRA` | — | 1 | consultation |
| 1885 | Consultation Paper No9 Of 2018 Licence Fines Policy | `FSRA` | — | 1 | consultation |
| 1886 | Consultation Paper No 12 Arbitration Regulations | `FSRA` | — | 1 | consultation |
| 1887 | Appendix 7 Anti Money Laundering And Sanctions Rules And Guidance Aml | `FSRA` | — | 1 | consultation |
| 1889 | Consultation Paper No 6 Of 2018 Litigation Funding Rules | `FSRA` | — | 1 | consultation |
| 1890 | Consultation Paper No 5 Of 2019 Pru Updates | `FSRA` | — | 1 | consultation |
| 1891 | Annex A Adgm Foundations Regulations 2017 | `FSRA` | — | 1 | consultation |
| 1893 | Annex A   Amendments To Fsmr | `FSRA` | — | 1 | consultation |
| 1895 | (02) Annex A(Proposed Amendments To Fsmr) | `FSRA` | — | 1 | consultation |
| 1896 | Annex B   Proposed Foundations Regulations (Amendment No. 1) 2023 | `FSRA` | — | 1 | consultation |
| 1897 | Appendix 1   Consumer Protection Regulations 2025 (13 May2025) | `FSRA` | — | 1 | consultation |
| 1898 | Consultation Paper No 4 Of 2017 | `FSRA` | — | 1 | consultation |
| 1899 | Appendix 11   Proposed Limited Liability Partnerships Rules 2022 | `FSRA` | — | 1 | consultation |
| 1900 | Consultation Paper No 1 Of 2019 Proposed Aml Amendments | `FSRA` | — | 1 | consultation |
| 1902 | Annex C Adgm Rule On Engaging Non Employees Pc Version | `FSRA` | — | 1 | consultation |
| 1903 | 03 Appendix 1 Gen Misc Amendments | `FSRA` | — | 1 | consultation |
| 1906 | Annex C   Commercial Licensing Regulations (Amendment No 1) 2020   Showing Effect Of Proposed Amendments | `FSRA` | — | 1 | consultation |
| 1907 | Annex A   Proposed Application Of English Law Regulations (Amendment No.1) 2020 | `FSRA` | — | 1 | consultation |
| 1908 | Annex B   Foundations Amendment No. 2 Regulations 2019 | `FSRA` | — | 1 | consultation |
| 1909 | Appendix 1   Draft Amendments To The Registration Authority%E2%80%99S Decision Procedures And Enforcement Manual | `FSRA` | — | 1 | consultation |
| 1910 | Annex B Judicial Discipline Prescribed Procedures Rules 20102015 | `FSRA` | — | 1 | consultation |
| 1911 | Adgm1547 3270 Ver021913.10 | `FSRA` | — | 1 | consultation |
| 1912 | Appendix 2 Draft Amendments To Mkt | `FSRA` | — | 1 | consultation |
| 1913 | Annex A   Data Protection Regulations (Amendment No. 1) 2025 | `FSRA` | — | 1 | consultation |
| 1914 | 10 Appendix 8 Mir Misc Amendments | `FSRA` | — | 1 | consultation |
| 1915 | Annex A Data Protection Amendment Regulations 2017 | `FSRA` | — | 1 | consultation |
| 1916 | Annex C Offers To Settle In Civil And Commercial Proceedings Rules 20102015 | `FSRA` | — | 1 | consultation |
| 1917 | Annex C Abbreviations | `FSRA` | — | 1 | consultation |
| 1918 | Annex A Beneficial Ownership And Control Regulations 2022 | `FSRA` | — | 1 | consultation |
| 1919 | Annex C Interpretation Amendment Regulations 2017 | `FSRA` | — | 1 | consultation |
| 1920 | Appendix 1   Amendments To Cobs | `FSRA` | — | 1 | consultation |
| 1921 | Annex A App 6 Glo Misc Amendments | `FSRA` | — | 1 | consultation |
| 1923 | (02) Annex A Fsmr Privatecreditfunds | `FSRA` | — | 1 | consultation |
| 1924 | Adgm1547 22453 Ver04232020 | `FSRA` | — | 1 | consultation |
| 1926 | Appendix 1 Draft Amendments To Mir | `FSRA` | — | 1 | consultation |
| 1927 | 05 Appendix 3 Pru Misc Amendments | `FSRA` | — | 1 | consultation |
| 1928 | Consultation Paper No 10 Of 2015 Data Protection Regulations | `FSRA` | — | 1 | consultation |
| 1929 | Annex A   Beneficial Ownership And Control Regulations (Amendment No.1) 2022 | `FSRA` | — | 1 | consultation |
| 1930 | (05) Appendix 4 Otclps Glo Amendments | `FSRA` | — | 1 | consultation |
| 1932 | Appendix 3 Draft Amendments To Glo | `FSRA` | — | 1 | consultation |
| 1933 | Consultation Paper No 5 Of 2015 Employment Regulations | `ADGM_RA` | — | 1 | consultation |
| 1934 | Annex A Limited Liability Partnerships Regulations 2015 | `FSRA` | — | 1 | consultation |
| 1936 | Annex C   Proposed Commercial Licensing Regulations (Amendment No.1) 2022 | `FSRA` | — | 1 | consultation |
| 1937 | Adgm1547 3267 Ver031404.10 | `FSRA` | — | 1 | consultation |
| 1938 | Appendix 1   Commercial Permits Regulations (Alcohol) Rules 2024 | `FSRA` | — | 1 | consultation |
| 1939 | (07) Appendix 4 Susfin Gloamendments | `FSRA` | — | 1 | consultation |
| 1941 | Consultation Paper No 2 Of 2019 Proposed Adgm Employment Regulations | `ADGM_RA` | — | 1 | consultation |
| 1942 | (06) Appendix 3 Susfin Mktamendments | `FSRA` | — | 1 | consultation |
| 1943 | 14 Appendix 12 Gpm Misc Amendments | `FSRA` | — | 1 | consultation |
| 1944 | Annex G   Proposed Limited Liability Partnerships Regulations (Amendment No.1) 2022 | `FSRA` | — | 1 | consultation |
| 1945 | 04 Appendix 2 Cobs Misc Amendments | `FSRA` | — | 1 | consultation |
| 1946 | Annex A   Real Property Regulations (Editorial Blackline) | `FSRA` | — | 1 | consultation |
| 1948 | Annex A   Companies Regulations (Amendment No. 2) 2020 | `FSRA` | — | 1 | consultation |
| 1949 | (03) Appendix 1 Privatecreditfunds Fundsamendments | `FSRA` | — | 1 | consultation |
| 1950 | Appendix 1   Limited Liability Partnership Amendment No. 1 Rules 2019 | `FSRA` | — | 1 | consultation |
| 1951 | Appendix 2   Amendments To Pru | `FSRA` | — | 1 | consultation |
| 1953 | Appendix 3 Takeover Regulations | `FSRA` | — | 1 | consultation |
| 1954 | Consultation Paper No 7 Of 2018 Fund Passporting Regulations | `FSRA` | — | 1 | consultation |
| 1956 | Annex A   Proposed Companies Regulations (Amendment No. 1) 2023 | `FSRA` | — | 1 | consultation |
| 1957 | Appendix 1   Ra Decisions Procedures And Enforcement Manual Chapter 3 | `FSRA` | — | 1 | consultation |
| 1960 | Consultation Paper No 5 Of 2018 Bank Recovery Resolution Regulations | `FSRA` | — | 1 | consultation |
| 1961 | (02) Annex A Cos Regs Susfin | `FSRA` | — | 1 | consultation |
| 1962 | Annex A   Proposed Commercial Licensing Regulations (Amendment No. 1) 2024 | `FSRA` | — | 1 | consultation |
| 1963 | Annex A Proposed Amendments To Fsmr | `FSRA` | — | 1 | consultation |
| 1964 | Annex A   Proposed Amendments To Financial Services And Marketsregulations | `FSRA` | — | 1 | consultation |
| 1965 | (01) Consultation Paper No. 5 Of 2022 Otclps | `FSRA` | — | 1 | consultation |
| 1967 | 13 Appendix 11 Cib Misc Amendments | `FSRA` | — | 1 | consultation |
| 1968 | Consultation Paper No 6 Of 2015 Real Property And Strata Title Regulations | `FSRA` | — | 1 | consultation |
| 1969 | Appendix 11   Proposed Amendments To Pru | `FSRA` | — | 1 | consultation |
| 1973 | Annex A Real Property Regulations Consultation Paper No 6 Of 2015 | `FSRA` | — | 1 | consultation |
| 1974 | Annex A Operating Regulations Consultation Paper No 3 | `FSRA` | — | 1 | consultation |
| 1975 | Consultation Paper No 2 Of 2018 Introduction Of Crypto Asset Regulatory Framework In Adgm | `FSRA` | — | 1 | consultation |
| 1979 | Consultation Paper No 6 Of 2019   Proposed Amendments To Adgm Commercial Legislation | `FSRA` | — | 1 | consultation |
| 1980 | Consultation Paper No1 Of 2020 (Proposal For Revision Of Regulatory Framework For Providing Money Services In Adgm) | `FSRA` | — | 1 | consultation |
| 1981 | Annex A Draft Amendments To The Fsmr Consultation Paper No 3 Of 2016 | `FSRA` | — | 1 | consultation |
| 1982 | (6) Attachment 1   Proposed Amendments To The Guidance And Policy Manual | `FSRA` | — | 1 | consultation |
| 1983 | Appendix 6 Rules Of Market Conduct Rmc | `FSRA` | — | 1 | consultation |
| 1984 | Annex D Foundations Amendment Regulations 2018 | `FSRA` | — | 1 | consultation |
| 1985 | Appendix 2 %E2%80%94 Dlt Foundations Regulations (International Accounting Standards) Rules 2023 | `FSRA` | — | 1 | consultation |
| 1986 | Annex A Companies Regulations Consultation Paper No 2 Of 2015 | `FSRA` | — | 1 | consultation |
| 1987 | Annex A App 4 Fund Rules Misc Amendments | `FSRA` | — | 1 | consultation |
| 1988 | 02 Annex A Fsmr Misc Amendments | `FSRA` | — | 1 | consultation |
| 1989 | Appendix 2   Commercial Licensing Regulations 2015 (Conditions Of Licence) Rules | `FSRA` | — | 1 | consultation |
| 1990 | Annex A   Commercial Permits Regulations 2024 | `FSRA` | — | 1 | consultation |
| 1991 | Annex A   Proposed Electronic Transaction Regulations 2020 | `FSRA` | — | 1 | consultation |
| 1993 | Appendix 1 Pin | `FSRA` | — | 1 | consultation |
| 1994 | (02) Draft Principles | `FSRA` | — | 1 | consultation |
| 1995 | Annex A   Companies Regulations (Amendment No. 2) 2024 | `FSRA` | — | 1 | consultation |
| 1997 | Appendix 1   Proposed Commercial Licensing Regulations (Conditions Of Licence %26 Br. Reg) Rules 2023 | `FSRA` | — | 1 | consultation |
| 1998 | (06) Appendix 4 Privatecreditfunds Mktamendments | `FSRA` | — | 1 | consultation |
| 2000 | (09) Attachment 2   Sustainable Finance Supplementary Guidance | `FSRA` | — | 1 | consultation |
| 2001 | Annex B   Proposed Limited Liability Partnership Regulations (Amendment No. 1) 2024 | `FSRA` | — | 1 | consultation |
| 2002 | Appendix 1   Proposed Amendments To Cobs | `FSRA` | — | 1 | consultation |
| 2003 | Annex B App 1 Companies Regulations Model Articles Rules 2017 | `FSRA` | — | 1 | consultation |
| 2004 | Annex C   Off Plan And Real Property Professionals Regulations 2024 | `FSRA` | — | 1 | consultation |
| 2006 | Appendix 1 Feeslateregulatoryreturns Feesamendments | `FSRA` | — | 1 | consultation |
| 2007 | Appendix 2   Commercial Licensing Regulations (Controlledactivities) Rules 2025 (Editorial Blackline) | `FSRA` | — | 1 | consultation |
| 2008 | Annex A Data Protection Regulations | `FSRA` | — | 1 | consultation |
| 2010 | Annex A App 3 Cib Misc Amendments | `FSRA` | — | 1 | consultation |
| 2014 | (06) Attachment 1 Otclps Proposed Supplementary Guidance | `FSRA` | — | 1 | consultation |
| 2015 | (01) Consultation Paper No 1 Of 2023 | `FSRA` | — | 1 | consultation |
| 2016 | Annex C Draft Amendments To Insolvency Regulations | `FSRA` | — | 1 | consultation |
| 2018 | Annex B Strata Title Regulations Consultation Paper No 6 Of 2015 | `FSRA` | — | 1 | consultation |
| 2019 | Annex D   Proposed Data Protection Regulations (Amendment No. 1) 2022 | `FSRA` | — | 1 | consultation |
| 2020 | Annex B Companies Amendment Regulations 2017 | `FSRA` | — | 1 | consultation |
| 2021 | Consultation Paper For Beneficial Ownership And Control Regulations | `FSRA` | — | 1 | consultation |
| 2022 | Annex D   Commercial Licensing Regulations 2015 Showing Effect Of Amendments | `FSRA` | — | 1 | consultation |
| 2023 | Annex A App1 Gen Misc Amendments | `FSRA` | — | 1 | consultation |
| 2024 | Appendix 1   Off Plan Development Regulations (Project Account) Rules 2024 | `FSRA` | — | 1 | consultation |
| 2025 | Annex D   Limited Liability Partnerships Amendment No. 2 Regulations 2019 | `FSRA` | — | 1 | consultation |
| 2026 | Appendix 4 Aml Misc%20Amendments | `FSRA` | — | 1 | consultation |
| 2027 | Annex A Draft Amendments To Fsmr | `FSRA` | — | 1 | consultation |
| 2028 | Appendix 2 Gen Ekyc Digitalverification | `FSRA` | — | 1 | consultation |
| 2029 | Consultation Paper No 4 Of 2015 Insolvency Regulations | `FSRA` | — | 1 | consultation |
| 2030 | (1) Consultation Paper No. 2 Of 2024   Proposals For Whistleblowing Framework For The Abu Dhabi Global Market | `ADGM_RA` | — | 1 | consultation |
| 2031 | Adgm1547 3269 Ver021213.10 | `FSRA` | — | 1 | consultation |
| 2033 | Annex B Divisions And Jurisdiction Court Of First Instance Rules Consultation Paper No 11 | `FSRA` | — | 1 | consultation |
| 2034 | 08 Appendix 6 Glo Misc Amendments | `FSRA` | — | 1 | consultation |
| 2036 | (05) Appendix 3(Amendments To Gen) | `FSRA` | — | 1 | consultation |
| 2037 | Consultation Paper No 3 Foundations Regulations | `FSRA` | — | 1 | consultation |
| 2039 | Appendix 2   Amendments To Cobs | `FSRA` | — | 1 | consultation |
| 2042 | Annex D Taking Control Of Goods And Commercial Rent Arrears Recovery Rules Consultation Paper No 11 | `FSRA` | — | 1 | consultation |
| 2043 | (01) Sustainable Finance Consultation Paper No. 6 Of 2022(1) | `FSRA` | — | 1 | consultation |
| 2044 | Schedule A Additional Policy Amendments | `FSRA` | — | 1 | consultation |
| 2046 | Annex C   Commercial Licensing Regulations (Amendment No. 1) 2020 | `FSRA` | — | 1 | consultation |
| 2048 | Annex B Draft Amendments To Fsmr | `FSRA` | — | 1 | consultation |
| 2050 | (03) Annex B Fsmr Susfin | `FSRA` | — | 1 | consultation |
| 2051 | Consultation Paper No 5 Of 2017 | `FSRA` | — | 1 | consultation |
| 2052 | Appendix 3 Glo Ekyc Digitalverification | `FSRA` | — | 1 | consultation |
| 2053 | Annex B   Off Plan Development Regulations 2024 | `FSRA` | — | 1 | consultation |
| 2055 | Annex B   Companies Regulations 2020 Showing Effect Of Amendments | `FSRA` | — | 1 | consultation |
| 2056 | Appendix To Consultation Paper No 11 List Of Uk Statutes | `FSRA` | — | 1 | consultation |
| 2057 | Appendix 1   Amendments To Cib | `FSRA` | — | 1 | consultation |
| 2058 | Consultation Paper No 9 Of 2015 Fs Supplementary Rules Regs | `FSRA` | — | 1 | consultation |
| 2059 | Consultation Paper No 3 Of 2016 Regulatory Framework For Fintech | `FSRA` | — | 1 | consultation |
| 2060 | Annex A Ra Decisions Procedures And Enforcement Manual | `FSRA` | — | 1 | consultation |
| 2061 | Annex A Late Filing Penalty Guide Licence Renewal | `FSRA` | — | 1 | consultation |
| 2062 | Annex A Fsra Fund Passporting Rules | `FSRA` | — | 1 | consultation |
| 2063 | Annex F   Proposed Foundations Regulations (Amendment No.1) 2022 | `FSRA` | — | 1 | consultation |
| 2066 | Annex C Certification Of Enforcement Agents Rules Consultation Paper No 11 | `FSRA` | — | 1 | consultation |
| 2067 | Adgm Consult Paper No 2 Of 2016 Reg Framewk For Fin Tech Final | `FSRA` | — | 1 | consultation |
| 2068 | (02) Appendix1 Otclps Cobs Amendments | `FSRA` | — | 1 | consultation |
| 2069 | Appendix 1 Pru Updates | `FSRA` | — | 1 | consultation |
| 2072 | Consultation Paper No 1 Of 2015 Adgm Courts Regulations And Rules | `FSRA` | — | 1 | consultation |
| 2073 | (01) Cp 7 Of 2020 Proposed Regulatory Framework For Providing Third Party Financial Technology Services In Adgm | `FSRA` | — | 1 | consultation |
| 2075 | Annex C Limited Liability Partnerships Amendment Regulations 2018 | `FSRA` | — | 1 | consultation |
| 2076 | Consultation Paper No 1 Of 2017 Miscallaneous Amendments | `FSRA` | — | 1 | consultation |
| 2077 | Appendix 2 Captive Insurance Business Rules | `FSRA` | — | 1 | consultation |
| 2079 | 12 Appendix 10 Pin Misc Amendments | `FSRA` | — | 1 | consultation |
| 2080 | Appendix 2   Amendments To Glo | `FSRA` | — | 1 | consultation |
| 2081 | Adgm1547 22726 Ver2007 | `FSRA` | — | 1 | guidance |
| 2082 | Adgm1547 26706 Ver02072325 | `FSRA` | — | 1 | guidance |
| 2083 | Adgm1547 3268 Ver021113.10 | `FSRA` | — | 1 | guidance |
| 2084 | Adgm1547 22828 Ver20240909 | `FSRA` | — | 1 | guidance |
| 2085 | Adgm1547 22885 Ver12082020 | `FSRA` | — | 1 | guidance |
| 2086 | Adgm1547 3270 Ver021913.10 | `FSRA` | — | 1 | guidance |
| 2087 | Adgm1547 22453 Ver04232020 | `FSRA` | — | 1 | guidance |
| 2088 | Adgm1547 3267 Ver031404.10 | `FSRA` | — | 1 | guidance |
| 2089 | Adgm1547 28194 Ver20250610 | `FSRA` | — | 1 | guidance |
| 2090 | Adgm1547 26661 Ver02072325 | `FSRA` | — | 1 | guidance |
| 2091 | Adgm1547 22827 Ver20250421 | `FSRA` | — | 1 | guidance |
| 2092 | Adgm Court Procedure Rules Amendment No 1 Of 2025   17102025 | `FSRA` | — | 1 | guidance |
| 2093 | Adgm1547 23292 Ver04082021 | `FSRA` | — | 1 | guidance |
| 2094 | Adgm1547 3269 Ver021213.10 | `FSRA` | — | 1 | guidance |
| 2095 | Adgm1547 23293 Ver04082021 | `FSRA` | — | 1 | guidance |
| 2096 | Adgm1547 29641 Ver20251028 | `FSRA` | — | 1 | guidance |
| 2097 | Adgm1547 22829 Ver1032020 | `FSRA` | — | 1 | guidance |
| 2098 | Adgm1547 22830 Ver18022020 | `FSRA` | — | 1 | guidance |
| 2100 | Supplementary Guidance Regulatory Framework Whistleblowing July 2025 | `ADGM_RA` | — | 1 | guidance |
| 2101 | Abu Dhabi Law No 4 2013 | `FSRA` | — | 1 | guidance |
| 2102 | Covid 19 Implication Data Protection | `FSRA` | — | 1 | guidance |
| 2104 | Fsra | `FSRA` | — | 1 | guidance |
| 2105 | Beneficial Ownership And Control Guidance | `FSRA` | — | 1 | guidance |
| 2106 | Abu Dhabi Global Market | `FSRA` | — | 1 | guidance |
| 2107 | Alternative Financingfunding | `FSRA` | — | 1 | guidance |
| 2108 | Enforcement And Disqualification Manual October 2025 | `FSRA` | — | 1 | guidance |
| 2109 | Ra | `FSRA` | — | 1 | guidance |
| 2110 | Decision Procedures Disqualification And Enforcement Manual 1 | `FSRA` | — | 1 | guidance |
| 2111 | Cabinet Resolution No 28 2007 | `FSRA` | — | 1 | guidance |
| 2112 | Adgm Court Procedure Rules Amendment No 1 2025 | `FSRA` | — | 1 | guidance |
| 2113 | Spot Commodities | `FSRA` | — | 1 | guidance |
| 2114 | Guidance Exemptions Requirement Appoint Company Service Provider | `FSRA` | — | 1 | guidance |
| 2115 | Sustainable Finance | `FSRA` | — | 1 | guidance |
| 2116 | Sustainable Finance 0 | `FSRA` | — | 1 | guidance |
| 2117 | Guidance Applications Accounts Filing Extensions | `FSRA` | — | 1 | guidance |
| 2118 | Adgm Legal Framework | `FSRA` | — | 1 | guidance |
| 2119 | Guidance Client Money | `FSRA` | — | 1 | guidance |
| 2120 | Listing Authority | `FSRA` | — | 1 | guidance |
| 2121 | Data Protection Guidance Note | `FSRA` | — | 1 | guidance |
| 2122 | Guidance Policy Statements | `FSRA` | — | 1 | guidance |
| 2124 | Digital Assets | `FSRA` | — | 1 | guidance |
| 2125 | Voluntary Liquidation Guidance | `FSRA` | — | 1 | guidance |
| 2126 | Fintech | `FSRA` | — | 1 | guidance |
| 2140 | Appendix 4   Commercial Licensing Regulations 2015 (Client Money) Rules | `FSRA` | — | 1 | consultation |
| 2141 | Consultation Paper No. 9 Of 2024   Proposed Enhancements To Theregulatory Framework Of The Fsra | `FSRA` | — | 1 | consultation |
| 2142 | Appendix 8   Proposed Amendments To Mir | `FSRA` | — | 1 | consultation |
| 2143 | Consultation Paper 4 Of 2021 Proposed Merger Of Fsra Regulatory Committee And Appeals Panel 0 | `FSRA` | — | 1 | consultation |
| 2146 | Attachment 1   Blackline Of Beneficial Ownership And Control Regulations 2022 | `FSRA` | — | 1 | consultation |
| 2147 | Attachment 9 Draft Form 12 1 Petroleum Reporting Entities | `FSRA` | — | 1 | consultation |
| 2148 | Appendix 5   Amendments To Mir | `FSRA` | — | 1 | consultation |
| 2150 | Appendix 6   Proposed Amendments To Pin | `FSRA` | — | 1 | consultation |
| 2151 | Appendix 4 (Proposed Amendments To Glo) | `FSRA` | — | 1 | consultation |
| 2154 | Attachment C   Proposed Amendments To Marine Insurance Act 1906 | `FSRA` | — | 1 | consultation |
| 2156 | Appendix 5   Proposed Commercial Licensing Regulations (Fines) Rules 2022 | `FSRA` | — | 1 | consultation |
| 2158 | Appendix 4   Amendments To Glo | `FSRA` | — | 1 | consultation |
| 2159 | Appendix 7   Amendments To Pru | `FSRA` | — | 1 | consultation |
| 2161 | Consultation Paper No. 4 Of 2022 (Insolvency Practitioner Rules) | `FSRA` | — | 1 | consultation |
| 2162 | Consultation Paper No. 9 Of 2020 Proposed Amendments To The Adgm Auditors Framework | `FSRA` | — | 1 | consultation |
| 2164 | Consultation Paper No. 5 Of 2020   Csp Regime | `FSRA` | — | 1 | consultation |
| 2165 | Attachment D   Proposed Amendments To Limited Partnerships Act 1907 | `FSRA` | — | 1 | consultation |
| 2166 | Appendix 4   Amendments To Glo 1 | `FSRA` | — | 1 | consultation |
| 2167 | Appendix 3   Clr (Conditions Of Licence And Branch Registration)   Editiorial Version | `FSRA` | — | 1 | consultation |
| 2168 | Attachment E   Proposed Insurance Act 2015 | `FSRA` | — | 1 | consultation |
| 2169 | Appendix 2   Proposed Amendments To Cib | `FSRA` | — | 1 | consultation |
| 2170 | Appendix 4 Proposed Amendmetnts To Anti Money Laundering (Aml) | `FSRA` | — | 1 | consultation |
| 2172 | Appendix 4   Proposed Amendments To Gpm | `FSRA` | — | 1 | consultation |
| 2174 | Consultation Paper No. 13 Of 2025   Iais Insurance Core Principles And Climate Risk Management | `FSRA` | — | 1 | consultation |
| 2175 | Appendix 4   Amendments To Glo 0 | `FSRA` | — | 1 | consultation |
| 2176 | Consultation Paper No. 7 Of 2024 Frts | `FSRA` | — | 1 | consultation |
| 2177 | Cp11 2025 Appendix 1   Commercial Permits Regulations (Temp | `FSRA` | — | 1 | consultation |
| 2178 | Appendix 2   Proposed Amendments To Pru | `FSRA` | — | 1 | consultation |
| 2179 | Appendix 3   Amendments To Pru | `FSRA` | — | 1 | consultation |
| 2181 | Cp No. 4 Of 2020   Proposed Amendments To The Application Of English Law Regulations 2015 | `FSRA` | — | 1 | consultation |
| 2182 | Attachment F   Proposed Application Of English Law Regulations Showing Effect Of Proposed Amendments | `FSRA` | — | 1 | consultation |
| 2183 | Consultation Paper No. 6 Of 2020  New Data Protection Regulations | `FSRA` | — | 1 | consultation |
| 2184 | Consultation Paper No. 6 Of 2024   Employment Regulations | `ADGM_RA` | — | 1 | consultation |
| 2185 | Cp11 2025 Appendix 2   Commercial Permits Regulations (Temp | `FSRA` | — | 1 | consultation |
| 2186 | Attachment 8 Draft Form 11 1 Mining Reporting Entities | `FSRA` | — | 1 | consultation |
| 2187 | Appendix 5   Amendments To Mir 0 | `FSRA` | — | 1 | consultation |
| 2188 | Consultation Paper No. 4 Of 2025   Consumer Protection (13 May2025) | `FSRA` | — | 1 | consultation |
| 2189 | Consultation Paper No. 7 Of 2025   Administrative Regulations | `FSRA` | — | 1 | consultation |
| 2190 | Consultation Paper No. 3 Of 2023 | `FSRA` | — | 1 | consultation |
| 2191 | Appendix 2 Feeslateregulatoryreturns Pruamendments | `FSRA` | — | 1 | consultation |
| 2192 | Appendix 3   Proposed Amendments To Gen | `FSRA` | — | 1 | consultation |
| 2193 | Consultation Paper No. 3 Of 2024   Proposal Concerning Registration Of Certain Trusts Particulars | `FSRA` | — | 1 | consultation |
| 2195 | Consultation Paper No. 8 Of 2024   Commercial Permits | `FSRA` | — | 1 | consultation |
| 2196 | Appendix 9   Proposed Amendments To Mkt | `FSRA` | — | 1 | consultation |
| 2198 | Consultation Paper No 4 Of 2018 Proposed Regulatory Framework For Operators Of Private Financing Platforms | `FSRA` | — | 1 | consultation |
| 2199 | Appendix 4   Proposed Amendments T %20Funds | `FSRA` | — | 1 | consultation |
| 2201 | Consultation Paper No.1 Of 2021   Proposed Amendments To The Registration Authority%E2%80%99S Decision Procedures And Enforcement Manual | `FSRA` | — | 1 | consultation |
| 2202 | Appendix 5   Clr (Exemption Order)   Editorial Version | `FSRA` | — | 1 | consultation |
| 2203 | Attachment 1   Guidance On Information Technology Risk Management | `FSRA` | — | 1 | consultation |
| 2205 | Consultation Paper No. 11 Of 2024   Proposed Amendments To Thedigital Asset Regulatory Framework | `FSRA` | — | 1 | consultation |
| 2207 | Appendix 3   Proposed Commercial Licensing Regulations (Conditions Of Licence And Br. Rules) 2022 | `FSRA` | — | 1 | consultation |
| 2208 | Attachment B   Proposed Amendments To Bills Of Exchange Act 1882 | `FSRA` | — | 1 | consultation |
| 2209 | Consultation Paper No 10 Of 2025   Proposed Framework For Thestaking Of Virtual Assets | `FSRA` | — | 1 | consultation |
| 2210 | Consultation Paper No. 3 Of 2022   Proposed Changes To Adgm Commercial Legislation | `FSRA` | — | 1 | consultation |
| 2211 | Appendix 6 (Proposed Amendments To Mir) | `FSRA` | — | 1 | consultation |
| 2212 | Attachment A   Proposed Amendments To Trustee Act 1925 | `FSRA` | — | 1 | consultation |
| 2214 | Consultation Paper No8 Of 2018 Accountsfinespolicy Dec 2018 | `FSRA` | — | 1 | consultation |
| 2215 | Appendix 3 Feeslateregulatoryreturns Pinamendments | `FSRA` | — | 1 | consultation |
| 2217 | Discussionpaper No1Of2022 Decentralisedfinance Apr2022 Final | `FSRA` | — | 1 | consultation |
| 2218 | Attachment 6 Draft Form 9 1 Restriction Agreement | `FSRA` | — | 1 | consultation |
| 2220 | Consultation Paper No. 5 Of 2024 Sfos And Company Charges | `FSRA` | — | 1 | consultation |
| 2221 | Consultation Paper No. 8 Of 2025   Proposed Enhancements To Theregulatory Framework | `FSRA` | — | 1 | consultation |
| 2222 | Appendix 6   Proposed Amendments T Glo | `FSRA` | — | 1 | consultation |
| 2223 | Appendix 4   Clr (Controlled Activities) Rules   Editorial Version | `FSRA` | — | 1 | consultation |
| 2224 | Appendix 5   Proposed Amendments To Gen | `FSRA` | — | 1 | consultation |
| 2225 | Appendix 6   Amendments To Pin | `FSRA` | — | 1 | consultation |
| 2226 | Attachment 1   Proposed Guidance On Crypto Mining Activities (Updated 14.01.2026) | `FSRA` | — | 1 | consultation |
| 2227 | Appendix 3   Proposed Amendments To Cobs | `FSRA` | — | 1 | consultation |
| 2228 | Appendix 4   Proposed Amendments To Glo | `FSRA` | — | 1 | consultation |
| 2229 | Attachment%201%20 %20Regulatory%20Considerations%20Outline | `FSRA` | — | 1 | consultation |
| 2230 | Appendix 6   Amendments To Mkt | `FSRA` | — | 1 | consultation |
| 2231 | Appendix 5   Proposed Amendments To Mir | `FSRA` | — | 1 | consultation |
| 2232 | Discussion Paper 1 Of 2025 Updating The Regulatory Framework For Insurance In Adgm | `FSRA` | — | 1 | consultation |
| 2233 | Data Protection Regulations 2020 | `FSRA` | — | 1 | consultation |
| 2234 | Consultation Paper No.3 2020   Electronic Transactions Regulations | `FSRA` | — | 1 | consultation |
| 2236 | Consultation Paper No. 4 Of 2024 (27 May 2024) | `FSRA` | — | 1 | consultation |
| 2237 | Appendix 7   Proposed Amendments To Ifr | `FSRA` | — | 1 | consultation |
| 2238 | Attachment 7 %20Draft Form 10 1 Reporting Entities Quarterly Cash Report | `FSRA` | — | 1 | consultation |
| 2239 | Attachment 2   Proposed Amendments To Va Guidance | `FSRA` | — | 1 | consultation |
| 2240 | Appendix 3   Business And Company Names Rules 2020 | `FSRA` | — | 1 | consultation |
| 2241 | Discussion Paper No. 1 Of 2026 Concerning Crypto Mining Activities | `FSRA` | — | 1 | consultation |
| 2242 | Appendix 7   Proposed Amendments To Pru | `FSRA` | — | 1 | consultation |
| 2243 | Appendix 3   Proposed Amendments To Glo 0 | `FSRA` | — | 1 | consultation |
| 2244 | Discussion Paper No. 1 Of 2024   Enhancing The Sustainable Finance Regulatory Framework For Adgm | `FSRA` | — | 1 | consultation |
| 2246 | Consultation Paper No. 5 Of 2025   Law Firms And Csp Conditions (16May 2025) | `FSRA` | — | 1 | consultation |
| 2247 | Discussion Paper No1 Of 2018 On Proposed Regulatory Framework For Private Financing Platforms Final | `FSRA` | — | 1 | consultation |
| 2248 | Consultation Paper No. 1 Of 2025   Proposal For Periodic Fundreporting Requirements | `FSRA` | — | 1 | consultation |
| 2249 | Consultation Paper No.2 Of 2020   Proposed Amendments To Dpem | `FSRA` | — | 1 | consultation |
| 2250 | Consultation Paper 9 Of 2025 | `FSRA` | — | 1 | consultation |
| 2251 | Appendix 3   Amendments To Gen 0 | `FSRA` | — | 1 | consultation |
| 2252 | Appendix 3   Limited Liability Partnership Rules 2020 | `FSRA` | — | 1 | consultation |
| 2253 | Appendix 3   Amendments To Gen 1 | `FSRA` | — | 1 | consultation |
| 2254 | Appendix 2   Proposed Limited Liability Partnerships Rules 2023 | `FSRA` | — | 1 | consultation |
| 2257 | Appendix 2   Proposed Amendments To Cobs | `FSRA` | — | 1 | consultation |
| 2258 | Attachment 1   Amendments To Cmc | `FSRA` | — | 1 | consultation |
| 2260 | Appendix 8   Amendments To Gpm | `FSRA` | — | 1 | consultation |
| 2261 | Consultation Paper No. 3 Of 2025   Cyber Risk Management Framework(Amended 6 May 2025) | `FSRA` | — | 1 | consultation |
| 2263 | Discussion Paper No. 1 Of 2023   It Risk Management | `FSRA` | — | 1 | consultation |
| 2264 | Consultation Paper No. 10 Of 2024   Proposed Miscellaneousamendments To Fsra Regualtions Rules And Guidance | `FSRA` | — | 1 | consultation |
| 2265 | Consultation Paper No. 11 Of 2025   Sales%2C Promot | `FSRA` | — | 1 | consultation |
| 2268 | Appendix 5 (Proposed Amendments To Ifr) | `FSRA` | — | 1 | consultation |
| 2269 | Appendix 5   Amendments To Pru | `FSRA` | — | 1 | consultation |
| 2270 | Consultation Paper No. 6 Of 2025   Substantial Public Interestrules (11 June 2025) | `FSRA` | — | 1 | consultation |
| 2271 | Appendix 3 (Proposed Amendments To Gen) | `FSRA` | — | 1 | consultation |
| 2272 | Cp11 2025 Appendix 3   Commercial Permits Regulations (Sale | `FSRA` | — | 1 | consultation |
| 2273 | Attachment 1   Proposed Amendments To Gpm | `FSRA` | — | 1 | consultation |
| 2274 | Attachment 2   Amendments To Gpm | `FSRA` | — | 1 | consultation |
| 2276 | Consultation Paper No. 7 Of 2022   Amendments To The Adgm%E2%80%99S Company Service Provider Regulatory Framework | `FSRA` | — | 1 | consultation |
| 2277 | Appendix 6   Proposed Data Protection Regulation (Fines) Rules 2022 0 | `FSRA` | — | 1 | consultation |
| 2278 | Appendix 2   Commercial Permits Regulations (Shisha) Rules 2024 | `FSRA` | — | 1 | consultation |
| 2279 | Consultation Paper No.6 Of 2021 Boc Regulations | `FSRA` | — | 1 | consultation |
| 2280 | Appendix 3   Proposed Amendments To Glo | `FSRA` | — | 1 | consultation |
| 2283 | Consultation Paper No. 1 Of 2024 Proposed Enhancements To The Ra'S Investigative Powers 29 Feb 2024 | `FSRA` | — | 1 | consultation |
| 2286 | Appendix 2   Proposed Amendments To Gen | `FSRA` | — | 1 | consultation |
| 2287 | Appendix 3   Amendments To Gen | `FSRA` | — | 1 | consultation |
| 2289 | Appendix 4 Feeslateregulatoryreturns Gloamendments | `FSRA` | — | 1 | consultation |
| 2292 | Guidance Authorisation Investment Management | `FSRA` | — | 1 | guidance |
| 2293 | Guidance Vc Fund Managers | `FSRA` | — | 1 | guidance |
| 2294 | Guidance Fintech Reglab | `FSRA` | — | 1 | guidance |
| 2295 | Guidance Private Financing Platforms | `FSRA` | — | 1 | guidance |
| 2297 | Guidance Digital Securities Virtual Assets | `FSRA` | — | 1 | guidance |
| 2298 | Guidance Digital Investment Management | `FSRA` | — | 1 | guidance |
| 2299 | Guidance Otc Leveraged Products | `FSRA` | — | 1 | guidance |
| 2300 | Guidance Virtual Asset Activities | `FSRA` | — | 1 | guidance |
| 2311 | Guidance Esg Disclosures | `FSRA` | — | 1 | guidance |
| 2312 | Guidance Listing Applications | `FSRA` | — | 1 | guidance |
| 2313 | Code Of Market Conduct Cmc | `FSRA` | — | 1 | guidance |
| 2314 | Guidance Fintech | `FSRA` | — | 1 | guidance |
| 2315 | Guidance Enforcement And Disqualificati | `FSRA` | — | 1 | guidance |
| 2317 | Guidance Data Protection Guidance Note | `FSRA` | — | 1 | guidance |
| 2319 | Guidance Digital Securities Activities | `FSRA` | — | 1 | guidance |
| 2320 | Guidance Enabling Technologies | `FSRA` | — | 1 | guidance |
| 2321 | Guidance Guidance Exemptions Requiremen | `FSRA` | — | 1 | guidance |
| 2322 | Guidance Apis In Adgm | `FSRA` | — | 1 | guidance |
| 2323 | Guidance Sustainable Finance | `FSRA` | — | 1 | guidance |
| 2324 | Guidance Restricted Securities | `FSRA` | — | 1 | guidance |
| 2326 | Guidance Continuous Disclosure | `FSRA` | — | 1 | guidance |
| 2327 | Guidance Preparing Prospectus | `FSRA` | — | 1 | guidance |
| 2328 | Guidance Spot Commodities | `FSRA` | — | 1 | guidance |
| 2329 | Guidance Digital Assets | `FSRA` | — | 1 | guidance |
| 2330 | Guidance Guidance Policy Statements | `FSRA` | — | 1 | guidance |
| 2331 | Fsra Confidentiality Policy | `FSRA` | — | 1 | guidance |
| 2332 | Guidance Sustainable Finance 0 | `FSRA` | — | 1 | guidance |
| 2333 | Guidance Beneficial Ownership And Contr | `FSRA` | — | 1 | guidance |
| 2334 | Guidance Petroleum Disclosure | `FSRA` | — | 1 | guidance |
| 2335 | Guidance Guidance Applications Accounts | `FSRA` | — | 1 | guidance |
| 2336 | Guidance Mining Disclosure | `FSRA` | — | 1 | guidance |
| 2337 | Guidance Guidance Client Money | `FSRA` | — | 1 | guidance |
| 2338 | Guidance Voluntary Liquidation Guidance | `FSRA` | — | 1 | guidance |
| 2339 | Guidance Alternative Financingfunding | `FSRA` | — | 1 | guidance |
| 2451 | FCCP Notice No. 1 of 2024 - Terrorist Proliferation Financing Red Flags | `FSRA` | — | 1 | circular |
| 2452 | Code of Market Conduct (CMC) VER04.311025 | `FSRA` | — | 1 | guidance |
| 2453 |  | `FSRA` | — | 1 | circular |
| 2455 | Dear SEO Letter (Banks) - Banking Sector Risk Assessments 20260210 | `FSRA` | — | 1 | circular |
| 2456 | FSRA Dear SEO letter Outsourcing Thematic Review 20260129 | `FSRA` | — | 1 | circular |
| 2457 | 2025 Dear SEO AML letter 2025 | `FSRA` | — | 1 | circular |
| 2460 | Dear SEO Letter Countercyclical Buffer | `FSRA` | — | 1 | circular |
| 2461 | Dear SEO Letter Banks 20250317 PRU Data FINAL | `FSRA` | — | 1 | circular |
| 2462 | Thematic Review AMLCFT Overall observations | `FSRA` | — | 1 | circular |
| 2464 | 20220826-Thematic-review | `FSRA` | — | 1 | circular |
| 2465 | FSRA-SEO-22-0001L-CEO | `FSRA` | — | 1 | circular |
| 2466 | PDF | `FSRA` | — | 1 | circular |
| 2467 | FSRA - FCCP -  Notice No. 15 of 2026 - Cyber Risk Survey Findings and Recommendations | `FSRA` | — | 1 | circular |
| 2468 | FSRA - FCCP -  Notice No. 22 of 2026 - Updates to Information Technology IT and Cyber Incident Reporting | `FSRA` | — | 1 | circular |
| 2469 | FSRA - FCCP - Notice No. 1 of 2022 - UAE Strategic Review on the TFS Case Studies | `FSRA` | — | 1 | circular |
| 2470 | FSRA - FCCP - Notice No. 1 of 2023 - Regarding Decision of National Committee No 1 (9/2021) | `FSRA` | — | 1 | circular |
| 2471 | FSRA - FCCP - Notice No. 12 of 2022 - TIN Collections | `FSRA` | — | 1 | circular |
| 2472 | FSRA - FCCP - Notice No. 128 of 2025 - Cybercrime Prevention - Protect your organsation from Malware | `FSRA` | — | 1 | circular |
| 2473 | FSRA - FCCP - Notice No. 14 of 2022 - Interpretative Jurisdictional Risk | `FSRA` | — | 1 | circular |
| 2474 | FSRA - FCCP - Notice No. 14 of 2023 - Reminder on the key AML-TFS Federal Reporting Obligations | `FSRA` | — | 1 | circular |
| 2475 | FSRA - FCCP - Notice No. 15 of 2023 - Rising use of Virtual Currencies by Criminals to Launder their Illegal Profit | `FSRA` | — | 1 | circular |
| 2476 | FSRA - FCCP - Notice No. 15 of 2024 - Cyber Security Council Alerts | `FSRA` | — | 1 | circular |
| 2477 | FSRA - FCCP - Notice No. 16 of 2022 - Counter Proliferation Financing Guidance | `FSRA` | — | 1 | circular |
| 2478 | FSRA - FCCP - Notice No. 165 of 2025 – Unlicensed Virtual Asset activities | `FSRA` | — | 1 | circular |
| 2479 | FSRA - FCCP - Notice No. 172 of 2025 – Update on the UAE Federal AMLCFT Legislative Framework | `FSRA` | — | 1 | circular |
| 2480 | FSRA - FCCP - Notice No. 179 of 2025 – Announcement of the 1st FSRA cyber threat intelligence weekly newsletter | `FSRA` | — | 1 | circular |
| 2481 | FSRA - FCCP - Notice No. 183 of 2025 – Reminder on the Re-Imposition of UN Targeted Financial Sanctions 1737 (2006) Following the Expiry of UNSCR 2231 (2015) | `FSRA` | — | 1 | circular |
| 2482 | FSRA - FCCP - Notice No. 186 of 2025 – Regarding the Decision of the National Committee No (15) of 2025 - Update the list of High-Risk | `FSRA` | — | 1 | circular |
| 2483 | FSRA - FCCP - Notice No. 2 of 2024 - Guidance on Proliferation Finance Institutional Risk Assessment for FIs, DNFBPs and VASPs | `FSRA` | — | 1 | circular |
| 2484 | FSRA - FCCP - Notice No. 20 of 2024 - Regarding Decision of National Committee No 1 (9/2021) - Update the list of High-Risk Jurisdiction | `FSRA` | — | 1 | circular |
| 2485 | FSRA - FCCP - Notice No. 23 of 2022 - Targeted Financial Sanctions Guideline for Insurance Sector | `FSRA` | — | 1 | circular |
| 2486 | FSRA - FCCP - Notice No. 23 of 2023 - Decision of National Committee No. 1(9/2021) - Update on High-Risk Jurisdiction | `FSRA` | — | 1 | circular |
| 2487 | FSRA - FCCP - Notice No. 24 of 2022 - UAE Joint typologies Report on Money or Value Transfer | `FSRA` | — | 1 | circular |
| 2488 | FSRA - FCCP - Notice No. 25 of 2021 - CRS Compliance Programme | `FSRA` | — | 1 | circular |
| 2489 | FSRA - FCCP - Notice No. 26 of 2025 – Updating the annual AML Return form | `FSRA` | — | 1 | circular |
| 2490 | FSRA - FCCP - Notice No. 28 of 2021 - regarding the Decision of National Committee No 1 (9/2021) | `FSRA` | — | 1 | circular |
| 2491 | FSRA - FCCP - Notice No. 28 of 2025 - regarding Decision of National Committee No 1 (9/2021) - Update the list of High-Risk Jurisdiction | `FSRA` | — | 1 | circular |
| 2492 | FSRA - FCCP - Notice No. 29 of 2021- Updated Targeted Financial Sanctions (TFS) Guidance and Typologies paper | `FSRA` | — | 1 | circular |
| 2493 | FSRA - FCCP - Notice No. 29 of 2023 - Guidance on Terrorist and Proliferation Financing Red Flags for FIs, DNFBPs and VASPs | `FSRA` | — | 1 | circular |
| 2494 | FSRA - FCCP - Notice No. 3 of 2023 - Reminder on the key AML Federal Obligations | `FSRA` | — | 1 | circular |
| 2495 | FSRA - FCCP - Notice No. 3 of 2024 - Regarding Decision of National Committee No 7(5/2023) - Unlicensed Virtual Assets Service Providers Guidance | `FSRA` | — | 1 | circular |
| 2496 | FSRA - FCCP - Notice No. 33 of 2025 - Cybercrime Prevention - Avoiding Phishing Attacks | `FSRA` | — | 1 | circular |
| 2497 | FSRA - FCCP - Notice No. 34 of 2024 - Strategic Review on the Targeted Financial Sanctions (TFS) Case Studies | `FSRA` | — | 1 | circular |
| 2498 | FSRA - FCCP - Notice No. 37 of 2025 - Updated UAE National ML-TF Risk Assessment Report - Public Version | `FSRA` | — | 1 | circular |
| 2499 | FSRA - FCCP - Notice No. 4 of 2022 - TFS Awareness in relation to UNSCRs 1718 (2006) and 2231 (2015) | `FSRA` | — | 1 | circular |
| 2500 | FSRA - FCCP - Notice No. 41 of 2022 - Updated Targeted Financial Sanctions (TFS) Guidance | `FSRA` | — | 1 | circular |
| 2501 | FSRA - FCCP - Notice No. 47 of 2023 - regarding Decision of National Committee No 1(9/2021) - Update the list of High-Risk Jurisdiction | `FSRA` | — | 1 | circular |
| 2502 | FSRA - FCCP - Notice No. 49 of 2024 - Regarding Decision of National Committee No 1(9/2021) - Update the list of High-Risk Jurisdiction | `FSRA` | — | 1 | circular |
| 2503 | FSRA - FCCP - Notice No. 50 of 2022 - Invitation to DOLFIN E-learning Platform | `FSRA` | — | 1 | circular |
| 2504 | FSRA - FCCP - Notice No. 51 of 2022 - Updated Guidance on Counter Proliferation Financing for FIs, DNFBPs and VASPs | `FSRA` | — | 1 | circular |
| 2505 | FSRA - FCCP - Notice No. 6 of 2023 - Revision of the annual AML Return form | `FSRA` | — | 1 | circular |
| 2506 | FSRA - FCCP - Notice No. 7 of 2022 - Revised AML Return form | `FSRA` | — | 1 | circular |
| 2507 | FSRA - FCCP - Notice No. 7 of 2024 - Revision and automation of the annual AML Return form | `FSRA` | — | 1 | circular |
| 2508 | FSRA - FCCP - Notice No. 78 of 2025 - regarding Decision of National Committee No (6) of 2025 - Update the list of High-Risk Jurisdiction | `FSRA` | — | 1 | circular |
| 2509 | FSRA - FCCP - Notice No. 8 of 2023 - Joint Guidance on common themes observed during the STR/SARs thematic Review of FIs and DNFBPs | `FSRA` | — | 1 | circular |
| 2510 | FSRA - FCCP - Notice No. 80 of 2025 - Reminder on Compliance with Targeted Financial Sanctions and Reporting through goAML | `FSRA` | — | 1 | circular |
| 2511 | FSRA - FCCP - Notice No. 84 of 2024 - Cyber Security Council Alerts - Indicators of Compromise (IoC’s) | `FSRA` | — | 1 | circular |
| 2512 | FSRA - FCCP - Notice No. 84 of 2025 - Reminder on key AML / TFS Obligation, Registration and Reporting through goAML portal | `FSRA` | — | 1 | circular |
| 2513 | FSRA - FCCP - Notice No. 9 of 2023 - Requirement to conduct an Institutional Terrorist Financing (TF) and Proliferation Financing (PF) Risk Assessment | `FSRA` | — | 1 | circular |
| 2514 | FSRA - FCCP - Notice No. 91 of 2025 - Updated on Targeted Financial Sanctions (TFS) Guidance | `FSRA` | — | 1 | circular |
| 2515 | FSRA - FCCP - Notice No. 92 of 2024 - Regarding Decision of National Committee No 1 (9/2021) - Update the list of High-Risk Jurisdiction | `FSRA` | — | 1 | circular |
| 2517 | FSRA - FCPU - Notice No. 23 of 2021 - Unusual money flows should be reported through "GoAML" | `FSRA` | — | 1 | circular |
| 2518 | FSRA - FCPU - Notice No. 24 of 2021 - Targeted Financial Sanctions in relation to UNSCRs 1267 (1999), 1989 (2011), and 1988 (2011) | `FSRA` | — | 1 | circular |
| 2519 | FSRA - FCPU Circular No. 1 of 2017 - Reporting Suspicious Activities to The AMLSCU | `FSRA` | — | 1 | circular |
| 2520 | FSRA - FCPU Notice No. 1 of 2017 - UAE Upcoming FATF ME and NRA | `FSRA` | — | 1 | circular |
| 2521 | FSRA - FCPU Notice No. 1 of 2020 - Revised Anti-Money Laundering and Sanctions Rules and Guidance (AML Rulebook) | `FSRA` | — | 1 | circular |
| 2522 | FSRA - FCPU Notice No. 1 of 2021 - Updated version of Cabinet Resolution No. (74) of 2020 replacement for (20) of 2019 | `FSRA` | — | 1 | circular |
| 2523 | FSRA - FCPU Notice No. 10 of 2020 - UAE National AML Committee Launched its website | `FSRA` | — | 1 | circular |
| 2524 | FSRA - FCPU Notice No. 10 of 2021 - AMLCFT Guidance’s for FIs and DNFBPs | `FSRA` | — | 1 | circular |
| 2525 | FSRA - FCPU Notice No. 11 of 2020 - FATF report on VAs - Red Flag Indicators | `FSRA` | — | 1 | circular |
| 2526 | FSRA - FCPU Notice No. 13 of 2019 - Cabinet Resolution No.20 of 2019 | `FSRA` | — | 1 | circular |
| 2527 | FSRA - FCPU Notice No. 13 of 2020 - Update on the UAE National List of Terrorist Individuals and Entities | `FSRA` | — | 1 | circular |
| 2528 | FSRA - FCPU Notice No. 13 of 2021 - Targeted Financial Sanctions Typologies paper | `FSRA` | — | 1 | circular |
| 2529 | FSRA - FCPU Notice No. 15 of 2019 - Reporting Suspicious Activities to the FIU through ‘goAML’ System | `FSRA` | — | 1 | circular |
| 2530 | FSRA - FCPU Notice No. 15 of 2020 - Governance Principles and Practices to Mitigate Cyber Threats and Crime | `FSRA` | — | 1 | circular |
| 2531 | FSRA - FCPU Notice No. 15 of 2021 - AML thematic review outcome to DNFBPs | `FSRA` | — | 1 | circular |
| 2533 | FSRA - FCPU Notice No. 16 of 2020 - Cabinet Resolution No. (74) of 2020 replacement for (20) of 2019 | `FSRA` | — | 1 | circular |
| 2534 | FSRA - FCPU Notice No. 16 of 2021 - Targeted Financial Sanctions Guidance | `FSRA` | — | 1 | circular |
| 2535 | FSRA - FCPU Notice No. 17 of 2019 on ‘go-live’ plan for the goAML system | `FSRA` | — | 1 | circular |
| 2537 | FSRA - FCPU Notice No. 18 of 2019 - UAE Updated National Risk Assessment (NRA) FOR 2019 | `FSRA` | — | 1 | circular |
| 2538 | FSRA - FCPU Notice No. 18 of 2021 - report Targeted Financial Sanction (TFS) match to the Financial Intelligence Unit through the “goAML” system | `FSRA` | — | 1 | circular |
| 2539 | FSRA - FCPU Notice No. 2 of 2020 - Launch of new format for AML annual return form | `FSRA` | — | 1 | circular |
| 2540 | FSRA - FCPU Notice No. 21 of 2019 - SEO Letter - AML Thematic Review Outcome | `FSRA` | — | 1 | circular |
| 2542 | FSRA - FCPU Notice No. 4 of 2020 - Notice on extra cybersecurity measures in response to COVID-19 | `FSRA` | — | 1 | circular |
| 2543 | FSRA - FCPU Notice No. 5 of 2021 - regarding Subscribe to UNSCR and National Sanction Lists Alerts of the Executive Office website | `FSRA` | — | 1 | circular |
| 2544 | FSRA - FCPU Notice No. 6 of 2020 - Joint AML Supervisory Guidance on the treatment of AML related and Obligations in the Context of the COIVD-19 Crisis - Arabic | `FSRA` | — | 1 | circular |
| 2545 | FSRA - FCPU Notice No. 6 of 2020 - Joint AML Supervisory Guidance on the treatment of AML related and Obligations in the Context of the COIVD-19 Crisis - English | `FSRA` | — | 1 | circular |
| 2546 | FSRA - FCPU Notice No. 6 of 2021 - regarding Decision of National Committee No 1(2/2021) | `FSRA` | — | 1 | circular |
| 2548 | FSRA - FCPU Notice No. 7 of 2020 - Subscribe to UNSCR and National Sanctions Lists Alerts, and Obligations Under Article (19/1) of Cabinet Resolution No. (20) of 2019 | `FSRA` | — | 1 | circular |
| 2549 | FSRA - FCPU Notice No. 7 of 2021 - Regarding the request to cross check customer databases | `FSRA` | — | 1 | circular |
| 2550 | FSRA - FCPU Notice No. 8 of 2020 - CRS Regulation amendments and implementation | `FSRA` | — | 1 | circular |
| 2551 | FSRA - FCPU Notice No. 8 of 2021 - Subscribe to UNSCR and National Sanction Lists Alerts of the Executive Office website | `FSRA` | — | 1 | circular |
| 2552 | FSRA - FCPU Notice No. 9 of 2019 - UAE National Money Laundering and Terrorist Financing Risk Report | `FSRA` | — | 1 | circular |
| 2553 | FSRA - FCPU Notice No. 9 of 2020 - Update on goAML Guides | `FSRA` | — | 1 | circular |
| 2554 | FSRA - FCPU Notice No. 9 of 2021 - ADGM - Know Your Customer (KYC) Guidelines for Financial Institutions (FIs) and Designated Non-Financial Businesses and Professions (DNFBPs) | `FSRA` | — | 1 | circular |
| 2712 | Amendments Companies Regulations Register Of Auditors Rules 2017 | `FSRA` | — | 1 | rulebook |
| 2713 | Amendments Companies Regulations Model Articles Rules 2015 2 | `FSRA` | — | 1 | rulebook |
| 2714 | (3) Companies Regulations (Auditors) Rules 2022   Editorial Version 0 | `FSRA` | — | 1 | rulebook |
| 2715 | Amendments Companies Regulations 2020 May 2020 | `FSRA` | — | 1 | rulebook |
| 2716 | (6) Companies Regulations (Names Adjudication) Rules 2022   Editorial Version | `FSRA` | — | 1 | rulebook |
| 2757 | Adgm+Brand+Book 2025 | `FSRA` | — | 1 | guidance |
| 2758 | Adgm+Brand+Book 2025 | `FSRA` | — | 1 | consultation |
| 2774 | Annex A   Amendments To Fsmr 2 | `FSRA` | — | 1 | consultation |
| 2775 | Appendix 1   Amendments To Aml | `FSRA` | — | 1 | consultation |
| 2776 | Appendix 2   Amendments To Gen | `FSRA` | — | 1 | consultation |
| 2777 | Appendix 3   Amendments To Glo | `FSRA` | — | 1 | consultation |
| 2778 | Attachment 1   Amendments To Gpm | `FSRA` | — | 1 | consultation |
| 2779 | Consultation Paper No. 1 Of 2026   Proposed Enhancements To The Anti Money Laundering Framework Of The Fsra | `FSRA` | — | 1 | consultation |
| 67 | Adgm Courts Regulations Amendment No 1 Of 2025   17102025 | `FSRA` | `OTHER` | 0 | rulebook |
| 69 | Adgm Courts Regulations Amendment No 1 Of 2023   Final 08112023 | `FSRA` | `OTHER` | 0 | rulebook |
| 70 | Amendments Companies Regulations Register Of Auditors Rules 2017 | `FSRA` | `OTHER` | 0 | rulebook |
| 73 | Adgm Court Procedure Rules Amendment No 2 Of 2022 | `FSRA` | `OTHER` | 0 | rulebook |
| 75 | Amendments Limited Liability Partnership Rules 2020 April 2020 | `FSRA` | `OTHER` | 0 | rulebook |
| 79 | Adgm1547 19839 Ver20250228 | `FSRA` | `OTHER` | 0 | rulebook |
| 81 | Adgm1547 26706 Ver02072325 | `FSRA` | `OTHER` | 0 | rulebook |
| 84 | Adgm Court Procedure Rules Amendment No 1 Of 2022 | `FSRA` | `OTHER` | 0 | rulebook |
| 89 | Adgm1547 22828 Ver20240909 | `FSRA` | `OTHER` | 0 | rulebook |
| 96 | Adgm1547 22885 Ver12082020 | `FSRA` | `OTHER` | 0 | rulebook |
| 98 | Adgm Courts Regulations Amendment No 2 Of 2023 | `FSRA` | `OTHER` | 0 | rulebook |
| 107 | Adgm Courts Regulations Amendment No 1 Of 2020   24 June 2020 | `FSRA` | `OTHER` | 0 | rulebook |
| 108 | Adgm Court Procedure Rules Amendment No 1 Of 2018 | `FSRA` | `OTHER` | 0 | rulebook |
| 112 | Divisions And Jurisdiction (Court Of First Instance) Rules 2015Amendment No 1 Of 2025   17102025 | `FSRA` | `OTHER` | 0 | rulebook |
| 114 | Adgm Court Procedure Rules Amendment No 3 Of 2020 (Amended 30112020) | `FSRA` | `OTHER` | 0 | rulebook |
| 118 | Adgm Court Procedure Rules Amendment No 1 Of 2019 | `FSRA` | `OTHER` | 0 | rulebook |
| 119 | Amendments Companies Regulations Model Articles Rules 2015 2 | `FSRA` | `OTHER` | 0 | rulebook |
| 120 | Adgm Courts Regulations Amendment No 1 Of 2018 | `FSRA` | `OTHER` | 0 | rulebook |
| 125 | Adgm1547 19538 Ver01110319 | `FSRA` | `OTHER` | 0 | rulebook |
| 127 | Adgm Court Procedure Rules Amendment No 1 Of 2021 15022021 | `FSRA` | `OTHER` | 0 | rulebook |
| 131 | Adgm Court Procedure Rules Amendment No 1 Of 2020 | `FSRA` | `OTHER` | 0 | rulebook |
| 132 | Adgm1547 13059 Ver20251017 | `FSRA` | `OTHER` | 0 | rulebook |
| 138 | Adgm1547 22453 Ver04232020 | `FSRA` | `OTHER` | 0 | rulebook |
| 143 | Adgm Court Procedure Rules Amendment No 1 Of 2023 | `FSRA` | `OTHER` | 0 | rulebook |
| 147 | Adgm Court Procedure Rules Amendment No1 Of 2017 | `FSRA` | `OTHER` | 0 | rulebook |
| 148 | Amendments Rmc Ver02 210218 | `FSRA` | `OTHER` | 0 | rulebook |
| 152 | Adgm Courts Regulations Amendment No 1 Of 2017 | `FSRA` | `OTHER` | 0 | rulebook |
| 163 | Amendments Employment Regulations 2019 (Engaging Non Employees) Rules 2020 March 2020 | `ADGM_RA` | `OTHER` | 0 | rulebook |
| 167 | Adgm1547 28194 Ver20250610 | `FSRA` | `OTHER` | 0 | rulebook |
| 168 | Adgm1547 18205 Ver20251017 | `FSRA` | `OTHER` | 0 | rulebook |
| 171 | Rmc Ver02 210218 | `FSRA` | `OTHER` | 0 | rulebook |
| 172 | Divisions And Jurisdiction (Court Of First Instance) Rules 2015 Amendment No 1 Of 2020 | `FSRA` | `OTHER` | 0 | rulebook |
| 173 | Amendments Commercial Licensing Regulations 2015 (Fines) Rules 2020 | `FSRA` | `OTHER` | 0 | rulebook |
| 177 | Adgm1547 26661 Ver02072325 | `FSRA` | `OTHER` | 0 | rulebook |
| 180 | Adgm1547 22827 Ver20250421 | `FSRA` | `OTHER` | 0 | rulebook |
| 181 | Adgm Court Procedure Rules Amendment No 2 Of 2020 (Amended 01112020) Final | `FSRA` | `OTHER` | 0 | rulebook |
| 185 | Adgm Court Procedure Rules Amendment No 1 Of 2025   17102025 | `FSRA` | `OTHER` | 0 | rulebook |
| 188 | Adgm1547 23292 Ver04082021 | `FSRA` | `OTHER` | 0 | rulebook |
| 190 | Amendments Companies Regulations 2020 May 2020 | `FSRA` | `OTHER` | 0 | rulebook |
| 191 | Adgm Court Procedure Rules Amendment No 2 Of 2017 | `FSRA` | `OTHER` | 0 | rulebook |
| 192 | Adgm Courts Regulations Amendment No 1 Of 2024 11122024 | `FSRA` | `OTHER` | 0 | rulebook |
| 198 | Adgm1547 23293 Ver04082021 | `FSRA` | `OTHER` | 0 | rulebook |
| 202 | Adgm1547 29641 Ver20251028 | `FSRA` | `OTHER` | 0 | rulebook |
| 205 | Adgm Court Procedure Rules Amendment No 2 Of 2021 01092021 | `FSRA` | `OTHER` | 0 | rulebook |
| 211 | Adgm1547 22830 Ver18022020 | `FSRA` | `OTHER` | 0 | rulebook |
| 213 | Amendments Adgm Business And Company Names Rules 2016 2 | `FSRA` | `OTHER` | 0 | rulebook |
| 165 | Bank Recovery And Resolution Regulation 2018 20 December 2018 | `FSRA` | `BRR` | 0 | rulebook |
| 2748 | Employment Regulations 2019 (Consolidated) | `ADGM_RA` | `ADGM-ER` | 0 | legislation |
| 2731 | Companies Regulations 2020 | `ADGM` | `ADGM-CR` | 0 | company_law |
| 1779 | Annex A Draft Adgm Employment Regulations 2019 Pc Version Tracked | `ADGM_RA` | — | 0 | consultation |
| 1796 | Annex A   Proposed Employment Regulations 2024 | `ADGM_RA` | — | 0 | consultation |
| 1894 | Annex B   Proposed Employment Regulations 2024 (Editorial Blackline) | `ADGM_RA` | — | 0 | consultation |
| 1905 | Annex E   Proposed Employment Regulations (Amendment No.1) 2022 | `ADGM_RA` | — | 0 | consultation |
| 1958 | (2) Annex A   Proposed Whistleblowing Regulations 2024 | `ADGM_RA` | — | 0 | consultation |
| 1996 | Annex A Employment Regulations Consultation Paper No 5 Of 2015 | `ADGM_RA` | — | 0 | consultation |
| 2038 | Annex A Draft Adgm Employment Regulations 2019 Pc Version Clear | `ADGM_RA` | — | 0 | consultation |
| 2041 | Annex B Employment Regulations Compensation And Awards Limits Rules 2019 Pc Version Clean | `ADGM_RA` | — | 0 | consultation |
| 2054 | (3) Annex B   Proposed Amendments To Employment Regulations 2019 | `ADGM_RA` | — | 0 | consultation |
| 2103 | Supplementary Guidance Regulatory Framework Whistleblowing July 2025 0 | `ADGM_RA` | — | 0 | guidance |
| 2290 | Appendix 7   Proposed Employment Regulations (Engaging Non Employees) Rules 2022 | `ADGM_RA` | — | 0 | consultation |

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
