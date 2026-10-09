---
description: Run the TRP quality checklist on a book (stage 7)
argument-hint: <PRODUCT-ID>
---

# /quality-check

Run the quality check for **$ARGUMENTS**.

## Steps
1. Read `docs/quality-control.md` and every file in the book folder.
2. Work through every checklist item. Mark each as `PASS`, `FAIL` or `N/A` with a short note.
3. Write the report to `books/<age>/<PRODUCT-ID>/quality-report.md` with the date.
4. Summarise blocking issues first, then minor issues.
5. If all items pass, tell the owner the book is **ready for their review**. Do not change the state to `READY`; only the owner's approval does that.

## Rules
- Be strict. If in doubt, mark `FAIL` and explain why.
- Include the originality check (CLAUDE.md §8).
