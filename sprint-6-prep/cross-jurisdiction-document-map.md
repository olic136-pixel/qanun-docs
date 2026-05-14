# Cross-Jurisdiction Document Equivalence Mapping

**Block G — Sprint 6 prep overnight (15-16 May 2026)**

Pre-Option-C reference for TemplateDiscoveryAgent. Maps logical document
types to their equivalents across the 5 supported jurisdictions. Enables
context propagation: the SAME logical document exists per-jurisdiction
under different names, so a Tier-3 Board Charter drafted for ADGM and one
drafted for VARA share entity facts but differ on provisions.

The 5-tier model (per UCIE v2 SOW §5.2) is jurisdiction-agnostic; this
table is how TemplateDiscoveryAgent knows which jurisdiction-specific
document fills each tier slot.

## Tier 1 — Registration Pack

| Logical Document | ADGM (FSRA) | VARA | DFSA (DIFC) | BVI (FSC) | EL_SALVADOR (CNAD) |
|---|---|---|---|---|---|
| Pre-registration form | FSRA Pre-Application Form | VARA Company Registration Form | DFSA Authorisation Application Form | BVI FSC Approval/Application Form | CNAD DASP Pre-Registration Form + Supporting Letter |
| Corporate documentation | ADGM RA documents + UBO register | VARA Corporate Documents pack | DIFC Registrar incorporation docs | BVI BCA incorporation docs | CNAD Corporate Documentation package |
| Business plan | Business Plan + Activity Description | Business Plan | Regulatory Business Plan | Business Plan (Approved Person) | Business Plan + Capital Adequacy statement |
| Fit & proper | F&P Declarations (senior management) | F&P Declarations (Responsible Individuals) | F&P Forms (Authorised Individuals) | Approved Persons F&P forms | F&P Declarations (Directors + MLRO) |
| Technology statement | (Cat 3C: minimal / per GEN) | Technology Architecture Statement | Tech-risk statement (varies by activity) | (varies by licence) | Cybersecurity Architecture statement |
| AML programme summary | AML Programme Summary | AML/CFT Summary | AML Summary | AML Programme summary | Initial AML/CFT/PWMD Summary |
| Initial capital | Capital Evidence | Initial Capital Evidence | Base Capital Evidence | Statutory Capital evidence | Capital Adequacy + Financial Statement |

## Tier 2 — Mandatory Compliance Framework

| Logical Document | ADGM | VARA | DFSA | BVI | EL_SALVADOR |
|---|---|---|---|---|---|
| AML/CFT policy + procedures | AML Policy + Compliance Manual | AML/CFT Policy & Procedures Manual | AML Compliance Manual | AML/CFT Programme | AML/CFT/PWMD Prevention Programme |
| KYC/CDD procedures | (within AML Policy) | KYC/CDD Procedures Manual | KYC/CDD Procedures | CDD Procedures | KYC/CDD Policy & Procedures Manual |
| Travel rule | (FSRA AML Rules — within AML Policy) | Travel Rule Compliance Procedures | (within DFSA AML) | (per AML Code) | FATF Travel Rule Compliance |
| Market conduct | Market Conduct Policy | Market Conduct Policy | Code of Market Conduct (CMC) | (per SIBA conduct rules) | Market Conduct Policy (per CNAD) |
| Conflicts of interest | COI Policy | COI Policy | COI Policy | COI Policy | COI Policy |
| Client protection | Client Protection Policy | Client Protection Policy | Conduct of Business module | Client Asset Protection Policy | Consumer Protection Policy |
| Custody / safeguarding | Custody Policy (where applicable) | Custody & Safeguarding Policy | Client Money + Custody provisions | Trust & Custody (per Banks & Trust Companies Act) | Custody & Safeguarding Policy |
| Complaints | Complaints Policy & Procedure | Complaints Policy & Procedure | Complaints Handling procedures | Complaints Procedure | Complaints Handling Policy |
| Cybersecurity | Cyber Risk Policy (per GEN 3.5) | Cybersecurity & Info Security Policy | Operational Risk + Tech Risk | Cybersecurity (per AML/MLR) | Cybersecurity & Information Security Policy |
| Outsourcing | Outsourcing Policy (per GEN 3.3.32) | Outsourcing Policy | Outsourcing Policy | Outsourcing Policy | Outsourcing & Third-Party Risk Policy |
| Risk management | Risk Management Framework | Compliance & Risk Management Manual | Risk Management Framework | Risk Management Policy | Risk Management Framework |

## Tier 3 — Corporate Governance Framework

| Logical Document | ADGM | VARA | DFSA | BVI | EL_SALVADOR |
|---|---|---|---|---|---|
| Board charter | Board Terms of Reference | Board of Directors Charter | Board Charter | Board Terms of Reference | Board / Governing Body Charter |
| Audit committee | Audit Committee ToR | Audit Committee ToR | Audit Committee ToR | (per board / smaller entities) | (per board) |
| Risk committee | Risk Committee ToR | Risk Committee ToR | Risk Committee ToR | (per board) | (per board) |
| MLRO charter | MLRO Terms of Reference | (within Compliance & Risk Mgmt Manual) | MLRO Role Description | MLRO Terms of Reference | Compliance Officer / MLRO Charter |
| Senior management map | Senior Management Responsibilities Map | Senior Management Map | Senior Manager Regime (SMR) map | (per Approved Persons regime) | Senior Management Responsibilities Map |
| Delegation of authority | DoA Matrix | DoA Matrix | DoA Matrix | DoA Matrix | DoA Matrix |
| Remuneration | Remuneration Policy | Remuneration Policy | Remuneration Policy | Remuneration Policy | Remuneration Policy |
| Whistleblowing | Whistleblowing Policy (per GEN 3.4) | Whistleblowing Policy | Whistleblowing Policy | Whistleblowing Policy | Whistleblowing Policy |
| Fitness & propriety (ongoing) | Ongoing F&P Monitoring Policy | Continuing F&P Requirements | Ongoing F&P Policy | Continuing Approved Persons obligations | Ongoing F&P Monitoring Policy |

## Tier 4 — Operational Procedures

Tier 4 is the most activity-specific tier — the procedures vary heavily
by licence type, not just by jurisdiction. The "same activity" (exchange,
custody, broker-dealer) yields similar manuals across jurisdictions.

| Logical Document | ADGM | VARA | DFSA | BVI | EL_SALVADOR |
|---|---|---|---|---|---|
| Trade execution / dealing procedures | Dealing Procedures (Matched Principal) | Trade Execution Procedures (per VASP-BD/EX) | Dealing Procedures (per COB) | Dealing Procedures (per SIBA) | Trade Execution Procedures (per DASP-EX) |
| Custody operations manual | Client Asset Operations Manual | Custody Operations Manual (per VASP-CUST) | Client Money & Custody Operations | Custody Operations (per Banks & Trust Cos Act) | Custody Operations Manual (per DASP-CUST) |
| Order & transaction records | Order Records procedure (Appendix F-pattern) | Order & Transaction Recording Procedure | Transaction Records procedure | Transaction Records (per SIBA) | Order & Transaction Records Procedure |
| Transaction monitoring (AML ops) | Transaction Monitoring Procedure | Transaction Monitoring Procedure | Transaction Monitoring Procedure | Transaction Monitoring Procedure | Transaction Monitoring Procedure |
| Suspicious activity reporting ops | STR/SAR Reporting Procedure (per AML 14.x) | STR Reporting Procedure | STR Reporting Procedure | SAR Procedure (per AML Code) | ROS Reporting Procedure (UIF) |
| Client onboarding workflow | Client Onboarding Procedure | Client Onboarding Procedure (per VASP) | Client Onboarding Procedure | Client Onboarding Procedure | Client Onboarding Procedure |
| Reconciliation procedures | Client Money Reconciliation Procedure | Asset Reconciliation Procedure | Client Money Reconciliation | Reconciliation Procedure | Asset Reconciliation Procedure |
| Business continuity / DR | BCP + Disaster Recovery Plan | BCP + DR Plan | BCP (per operational risk) | BCP | BCP + DR Plan |
| Incident response | Incident Response Procedure | Cyber/Operational Incident Response | Incident Response Procedure | Incident Response Procedure | Incident Response Procedure |
| Complaints handling workflow | Complaints Handling Procedure | Complaints Handling Procedure | Complaints Handling Procedure | Complaints Handling Procedure | Complaints Handling Procedure |
| Sanctions screening ops | Sanctions Screening Procedure | Sanctions Screening Procedure | Sanctions Screening Procedure | Sanctions Screening Procedure | Sanctions Screening Procedure |

## Tier 5 — Regulatory Filings & Monitoring

Tier 5 is filing/return templates + ongoing-monitoring schedules. Highly
jurisdiction-specific in form (each regulator has its own return formats)
but the same logical obligations recur.

| Logical Document | ADGM | VARA | DFSA | BVI | EL_SALVADOR |
|---|---|---|---|---|---|
| Periodic regulatory returns | FSRA Returns templates | VARA Periodic Returns templates | DFSA Returns (per PRU) | BVI FSC Returns | CNAD Periodic Returns templates |
| Annual compliance report | Annual Compliance Report | Annual Compliance Report | Annual Compliance Report | Annual Compliance Report | CNAD Annual Report (cf. SV-ANNUAL corpus doc) |
| Notification templates | FSRA Notifications pack | VARA Notification templates | DFSA Notifications | BVI FSC Notifications | CNAD Notification templates |
| Capital adequacy monitoring | Capital Adequacy Monitoring schedule | Capital Adequacy Monitoring | Capital Adequacy Returns (PRU) | Statutory Capital Monitoring | Capital Adequacy Monitoring (CNAD) |
| AML monitoring schedule | AML Monitoring Schedule (cf. CMP schedule) | AML Monitoring Schedule | AML Monitoring Schedule | AML Monitoring Schedule | AML/CFT Monitoring Schedule |
| Compliance monitoring programme | Compliance Monitoring Programme (CMP) | Compliance Monitoring Programme | Compliance Monitoring Programme | Compliance Monitoring Programme | Compliance Monitoring Programme |
| Record-keeping schedule | Record Keeping Schedule | Record Keeping Schedule | Record Keeping Schedule | Record Keeping Schedule | Record Keeping Schedule |
| Board/committee meeting calendar | Governance Calendar | Governance Calendar | Governance Calendar | Governance Calendar | Governance Calendar |
| Regulatory change log | Regulatory Change Register | Regulatory Change Register | Regulatory Change Register | Regulatory Change Register | Regulatory Change Register |

## Notes for TemplateDiscoveryAgent (Option C)

- **Equivalence ≠ identity.** Same logical document, jurisdiction-specific
  provisions. Context propagation should preserve entity facts (entity
  name, directors, MLRO, activities) but rewrite the regulatory provisions
  from the target jurisdiction's corpus.
- **Mandatory variance.** Some Tier-2 documents are mandatory in one
  jurisdiction, best-practice in another. Audit/Risk committee ToRs are
  mandatory at scale in ADGM/VARA/DFSA but often folded into the board
  for smaller BVI/SV entities. The DocumentSuite.is_mandatory flag (I1)
  carries this.
- **Activity-specificity dominates Tier 4.** A VASP-CUST custody operations
  manual and a Cat-3C client-asset operations manual share ~70% structure;
  the divergence is the provision set, not the document shape. Tier 4 is
  where licence_type matters most.
- **Tier 5 form variance is high but obligation set is stable.** Every
  jurisdiction wants periodic returns + an annual compliance report + a
  CMP + a record-keeping schedule. The templates differ in field layout,
  not in what's being monitored.
- **ADGM is the reference shape.** Stark (Block F) is the canonical Tier-2/3
  exemplar; the qanun-api template registry (Block E, 162 templates) is
  ADGM-heavy. TemplateDiscoveryAgent should treat ADGM templates as the
  structural baseline and adapt per-jurisdiction.
- **Gaps in this map** are marked "(per X)" or "(varies)" — these are
  where the equivalent exists implicitly within a broader document rather
  than as a standalone. Option C should decide whether to split them out
  per-jurisdiction or keep them folded.
