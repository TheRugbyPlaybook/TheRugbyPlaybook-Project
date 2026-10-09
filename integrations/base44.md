# Integration: Base44 (Storefront and Customer Access)

> Never store credentials in this repo; use a gitignored `.env` file. A connection is not permission: every guarded action also needs the owner's explicit instruction.

## Connection status (verified 2026-10-09)
- **Verified (read-only):** the connector works, and an app named **"The Rugby Playbook"** already exists. Its contents, build status and published state have **not** been reviewed.
- **Possible, not tested:** builder-AI edits (these cost Base44 credits), direct code edits, data-model and record changes, deploy/publish, secrets and custom domains.
- **Risk:** a deploy makes changes live to customers.
- **Guarded in `.claude/settings.json` (asks each time):** app creation, builder edits, `execute_api` (deploys, secrets, domains, and reads through it too), file edits, commands, checkpoints, entity and schema changes, connector connections.

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
