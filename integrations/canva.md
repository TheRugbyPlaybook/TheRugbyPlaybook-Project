# Integration: Canva (Design and PDF Export)

> Never store credentials in this repo; use a gitignored `.env` file. A connection is not permission: every guarded action also needs the owner's explicit instruction.

## Connection status (verified 2026-10-09)
- **Verified (read-only):** the connector works and can search the owner's existing designs. None of them are TRP work yet. **No Brand Kit exists.**
- **Possible, not tested:** creating, editing, copying, resizing and exporting designs; brand templates; asset uploads; image generation. Whether the current plan allows Brand Kits and brand templates is unverified.
- **Guarded in `.claude/settings.json` (asks each time):** all create, edit, generate, export, upload, publish-template, folder and comment actions.

## Role
Canva handles page layout, cover design, brand templates and PDF export of finished eBooks.

## Planned workflow
1. Page content is built in `books/<age>/<PRODUCT-ID>/content.md` (`/build-pages`).
2. Approved illustrations are placed into a Canva template (`templates/canva/` documents the templates).
3. The owner reviews the layout in Canva.
4. After quality check and approval, the PDF is exported to `output/final/` and preview pages to `output/previews/`.

## Decisions
| Item | Decision |
|---|---|
| Canva plan | `TO BE CONFIRMED` |
| Brand Kit set-up | `TO BE CONFIRMED` (after colours and fonts are approved) |
| Master templates per age group | `TO BE CONFIRMED` |
| Export settings (PDF type, resolution) | `TO BE CONFIRMED` |
| Where design links are recorded | `TO BE CONFIRMED` (suggest: book `status.md`) |
