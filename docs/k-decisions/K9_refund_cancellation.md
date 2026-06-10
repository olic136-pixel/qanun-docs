# K9 — Refund policy + cancellation flow (decision memo)

**Register item:** K9 — Refund policy + cancellation flow. Size: Half-day. Deps: K1.
**Status:** CLIENT-DECISION on policy; the *flow* mostly disappears if K1 lands on Stripe.
**Author:** V4 (MAX-4 K-readiness), 2026-06-10.

## Key point

If K1 resolves to Stripe (recommended), **the Stripe Customer Portal gives cancellation, card update, and invoice history with zero custom code**, and refunds are two clicks in the Stripe dashboard. The only genuine work in K9 is choosing the policy and writing ~4 paragraphs into the ToS. Building an in-product cancellation+refund engine for a customer base of <10 is enterprise theater.

## Policy options

| Option | Refunds | Cancellation | Pros | Cons |
|---|---|---|---|---|
| **A. 14-day money-back (first subscription only) + cancel-anytime effective period end, no pro-rata** | Cooling-off only | Period end | Industry standard; UK consumer-law-shaped (though customers are B2B); trivially administered manually | Rare edge: annual plan cancelled month 2 keeps 10 months' money — mitigated by goodwill discretion |
| **B. Pro-rata refunds on cancellation** | Always | Immediate | Friendliest | Refund accounting on every cancel; pointless generosity for monthly billing |
| **C. No refunds** | None | Period end | Simplest | Bad look for a trust-led compliance product; argues with the 14-day trial anyway |
| **Per-suite one-offs (if K6 Option B)** | — | — | Suggest: no refund once drafting has started; full refund before | Matches digital-goods norms |

## Recommendation

**Option A**, administered manually:

- 14-day money-back on a customer's first paid subscription, on request, no questions.
- Cancel anytime via Stripe Customer Portal; access runs to period end; no pro-rata mid-period refunds (monthly billing makes this a non-issue; for annual plans, goodwill pro-rata at Oliver's discretion).
- Per-suite purchases: refundable until drafting starts, not after.
- Data after cancellation: account reverts to read-only/export for 30 days, then K3 soft-delete retention rules apply (window per K8 decision).
- Day-1 process: refund = Stripe dashboard click + a line in `decisions.log`-equivalent. No code.

## What this unblocks / requires

- ~4 paragraphs in the ToS (K8)
- A "Manage subscription" link in the billing page pointing at the Stripe portal (part of K1 fast-follow)
- Nothing else. Resist building more.

## Decision

- **Policy (A/B/C):** ____________
- **Annual-plan pro-rata discretion:** yes / no
- **Post-cancellation read-only window:** ____________
- **Decided by / date:** ____________
