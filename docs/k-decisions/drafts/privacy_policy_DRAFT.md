> **DRAFT — NOT IN FORCE — for KC review**

# Qanun — Privacy Policy (WORKING DRAFT)

**Status:** Working draft prepared overnight (MAX-6 N5, 2026-06-11) from the K8 decision memo structure. **Drafting accelerant for Oliver-the-KC to settle — not legal advice**; unreviewed; must not be published or linked until the K8 decision block is completed. Decision points `[DECISION: …]`; unsettled facts `[TBD: …]`.

**Posture (per K8 memo):** a single policy covering **UK GDPR and UAE PDPL** (Federal Decree-Law No. 45 of 2021) — "they are close enough for a policy of this size" — with jurisdictional notes where the regimes diverge. If the K8 governing-law decision lands on ADGM and the contracting entity is an ADGM establishment, the **ADGM Data Protection Regulations 2021** become the primary regime and this draft needs re-anchoring (see "Jurisdictional notes" below).

---

## 1. Who we are

[TBD: contracting entity legal name, registered office — must match ToS §1.1.] ("**Qanun**", "we") is the controller of the personal data described in this policy.

**Data-protection contact:** [TBD: privacy@qanun.io — K8 memo: "name a contact email as the data-protection contact". Decide whether a formal DPO appointment is required — on current scale and processing, likely not under UK GDPR Art. 37; PDPL Art. 10 DPO triggers should be checked at settlement.]

## 2. What we collect

| Category | Examples | Source |
|---|---|---|
| Account data | name, business email, password hash, organisation, role | you, at sign-up |
| Entity profile data | entity names, licence types and categories, registration/licence numbers, permitted activities, addresses, staffing and AUM ranges, key personnel names (MLRO, SEO, compliance officer) | you, via onboarding, questionnaires and twins |
| Usage content | research queries, drafting instructions, questionnaire answers, generated documents and exports | you, by using the Service |
| Support data | messages to support, ticket contents | you |
| Technical data | log data, IP address, session identifiers | automatic |

**A note on whose data this is:** entity profiles and licence details typically concern **regulated firms** (your firm or your clients' firms) and their named officers. Where you submit personal data of third parties (e.g. an MLRO's name), you confirm you are entitled to do so; we process it as part of Customer Content under our contract with you. [KC NOTE: the K8 memo flags that the first law-firm customer will ask about exactly this — consider whether a short controller/processor split or a data-processing addendum is needed for firm customers submitting client data. This draft treats Qanun as controller for account/technical data and processor-like for Customer Content; settle the characterisation.]

## 3. Why we process it (lawful bases)

| Purpose | UK GDPR basis | UAE PDPL note |
|---|---|---|
| Providing the Service (accounts, queries, drafting, twins, alerts) | Contract (Art. 6(1)(b)) | PDPL contractual-necessity ground |
| AI-assisted processing of queries and drafting via our model provider (§6) | Contract | disclosed processing purpose; no automated decision producing legal effects without review — the §5 ToS professional-review duty is also the PDPL Art. 18 mitigation |
| Service emails (verification, password reset, support acknowledgements) | Contract / legitimate interests | contractual necessity |
| Security, abuse prevention, logging | Legitimate interests | legitimate-interest-equivalent per PDPL Art. 4 exemptions [KC: PDPL has no general legitimate-interests basis — map these to contract/legal-obligation/consent at settlement] |
| Product communications / marketing | Consent or soft opt-in (PECR) | **PDPL: consent required** — do not rely on soft opt-in for UAE data subjects |
| Legal obligations | Legal obligation (Art. 6(1)(c)) | compliance with applicable law |

We do **not**: sell personal data; use Customer Content to train AI models (and our subprocessor terms prohibit our AI providers from doing so); or carry out automated decision-making producing legal or similarly significant effects.

## 4. Jurisdictional notes — [K8: "jurisdictional-data notes"]

- **UK/EU data subjects:** UK GDPR applies as drafted. [TBD: if EU (not just UK) customers are expected, add EU GDPR representative analysis under Art. 27.]
- **UAE data subjects:** UAE PDPL applies. Key divergences handled in this draft: consent-first marketing (§3), cross-border transfer rules (§7), breach notification to the UAE Data Office.
- **ADGM/DIFC customers:** customers established in ADGM or DIFC are subject to their own free-zone data-protection regimes (ADGM DPR 2021; DIFC DP Law No. 5 of 2020) **as controllers of their own data**; this policy governs Qanun's processing, not theirs. [DECISION: if the contracting entity is an ADGM establishment, the ADGM DPR 2021 governs Qanun directly — re-anchor §§3, 7, 8 and notify the ADGM Office of Data Protection as required.]
- **Hosting:** the Service is hosted on [TBD: confirm — Hetzner, Germany (EU), per the deployment plan; name the region at settlement]. Regulatory corpus content (public regulatory texts) is not personal data.

## 5. Retention

- Account and entity-profile data: for the life of the account.
- After account deletion (or post-cancellation expiry of the read-only window in ToS §9.4): soft-deleted and retained for **[TBD: 90 days suggested — K8 decision block; this number drives the K3 soft-delete build]**, then purged.
- Generated documents: retained while your account is active; included in the export window and deletion schedule above.
- Support tickets: [TBD: suggest 24 months].
- Logs: [TBD: suggest 90 days].

## 6. Subprocessors and recipients

| Recipient | Role | Location |
|---|---|---|
| Anthropic | AI model provider — processes query text, drafting prompts and entity context to generate Output; contractual terms prohibit training on our customers' data [KC: verify current Anthropic commercial terms at settlement] | [TBD: US/EU processing region] |
| [TBD: Stripe, per K1] | payment processing — we never hold full card data | global |
| [TBD: hosting provider — Hetzner per deployment plan] | infrastructure | Germany (EU) |
| [TBD: email/ESP when chosen — currently none; transactional email is console/SMTP] | transactional email | [TBD] |

We will keep a current subprocessor list available and notify material changes. No analytics or advertising processors are in use. [KC NOTE: keep this true, or amend §9.]

## 7. International transfers

Personal data is hosted in [TBD: Germany/EU]. Transfers to our AI provider may involve processing in the United States [TBD: confirm Anthropic processing region / data-residency options]. Where personal data is transferred out of the UK, we rely on [TBD: UK adequacy / IDTA / Addendum to EU SCCs]; where transferred out of the UAE, PDPL Arts. 22–23 transfer conditions apply [KC: the UAE adequacy list and Data Office executive regulations remain incomplete — settle the PDPL transfer ground at review].

## 8. Your rights

Subject to applicable law, you may request: access; rectification; erasure; restriction; portability; objection (UK GDPR); and equivalent PDPL rights (access, rectification, erasure, restriction, objection to direct marketing, and human review of solely-automated decisions — not applicable, see §3). Contact [TBD: privacy@qanun.io]. We respond within one month (UK GDPR) [KC: PDPL response periods are set by executive regulations — confirm at settlement]. You may complain to the ICO (UK) or the UAE Data Office, or [DECISION: ADGM Office of Data Protection if re-anchored].

## 9. Cookies

The Service uses only functional cookies/storage strictly necessary for authentication and session state. **No analytics or advertising cookies are set, so no consent banner is presented** (per the K8 memo: "do not add a banner for cookies that don't exist"). [KC NOTE / build gate: verify before launch that no analytics have crept in; if they do, this section and a consent mechanism must be added.]

## 10. Security

Encryption in transit; access controls; environment separation; least-privilege credentials. [TBD: settle the honest, specific list at review — encryption-at-rest claims must match the actual deployment before this publishes.] We notify personal-data breaches to the ICO within 72 hours where required (UK GDPR Art. 33) and to the UAE Data Office as required by PDPL, and to affected customers without undue delay.

## 11. Changes

Material changes notified by email or in-app notice at least [TBD: 14/30] days before effect.

---

## K8 decision block (privacy-relevant lines)

- **Governing law / contracting entity (drives §1, §4, §8):** ____________
- **Post-deletion retention window (§5):** ____________ (suggested: 90 days)
- **DP contact mailbox (§1):** ____________ (suggested: privacy@qanun.io)
- **Decided by / date:** ____________

---

> **DRAFT — NOT IN FORCE — for KC review**
