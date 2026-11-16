# SEO mini brief: homepage v0

| | |
|---|---|
| URL | `/` (`https://nowiutko.pl/`) |
| Status | **Draft 16 Nov 2026, for owner review.** Not sent. After approval: "SEO brief: homepage-v0" in cleaning-design. |
| For | Early launch, target Fri 20 Nov 2026. Owner priority cleaning-seo [#2](https://github.com/Yariandres/cleaning-seo/issues/2), task 2 · designer scope cleaning-design [#5](https://github.com/Yariandres/cleaning-design/issues/5), item 2 · developer scope cleaning-sell-system [#8](https://github.com/Yariandres/cleaning-sell-system/issues/8), checklist [#10](https://github.com/Yariandres/cleaning-sell-system/issues/10) |
| Replaces | The "Wkrótce otwieramy" placeholder now at `/` |
| Not this | The full homepage (PRD S1, "reception desk"). That gets its own brief and its own research later; see §1. |
| Brand | **Nowiutko** (`docs/brand.md`). All Polish strings below are **proposals**; final wording is the brand strategy's. |

**One decision is the owner's and changes the title, H1 and one section: §6 (are the other services shown).** Everything else can be designed now. Strings that depend on it are marked **[B]** (other services named, my recommendation) and **[A]** (strollers and car seats only).

## 1. Purpose and target queries

**What v0 is for.** Three jobs, in this order:
1. **Answer a search for the name.** Someone who heard "Nowiutko" from a neighbour, a Facebook post or the Business Profile must find out in one screen what it is, where it works and how to book.
2. **Give the stroller page its one internal link.** At launch nothing else on the site links to `/poznan/pranie-wozkow-i-fotelikow` (the `/cennik` and service-area links are out until those pages exist).
3. **Tell Google what the site is called.** Google takes the site name from the home page: `WebSite` structured data first, then `og:site_name`, `<title>` and headings ([Site names](https://developers.google.com/search/docs/appearance/site-names)).

**Target queries**

| Query (PL) | Type | Source | Volume |
|---|---|---|---|
| **Nowiutko** | **primary** (brand, navigational) | Google results page and autocomplete, read 16 Nov 2026 (below) | unknown; a new name, so close to none today |
| nowiutko poznań · nowiutko pranie · nowiutko.pl | secondary (brand + qualifier) | none: autocomplete suggests nothing for them yet (16 Nov). They are what a person types after hearing the name, not measured demand | unknown |

**What Google shows for "nowiutko" today** (google.com, `hl=pl&gl=pl`, read 16 Nov 2026 in the browser on the owner's computer; results vary by place and person; this is a quick read, not the full brand check, which is still on the list):
- An **AI Overview that defines the word** ("potoczny przysłówek … bardzo nowo, świeżo"), then dictionary and crossword pages. **No business, no map result, no other company called Nowiutko** on the first page.
- Autocomplete for "nowiutko" offers only word forms (nowiutki, nowiutka …).
- What that means: the name is an ordinary Polish word, so Google has no reason yet to treat it as a business. The home page has to say plainly, in text and in markup, that Nowiutko is a cleaning service in Poznań. The Business Profile (task 3) does the other half.

**What v0 must NOT target yet**

| Query | Why not on v0 | Where it goes |
|---|---|---|
| pranie tapicerki poznań · pranie tapicerki z dojazdem do klienta | The keyword map gives these to the **homepage**, and that stays true. But they need a page that proves it: prices, proof, links to the sofa and car counters. v0 has none of that. A short page with the phrase in its title would not rank and would set the wrong first impression in Google. | The full homepage brief |
| pranie wózków dziecięcych poznań and the stroller group | Owned by the stroller counter. v0 names the service once and links; it does not repeat the counter's H1, prices table or FAQ. | Stroller counter |
| pranie kanapy / materaca / tapicerki samochodowej poznań, town queries | Owned by pages that don't exist yet. | Their counters; service-area page |

Under [B] the words "pranie tapicerki" still appear, because they are in the brand's own tagline. That describes the business; it is not an attempt to rank, and no success measure hangs on it.

**How v0 differs from the full homepage, so nothing here boxes it in**
- Same URL (`/`), so no redirect later. Title, H1, outline and markup are all replaced by the full brief.
- v0 has **no** menu of outcomes, package tiles, "wanted now" item, proof section, reviews, FAQ or town list. The full homepage has them (PRD S1).
- No decision here about navigation, tiles or the "pranie tapicerki poznań" strategy carries over. `seo/strategy.md` and the keyword map are unchanged.

## 2. Title tag and meta description (proposals)

**Title** (the home page title is written out in full; the template must **not** append " – Nowiutko" to it):
- **[B]** `Nowiutko – pranie tapicerki, wózków i aut u Ciebie | Poznań` (59)
- **[A]** `Nowiutko – pranie wózków i fotelików u Ciebie | Poznań` (54)

The name goes first: this page answers the brand query, and the title is one of the places Google reads the site name from. [B] is the brand's descriptive tagline plus the city. Google's guidance says the home page title is the right place for a little more than the name ([Title links](https://developers.google.com/search/docs/appearance/title-link)).

**Meta description** (≤ 155):
- **[B]** `Nowiutko: pierzemy wózki, foteliki, kanapy, materace i wnętrza aut u Ciebie, w Poznaniu i okolicach. Wyślij zdjęcia na WhatsApp – podamy cenę.` (142)
- **[A]** `Nowiutko: pierzemy wózki dziecięce i foteliki samochodowe u Ciebie w domu, w Poznaniu i okolicach. Wyślij zdjęcia na WhatsApp – podamy cenę.` (140)

No price in either: v0 has no single "od" price that covers the page.

## 3. H1 and outline (proposals)

**H1** (one, real text, contains the name):
- **[B]** `Nowiutko – pranie tapicerki, wózków i aut u Ciebie w Poznaniu i okolicach` (the tagline + the area)
- **[A]** `Nowiutko – pranie u Ciebie w domu, w Poznaniu i okolicach`

Same pattern as the stroller page (its option a): the H1 may be styled as the small eyebrow, with the brand's voice line *Świeżo i jak nowe — bez wychodzenia z domu.* as the big headline in a `<p>`. Or the H1 is the headline itself. Either is fine for SEO; designer's choice.

Under [A] I kept "wózków i fotelików" **out** of the H1 on purpose: `Nowiutko – pranie wózków i fotelików … w Poznaniu i okolicach` would be nearly the stroller page's H1, and the two pages would compete for the same query. This is one of the reasons I recommend [B].

**Outline** (short page; four sections and the footer)

| # | Section | Heading | Content |
|---|---|---|---|
| 0 | Header | none | Shared pattern: logo, phone (`tel:`), WhatsApp button. No menu: there is nothing to list yet. |
| 1 | Hero | **H1** + voice line | One or two sentences: what Nowiutko is and that we come to the customer with our own equipment. WhatsApp button, phone number as visible text. |
| 2 | Services | H2, e.g. `Co pierzemy` | The stroller card with the link (§4). Under [B], the other services as plain text and one sentence on how to ask (§6). |
| 3 | How to book | H2, e.g. `Jak to działa` | The three steps, reused from the stroller page in short form: photos on WhatsApp → price → we come to you. |
| 4 | Area | H2, e.g. `Gdzie dojeżdżamy` | One or two sentences: Poznań and powiat poznański, mobile service. Town names only from `{zones}` data, as on the stroller page, in a sentence or the existing zone component. Not a wall of towns. |
| 5 | Final CTA | H2, same component as the stroller page | The master promise (PRD S9), WhatsApp button, call button, SMS line. |
| 6 | Footer | none | Shared footer, unchanged. |

No FAQ, no reviews strip, no before/after, no packages on v0. If the stroller card has a title, it is an H3. No heading per unbuilt service.

## 4. Links

**Internal**

| To | Rule |
|---|---|
| `/poznan/pranie-wozkow-i-fotelikow` | **Required: at least one normal `<a href>` in the page body, in the server HTML, with words as its text.** This is the stroller page's only internal inbound link at launch. Google only reliably follows `<a href>` links and reads the anchor text to understand the target; "every page you care about should have a link from at least one other page" ([Link best practices](https://developers.google.com/search/docs/crawling-indexing/links-crawlable)). |
| `/polityka-prywatnosci` | Footer "Prywatność"; cookie banner "Szczegóły" → `#cookies`. As already built. |
| `/` | The header logo may link to `/` or be plain on this page; either is fine. |

**Anchor text for the stroller link (proposals)**
- Main (card title or the link inside the card): `Pranie wózków i fotelików`
- If a second link sits in running text: `pranie wózków dziecięcych i fotelików samochodowych`
- Optional third, to the price section: `Cennik prania wózków i fotelików` → `/poznan/pranie-wozkow-i-fotelikow#cennik`
- Not as the only link text: "Zobacz", "Więcej", "Sprawdź", an arrow, or an icon alone. If the whole card is one link, its text must still contain the service name. Two or three links to the same page are plenty.

**Contact (not pages)**
- WhatsApp: `https://wa.me/48736369704?text=…`, `rel="noopener"`, **no `nofollow`** (as answered on #2).
- Phone: `tel:+48736369704`, shown as "736 369 704". SMS: `sms:+48736369704` if the final CTA line is reused.
- The homepage needs **its own prefilled WhatsApp message**. The stroller one says "wózka lub fotelika", which is wrong for someone asking about a sofa. Proposal: `Dzień dobry, proszę o wycenę prania. Wysyłam zdjęcia. Miejscowość: ` (wording for the brand strategist).

**Must not appear:** links to `/cennik`, `/poznan/obszar-dzialania`, `/poznan/wycena`, any other counter, `/regulamin`, `/cookies`; `href="#"` or empty links; "coming soon" pages; social icons (no profiles exist yet). The Business Profile link is added when the profile exists.

## 5. Indexable: yes

`index, follow` (no robots meta needed), self-canonical `https://nowiutko.pl/`, listed in the sitemap, answers 200. This matches checklist items 1, 3, 4 and 6. Reasons:
- Google needs a crawlable, indexable home page to work out the site name ([Site names](https://developers.google.com/search/docs/appearance/site-names): the home page must not be blocked by robots.txt or `noindex`).
- It is the landing page for the brand search, and the only internal link to the stroller page. A `noindex` home page would leave the stroller page with no indexed page pointing at it.
- The risk of indexing a small page is that it is thin. §9 is the answer to that: it is short, but it answers what a searcher of the name wants.

Staging stays `noindex`, as now.

## 6. Unbuilt services: how they show

Sofas, armchairs, mattresses, rugs and car interiors have no pages yet. Options:

| Option | What the visitor sees | SEO effect | Honesty |
|---|---|---|---|
| **A. Not shown** | Only strollers and car seats. | Safe, but the homepage becomes a smaller copy of the stroller page: same topic, same area. The two compete, and Google and AI answers learn "Nowiutko = stroller cleaning" for now. The brand tagline ("tapicerki, wózków i aut") then says more than the page does. | Fully honest about what the site sells today. |
| **B. Named as plain text, with "ask on WhatsApp"** *(recommended, if the owner confirms)* | The stroller card with a link, then one short block: the other services by name, and one sentence saying the price comes from photos on WhatsApp or by phone. | The homepage gets its own subject (the whole business), so it does not compete with the stroller page. Google and AI answers see what Nowiutko does. No URLs are created, so there is nothing thin to index and nothing to redirect later. It does **not** make the page rank for sofa or car queries; those wait for their counters. | Honest **only if** the owner really takes these jobs now. |
| C. Links to "coming soon" pages, or tiles linking to empty URLs | Tiles that go somewhere empty. | **Rejected.** Empty pages are thin content, waste the first crawl of a new site, and break checklist item 2 (nothing unbuilt is reachable). | Promises pages that don't exist. |
| D. Greyed-out tiles marked "wkrótce" | Things you can't have. | Harmless to Google, but it tells a brand-new visitor the business isn't ready, when in fact the owner can do the job today. | Misleading in the other direction. |

**Recommendation: B.** Rules for it:
- **Plain text, not links.** A simple list, one line per service, no paragraph each (that copy belongs to the future counters), no H3 per service, no styling that looks clickable.
- Proposed names, from the price list: `Kanapy, narożniki i fotele` · `Materace` · `Dywany` · `Tapicerka samochodowa (wnętrze auta)`. Only the ones the owner confirms.
- One sentence with the route, e.g. `Kanapę, materac, dywan albo wnętrze auta też pierzemy u Ciebie. Wyślij zdjęcia na WhatsApp – podamy cenę.` (proposal).
- **No "wkrótce", no "strony w przygotowaniu".** The services are available; only their web pages aren't.
- No prices for these on v0 unless the owner wants them **and** they come from the production price list (never typed into the page). My suggestion: leave them out; the price is the reason to send photos.
- When a counter ships, its line becomes a link with descriptive anchor text. Nothing else changes.

**This is the owner's (and sales desk's) decision, not mine:** whether sofa, mattress, rug and car jobs are really accepted by WhatsApp from 20 Nov, and which ones. If the answer is "strollers and car seats only for now", use **A** and the [A] strings; the page is still valid. Note for the decision: the home plan names "the sofa before Christmas" as the seasonal item until 20 December.

## 7. Structured data for `/`

One JSON-LD graph, server-rendered.

| Node | Requirement |
|---|---|
| **LocalBusiness** | **The same node as on the stroller page, from the same source**: `@id` `https://nowiutko.pl/#business`, `name` `Nowiutko`, `url`, `telephone` `+48736369704`, `areaServed` list from the towns data, locality-only `address`, `logo`/`image`. Exactly as checklist item 7. Nothing added for the homepage. |
| **WebSite** | **Yes.** `@id` `https://nowiutko.pl/#website`, `name`: `Nowiutko`, `url`: `https://nowiutko.pl/`, `inLanguage`: `pl-PL`, `publisher`: `{"@id": "https://nowiutko.pl/#business"}`. Google names `WebSite` on the home page as the most important input for the site name. The module already outputs a WebSite node; check that `name` is exactly `Nowiutko` (not the page title, not "nowiutko.pl"). **No `alternateName`** (the brand has one spelling; `docs/brand.md` rules out "Nowiutko.pl" as a name). **No `SearchAction`** (the site has no search). |
| **WebPage** | The module default is fine. |
| **Service / Offer** | **None on `/`.** The stroller Service and its Offers live on the stroller page only. |
| **BreadcrumbList** | **None.** The home page is the top of the trail. |
| **FAQPage** | **None**, because v0 has no visible FAQ. |
| **AggregateRating / Review** | **None**, anywhere, until real reviews exist. |

Also: `og:site_name` = `Nowiutko` (checklist item 9) and the logo's `alt="Nowiutko"`.

## 8. Open Graph and share image

| Tag | Value (proposal) |
|---|---|
| `og:title` | **[B]** `Nowiutko – pranie tapicerki, wózków i aut u Ciebie` (50) · **[A]** `Nowiutko – pranie wózków i fotelików u Ciebie` |
| `og:description` | The meta description |
| `og:url` | `https://nowiutko.pl/` |
| `og:type` / `og:site_name` / `og:locale` | `website` / `Nowiutko` / `pl_PL` |
| `twitter:card` | `summary_large_image` |
| `og:image` | Checklist item 12: one static 1200 × 630 file on nowiutko.pl, absolute HTTPS URL, with `og:image:width`, `og:image:height`, `og:image:alt`. Suggested file name `og-nowiutko-1200x630.png`. |

**Share image:** the designer's existing **no-photo variant**, with the homepage's own text. Proposals for the copy keys:
- `og.title` (text in the image; the logo supplies the name): **[B]** `Pranie tapicerki, wózków i aut u Ciebie` · **[A]** `Pranie u Ciebie w domu`
- `og.line`: `Poznań i okolice · bez wychodzenia z domu`
- `og.alt`: **[B]** `Nowiutko: pranie tapicerki, wózków i aut u Ciebie. Poznań i okolice.`

No price and no phone number inside the image (both can change). One image is enough: the template is already safe in a centre-square crop, so no second square file. **Ship it with the launch if possible**: WhatsApp and Facebook keep the first preview they fetch, and the home page URL is the one that gets shared when someone says "look up Nowiutko".

## 9. Minimum content (so the page is small, not thin)

All of it as real text in the server HTML, readable without JavaScript:

1. **The name:** Nowiutko, in the H1, the title and the logo alt.
2. **What it is,** in one or two sentences: a mobile cleaning service; we come to your home with our own equipment.
3. **What can be booked:** strollers and car seats, with the link; under [B] the other services by name.
4. **Where:** Poznań and powiat poznański (the county), stated in words.
5. **How to book:** photos on WhatsApp → price → visit. The WhatsApp button and the **phone number visible as text**, not only behind an icon.
6. **The master promise** (PRD S9): *Przyjeżdżamy na czas. Płacisz tyle, ile podaliśmy ze zdjęć. Jeśli coś wyjdzie po wyschnięciu, wracamy za darmo.*
7. **NAP, exactly:** name **Nowiutko** (no city, no keywords, no ".pl") · phone **+48 736 369 704** (shown "736 369 704") · area **Poznań i okolice**. No street address unless the owner decides to publish one. The same three everywhere: page, footer, JSON-LD, later the Business Profile.

**Must not be added to fill space:** reviews, star ratings or customer counts; stock photos or photos of other people's work; opening hours (none are set); "ubezpieczenie OC" or any other claim the owner hasn't confirmed; a block of town names; a paragraph of keywords. A list of towns a page wants to rank for is Google's own example of keyword stuffing ([Spam policies](https://developers.google.com/search/docs/essentials/spam-policies)).

Other basics, same as the stroller page: `<html lang="pl-PL">`, one H1, the page works at 375 px, no layout shift from the cookie banner, no photo needed for launch.

## 10. Open questions

**For the owner**
1. **§6: A or B?** From 20 Nov, do you take sofa, armchair, mattress, rug and car-interior jobs by WhatsApp and phone? Which ones may the homepage name?
2. If B: prices for those services on v0, or "price from photos" only? (My suggestion: no prices on v0.)
3. The "sofa before Christmas" item: do you want it on v0 at all? It needs B. I would keep v0 plain and leave the seasonal item to the full homepage.
4. Still open from the stroller handover and relevant here too: registered name and NIP for the footer; whether "Cenę podamy dziś" is true in the evening and on Sunday (the homepage reuses the steps).

**For the designer**
1. H1 as the eyebrow with the voice line as the headline, or the H1 as the headline: your call.
2. The stroller card: please keep the service name inside the `<a>` text (§4). Is the whole card a link, or only its title?
3. Does v0 reuse the counter header as it is (logo, phone, WhatsApp button)? Fine for SEO; no menu is needed.
4. The area section: a sentence, or the existing zone component in a compact form? Either, as long as the towns come from data.
5. Share image text (§8): does [B]'s `og.title` fit three lines at 80 px, or does it need the 64 px size?

**For the brand strategist (through the owner)**
1. The H1 and title use the descriptive tagline plus "Poznań" / "w Poznaniu i okolicach". Is that wording acceptable?
2. The tagline says "tapicerki, wózków i aut". Under option A the site sells only strollers and car seats at launch; the designer has already raised this (cleaning-design #6). Under B the tagline is true.
3. The homepage's prefilled WhatsApp message (§4) and the one-sentence route to the other services (§6).

**For the developer (goes with the handover; nothing new to build beyond checklist #10)**
- Home page title without a site-name suffix; `WebSite.name` exactly `Nowiutko`, no `alternateName`, no `SearchAction`; the homepage's own WhatsApp prefill; the stroller link present in the server HTML (checklist item 3's check).

## Success measure

In Search Console, two to four weeks after go-live:
- `/` is indexed on nowiutko.pl; a search for "Nowiutko" shows the site, with the site name "Nowiutko" (site names can take time to appear; that is Google's timing, not a fault).
- The stroller page shows `/` as an internal linking page.
- Impressions for the name and name + "poznań". These are expected to be small; the page is judged on being found for the name, not on traffic.

## Sources (read 16 Nov 2026)

- Google results page and autocomplete for [nowiutko](https://www.google.com/search?q=nowiutko&hl=pl&gl=pl) and "nowiutko poznań", "nowiutko pranie", "nowiutko.pl" (browser on the owner's computer)
- Google Search Central: [Site names](https://developers.google.com/search/docs/appearance/site-names) · [Title links](https://developers.google.com/search/docs/appearance/title-link) · [Link best practices](https://developers.google.com/search/docs/crawling-indexing/links-crawlable) · [Spam policies](https://developers.google.com/search/docs/essentials/spam-policies)
- Internal: `docs/brand.md`, `seo/strategy.md`, `seo/keywords/keyword-map.md`, `seo/notes/early-launch-checklist.md`, `seo/briefs/stroller-counter.md`, `docs/prd.md` (S1, S9), `docs/source/price-list.md`, `docs/source/digital-home-plan.md`
- cleaning-design at `stroller-v1.2`: `handoff/pages/stroller-counter/README.md`, `handoff/components/footer.md`, `handoff/components/share-image.md`, `copy.md`
