# Integration: OpenArt (Illustrations)

> **Status: CONNECTOR LINKED — NOT APPROVED FOR USE.** An OpenArt connector is linked to the owner's claude.ai account, but no use has been approved and the account decisions below are still open. Every write, generation, publication, payment or ad action triggers an approval prompt (`.claude/settings.json`) and needs the owner's explicit approval for that single action; see the external action approval procedure in `CLAUDE.md`. Never store credentials in this repo; use a gitignored `.env` file.

## Role
OpenArt generates book illustrations and character reference images from prompts written in this repo.

## Planned workflow
1. Claude writes the illustration plan and prompts (`/create-illustration`).
2. The owner reviews and approves the prompts.
3. Images are generated in OpenArt (manually, or via the integration once approved).
4. The owner selects images. They are saved to `illustrations/<age>/<PRODUCT-ID>/images/` using the naming conventions.
5. The image status in the illustration plan is updated.

## Decisions
| Item | Decision |
|---|---|
| Account / plan | `TO BE CONFIRMED` |
| Model(s) to use | `TO BE CONFIRMED` |
| Character-consistency method | `TO BE CONFIRMED` |
| Monthly credit budget | `TO BE CONFIRMED` |
| Commercial-use licence terms checked | `TO BE CONFIRMED` |

## Rules
- No competitor images as references. No prompts naming living artists, real players, teams or logos.
- Every image needs owner approval before it is used.
