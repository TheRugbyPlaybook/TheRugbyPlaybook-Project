# Integration: Base44 (Storefront and Customer Access)

> **Status: NOT CONNECTED.** This file is documentation only. No account, API key or connection has been set up. Do not connect, authenticate or spend money without explicit owner instruction. Never store credentials in this repo; use a gitignored `.env` file.

## Role
Base44 hosts the digital storefront: product pages, customer accounts and secure access to purchased eBooks.

## Planned workflow
1. A book reaches `READY` (owner-approved).
2. Listing copy is drafted in `books/<age>/<PRODUCT-ID>/listing.md`.
3. The owner creates or approves the product listing in Base44, using the product ID as the reference.
4. Once live, the owner sets the state to `PUBLISHED`.

## Decisions
| Item | Decision |
|---|---|
| Storefront structure (pages, categories by age) | `TO BE CONFIRMED` |
| Customer access model (account, download link, in-browser reader) | `TO BE CONFIRMED` |
| File delivery / anti-sharing approach | `TO BE CONFIRMED` |
| Privacy policy, terms, refund policy | `TO BE CONFIRMED` |
| Children's data / privacy compliance | `TO BE CONFIRMED` (customers are parents/adults) |
