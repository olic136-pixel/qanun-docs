# DFSA Corpus Topology Survey

**Generated:** 2026-05-14T16:35:27.944990+00:00
**Block B — Sprint 6 prep overnight**

Purpose: surface what DFSA corpus material is available for TemplateDiscoveryAgent (Option C) to consume.

## Rulebook Inventory

| Rulebook Code | Doc ID | Title | Sections | Version |
|---|---|---|---|---|
| None | 2428 | Supervisory Guidelines on Assessing the Suitability of  | 0 | ? |
| DFSA-AFN | 2812 | DFSA AFN Rulebook | 364 | VER5211-22 |
| DFSA-AMI | 2813 | DFSA AMI Rulebook | 632 | VER3001-26 |
| DFSA-AML | 2814 | DFSA AML Rulebook | 405 | VER3004-26 |
| DFSA-AUD | 2815 | DFSA AUD Rulebook | 205 | VER1001-26 |
| DFSA-CIR | 2816 | DFSA CIR Rulebook | 1000 | VER4001-26 |
| DFSA-CMC | 2817 | DFSA CMC Rulebook | 0 | VER411-22 |
| DFSA-COB | 2818 | DFSA COB Rulebook | 1376 | VER5001-26 |
| DFSA-FER | 2819 | DFSA FER Rulebook | 209 | VER3504-26 |
| DFSA-FPR | 2820 | DFSA FPR Rulebook | 186 | VER102-19 |
| DFSA-GEN | 2821 | DFSA GEN Rulebook | 1216 | VER7101-26 |
| DFSA-GLO | 2822 | DFSA GLO Rulebook | 17 | VER6401-26 |
| DFSA-IFR | 2823 | DFSA IFR Rulebook | 294 | VER2212-25 |
| DFSA-MKT | 2824 | DFSA MKT Rulebook | 690 | VER2701-26 |
| DFSA-PIB | 2825 | DFSA PIB Rulebook | 1174 | VER5201-26 |
| DFSA-PIN | 2826 | DFSA PIN Rulebook | 501 | VER1804-23 |
| DFSA-PRS | 2827 | DFSA PRS Rulebook | 107 | VER704-18 |
| DFSA-PRU | 2828 | DFSA PRU Rulebook | 0 | VER1012-25 |
| DFSA-RAR | 2829 | DFSA RAR Rulebook | 202 | VER104-21 |
| DFSA-REC | 2830 | DFSA REC Rulebook | 89 | VER1305-24 |
| DFSA-REP | 2831 | DFSA REP Rulebook | 122 | VER1211-22 |
| DFSA-TKO | 2832 | DFSA TKO Rulebook | 365 | VER0804-20 |

**22 current documents, 9154 total sections.**

## Section Level Distribution

| Rulebook | L0 | L1 | L2 | L3 | Total |
|---|---|---|---|---|---|
| None | 0 | 0 | 0 | 0 | 0 |
| DFSA-AFN | 12 | 186 | 165 | 1 | 364 |
| DFSA-AMI | 0 | 64 | 165 | 403 | 632 |
| DFSA-AML | 1 | 52 | 105 | 247 | 405 |
| DFSA-AUD | 0 | 29 | 62 | 114 | 205 |
| DFSA-CIR | 16 | 100 | 298 | 586 | 1000 |
| DFSA-CMC | 0 | 0 | 0 | 0 | 0 |
| DFSA-COB | 0 | 108 | 407 | 861 | 1376 |
| DFSA-FER | 0 | 31 | 76 | 102 | 209 |
| DFSA-FPR | 0 | 22 | 81 | 83 | 186 |
| DFSA-GEN | 0 | 106 | 438 | 672 | 1216 |
| DFSA-GLO | 0 | 2 | 2 | 13 | 17 |
| DFSA-IFR | 2 | 44 | 103 | 145 | 294 |
| DFSA-MKT | 1 | 67 | 209 | 413 | 690 |
| DFSA-PIB | 11 | 67 | 363 | 733 | 1174 |
| DFSA-PIN | 0 | 76 | 223 | 202 | 501 |
| DFSA-PRS | 0 | 20 | 33 | 54 | 107 |
| DFSA-PRU | 0 | 0 | 0 | 0 | 0 |
| DFSA-RAR | 0 | 13 | 43 | 146 | 202 |
| DFSA-REC | 0 | 17 | 32 | 40 | 89 |
| DFSA-REP | 0 | 24 | 50 | 48 | 122 |
| DFSA-TKO | 0 | 61 | 157 | 147 | 365 |

## Most-Referenced Sections (Top 20)

Candidate Tier-1/Tier-2 `required_provisions` for TemplateDiscoveryAgent.

| Section Ref | Referenced by |
|---|---|
| DFSA-PIB 4.14 | 38 |
| DFSA-PIB 3 | 16 |
| GEN 5.3 | 14 |
| DFSA-COB 7.12 | 11 |
| DFSA-PIB 2 | 11 |
| DFSA-PIB 4.11 | 11 |
| DFSA-TKO 1.5 | 11 |
| GEN 11.10 | 11 |
| AML 9.3 | 10 |
| DFSA-PIB 4 | 10 |
| DFSA-PIN 6.5 | 10 |
| DFSA-CIR 14.4 | 9 |
| DFSA-CIR 2.1 | 9 |
| DFSA-PIB 3.16 | 9 |
| DFSA-PIN 9.4 | 9 |
| GEN 7.6 | 9 |
| DFSA-CIR 13.12 | 8 |
| DFSA-COB 12.3 | 8 |
| DFSA-COB 5.2 | 8 |
| DFSA-PIB 1 | 8 |

## Vector Store Coverage

- ChromaDB `adgm_docs` DFSA vectors: 9154
- Pinecone `dfsa` namespace: 9154 vectors
- Case law decisions: 0

## Carries / Known Gaps

- 21-module supersede applied Session 4b (docs 2812-2832, version_str populated). Sourcebooks CMC + PRU parse to 0 sections (Block K target this session); FPR/PRS/RAR already parsed; RPP not present as a doc.

## Licence Types

For TemplateDiscoveryAgent (Option C) consumption:

- Category 1-4 Authorised Persons (deposit-taking → advisory)
- DIFC Registered Auditor, Recognised Body, Recognised Member
- Credit Rating Agency, Representative Office
