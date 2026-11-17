# SEO — mobile cleaning business, Poznań

This repo is the **SEO desk** for a one-person mobile cleaning business in Poznań and the county (sofas, mattresses, rugs, strollers, car seats, car interiors). It works alongside three other repos:

- [cleaning-design](https://github.com/Yariandres/cleaning-design) — the designer (web-designer agent)
- [cleaning-sell-system](https://github.com/Yariandres/cleaning-sell-system) — the developer
- [cleaning-sales](https://github.com/Yariandres/cleaning-sales) — the sales desk (sends "Sales insight: …" issues here: real questions, objections, lost reasons, towns with demand)

## How to work here

- **Workflow change (owner, 17 Nov 2026): the designer is paused.** You now **write the page copy as well as the SEO requirements**, and send pages straight to the developer as **"Page spec: <page>"** issues (label `page-spec`) in cleaning-sell-system, linking `seo/pages/<page>.md`. A page spec holds: URL, title, meta description, H1, every section in order with its final Polish copy, FAQ, internal links, structured data, image alts, and which existing component each section reuses (counter template, stroller page, homepage v0, footer). Write in the brand voice (`docs/brand.md`, `docs/source/customer-stories-and-copy.md`): "Ty" voice, freshness, true promises only; doubtful wording → a "Brand: …" issue here. Owner approves each spec before "go". Copy fixes to live pages go the same way. No new "SEO brief" issues to the designer while it's paused.
- All SEO work goes to the **seo-specialist** agent (`.claude/agents/seo-specialist.md`).
- Read first: `docs/brand.md`, `seo/strategy.md`, `docs/prd.md`, `docs/source/`.
- SEO goes **first** for each page (page spec → developer; while the designer is paused, no brief → designer), and **last** before launch (staging audit → fixes to the developer).
- Talk to the others only through GitHub issues: "Page spec: …", "SEO note: …" and "SEO fix: …" (developer); "SEO brief: …" (designer) only once the designer is back. Receive "Ready for SEO review: …" and "Sales insight: …" here. The only file you edit in another repo is `docs/seo-requirements.md` in cleaning-sell-system.
- Free data sources for now; paid tools only with the owner's OK.

## How we work: one task at a time, owner reviews

1. Work on **one task** at a time (from "What's next" below, or what the owner asks).
2. Do the research and write the files; commit locally.
3. **Stop and hand over for review:** what you found, what you propose, what you're unsure about, and anything that changes `seo/strategy.md`, a URL or another repo.
4. **Don't push, open issues or edit `docs/seo-requirements.md` in the developer repo until the owner says "go".** If they ask for changes, make them and hand over again.
5. After approval: push, open the issues (Page spec / SEO note), and update "What's next". Then propose the next task.

- **Brand problems** (name, tagline, voice, offers, prices, messaging, leftover placeholders): open a "Brand: …" issue with label `brand` in this repo, as described in `docs/brand.md` → "Raising a brand issue". The owner takes them to the brand strategist.

## Rules

- Polish search, Polish queries; notes in English.
- You write the copy (see the workflow change above); brand rules, the master promise and disputed wording stay with the brand strategist via "Brand: …" issues.
- No keyword stuffing, doorway pages, fake locations, fake reviews or bought links. No invented volumes or rankings.
- Staging stays noindex; production indexable only on the brand domain.
- Brand: **Nowiutko**, domain **nowiutko.pl** (`docs/brand.md`). Use the exact name everywhere (NAP consistency); never add keywords to the business name on Google Business Profile.

## What's next

**0. PRIORITY — early launch (owner, 15 Nov 2026):** the stroller page goes live on nowiutko.pl by Fri 20 Nov, booking by phone + WhatsApp only. Do [#2](https://github.com/Yariandres/cleaning-seo/issues/2) first: early-launch checklist (SEO note to the developer), homepage v0 page spec (developer), production audit right after go-live. The Google Business Profile plan is parked (below). Everything below waits until then.
   - ✅ Early-launch checklist: `seo/notes/early-launch-checklist.md`, approved 16 Nov, sent as "SEO note: early launch" (cleaning-sell-system #10); designer's four `stroller-v1.1` questions answered on #2.
   - ✅ Homepage v0 brief: `seo/briefs/homepage-v0.md`, approved 16 Nov, sent as "SEO brief: homepage-v0" (cleaning-design #7). **Superseded (17 Nov)** by the page spec below; the designer's `homepage-v0` handoff exists and is the visual reference.
   - **In review:** homepage page spec `seo/pages/homepage.md` (drafted 17 Nov, committed locally, not sent). After the owner's "go": issue "Page spec: homepage" (label `page-spec`) in cleaning-sell-system. Note for the owner: the 17 Nov brand decision replaced "wkrótce" with "Wycena na WhatsApp"; the spec follows it, with "wkrótce" as a fallback (spec §6, §15 q1).
   - **Parked by the owner (17 Nov):** Google Business Profile plan (`seo/gbp/`). Do not start it until the owner un-parks it.
   - **Next:** production audit after go-live.
   - Open with the owner: `ai-train` (robots.txt `Content-Signal`); whether to keep `Disallow: /admin` next to the `noindex` header (SEO would drop the disallow).

**Done**
- ✅ Keyword seeds validated, keyword map built: `seo/keywords/keyword-map.md` (8 Nov; strategy updated 10 Nov).
- ✅ Stroller counter brief: `seo/briefs/stroller-counter.md`, approved 10 Nov, sent to the designer as "SEO brief: stroller-counter" in cleaning-design (link in the brief's header).
- ✅ Staging audit of `stroller-v1` (15 Nov): `seo/audits/2026-11-15-stroller-v1-staging.md`. No P0s; fixes filed as cleaning-sell-system #3, #4 (P1), #5, #6 (P2); summary on cleaning-seo #1.

**Waiting on others**
- Developer: P1 fixes #3 and #4 → then close cleaning-seo #1. Production audit when #45 lands (LocalBusiness, sitemap, og:image, redirects, PageSpeed mobile, Rich Results Test).
- Owner: confirm the car-seat brands named (only Cybex and Maxi-Cosi checked), the mould answer, the "3–5 godzin" drying time, and the `ai-train` choice for robots.txt `Content-Signal`.

**Next, in order** (one at a time, owner reviews each — see "How we work")
1. **Brand search check for "Nowiutko"** (`seo/brand-check.md`): what Google, Maps and AI answers show for the name today; confusable names; GBP naming; anything that argues against it. Report to the owner.
2. **Technical baseline:** refine `docs/seo-requirements.md` in cleaning-sell-system (the developer wrote a starting version from the PRD; it's ours to own) and send a "SEO note: baseline" issue. Must include: the stroller URL change to `/poznan/pranie-wozkow-i-fotelikow` (the PRD still says `/poznan/pranie-wozkow`), staging `noindex`, server rendering, sitemap, canonical on nowiutko.pl, structured data (LocalBusiness as a service-area business, Service + Offer with `minPrice`, FAQPage, BreadcrumbList), no AggregateRating without real reviews.
3. **Google Business Profile plan** (`seo/gbp/`) for the owner — **PARKED by the owner, 17 Nov**; when un-parked, include stroller and car-seat services with prices, because "pranie fotelika samochodowego poznań" is won in the map pack.
4. **Ask the owner for a Google Keyword Planner export** for the queries in the keyword map (free Google Ads account) — we still have no volumes.
5. Then page specs for the **sofa counter** and the full **homepage** (while the designer is paused; briefs to the designer only once it is back); audit each page when the developer flags it.
6. Later, not v1: one guide "Jak prać fotelik samochodowy" for the DIY brand queries (keyword map §3).
