# Page spec: homepage (`/`), early-launch version "homepage v0"

| | |
|---|---|
| URL | `/` (`https://nowiutko.pl/`) |
| Status | **Draft 17 Nov 2026, for owner review.** Not sent. Becomes the issue "Page spec: homepage" in cleaning-sell-system (label `page-spec`) after the owner says "go". |
| Replaces | The "Wkrótce otwieramy" placeholder in `app/pages/index.vue` (cleaning-sell-system #43, early-launch subset; checklist items 3, 7, 9, 12 in cleaning-sell-system #10) |
| Supersedes | The SEO brief `seo/briefs/homepage-v0.md` (cleaning-design #7). The brief stays as the research record; where this spec and the brief differ, **this spec wins** (differences in §13) |
| Visual reference | The designer's finished handoff, tag `homepage-v0`: `cleaning-design/handoff/pages/homepage-v0/` (`README.md`, `copy.md`, `screens/`, `assets/og-nowiutko-1200x630.png`). **Layout, spacing, colours and the hero story board come from there.** This file fixes the words, the markup rules and the data. |
| Not this | The full homepage (PRD S1: outcome menu, packages, proof, FAQ, reviews). That gets its own spec later. |
| Brand | **Nowiutko** (`docs/brand.md`). Name written exactly so; never with a city, keyword or ".pl". |

**Read first (decisions, all confirmed by the owner on 17 Nov 2026)**
1. **"Wycena na WhatsApp", not "wkrótce".** The owner takes sofa, mattress, rug and car-interior jobs **by hand from day one**, so those services are listed as bookable, each row opening WhatsApp with the service in the message (cleaning-design #7, brand strategist, 17 Nov).
2. **The designer's `homepage-v0` handoff exists and is approved by the owner (17 Nov).** The developer builds from it. The copy below follows its `copy.md` except where §14 lists a deliberate change.
3. **Brand corrections of 17 Nov applied** (cleaning-design #8, cleaning-sell-system #12): the homepage chat example's reply reads `Dzień dobry! Dziękujemy — cenę podamy jeszcze dziś.`

---

## 1. Purpose and target

1. Answer a search for the name "Nowiutko" (primary query; today Google shows only the dictionary word, no business: read 16 Nov 2026, see the brief §1).
2. Give the stroller page its internal link (`/poznan/pranie-wozkow-i-fotelikow`), as a normal `<a href>` in the server HTML.
3. Tell Google the site name (`WebSite` node, `og:site_name`, title, H1).

Not targeted here: "pranie tapicerki poznań" and every service query (they wait for their counters and for the full homepage). No volumes exist for any of these; none is claimed.

## 2. Head

| Tag | Value |
|---|---|
| `<html lang>` | `pl-PL` |
| `<title>` | `Nowiutko — pranie tapicerki, wózków i aut u Ciebie \| Poznań` (59 characters; em dash U+2014 as in `docs/brand.md`; **no site-name suffix**: set `titleTemplate: '%s'` as the stroller page does) |
| meta description | `Nowiutko: pierzemy wózki, foteliki, kanapy, materace, dywany i wnętrza aut u Ciebie w domu, w Poznaniu i okolicach. Cena ze zdjęć na WhatsApp.` (142). Plain spaces, no price. |
| canonical | `https://nowiutko.pl/` (self, absolute, apex, HTTPS) |
| robots | none (indexable) on production; staging keeps `noindex, nofollow` |
| `og:title` | `Nowiutko — pranie tapicerki, wózków i aut u Ciebie` |
| `og:description` | same as the meta description |
| `og:url` | `https://nowiutko.pl/` |
| `og:type` / `og:site_name` / `og:locale` | `website` / `Nowiutko` / `pl_PL` |
| `og:image` | `https://nowiutko.pl/og-nowiutko-1200x630.png` (the designer's file, 61 KB; copy it to `public/`), with `og:image:width` 1200, `og:image:height` 630, `og:image:type` `image/png` |
| `og:image:alt` | `Nowiutko: pranie tapicerki, wózków i aut u Ciebie. Poznań i okolice.` |
| `twitter:card` | `summary_large_image` (plus `twitter:image` and `twitter:image:alt` = the same) |
| favicon | already set in `nuxt.config.ts` |

The image is static (the dynamic `ogImage` module stays off, as in the checklist, item 12). The text inside the image is the designer's: title `Pranie tapicerki, wózków i aut u Ciebie`, line `Poznań i okolice · bez wychodzenia z domu`. No price and no phone number in it.

## 3. Heading outline (exactly this)

```
H1  Nowiutko — pranie tapicerki, wózków i aut u Ciebie w Poznaniu i okolicach
  H2  Co pierzemy
    H3  Pranie wózków i fotelików            (the card title; contains the <a>)
  H2  Jak to działa
    H3  Wyślij zdjęcia
    H3  Dostań cenę i termin
    H3  Pierzemy u Ciebie
  H2  Gdzie dojeżdżamy
  H2  Wyślij 2–3 zdjęcia. Cenę podamy dziś.      (final CTA band)
```

No heading in the header, hero story board, footer, or per other-service row. Eyebrows ("Usługi", "Trzy kroki, zero wychodzenia z domu", "Obszar działania") are not headings (use `AppEyebrow` as a `<p>`/`<span>`, not `as="h*"`). Exactly one `<h1>`.

## 4. Sections in order, with final copy

Notation: `{…}` is data (§9). Strings in `pl.json` carry a non-breaking space (U+00A0) after the one-letter words **u, w, i, z, a, o** and between "wnętrza" and "aut", as the designer's handoff specifies. Title, meta, OG and JSON-LD use plain spaces. Here the copy is shown with plain spaces.

### 4.0 Skip link
`Przejdź do usług` → `#uslugi` (the services section's `id`). Same markup as the stroller page's skip link.

### 4.1 Header
**Reuse `CounterHeader`** unchanged: logo (`<a href="/">`, `aria-label` = `common.homeLabel`), phone as text with `tel:+48736369704` (shown "736 369 704"), WhatsApp button from 900 px (label `Wyślij zdjęcia na WhatsApp`). No menu.

### 4.2 Hero
**New component** `HomeHero` (the stroller `CounterHero` can't be reused: its H1 is a small eyebrow and its right column is a price card). Layout per the designer's README §4, `bg-primary-50`.

- **H1** (the headline itself, "Nowiutko" in `text-primary-500`): `Nowiutko — pranie tapicerki, wózków i aut u Ciebie w Poznaniu i okolicach`
- Voice line, a `<p>` under it: `Świeżo i jak nowe — bez wychodzenia z domu.`
- Lede, `<p>`: `Przyjeżdżamy z własnym sprzętem i pierzemy u Ciebie, na miejscu: wózki, foteliki, kanapy, materace, dywany i wnętrza aut.`
- Buttons: solid `Wyślij zdjęcia na WhatsApp` (→ `{whatsappHref}`, `data-cta="whatsapp"`, `data-cta-pos="hero"`) · outline `Zadzwoń: 736 369 704` (`tel:`, `data-cta="phone"`, `data-cta-pos="hero"`).
- Promise line (muted): `2–3 zdjęcia wystarczą. Cenę podamy dziś.`
- Hours line, directly under the promise line: `Odpisujemy pn–pt 9:00–17:00, sob 9:00–14:00`
- **Story board** (decorative, right column from 900 px; below the text as a slim strip under it on phones): the designer's three beats and chat example. One `role="img"` with
  - `alt`: `Trzy kroki: zaplamiony wózek, zdjęcia wysłane w rozmowie na WhatsApp, wózek jak nowy.`
  - visible labels: `Plama na wózku` · `Przykład: tak wygląda rozmowa` · `Wózek jak nowe`; phone strip (`aria-hidden`): `Plama` · `Zdjęcia` · `Jak nowe`
  - chat example (hard-coded illustration, not data; no name, time, rating or input): header `Nowiutko / WhatsApp`; customer bubble: two grey image thumbnails + `Dzień dobry, proszę o wycenę wózka.`; reply bubble: `Dzień dobry! Dziękujemy — cenę podamy jeszcze dziś.` (brand strategist, cleaning-design #8, 17 Nov; replaces the handoff's "Dziękujemy! Cenę podamy dziś.") + the hours line. The label `Przykład: tak wygląda rozmowa` stays.
  - nothing essential lives only inside the board (every fact is also in the lede, promise, hours and "Jak to działa"). Icons: Lucide plus the two custom SVGs (stroller, chamomile) from `cleaning-design/handoff` (`brand/`, `tokens/`).

### 4.3 Services: `id="uslugi"` (H2)
**Reuse `CounterSection`** (eyebrow, title, lede slot). New child markup per the designer's "Services block".

- Eyebrow: `Usługi` · **H2**: `Co pierzemy`
- Lede: `Wybierz, co chcesz odświeżyć. Cenę podajemy ze zdjęć, zanim przyjedziemy.`
- **Card (the only link to a page):** chip `Wózki i foteliki`; **H3 containing the `<a href="/poznan/pranie-wozkow-i-fotelikow">`** with text exactly `Pranie wózków i fotelików`; text `Wózki spacerowe, gondole, 2w1 i 3w1 oraz foteliki samochodowe. Cennik i pakiety na osobnej stronie.`; decorative line `Cennik i szczegóły →` (`aria-hidden="true"`). Whole card clickable through a `::after` stretched over the link; the anchor text stays the service name. Focus ring on the card.
- **Other services:** `<p>` label `Pozostałe usługi`, then a `<ul>` with four rows. Each row is **one `<a>`** to WhatsApp; its text is the service name, a visually hidden ` — `, and the visible label `Wycena na WhatsApp` (Lucide `message-circle`), so the link is never a bare "Wycena":

| Row text | `{object}` for the message |
|---|---|
| Kanapy, narożniki i fotele — Wycena na WhatsApp | kanap, narożników lub foteli |
| Materace — Wycena na WhatsApp | materaca |
| Dywany — Wycena na WhatsApp | dywanu |
| Tapicerka samochodowa (wnętrze auta) — Wycena na WhatsApp | tapicerki samochodowej (wnętrza auta) |

  Row `href` = `https://wa.me/48736369704?text=` + `encodeURIComponent('Dzień dobry, proszę o wycenę prania {object}. Wysyłam zdjęcia. Miejscowość: ')` (trailing space kept). Example for the first row:
  `https://wa.me/48736369704?text=Dzie%C5%84%20dobry%2C%20prosz%C4%99%20o%20wycen%C4%99%20prania%20kanap%2C%20naro%C5%BCnik%C3%B3w%20lub%20foteli.%20Wysy%C5%82am%20zdj%C4%99cia.%20Miejscowo%C5%9B%C4%87%3A%20`
  `rel="noopener"`, **no** `nofollow`/`sponsored`/`ugc`, `data-cta="whatsapp"`, `data-cta-pos="services"`.
- **Rules:** no prices, no heading, no paragraph, no icon-per-service claim, no Service/Offer markup for these four. No row may link to a page; a row that did would be a link to a URL that does not exist. When a counter ships, its row becomes a normal link with that counter's anchor text and the WhatsApp label goes (flip one field in the data, §9).

### 4.4 How it works (H2)
**Reuse `CounterSection` + `CounterSteps`.**
- Eyebrow: `Trzy kroki, zero wychodzenia z domu` · **H2**: `Jak to działa`
- 1 **Wyślij zdjęcia** — `2–3 zdjęcia przez WhatsApp lub SMS. Napisz, gdzie mieszkasz.`
- 2 **Dostań cenę i termin** — `Zwykle w kilka minut.` (owner confirmed 17 Nov, brand #6 point 3)
- 3 **Pierzemy u Ciebie** — `Przywozimy sprzęt i środki. Potrzebujemy tylko wody i gniazdka.`
- Button under the steps (as on the stroller page): `Wyślij zdjęcia na WhatsApp` (`data-cta-pos="steps"`).

### 4.5 Area (H2, `bg-muted` band)
**Reuse `CounterSection band`.** No `CounterZones` (no zone names, no fees on the homepage).
- Eyebrow: `Obszar działania` · **H2**: `Gdzie dojeżdżamy`
- `<p>` (display size): `Poznań i powiat poznański.`
- `<p>` lede: `Jeździmy po całym powiecie, na przykład: {zones:featured}. Napisz, gdzie mieszkasz, a potwierdzimy dojazd.`
- `{zones:featured}`: the first five towns of Strefa 1 by the owner's sort order, **excluding Poznań**, in the nominative, joined with ", " (the designer's prototype shows "Swarzędz, Luboń, Suchy Las, Komorniki, Plewiska"; the live value follows the data). Not a wall of towns, no more than five, no link to `/poznan/obszar-dzialania` (it does not exist).

### 4.6 Final call to action: `id="kontakt"` (H2)
**Reuse `CounterFinalCta`** unchanged except one new optional line (hours, below).
- **H2**: `Wyślij 2–3 zdjęcia. Cenę podamy dziś.` (same strings as `counters.stroller.final.h2`)
- Promise (`t('brand.promise')`, unchanged): `Przyjeżdżamy na czas. Płacisz tyle, ile podaliśmy ze zdjęć. Jeśli coś wyjdzie po wyschnięciu, wracamy za darmo.`
- Buttons: `Wyślij zdjęcia na WhatsApp` · `Zadzwoń: 736 369 704`
- SMS line: `Nie masz WhatsAppa? Wyślij zdjęcia SMS-em na ten sam numer.` (as on the stroller page: `sms:+48736369704`)
- **New:** the hours line `Odpisujemy pn–pt 9:00–17:00, sob 9:00–14:00` under the buttons (add an optional `hours` prop or default slot to `FinalCta.vue`; the stroller page may adopt it later).

### 4.7 Footer, sticky bar, cookie banner
**Reuse unchanged:** `CounterFooter` as the stroller page ships it at launch, **without the company block** (legal name and NIP are parked by the owner until Fri 20 Nov; the block shows only when both values exist and a placeholder never ships, so leave it out of the build for now; see the follow-up in §12), `CounterStickyBar` (phones, below 900 px), `CookieBanner`. Wrap the page like the stroller page: `<div class="pb-[76px] min-[900px]:pb-0" data-page="home">`, `<main>` around sections 4.2 to 4.6.

## 5. FAQ

**None on this page** (decision). The approved design has no FAQ, the stroller page owns the seven real questions, and a second FAQ here would repeat or contradict them. **Therefore no FAQPage markup on `/`.** The full homepage spec adds the sofa, mattress, price and drying questions once those counters exist.

## 6. (removed)

The "wkrótce" fallback is dropped: the owner confirmed "Wycena na WhatsApp" on 17 Nov. Section numbers below are unchanged.

## 7. Internal links (complete list)

| From | To | Anchor text | Notes |
|---|---|---|---|
| Services card | `/poznan/pranie-wozkow-i-fotelikow` | `Pranie wózków i fotelików` | `<a href>` in server HTML. **The stroller page's only internal inbound link at launch.** Acceptance: present in `curl` output |
| Header and footer logo | `/` | logo `alt="Nowiutko"` | header only; footer logo not a link |
| Footer | privacy page (when `siteLinks.privacy` is set) | `Prywatność` | existing behaviour |
| Cookie banner | `/polityka-prywatnosci#cookies` | `Szczegóły` | existing behaviour |

Optional (only if the card gets a second link, not required): `Cennik prania wózków i fotelików` → `/poznan/pranie-wozkow-i-fotelikow#cennik`.
**Must not appear:** links to `/cennik`, `/poznan/obszar-dzialania`, `/poznan/wycena`, `/regulamin`, `/cookies`, any other counter, `href="#"`, empty or placeholder links, social icons, a Business Profile link (added when the profile exists).
Contact links: `https://wa.me/48736369704?text=…` · `tel:+48736369704` · `sms:+48736369704`. WhatsApp links: `rel="noopener"`, no `nofollow`. Numbers come from `{business:phone}` / `{business:whatsapp}`; the placeholder 500 000 000 must not reach production.

## 8. Structured data (one JSON-LD graph, server-rendered)

Use `useSchemaOrg` as on the stroller page. The **LocalBusiness node must come from one shared source** used by both pages (a composable such as `useBusinessSchema()`), so the two pages emit identical nodes (checklist item 7, closes SEO fix #4). `WebSite` and `WebPage` come from `@nuxtjs/seo` defaults; check and override them to match this graph.

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "LocalBusiness",
      "@id": "https://nowiutko.pl/#business",
      "name": "Nowiutko",
      "url": "https://nowiutko.pl/",
      "telephone": "+48736369704",
      "description": "Mobilne pranie tapicerki, wózków dziecięcych, fotelików samochodowych i wnętrz aut u klienta w domu, w Poznaniu i powiecie poznańskim.",
      "logo": "https://nowiutko.pl/brand/logo.png",
      "image": "https://nowiutko.pl/brand/logo.png",
      "address": {
        "@type": "PostalAddress",
        "addressLocality": "Poznań",
        "addressRegion": "wielkopolskie",
        "addressCountry": "PL"
      },
      "areaServed": [
        { "@type": "City", "name": "Poznań" },
        { "@type": "Place", "name": "Suchy Las" },
        { "@type": "Place", "name": "Swarzędz" },
        { "@type": "Place", "name": "Luboń" },
        { "@type": "Place", "name": "Komorniki" },
        { "@type": "Place", "name": "Plewiska" }
      ]
    },
    {
      "@type": "WebSite",
      "@id": "https://nowiutko.pl/#website",
      "url": "https://nowiutko.pl/",
      "name": "Nowiutko",
      "inLanguage": "pl-PL",
      "publisher": { "@id": "https://nowiutko.pl/#business" }
    },
    {
      "@type": "WebPage",
      "@id": "https://nowiutko.pl/#webpage",
      "url": "https://nowiutko.pl/",
      "name": "Nowiutko — pranie tapicerki, wózków i aut u Ciebie | Poznań",
      "description": "Nowiutko: pierzemy wózki, foteliki, kanapy, materace, dywany i wnętrza aut u Ciebie w domu, w Poznaniu i okolicach. Cena ze zdjęć na WhatsApp.",
      "inLanguage": "pl-PL",
      "isPartOf": { "@id": "https://nowiutko.pl/#website" },
      "about": { "@id": "https://nowiutko.pl/#business" }
    }
  ]
}
```

Rules:
- `areaServed` above is **illustrative**: generate it with `areaServed(city.name, zones)` (`shared/utils/serviceArea.ts`), exactly as the stroller Service does (Poznań, then every Zone 1 and Zone 2 town in the owner's list). Never type it by hand.
- `name` of `LocalBusiness` and `WebSite` is exactly `Nowiutko`. **No** `alternateName`, **no** `SearchAction`/`potentialAction`, **no** `priceRange`, `openingHoursSpecification` (the "Odpisujemy …" line is reply time, not opening hours), `sameAs` (no profiles yet), `geo`, `streetAddress`, `postalCode`.
- Logo: `logo` and `image` use a **PNG export of `public/brand/logo.svg`** (developer task, §12), e.g. `https://nowiutko.pl/brand/logo.png`, square-friendly and at least 112×112 px, absolute URL. Change the two URLs in the JSON-LD above to it.
- **None on `/`:** Service, Offer, FAQPage, BreadcrumbList (the home page is the top of the trail), AggregateRating, Review.
- Validate the **rendered** HTML in the Rich Results Test and the Schema Markup Validator; the page should show no errors. (LocalBusiness is not a rich-result type; the check is for syntax and for `@id` consistency.)

## 9. Data and components

**Component map**

| Section | Component | Status |
|---|---|---|
| Header | `app/components/counter/Header.vue` (`CounterHeader`) | reuse unchanged |
| Hero + story board | new `app/components/home/HomeHero.vue`, `HomeStoryBoard.vue` (two custom SVG icons) | new, from the designer's handoff |
| Services (card + rows) | `CounterSection` (`counter/Section.vue`) + new `home/HomeServices.vue` | new content in an existing section |
| How it works | `CounterSection` + `counter/Steps.vue` | reuse; the stroller copy keys are copied, not shared |
| Area | `CounterSection band` | reuse; no `CounterZones` |
| Final CTA | `counter/FinalCta.vue` | reuse + optional `hours` line |
| Footer / sticky bar / cookies | `counter/Footer.vue`, `counter/StickyBar.vue`, `CookieBanner.vue` | reuse unchanged |
| Page | `app/pages/index.vue` | replace the placeholder |

**Copy:** new tree `home.*` in `i18n/locales/pl.json` read with `useCopyTree`, same pattern as `counters.stroller`. Keys: `meta.title`, `meta.description`, `og.*`, `hero.{h1,voice,lede,promise}`, `story.*`, `hours`, `services.{eyebrow,h2,lede,card,otherLabel,wa}`, `steps.*`, `area.*`, `final.{h2,smsLink}`, `whatsappMessage`, `whatsappServiceMessage`. Strings exactly as §4.

**Data (new endpoint, e.g. `server/api/home/[city].get.ts`, city `poznan`):** `business.{phone, whatsapp, hours}`, `city.name`, `zones` (for `areaServed` and `{zones:featured}`), `services[]` (see below). Read the business data the same way `getCounterData` does, so owner edits show at once.
- `hours`: not in the data model yet (admin working hours are for slot calculation). For v0 put the string in `pl.json` (`home.hours`) and move it to `{business:hours}` when the owner can edit it. Do not derive it from working hours.
- `services[]` for v0 can be a small list in `server/data/` or `pl.json`: `{ key, name, objectGenitive, pagePath | null }`. `pagePath` set → card/link row to the page with the counter's anchor text; `null` → WhatsApp row. Stroller: `pagePath: '/poznan/pranie-wozkow-i-fotelikow'`.
- Add `siteLinks.stroller` (or reuse the `pagePath`) so the card link is not typed in a template.

**WhatsApp message for the hero, header, sticky bar, steps and final buttons (decision):** use a generic one, new key `home.whatsappMessage`: `Dzień dobry, proszę o wycenę prania. Wysyłam zdjęcia. Miejscowość: ` (trailing space kept). The designer's copy kept the stroller message ("…wózka lub fotelika…"), which no longer fits a page that now offers sofas, mattresses, rugs and cars. The four service rows use their own message (§4.3). The stroller page keeps its own.

## 10. Images and alt text

No photos at launch (no stock, no placeholders). Only SVG and one PNG.

| Image | `alt` / treatment |
|---|---|
| Logo in the header (`/brand/logo.svg`, 355×100) | `Nowiutko` (`t('brand.name')`), as the stroller header |
| Story board | one `role="img"` with `Trzy kroki: zaplamiony wózek, zdjęcia wysłane w rozmowie na WhatsApp, wózek jak nowy.`; everything inside `aria-hidden`; phone strip `aria-hidden` |
| Chat thumbnails | decorative, `aria-hidden`, no `<img>` |
| Lucide icons | `aria-hidden="true"` |
| Share image `og-nowiutko-1200x630.png` | `og:image:alt` as §2; not on the page |

`width`/`height` on every `<img>`; the board has a fixed aspect ratio (500/640, 540/640 from 1100 px) so nothing shifts.

## 11. Indexing, sitemap, robots

`index, follow`; in `sitemap.xml` (`https://nowiutko.pl/`); answers 200; not in `routeRules` exclusions; staging stays `noindex, nofollow` and `Disallow: /` (unchanged). **Production `robots.txt` (owner decisions 17 Nov; replaces checklist #10 item 6 and item 16):**
```
User-agent: *
Allow: /

Content-Signal: search=yes, ai-input=yes, ai-train=yes

Sitemap: https://nowiutko.pl/sitemap.xml
```
No `Disallow: /admin`. The admin stays out of the index through the `X-Robots-Tag: noindex` header that `routeRules` already sets for `/admin/**` (a crawler can only read a noindex header on a page it is allowed to fetch). Nothing else is disallowed.

## 12. Developer checklist

- [ ] Replace `app/pages/index.vue`; build from `cleaning-design/handoff/pages/homepage-v0/` (README §4–§7) and the words in §4 of this file
- [ ] `home.*` copy in `pl.json`; NBSP after u/w/i/z/a/o; plain spaces in head/OG/JSON-LD
- [ ] Title with `titleTemplate: '%s'`, description, canonical, OG and Twitter tags (§2); copy `og-nowiutko-1200x630.png` to `public/` and absolute-URL it
- [ ] One `<h1>`; heading order exactly §3; no heading in the header, footer, board or service rows
- [ ] Services card with the stroller link; four WhatsApp rows with the per-service message (§4.3); no row links to a page
- [ ] Hours line in the hero and the final CTA band (`FinalCta` gets an optional `hours`)
- [ ] `{zones:featured}` from data, nominative, five towns, no Poznań
- [ ] Shared `LocalBusiness` composable used by `/` and the stroller page; `WebSite` `name` = `Nowiutko`, no `alternateName`/`SearchAction`; `areaServed` generated; no Service/FAQ/Breadcrumb/Rating nodes on `/`
- [ ] Real phone `+48736369704` everywhere; 500 000 000 absent from production
- [ ] Contact-click events carry `data-cta` and `data-cta-pos` (`header|hero|services|steps|final|sticky`), sent only after analytics consent (checklist item 13)
- [ ] Skip link `#uslugi`; keyboard order and focus ring per the designer's README §7; works at 320 to 1440 px, no horizontal scroll, no layout shift from the cookie banner; reduced motion honoured
- [ ] Nothing essential only in JS: `curl` shows every string and the stroller `href`
- [ ] Add `/` to the JSON-LD e2e test (LocalBusiness `@id` the same on both pages)
- [ ] Export `public/brand/logo.png` from `logo.svg` (at least 112×112 px; keep the logo's proportions or use the mark on a square canvas) and use it for LocalBusiness `logo` and `image`
- [ ] `robots.txt` as in §11: `Content-Signal` with `ai-train=yes`, **no** `Disallow: /admin`; confirm `curl -sI https://nowiutko.pl/admin` still shows `x-robots-tag: noindex` (and no cache of the admin)
- [ ] Footer: no company block at launch. **Post-launch follow-up (after Fri 20 Nov):** when the owner supplies legal name and NIP, enter them in the business data so the shared footer block appears (`footer.md` v1.2); no placeholder before that

## 13. Acceptance criteria (the SEO desk checks these on staging, then on production)

1. `curl -s https://nowiutko.pl/` returns 200, `<html lang="pl-PL">`, **one** `<h1>` with the exact text in §3, and the `<title>` and meta description of §2 (59 / 142 characters, no suffix).
2. `grep -c 'href="/poznan/pranie-wozkow-i-fotelikow"'` on the homepage HTML is at least 1, with the anchor text `Pranie wózków i fotelików`.
3. Canonical is `https://nowiutko.pl/`; no `noindex` in meta or header on production; the same two checks on staging still show `noindex, nofollow`; no staging host name in production HTML.
4. Every internal link on the page returns 200; no link to `/cennik`, `/poznan/obszar-dzialania`, `/poznan/wycena`, `/regulamin`, `/cookies`; no `href="#"`.
5. The four service rows are links to `wa.me/48736369704?text=…` with the service in the message; none has a heading, paragraph or price; the visible label is `Wycena na WhatsApp`; the screen-reader text reads "service name, Wycena na WhatsApp".
6. Rendered JSON-LD: `LocalBusiness` (`#business`), `WebSite` (`#website`, `name` `Nowiutko`), `WebPage`; the `LocalBusiness` node is identical to the one on the stroller page; `areaServed` matches the owner's towns; **0** hits for `AggregateRating`, `Review`, `FAQPage`, `Offer`, `SearchAction`, `alternateName`, `openingHours`, `streetAddress`.
7. OG: all tags of §2 present; the image URL returns 200, 1200×630; Facebook Sharing Debugger shows image, title and description.
8. The hours line appears under the hero promise and under the final CTA buttons, with the exact text of §4.2.
9. `curl` shows no `500 000 000` and does show `48736369704`.
10. Page is in `sitemap.xml`; `robots.txt` exactly as in §11 (Content-Signal `ai-train=yes`, no `Disallow: /admin`); `/admin` answers with `x-robots-tag: noindex`; `https://nowiutko.pl/brand/logo.png` returns 200 and is the URL in `logo`/`image`.
11. Mobile (375 px): the WhatsApp button, the phone number and the H1 are in the first screen; PageSpeed mobile on the live URL: LCP under 2.5 s, CLS under 0.1, INP under 200 ms (filed as a separate "SEO fix" if not).
12. Search Console, 2 to 4 weeks after go-live: `/` indexed; a search for "Nowiutko" shows the site (site-name display is Google's timing, not a fault); the stroller page lists `/` as a linking page. Judged on being found for the name, not on traffic.

## 14. Differences from the 16 Nov brief and from the designer's `copy.md` (so nothing surprises)

| Item | Brief (16 Nov) | Now | Why |
|---|---|---|---|
| Unbuilt services | plain text, labelled as coming soon | WhatsApp rows, "Wycena na WhatsApp" | Owner's decision 17 Nov (cleaning-design #7, brand strategist) |
| Meta description | strollers and car seats now, the rest as coming | all services named, "Cena ze zdjęć na WhatsApp" | follows the decision above; matches the designer's `copy.md` |
| Hero WhatsApp message | reuse the stroller one | generic `home.whatsappMessage` | the page now offers more than strollers (this spec's decision, not in the designer's copy) |
| Hours line | not in the brief | `Odpisujemy pn–pt 9:00–17:00, sob 9:00–14:00` in hero and final CTA | owner's decision 17 Nov (brand #6 point 3) |
| Title dash | en dash | em dash U+2014 | `docs/brand.md`; approved by the brand strategist |
| Share-image copy | "U Ciebie w domu · …" ideas | the designer's final: `Pranie tapicerki, wózków i aut u Ciebie` / `Poznań i okolice · bez wychodzenia z domu` | brand #6 point 7 (the line must not read as a same-day visit) |
| Chat example reply | "Dziękujemy! Cenę podamy dziś." | "Dzień dobry! Dziękujemy — cenę podamy jeszcze dziś." | brand strategist, cleaning-design #8 (17 Nov) |
| "tego samego dnia" | n/a | **not used on `/`** (§16) | page covers more than strollers; rule from cleaning-design #8: only in the "ready" sense, never a visit |
| robots.txt | `Disallow: /admin`, no Content-Signal yet | no Disallow, `ai-train=yes` | owner, 17 Nov |
| FAQ, Service, Offer, Breadcrumb | none | none | unchanged |

## 15. Open items (everything else is closed)

Decided by the owner on 17 Nov and now written into the spec: "Wycena na WhatsApp" (not "wkrótce"); sofa, mattress, rug and car jobs taken by hand from day one; hours line and "Cenę podamy dziś" (a Saturday-evening message gets its price on Monday); "Zwykle w kilka minut"; logo PNG export; `ai-train=yes`; no `Disallow: /admin`.

Still open:
1. **Registered name and NIP** for the footer: parked until Fri 20 Nov; the company block stays out of the launch build (§4.7, §12 follow-up).

Nothing else is open. The "tego samego dnia" question is closed (§16).

## 16. Wording rule: "tego samego dnia"

Ruling of the brand strategist, 17 Nov (cleaning-design #8, applied by the developer through cleaning-sell-system #12; it reverses the 16 Nov note on #6): the phrase **stays where it means the stroller is ready the same day** (true: washed in the morning, dry in 3 to 5 hours), and goes only where it could read as a same-day visit, which Nowiutko does not promise. On the stroller page that means the hero accent "Gotowy na spacer tego samego dnia.", with the meta description, the seeded FAQ answer and the proof bar kept unless proof[0] reads as a visit. No Brand issue is needed; the draft is withdrawn.

**Homepage decision: do not use "tego samego dnia" on `/` at all.** The page speaks about the whole business, and sofa, mattress, rug and car jobs do not dry in hours (4 to 12 hours per the price list), so the phrase would be true only for the stroller card and invite a misreading as a same-day visit. The stroller page carries it. If the owner wants it on the stroller card, the only allowed form is "gotowy tego samego dnia".

Minor, no issue: the stroller title uses an en dash, the homepage title the em dash of `docs/brand.md`; align on the next copy pass.

## 17. What the "Page spec: homepage" issue will contain (once approved)

- Title **"Page spec: homepage"**, label `page-spec`, repo cleaning-sell-system; body = a link to `seo/pages/homepage.md` (§ numbers above), the decisions to know first ("Wycena na WhatsApp", designer's `homepage-v0` handoff is the visual contract, the generic WhatsApp message, the corrected chat reply, no footer company block yet), the `robots.txt` and logo-PNG tasks, the component map (§9), the checklist (§12) and the acceptance criteria (§13), the JSON-LD (§8) pasted in full, and the one open owner item (company name and NIP, post-launch).
- Priority: P0 for the 20 Nov early launch (cleaning-sell-system #8 point 4, checklist #10 items 3, 7, 9, 12).
- After the build: the developer files "Ready for SEO review: homepage" in cleaning-seo; the SEO desk audits staging against §13, then production the day it goes live.

## Sources (read 17 Nov 2026)

`CLAUDE.md`, `docs/brand.md`, `seo/strategy.md`, `seo/keywords/keyword-map.md`, `seo/briefs/homepage-v0.md`, `seo/briefs/stroller-counter.md`, `seo/notes/early-launch-checklist.md`, `docs/prd.md` (S1, S9), `docs/source/customer-stories-and-copy.md`, `price-list.md`. Read-only, local clones: cleaning-sell-system at `af390c4` (`app/pages/index.vue`, `app/pages/poznan/pranie-wozkow-i-fotelikow.vue`, `app/components/counter/*`, `app/utils/siteLinks.ts`, `i18n/locales/pl.json`, `shared/utils/serviceArea.ts`, `nuxt.config.ts`, `server/data/counters.ts`, `docs/design-constraints.md`); comments on cleaning-design #8 and cleaning-sell-system #12 (read again 17 Nov); cleaning-design at `938c3a2` (`handoff/pages/homepage-v0/README.md`, `copy.md`, `handoff/components/footer.md`); comments on cleaning-design #6 and #7. Nothing here was tested on a live page.
