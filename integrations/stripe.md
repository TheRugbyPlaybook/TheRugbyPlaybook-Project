# Integration: Stripe (Payments)

> **Status: CONNECTOR LINKED — NOT APPROVED FOR USE.** A Stripe connector is linked to the owner's claude.ai account, but no use has been approved and the account decisions below are still open. Every write, generation, publication, payment or ad action triggers an approval prompt (`.claude/settings.json`) and needs the owner's explicit approval for that single action; see the external action approval procedure in `CLAUDE.md`. Never store credentials in this repo; use a gitignored `.env` file.

## Role
Stripe processes customer payments for eBook purchases, connected to the Base44 storefront.

## Current state (verified 2026-10-09, read-only)
- One Stripe account, "The Rugby Playbook", in **live mode**: 0 products, 0 webhook endpoints, 0 charges.
- Base44's Stripe integration is **not installed** for the TRP app: no sandbox, no test keys, no live keys.
- The live site currently takes payments through Shopify. See `docs/migration/shopify-to-base44-stripe.md`.

## Planned workflow
1. The owner sets the price for a `READY` book.
2. A Stripe product/price is created (manually or on explicit instruction), using the product ID in its metadata.
3. The checkout is connected to Base44.
4. Sales data feeds `marketing/campaign-data.md` and `marketing/performance-reports.md`.

## Decisions
| Item | Decision |
|---|---|
| Stripe for payments, replacing Shopify checkout | Owner decision, 2026-10-09 |
| Checkout method | Proposed: Stripe Checkout through Base44's built-in Stripe integration — `TO BE CONFIRMED` |
| Set-up order | Proposed: sandbox first; live keys only after sandbox tests pass and with explicit owner approval |
| Payment confirmation | Proposed: server-side only (verified event and/or session retrieval, plus reconciliation) — never the browser redirect |
| Stripe account / business entity | `TO BE CONFIRMED` (account exists; activation and country not yet checked) |
| Currency / currencies | `TO BE CONFIRMED` |
| Pricing per age group / bundles | `TO BE CONFIRMED` |
| Tax / GST handling | `TO BE CONFIRMED` |
| Receipt emails from Stripe | `TO BE CONFIRMED` |
| Refund policy, and whether a refund revokes access | `TO BE CONFIRMED` |

## Rules
- Never create live products, prices, payment links or charges without explicit owner instruction.
- Use test mode for any trial set-up.
- The connected account is in **live mode**. Before any Stripe write, explain the exact call and its financial consequence, and get approval for that single action.
- Products and prices belong to the Stripe account, so every app using the same account shares the catalogue.
