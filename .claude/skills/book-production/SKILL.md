---
name: book-production
description: Produce a TRP rugby eBook from brief to page content, following the TRP workflow, age-group guides and approval gates. Use when creating, outlining, planning or writing a book.
---

# Book production

## Workflow
```
brief → outline → page plan → content → illustration plan → assets → quality check → approval → final export
```
This skill covers **brief → outline → page plan → content**. It hands off to `illustration-production` (illustration plan, assets) and `publishing` (export).

## Inputs to read first
- `CLAUDE.md`
- `age-groups/<age>.md`: word counts, page counts, reading level, rugby content limits
- `brand/brand-bible.md`: voice and tone
- `characters/character-bible.md`: approved characters only
- `docs/naming-conventions.md`

## Book folder layout
```
books/<age>/<PRODUCT-ID>/
├── status.md          # product ID, state, stage, approval log
├── brief.md
├── outline.md
├── page-plan.md
├── content.md
├── quality-report.md  # from /quality-check
└── listing.md         # from /export-book
```

## status.md template
```markdown
# <PRODUCT-ID>
- Title: <working title>
- Age group: <3-6 | 7-12 | 12-plus>
- State: DRAFT
- Current stage: brief
- Created: YYYY-MM-DD

## Approval log
| Date | Stage | Decision | Owner wording |
|---|---|---|---|
```

## Gates
- Stop at the end of each stage for owner review. Record approvals in `status.md`.
- Never set the state beyond `DRAFT`.

## Writing rules
- Keep the text original, age-appropriate and rugby-accurate, with safety first.
- Follow `CLAUDE.md` §8 for originality.
- Mark unknowns `TO BE CONFIRMED`. Never invent brand decisions.
