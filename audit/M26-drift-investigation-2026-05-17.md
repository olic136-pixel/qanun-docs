# M26 — Local↔Hetzner corpus snapshot drift investigation

**Date:** 17 May 2026
**Source session:** Wave C M26 drift parity
**Mode:** Read-only diagnostic; apply deferred to follow-on session

## Per-entity row count delta

| Entity | Local | Hetzner | Delta | Local max_updated | Hetzner max_updated |
|---|---:|---:|---:|---|---|
| ADGM | 7 | 2 | -5 | 2026-05-13 17:21:16 | — |
| ADGM FSRA | 71 | 37 | -34 | 2026-05-13 17:19:42 | — |
| ADGM_COURTS | 287 | 264 | -23 | 2026-05-13 17:21:16 | 2026-05-12T09:06:05.060081+00:00 |
| ADGM_RA | 66 | 43 | -23 | 2026-05-13 17:21:16 | 2026-05-10T07:05:55.895348+00:00 |
| BVI_FSC | 27 | 29 | +2 | 2026-04-15T07:01:20.582934+00:00 | 2026-04-15T07:01:20.582934+00:00 |
| DFSA | 22 | 22 | 0 | 2026-05-17 15:07:03 | 2026-05-17 15:20:21 |
| DIFC | 6 | 6 | 0 | 2026-03-18T02:31:10.782416+00:00 | 2026-03-18T02:31:10.782416+00:00 |
| DIFC_COURTS | 1066 | 1066 | 0 | 2026-03-15T18:40:06.140464+00:00 | 2026-03-15T18:40:06.140464+00:00 |
| EL_SALVADOR | 16 | 19 | +3 | 2026-04-03T07:32:21.975734+00:00 | 2026-04-03T07:32:49.389212+00:00 |
| FSRA | 657 | 732 | +75 | 2026-05-13 17:21:16 | 2026-05-02T05:21:13.500874+00:00 |
| MONDAQ | 2 | 2 | 0 | 2026-03-15T20:51:42.544202+00:00 | 2026-03-15T20:51:42.544202+00:00 |
| PANAMA | 1 | 1 | 0 | 2026-04-03T07:33:57.190209+00:00 | 2026-04-03T07:33:57.190209+00:00 |
| PANAMA_SMV | 6 | 6 | 0 | 2026-03-31T10:53:12.107879+00:00 | 2026-03-31T10:53:12.107879+00:00 |
| UAE_FEDERAL | 5 | 0 | -5 | 2026-05-13 17:21:16 | — |
| UNKNOWN | 0 | 57 | +57 | — | 2026-04-03T07:32:46.802550+00:00 |
| VARA | 12 | 12 | 0 | — | 2026-04-09T13:14:52.688466+00:00 |

## Set difference by source_key

- **Local-only rows** (in local, missing on Hetzner): 34
- **Hetzner-only rows** (in Hetzner, missing on local): 81

### Hetzner-only rows (sample, up to 20)

- `bvi_bvi_business_companies_act_schedules` — entity=BVI_FSC code=BVI-BCA title='Bvi Business Companies Act Schedules'
- `company_law_bvi_bvi_investment_business_approved_managers_regs` — entity=BVI_FSC code=BVI-REGS title='Bvi Investment Business Approved Managers Regs'
- `courts_adgm_2026_adgm_court_2026_ADGMCFI_13` — entity=ADGM_COURTS code=<NULL> title='Adgm Court 2026 Adgmcfi 13'
- `dfsa_afn_application-forms-and-notices-module-afn-ver5211-22` — entity=DFSA code=DFSA-AFN title='DFSA AFN Rulebook'
- `dfsa_ami_authorised-market-institutions-ami-ver3001-26` — entity=DFSA code=DFSA-AMI title='DFSA AMI Rulebook'
- `dfsa_aml_anti-money-laundering-counter-terrorist-financing-and-sanctions-module-aml-ver30` — entity=DFSA code=DFSA-AML title='DFSA AML Rulebook'
- `dfsa_aud_auditor-module-aud-ver1001-26` — entity=DFSA code=DFSA-AUD title='DFSA AUD Rulebook'
- `dfsa_cir_collective-investment-rules-cir-ver4001-26` — entity=DFSA code=DFSA-CIR title='DFSA CIR Rulebook'
- `dfsa_cob_conduct-business-module-cob-ver5001-26` — entity=DFSA code=DFSA-COB title='DFSA COB Rulebook'
- `dfsa_fer_fees-module-fer-ver3504-26` — entity=DFSA code=DFSA-FER title='DFSA FER Rulebook'
- `dfsa_gen_general-module-gen-ver7101-26` — entity=DFSA code=DFSA-GEN title='DFSA GEN Rulebook'
- `dfsa_glo_glossary-module-glo-ver6401-26` — entity=DFSA code=DFSA-GLO title='DFSA GLO Rulebook'
- `dfsa_ifr_islamic-finance-rules-ifr-ver2212-25` — entity=DFSA code=DFSA-IFR title='DFSA IFR Rulebook'
- `dfsa_mkt_markets-rules-mkt-ver2701-26` — entity=DFSA code=DFSA-MKT title='DFSA MKT Rulebook'
- `dfsa_pib_prudential-investment-insurance-intermediation-and-banking-module-pib-ver5201-26` — entity=DFSA code=DFSA-PIB title='DFSA PIB Rulebook'
- `dfsa_pin_prudential-insurance-business-module-pin-ver1804-23` — entity=DFSA code=DFSA-PIN title='DFSA PIN Rulebook'
- `dfsa_rec_recognition-rec-ver1305-24` — entity=DFSA code=DFSA-REC title='DFSA REC Rulebook'
- `dfsa_rep_representative-office-module-rep-ver1211-22` — entity=DFSA code=DFSA-REP title='DFSA REP Rulebook'
- `dfsa_rulebooks_fpr_dfsa_fpr_module` — entity=DFSA code=DFSA-FPR title='Dfsa Fpr Module'
- `dfsa_rulebooks_prs_dfsa_prs_module` — entity=DFSA code=DFSA-PRS title='Dfsa Prs Module'

### Local-only rows (sample, up to 20)

- `dfsa_s3_dfsa-afn` — entity=DFSA code=DFSA-AFN title='DFSA AFN Rulebook'
- `dfsa_s3_dfsa-ami` — entity=DFSA code=DFSA-AMI title='DFSA AMI Rulebook'
- `dfsa_s3_dfsa-aml` — entity=DFSA code=DFSA-AML title='DFSA AML Rulebook'
- `dfsa_s3_dfsa-aud` — entity=DFSA code=DFSA-AUD title='DFSA AUD Rulebook'
- `dfsa_s3_dfsa-cir` — entity=DFSA code=DFSA-CIR title='DFSA CIR Rulebook'
- `dfsa_s3_dfsa-cmc` — entity=DFSA code=DFSA-CMC title='DFSA CMC Rulebook'
- `dfsa_s3_dfsa-cob` — entity=DFSA code=DFSA-COB title='DFSA COB Rulebook'
- `dfsa_s3_dfsa-fer` — entity=DFSA code=DFSA-FER title='DFSA FER Rulebook'
- `dfsa_s3_dfsa-fpr` — entity=DFSA code=DFSA-FPR title='DFSA FPR Rulebook'
- `dfsa_s3_dfsa-gen` — entity=DFSA code=DFSA-GEN title='DFSA GEN Rulebook'
- `dfsa_s3_dfsa-glo` — entity=DFSA code=DFSA-GLO title='DFSA GLO Rulebook'
- `dfsa_s3_dfsa-ifr` — entity=DFSA code=DFSA-IFR title='DFSA IFR Rulebook'
- `dfsa_s3_dfsa-mkt` — entity=DFSA code=DFSA-MKT title='DFSA MKT Rulebook'
- `dfsa_s3_dfsa-pib` — entity=DFSA code=DFSA-PIB title='DFSA PIB Rulebook'
- `dfsa_s3_dfsa-pin` — entity=DFSA code=DFSA-PIN title='DFSA PIN Rulebook'
- `dfsa_s3_dfsa-prs` — entity=DFSA code=DFSA-PRS title='DFSA PRS Rulebook'
- `dfsa_s3_dfsa-pru` — entity=DFSA code=DFSA-PRU title='DFSA PRU Rulebook'
- `dfsa_s3_dfsa-rar` — entity=DFSA code=DFSA-RAR title='DFSA RAR Rulebook'
- `dfsa_s3_dfsa-rec` — entity=DFSA code=DFSA-REC title='DFSA REC Rulebook'
- `dfsa_s3_dfsa-rep` — entity=DFSA code=DFSA-REP title='DFSA REP Rulebook'

## Intersection mismatches (same source_key, different fields)

- **content_hash mismatch**: 106 rows (version drift — same source, different content)
- **source_entity mismatch**: 91 rows (classification drift)
- **source_url mismatch**: 0 rows (metadata drift — A5.C.1 work expected to surface here)

### content_hash mismatch sample

- `` — local 2026-03-21T08:47:39.074414+00:00, hetzner 2026-03-21T08:47:39.074414+00:00 — ''
- `20220826-thematic-review` — local 2026-03-21T08:49:50.264973+00:00, hetzner 2026-03-21T08:49:50.264973+00:00 — '20220826-Thematic-review'
- `2025_dear_seo_aml_letter_2025` — local 2026-03-21T08:49:28.421071+00:00, hetzner 2026-03-21T08:49:28.421071+00:00 — '2025 Dear SEO AML letter 2025'
- `code_of_market_conduct_(cmc)_ver04.311025` — local 2026-03-21T07:45:41.608328+00:00, hetzner 2026-03-21T07:45:41.608328+00:00 — 'Code of Market Conduct (CMC) VER04.311025'
- `dea_seo_letter_-_general_operations_02032026` — local 2026-03-21T08:49:15.017612+00:00, hetzner 2026-03-21T08:49:15.017612+00:00 — 'Dea SEO Letter - General Operations 02032026'
- `dear_seo_letter_(banks)_-_banking_sector_risk_assessments_20260210` — local 2026-03-21T08:49:19.275274+00:00, hetzner 2026-03-21T08:49:19.275274+00:00 — 'Dear SEO Letter (Banks) - Banking Sector Risk Assessments 20260210'
- `dear_seo_letter_banks_20250317_pru_data_final` — local 2026-03-21T08:49:41.120063+00:00, hetzner 2026-03-21T08:49:41.120063+00:00 — 'Dear SEO Letter Banks 20250317 PRU Data FINAL'
- `dear_seo_letter_countercyclical_buffer` — local 2026-03-21T08:49:38.407575+00:00, hetzner 2026-03-21T08:49:38.407575+00:00 — 'Dear SEO Letter Countercyclical Buffer'
- `dear_seo_letter_requirements_for_funds` — local 2026-03-21T08:49:32.055620+00:00, hetzner 2026-03-21T08:49:32.055620+00:00 — 'Dear SEO Letter requirements for funds'
- `fccp_fsra_-_fccp_-__notice_no._15_of_2026_-_cyber_risk_survey_findings_and_` — local 2026-03-21T08:58:59.194809+00:00, hetzner 2026-03-21T08:58:59.194809+00:00 — 'FSRA - FCCP -  Notice No. 15 of 2026 - Cyber Risk Survey Findings and Recommenda'
- `fccp_fsra_-_fccp_-__notice_no._22_of_2026_-_updates_to_information_technolo` — local 2026-03-21T08:59:00.397517+00:00, hetzner 2026-03-21T08:59:00.397517+00:00 — 'FSRA - FCCP -  Notice No. 22 of 2026 - Updates to Information Technology IT and '
- `fccp_fsra_-_fccp_-_notice_no._128_of_2025_-_cybercrime_prevention_-_protect` — local 2026-03-21T08:59:06.916967+00:00, hetzner 2026-03-21T08:59:06.916967+00:00 — 'FSRA - FCCP - Notice No. 128 of 2025 - Cybercrime Prevention - Protect your orga'
- `fccp_fsra_-_fccp_-_notice_no._12_of_2022_-_tin_collections` — local 2026-03-21T08:59:05.844396+00:00, hetzner 2026-03-21T08:59:05.844396+00:00 — 'FSRA - FCCP - Notice No. 12 of 2022 - TIN Collections'
- `fccp_fsra_-_fccp_-_notice_no._14_of_2022_-_interpretative_jurisdictional_ri` — local 2026-03-21T08:59:07.587749+00:00, hetzner 2026-03-21T08:59:07.587749+00:00 — 'FSRA - FCCP - Notice No. 14 of 2022 - Interpretative Jurisdictional Risk'
- `fccp_fsra_-_fccp_-_notice_no._14_of_2023_-_reminder_on_the_key_aml-tfs_fede` — local 2026-03-21T08:59:08.995748+00:00, hetzner 2026-03-21T08:59:08.995748+00:00 — 'FSRA - FCCP - Notice No. 14 of 2023 - Reminder on the key AML-TFS Federal Report'
- `fccp_fsra_-_fccp_-_notice_no._15_of_2023_-_rising_use_of_virtual_currencies` — local 2026-03-21T08:59:12.719423+00:00, hetzner 2026-03-21T08:59:12.719423+00:00 — 'FSRA - FCCP - Notice No. 15 of 2023 - Rising use of Virtual Currencies by Crimin'
- `fccp_fsra_-_fccp_-_notice_no._15_of_2024_-_cyber_security_council_alerts` — local 2026-03-21T08:59:13.707092+00:00, hetzner 2026-03-21T08:59:13.707092+00:00 — 'FSRA - FCCP - Notice No. 15 of 2024 - Cyber Security Council Alerts'
- `fccp_fsra_-_fccp_-_notice_no._165_of_2025_–_unlicensed_virtual_asset_activi` — local 2026-03-21T08:59:16.221370+00:00, hetzner 2026-03-21T08:59:16.221370+00:00 — 'FSRA - FCCP - Notice No. 165 of 2025 – Unlicensed Virtual Asset activities'
- `fccp_fsra_-_fccp_-_notice_no._16_of_2022_-_counter_proliferation_financing_` — local 2026-03-21T08:59:14.825367+00:00, hetzner 2026-03-21T08:59:14.825367+00:00 — 'FSRA - FCCP - Notice No. 16 of 2022 - Counter Proliferation Financing Guidance'
- `fccp_fsra_-_fccp_-_notice_no._172_of_2025_–_update_on_the_uae_federal_amlcf` — local 2026-03-21T08:59:17.522458+00:00, hetzner 2026-03-21T08:59:17.522458+00:00 — 'FSRA - FCCP - Notice No. 172 of 2025 – Update on the UAE Federal AMLCFT Legislat'

### source_entity mismatch sample

- `adgm_fsra_forms_AMS_Asset_Management_Supplement` — local=ADGM FSRA → hetzner=UNKNOWN — 'Ams Asset Management Supplement'
- `adgm_fsra_forms_BBS_Banking_Business_Supplement` — local=ADGM FSRA → hetzner=UNKNOWN — 'Bbs Banking Business Supplement'
- `adgm_fsra_forms_CIBF_Captive_Insurance_Business` — local=ADGM FSRA → hetzner=UNKNOWN — 'Cibf Captive Insurance Business'
- `adgm_fsra_forms_CIC_Change_in_Control` — local=ADGM FSRA → hetzner=UNKNOWN — 'Cic Change In Control'
- `adgm_fsra_forms_CRA_Credit_Rating_Agency` — local=ADGM FSRA → hetzner=UNKNOWN — 'Cra Credit Rating Agency'
- `adgm_fsra_forms_DAS_Dealing_Advisory_Supplement` — local=ADGM FSRA → hetzner=UNKNOWN — 'Das Dealing Advisory Supplement'
- `adgm_fsra_forms_FEQN_Exempt_Qualified_Fund_Notification` — local=ADGM FSRA → hetzner=UNKNOWN — 'Feqn Exempt Qualified Fund Notification'
- `adgm_fsra_forms_FFM_Foreign_Fund_Manager` — local=ADGM FSRA → hetzner=UNKNOWN — 'Ffm Foreign Fund Manager'
- `adgm_fsra_forms_FFN_Foreign_Fund_Notification` — local=ADGM FSRA → hetzner=UNKNOWN — 'Ffn Foreign Fund Notification'
- `adgm_fsra_forms_FMN_Marketing_Selling_Funds` — local=ADGM FSRA → hetzner=UNKNOWN — 'Fmn Marketing Selling Funds'
- `adgm_fsra_forms_FPP_Funds_Passporting_Notification` — local=ADGM FSRA → hetzner=UNKNOWN — 'Fpp Funds Passporting Notification'
- `adgm_fsra_forms_FPR_Public_Fund_Registration` — local=ADGM FSRA → hetzner=UNKNOWN — 'Fpr Public Fund Registration'
- `adgm_fsra_forms_FSPC_Cancel_Financial_Services_Permission` — local=ADGM FSRA → hetzner=UNKNOWN — 'Fspc Cancel Financial Services Permission'
- `adgm_fsra_forms_GIRA_General_Information_Regulated_Activities` — local=ADGM FSRA → hetzner=UNKNOWN — 'Gira General Information Regulated Activities'
- `adgm_fsra_forms_IBS_Insurance_Business_Supplement` — local=ADGM FSRA → hetzner=UNKNOWN — 'Ibs Insurance Business Supplement'
- `adgm_fsra_forms_IFBS_Islamic_Financial_Business` — local=ADGM FSRA → hetzner=UNKNOWN — 'Ifbs Islamic Financial Business'
- `adgm_fsra_forms_MKT_1-1_Waiver_Modification_Request` — local=ADGM FSRA → hetzner=UNKNOWN — 'Mkt 1 1 Waiver Modification Request'
- `adgm_fsra_forms_MKT_10-1_Quarterly_Cash_Report` — local=ADGM FSRA → hetzner=UNKNOWN — 'Mkt 10 1 Quarterly Cash Report'
- `adgm_fsra_forms_MKT_11-1_Mining_Reporting_Entities` — local=ADGM FSRA → hetzner=UNKNOWN — 'Mkt 11 1 Mining Reporting Entities'
- `adgm_fsra_forms_MKT_12-1_Petroleum_Reporting_Entities` — local=ADGM FSRA → hetzner=UNKNOWN — 'Mkt 12 1 Petroleum Reporting Entities'

## UNKNOWN entity audit

- Local UNKNOWN/empty-entity rows: 0
- Hetzner UNKNOWN/empty-entity rows: 57

### Hetzner UNKNOWN rows (full listing)

| id | source_key | rulebook_code | title | local_path | updated_at |
|---:|---|---|---|---|---|
| 2665 | `company_law_adgm_Schedule_of_F` | `COMP-LAW-SCHEDULE` | 'Schedule Of Fees 2025' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/Schedule` | 2026-04-03T07:31:31.445966+00:00 |
| 2666 | `company_law_adgm_Private_Ltd_N` | `COMP-LAW-PRIVATE_` | 'Private Ltd Non Financial' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/Private_` | 2026-04-03T07:31:31.719741+00:00 |
| 2667 | `company_law_adgm_Private_Ltd_R` | `COMP-LAW-PRIVATE_` | 'Private Ltd Rsc Non Financial' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/Private_` | 2026-04-03T07:31:32.007077+00:00 |
| 2668 | `company_law_adgm_Foundation_Re` | `COMP-LAW-FOUNDATI` | 'Foundation Registration' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/Foundati` | 2026-04-03T07:31:32.276730+00:00 |
| 2669 | `company_law_adgm_Foundation_Co` | `COMP-LAW-FOUNDATI` | 'Foundation Continuance' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/Foundati` | 2026-04-03T07:31:32.631515+00:00 |
| 2670 | `company_law_adgm_Branch_Financ` | `COMP-LAW-BRANCH_F` | 'Branch Financial And Non Financial Services' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/Branch_F` | 2026-04-03T07:31:32.917188+00:00 |
| 2671 | `company_law_adgm_LLP_Financial` | `COMP-LAW-LLP_FINA` | 'Llp Financial And Non Financial' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/LLP_Fina` | 2026-04-03T07:31:33.093656+00:00 |
| 2672 | `company_law_adgm_Guidance_Cont` | `COMP-LAW-GUIDANCE` | 'Guidance Continuance Into Adgm' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/Guidance` | 2026-04-03T07:31:33.412035+00:00 |
| 2673 | `company_law_adgm_Private_Ltd_R` | `COMP-LAW-PRIVATE_` | 'Private Ltd Retail' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/Private_` | 2026-04-03T07:31:33.636561+00:00 |
| 2674 | `company_law_adgm_LP_Financial_` | `COMP-LAW-LP_FINAN` | 'Lp Financial And Non Financial' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/LP_Finan` | 2026-04-03T07:31:33.823251+00:00 |
| 2675 | `adgm_fsra_forms_MKT_10-1_Quart` | `—` | 'Mkt 10 1 Quarterly Cash Report' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/MKT_10-1_` | 2026-04-03T07:31:34.166628+00:00 |
| 2676 | `adgm_fsra_forms_FFN_Foreign_Fu` | `—` | 'Ffn Foreign Fund Notification' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/FFN_Forei` | 2026-04-03T07:31:34.538921+00:00 |
| 2677 | `adgm_fsra_forms_DAS_Dealing_Ad` | `—` | 'Das Dealing Advisory Supplement' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/DAS_Deali` | 2026-04-03T07:31:34.990397+00:00 |
| 2678 | `adgm_fsra_forms_FFM_Foreign_Fu` | `—` | 'Ffm Foreign Fund Manager' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/FFM_Forei` | 2026-04-03T07:31:35.440343+00:00 |
| 2679 | `adgm_fsra_forms_CIBF_Captive_I` | `—` | 'Cibf Captive Insurance Business' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/CIBF_Capt` | 2026-04-03T07:31:36.418982+00:00 |
| 2680 | `adgm_fsra_forms_IBS_Insurance_` | `—` | 'Ibs Insurance Business Supplement' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/IBS_Insur` | 2026-04-03T07:31:36.753946+00:00 |
| 2681 | `adgm_fsra_forms_CRA_Credit_Rat` | `—` | 'Cra Credit Rating Agency' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/CRA_Credi` | 2026-04-03T07:31:37.306849+00:00 |
| 2682 | `adgm_fsra_forms_CIC_Change_in_` | `—` | 'Cic Change In Control' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/CIC_Chang` | 2026-04-03T07:31:37.561511+00:00 |
| 2683 | `adgm_fsra_forms_MKT_11-1_Minin` | `—` | 'Mkt 11 1 Mining Reporting Entities' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/MKT_11-1_` | 2026-04-03T07:31:37.766202+00:00 |
| 2684 | `adgm_fsra_forms_MKT_9-1_Restri` | `—` | 'Mkt 9 1 Restriction Agreement' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/MKT_9-1_R` | 2026-04-03T07:31:38.086191+00:00 |
| 2685 | `adgm_fsra_forms_Remote_Member_` | `—` | 'Remote Member Recognition' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/Remote_Me` | 2026-04-03T07:31:38.289964+00:00 |
| 2686 | `adgm_fsra_forms_MKT_12-1_Petro` | `—` | 'Mkt 12 1 Petroleum Reporting Entities' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/MKT_12-1_` | 2026-04-03T07:31:38.575563+00:00 |
| 2687 | `adgm_fsra_forms_PRS-1_Principa` | `—` | 'Prs 1 Principal Representative Status' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/PRS-1_Pri` | 2026-04-03T07:31:39.018670+00:00 |
| 2688 | `adgm_fsra_forms_WM_Waivers_Mod` | `—` | 'Wm Waivers Modifications' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/WM_Waiver` | 2026-04-03T07:31:39.335260+00:00 |
| 2689 | `adgm_fsra_forms_MKT_2-4_Admiss` | `—` | 'Mkt 2 4 Admission Securities Official List' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/MKT_2-4_A` | 2026-04-03T07:31:39.431606+00:00 |
| 2690 | `adgm_fsra_forms_MKT_1-1_Waiver` | `—` | 'Mkt 1 1 Waiver Modification Request' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/MKT_1-1_W` | 2026-04-03T07:31:39.565306+00:00 |
| 2691 | `adgm_fsra_forms_VCFM_Venture_C` | `—` | 'Vcfm Venture Capital Fund Manager' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/VCFM_Vent` | 2026-04-03T07:31:40.156706+00:00 |
| 2692 | `adgm_fsra_forms_MKT_4.6-1_Appr` | `—` | 'Mkt 4.6 1 Approval Prospectus' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/MKT_4.6-1` | 2026-04-03T07:31:40.272787+00:00 |
| 2693 | `adgm_fsra_forms_PFP_Private_Fi` | `—` | 'Pfp Private Financing Platform' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/PFP_Priva` | 2026-04-03T07:31:40.471930+00:00 |
| 2694 | `adgm_fsra_forms_FSPC_Cancel_Fi` | `—` | 'Fspc Cancel Financial Services Permission' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/FSPC_Canc` | 2026-04-03T07:31:40.664512+00:00 |
| 2695 | `adgm_fsra_forms_RO_Representat` | `—` | 'Ro Representative Office' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/RO_Repres` | 2026-04-03T07:31:41.006823+00:00 |
| 2696 | `adgm_fsra_forms_FPR_Public_Fun` | `—` | 'Fpr Public Fund Registration' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/FPR_Publi` | 2026-04-03T07:31:41.551664+00:00 |
| 2697 | `adgm_fsra_forms_VA_Notificatio` | `—` | 'Va Notification Accepted Status' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/VA_Notifi` | 2026-04-03T07:31:41.720017+00:00 |
| 2698 | `adgm_fsra_forms_GIRA_General_I` | `—` | 'Gira General Information Regulated Activities' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/GIRA_Gene` | 2026-04-03T07:31:42.783390+00:00 |
| 2699 | `adgm_fsra_forms_MKT_4.6-2_Paym` | `—` | 'Mkt 4.6 2 Payment Form' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/MKT_4.6-2` | 2026-04-03T07:31:42.840397+00:00 |
| 2700 | `adgm_fsra_forms_FMN_Marketing_` | `—` | 'Fmn Marketing Selling Funds' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/FMN_Marke` | 2026-04-03T07:31:43.031357+00:00 |
| 2701 | `adgm_fsra_forms_MKT_4-7_Approv` | `—` | 'Mkt 4 7 Approval Offer Document' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/MKT_4-7_A` | 2026-04-03T07:31:43.192324+00:00 |
| 2702 | `adgm_fsra_forms_FPP_Funds_Pass` | `—` | 'Fpp Funds Passporting Notification' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/FPP_Funds` | 2026-04-03T07:31:43.457043+00:00 |
| 2703 | `adgm_fsra_forms_BBS_Banking_Bu` | `—` | 'Bbs Banking Business Supplement' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/BBS_Banki` | 2026-04-03T07:31:44.136257+00:00 |
| 2704 | `adgm_fsra_forms_RBK-1_Key_Indi` | `—` | 'Rbk 1 Key Individuals Application' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/RBK-1_Key` | 2026-04-03T07:31:44.811734+00:00 |
| 2705 | `adgm_fsra_forms_AMS_Asset_Mana` | `—` | 'Ams Asset Management Supplement' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/AMS_Asset` | 2026-04-03T07:31:45.174073+00:00 |
| 2706 | `adgm_fsra_forms_VAS_Virtual_As` | `—` | 'Vas Virtual Assets Application' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/VAS_Virtu` | 2026-04-03T07:31:46.051327+00:00 |
| 2707 | `adgm_fsra_forms_IFBS_Islamic_F` | `—` | 'Ifbs Islamic Financial Business' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/IFBS_Isla` | 2026-04-03T07:31:46.609291+00:00 |
| 2708 | `adgm_fsra_forms_FEQN_Exempt_Qu` | `—` | 'Feqn Exempt Qualified Fund Notification' | `/Users/oliver/ADGM/adgm-corpus/raw/adgm/fsra_forms/FEQN_Exem` | 2026-04-03T07:31:47.178944+00:00 |
| 2718 | `vara_rulebooks_custody-service` | `—` | 'Custody Services Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/custody-se` | 2026-04-03T07:32:46.538364+00:00 |
| 2719 | `vara_rulebooks_company-ruleboo` | `—` | 'Company Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/company-ru` | 2026-04-03T07:32:46.577719+00:00 |
| 2720 | `vara_rulebooks_exchange-servic` | `—` | 'Exchange Services Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/exchange-s` | 2026-04-03T07:32:46.603320+00:00 |
| 2721 | `vara_rulebooks_lending-and-bor` | `—` | 'Lending And Borrowing Services Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/lending-an` | 2026-04-03T07:32:46.619327+00:00 |
| 2722 | `vara_rulebooks_compliance-and-` | `—` | 'Compliance And Risk Management Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/compliance` | 2026-04-03T07:32:46.657630+00:00 |
| 2723 | `vara_rulebooks_virtual-asset-i` | `—` | 'Virtual Asset Issuance Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/virtual-as` | 2026-04-03T07:32:46.682006+00:00 |
| 2724 | `vara_rulebooks_advisory-servic` | `—` | 'Advisory Services Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/advisory-s` | 2026-04-03T07:32:46.693012+00:00 |
| 2725 | `vara_rulebooks_va-transfer-and` | `—` | 'Va Transfer And Settlement Services Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/va-transfe` | 2026-04-03T07:32:46.705805+00:00 |
| 2726 | `vara_rulebooks_market-conduct-` | `—` | 'Market Conduct Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/market-con` | 2026-04-03T07:32:46.720790+00:00 |
| 2727 | `vara_rulebooks_va-management-a` | `—` | 'Va Management And Investment Services Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/va-managem` | 2026-04-03T07:32:46.732925+00:00 |
| 2728 | `vara_rulebooks_technology-and-` | `—` | 'Technology And Information Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/technology` | 2026-04-03T07:32:46.752612+00:00 |
| 2729 | `vara_rulebooks_broker-dealer-s` | `—` | 'Broker Dealer Services Rulebook' | `/Users/oliver/ADGM/adgm-corpus/raw/vara/rulebooks/broker-dea` | 2026-04-03T07:32:46.767911+00:00 |
| 2730 | `company_law_adgm_model_article` | `COMP-LAW-MODEL_AR` | 'Model Articles Rules 2015' | `/Users/oliver/ADGM/adgm-corpus/raw/company_law/adgm/model_ar` | 2026-04-03T07:32:46.802550+00:00 |

## Root cause taxonomy

The blanket "a/b/c reconciliation" framing in the M26 register entry pre-dates this discovery and is too coarse. The 369-row affected surface decomposes into **four distinct root causes**, each with its own fix shape. Treating them as one blanket reconciliation would mis-prescribe — Hetzner-as-truth is correct for RC2/RC4 but wrong for RC1, etc.

### RC1 — DFSA `source_key` shape mismatch (~20 rows)

Hetzner has 20+ DFSA rows under an **older keying convention** (e.g. `dfsa_aml_anti-money-laundering-...-ver30...`); local has the same DFSA modules under a **newer convention** (e.g. `dfsa_s3_dfsa-aml`). Same documents — different `source_key` shape — so they appear as set-difference (local-only AND Hetzner-only) instead of as intersection-mismatch. ~20 of the 81 Hetzner-only rows + ~20 of the 34 local-only rows are this same pattern. Surfaces as ghost duplicates inflating both side-difference counts.

**Fix shape:** one-shot migration table mapping `old_source_key` → `new_source_key` on Hetzner; single SQL UPDATE pass. Resolves the apparent set-difference without any actual document movement.

### RC2 — `content_hash` recomputation lag (~106 rows)

A5.D landed in Wave B Session 1 (15 May 2026) — `write_rulebook` now derives `content_hash` from `full_text` (canonical) and overrides any scraper-provided hash. The 106 intersection content_hash mismatches are likely rows that local has re-processed under A5.D (full_text-derived hash) but Hetzner still has the older PDF-bytes-derived hashes from before A5.D was deployed. Same content, different hash convention.

**Fix shape:** selective recompute on Hetzner — for the 106 mismatched rows, recompute `content_hash` from local's stored `full_text` (the canonical formula) and UPDATE on Hetzner. Validates A5.D as the canonical formula by making Hetzner conform without touching content.

### RC3 — Hetzner-only `UNKNOWN` entity rows (57 rows)

57 rows on Hetzner with `source_entity` in (NULL, '', 'UNKNOWN'); zero on local. `max_updated` ~2026-04-03 — settled state, not recent timer misfires. Either (a) production-timer ingests that failed entity classification (and were never cleaned up), (b) docs that local never had at all (and were dropped from a dev rebuild). Local doesn't classify any row as UNKNOWN.

**Fix shape:** heuristic classification first (rulebook_code prefix + local_path pattern → source_entity), manual audit of the residue. Likely some rows are legitimately classifiable; others may be production garbage candidates for `is_current=0` flip.

### RC4 — True entity drift (small)

A few entities have **genuine row-count delta** that isn't explained by RC1/RC2/RC3:
- **EL_SALVADOR**: +3 on Hetzner (16 → 19); max_updated 2026-04-03 on both — but Hetzner has 3 extra docs
- **BVI_FSC**: +2 on Hetzner (27 → 29); max_updated identical 2026-04-15
- **FSRA**: +75 on Hetzner (657 → 732) — much larger; needs separate investigation (could be mostly RC1 keying-convention residue or genuine timer-driven ingests)
- **ADGM family** (ADGM −5, ADGM FSRA −34, ADGM_COURTS −23, ADGM_RA −23, UAE_FEDERAL −5): local-heavy, mostly from 13 May Wave A/B re-ingests that haven't propagated

**Fix shape:** per-row investigation — read each title, decide if a Hetzner-extra row is a real new doc OR a duplicate of an existing local doc under different `source_key` (in which case it's RC1, not RC4). Small per-entity counts (5 each ex-FSRA) allow manual review.

## Reconciliation strategy — six decisions (D1-D6)

Strategy is decomposed into per-root-cause decisions rather than one blanket choice. Each grounded in the actual finding above.

### D1 — DFSA `source_key` migration (RC1)

- **(a)** Build mapping table from set-diff sample analysis (manual pairing of old↔new keys based on title + content_hash); single SQL UPDATE pass on Hetzner.
- **(b)** Skip migration; treat as "Hetzner has older rows under different keys; new convention superseded them" — let A5.C bulk apply work around it.

**Recommendation: (a)** — key migration is one-shot SQL work and resolves ~20 ghost-duplicate rows cleanly. (b) is technical debt that compounds at next drift audit.

### D2 — `content_hash` recomputation (RC2)

- **(a)** Re-run A5.D recomputation logic on Hetzner via SSH — for each of the 106 mismatched rows, recompute content_hash from full_text and UPDATE.
- **(b)** Selective re-run: only for rows where local hash matches the A5.D formula and Hetzner doesn't (catches the A5.D-lag specifically; skips genuinely-different content rows that need other treatment).
- **(c)** Skip; accept hash drift as informational only (content is the same; hash difference doesn't break product).

**Recommendation: (b)** — selective approach is correct work, and confirms A5.D defense-in-depth catches what it should.

### D3 — `UNKNOWN` entity classification (RC3)

- **(a)** Heuristic classification: map rulebook_code prefix + local_path pattern → source_entity. Apply via Python script. 57 rows.
- **(b)** Manual audit: read each row's title + local_path, classify in a focused 30-min session.
- **(c)** Hybrid: heuristic first, manual review of residue.

**Recommendation: (c)** — start with high-confidence heuristic patterns; manually classify whatever doesn't match. Best precision-recall trade.

### D4 — True entity drift (RC4)

- **(a)** Pull Hetzner-only rows to local via INSERT (with section-table doc_id re-keying); preserve both sides going forward.
- **(b)** Investigate per-row before deciding: read each title, decide if it's a real new doc or a duplicate of an existing local doc under a different `source_key`.

**Recommendation: (b)** — 5 rows is small enough to verify; ensures we don't propagate ghost duplicates that should have surfaced as RC1.

### D5 — Apply timing

- **(x)** This session: extend 1-2 hours, run D1-D4 applies serially.
- **(y)** Follow-on session: re-brief against authorised D1-D4 decisions; apply session designed against the four-root-cause structure.

**Recommendation: (y)** — each apply needs careful script design (D1 mapping table, D2 selective recomputation, D3 heuristic+audit, D4 per-row review). Bundling into this session bypasses the design discipline that surfaced this restructuring in the first place.

### D6 — Sync model going forward

- **1.** Hetzner timers stay; periodic local-from-Hetzner sync.
- **2.** Hetzner timers disabled; local-only writes, deploy via SSH SQL.
- **3.** Two-way merge protocol with timestamps.

**Recommendation:** defer to architectural memo session. Decision doesn't block applies; can be made after parity achieved.

## Apply prerequisite: section-table coordination

Pulling Hetzner-only docs to local requires re-keying `sections.doc_id` (and likely `citations.source_section_id`) because doc IDs are AUTOINCREMENT per-DB and won't match across sides. Apply session must handle this — typically by inserting the doc on local (gets new id), then bulk-updating sections + citations to reference the new id. Non-trivial; deserves its own focused session per session scoping discipline.

## Sync model going forward

(To be decided in design discussion. Options surfaced for follow-on memo:

1. Hetzner timers stay on; local is dev-mirror; periodic sync Hetzner-to-local (cron or manual).
2. Hetzner timers disabled; only local writes; deploys propagate to Hetzner via remote SSH SQL.
3. Two-way merge protocol with timestamps.

## Next steps

1. Strategy decision via design gate
2. UNKNOWN entity handling decision
3. Follow-on session: build reconciliation script with section-table doc_id re-keying logic; apply with backups on both sides; verify parity
4. Sync model architectural decision (separate memo)