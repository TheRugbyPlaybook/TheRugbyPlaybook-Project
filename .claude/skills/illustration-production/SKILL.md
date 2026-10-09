---
name: illustration-production
description: Plan TRP illustrations and write OpenArt prompts with character and style consistency. Use for illustration plans, prompts, reference sheets and asset tracking.
---

# Illustration production

Covers the workflow stages **illustration plan → assets**.

## Inputs to read first
- Book `page-plan.md` / `content.md`
- `brand/visual-style.md`, `brand/colour-system.md`
- Relevant `characters/<age>/*.md`
- `integrations/openart.md`

## Folder layout
```
illustrations/<age>/<PRODUCT-ID>/
├── illustration-plan.md   # one entry per image
├── prompts/               # optional: one prompt file per image
└── images/                # generated images, once approved and downloaded
```

## Per-image entry template
```markdown
### <IMAGE-ID>  (e.g. TRP-7-12-PASS-PERFECT-v1-P03-A)
- Page:
- Scene:
- Characters:
- Action (rugby-accurate, safe):
- Mood:
- Composition / aspect ratio:
- Prompt:
- Negative prompt:
- Consistency notes:
- Status: PLANNED | GENERATED | SELECTED | APPROVED
```

## Rules
- **OpenArt use is not approved.** Write prompts as text only. Do not generate images or spend credits without explicit owner approval of that specific generation, after stating its credit cost.
- Do not reference competitor art, named living artists, real players, team kits or logos in prompts.
- Do not use competitor images as reference inputs.
- Show rugby technique correctly and safely, especially tackles and contact.
- Every image needs owner approval before it is used in a final book.
