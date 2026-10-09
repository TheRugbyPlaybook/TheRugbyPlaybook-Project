# Quality Control

Every book must pass this checklist (`/quality-check`) before it is presented to the owner for approval. Mark each item `PASS`, `FAIL` or `N/A`, with a note.

Each section is a quality gate. Save the evidence for each gate in the book's folder (`books/<age>/<PRODUCT-ID>/`), for example in `quality-report.md`.

## 0. Learning outcomes
- [ ] The approved brief lists 3–5 measurable learning outcomes
- [ ] Each outcome is mapped to the pages that teach it
- [ ] The book ends with a recap or check that matches the outcomes

## 1. Age-appropriateness
- [ ] Word count per page and page count match `age-groups/<age>.md`
- [ ] Vocabulary and sentence length suit the reading level
- [ ] Concepts and rugby content suit the age group

## 2. Rugby accuracy and safety
- [ ] Terminology and laws are correct (region / law source: `TO BE CONFIRMED`)
- [ ] Techniques are shown and described correctly
- [ ] Contact and tackling are safe, or absent where required (always absent for 3-6)
- [ ] Drills include safety notes where needed
- [ ] Health / injury content is general and responsible (not medical advice)
- [ ] Law sources named and cited in the evidence (e.g. World Rugby laws, national age-grade rules: `TO BE CONFIRMED`)
- [ ] Reviewed and signed off by a qualified rugby coach or referee (reviewer: `TO BE CONFIRMED`)

## 3. Inclusion and messaging
- [ ] Diverse, inclusive representation
- [ ] No stereotypes, put-downs or exclusionary language
- [ ] Positive values: teamwork, respect, fair play

## 4. Consistency
- [ ] Characters match `characters/character-bible.md` and are all approved
- [ ] Illustrations match the text on each page
- [ ] Visual style, colours and fonts follow `brand/` (once confirmed)
- [ ] Product ID and file names follow `docs/naming-conventions.md`

## 5. Originality and copyright
- [ ] Text, title and storyline are original and not close to any competitor or existing work
- [ ] Characters are original (no resemblance to competitors, real people or existing IP)
- [ ] Illustrations and prompts do not imitate competitor art or named living artists
- [ ] Layouts are not copied from distinctive competitor designs
- [ ] No real players, teams, logos or trademarks without permission
- [ ] Commercial-use rights confirmed for fonts, images and tools

## 6. Editorial
- [ ] Two proofreading passes completed, at least one by a human
- [ ] Spelling and grammar checked (spelling convention: `TO BE CONFIRMED`)
- [ ] No placeholder text and no `TO BE CONFIRMED` left in content
- [ ] Page numbering and order are correct
- [ ] Title page, copyright page and credits present (copyright page wording: `TO BE CONFIRMED`)

## 6a. Accessibility
- [ ] Text contrast at least 4.5:1 against its background
- [ ] Minimum body font size met for the age group (size: `TO BE CONFIRMED`)
- [ ] Meaning is never carried by colour alone
- [ ] Reading order is logical; images have alt text; PDF is tagged where the export tool allows (feasibility from Canva: `TO BE CONFIRMED`)

## 6b. Layout
- [ ] Built on the approved Canva template
- [ ] Margins, bleed and safe areas respected
- [ ] Text matches the approved `content.md` exactly

## 7. Final PDF validation (at export)
- [ ] PDF opens correctly and all pages render
- [ ] All fonts embedded
- [ ] Images are sharp at intended display size (minimum resolution: `TO BE CONFIRMED`)
- [ ] File size within the limit (`TO BE CONFIRMED`)
- [ ] Document metadata set (title, author)
- [ ] Opens correctly on iOS, Android and a desktop PDF reader
- [ ] SHA-256 checksum recorded in `status.md`
- [ ] File named correctly and saved in `output/final/`

## Result
A book with any `FAIL` goes back to the relevant workflow stage. A book with all `PASS` / `N/A` goes to the **owner for explicit approval**. Passing the checklist is not approval.
