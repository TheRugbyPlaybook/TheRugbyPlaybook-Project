# Integration: Canva (Design and PDF Export)

> **Status: CONNECTOR LINKED — NOT APPROVED FOR USE.** A Canva connector is linked to the owner's claude.ai account, but no use has been approved and the account decisions below are still open. Every write, generation, publication, payment or ad action triggers an approval prompt (`.claude/settings.json`) and needs the owner's explicit approval for that single action; see the external action approval procedure in `CLAUDE.md`. Never store credentials in this repo; use a gitignored `.env` file.

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
