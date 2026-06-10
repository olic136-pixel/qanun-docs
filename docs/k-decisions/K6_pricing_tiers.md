# K6 — Pricing tiers definition (decision memo)

**Register item:** K6 — Pricing tiers definition + UI. Size: Day. Deps: K1.
**Status:** CLIENT-DECISION — the numbers are Oliver's call; the UI work is small once numbers exist.
**Author:** V4 (MAX-4 K-readiness), 2026-06-10.

## Current state

- Marketing pricing page (`app/(marketing)/pricing/page.tsx`) already ships three tiers — Starter / Professional / Enterprise — with feature lists but **no prices** ("Request access" / "Talk to us" CTAs).
- Dashboard billing page hardcodes "Professional $299/mo".
- The register asks for per-document, per-suite, per-firm dimensions. The product's standout value unit is the **governance suite draft** (a full 5-tier suite that would cost five figures from a law firm), which the subscription framing currently undersells.

## Options

| Option | Shape | Pros | Cons |
|---|---|---|---|
| **A. Pure subscription** (Starter ~£99/mo, Professional ~£249–299/mo, Enterprise custom) | Matches existing page + billing mock | Predictable MRR; simplest Stripe setup (2 prices + custom) | Underprices suite drafting; Starter may attract support-heavy low-value users |
| **B. Subscription + per-suite credit** (Professional ~£249/mo incl. 1 suite/quarter; extra suites ~£500–1,500 each) | Hybrid | Captures suite value; clean upsell; per-document covered by "redraft included" | Slightly more billing logic (one-off Stripe prices alongside subscription) |
| **C. Pure per-document / per-suite** (no subscription) | Usage-based | Easiest first sale ("one suite, £X") | No recurring revenue; twins/alerts (continuous monitoring) don't fit one-offs |
| **D. Founding-customer manual pricing** (first 3–5 customers: bespoke quotes, annual invoice) | Concierge | Maximum learning, zero billing build; honest about where the product is | Doesn't scale; needs discipline to graduate to A/B |

## Recommendation

**D now, B as the published structure.** Sign the first customers on founding-customer terms (annual invoice, bespoke). Publish Option B numbers on the pricing page so the page stops looking unfinished — visible pricing is itself a credibility signal for compliance buyers. Suggested opening numbers (deliberately revisable):

- **Starter** £99/mo — 50 queries, 1 twin, ADGM+DIFC (the page's existing feature list)
- **Professional** £299/mo — unlimited queries, all jurisdictions, 5 twins, 1 governance-suite draft per quarter included; additional suites £750
- **Enterprise / Firm** custom — per-firm pricing (K4 FIRM_ADMIN multi-entity tenancy is the natural billing boundary when it activates)

Trial: 14-day trial on Starter/Professional via Stripe `trial_period_days` — no extra build. Currency: price in GBP, let Stripe present AED/USD via multi-currency prices when needed; do not hand-build currency display.

## Blocked on this decision

- Pricing page numbers + CTA swap (an hour of frontend once numbers exist)
- Stripe price objects (K1)
- Trial-vs-paid gating in-product

## Decision

- **Structure (A/B/C/D):** ____________
- **Numbers:** Starter ______ / Professional ______ / per-suite ______ / Enterprise floor ______
- **Trial length:** ____________
- **Decided by / date:** ____________
