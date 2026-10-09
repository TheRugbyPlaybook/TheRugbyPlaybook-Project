---
description: Prepare an owner-approved book for final export (stage 9)
argument-hint: <PRODUCT-ID>
---

# /export-book

Prepare **$ARGUMENTS** for final export using the `publishing` skill.

## Pre-conditions (all required, else stop)
- `quality-report.md` exists and all items are `PASS` or `N/A`.
- `status.md` records the owner's **explicit approval** with a date.
- No `TO BE CONFIRMED` remains in the book's content.

## Steps
1. Verify the pre-conditions above. If any fail, report them and stop.
2. Produce an export checklist: Canva design link (to be filled in by the owner), file name per `docs/naming-conventions.md`, target folder `output/final/`, preview pages for `output/previews/`.
3. Draft store-listing copy (title, description, age group, page count) in `books/<age>/<PRODUCT-ID>/listing.md` for owner review.
4. Update `status.md` with the export stage.

## Rules
- Do not export from Canva, upload to Base44, create Stripe products or publish anything. These steps are manual or need explicit owner instruction.
- Only the owner moves a book to `READY` or `PUBLISHED`.
