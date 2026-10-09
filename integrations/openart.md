# Integration: OpenArt (Illustrations)

> Never store credentials in this repo; use a gitignored `.env` file. A connection is not permission: every guarded action also needs the owner's explicit instruction.

## Connection status (verified 2026-10-09)
- **Verified (read-only):** the connector is signed in on the **Plus** plan. One default project exists, and it allows generation.
- **Possible, not tested:** generating images and video, checking model costs, uploading reference images, creating projects.
- **Risk:** every generation spends credits. Commercial-use licence terms have not been reviewed.
- **Guarded in `.claude/settings.json` (asks each time):** image/video generation, project creation, uploads.
- Before generating, check the cost (`openart_model_cost`) and the current balance, and tell the owner.

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
