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

- **Brand problems** (name, tagline, voice, offers, prices, messaging, leftover placeholders): open a "Brand: …" issue with label `brand` in this repo, as described in `docs/brand.md` → "Raising a brand issue". The owner takes them to the brand strategist.

## Rules

- Polish search, Polish queries; notes in English.
- Brand voice and final wording belong to the brand strategy: briefs propose terms, headings and FAQ questions, not rewrites.
- No keyword stuffing, doorway pages, fake locations, fake reviews or bought links. No invented volumes or rankings.
- Staging stays noindex; production indexable only on the brand domain.
- Brand: **Nowiutko**, domain **nowiutko.pl** (`docs/brand.md`). Use the exact name everywhere (NAP consistency); never add keywords to the business name on Google Business Profile.

## What's next

**Done**
- ✅ Keyword seeds validated, keyword map built: `seo/keywords/keyword-map.md` (8 Nov; strategy updated 10 Nov).
- ✅ Stroller counter brief: `seo/briefs/stroller-counter.md`, approved 10 Nov, sent to the designer as "SEO brief: stroller-counter" in cleaning-design (link in the brief's header).

**Next, in order** (one at a time, owner reviews each — see "How we work")
1. **Brand search check for "Nowiutko"** (`seo/brand-check.md`): what Google, Maps and AI answers show for the name today; confusable names; GBP naming; anything that argues against it. Report to the owner.
2. **Technical baseline:** write `docs/seo-requirements.md` in cleaning-sell-system and send a "SEO note: baseline" issue. Must include: the stroller URL change to `/poznan/pranie-wozkow-i-fotelikow` (the PRD still says `/poznan/pranie-wozkow`), staging `noindex`, server rendering, sitemap, canonical on nowiutko.pl, structured data (LocalBusiness as a service-area business, Service + Offer with `minPrice`, FAQPage, BreadcrumbList), no AggregateRating without real reviews.
3. **Google Business Profile plan** (`seo/gbp/`) for the owner — include stroller and car-seat services with prices, because "pranie fotelika samochodowego poznań" is won in the map pack.
4. **Ask the owner for a Google Keyword Planner export** for the queries in the keyword map (free Google Ads account) — we still have no volumes.
5. Then briefs for the **sofa counter** and **homepage**; answer the designer's questions on the stroller brief issue; audit each page when the developer flags it.
6. Later, not v1: one guide "Jak prać fotelik samochodowy" for the DIY brand queries (keyword map §3).
