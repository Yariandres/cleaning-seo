# SEO — mobile cleaning business, Poznań

This repo is the **SEO desk** for a one-person mobile cleaning business in Poznań and the county (sofas, mattresses, rugs, strollers, car seats, car interiors). It works alongside three other repos:

- [cleaning-design](https://github.com/Yariandres/cleaning-design) — the designer (web-designer agent)
- [cleaning-sell-system](https://github.com/Yariandres/cleaning-sell-system) — the developer
- [cleaning-sales](https://github.com/Yariandres/cleaning-sales) — the sales desk (sends "Sales insight: …" issues here: real questions, objections, lost reasons, towns with demand)

## How to work here

- All SEO work goes to the **seo-specialist** agent (`.claude/agents/seo-specialist.md`).
- Read first: `seo/strategy.md`, `docs/prd.md`, `docs/source/`.
- SEO goes **first** for each page (brief → designer), and **last** before launch (staging audit → fixes to the developer).
- Talk to the others only through GitHub issues: "SEO brief: …" (designer), "SEO note: …" and "SEO fix: …" (developer). Receive "Ready for SEO review: …" and "Sales insight: …" here. The only file you edit in another repo is `docs/seo-requirements.md` in cleaning-sell-system.
- Free data sources for now; paid tools only with the owner's OK.

## Rules

- Polish search, Polish queries; notes in English.
- Brand voice and final wording belong to the brand strategy: briefs propose terms, headings and FAQ questions, not rewrites.
- No keyword stuffing, doorway pages, fake locations, fake reviews or bought links. No invented volumes or rankings.
- Staging stays noindex; production indexable only on the brand domain.
- Brand name not chosen yet: `[Nazwa firmy]`.

## What's next

1. Validate the keyword seeds in `seo/strategy.md` and build the keyword map (`seo/keywords/`).
2. Write `docs/seo-requirements.md` in cleaning-sell-system (technical baseline) and send a "SEO note: baseline" issue.
3. SEO brief for the **stroller counter** → "SEO brief: stroller-counter" issue in cleaning-design (the designer's first job).
4. Google Business Profile setup plan (`seo/gbp/`) for the owner.
5. Then briefs for the sofa counter and homepage; audit each page when the developer flags it.
