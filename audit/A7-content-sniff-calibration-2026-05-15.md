# Content-Sniff Signature Calibration — Discovery Memo

**Date:** 2026-05-15
**Session:** Wave A Session 3a (read-only discovery)
**Source DB:** `/Users/oliver/ADGM/adgm-corpus/corpus.db`
**Tuples enumerated:** 137

## Format

For each `(source_entity, rulebook_code)` tuple with `is_current=1` rows:
- 1-3 representative `full_text` samples (first 500 chars each)
- Proposed signature substring (longest common prefix heuristic, trimmed)
- Backfill dry-run: count of rows containing the signature in first 500 chars
- Risk flag if signature confidence is low

Signatures are PROPOSED for review. Session 3b applies them as enforcement.


## ADGM

### ADGM / `ADGM-CR` (1 rows)

**Representative sample (doc id=2587, title=`ADGM Companies Regulations 2020`):**

```
Entire Section | Rulebook
Skip to main content
ADGM LEGAL FRAMEWORK
Back
Custom print
Print
Search
View Current PDF
Companies Regulations 2020
Regulations to make provision for the formation and registration of companies in the Abu Dhabi Global Market.
Date of Enactment: 29 April 2020
The Board of Directors of the Abu Dhabi Global Market, in exercise of its powers under Article 6(1) of
Law No. 4 o...
```

**Proposed signature:** `Entire Section | Rulebook\nSkip to main content\nADGM LEGAL FRAMEWORK\nBack\nCustom`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM / `ADGM-CR-MAR` (1 rows)

**Representative sample (doc id=2588, title=`ADGM Companies Regulations (Model Articles) Rules 2015`):**

```
Entire Section | Rulebook
Skip to main content
ADGM LEGAL FRAMEWORK
Back
Custom print
Print
Search
View Current PDF
Companies Regulations (Model Articles) Rules 2015
Date of Adoption: 12 April 2015
The Board of Directors of Abu Dhabi Global Market, in exercise of the powers conferred by
section 17
of the Companies Regulations 2015, hereby makes the following Rules: —
1. Citation and commencement
(...
```

**Proposed signature:** `Entire Section | Rulebook\nSkip to main content\nADGM LEGAL FRAMEWORK\nBack\nCustom`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM / `ADGM-CRS` (1 rows)

**Representative sample (doc id=159, title=`Adgm1547 19312 Ver142023`):**

```
COMMON REPORTING STANDARD REGULATIONS 2017
(CONSOLIDATED VERSION)

TABLE OF CONTENTS
Part 1 Introduction ................................................................................................................................ 1
Part 2 Role and Powers of the Regulatory Authority ...................................................................... 3
Part 3 Reporting and Record keeping .......
```

**Proposed signature:** `COMMON REPORTING STANDARD REGULATIONS 2017\n(CONSOLIDATED VERSION)\n\nTABLE OF CONT`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM / `ADGM-FATCA` (1 rows)

**Representative sample (doc id=216, title=`Adgm1547 24944 Ver012022`):**

```
FOREIGN ACCOUNT TAX COMPLIANCE REGULATIONS 2022

TABLE OF CONTENTS
Part 1 Introduction ................................................................................................................. 1
Part 2 Role and Powers of the Regulatory Authority ............................................................. 2
Part 3 Record keeping ...............................................................
```

**Proposed signature:** `FOREIGN ACCOUNT TAX COMPLIANCE REGULATIONS 2022\n\nTABLE OF CONTENTS\nPart 1 Introd`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM / `NOTICES` (3 rows)

**Representative sample (doc id=65, title=`Notice Of Publication Rules Made By The Registrar File 1`):**

```
NOTICE OF PUBLICATION OF RULES
1. The CEO of the Registration Authority of the Abu Dhabi Global Market (the "Registrar") enacted
the regulations set out in paragraph 3 and annexed to this notice on 15 June 2015 (the "Rules").
2. The Registrar has directed the Rules to be published and accordingly the Rules are hereby
published on 15 June 2015.
3. The Rules are:
(a) Companies Regulations (Applicati...
```

**Additional samples (2):** doc ids 154, 210

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/3 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix



## ADGM FSRA

### ADGM FSRA / `ADGM-FSRA-F` (71 rows)

**Representative sample (doc id=2619, title=`Restriction Agreement (MKT Form 9-1)`):**

```
Restriction Agreement (MKT 9-1)
MKT Form 9 – 1
Restriction Agreement
FSRA – MKT9-1 v.1.2_03/22
Page 1 of 7
Restriction Agreement (MKT 9-1)
Contents
1) Restriction Agreement ....................................................................................................................... 3
FSRA – MKT9-1 v.1.2_03/22
Page 2 of 7
Restriction Agreement (MKT 9-1)
1
Restriction Agreement
RESTRICTION...
```

**Additional samples (4):** doc ids 2620, 2621, 2622, 2623

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/71 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix



## ADGM_COURTS

### ADGM_COURTS / `<NULL>` (287 rows)

**Representative sample (doc id=71, title=`Adgm1547 19064 Ver2025`):**

```
ADGM Courts Rules of Conduct 2016

Table of Contents
1. Scope and Objective ....................................................................................................... 1
2. Interpretations ............................................................................................................... 1
3. Fundamental ethical duties ..........................................................
```

**Additional samples (4):** doc ids 80, 94, 95, 110

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/287 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix



## ADGM_RA

### ADGM_RA / `<NULL>` (5 rows)

**Representative sample (doc id=1933, title=`Consultation Paper No 5 Of 2015 Employment Regulations`):**

```
CONSULTATION PAPER
NO 5 OF 2015
6 JANUARY 2015
EMPLOYMENT REGULATIONS
1

WHY ARE WE ISSUING THIS PAPER?
1. The Board of Directors (the "Board") of Abu Dhabi Global Market ("ADGM") have issued this Consultation
Paper to invite public comment on the Board's proposals to adopt new employment regulations for
ADGM to be called the Employment Regulations (the "Regulations"). A proposed draft of the Regu...
```

**Additional samples (4):** doc ids 1941, 2030, 2100, 2184

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/5 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix


### ADGM_RA / `ADGM-CLR` (1 rows)

**Representative sample (doc id=2747, title=`Commercial Licensing Regulations 2015`):**

```
‹ 46. Manager 47. Short title, extent and commencement ›
PART 5: GENERAL
View Current PDF
47. Short title, extent and commencement
‹ 46. Manager 47. Short title, extent and commencement ›

‹ PART 1: LICENSING OF CONTROLLED ACTIVITIES 2. Controlled activities ›
1. The general prohibition
View Current PDF

(1) No person may carry on a controlled activity in or from the Abu Dhabi Global Market, or pu...
```

**Proposed signature:** `‹ 46. Manager 47. Short title, extent and commencement ›\nPART 5: GENERAL\nView Cu`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `ADGM-DPR` (2 rows)

**Representative sample (doc id=208, title=`Adgm1547 22829 Ver1032020`):**

```
Coronavirus (COVID-19) – Implications for Data Protection
Frequently Asked Questions
Registration Authority
Office of Data Protection
March 2020

Introduction to Abu Dhabi Global Market
Abu Dhabi Global Market (ADGM) is a broad based international financial centre, established
pursuant to Abu Dhabi Law No. 4 of 2013 in the Emirate of Abu Dhabi. With its own civil and
commercial laws based on the E...
```

**Additional samples (1):** doc ids 2749

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/2 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix


### ADGM_RA / `ADGM-ER-2024` (1 rows)

**Representative sample (doc id=2797, title=`ADGM Employment Regulations 2024`):**

```
EMPLOYMENT REGULATIONS 2024

TABLE OF CONTENTS
PART 1: HIRING EMPLOYEES ................................................................................ 1
PART 2: PART-TIME EMPLOYEES AND REMOTE EMPLOYEES .......................... 5
PART 3: PROTECTION OF WAGES ........................................................................ 6
PART 4: WORKING TIME AND LEAVE ....................................
```

**Proposed signature:** `EMPLOYMENT REGULATIONS 2024\n\nTABLE OF CONTENTS\nPART 1: HIRING EMPLOYEES ........`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `ADGM-ER-2024-EAO` (1 rows)

**Representative sample (doc id=2799, title=`ADGM EAO Guidance on ER 2024 (Feb 2025)`):**

```
Employment Affairs Office –
Guidance on the ADGM
Employment Regulations 2024
Employment in Abu Dhabi Global Market
Published: 18 February 2025

Introduction
Abu Dhabi Global Market (“ADGM”) is an international financial centre established in the Emirate
of Abu Dhabi pursuant to the UAE Federal Decree No. 15 of 2013 and Abu Dhabi Law No. 4 of
2013, as amended (“ADGM Law”). With its own civil and co...
```

**Proposed signature:** `Employment Affairs Office –\nGuidance on the ADGM\nEmployment Regulations 2024\nEmp`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `ADGM-IR` (1 rows)

**Representative sample (doc id=2750, title=`Insolvency Regulations 2022`):**

```
‹ Chapter 1 — General Chapter 2 — Provisions applicable to receivership and administrative receivership ›
152. Appointment and powers of receivers and administrative receivers
Versions
(3 versions)

View Current PDF
(1) Where a Company grants a person powers contained in an instrument to appoint an Office-holder to get in and sell any part of its property and to apply the proceeds in reduction of ...
```

**Proposed signature:** `‹ Chapter 1 — General Chapter 2 — Provisions applicable to receivership and admi`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `ADGM-RA-F` (32 rows)

**Representative sample (doc id=2592, title=`Branch – Financial and Non-Financial Services Registration Guide`):**

```
Registration Authority
Checklist – Company Set-up
Confidential
REGISTRATION OF BRANCH OF A FOREIGN COMPANY – STANDARD REQUIREMENTS
(FINANCIAL and NON-FINANCIAL FIRMS)
Requirements
In-principle approval from ADGM Financial Services
FSRA Application Process
Regulatory Authority
(Mandatory requirement prior to submission of the
online application form if business activity is financial)
OR
Business Pl...
```

**Additional samples (4):** doc ids 2593, 2594, 2595, 2596

**Proposed signature:** `Registration Authority`

**Backfill dry-run:** 17/32 rows contain signature in first 500 chars

**Risk:** ⚠️ CALIBRATION GAP — signature found in 17/32 rows (15 would fail the gate)


### ADGM_RA / `ADGM-RA-RULES` (11 rows)

**Representative sample (doc id=72, title=`Commercial Licensing Regulations 2015 (Controlled Activities) Rules 2021`):**

```
COMMERCIAL LICENSING REGULATIONS 2015 (CONTROLLED ACTIVITIES) RULES
20182021
Date of Adoption: 23 April 2018 17 March 2021
The Board of Directors of the Abu Dhabi Global Market, in implementation of the provisions of
section 2(1) of the Commercial Licensing Regulations 2015, hereby makes the following
rules:-
1. Citation, commencement and interpretation
(1) These Rules may be cited as the Commerci...
```

**Additional samples (4):** doc ids 82, 88, 142, 153

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/11 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix


### ADGM_RA / `ADGM-WB-2024` (1 rows)

**Representative sample (doc id=2798, title=`ADGM Whistleblower Protection Regulations 2024`):**

```
WHISTLEBLOWER PROTECTION REGULATIONS 2024

TABLE OF CONTENTS
Part 1: Citation, Entry Into Force, Definitions And Interpretation.................................. 1
Part 2: Whistleblower Protection ...................................................................................... 2
Part 3: Powers Of The Registrar .....................................................................................
```

**Proposed signature:** `WHISTLEBLOWER PROTECTION REGULATIONS 2024\n\nTABLE OF CONTENTS\nPart 1: Citation, E`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-BRANCH_FN` (1 rows)

**Representative sample (doc id=2670, title=`Branch Financial And Non Financial Services`):**

```
Registration Authority
Checklist – Company Set-up

REGISTRATION OF BRANCH OF A FOREIGN COMPANY – STANDARD REQUIREMENTS
(FINANCIAL and NON-FINANCIAL FIRMS)
Requirements
In-principle approval from ADGM Financial Services
FSRA Application Process
Regulatory Authority
(Mandatory requirement prior to submission of the
online application form if business activity is financial)
OR
Business Plan www.regis...
```

**Proposed signature:** `Registration Authority\nChecklist – Company Set-up\n\nREGISTRATION OF BRANCH OF A F`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-FEES_2025` (1 rows)

**Representative sample (doc id=2665, title=`Schedule Of Fees 2025`):**

```
Registration Authority
Overview of Fees 2025
Version Date: January 2025

Contents
Introduction ................................................................................................................................................................ 3
Available Payment Methods .......................................................................................................................
```

**Proposed signature:** `Registration Authority\nOverview of Fees 2025\nVersion Date: January 2025\n\nContent`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-FOUNDATION_CONT` (1 rows)

**Representative sample (doc id=2669, title=`Foundation Continuance`):**

```
Registration Authority
Checklist – Foundation Continuance to ADGM

CONTINUANCE OF FOUNDATION TO ADGM – STANDARD REQUIREMENTS
Requirements for Continuance
Standard Requirements
Useful Links
Legal Personality
Foundations Regulations
- Confirmation that the Foundation has legal
personality in the original jurisdiction. This
eligibility criteria must be met for continuance to
ADGM.
Declaration
Foundat...
```

**Proposed signature:** `Registration Authority\nChecklist – Foundation Continuance to ADGM\n\nCONTINUANCE O`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-FOUNDATION_REG` (1 rows)

**Representative sample (doc id=2668, title=`Foundation Registration`):**

```
Registration Authority
Checklist – Foundation Registration

REGISTRATION OF FOUNDATION – STANDARD REQUIREMENTS
FOUNDATION (NON-EXEMPT)
Standard Requirements
Useful Links
Foundation Purpose Statement
Foundation Application
Process
- Please attach a statement from the applicant’s
company service provider to clarify the purpose of
registering the foundation in ADGM, the objects of
the foundation, the...
```

**Proposed signature:** `Registration Authority\nChecklist – Foundation Registration\n\nREGISTRATION OF FOUN`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-GUIDANCE_CONT_ADGM` (1 rows)

**Representative sample (doc id=2672, title=`Guidance Continuance Into Adgm`):**

```
Registration Authority
Checklist – Company Set-up

1. Important information
A body corporate which is incorporated outside the Abu Dhabi Global Market may apply for continuance in
ADGM if it is authorised by the law of the jurisdiction under which it is incorporated. Additionally, to check
the entity’s eligibility, please answer the below questions.
2. Check entity’s eligibility
No.
☐ Yes
Pursuant...
```

**Proposed signature:** `Registration Authority\nChecklist – Company Set-up\n\n1. Important information\nA bo`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-LLP_FN` (1 rows)

**Representative sample (doc id=2671, title=`Llp Financial And Non Financial`):**

```
Registration Authority
Checklist – Limited Liability Partnership

INCORPORATION OF LIMITED LIABILITY PARTNERSHIP – STANDARD
REQUIREMENTS
Standard Requirements
Useful Links
In-principle approval from ADGM Financial Services
FSRA Application Process
Regulatory Authority
(Mandatory requirement prior to submission of the
online application form if business activity is financial).
OR
Business Plan for ...
```

**Proposed signature:** `Registration Authority\nChecklist – Limited Liability Partnership\n\nINCORPORATION`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-LP_FN` (1 rows)

**Representative sample (doc id=2674, title=`Lp Financial And Non Financial`):**

```
Registration Authority
Checklist – Limited Partnership Registration

REGISTRATION OF LIMITED PARTNERSHIP – STANDARD REQUIREMENTS
Limited Partnership Registration
Standard Requirements
Useful Links
In-principle approval from ADGM Financial Services
FSRA Application Process
Regulatory Authority
(Mandatory requirement prior to submission of the
online application form if business activity is financia...
```

**Proposed signature:** `Registration Authority\nChecklist – Limited Partnership Registration\n\nREGISTRATIO`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-MODEL_ARTICLES` (1 rows)

**Representative sample (doc id=2730, title=`Model Articles Rules 2015`):**

```
Back

Custom print

Print

Search

View Current PDF

Companies Regulations (Model Articles) Rules 2015Date of Adoption: 12 April 2015The Board of Directors of Abu Dhabi Global Market, in exercise of the powers conferred bysection 17of the Companies Regulations 2015, hereby makes the following Rules: —

Companies Regulations (Model Articles) Rules 2015

Date of Adoption: 12 April 2015

The Board of...
```

**Proposed signature:** `Back\n\nCustom print\n\nPrint\n\nSearch\n\nView Current PDF\n\nCompanies Regulations (Mode`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-PRIV_LTD_NF` (1 rows)

**Representative sample (doc id=2666, title=`Private Ltd Non Financial`):**

```
Registration Authority
Checklist – Company Set-up

INCORPORATION OF COMPANY – STANDARD REQUIREMENTS
Standard Requirements
Useful Links
Prepare a business plan.
Suggested information to be included in the business plan
The business plan is fundamental to the application process, and
will be used by the ADGM Registration Authority (ADGM RA) to
form decisions about the applicant, and applicant’s read...
```

**Proposed signature:** `Registration Authority\nChecklist – Company Set-up\n\nINCORPORATION OF COMPANY – ST`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-PRIV_LTD_RETAIL` (1 rows)

**Representative sample (doc id=2673, title=`Private Ltd Retail`):**

```
Registration Authority
Checklist – Company Set-up

INCORPORATION / REGISTRATION OF COMPANY – STANDARD REQUIREMENTS
PRIVATE COMPANY LIMITED BY SHARES – RETAIL
Standard Requirements
Useful Links
Lease Agreement with the landlord
Business Activities in line with the store concept
submitted to Gulf Related
Choose a company name. www.registration.adgm.com
- Search if the company name is still available...
```

**Proposed signature:** `Registration Authority\nChecklist – Company Set-up\n\nINCORPORATION / REGISTRATION`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### ADGM_RA / `COMP-LAW-PRIV_LTD_RSC_NF` (1 rows)

**Representative sample (doc id=2667, title=`Private Ltd Rsc Non Financial`):**

```
Registration Authority
Checklist – Company Set-up

INCORPORATION OF COMPANY – STANDARD REQUIREMENTS
PRIVATE COMPANY LIMITED BY SHARES (RSC) – NON-FINANCIAL
Private Company Limited by Shares (RSC) - Non-Financial Services - New
Format_Updated Fees
Page 2 of 11

Requirements
Useful Links
Choose business activities. Setting up in ADGM -
Permitted Activities
- Refer: List of permitted activities avail...
```

**Proposed signature:** `Registration Authority\nChecklist – Company Set-up\n\nINCORPORATION OF COMPANY – ST`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars



## BVI_FSC

### BVI_FSC / `BVI-AML` (1 rows)

**Representative sample (doc id=2570, title=`Anti Money Laundering And Terrorist Financing Code Of Practice`):**

```
LAW OF Terrorist Financing Code of Practice 21
VIRGIN ISLANDS
Revision Date: 1 Jan 2020 [Statutory Instrument]
ANTI-MONEY LAUNDERING AND TERRORIST
FINANCING CODE OF PRACTICE
ARRANGEMENT OF SECTIONS
PRELIMINARY
SECTION
1. Citation
2. Interpretation
3. Objectives
4. General application and exception
4A. Application to charities, etc.
5. Compliance with this Code
PART I
DUTIES OF THE AGENCY AND THE C...
```

**Proposed signature:** `LAW OF Terrorist Financing Code of Practice 21\nVIRGIN ISLANDS\nRevision Date: 1 J`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-AML-AMD-2022` (1 rows)

**Representative sample (doc id=2739, title=`Anti Money Laundering Amendment Regulations 2022`):**

```
VIRGIN ISLANDS
ANTI-MONEY LAUNDERING (AMENDMENT) REGULATIONS,
2022
ARRANGEMENT OF REGULATIONS
REGULATION
1. Citation and commencement
2. Regulation 2 amended
3. Regulation 3 amended
4. Regulation 4 amended
5. Regulation 6 amended
6. Regulation 7 amended
7. Regulation 9 amended
8. Regulation 10 amended
9. Regulation 13 amended
10. Regulation 14 amended
11. Regulation 16 amended
12. Regulation 17 am...
```

**Proposed signature:** `VIRGIN ISLANDS\nANTI-MONEY LAUNDERING (AMENDMENT) REGULATIONS,\n2022\nARRANGEMENT O`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-AML-AMD-2023` (1 rows)

**Representative sample (doc id=2738, title=`Anti Money Laundering Amendment Regulations 2023`):**

```
ANTI-MONEY LAUNDERING (AMENDMENT) REGULATIONS,
ARRANGEMENT OF REGULATIONS
REGULATION
1. Citation and commencement
2. Regulation 2 amended
3. Regulation 6 amended
4. Regulation 13 amended
5. Regulation 16 amended

STATUTORY INSTRUMENT 2023 NO. 17
PROCEEDS OF CRIMINAL CONDUCT ACT
(REVISED EDITION 2020)
Anti-money Laundering (Amendment) Regulations, 2023
[Gazetted 1st March, 2023]
The Cabinet, in exe...
```

**Proposed signature:** `ANTI-MONEY LAUNDERING (AMENDMENT) REGULATIONS,\nARRANGEMENT OF REGULATIONS\nREGULA`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-AML-CODE-AMD-2022` (1 rows)

**Representative sample (doc id=2743, title=`Anti Money Laundering And Terrorist Financing Amendment Code Of Practice 2022`):**

```
VIRGIN ISLANDS
ANTI-MONEY LAUNDERING AND TERRORIST FINANCING
(AMENDMENT) CODE OF PRACTICE, 2022
ARRANGEMENT OF SECTIONS
Section
1… Citation and commencement
2… Section 2 amended
3… Section 3 amended
4… Section 4 amended
5… Section 4A amended
6… Section 5 revoked and substituted
7… Section 6 amended
8… Section 7 amended
9… Section 8 amended
10… Section 9 amended
11… Section 10 amended
12… Section 1...
```

**Proposed signature:** `VIRGIN ISLANDS\nANTI-MONEY LAUNDERING AND TERRORIST FINANCING\n(AMENDMENT) CODE OF`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-AML-CODE-AMD-2023` (1 rows)

**Representative sample (doc id=2742, title=`Anti Money Laundering And Terrorist Financing Amendment Code Of Practice 2023`):**

```
VIRGIN ISLANDS
ANTI-MONEY LAUNDERING AND TERRORIST FINANCING
(AMENDMENT) CODE OF PRACTICE, 2023
ARRANGEMENT OF SECTIONS
SECTION
1. Citation and commencement
2. Section 2 amended
3. Section 4 amended
4. Section 4A amended
5. Section 9 amended
6. Section 11 amended
7. Section 12 amended
8. Section 13 amended
9. Section 16 amended
10. Section 17 amended
11. Section 18 amended
12. Section 19 amended
1...
```

**Proposed signature:** `VIRGIN ISLANDS\nANTI-MONEY LAUNDERING AND TERRORIST FINANCING\n(AMENDMENT) CODE OF`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-AMLR` (1 rows)

**Representative sample (doc id=2571, title=`Anti Money Laundering Regulations`):**

```
LAW OF Anti-Money Laundering Regulations 3
VIRGIN ISLANDS
Revision Date: 1 Jan 2020 [Statutory Instrument]
ANTI-MONEY LAUNDERING REGULATIONS
ARRANGEMENTOF REGULATIONS
REGULATION
1. Short title
2. Interpretation
3. General requirements
4. Identification procedures in relation to new and continuing business
relationships
5. Establishing and maintaining verification procedures
6. Exceptions to identi...
```

**Proposed signature:** `LAW OF Anti-Money Laundering Regulations 3\nVIRGIN ISLANDS\nRevision Date: 1 Jan 2`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-BCA` (1 rows)

**Representative sample (doc id=2756, title=`Bvi Business Companies Act Schedules`):**

```
VIRGIN ISLANDS
BVI BUSINESS COMPANIES ACT
Revised Edition
showing the law as at 1 January 2020
This is a revised edition of the law, prepared by the Law Revision Commissioner
under the authority of the Law Revision Act 2014.
This edition contains a consolidation of the following laws—
Page
BVI BUSINESS COMPANIES ACT 3
Act 16 of 2004 .. in force 1 January 2005
Amended by Acts: 26 of 2005 .. in forc...
```

**Proposed signature:** `VIRGIN ISLANDS\nBVI BUSINESS COMPANIES ACT\nRevised Edition\nshowing the law as at`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-BCA-S` (1 rows)

**Representative sample (doc id=2586, title=`BVI Business Companies Act 2004 — Schedules 1 and 2 (Model Forms)`):**

```
VIRGIN ISLANDS
BVI BUSINESS COMPANIES ACT
Revised Edition
showing the law as at 1 January 2020
This is a revised edition of the law, prepared by the Law Revision Commissioner
under the authority of the Law Revision Act 2014.
This edition contains a consolidation of the following laws—
Page
BVI BUSINESS COMPANIES ACT 3
Act 16 of 2004 .. in force 1 January 2005
Amended by Acts: 26 of 2005 .. in forc...
```

**Proposed signature:** `VIRGIN ISLANDS\nBVI BUSINESS COMPANIES ACT\nRevised Edition\nshowing the law as at`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-BO-GUIDE` (1 rows)

**Representative sample (doc id=2735, title=`Bvifsc Beneficial Ownership Guidance`):**

```
Revised as of 2nd January 2026
1 | Page

Table of Contents
ACRONYMS ................................................................................................................. 4
DEFINITIONS ............................................................................................................... 4
1. INTRODUCTION .............................................................................
```

**Proposed signature:** `Revised as of 2nd January 2026\n1 | Page\n\nTable of Contents\nACRONYMS ............`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-BOSS` (1 rows)

**Representative sample (doc id=2741, title=`Beneficial Ownership Secure Search System Act`):**

```
VIRGIN ISLANDS
BENEFICIAL OWNERSHIP
SECURE SEARCH SYSTEM ACT
Revised Edition
showing the law as at 1 January 2020
This is a revised edition of the law, prepared by the Law Revision Commissioner
under the authority of the Law Revision Act 2014.
This edition contains a consolidation of the following laws—
Page
BENEFICIAL OWNERSHIP SECURE SEARCH SYSTEM ACT 3
Act 15 of 2017 .. in force 30 June 2017
Am...
```

**Proposed signature:** `VIRGIN ISLANDS\nBENEFICIAL OWNERSHIP\nSECURE SEARCH SYSTEM ACT\nRevised Edition\nsho`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-BTCA` (1 rows)

**Representative sample (doc id=2572, title=`Banks And Trust Companies Act`):**

```
VIRGIN ISLANDS
BANKS AND TRUST COMPANIES ACT
Revised Edition
showing the law as at 1 January 2020
This is a revised edition of the law, prepared by the Law Revision Commissioner
under the authority of the Law Revision Act 2014.
This edition contains a consolidation of the following laws—
Page
BANKS AND TRUST COMPANIES ACT 3
Act 9 of 1990 .. in force 27 September 1990
Amended by Acts: 2 of 1995 .. ...
```

**Proposed signature:** `VIRGIN ISLANDS\nBANKS AND TRUST COMPANIES ACT\nRevised Edition\nshowing the law as`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-CMA` (1 rows)

**Representative sample (doc id=2574, title=`Company Management Act 1990`):**

```
NO. 8 of 1990
VIRGIN ISLANDS
The Company Management Act, 1990
Arrangement of Sections
Sections
1. Short title
PART 1
Preliminary
2. Interpretation
PART II
Licences
3. Requirement of licence.
4. Application for licence.
5. Fees.
6. Duration of licence
7. Exemptions from licences
8. Existing businesses.
9. Notification of Change in particulars of Licencee.
10. Capitalization of Company Management Co...
```

**Proposed signature:** `NO. 8 of 1990\nVIRGIN ISLANDS\nThe Company Management Act, 1990\nArrangement of Sec`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-CTA` (1 rows)

**Representative sample (doc id=2736, title=`Counter Terrorism Act 2021`):**

```
No. 33 of 2021
VIRGIN ISLANDS
COUNTER-TERRORISM ACT, 2021
ARRANGEMENT OF SECTIONS
Section
PART I
PRELIMINARY
1. Short title and commencement.
2. Interpretation.
3. Governor may delegate power.
4. Act binds the Crown.
PART II
TERRORIST OFFENCES
5. Terrorist act.
6. Carrying out and facilitating terrorist acts.
7. Terrorist bombing.
8. Financing of terrorism.
9. Prohibition on dealing with property ...
```

**Proposed signature:** `No. 33 of 2021\nVIRGIN ISLANDS\nCOUNTER-TERRORISM ACT, 2021\nARRANGEMENT OF SECTION`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-DPA` (1 rows)

**Representative sample (doc id=2746, title=`Act No. 3 Of 2021 Data Protection Act, 2021`):**

```
No. 3 of 2021
VIRGIN ISLANDS
DATA PROTECTION ACT, 2021
ARRANGEMENT OF SECTIONS
Section
PART I
PRELIMINARY
1. Short title and commencement.
2. Interpretation.
3. Objects of Act.
4. Application of Act.
5. Saving of certain laws.
6. Act binds the Crown.
PART II
PRIVACY AND DATA PROTECTION PRINCIPLES
7. General Principle.
8. Notice and Choice Principle.
9. Disclosure Principle.
10. Security Principle....
```

**Proposed signature:** `No. 3 of 2021\nVIRGIN ISLANDS\nDATA PROTECTION ACT, 2021\nARRANGEMENT OF SECTIONS\nS`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-ESA` (1 rows)

**Representative sample (doc id=2745, title=`Economic Substance Companies And Ltd Partnerships Act`):**

```
VIRGIN ISLANDS
ECONOMIC SUBSTANCE (COMPANIES AND
LIMITED PARTNERSHIPS) ACT
Revised Edition
showing the law as at 1 January 2020
This is a revised edition of the law, prepared by the Law Revision Commissioner
under the authority of the Law Revision Act 2014.
This edition contains a consolidation of the following laws—
Page
ECONOMIC SUBSTANCE (COMPANIES AND LIMITED PARTNERSHIPS) ACT 3
Act 12 of 2018...
```

**Proposed signature:** `VIRGIN ISLANDS\nECONOMIC SUBSTANCE (COMPANIES AND\nLIMITED PARTNERSHIPS) ACT\nRevis`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-FMSA` (1 rows)

**Representative sample (doc id=2580, title=`Financing And Money Services Act 2009`):**

```
No. 9 of 2009
VIRGIN ISLANDS

FINANCING AND MONEY
SERVICES ACT, 2009

ARRANGEMENT OF SECTIONS

Section
PRELIMINARY

.. Short title and commencement.

.. Interpretation.

.. Exemption from application of this Act.

.. Definition of “financing agreement”, “lease” and “financing lease”.
.. Definition of “financing business”.

.. Meaning of “money services business”.

AnkYNE

PARTI

REGULATION AND SUP...
```

**Proposed signature:** `No. 9 of 2009\nVIRGIN ISLANDS\n\nFINANCING AND MONEY\nSERVICES ACT, 2009\n\nARRANGEMEN`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-FSCA` (1 rows)

**Representative sample (doc id=2575, title=`Financial Services Commission Act`):**

```
VIRGIN ISLANDS
FINANCIAL SERVICES COMMISSION ACT
Revised Edition
showing the law as at 1 January 2020
This is a revised edition of the law, prepared by the Law Revision Commissioner
under the authority of the Law Revision Act 2014.
This edition contains a consolidation of the following laws—
Page
FINANCIAL SERVICES COMMISSION ACT 3
Act 12 of 2001 .. in force 1 January 2002 (S.I. 51/2001)
Amended b...
```

**Proposed signature:** `VIRGIN ISLANDS\nFINANCIAL SERVICES COMMISSION ACT\nRevised Edition\nshowing the law`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-MFA` (1 rows)

**Representative sample (doc id=2576, title=`Mutual Funds Act`):**

```
No. of 1996
VIRGIN ISLANDS
MUTUAL FUNDS ACT, 1996
ARRANGEMENT OF SECTIONS
Section
Preliminary
1. Short title and commencement.
2. Interpretation.
PART I
Administration
3. Appointments.
4. Delegation of power.
5. Annual report.
6. Records of the Registrar.
7. Mutual Funds Advisory Committee.
PART II
Public Funds
8. Registration.
9. Application for registration.
10. Application for consent to be reg...
```

**Proposed signature:** `No. of 1996\nVIRGIN ISLANDS\nMUTUAL FUNDS ACT, 1996\nARRANGEMENT OF SECTIONS\nSectio`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-MFR` (1 rows)

**Representative sample (doc id=2577, title=`Mutual Funds Regulations 2010`):**

```
VIRGIN ISLANDS
MUTUAL FUNDS REGULATIONS, 2010
ARRANGEMENT OF REGULATIONS
Regulation
PRELIMINARY PROVISIONS
1. Citation and commencement.
2. Interpretation.
3. Fund administration services.
PART 1
PRIVATE AND PROFESSIONAL FUNDS
Application for recognition
4. Application for recognition as private or professional fund.
5. Matters required to be prescribed, professional investor and professional fund...
```

**Proposed signature:** `VIRGIN ISLANDS\nMUTUAL FUNDS REGULATIONS, 2010\nARRANGEMENT OF REGULATIONS\nRegulat`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-PCCA` (1 rows)

**Representative sample (doc id=2744, title=`Proceeds Of Criminal Conduct Act`):**

```
VIRGIN ISLANDS
PROCEEDS OF CRIMINAL CONDUCT ACT
Revised Edition
showing the law as at 1 January 2020
This is a revised edition of the law, prepared by the Law Revision Commissioner
under the authority of the Law Revision Act 2014.
This edition contains a consolidation of the following laws—
Page
PROCEEDS OF CRIMINAL CONDUCT ACT 3
Act 5 of 1997 .. in force 2 January 1998 (S.I. 59/1997)
Amended by A...
```

**Proposed signature:** `VIRGIN ISLANDS\nPROCEEDS OF CRIMINAL CONDUCT ACT\nRevised Edition\nshowing the law`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-PFA` (1 rows)

**Representative sample (doc id=2740, title=`Proliferation Financing Prohibition Act`):**

```
No. 15 of 2009
VIRGIN ISLANDS
PROLIFERATION FINANCING (PROHIBITION) ACT, 2009
ARRANGEMENT OF SECTIONS
Section
PRELIMINARY
1. Short title.
2. Interpretation.
DIRECTIONS
3. Power to give a direction.
4. Persons to whom a direction may be given.
5. Conditions for giving a direction.
REQUIREMENTS IN RELATION TO DIRECTIONS
6. Imposing requirements.
7. Customer due diligence.
8. Ongoing monitoring.
9. S...
```

**Proposed signature:** `No. 15 of 2009\nVIRGIN ISLANDS\nPROLIFERATION FINANCING (PROHIBITION) ACT, 2009\nAR`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-RC` (1 rows)

**Representative sample (doc id=2578, title=`Regulatory Code 2009`):**

```
VIRGIN ISLANDS
REGULATORY CODE, 2009
ARRANGEMENT OF SECTIONS
Section
PRELIMINARY PROVISIONS
1. Citation and commencement.
2. Definitions.
3. Commission may determine undertaking to be parent.
4. Definition of “senior officer”, “senior manager” and “senior management”.
5. General interpretative provisions.
6. Application of the Code.
PART I
PRINCIPLES FOR BUSINESS
7. Application of this Part.
8. Hi...
```

**Proposed signature:** `VIRGIN ISLANDS\nREGULATORY CODE, 2009\nARRANGEMENT OF SECTIONS\nSection\nPRELIMINARY`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-REGS` (1 rows)

**Representative sample (doc id=2589, title=`Investment Business (Approved Managers) Regulations 2012 (S.I. 2012 No. 54)`):**

```
VIRGIN ISLANDS
INVESTMENT BUSINESS (APPROVED MANAGERS) REGULATIONS, 2012
ARRANGEMENT OF REGULATIONS
Regulation
1… Citation and commencement.
2… Interpretation.
3… Application of these Regulations.
4… Application for approval as an investment manager.
5… Required information.
6… Fees.
7… Decision by the Commission.
8… Effect of approval.
9… Functions that may be performed.
10.. Restrictions in rela...
```

**Proposed signature:** `VIRGIN ISLANDS\nINVESTMENT BUSINESS (APPROVED MANAGERS) REGULATIONS, 2012\nARRANGE`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-SIBA` (1 rows)

**Representative sample (doc id=2579, title=`Securities And Investment Business Act 2010`):**

```
No. 2 of 2010
VIRGIN ISLANDS
SECURITIES AND INVESTMENT BUSINESS ACT, 2010
ARRANGEMENT OF SECTIONS
Section
PRELIMINARY PROVISIONS
1. Short title and commencement.
2. Interpretation.
3. Meaning of “investment activity” and “investment business”.
PART I
INVESTMENT BUSINESS
Unauthorised investment business
4. Prohibition on unauthorised investment business.
Licensing
5. Categories of, and restrictions...
```

**Proposed signature:** `No. 2 of 2010\nVIRGIN ISLANDS\nSECURITIES AND INVESTMENT BUSINESS ACT, 2010\nARRANG`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-VASP-AML-GUIDE` (1 rows)

**Representative sample (doc id=2733, title=`Vasp Aml Cft Guidance`):**

```
2023
Virtual Assets Service Providers
Guide to the Prevention of
Money Laundering, Terrorist
Financing and Proliferation
Financing
APPROVED BY THE BOARD OF COMMISSIONERS – 26/1/23
ISSUED BY FINANCIAL SERVICES COMMISSION – 31/1/23
PUBLISHED - 1/2/23
COMMENCEMENT DATE – 1/2/23

Contents
1. Introduction .....................................................................................................
```

**Proposed signature:** `2023\nVirtual Assets Service Providers\nGuide to the Prevention of\nMoney Launderin`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-VASP-TRAVEL` (1 rows)

**Representative sample (doc id=2734, title=`Vasp Travel Guidance`):**

```
VASP
TRAVEL RULE
GUIDANCE

Introduction
and Context
The Financial Action Task Force (FATF) introduced
the ‘Travel Rule’ in 2019 by way of a revision to
Recommendation 15 to extend anti-money
laundering, counter terrorist financing and counter-
proliferation financing obligations to virtual assets
(VA) and Virtual Assets Services Providers (VASPs).
The amendment to the recommendation required
count...
```

**Proposed signature:** `VASP\nTRAVEL RULE\nGUIDANCE\n\nIntroduction\nand Context\nThe Financial Action Task Fo`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### BVI_FSC / `BVI-VASPA` (1 rows)

**Representative sample (doc id=2737, title=`Virtual Assets Service Providers Act 2022`):**

```
No. 17 of 2022
VIRGIN ISLANDS
VIRTUAL ASSETS SERVICE PROVIDERS ACT, 2022
ARRANGEMENT OF SECTIONS
SECTION
PART I
PRELIMINARY
1. Short title and commencement
2. Interpretation
3. Application and prohibition
4. Powers of the Agency and the Commission
PART II
REGISTRATION REQUIREMENTS FOR VASPS
5. Prohibition against providing or engaging in transactions involving virtual
assets
6 . Application for re...
```

**Proposed signature:** `No. 17 of 2022\nVIRGIN ISLANDS\nVIRTUAL ASSETS SERVICE PROVIDERS ACT, 2022\nARRANGE`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars



## DFSA

### DFSA / `<NULL>` (1 rows)

**Representative sample (doc id=2428, title=`Supervisory Guidelines on Assessing the Suitability of Crypto Tokens`):**

```
Supervisory Guidelines on Assessing the Suitability of Crypto Tokens

Clickhereto view Supervisory Guidelines in PDF format.

Introduction

1. This document sets out guidelines to facilitate aPerson’s assessment of the suitability of aCrypto Tokenunder GEN Rule3A.2.1(2)(a). It communicates theDFSA’s expectations as to how aPersonwill typically seek to achieve compliance with relevant requirements ...
```

**Proposed signature:** `Supervisory Guidelines on Assessing the Suitability of Crypto Tokens\n\nClickheret`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-AFN` (1 rows)

**Representative sample (doc id=2812, title=`DFSA AFN Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesSourcebook ModulesApplication Forms and Notices Module (AFN) [VER52/11-22]Code of Market Conduct (CMC) [VER4/11-22]Regulatory Policy and Process Sourcebook (RPP) April 2022 EditionNotices of UpdatesArchiveCall ...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-AMI` (1 rows)

**Representative sample (doc id=2813, title=`DFSA AMI Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Part 1 IntroductionPart 2 Application and AuthorisationPart 3 Licensi...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-AML` (1 rows)

**Representative sample (doc id=2814, title=`DFSA AML Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]AML 1 IntroductionAML 2 Overview and Purpose of the ModuleAML 3 Interpretation and TerminologyAML 4 Applying a Risk-Bas...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-AUD` (1 rows)

**Representative sample (doc id=2815, title=`DFSA AUD Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Part 1 IntroductionPart 2 Registere...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-CIR` (1 rows)

**Representative sample (doc id=2816, title=`DFSA CIR Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-CMC` (1 rows)

**Representative sample (doc id=2817, title=`DFSA CMC Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesSourcebook ModulesApplication Forms and Notices Module (AFN) [VER52/11-22]Code of Market Conduct (CMC) [VER4/11-22]CMC 1 IntroductionCMC 2 Market Manipulation and FraudCMC 3 Dissemination of False or Misleading...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-COB` (1 rows)

**Representative sample (doc id=2818, title=`DFSA COB Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-FER` (1 rows)

**Representative sample (doc id=2819, title=`DFSA FER Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-FPR` (1 rows)

**Representative sample (doc id=2820, title=`DFSA FPR Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-GEN` (1 rows)

**Representative sample (doc id=2821, title=`DFSA GEN Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-GLO` (1 rows)

**Representative sample (doc id=2822, title=`DFSA GLO Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-IFR` (1 rows)

**Representative sample (doc id=2823, title=`DFSA IFR Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-MKT` (1 rows)

**Representative sample (doc id=2824, title=`DFSA MKT Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-PIB` (1 rows)

**Representative sample (doc id=2825, title=`DFSA PIB Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-PIN` (1 rows)

**Representative sample (doc id=2826, title=`DFSA PIN Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-PRS` (1 rows)

**Representative sample (doc id=2827, title=`DFSA PRS Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-PRU` (1 rows)

**Representative sample (doc id=2828, title=`DFSA PRU Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesSourcebook ModulesApplication Forms and Notices Module (AFN) [VER52/11-22]Code of Market Conduct (CMC) [VER4/11-22]PRU IntroductionPRU 1 Instructional Guidelines for PIB FormsPRU 2 PIB FormsPRU 3 Instructional ...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-RAR` (1 rows)

**Representative sample (doc id=2829, title=`DFSA RAR Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-REC` (1 rows)

**Representative sample (doc id=2830, title=`DFSA REC Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-REP` (1 rows)

**Representative sample (doc id=2831, title=`DFSA REP Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### DFSA / `DFSA-TKO` (1 rows)

**Representative sample (doc id=2832, title=`DFSA TKO Rulebook`):**

```
Dubai Financial Services Authority (DFSA)

Dubai Financial Services Authority (DFSA)LawsRecognised Jurisdictions and FundsDeclaration NoticesFinancial Markets TribunalArchiveRulebook ModulesAnti-Money Laundering, Counter-Terrorist Financing and Sanctions Module (AML) [VER30/04-26]Authorised Market Institutions (AMI) [VER30/01-26]Auditor Module (AUD) [VER10/01-26]Conduct of Business Module (COB) [V...
```

**Proposed signature:** `Dubai Financial Services Authority (DFSA)\n\nDubai Financial Services Authority (D`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars



## DIFC

### DIFC / `<NULL>` (5 rows)

**Representative sample (doc id=2423, title=`Markets Law`):**

```
Markets Law

Consolidated Version of theMarkets LawDIFC Law No. 1 of 2012which was enacted and came into force on 5 July 2012and was subsequently amended by :•DIFC Laws Amendment Law,DIFC Law No. 2 of 2013,on 5 January 2014; and•DIFC Laws Amendment Law,DIFC Law No.1 of 2014,on 21 August 2014.•DIFC Laws Amendment Law,DIFC Law No.2 of 2021,on 12 April 2021.•DIFC Laws Amendment Law,DIFC Law No.6 of 2...
```

**Additional samples (4):** doc ids 2424, 2425, 2426, 2427

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/5 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix


### DIFC / `DIFC-CL` (1 rows)

**Representative sample (doc id=2656, title=`DIFC Companies Law No. 5 of 2018 (Consolidated March 2022)`):**

```
COMPANIES LAW
DIFC LAW NO. 5 OF 2018
Consolidated Version
(March 2022)
As amended by
DIFC Laws Amendment Law
DIFC Law No. 2 of 2022
COMPANIES LAW
CONTENTS
Part 1 : GENERAL .................................................................................................................................................... 1
1. Title and repeal ............................................................
```

**Proposed signature:** `COMPANIES LAW\nDIFC LAW NO. 5 OF 2018\nConsolidated Version\n(March 2022)\nAs amende`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars



## DIFC_COURTS

### DIFC_COURTS / `<NULL>` (1066 rows)

**Representative sample (doc id=464, title=`Difc Bailii 2013 Sct 004`):**

```
Claim No.

THE DUBAI INTERNATIONAL FINANCIAL CENTRE
COURTSCourt

In the name of His Highness Sheikh Mohammad Bin Rashid Al Maktoum,
RulerRulerof Dubai

IN THE SMALL CLAIMS
TRIBUNALTribunalOF
DIFC COURTSDIFC Courts

BEFORE SCT
JUDGEJudgeSHAMLAN AL SAWALEHI

BETWEEN

DAISY

Claimant

and

(1) DALE

(2) DALTON

Defendants

Hearing: 4 July 2013

Judgment: 22 July 2013

JUDGMENT OF SCT JUDGE SHAMLAN AL...
```

**Additional samples (4):** doc ids 465, 466, 468, 469

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/1066 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix



## EL_SALVADOR

### EL_SALVADOR / `SV-AML` (1 rows)

**Representative sample (doc id=2381, title=`Ley Especial para la Prevención del Lavado de Dinero (Decreto 426, 2025)`):**

```
DECRETO No. 426
LA ASAMBLEA LEGISLATIVA DE LA REPÚBLICA DE EL SALVADOR,
CONSIDERANDO:
I. Que de conformidad con el Art. 2 inciso 1º de la Constitución de la República, toda persona tiene
derecho a la vida, a la integridad física y moral, a la libertad, a la seguridad, al trabajo, a la propiedad
y posesión, y a ser protegida en la conservación y defensa de éstos.
II. Que mediante Decreto Legislativ...
```

**Proposed signature:** `DECRETO No. 426\nLA ASAMBLEA LEGISLATIVA DE LA REPÚBLICA DE EL SALVADOR,\nCONSIDER`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-AML-GUIDE` (1 rows)

**Representative sample (doc id=2385, title=`CNAD AML/CFT Compliance Guide [English]`):**

```
GuideforMoneyLaunderingandTerroristFinancingRiskManagement
fortheDigitalAssetsindustry
In order to provide specific guidelines for Digital Asset Service Providers(DASPs)regardingthe
application ofarticles21lettero)oftheDigitalAssetIssuanceLaw(DAIL),19oftheDigitalAsset
Service Providers Regulation, and other applicable regulations for the management of Money
Laundering, Terrorist Financing, and Pro...
```

**Proposed signature:** `GuideforMoneyLaunderingandTerroristFinancingRiskManagement\nfortheDigitalAssetsin`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-ANNUAL` (1 rows)

**Representative sample (doc id=2386, title=`CNAD Annual Report 2023-2024`):**

```
Superando
Expectativas
DE
CERO A
LÍDERES
MUNDIALES
EN LA INDUSTRIA DE
ACTIVOS DIGITALES
2023 - 2024
Informe Anual de actividades 2023-2024 de la Comisión
Nacional de Activos Digitales. El Salvador, América
Central.

Índice
General
02 - 07 38 - 41
I Bienvenida del Presidente y V Registro Público
Director Ejecutivo de la Comisión
Nacional de Activos Digitales Registro Público del ecosistema de 38
ac...
```

**Proposed signature:** `Superando\nExpectativas\nDE\nCERO A\nLÍDERES\nMUNDIALES\nEN LA INDUSTRIA DE\nACTIVOS DI`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-BTC` (1 rows)

**Representative sample (doc id=2342, title=`Ley Bitcoin (Decreto Legislativo No. 57, 2021)`):**

```
DECRETO N° 57
LA ASAMBLEA LEGISLATIVA DE LA REPÚBLICA DE EL SALVADOR,
CONSIDERANDO:
I. Que de conformidad al artículo 102 de la Constitución de la República, el Estado está en la obligación
de fomentar y proteger la iniciativa privada, generando las condiciones necesarias para acrecentar la
riqueza nacional en beneficio del mayor número de habitantes.
II. Que bajo el Decreto Legislativo n.° 201, d...
```

**Proposed signature:** `DECRETO N° 57\nLA ASAMBLEA LEGISLATIVA DE LA REPÚBLICA DE EL SALVADOR,\nCONSIDERAN`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-CC` (1 rows)

**Representative sample (doc id=2591, title=`Código de Comercio de El Salvador (Decreto 671, 1970 — ed. 2008)`):**

```
DECRETOS LEYES Y REGLAMENTOS DE EL SALVADOR
Raíz
Código de Comercio No. 671
CÓDIGO DE COMERCIO
Decreto Legislativo No. 671 del 8 de mayo de 1970,
Publicado en el Diario Oficial No. 140, Tomo No. 228 del 31 de julio de 1970.
LA ASAMBLEA LEGISLATIVA DE LA REPUBLICA DE EL SALVADOR,
En uso de sus facultades constitucionales, a iniciativa del Presidente de la República por medio del Ministro de
Justici...
```

**Proposed signature:** `DECRETOS LEYES Y REGLAMENTOS DE EL SALVADOR\nRaíz\nCódigo de Comercio No. 671\nCÓDI`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-CNAD-DOCS` (1 rows)

**Representative sample (doc id=2569, title=`CNAD Documentation Library — Reference Page`):**

```
<!doctype html>
<html lang="en-US">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="profile" href="https://gmpg.org/xfn/11">
	<meta name='robots' content='index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1' />
<link rel="alternate" href="https://cnad.gob.sv/documentation-library/" hreflang="en" />
<link rel=...
```

**Proposed signature:** `<!doctype html>\n<html lang="en-US">\n<head>\n	<meta charset="UTF-8">\n	<meta name="`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-CNAD-FRAMEWORK` (1 rows)

**Representative sample (doc id=2568, title=`CNAD Legal Framework — Reference Page`):**

```
<!doctype html>
<html lang="en-US">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="profile" href="https://gmpg.org/xfn/11">
	<meta name='robots' content='index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1' />
<link rel="alternate" href="https://cnad.gob.sv/documentation-library/legal-framework/" hreflang="e...
```

**Proposed signature:** `<!doctype html>\n<html lang="en-US">\n<head>\n	<meta charset="UTF-8">\n	<meta name="`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-DASP` (1 rows)

**Representative sample (doc id=2389, title=`CNAD DASP Regulation [English]`):**

```
Non official translation. For reference only.
THE NATIONAL COMMISSION OF DIGITAL ASSETS
CONSIDERING:
1. That by means of Legislative Decree No. 643 dated January 11, 2023, published
in the Official Gazette No. 653, Volume No. 438, dated January 24 of the same
month and year, the Law of Issuance of Digital Assets of El Salvador was
issued.;
2. That by means of Art. 6 of said Law, the National Commi...
```

**Proposed signature:** `Non official translation. For reference only.\nTHE NATIONAL COMMISSION OF DIGITAL`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-ISS` (1 rows)

**Representative sample (doc id=2388, title=`CNAD Issuer Registration Regulation [English]`):**

```
Non official translation. For reference only.
THE NATIONAL COMMISSION OF DIGITAL ASSETS
CONSIDERING:
1. That by means of Legislative Decree No. 643 dated January eleventh, 2023, published in the
Official Gazette No.653, Volume No. 438, of the 24th of that same month and year, the Law
of Issuance of Digital Assets of El Salvador was issued;
2. That by means of Art. 6 of said Law, the National Commi...
```

**Proposed signature:** `Non official translation. For reference only.\nTHE NATIONAL COMMISSION OF DIGITAL`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-LBAN` (1 rows)

**Representative sample (doc id=2373, title=`Ley de Bancos Cooperativos y Sociedades de Ahorro y Crédito`):**

```
ASAMBLEA LEGISLATIVA - REPUBLICA DE EL SALVADOR 1
____________________________________________________________________
DECRETO No. 849.-
LA ASAMBLEA LEGISLATIVA DE LA REPUBLICA DE EL SALVADOR,
CONSIDERANDO:
I.- Que para fortalecer el desarrollo y la integración financiera del país, es necesario
mejorar el acceso y disponibilidad de los servicios financieros en todas las
actividades de las comunida...
```

**Proposed signature:** `ASAMBLEA LEGISLATIVA - REPUBLICA DE EL SALVADOR 1\n______________________________`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-LEAD` (1 rows)

**Representative sample (doc id=2378, title=`Digital Asset Issuance Law (Decreto 643, 2023) [English]`):**

```
San Salvador, november 14th, 2022
Secretaries of the Honorable
Legislative Assembly
Secretaries:
Complying with special instructions from the President of the Republic, I hereby submit to this
Honorable Legislative Assembly, by your honorable means, based on the provisions of the
second paragraph of Article 133 of the Constitution of the Republic, having been granted the
Initiative of Law to the d...
```

**Proposed signature:** `San Salvador, november 14th, 2022\nSecretaries of the Honorable\nLegislative Assem`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-LEAD24` (1 rows)

**Representative sample (doc id=2341, title=`Reformas a la Ley de Emisión de Activos Digitales (2024)`):**

```
1
DECRETO N.° 781
LA ASAMBLEA LEGISLATIVA DE LA REPÚBLICA DE EL SALVADOR,
CONSIDERANDO:
I. Que el artículo 101 de la Constitución señala que el Estado promoverá el desarrollo
económico y social mediante el incremento de la producción, la productividad y la
racional utilización de los recursos, y, además, fomentará a los diversos sectores de
la producción, y, por tanto, debe armonizar las leyes exi...
```

**Proposed signature:** `1\nDECRETO N.° 781\nLA ASAMBLEA LEGISLATIVA DE LA REPÚBLICA DE EL SALVADOR,\nCONSID`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-LMV` (1 rows)

**Representative sample (doc id=2374, title=`Ley del Mercado de Valores`):**

```
Superintendencia del Sistema Financiero
DECRETO Nº 809.-
LA ASAMBLEA LEGISLATIVA DE LA REPÚBLICA DE EL SALVADOR,
CONSIDERANDO:
I. Que el desarrollo económico nacional requiere de un Sistema Financiero moderno
que promueva el aumento de los niveles de ahorro nacional, la asignación
eficiente de los recursos, y la ampliación de los servicios financieros, todo en un
marco de un mercado libre y transp...
```

**Proposed signature:** `Superintendencia del Sistema Financiero\nDECRETO Nº 809.-\nLA ASAMBLEA LEGISLATIVA`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-LSSF` (1 rows)

**Representative sample (doc id=2372, title=`Ley de Supervisión y Regulación del Sistema Financiero`):**

```
ASAMBLEA LEGISLATIVA - REPÚBLICA DE EL SALVADOR
____________________________________________________________________
DECRETO No. 592
LA ASAMBLEA LEGISLATIVA DE LA REPÚBLICA DE EL SALVADOR,
CONSIDERANDO:
I.- Que el marco jurídico bajo el cual se regula el funcionamiento de las
instituciones supervisoras del sistema financiero actualmente se encuentra
establecido en la Ley Orgánica de la Superintend...
```

**Proposed signature:** `ASAMBLEA LEGISLATIVA - REPÚBLICA DE EL SALVADOR\n________________________________`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-MISC` (1 rows)

**Representative sample (doc id=2710, title=`Cnad Download`):**

```
Superando
Expectativas
DE
CERO A
LÍDERES
MUNDIALES
EN LA INDUSTRIA DE
ACTIVOS DIGITALES
2023 - 2024
Informe Anual de actividades 2023-2024 de la Comisión
Nacional de Activos Digitales. El Salvador, América
Central.

Índice
General
02 - 07 38 - 41
I Bienvenida del Presidente y V Registro Público
Director Ejecutivo de la Comisión
Nacional de Activos Digitales Registro Público del ecosistema de 38
ac...
```

**Proposed signature:** `Superando\nExpectativas\nDE\nCERO A\nLÍDERES\nMUNDIALES\nEN LA INDUSTRIA DE\nACTIVOS DI`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### EL_SALVADOR / `SV-STBL` (1 rows)

**Representative sample (doc id=2387, title=`CNAD Stablecoin Regulation [English]`):**

```
THE NATIONAL COMMISSION FOR DIGITAL ASSETS
WHEREAS:
1. That by means of Legislative Decree No. 643 dated January eleventh, two
thousand twenty-three, published in the Official Gazette No. 438, Volume No. 16,
of the twenty-fourth of that same month and year, the Digital Asset Issuance Act
of El Salvador was issued.
2. That, as provided in Art. 9, subparagraph q), of the Digital Asset Issuance Act, ...
```

**Proposed signature:** `THE NATIONAL COMMISSION FOR DIGITAL ASSETS\nWHEREAS:\n1. That by means of Legislat`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars



## FSRA

### FSRA / `<NULL>` (636 rows)

**Representative sample (doc id=1778, title=`11 Appendix 9 Mkt Misc Amendments`):**

```
Consultation Paper No. 4 of 2019
Appendix 9
Market Rules (MKT)

Appendix 9
2.5 Determination of applications and references
Guidance
Determination of applications
1. Under section 50(2) of the FSMR, a Recognised Body or the Regulator may only
grant admission of Securities to an Official List of Securities maintained by it,
in accordance with the requirements in the FSMR and this Rulebook.
…
4.6.5 ...
```

**Additional samples (4):** doc ids 1780, 1781, 1782, 1783

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/636 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix


### FSRA / `AML` (1 rows)

**Representative sample (doc id=200, title=`Adgm1547 5692 Ver10020125`):**

```
Anti-Money Laundering and Sanctions Rulebook (AML)
(VER10.020125)

TABLE OF CONTENTS
The contents of the AML Rulebook are divided into the following Chapters and sections:
1. INTRODUCTION ......................................................................................... 1
1.1 Jurisdiction.............................................................................................1
1.2 Appli...
```

**Proposed signature:** `Anti-Money Laundering and Sanctions Rulebook (AML)\n(VER10.020125)\n\nTABLE OF CONT`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `BRR` (1 rows)

**Representative sample (doc id=116, title=`Bank Recovery And Resolution Regulation 2018 20`):**

```
BANK RECOVERY AND RESOLUTION REGULATIONS
2018
i

BANK RECOVERY AND RESOLUTION REGULATIONS 2018
General ......................................................................................................................................... 1
The Regulator ............................................................................................................................. 13
Recovery and R...
```

**Proposed signature:** `BANK RECOVERY AND RESOLUTION REGULATIONS\n2018\ni\n\nBANK RECOVERY AND RESOLUTION RE`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `CIB` (1 rows)

**Representative sample (doc id=62, title=`Adgm1547 9385 Ver06290725`):**

```
Captive Insurance Business Rulebook (CIB)
(VER06.290725)

TABLE OF CONTENTS
1 GENERAL PROVISIONS ................................................................................ 1
1.1 Application.......................................................................................................... 1
1.2 Captive Insurance Business ....................................................................
```

**Proposed signature:** `Captive Insurance Business Rulebook (CIB)\n(VER06.290725)\n\nTABLE OF CONTENTS\n1 GE`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `CIB-AMEND` (1 rows)

**Representative sample (doc id=2766, title=`Amendments To Cib`):**

```
Captive Insurance Business Rulebook (CIB)
*In this attachment underlining indicates new text and striking through indicates deleted text.

…
2.3.3 Quarterly Regulatory Return [Deleted]
(1) Except as otherwise provided in this Rule 2.3, a Captive Insurer must, at the end
of March, June, September and December in each year, prepare a quarterly
Regulatory Return in respect of the period commencing at...
```

**Proposed signature:** `Captive Insurance Business Rulebook (CIB)\n*In this attachment underlining indica`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `COBS` (1 rows)

**Representative sample (doc id=2788, title=`Cobs Ver23.290426`):**

```
Conduct of Business Rulebook (COBS)
(VER23.290426)

TABLE OF CONTENTS
1. INTRODUCTION ..................................................................................................... 1
2. CLIENT CLASSIFICATION ...................................................................................... 1
3. CORE RULES – INVESTMENT BUSINESS, ACCEPTING DEPOSITS, PROVIDING
CREDIT AND PROVIDING TRUST SE...
```

**Proposed signature:** `Conduct of Business Rulebook (COBS)\n(VER23.290426)\n\nTABLE OF CONTENTS\n1. INTRODU`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `FEES` (1 rows)

**Representative sample (doc id=87, title=`Adgm1547 7504 Ver20010126`):**

```
Fees Rulebook (FEES)
(VER20.010126)

TABLE OF CONTENTS
1. INTRODUCTION .............................................................................................................. 1
2. AMENDMENTS TO FINANCIAL SERVICES PERMISSIONS, AND WAIVERS AND
MODIFICATIONS ............................................................................................................. 4
3. APPLICATION AND SUPERV...
```

**Proposed signature:** `Fees Rulebook (FEES)\n(VER20.010126)\n\nTABLE OF CONTENTS\n1. INTRODUCTION .........`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `FORMS` (1 rows)

**Representative sample (doc id=2555, title=`FSRA Application Forms and Guidance`):**

```
Form: General Information for Regulated Activities (GIRA)

Sections:
- Applicant Details
  - Legal name of applicant (required)
  - Trading name(s)
  - Legal form (company, partnership, etc.) (required)
  - Country of incorporation (required)
  - Registered office address (required)
  - ADGM office address (required)
- Regulated Activities
  - Regulated Activities applied for (required)
  - Financ...
```

**Proposed signature:** `Form: General Information for Regulated Activities (GIRA)\n\nSections:\n- Applicant`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `FSMR` (1 rows)

**Representative sample (doc id=99, title=`Adgm1547 12483 Ver28311025`):**

```
FINANCIAL SERVICES AND MARKETS REGULATIONS 2015
(CONSOLIDATED VERSION)

TABLE OF CONTENTS
Chapter 1 Powers, Functions and Objectives ....................................................................................... 1
Chapter 1 Rule-making Powers ............................................................................................................ 4
Chapter 2 Rules: Modification, Waiver...
```

**Proposed signature:** `FINANCIAL SERVICES AND MARKETS REGULATIONS 2015\n(CONSOLIDATED VERSION)\n\nTABLE OF`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `FUNDS` (1 rows)

**Representative sample (doc id=2789, title=`Funds Ver12.290426`):**

```
Fund Rulebook (FUNDS)
(VER12.290426)

TABLE OF CONTENTS
The contents of these Rules are divided into the following Chapters, Rules and Appendices:
Page
PART 1 : INTRODUCTION ............................................................................................................ 1
1. APPLICATION AND CLIENT CLASSIFICATION ................................................................. 1
PART 2...
```

**Proposed signature:** `Fund Rulebook (FUNDS)\n(VER12.290426)\n\nTABLE OF CONTENTS\nThe contents of these Ru`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `GEN` (1 rows)

**Representative sample (doc id=2790, title=`Gen Ver13.270426`):**

```
General Rulebook (GEN)
(VER13.270426)

TABLE OF CONTENTS
The contents of this Rulebook are divided into the following Chapters, Rules and Appendices:
Page
1. INTRODUCTION ........................................................................................... 1
1.1 Application .............................................................................................. 1
1.2 Overview of the Ru...
```

**Proposed signature:** `General Rulebook (GEN)\n(VER13.270426)\n\nTABLE OF CONTENTS\nThe contents of this Ru`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `GLO` (1 rows)

**Representative sample (doc id=2792, title=`Glo Ver27.290426`):**

```
Glossary Rulebook (GLO)
(VER27.290426)

1. INTRODUCTION
1.1 Application
1.1.1 This Rulebook ("GLO") applies to every Person to whom any of the Rulebooks apply.
1.2 Defined Terms
1.2.1 In the Rulebooks:
(1) a word or phrase which is defined in GLO is a defined term and has the meaning
given in GLO; and
(2) a word or phrase which relates to a defined term must be interpreted accordingly.
Guidance
1....
```

**Proposed signature:** `Glossary Rulebook (GLO)\n(VER27.290426)\n\n1. INTRODUCTION\n1.1 Application\n1.1.1 Th`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `GPM` (1 rows)

**Representative sample (doc id=2325, title=`Guidance & Policies Manual (GPM)`):**

```
GPM 1.1 General
This document is called the Guidance and Policies Manual (“GPM”). The GPM is for
information purposes only and explains how we may regulate and supervise financial
services firms and markets that operate in ADGM. The GPM has purposely been written
in plain English. The GPM contains guidance on:
(a) our regulatory policies;
(b) our risk-based approach to authorisation, supervision a...
```

**Proposed signature:** `GPM 1.1 General\nThis document is called the Guidance and Policies Manual (“GPM”)`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `IFR` (1 rows)

**Representative sample (doc id=117, title=`Adgm1547 5911 Ver08020125`):**

```
Islamic Finance Rulebook (IFR)
(VER08.020125)

TABLE OF CONTENTS
The contents of this Rulebook are divided into the following chapters, sections and appendices:
1. INTRODUCTION .................................................................................................1
2. ISLAMIC FINANCE ..............................................................................................2
3. GENERA...
```

**Proposed signature:** `Islamic Finance Rulebook (IFR)\n(VER08.020125)\n\nTABLE OF CONTENTS\nThe contents of`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `MIR` (1 rows)

**Representative sample (doc id=2793, title=`Mir Ver12.270426`):**

```
Market Infrastructure Rulebook (MIR)
(VER12.270426)

TABLE OF CONTENTS
1 INTRODUCTION ...................................................................................................................... 1
2 RULES APPLICABLE TO ALL RECOGNISED BODIES .......................................................... 3
2.1 Introduction ..........................................................................
```

**Proposed signature:** `Market Infrastructure Rulebook (MIR)\n(VER12.270426)\n\nTABLE OF CONTENTS\n1 INTRODU`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `MKT` (1 rows)

**Representative sample (doc id=2833, title=`FSRA MKT Rulebook`):**

```
Market Rulebook (MKT)
(VER10.311025)

TABLE OF CONTENTS
The contents of this Rulebook are divided into the following chapters, sections and appendices:
1. INTRODUCTION ......................................................................................... 1
1.1 Application ............................................................................................... 1
1.2 Overview of the Rulebo...
```

**Proposed signature:** `Market Rulebook (MKT)\n(VER10.311025)\n\nTABLE OF CONTENTS\nThe contents of this Rul`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `PIN` (1 rows)

**Representative sample (doc id=91, title=`Adgm1547 9602 Ver11250925`):**

```
Fund Rulebook (FUNDS)
(VER11.250925)

TABLE OF CONTENTS
The contents of these Rules are divided into the following Chapters, Rules and Appendices:
Page
PART 1 : INTRODUCTION ................................................................................................................ 1
1. APPLICATION AND CLIENT CLASSIFICATION ................................................................... 1
...
```

**Proposed signature:** `Fund Rulebook (FUNDS)\n(VER11.250925)\n\nTABLE OF CONTENTS\nThe contents of these Ru`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `PIN-AMEND` (1 rows)

**Representative sample (doc id=2771, title=`Amendments To Pin`):**

```
Prudential – Insurance Business Rulebook (PIN)
*In this attachment underlining indicates new text and striking through indicates deleted text.

…
2.3 Management of particular risks
2.3.1 An Insurer must develop, implement and maintain a risk management system to identify,
assess, monitor, mitigate and control balance sheet risk, including but not limited to:
(a) reserving risk;
(b) investment risk...
```

**Proposed signature:** `Prudential – Insurance Business Rulebook (PIN)\n*In this attachment underlining i`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `PRU` (1 rows)

**Representative sample (doc id=2795, title=`Pru Ver20.270426`):**

```
Prudential – Investment, Insurance Intermediation and Banking
Rulebook (PRU)
(VER20.270426)

TABLE OF CONTENTS
These Rules are divided into the following Chapters, Parts, Sections and Appendices:
1 APPLICATION, INTERPRETATION AND CATEGORISATION .............................. 1
1.1 Application .............................................................................................................
```

**Proposed signature:** `Prudential – Investment, Insurance Intermediation and Banking\nRulebook (PRU)\n(VE`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `REP` (1 rows)

**Representative sample (doc id=304, title=`Adgm Courts Guidelines For Self Represented Litigants (English)04042025`):**

```
ADGM COURTS
GUIDELINES FOR SELF-REPRESENTED LITIGANTS

ADGM COURTS
GUIDELINES FOR SELF-REPRESENTED LITIGANTS
TABLE OF CONTENTS
INTRODUCTION ......................................................................................................................... 1
ADGM COURTS .......................................................................................................................... 1...
```

**Proposed signature:** `ADGM COURTS\nGUIDELINES FOR SELF-REPRESENTED LITIGANTS\n\nADGM COURTS\nGUIDELINES FO`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### FSRA / `WAIVERS` (2 rows)

**Representative sample (doc id=78, title=`Wm54 2020 Class Modification Notice Operating A Multilateral Trading Facility In Relation To Virtual Assets`):**

```
Scope - Authorised Person, Recognised Body or Licensed Person:
CLASS MODIFICATION AND WAIVER - Authorised Persons; and Recognised Investment Exchanges with a
stipulation on their Recognition Order permitting them to conduct the Regulated Activity of Operating a
Multilateral Trading Facility in relation to Virtual Assets
Address:
N/A
Firm Number:
N/A
Notice Number:
WM 54/2020
THE ADGM FSRA HEREBY G...
```

**Additional samples (1):** doc ids 102

**Proposed signature:** `Scope - Authorised Person`

**Backfill dry-run:** 2/2 rows contain signature in first 500 chars

**Risk:** ⚠️ SHORT SIGNATURE — only 25 chars, may collide



## MONDAQ

### MONDAQ / `<NULL>` (2 rows)

**Representative sample (doc id=2127, title=` Fintech 1747894 How To Select The Best Csp For Digital Asse`):**

```
within Technology topic(s)

in United Kingdom

with readers working within the Media & Information industries

within Technology, Finance and Banking and Corporate/Commercial Law topic(s)

Introduction

As digital asset businesses mature and global regulators begin
to converge around common standards, founders, investors, and legal
advisors are increasingly looking toward Abu Dhabi Global Market
(...
```

**Additional samples (1):** doc ids 2128

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/2 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix



## PANAMA

### PANAMA / `PAN-LEY52` (1 rows)

**Representative sample (doc id=2663, title=`Pan Ley52`):**

```
LEY 521
De 27 de octubre de 2016
Que establece la obligación de mantener registros contables para determinadas personas
jurídicas y dicta otras disposiciones
LA ASAMBLEA NACIONAL
DECRETA:
Capítulo I
Registros Contables y su Documentación de Respaldo
Artículo 1. Las personas jurídicas que no realicen operaciones que se perfeccionen, consuman o
surtan sus efectos dentro de la República de Panamá, as...
```

**Proposed signature:** `LEY 521\nDe 27 de octubre de 2016\nQue establece la obligación de mantener registr`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars



## PANAMA_SMV

### PANAMA_SMV / `PAN-AML` (1 rows)

**Representative sample (doc id=2582, title=`Ley 23 De 2015 Blanqueo Seccion Valores`):**

```
Ley 23
De 27 de abril de 2015
Que adopta medidas para prevenir el blanqueo de capitales, el financiamiento del terrorismo y
el financiamiento de la proliferación de armas de destrucción masiva, y dicta otras disposiciones
LA ASAMBLEA NACIONAL
DECRETA:
Título XI
Disposiciones Adicionales
Artículo 69. El artículo 14 del texto único que comprende el Título II de la Ley 67 de 2011 queda
así:
Artículo ...
```

**Proposed signature:** `Ley 23\nDe 27 de abril de 2015\nQue adopta medidas para prevenir el blanqueo de ca`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### PANAMA_SMV / `PAN-LEY32` (1 rows)

**Representative sample (doc id=2590, title=`Ley 32 de 1927 — Sobre Sociedades Anónimas (Panamá)`):**

```
Ley Nº 32 de 1927
1Ley Nº 32
De 26 de febrero de 1927
Sobre Sociedades Anónimas
Sección Primera
De la Formación de la Sociedad
Artículo 1. Dos o más personas mayores de edad, de cualquiera nacionalidad, aun cuando no estén domiciliadas en la
República, podrán constituir una sociedad anónima para cualquier objeto lícito, de acuerdo con las formalidades prescritas
en la presente ley.
Artículo 2. Las...
```

**Proposed signature:** `Ley Nº 32 de 1927\n1Ley Nº 32\nDe 26 de febrero de 1927\nSobre Sociedades Anónimas`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### PANAMA_SMV / `PAN-LMV` (1 rows)

**Representative sample (doc id=2585, title=`Texto Unico Dl1 1999 Ley De Valores`):**

```
TEXTO ÚNICO
Ordenado por la Asamblea Nacional, que comprende
el Decreto Ley 1 de 1999 y sus leyes reformatorias
y el Título II de la Ley 67 de 2011
Sobre el mercado de valores en la República de Panamá
y la Superintendencia del Mercado de Valores
LA ASAMBLEA NACIONAL
DECRETA:
Título Preliminar
Superintendencia del Mercado de Valores
Capítulo I
Creación, Objetivos y Órganos
Artículo 1. Alcance. Par...
```

**Proposed signature:** `TEXTO ÚNICO\nOrdenado por la Asamblea Nacional, que comprende\nel Decreto Ley 1 de`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### PANAMA_SMV / `PAN-LMV-56` (1 rows)

**Representative sample (doc id=2583, title=`Ley 56 De 2012`):**

```
REPÚBLICA DE PANAMÁ
ASAMBLEA NACIONAL
LEGISPAN
LEGISLACIÓN DE LA REPÚBLICA DE PANAMÁ
Tipo de Norma:LEY
Número: 56 Referencia:
Año: 2012 Fecha(dd-mm-aaaa):02-10-2012
Titulo:QUE MODIFICA ARTICULOS DEL DECRETO LEY 1 DE 1999, SOBRE MERCADO DE VALORES
DE LA REPUBLICA DE PANAMA.
Dictada por:ASAMBLEA NACIONAL
Gaceta Oficial:27136 Publicada el:05-10-2012
Rama del Derecho:DER. ADMINISTRATIVO, DER. COMERCIA...
```

**Proposed signature:** `REPÚBLICA DE PANAMÁ\nASAMBLEA NACIONAL\nLEGISPAN\nLEGISLACIÓN DE LA REPÚBLICA DE PA`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### PANAMA_SMV / `PAN-LMV-67` (1 rows)

**Representative sample (doc id=2584, title=`Ley 67 De 2011`):**

```

Gaceta Oficial Digital, viernes 02 de septiembre de 2011

LEY @7

De / depauy de 2051

Que establece el sistema de coordinacién y cooperacion interinstitucional entre los entes de

fiscalizacion financiera, crea la Superintendencia del Mercado de Valores, reforma el

Decreto Ley t de 1999 y la Ley 10 de 1993 y dicta otras disposiciones

LA ASAMBLEA NACIONAL
DECRETA:

Titulo I
Sistemas de Coordina...
```

**Proposed signature:** `Gaceta Oficial Digital, viernes 02 de septiembre de 2011\n\nLEY @7\n\nDe / depauy d`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### PANAMA_SMV / `PAN-LSEG` (1 rows)

**Representative sample (doc id=2581, title=`Ley 12 De 2012 Seguros`):**

```
REPÚBLICA DE PANAMÁ
ASAMBLEA NACIONAL
LEGISPAN
LEGISLACIÓN DE LA REPÚBLICA DE PANAMÁ
Tipo de Norma:LEY
Número: 12 Referencia:
Año: 2012 Fecha(dd-mm-aaaa):03-04-2012
Titulo:QUE REGULA LA ACTIVIDAD DE SEGUROS Y DICTA OTRAS DISPOSICIONES.
Dictada por:ASAMBLEA NACIONAL
Gaceta Oficial:27007-A Publicada el:03-04-2012
Rama del Derecho:DER. COMERCIAL, DER. ADMINISTRATIVO
Palabras Claves:Seguros, Responsab...
```

**Proposed signature:** `REPÚBLICA DE PANAMÁ\nASAMBLEA NACIONAL\nLEGISPAN\nLEGISLACIÓN DE LA REPÚBLICA DE PA`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars



## UAE_FEDERAL

### UAE_FEDERAL / `FEDERAL-LAW` (5 rows)

**Representative sample (doc id=68, title=`Adgm1547 22726 Ver2007`):**

```
CABINET RESOLUTION NO. 28 OF 2007
ON THE IMPLEMENTING REGULATIONS OF FEDERAL LAW NO. 8 OF
2004 CONCERNING FINANCIAL FREE ZONES
The Ministerial Council,
Upon perusal of the Constitution;
Federal Law No. (1) of 1972 Concerning Jurisdiction of Ministries and Powers of Ministers, as
amended;
Federal Law No. (10) of 1980 Concerning the Central Bank, Monetary Regulations and Regulation
of Banking, as am...
```

**Additional samples (4):** doc ids 86, 126, 150, 197

**Proposed signature:** *(none — no reliable common prefix)*

**Backfill dry-run:** 0/5 rows contain signature in first 500 chars

**Risk:** ⚠️ HIGH RISK — no reliable common prefix



## VARA

### VARA / `VARA-ADV` (1 rows)

**Representative sample (doc id=2811, title=`Advisory Services Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Advisory Services Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ") was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ") to regulate Virtual Asset Service Providers (“ VASPs "). This Advisory Services Rulebook is issued pursuant to, and form...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nAdvisory Services Rul`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-BD` (1 rows)

**Representative sample (doc id=2804, title=`Broker-Dealer Services Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Broker-Dealer Services Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ") was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ") to regulate Virtual Asset Service Providers (“ VASPs "). This Broker-Dealer Services Rulebook is issued pursuant to...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nBroker-Dealer Service`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-COMP` (1 rows)

**Representative sample (doc id=2800, title=`Company Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Company Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ”) was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ”) to regulate Virtual Asset Service Providers (“ VASPs ”). This Company Rulebook is issued pursuant to, and forms part of, the Virtu...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nCompany Rulebook\n\nInt`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-CRM` (1 rows)

**Representative sample (doc id=2801, title=`Compliance and Risk Management Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Compliance and Risk Management Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ”) was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ”) to regulate Virtual Asset Service Providers (“ VASPs ”). This Compliance and Risk Management Rulebook is is...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nCompliance and Risk M`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-CUST` (1 rows)

**Representative sample (doc id=2806, title=`Custody Services Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Custody Services Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ”) was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ”) to regulate Virtual Asset Service Providers (“ VASPs ”). This Custody Services Rulebook is issued pursuant to, and forms ...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nCustody Services Rule`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-EX` (1 rows)

**Representative sample (doc id=2805, title=`Exchange Services Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Exchange Services Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ") was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ") to regulate Virtual Asset Service Providers (“ VASPs "). This Exchange Services Rulebook is issued pursuant to, and form...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nExchange Services Rul`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-ISS` (1 rows)

**Representative sample (doc id=2810, title=`Virtual Asset Issuance Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Virtual Asset Issuance Rulebook

Introduction This Virtual Asset Issuance Rulebook (“ VA Issuance Rulebook ”) is issued by VARA pursuant to the Virtual Assets and Related Activities Regulations 2023 , as may be amended from time to time (“ Regulations ”), and includes requirements that all Entities in the Emirate wishing to issue a Virtual...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nVirtual Asset Issuanc`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-LB` (1 rows)

**Representative sample (doc id=2808, title=`Lending and Borrowing Services Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Lending and Borrowing Services Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ") was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ") to regulate Virtual Asset Service Providers (“ VASPs "). This Lending and Borrowing Services Rulebook is is...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nLending and Borrowing`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-MC` (1 rows)

**Representative sample (doc id=2803, title=`Market Conduct Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Market Conduct Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ”) was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ”) to regulate Virtual Asset Service Providers (“ VASPs ”). This Market Conduct Rulebook is issued pursuant to, and forms part...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nMarket Conduct Rulebo`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-MGMT` (1 rows)

**Representative sample (doc id=2807, title=`VA Management and Investment Services Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

VA Management and Investment Services Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ") was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ") to regulate Virtual Asset Service Providers (“ VASPs "). This VA Management and Investment Services ...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nVA Management and Inv`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-TI` (1 rows)

**Representative sample (doc id=2802, title=`Technology and Information Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

Technology and Information Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ”) was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ”) to regulate Virtual Asset Service Providers (“ VASPs ”). This Technology and Information Rulebook is issued pur...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nTechnology and Inform`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars


### VARA / `VARA-TRS` (1 rows)

**Representative sample (doc id=2809, title=`VA Transfer and Settlement Services Rulebook | Virtual Assets Regulatory Authority (VARA)`):**

```
Entire section

Custom print

Text Only

Rich Text

Print

VA Transfer and Settlement Services Rulebook

Introduction The Dubai Virtual Assets Regulatory Authority (“ VARA ”) was established and authorised by Law No. (4) of 2022 Regulating Virtual Assets in the Emirate of Dubai (“ Dubai VA Law ”) to regulate Virtual Asset Service Providers (“ VASPs ”), including to issue authorisations to conduct ...
```

**Proposed signature:** `Entire section\n\nCustom print\n\nText Only\n\nRich Text\n\nPrint\n\nVA Transfer and Settl`

**Backfill dry-run:** 1/1 rows contain signature in first 500 chars



---

## Summary

- Total tuples inspected: 137
- Source entities present (15): ADGM, ADGM FSRA, ADGM_COURTS, ADGM_RA, BVI_FSC, DFSA, DIFC, DIFC_COURTS, EL_SALVADOR, FSRA, MONDAQ, PANAMA, PANAMA_SMV, UAE_FEDERAL, VARA
- Tuples with clean signature matching all rows: 125
- Tuples with calibration gaps: 1

  Calibration-gap tuples:
  - `ADGM_RA/ADGM-RA-F`: 17/32
- Tuples with NO reliable signature: 11

  HIGH-RISK tuples:
  - `ADGM/NOTICES` (3 rows)
  - `ADGM FSRA/ADGM-FSRA-F` (71 rows)
  - `ADGM_COURTS/<NULL>` (287 rows)
  - `ADGM_RA/<NULL>` (5 rows)
  - `ADGM_RA/ADGM-DPR` (2 rows)
  - `ADGM_RA/ADGM-RA-RULES` (11 rows)
  - `DIFC/<NULL>` (5 rows)
  - `DIFC_COURTS/<NULL>` (1066 rows)
  - `FSRA/<NULL>` (636 rows)
  - `MONDAQ/<NULL>` (2 rows)
  - `UAE_FEDERAL/FEDERAL-LAW` (5 rows)
- Tuples with short signatures (<30 chars, may collide): 1

  Short-signature tuples:
  - `FSRA/WAIVERS`: 25 chars

## Next session (3b)

Session 3b reads this memo, encodes verified signatures into
`RULEBOOK_SIGNATURES` dict in `adgm_corpus/storage/db.py`, adds Gate 4
(content-sniff classifier) to `assert_write_invariants`, writes unit tests,
and applies xfail-strict markers to any global backfill tests for tuples
with calibration gaps (rows that wouldn't pass with the proposed signature).
