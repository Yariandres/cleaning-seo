# SEO — mobile cleaning business, Poznań

This repo is the **SEO desk** for a one-person mobile cleaning business in Poznań and the county (sofas, mattresses, rugs, strollers, car seats, car interiors). It works alongside three other repos:

- [cleaning-design](https://github.com/Yariandres/cleaning-design) — the designer (web-designer agent)
- [cleaning-sell-system](https://github.com/Yariandres/cleaning-sell-system) — the developer
- [cleaning-sales](https://github.com/Yariandres/cleaning-sales) — the sales desk (sends "Sales insight: …" issues here: real questions, objections, lost reasons, towns with demand)

## How to work here

- All SEO work goes to the **seo-specialist** agent (`.claude/agents/seo-specialist.md`).
- Read first: `docs/brand.md`, `seo/strategy.md`, `docs/prd.md`, `docs/source/`.
- SEO goes **first** for each page (brief → designer), and **last** before launch (staging audit → fixes to the developer).
- Talk to the others only through GitHub issues: "SEO brief: …" (designer), "SEO note: …" and "SEO fix: …" (developer). Receive "Ready for SEO review: …" and "Sales insight: …" here. The only file you edit in another repo is `docs/seo-requirements.md` in cleaning-sell-system.
- Free data sources for now; paid tools only with the owner's OK.

## How we work: one task at a time, owner reviews

1. Work on **one task** at a time (from "What's next" below, or what the owner asks).
2. Do the research and write the files; commit locally.
3. **Stop and hand over for review:** what you found, what you propose, what you're unsure about, and anything that changes `seo/strategy.md`, a URL or another repo.
4. **Don't push, open issues or edit `docs/seo-requirements.md` in the developer repo until the owner says "go".** If they ask for changes, make them and hand over again.
5. After approval: push, open the issues (SEO brief / SEO note), and update "What's next". Then propose the next task.

## Rules

- Polish search, Polish queries; notes in English.
- Brand voice and final wording belong to the brand strategy: briefs propose terms, headings and FAQ questions, not rewrites.
- No keyword stuffing, doorway pages, fake locations, fake reviews or bought links. No invented volumes or rankings.
- Staging stays noindex; production indexable only on the brand domain.
- Brand: **Nowiutko**, domain **nowiutko.pl** (`docs/brand.md`). Use the exact name everywhere (NAP consistency); never add keywords to the business name on Google Business Profile.

## What's next

0. **Brand search check for "Nowiutko"** (`seo/brand-check.md`): what Google, Maps and AI answers show for the name today; confusable names; GBP naming; anything that argues against it. Report to the owner.
1. Validate the keyword seeds in `seo/strategy.md` and build the keyword map (`seo/keywords/`).
2. Write `docs/seo-requirements.md` in cleaning-sell-system (technical baseline) and send a "SEO note: baseline" issue.
3. SEO brief for the **stroller counter** → "SEO brief: stroller-counter" issue in cleaning-design (the designer's first job).
4. Google Business Profile setup plan (`seo/gbp/`) for the owner.
5. Then briefs for the sofa counter and homepage; audit each page when the developer flags it.
