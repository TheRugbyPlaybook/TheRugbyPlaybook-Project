# Integration: Canva (Design and PDF Export)

> **Status: NOT CONNECTED.** This file is documentation only. No account, API key or connection has been set up. Do not connect, authenticate or spend money without explicit owner instruction. Never store credentials in this repo; use a gitignored `.env` file.

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
