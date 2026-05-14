# Provision Coverage Matrix (Review)

**Generated:** 2026-05-14T16:39:29.790285+00:00
**Block H — Sprint 6 prep overnight**

TemplateDiscoveryAgent input: maps (jurisdiction, licence_type, tier, document) to primary_provisions; each provision verified against corpus.db. Representative coverage — Option C extends from the full UCIE v2 SOW §6.1/§8.2 tables.

> Provisions are given at rulebook-or-chapter granularity (e.g. "AML 1.1", "VARA-COMP I.A") because section-level required_provisions for every document is Option C's job. This matrix verifies the rulebook anchors EXIST and surfaces which jurisdictions have thin coverage.

## ADGM

- Documents mapped: 6
- Provision anchors verified: **13** / missing: **0**

| Tier | Document | Licence | Provisions (✓ verified / ✗ missing) |
|---|---|---|---|
| 1 | Business Plan | All | ✓GEN Chapter 1 ✓GEN 8.4 |
| 1 | AML Programme Summary | All | ✓AML 1.1 ✓AML 3.1 |
| 2 | AML/CFT Policy + Compliance Manual | All | ✓AML 1.1 ✓AML 1.2 ✓AML 1.3 ✓AML 3.1 |
| 2 | Conflicts of Interest Policy | All | ✓COBS Chapter 3 |
| 2 | Prudential / Capital Policy | Cat 1-3 | ✓PRU 1.1 ✓PRU 1.1.1 ✓PRU 8.3 |
| 3 | Board Terms of Reference | All | ✓GEN Chapter 1 |

## VARA

- Documents mapped: 3
- Provision anchors verified: **7** / missing: **0**

| Tier | Document | Licence | Provisions (✓ verified / ✗ missing) |
|---|---|---|---|
| 1 | Business Plan | All | ✓VARA-COMP I ✓VARA-COMP I.A |
| 2 | Compliance & Risk Management Manual | All | ✓VARA-CRM I ✓VARA-CRM I.A.7 ✓VARA-CRM I.B |
| 3 | Board of Directors Charter | All | ✓VARA-COMP I.A.1 ✓VARA-COMP I.A.2 |

## DFSA

- Documents mapped: 4
- Provision anchors verified: **9** / missing: **0**

| Tier | Document | Licence | Provisions (✓ verified / ✗ missing) |
|---|---|---|---|
| 1 | Regulatory Business Plan | Cat 1-4 | ✓GEN 1.1 ✓GEN 1.2 |
| 2 | AML Compliance Manual | All | ✓AML 1.1 ✓AML 1.1.1 ✓AML 1.1.1(a) |
| 2 | Conduct of Business module compliance | All | ✓COB 1.1 ✓COB 1.1.1 |
| 3 | Board Charter | All | ✓GEN 1.1 ✓GEN 2.1 |

## BVI

- Documents mapped: 3
- Provision anchors verified: **6** / missing: **0**

| Tier | Document | Licence | Provisions (✓ verified / ✗ missing) |
|---|---|---|---|
| 1 | Business Plan (Approved Person) | All | ✓BVI-SIBA Part I ✓BVI-SIBA Part II |
| 2 | AML/CFT Programme | All | ✓BVI-AML Part I ✓BVI-AML Part II ✓BVI-AML Part III |
| 3 | Board Terms of Reference | All | ✓BVI-SIBA Part III |

## EL_SALVADOR

- Documents mapped: 3
- Provision anchors verified: **7** / missing: **0**

| Tier | Document | Licence | Provisions (✓ verified / ✗ missing) |
|---|---|---|---|
| 1 | Business Plan + Capital Adequacy | All DASP | ✓SV-LEAD Art.1 ✓SV-LEAD Art.2 ✓SV-DASP Art.37 |
| 2 | AML/CFT/PWMD Prevention Programme | All | ✓SV-AML Art.1 ✓SV-DASP Art.38 ✓SV-DASP Art.39 |
| 3 | Board / Governing Body Charter | All | ✓SV-DASP Art.40 |

## For TemplateDiscoveryAgent (Option C)

- The JSON sibling (`provision-coverage-matrix.json`) is the machine-readable form.
- This is a *representative* matrix — Option C extends it to every document in the cross-jurisdiction map (Block G) using the full UCIE v2 SOW §6.1 (VARA) + §8.2 (SV) tables.
- Any provision marked ✗ missing means the rulebook anchor isn't in corpus.db at that section_ref — either the ref shape is wrong or the content isn't ingested. Option C must not emit a SectionSpec citing a ✗ provision.
