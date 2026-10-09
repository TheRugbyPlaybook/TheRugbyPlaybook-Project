---
description: Draft a new TRP character profile for owner approval
argument-hint: <age-group> <character concept>
---

# /create-character

Draft a character for **$ARGUMENTS** using the `character-production` skill.

## Steps
1. Read `CLAUDE.md`, `characters/character-bible.md`, `brand/visual-style.md` and the matching `age-groups/<age>.md`.
2. Check the character bible for overlap with existing characters (name, role, look, personality).
3. Create `characters/<age>/<character-slug>.md` using the template in `characters/character-bible.md`.
4. Set **Status: PROPOSED**. Never mark a character as approved.
5. List open questions and anything marked `TO BE CONFIRMED`.
6. Ask the owner to review. Add the character to the bible index only after explicit approval.

## Rules
- The character must be original. It must not resemble competitor characters, real players or existing franchises.
- Use inclusive, positive representation that suits the age group.
- Do not generate images. Reference sheets are produced later via `/create-illustration`.
