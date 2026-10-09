# Integration: Shopify (current live backend — being retired)

> **Status: CURRENT LIVE COMMERCE BACKEND — BEING RETIRED.** The live site's catalogue, checkout, payment and paid-file delivery run through Shopify. The owner decided on 2026-10-09 to replace it with Base44 + Stripe. No Shopify connector is in use; **every Shopify action is done manually by the owner.** Plan: `docs/migration/shopify-to-base44-stripe.md`.

## What depends on Shopify today
- Product catalogue, copied hourly into Base44 (the sync deletes Base44 products missing from Shopify).
- Product and Roadmap images on Shopify's CDN.
- Checkout and payment.
- Delivery of paid PDFs.
- Customer records and marketing consent (from free-sample and Legends sign-ups).
- Store policies (privacy, refund, terms, shipping), fetched live.
- Judge.me reviews.
- Early-access eligibility (All 4 Bundle orders).
- Currency by country (Shopify Markets).

## Export checklist (owner, read-only)
Exports containing personal data must be stored **outside git**.
- [ ] Orders, all statuses, all time
- [ ] Customers, including marketing consent and its date
- [ ] Product PDFs and source files for every existing book
- [ ] Product and Roadmap images
- [ ] Policy text (to rewrite without personal contact details)
- [ ] Judge.me reviews
- [ ] Digital-delivery app settings and link lifetime
- [ ] Payouts, disputes and tax reports

## Retirement criteria
See section 8 of the migration plan. In short: 30 days or more with no Shopify checkouts; refund and dispute windows passed; payouts settled; records exported; legacy downloads served from Base44; no domain attached in Shopify; tokens revoked.

## Decisions
| Item | Decision |
|---|---|
| Replace Shopify with Base44 + Stripe | Owner decision, 2026-10-09 |
| Retire existing eBooks and bundles | Owner decision, 2026-10-09 |
| Payment provider used in Shopify | `TO BE CONFIRMED` |
| Plan, monthly cost, pause option | `TO BE CONFIRMED` |
| Legacy buyers' continued access | `TO BE CONFIRMED` |
