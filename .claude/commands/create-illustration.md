---
description: Write illustration plans and OpenArt prompts for a book (stage 5)
argument-hint: <PRODUCT-ID> [page numbers]
---

# /create-illustration

Create the illustration plan for **$ARGUMENTS** using the `illustration-production` skill.

## Steps
1. Read the book's `page-plan.md` and content, `brand/visual-style.md`, `brand/colour-system.md` and the relevant character files.
2. Create or update `illustrations/<age>/<PRODUCT-ID>/illustration-plan.md` with, per image:
   - image ID (see `docs/naming-conventions.md`)
   - page, scene description, characters, action, mood, composition, aspect ratio
   - OpenArt prompt text and negative prompt
   - consistency notes (character reference, outfit, colours)
3. Flag any rugby-accuracy or safety issues in the depicted action.
4. Ask the owner to review the plan before any image is generated.

## Rules
- **Do not call OpenArt or spend credits.** Prompts are text only until the owner approves generation.
- Prompts must not name competitor works, real players, team logos or living artists.
- Do not use competitor images as references.
