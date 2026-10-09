---
description: Assemble final page-by-page content for Canva layout (stages 4 & 6)
argument-hint: <PRODUCT-ID>
---

# /build-pages

Build the page content for **$ARGUMENTS** using the `book-production` skill.

## Steps
1. Read `brief.md`, `outline.md`, `page-plan.md` and the age-group guide.
2. Write `books/<age>/<PRODUCT-ID>/content.md`: one section per page with:
   - page number and layout reference (`templates/page-layouts/`)
   - final text
   - illustration image ID
   - design notes for Canva
3. Check word counts per page against the age-group guide.
4. Update `status.md` with the current stage.
5. Ask the owner to review.

## Rules
- No placeholder text in content intended for layout. Mark gaps clearly as `TO BE CONFIRMED`.
- Do not create or edit Canva designs. Canva is not connected.
