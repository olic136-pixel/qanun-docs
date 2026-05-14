# VARA Corpus Topology Survey

**Generated:** 2026-05-14T16:35:27.122091+00:00
**Block A — Sprint 6 prep overnight**

Purpose: surface what VARA corpus material is available for TemplateDiscoveryAgent (Option C) to consume.

## Rulebook Inventory

| Rulebook Code | Doc ID | Title | Sections | Version |
|---|---|---|---|---|
| VARA-ADV | 2811 | Advisory Services Rulebook | Virtual Assets Regulatory  | 10 | ? |
| VARA-BD | 2804 | Broker-Dealer Services Rulebook | Virtual Assets Regula | 34 | ? |
| VARA-COMP | 2800 | Company Rulebook | Virtual Assets Regulatory Authority  | 101 | ? |
| VARA-CRM | 2801 | Compliance and Risk Management Rulebook | Virtual Asset | 111 | ? |
| VARA-CUST | 2806 | Custody Services Rulebook | Virtual Assets Regulatory A | 60 | ? |
| VARA-EX | 2805 | Exchange Services Rulebook | Virtual Assets Regulatory  | 66 | ? |
| VARA-ISS | 2810 | Virtual Asset Issuance Rulebook | Virtual Assets Regula | 49 | ? |
| VARA-LB | 2808 | Lending and Borrowing Services Rulebook | Virtual Asset | 23 | ? |
| VARA-MC | 2803 | Market Conduct Rulebook | Virtual Assets Regulatory Aut | 39 | ? |
| VARA-MGMT | 2807 | VA Management and Investment Services Rulebook | Virtua | 18 | ? |
| VARA-TI | 2802 | Technology and Information Rulebook | Virtual Assets Re | 30 | ? |
| VARA-TRS | 2809 | VA Transfer and Settlement Services Rulebook | Virtual  | 14 | ? |

**12 current documents, 555 total sections.**

## Section Level Distribution

| Rulebook | L0 | L1 | L2 | L3 | Total |
|---|---|---|---|---|---|
| VARA-ADV | 2 | 6 | 2 | 0 | 10 |
| VARA-BD | 4 | 15 | 15 | 0 | 34 |
| VARA-COMP | 8 | 48 | 45 | 0 | 101 |
| VARA-CRM | 7 | 47 | 57 | 0 | 111 |
| VARA-CUST | 5 | 24 | 31 | 0 | 60 |
| VARA-EX | 5 | 26 | 35 | 0 | 66 |
| VARA-ISS | 4 | 17 | 28 | 0 | 49 |
| VARA-LB | 2 | 9 | 12 | 0 | 23 |
| VARA-MC | 8 | 14 | 17 | 0 | 39 |
| VARA-MGMT | 2 | 13 | 3 | 0 | 18 |
| VARA-TI | 3 | 19 | 8 | 0 | 30 |
| VARA-TRS | 2 | 8 | 4 | 0 | 14 |

## Most-Referenced Sections (Top 20)

Candidate Tier-1/Tier-2 `required_provisions` for TemplateDiscoveryAgent.

*No intra-corpus citations extracted yet — see carries below.*

## Vector Store Coverage

- ChromaDB `adgm_docs` VARA vectors: 555
- Pinecone `vara` namespace: 555 vectors
- Case law decisions: 0

## Carries / Known Gaps

- VARA rulebooks parse to Part/lettered-section/rule (L0/L1/L2). VARA L3 sub-provisions still inline (Sprint 3 carry).

## Licence Types

For TemplateDiscoveryAgent (Option C) consumption:

- VASP-BD (Broker-Dealer), VASP-EX (Exchange), VASP-CUST (Custody)
- VASP-ADV (Advisory), VASP-LB (Lending/Borrowing), VASP-MGMT (Mgmt/Investment)
- VASP-TRS (Transfer/Settlement), VASP-ISS (Issuance)
