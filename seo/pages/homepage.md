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

**Read first (the two decisions that changed since the 16 Nov brief)**
1. **"wkrótce" is gone.** The brand strategist recorded the owner's decision of 17 Nov on cleaning-design #7: sofas, mattresses, rugs and car interiors are **taken by hand over WhatsApp**, so they are listed as bookable, each row opening WhatsApp with the service in the message, label **"Wycena na WhatsApp"**. The 16 Nov "wkrótce" instruction is superseded. If the owner wants "wkrótce" back, §6 has the alternative strings (one switch, no other change).
2. **The designer's `homepage-v0` handoff exists and is approved by the owner (17 Nov).** The developer builds from it. The copy below follows its `copy.md` except where §13 lists a deliberate change.

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
  - chat example (hard-coded illustration, not data; no name, time, rating or input): header `Nowiutko / WhatsApp`; customer bubble: two grey image thumbnails + `Dzień dobry, proszę o wycenę wózka.`; reply bubble: `Dziękujemy! Cenę podamy dziś.` + the hours line.
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
**Reuse unchanged:** `CounterFooter` (in whatever version the stroller page ships at launch; the company block and privacy link follow the stroller page), `CounterStickyBar` (phones, below 900 px), `CookieBanner`. Wrap the page like the stroller page: `<div class="pb-[76px] min-[900px]:pb-0" data-page="home">`, `<main>` around sections 4.2 to 4.6.

## 5. FAQ

**None on this page** (decision). The approved design has no FAQ, the stroller page owns the seven real questions, and a second FAQ here would repeat or contradict them. **Therefore no FAQPage markup on `/`.** The full homepage spec adds the sofa, mattress, price and drying questions once those counters exist.

## 6. If the owner prefers "wkrótce" (alternative, not the default)

Only if the owner reverses the 17 Nov decision. Change §4.3 and nothing else:
- Rows become plain, non-clickable list items (no `<a>`, no `href`, not styled like links); the text is `{service name} — wkrótce` with "wkrótce" as real text.
- Drop the four WhatsApp hrefs and the `services.wa` label.
- The meta description becomes: `Nowiutko: pierzemy wózki dziecięce i foteliki samochodowe u Ciebie w domu, w Poznaniu i okolicach. Wkrótce także kanapy, materace, dywany i wnętrza aut.` (152) and the lede in §4.2 is cut to `…: wózki i foteliki. Wkrótce także kanapy, materace, dywany i wnętrza aut.`

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
      "logo": "https://nowiutko.pl/brand/logo.svg",
      "image": "https://nowiutko.pl/brand/logo.svg",
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
- Logo: if a PNG of the logo exists, prefer it to the SVG for `logo`/`image` (Google lists SVG as supported; PNG is the safer default). Ask the owner/designer, not blocking.
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

`index, follow`; in `sitemap.xml` (`https://nowiutko.pl/`); answers 200; not in `routeRules` exclusions; staging stays `noindex, nofollow` and `Disallow: /` (unchanged). `robots.txt` unchanged (checklist item 6).

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
10. Page is in `sitemap.xml`; `robots.txt` as in checklist item 6.
11. Mobile (375 px): the WhatsApp button, the phone number and the H1 are in the first screen; PageSpeed mobile on the live URL: LCP under 2.5 s, CLS under 0.1, INP under 200 ms (filed as a separate "SEO fix" if not).
12. Search Console, 2 to 4 weeks after go-live: `/` indexed; a search for "Nowiutko" shows the site (site-name display is Google's timing, not a fault); the stroller page lists `/` as a linking page. Judged on being found for the name, not on traffic.

## 14. Differences from the 16 Nov brief and from the designer's `copy.md` (so nothing surprises)

| Item | Brief (16 Nov) | Now | Why |
|---|---|---|---|
| Unbuilt services | plain text, "wkrótce" | WhatsApp rows, "Wycena na WhatsApp" | Owner's decision 17 Nov (cleaning-design #7, brand strategist) |
| Meta description | strollers and car seats now, rest "wkrótce" | all services named, "Cena ze zdjęć na WhatsApp" | follows the decision above; matches the designer's `copy.md` |
| Hero WhatsApp message | reuse the stroller one | generic `home.whatsappMessage` | the page now offers more than strollers (this spec's decision, not in the designer's copy) |
| Hours line | not in the brief | `Odpisujemy pn–pt 9:00–17:00, sob 9:00–14:00` in hero and final CTA | owner's decision 17 Nov (brand #6 point 3) |
| Title dash | en dash | em dash U+2014 | `docs/brand.md`; approved by the brand strategist |
| Share-image copy | "U Ciebie w domu · …" ideas | the designer's final: `Pranie tapicerki, wózków i aut u Ciebie` / `Poznań i okolice · bez wychodzenia z domu` | brand #6 point 7 (no "tego samego dnia" promise) |
| "tego samego dnia" | n/a | **not used anywhere on `/`** | the brand strategist ruled it a promise we don't make (24 to 48 h slot) |
| FAQ, Service, Offer, Breadcrumb | none | none | unchanged |

## 15. Open questions for the owner

1. **"wkrótce" or "Wycena na WhatsApp"?** The spec follows the 17 Nov record on cleaning-design #7 (Wycena na WhatsApp). Your last instruction to the SEO desk said "wkrótce". Confirm; §6 is the fallback.
2. **Can you really take sofa, mattress, rug and car-interior jobs by hand from day one**, and answer those WhatsApp messages within the hours shown? The page now says so (lede, meta description, rows). If not, use §6.
3. **"Cenę podamy dziś"** with the hours line `pn–pt 9:00–17:00, sob 9:00–14:00`: a message sent on Saturday evening or Sunday gets its price on Monday. Brand decided "stays, read with the hours line". Confirm you are happy with that.
4. **"Zwykle w kilka minut"** (step 2): confirmed by you on 17 Nov; re-confirm it holds when you are on a job.
5. **Registered name and NIP for the footer** (the shared footer block shows only when both exist; a placeholder never ships).
6. **Logo as PNG** (for the `logo` property)? Not blocking; the SVG is used otherwise.
7. Unchanged and still open from `CLAUDE.md`: `ai-train` value for `Content-Signal`; keep `Disallow: /admin` next to the `noindex` header?

## 16. Brand wording to raise (draft, not opened)

**Issue (repo cleaning-seo, label `brand`): "Brand: stroller page still promises 'tego samego dnia'"**

> **Where:** cleaning-sell-system `i18n/locales/pl.json`, `counters.stroller.meta.description` ("Gotowe tego samego dnia"), `counters.stroller.hero.headlineAccent` ("Pod Twoim domem, tego samego dnia."), `counters.stroller.proof[0]` ("Tego samego dnia"), and the FAQ answer seeded in `server/data/poznan.seed.ts` line 384 ("Zwykle tego samego dnia…", also in the FAQPage markup).
> **What's wrong:** on cleaning-design #6 (16 Nov) the brand strategist decided "tego samego dnia" is a promise Nowiutko does not make (the PRD says a slot within 24 to 48 hours) and changed the share-image line for that reason. The stroller page, which goes live first, still says it in its meta description, headline, proof bar and a FAQ answer. It is also the page's main differentiator against 3-day drop-off laundries (`seo/briefs/stroller-counter.md` §1), so the owner needs to decide, not the SEO desk.
> **Suggestion:** either the owner confirms same-day is true for strollers and car seats (then the share-image line and the homepage can say so too), or the stroller copy changes to a true claim ("następnego dnia", "często jeszcze tego samego dnia", or "bez trzech dni czekania"). Needs a decision before Fri 20 Nov because it is in the title/description Google will index first.

**Smaller wording points for the brand strategist (no issue needed unless the owner wants one)**
- The label `Wycena na WhatsApp` on a row for a service that has no price page: fine for SEO; the brand strategist already approved it.
- The stroller title uses an en dash ("–"), the homepage title the em dash ("—") of `docs/brand.md`. Harmless; align on the next copy pass.

## 17. What the "Page spec: homepage" issue will contain (once approved)

- Title **"Page spec: homepage"**, label `page-spec`, repo cleaning-sell-system; body = a link to `seo/pages/homepage.md` (§ numbers above), the three decisions to know first (no "wkrótce", designer's `homepage-v0` handoff is the visual contract, the generic WhatsApp message), the component map (§9), the checklist (§12) and the acceptance criteria (§13), the JSON-LD (§8) pasted in full, and the open owner questions that block nothing.
- Priority: P0 for the 20 Nov early launch (cleaning-sell-system #8 point 4, checklist #10 items 3, 7, 9, 12).
- After the build: the developer files "Ready for SEO review: homepage" in cleaning-seo; the SEO desk audits staging against §13, then production the day it goes live.

## Sources (read 17 Nov 2026)

`CLAUDE.md`, `docs/brand.md`, `seo/strategy.md`, `seo/keywords/keyword-map.md`, `seo/briefs/homepage-v0.md`, `seo/briefs/stroller-counter.md`, `seo/notes/early-launch-checklist.md`, `docs/prd.md` (S1, S9), `docs/source/customer-stories-and-copy.md`, `price-list.md`. Read-only, local clones: cleaning-sell-system at `af390c4` (`app/pages/index.vue`, `app/pages/poznan/pranie-wozkow-i-fotelikow.vue`, `app/components/counter/*`, `app/utils/siteLinks.ts`, `i18n/locales/pl.json`, `shared/utils/serviceArea.ts`, `nuxt.config.ts`, `server/data/counters.ts`, `docs/design-constraints.md`); cleaning-design at `938c3a2` (`handoff/pages/homepage-v0/README.md`, `copy.md`, `handoff/components/footer.md`); comments on cleaning-design #6 and #7. Nothing here was tested on a live page.
