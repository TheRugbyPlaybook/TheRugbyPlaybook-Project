# Migration plan: Shopify → Base44 + Stripe

> **Status: PLAN — no live changes authorised.** Recorded 2026-10-09 from a read-only discovery. Every external action in this plan (Base44 writes or deploys, Stripe writes, domain changes, Shopify changes, customer emails) needs the owner's explicit approval for that single action. See the approval procedure in `CLAUDE.md`.

## 1. Owner business decisions (2026-10-09)
- TRP is being repositioned as a high-quality digital rugby education publishing brand.
- The existing eBooks and bundles will be **retired**. They do not meet the desired quality standard.
- New eBooks will be produced from the ground up through the gated workflow (`docs/workflow.md`, `docs/quality-control.md`).
- Shopify will be replaced. **Base44** becomes the storefront and product/order management interface, with **Stripe** for payments.
- Base44's existing capabilities are preferred where they are reliable; no unnecessary services.
- No live changes have been authorised yet.

## 2. Current state

### Verified (read-only checks, 2026-10-09)
| Area | Fact |
|---|---|
| Base44 app | "The Rugby Playbook". Published. Custom domain therugbyplaybook.com is attached, verified and serving the app. |
| Architecture | Base44 is a headless front end for Shopify. Catalogue, checkout, payment and paid-file delivery all run through Shopify. |
| Catalogue | 9 `Product` records copied from Shopify by an **hourly workflow** ("Hourly Shopify Product Sync"). The sync **deletes** any Base44 `Product` whose handle is not in Shopify. Prices are stored as decimals in NZD. |
| Images | Every product image, and the Roadmap images, are hosted on Shopify's CDN. Page images ("See Inside", header) are on Base44 media. |
| Checkout | `createShopifyCheckout` builds a Shopify cart and redirects to Shopify checkout. The customer returns to `/post-purchase`, which shows no order data. |
| Paid delivery | Handled by Shopify. No paid file is stored in Base44 (`download_url` is empty on all paid products). |
| Free sample | Delivered by email from Base44. The PDF sits at a **public** Base44 media URL; a second copy is referenced from Shopify. |
| Other Shopify ties | Free-sample and "Legends" sign-ups create or update Shopify customers (with marketing consent). Policies are fetched live from Shopify. Judge.me reviews. Early-access eligibility checks Shopify orders for the All 4 Bundle. Currency by country uses Shopify Markets. |
| Stored Base44 data | 1 admin user, 1 early-access registration (includes a child's first name and age group), 0 gift orders, 4 published blog posts, 5 Testimonial records. 14 further reviews are hard-coded in the site's source. |
| Stripe | One account, "The Rugby Playbook", in **live mode**: 0 products, 0 webhook endpoints, 0 charges. |
| Base44 Stripe integration | **Not installed**: no sandbox, no test keys, no live keys. |
| Base44 branches | `main`, plus `independent-inventory-payments`, which is an **older snapshot** with no payment code. It lacks the `GiftOrder` and `SiteError` entities. Do not merge it. |
| Access | Base44 roles are `admin` and `user` only. |

### TO BE CONFIRMED
| System | Item |
|---|---|
| Shopify | Order count and history; customer and marketing-consent records; which app delivers paid PDFs and how long its links stay valid; payment provider (Shopify Payments or other); payouts and open disputes; plan and monthly cost; whether therugbyplaybook.com is still attached as a Shopify domain; Judge.me export; gift-delivery workflow status. |
| Stripe | Account activation, country, default currency, GST registration, receipt emails. |
| Base44 | Whether app code can react to Stripe events, or only the platform does; private file storage with expiring links; default access rules where an entity defines none (`Product`, `FaqItem`, `Testimonial`); data export and backup options; email sending domain (SPF/DKIM); two-factor authentication for the admin account. |
| Content | Location of the source PDFs and design files for the existing books (Shopify, Canva or OpenArt). |

## 3. Inventory of existing products (to be retired, not deleted)

| Title | Handle | Price (NZD) | Type | Pages |
|---|---|---|---|---|
| Tackle Time | `how-to-tackle-in-rugby-for-beginners` | 4.99 | Book | 20 |
| Pass Perfect | `digital-product` | 4.99 | Book | 20 |
| Find Your Spot | `digital-product-1` | 4.99 | Book | 20 |
| Score Big | `digital-product-2` | 4.99 | Book | 20 |
| Tackle & Pass | `tackle-pass-bundle` | 7.99 (compare-at 11.66) | Bundle | 40 |
| Tackle & Position | `tackle-position` | 7.99 | Bundle | — |
| Score & Position | `digital-product-4` | 7.99 | Bundle | — |
| All 4 Bundle | `all-4-bundle` | 11.99 (compare-at 14.99) | Bundle | — |
| Rugby Playbook Free Sample | `digital-product-3` | 0.00 | Sample | — |

All existing products are labelled "Ages 4–12". This does not match TRP's age groups (3–6, 7–12, 12+).

**Things in the Base44 app that depend on these products:**
- Hard-coded fallback product lists in `src/pages/Shop.jsx` and `src/pages/Home.jsx`. They show **stale prices** (9.99 and 14.99).
- `src/lib/bundleMap.js` (bundle contents).
- `src/lib/roadmapData.js` ("…2" sequels, with images on Shopify's CDN).
- Emails that name the four titles (free sample, gift, early access).
- Early-access eligibility (the All 4 Bundle).
- Google Ads conversion tags in the cart.
- Judge.me reviews keyed to Shopify product IDs.

## 4. Target architecture
- **GitHub (this repo):** source of truth for content, quality evidence and approvals. Each released book version records its final PDF checksum.
- **Base44:** storefront, admin interface, catalogue, orders, entitlements and secure delivery. It reuses the existing site's design and pages where they meet the brand.
- **Stripe:** Stripe Checkout through Base44's built-in Stripe integration. Sandbox first; live keys only with owner approval. Prices are set on the server, never taken from the browser.
- **Fulfilment** only after payment is confirmed on the server: a verified Stripe event, and/or the server retrieving the checkout session from Stripe. A reconciliation job catches anything missed. The browser redirect is never trusted.
- **Files** are held in private storage. A backend function checks the entitlement, then issues a short-lived download link.
- **Shopify** stays read-only until it is retired (section 8).

Data model: `docs/commerce-data-model.md`.

## 5. Payments design

### Verified Base44 platform behaviour (from Base44's API documentation; all marked beta)
- Stripe setup runs sandbox → claim → live keys. Live keys can be the owner's existing keys or provisioned by Base44. Live webhook setup is described as "best effort".
- Base44 receives Stripe webhooks at its own platform endpoint and checks Stripe's signature.
- Stripe products and prices created through Base44 belong to the Stripe account, so every app using that account shares the catalogue.
- Refunds through Base44 take an idempotency key, are safe to retry, and are written to the workspace audit log. In live mode a refund cannot be undone.
- Transaction reports come from an analytics store and "can lag".

### Intended behaviour
| Case | Handling |
|---|---|
| Successful payment | On `checkout.session.completed` with `payment_status = paid` (and `checkout.session.async_payment_succeeded`), mark the order `paid` and grant entitlements in one step that can safely run more than once. |
| Duplicate events | Store Stripe event IDs and checkout session IDs as unique. Entitlements are unique per order line. A repeat event changes nothing. |
| Missed events | A scheduled reconciliation job compares pending orders with Stripe and completes or expires them. |
| Failed or abandoned payment | The order stays `pending`, expires with the checkout session, and grants nothing. |
| Refund | Admin-initiated with an idempotency key, or a refund event from Stripe. Entitlements are revoked according to the refund policy (`TO BE CONFIRMED`). Every action is written to `AuditLog`. |
| Dispute | The order is marked `disputed`; the owner decides on access. Logged. |
| Emails | Stripe sends the payment receipt (setting `TO BE CONFIRMED`). The app sends a delivery email linking to the customer's library, never to the raw file. |
| Backups | Stripe is the payment record. A nightly admin export of orders and entitlements (method `TO BE CONFIRMED`). A Base44 restore point before every deploy. App code mirrored to Git (`TO BE CONFIRMED`). |

### Limitations that must be tested, not assumed
1. Whether app code can react to Stripe events. If not, rely on server-side session retrieval plus reconciliation.
2. Private file storage with expiring links.
3. The default access rules for entities that define none.
4. How the platform handles duplicate and out-of-order events.
5. Payments in currencies other than NZD, and tax/GST behaviour.
6. Email delivery and the sending domain.
7. Whether the live webhook setup completes.

## 6. Phases

| # | Phase | Depends on | Acceptance | Size |
|---|---|---|---|---|
| 0 | **Plan and decisions in the repo** (this document). No external writes. | — | Docs merged; open decisions listed. | S |
| 1 | **Shopify export, done manually by the owner:** orders, customers and consent, PDFs, images, policies, reviews, delivery-app settings. | 0 | Export counts match the Shopify admin. Exports stored **outside git** (they contain personal data). | S |
| 2 | **First new book** through the gated workflow. | 0 | All quality gates pass; owner approval recorded. | L (in parallel) |
| 3 | **Base44 build on a branch.** Disable the hourly Shopify sync first. Add the new entities, private storage, checkout, payment verification, delivery, admin pages, rewritten policies, and admin-only access to the ads dashboard. | 0 | App builds; access-rule tests pass. | L |
| 4 | **Stripe sandbox testing.** | 3 | Every test in section 10 passes. | M |
| 5 | **Legacy access.** Import Shopify orders as `shopify_legacy`; store retired PDFs privately; earlier buyers get library access or a re-issued link. | 1, 3 | Every earlier buyer can download from Base44. | M |
| 6 | **Go-live.** Live Stripe keys; publish the new catalogue; archive (never delete) old products; remove Shopify checkout. The domain already serves Base44, so there is no DNS move. | 2, 4, 5 | A small live purchase and refund by the owner succeeds end to end. | M |
| 7 | **Retire Shopify.** | 6 | Criteria in section 8 are all met. | S |

Every phase from 3 onwards contains external writes and needs per-action owner approval.

## 7. Rollback
- Take a Base44 restore point immediately before go-live.
- Keep Shopify active and its checkout code available until Phase 7.
- Rollback = redeploy the pre-go-live restore point. Shopify checkout resumes. Stripe orders taken in the meantime stay valid in Base44.

## 8. Safe point to stop paying for Shopify
All of these must be true:
- No Shopify checkouts for at least 30 days.
- The refund window has passed, and the dispute window has passed (up to about 120 days if Shopify Payments was used: `TO BE CONFIRMED`).
- Payouts are settled. Tax and order records are exported.
- Legacy downloads are verified from Base44.
- No domain is attached in Shopify.
- Shopify storefront and admin tokens are revoked, and removed from Base44 secrets.

A cheaper Shopify "pause" plan during the waiting period is `TO BE CONFIRMED`.

## 9. Security risks
1. Paid PDFs at public URLs can be shared freely. Use private storage and expiring links.
2. Fulfilment triggered by the browser redirect. Verify on the server.
3. Prices taken from the browser. Look them up on the server.
4. Webhook replays and duplicate events. Use unique event IDs and safe-to-repeat updates.
5. `/admin-ads` and its data functions are public (ad spend, campaigns, analytics, error logs).
6. `/download?u=` displays any URL under the TRP domain.
7. Missing or unknown access rules on `Product`, `FaqItem` and `Testimonial`.
8. The hourly sync deletes catalogue records. Disable it before any Base44 catalogue work.
9. A Shopify admin token with write access to customer records stays live until revoked.
10. The Shopify policy text contains personal contact details. Rewrite the policies before cutover.
11. A child's data in the early-access list. Keep collection to a minimum.
12. Reviews in the source code that have not been verified as genuine. Remove anything that cannot be matched to a real customer.
13. Base44's payment APIs are beta.
14. A single admin account with no confirmed recovery route. Two-factor sign-in `TO BE CONFIRMED`.
15. Stripe products and prices are shared across every app that uses the live account.

## 10. Sandbox test plan (before any live change)
- Successful payment: single book, bundle, several items.
- Declined card; abandoned checkout; expired checkout; 3-D Secure authentication.
- The same webhook sent twice; events out of order; a missed webhook recovered by reconciliation.
- Tampered price, quantity or product ID sent from the browser.
- Refunds: full, partial, retried with the same idempotency key.
- Dispute handling.
- Downloads: expired link, link used too many times, another customer's link, revoked entitlement.
- An anonymous visitor trying to read or write commerce entities.
- Delivery email received and correct.
- Restore from backup.
- Legacy customer access.

## 11. Open decisions (owner)
| Decision | Status |
|---|---|
| Customer access model (account library, emailed link, or both) | `TO BE CONFIRMED` |
| Refund policy, and whether a refund revokes access | `TO BE CONFIRMED` |
| Legacy buyers: keep access to retired books, and for how long | `TO BE CONFIRMED` |
| Currencies, and GST registration | `TO BE CONFIRMED` |
| Pricing for new books and bundles | `TO BE CONFIRMED` |
| Keep or remove: Interactive Rugby, Legends keepsake, Roadmap, gift orders, coaches page | `TO BE CONFIRMED` |
| Reviews to keep (only verified genuine ones) | `TO BE CONFIRMED` |
| Rugby-accuracy reviewer (qualified coach or referee) and law sources | `TO BE CONFIRMED` |
| Email sending domain | `TO BE CONFIRMED` |
| Backup method for orders and entitlements | `TO BE CONFIRMED` |

## 12. Approval gates
`.claude/settings.json` makes Claude Code prompt before every Base44 write, deploy, domain or payment call, every Stripe write, every OpenArt generation, every Canva write, and every GitHub write or `git push`. The owner confirmed on 2026-10-09 that these prompts appear. There is no Shopify connector in use; all Shopify actions are manual by the owner.
