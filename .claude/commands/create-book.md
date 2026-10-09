---
description: Start a new TRP book — brief, outline and page plan (stages 1–3)
argument-hint: <age-group> <working title>
---

# /create-book

Start a new book for **$ARGUMENTS** using the `book-production` skill.

## Steps
1. Read `CLAUDE.md`, `docs/workflow.md`, `docs/naming-conventions.md` and the matching `age-groups/<age>.md`.
2. Confirm the age group (`3-6`, `7-12`, `12-plus`) and working title. If either is missing, ask.
3. Propose a product ID, e.g. `TRP-7-12-PASS-PERFECT-v1`. Check that no folder with that ID already exists in `books/<age>/`.
4. Create `books/<age>/<PRODUCT-ID>/` containing:
   - `brief.md`: audience, learning goal, rugby skill focus, tone, length, characters used, open questions
   - `outline.md`: (after the owner agrees the brief) story or chapter structure
   - `page-plan.md`: (after the owner agrees the outline) one row per page: text summary, illustration idea, layout note
   - `status.md`: product ID, state `DRAFT`, current stage, approval log
5. Stop after each stage and ask the owner to review before moving on.

## Rules
- State is always `DRAFT`. Never set `READY` or `PUBLISHED`.
- Use only approved characters from `characters/`. Unapproved characters must be marked `PROPOSED`.
- Follow the originality rules in `CLAUDE.md` §8.
- Do not contact external services.
