# Integration: Stripe (Payments)

> **Status: CONNECTOR LINKED — NOT APPROVED FOR USE.** A Stripe connector is linked to the owner's claude.ai account, but no use has been approved and the account decisions below are still open. Every write, generation, publication, payment or ad action triggers an approval prompt (`.claude/settings.json`) and needs the owner's explicit approval for that single action; see the external action approval procedure in `CLAUDE.md`. Never store credentials in this repo; use a gitignored `.env` file.

## Role
Stripe processes customer payments for eBook purchases, connected to the Base44 storefront.

## Planned workflow
1. The owner sets the price for a `READY` book.
2. A Stripe product/price is created (manually or on explicit instruction), using the product ID in its metadata.
3. The checkout is connected to Base44.
4. Sales data feeds `marketing/campaign-data.md` and `marketing/performance-reports.md`.

## Decisions
| Item | Decision |
|---|---|
| Stripe account / business entity | `TO BE CONFIRMED` |
| Currency / currencies | `TO BE CONFIRMED` |
| Pricing per age group / bundles | `TO BE CONFIRMED` |
| Tax / GST handling | `TO BE CONFIRMED` |
| Refund policy | `TO BE CONFIRMED` |

## Rules
- Never create live products, prices, payment links or charges without explicit owner instruction.
- Use test mode for any trial set-up.
