# K1 — Payment provider selection (decision memo)

**Register item:** K1 — Billing integration (payment provider selection + integration). Size: Week. Deps: K2, K3.
**Status:** CLIENT-DECISION — blocked on Oliver.
**Author:** V4 (MAX-4 K-readiness), 2026-06-10.

## Context

- Currencies required: GBP, AED, USD. UAE VAT (5%) must be addressed if the selling entity is UAE-established; UK VAT if UK-established. **The selling entity has not been stated anywhere in the register — this is actually the first decision, before the provider.**
- Current state: billing page is a mock (hardcoded "$299/mo Professional", fake card •••• 4242). Pricing page shows tiers with no prices and "Request access" CTAs. No payment code exists in either repo.
- Realistic day-1 volume: low single-digit customers, B2B (compliance officers, law firms). They will expect a proper invoice more than they expect a slick checkout.

## Options

| Option | Fees (approx) | Integration effort | Tax/VAT handling | Invoicing | Fit |
|---|---|---|---|---|---|
| **A. Stripe Billing + Customer Portal** | 2.9% + 30¢ (+0.5% billing) | Low–Medium. Payment Links/Checkout = zero code day-1; portal handles card update, cancel, invoice history for free | You handle VAT registration/filing (Stripe Tax add-on computes it, +0.5%) | Native, good B2B invoices | Best control + cheapest; UAE-entity Stripe support exists, UK trivially |
| **B. Paddle (merchant of record)** | ~5% + 50¢ | Low | Paddle is the seller — handles UAE/UK/EU VAT entirely, no registrations needed | Paddle-branded invoices (some B2B procurement teams dislike) | Best if Oliver wants zero tax admin; weaker for invoice-first B2B |
| **C. GoCardless (direct debit)** | ~1% capped | Medium | You handle VAT | Via integrations | GBP direct debit only — a complement later, not a day-1 provider |
| **D. Adyen** | Custom | High | You handle | Enterprise-grade | Enterprise theater at this stage. Not appropriate. |
| **E. Manual invoicing (bank transfer) for first 1–3 customers** | ~0 | Zero | Normal accounting | Hand-drafted | Entirely credible for first B2B customers; buys time on the integration |

## Recommendation

**Stripe (Option A), staged — with Option E as the bridge:**

1. **Day-1 minimum:** a Stripe account on the selling entity + **Payment Links** for each tier + the no-code **Customer Portal**. Zero backend work. First customer can pay this week. For a law-firm customer that wants an invoice, send a Stripe invoice or a manual one (Option E) — that is not embarrassing at this stage.
2. **Fast-follow (the real K1 build, ~1 week):** Stripe Checkout sessions from the app, webhook → subscription state on the `users` row, gate features by plan, swap the mock billing page for live data + a "Manage billing" link to the portal.
3. Add Stripe Tax when revenue justifies it; revisit GoCardless if UK firms ask for direct debit.

Paddle is the right answer only if Oliver decides he wants zero VAT administration at the cost of ~2% extra margin and Paddle-branded invoices. For a KC who already runs a practice with accounting support, Stripe is the better default.

## Blocked on this decision

- K6 (pricing tiers UI — needs provider's checkout links/price IDs)
- K9 (refund/cancellation flow — Stripe portal solves most of it for free)
- The billing page de-mocking; the pricing page "Request access" → real CTA swap

## Decision

- **Selling entity (UK / ADGM / other):** ____________
- **Provider:** ____________
- **Day-1 path (Payment Links vs full integration first):** ____________
- **Decided by / date:** ____________
