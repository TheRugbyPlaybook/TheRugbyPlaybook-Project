# Book-Production Workflow

```
brief → outline → page plan → content → illustration plan → assets → quality check → approval → final export
```

Every book moves through these nine stages in order. The current stage and state are tracked in `books/<age>/<PRODUCT-ID>/status.md`.

| # | Stage | Output | Who | Command / skill | Gate |
|---|---|---|---|---|---|
| 1 | **Brief** | `brief.md`: audience, goal, skill focus, length, characters | Claude drafts | `/create-book` | Owner agrees brief |
| 2 | **Outline** | `outline.md`: story/chapter structure | Claude drafts | `/create-book` | Owner agrees outline |
| 3 | **Page plan** | `page-plan.md`: per-page text summary, image idea, layout | Claude drafts | `/create-book` | Owner agrees page plan |
| 4 | **Content** | `content.md`: final text per page | Claude drafts | `/build-pages` | Owner reviews text |
| 5 | **Illustration plan** | `illustrations/<age>/<ID>/illustration-plan.md` with prompts | Claude drafts | `/create-illustration` | Owner approves prompts before any generation |
| 6 | **Assets** | Generated and selected images, Canva layout | Owner (OpenArt, Canva), Claude tracks | `illustration-production` | Owner selects images |
| 7 | **Quality check** | `quality-report.md` | Claude | `/quality-check` | All items PASS / N/A |
| 8 | **Approval** | Approval entry in `status.md` | **Owner only** | — | Explicit owner approval → state `READY` |
| 9 | **Final export** | PDF in `output/final/`, previews, `listing.md` | Owner (Canva export), Claude prepares | `/export-book` | Owner decides when to publish |

## Publication states
`DRAFT` → `READY` → `PUBLISHED` → `ARCHIVED`
- Stages 1–7: always `DRAFT`.
- `READY`, `PUBLISHED` and `ARCHIVED` are set **only by the owner**.

## Revisions
- Changes after `PUBLISHED` create a new version (`-v2`) with its own folder. The old version is kept.
- If quality check fails, return to the relevant earlier stage.

## External tools
OpenArt, Canva, Base44 and Stripe connectors are linked to the owner's account but **not approved for use**. Steps involving them are manual until the owner decides otherwise, and every external action needs per-action owner approval (see `integrations/` and the approval procedure in `CLAUDE.md`).

The live store currently runs on Shopify and is being replaced by Base44 + Stripe. See `docs/migration/shopify-to-base44-stripe.md`.
