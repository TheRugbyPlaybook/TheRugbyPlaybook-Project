# Integration: Stripe (Payments)

> Never store credentials in this repo; use a gitignored `.env` file. A connection is not permission: every guarded action also needs the owner's explicit instruction.

## Connection status (verified 2026-10-09)
> ⚠️ **LIVE MODE ONLY.** The only account available ("The Rugby Playbook") is in live mode, and there is no test account. Any write could create real products or prices, or move real money.

- **Verified (read-only):** the account listing.
- **Possible, not tested:** API reads and writes (products, prices, payment links), analytics.
- **Guarded in `.claude/settings.json` (asks each time):** `stripe_api_write`, account management, Atlas company formation.
- **Rule:** no Stripe writes until a test environment exists and the owner says to proceed.

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
| Test mode / sandbox set-up | `TO BE CONFIRMED` (required before any write) |

## Rules
- Never create live products, prices, payment links or charges without explicit owner instruction.
- Use test mode for any trial set-up. A test environment does not exist yet.
