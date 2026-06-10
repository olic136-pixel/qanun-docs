# K8 — ToS / Privacy Policy / AUP approach (decision memo)

**Register item:** K8 — Terms of service + privacy policy + acceptable use. Size: Half-day (drafting + legal review). Deps: none.
**Status:** CLIENT-DECISION — approach + governing law are Oliver's call; he is uniquely qualified to make it cheaply.
**Author:** V4 (MAX-4 K-readiness), 2026-06-10.

## Why this is genuinely day-1 (not theater)

1. The sign-up form already has a mandatory terms checkbox, and as of `sprint/max4-k-api` the backend **rejects registration without `terms: true`** — so users are currently agreeing to a document that does not exist. That is worse than no checkbox.
2. The product drafts regulatory documents. The single most important clause in the entire pack is the **no-legal-advice / no-reliance disclaimer**: output is AI-assisted drafting support, requires review by a qualified professional, and Qanun accepts no liability for regulatory outcomes. For a product whose premise is anti-hallucination, the contractual liability cap is the backstop for the day a hallucination gets through anyway.
3. Customer data includes entity profiles and licence details of regulated firms — confidentiality terms will be asked about by the first law-firm customer.

## Options

| Option | Cost | Time | Quality/risk |
|---|---|---|---|
| **A. Oliver self-drafts (KC self-review)** | £0 | 1–2 evenings | High quality — he is a KC; only risk is solicitor-style commercial-terms blind spots and his own time |
| **B. Template service (Termly / GetTerms / Avodocs) + KC self-review** | £0–200/yr | Half-day | Good skeleton fast; templates won't have the AI-drafting disclaimer or UAE PDPL nuances — those need hand-drafting anyway |
| **C. External counsel** | £2–5k | 1–2 weeks | Highest assurance; disproportionate pre-revenue, given who the founder is |
| **D. Launch without, fix later** | £0 | 0 | Not acceptable — see point 1 above |

## Recommended decisions

- **Approach: B + A.** Template skeleton for the boilerplate (cookies, IP, termination), Oliver hand-drafts the clauses that matter: AI-output disclaimer, liability cap (fees paid in prior 12 months), confidentiality, data retention.
- **Governing law:** England & Wales is the pragmatic default (enforceability familiar to every likely customer). ADGM courts are a defensible branding alternative given the product, but E&W removes friction for UK law-firm customers. **Oliver to choose.**
- **Data protection:** one privacy policy covering both UK GDPR and UAE PDPL (they are close enough for a policy of this size); name a contact email as the data-protection contact; state retention windows (drives the K3 soft-delete retention period — suggest 90 days post-deletion, then purge).
- **Cookie policy:** the app appears to use only functional auth/session storage — if that holds, a short cookie notice suffices, **no consent banner needed**. Verify no analytics cookies before launch; do not add a banner for cookies that don't exist.
- **AUP:** short — no scraping/resale of corpus content, no automated bulk extraction, no use of output as unreviewed regulatory filings, no credential sharing.

## Blocked on this decision

- Publishing `/terms`, `/privacy`, `/acceptable-use` marketing pages + footer links (an hour of frontend once text exists)
- Sign-up checkbox linking to real documents
- K9 (refund policy lives inside the ToS) and the K3 retention window

## Decision

- **Approach (A/B/C):** ____________
- **Governing law:** ____________
- **Post-deletion retention window:** ____________
- **Decided by / date:** ____________
