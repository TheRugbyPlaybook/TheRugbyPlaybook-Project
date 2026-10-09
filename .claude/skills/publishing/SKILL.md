---
name: publishing
description: Take an owner-approved TRP book through final export, listing preparation and publication-state tracking. Use for export, store listing drafts and state changes.
---

# Publishing

Covers the workflow stages **approval → final export**, plus post-export state tracking.

## Publication states
| State | Who sets it | Condition |
|---|---|---|
| `DRAFT` | Claude / owner | Default while in production |
| `READY` | **Owner only** | Quality check passed and owner approval recorded |
| `PUBLISHED` | **Owner only** | Live in the storefront |
| `ARCHIVED` | **Owner only** | Withdrawn from sale |

## Export checklist
1. `quality-report.md` is all `PASS` / `N/A`.
2. Owner approval is recorded in `status.md`.
3. Final PDF is exported from Canva (manual for now) and named per `docs/naming-conventions.md`.
4. Saved to `output/final/`. Preview pages saved to `output/previews/`.
5. `listing.md` is drafted for owner review (title, description, age group, page count, price `TO BE CONFIRMED`).
6. Storefront (Base44) and payment (Stripe) setup is **manual, or needs explicit owner instruction**. See `integrations/`.

## Rules
- Never publish, upload, create products or prices, or change live listings without explicit owner instruction.
- Never mark a book `READY` or `PUBLISHED` yourself. Only record the owner's decision.
- To change a published book, create a new version (`-v2`). Do not overwrite.
