# Integration: Base44 (Storefront and Customer Access)

> **Status: CONNECTOR LINKED — NOT APPROVED FOR USE.** A Base44 connector is linked to the owner's claude.ai account, but no use has been approved and the account decisions below are still open. Every write, generation, publication, payment or ad action triggers an approval prompt (`.claude/settings.json`) and needs the owner's explicit approval for that single action; see the external action approval procedure in `CLAUDE.md`. Never store credentials in this repo; use a gitignored `.env` file.

## Role
Base44 hosts the digital storefront and is the product and order management interface: catalogue, orders, customer entitlements and secure delivery of purchased eBooks. Payments go through Stripe (`integrations/stripe.md`).

## Current live setup (verified 2026-10-09)
The live app at therugbyplaybook.com is a front end for **Shopify**, which runs the catalogue, checkout, payment and paid-file delivery. It is being replaced. See `docs/migration/shopify-to-base44-stripe.md` and `integrations/shopify.md`. The proposed data model is in `docs/commerce-data-model.md`.

## Planned workflow
1. A book reaches `READY` (owner-approved).
2. Listing copy is drafted in `books/<age>/<PRODUCT-ID>/listing.md`.
3. The owner creates or approves the product listing in Base44, using the product ID as the reference.
4. Once live, the owner sets the state to `PUBLISHED`.

## Decisions
| Item | Decision |
|---|---|
| Base44 as storefront and product/order management interface | Owner decision, 2026-10-09 |
| Replace Shopify; retire existing eBooks and bundles | Owner decision, 2026-10-09 |
| Prefer Base44's existing capabilities where reliable | Owner decision, 2026-10-09 |
| Storefront structure (pages, categories by age) | `TO BE CONFIRMED` |
| Existing extras to keep or remove (Interactive Rugby, Legends, Roadmap, gift orders, coaches page) | `TO BE CONFIRMED` |
| Customer access model (account, download link, in-browser reader) | `TO BE CONFIRMED` |
| File delivery / anti-sharing approach (private storage, expiring links) | `TO BE CONFIRMED` — capability must be tested |
| Whether app code can react to Stripe events | `TO BE CONFIRMED` — must be tested |
| Default access rules for entities that define none | `TO BE CONFIRMED` — must be tested |
| Email sending domain (SPF/DKIM) | `TO BE CONFIRMED` |
| Admin account two-factor sign-in and recovery admin | `TO BE CONFIRMED` |
| Backup and export of orders and entitlements | `TO BE CONFIRMED` |
| Privacy policy, terms, refund policy (rewrite; not fetched from Shopify) | `TO BE CONFIRMED` |
| Children's data / privacy compliance | `TO BE CONFIRMED` (customers are parents/adults) |
