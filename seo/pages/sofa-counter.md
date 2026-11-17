# Page spec: sofa counter (`/poznan/pranie-kanap`)

| | |
|---|---|
| URL | `/poznan/pranie-kanap` (**recommended; conflicts with one document, see §1**) |
| Status | **Draft 17 Nov 2026, for owner review.** Not sent. Becomes the issue "Page spec: sofa counter" in cleaning-sell-system (label `page-spec`) after the owner says "go". |
| Scope | **Not part of the 20 Nov early launch** (cleaning-sell-system #8 lists the stroller page, homepage v0, privacy page and admin only). The developer builds it after the launch; it stays hidden on production until the owner says go (§10). |
| Template | The stroller counter: `app/pages/poznan/pranie-wozkow-i-fotelikow.vue` and `app/components/counter/*` in cleaning-sell-system (checked at `af390c4`). **No new design.** The designer is paused: this page reuses the counter components as they are; no new colours, icons or layouts (§9). |
| Persona | Kasia (sofa after a toddler), Tomek (pets), Ola (tenant), landlords (`docs/source/customer-stories-and-copy.md`); the page speaks mainly to a family with a sofa that has had a hard life |
| Brand | **Nowiutko** (`docs/brand.md`). Voice: "Ty", short sentences, freshness. `tego samego dnia` is **not used** on this page: a sofa takes 4 to 8 hours to dry, and the phrase may only mean "ready the same day", never a same-day visit (homepage spec §16; cleaning-design #8). |
| Booking | Phone and WhatsApp only, as on the stroller page (no quote form yet; `siteLinks.quote` is `null`). |

---

## 1. Intent, URL and keywords

**Who searches.** Households in Poznań and the county with a stained, smelly or just tired sofa or corner sofa: before Christmas guests, after a child or a pet, after moving into a rented flat. They want a price, to know how long it takes to dry, whether it is worth it versus a rented Kärcher, and whether it is safe for fabric and family (`docs/source/customer-questions.md`, "Sofas, carpets and upholstery", Google "Ludzie pytają też", read 5 Nov 2026).

**Competition** (competitor audit, Google results read 5 Nov 2026; results vary by place and person, and I did not re-read Google for this spec): PranieNaZawolanie24 is #1 for "pranie kanapy Poznań" with a text-heavy page, no prices on the homepage, no reviews, no WhatsApp; Pranie Posejdona (#3, 537 reviews pooled nationally, prices net of VAT, "od 160 zł" for a sofa); Karcher Czyszczenie Poznań (#7); Czysta Tapicerka Poznań (#8). Gaps we can fill: **gross prices on the page, drying time stated per item, WhatsApp photo quote, a free correction promise, suburbs included**.

**URL conflict to decide (open question 1).** The documents disagree:
- `seo/strategy.md` and cleaning-sell-system `docs/issues.md` #49 (and the designer's link checks): `/poznan/pranie-kanap`
- `seo/keywords/keyword-map.md` §2 and `docs/source/digital-home-plan.md`: `/poznan/pranie-kanap-i-dywanow` ("Sofa & rug counter")

**Recommendation: `/poznan/pranie-kanap`.** It matches the primary query, is shorter, and is the one in the developer's issue list. The rug part of the old name does not hold: the keyword map itself says drop-off rug laundries dominate "pranie dywanów poznań", rugs are not on this page's price list group, and a combined URL would invite a second primary query on one page. Rugs stay a WhatsApp-quote row on the homepage; a rug section or page is decided later, with data. If the owner chooses the other URL, only the slug, the canonical, the sitemap entry and the links in §7 change. The URL is hard to change later, so decide before the build.

**Primary query:** `pranie kanapy poznań` (autocomplete validated 8 Nov: "pranie kanapy poznań cena", "… olx", "pranie tapicerki kanapy poznań"). **No volumes exist**; none is claimed.

| Query (PL) | Role | Where it is answered |
|---|---|---|
| pranie kanapy poznań | primary | title, H1 (plural form), hero, price section |
| pranie tapicerki meblowej poznań | secondary | hero lede ("tapicerkę meblową") |
| pranie narożników poznań / pranie narożnika poznań | secondary | title, H1, price list ("Narożnik") |
| ile kosztuje pranie kanapy (… trzyosobowej, … narożnej, … w domu, … z dojazdem) | question | price H2 and FAQ 1, 2 |
| ile schnie kanapa po praniu | question | drying H2 and FAQ 3 |
| czym wyprać kanapę w domu / czy warto prać kanapę | question | "Dlaczego nie wyprać kanapy samemu?" and FAQ 8 |
| usuwanie zapachu moczu z kanapy | **not here** (pets counter) | one FAQ answer and one card only; no page-level targeting |
| pranie dywanów poznań | **not here** | later |
| pranie tapicerki poznań | **not here** (homepage) | never in title/H1/H2 |

## 2. Head

| Tag | Value |
|---|---|
| `<html lang>` | `pl-PL` |
| `<title>` | `Pranie kanapy Poznań – u Ciebie w domu, od {price:sofa-2}` → "…od 150 zł" (49 characters). Same pattern and en dash as the stroller title; `titleTemplate: '%s'`, no site-name suffix. Alternative if the owner wants the plural forms: `Pranie kanap i narożników Poznań – z dojazdem, od 150 zł` (56). |
| meta description | `Pierzemy kanapy i narożniki u Ciebie w domu, w Poznaniu i okolicach. Cena ze zdjęć przed przyjazdem, od {price:sofa-2}. Schnie 4–8 godzin.` → 130 characters with "150 zł". Price from the price list (2-seat sofa, the lowest sofa price), plain spaces. |
| canonical, `og:url` | `https://nowiutko.pl/poznan/pranie-kanap` |
| robots | none on production once launched; staging `noindex, nofollow` (unchanged) |
| `og:title` | `Pranie kanap i narożników u Ciebie w domu, Poznań` |
| `og:description` | the meta description |
| `og:type` / `og:site_name` / `og:locale` | `website` / `Nowiutko` / `pl_PL` |
| `og:image` | the site's static share image (`og-nowiutko-1200x630.png`) with its `og:image:alt`, until a page-specific one exists |
| `twitter:card` | `summary_large_image` |

## 3. Heading outline (exactly this)

```
H1  Pranie kanap i narożników w Poznaniu i okolicach              (styled as the small eyebrow, as on the stroller page)
  (not a heading) headline paragraph: "Kanapa jak nowa. Pranie u Ciebie, bez wynoszenia mebli."
  H2  Dlaczego nie wyprać kanapy samemu?
    (cards use no heading tags, as on the stroller page)
  H2  Pranie kanapy – cena
    H3  Jak pierzemy kanapę                                        (SafetyPanel)
    packages: no headings (as on the stroller page)
  H2  Jak to działa
    H3  Wyślij zdjęcia / Dostań cenę i termin / Pierzemy u Ciebie
  H2  Kanapy przed i po praniu                                      (only with real photos)
  H2  Ile schnie kanapa po praniu?
  H2  Co mówią klienci                                              (only with real reviews)
  H2  Najczęstsze pytania
  H2  Gdzie dojeżdżamy
    H3  zone names                                                  (CounterZones, as on the stroller page)
  H2  Wyślij 2–3 zdjęcia. Cenę podamy dziś.                        (final CTA)
```

One `<h1>`. Eyebrows (`AppEyebrow`) are not headings. The page contains **no** mention of mattresses, cars or strollers in a heading.

## 4. Sections in order, with final copy

Notation: `{price:key}` fills from the price list (`fillPriceTokens`), `{…}` other data. Strings in `pl.json` get a non-breaking space (U+00A0) after one-letter words (u, w, i, z, a, o). New copy tree `counters.sofa.*`, read with `useCopyTree`.

### 4.0 Skip link and header
Skip link `Przejdź do cennika` → `#cennik` (as the stroller page). **Reuse `CounterHeader`** unchanged (logo → `/`, phone, WhatsApp button `Wyślij zdjęcia na WhatsApp`).

### 4.1 Hero: `CounterHero` + `CounterHeroPriceCard`
- **H1** (eyebrow style): `Pranie kanap i narożników w Poznaniu i okolicach`
- Headline (`<p>`): `Kanapa jak nowa.` + accent `Pranie u Ciebie, bez wynoszenia mebli.`
- Lede: `Pierzemy tapicerkę meblową u Ciebie, na miejscu: kanapy, narożniki i fotele. Przyjeżdżamy z własnym sprzętem, więc nic nie wynosisz z domu.`
- Ticks: `Cena ze zdjęć, przed przyjazdem` · `Odkurzanie na sucho w cenie` · `Dojazd gratis w Strefie 1`
- Price card (`HeroPriceCard`): eyebrow `Cennik brutto`, sub `cena ze zdjęć, przed przyjazdem`; items from data in this order: **Kanapa 2-osobowa, Kanapa 3-osobowa, Narożnik, Fotel** (`heroItemKeys`: `sofa-2`, `sofa-3`, `sofa-corner`, `armchair`); price-list link `Pełny cennik i pakiety` → `#cennik`; promise `2–3 zdjęcia wystarczą. Cenę podamy dziś.`; the hours line `Odpisujemy pn–pt 9:00–17:00, sob 9:00–14:00` exactly as the stroller page and homepage show it at the time of the build (same string, same place). The "next free slot" line stays hidden (`showNextFreeSlot = false`).
- Buttons: solid `Wyślij zdjęcia na WhatsApp` (`data-cta-pos="hero"`), outline `Zadzwoń: 736 369 704`.

### 4.2 Proof bar: `CounterProofBar` (four facts; the component's icons are fixed by position: clock, house, shield, badge)
1. **Schnie w 4–8 godzin** — `Zależnie od tkaniny i wietrzenia.` (lead, large)
2. **U Ciebie w domu** — `Własny sprzęt. Potrzebujemy wody i gniazdka.`
3. **Hipoalergiczne środki** — `Bezpieczne dla dzieci i zwierząt po wyschnięciu.`
4. **Poprawka gratis** — `Jeśli coś wyjdzie po wyschnięciu, wracamy.`

### 4.3 Headache (H2): `CounterSection band` + `CounterProblemCard` ×4 (text variant, no photos at launch)
- Eyebrow `Z czym przychodzą klienci` · **H2** `Dlaczego nie wyprać kanapy samemu?`
- Lede: `Wynajęty odkurzacz piorący zostawia zbyt mokrą tapicerkę i zacieki, a plama bywa tylko rozmazana. My pierzemy ekstrakcyjnie i mocno odsysamy wodę, żeby kanapa szybko schła.`
- Cards (label `Problem`, `fixLabel` `Co robimy.`):
  1. **Plama po winie, kawie albo soku** — `Odkurzamy na sucho, a potem pierzemy. Większość plam, także starych, schodzi. Jeśli któraś nie zejdzie w całości, powiemy to przed rozpoczęciem.`
  2. **Kanapa po maluchu** — `Hipoalergiczne środki, dokładnie odsysane. Po wyschnięciu kanapa jest bezpieczna dla całej rodziny.` + text link `pranie wózków i fotelików` → `/poznan/pranie-wozkow-i-fotelikow` (the link component prop `to`/`linkLabel` of `ProblemCard`; stroller page is live at launch)
  3. **Sierść i wypadki zwierzaka** — `Przy moczu używamy środka enzymatycznego, który rozkłada go u źródła, a nie tylko maskuje zapach. Silne zabrudzenia wyceniamy ze zdjęć.` (**depends on open question 4**; if the owner does not confirm the enzyme treatment, replace with `Usuwamy sierść i zabrudzenia po zwierzaku. Silne zabrudzenia wyceniamy ze zdjęć, zanim przyjedziemy.`)
  4. **Narożnik, fotele i krzesła naraz** — `Cały salon w jednej wizycie, z jednym dojazdem.` + package link `Pakiet {name} od {price}` → `#cennik` (featured package `pack-home-refresh`, "Odświeżenie Domu")

### 4.4 Price (H2): `id="cennik"`, `CounterSection` + `CounterPriceList` + `CounterSafetyPanel` + `CounterPackageCard` ×3
- Eyebrow `Cennik` · **H2** `Pranie kanapy – cena`
- Lede: `Ceny brutto, z dojazdem w Strefie 1. Dokładną kwotę podajemy ze zdjęć, zanim przyjedziemy.`
- Price list: every visible item of group `upholstery`, in the owner's order: Fotel, Krzesło (siedzisko i oparcie), Kanapa 2-osobowa, Kanapa 3-osobowa, Narożnik. Current values from the price list: 90 / 25 / 150 / 180 / 260 zł (see open question 2). Each as "od".
- Note under the list: `Minimalne zamówienie {minOrder}. Silne zabrudzenia i plamy po zwierzętach podnoszą cenę o 20–30%, ale zawsze podajemy ją ze zdjęć przed przyjazdem.` + link `Pełny cennik` only when `siteLinks.priceList` is set. Then: `Wózek lub fotelik po maluchu? ` + link `Pranie wózków i fotelików` → `/poznan/pranie-wozkow-i-fotelikow`.
  (The 20 to 30% is from `docs/source/price-list.md`, "Add-ons and terms"; open question 5.)
- Safety panel: eyebrow `W cenie`, **H3** `Jak pierzemy kanapę`, points:
  - `Najpierw dokładne odkurzanie na sucho, w cenie.`
  - `Pranie ekstrakcyjne z mocnym odsysaniem wody, żeby kanapa szybko schła.`
  - `Hipoalergiczne środki, bezpieczne dla dzieci i zwierząt po wyschnięciu.`
- Packages (cards, no headings), `packageKeys`: `pack-family` (Rodzinny), `pack-home-refresh` (Odświeżenie Domu), `pack-home` (Dom). Names, contents, prices and savings from data (currently 339 zł, 450 zł, 569 zł; see the price list). Do not type them.

### 4.5 How it works (H2): `CounterSection` + `CounterSteps`
Same strings as the stroller page (`counters.stroller.steps`): eyebrow `Trzy kroki, zero wychodzenia z domu`, **H2** `Jak to działa`, steps `Wyślij zdjęcia` / `Dostań cenę i termin` / `Pierzemy u Ciebie` with the stroller texts. Button `Wyślij zdjęcia na WhatsApp` (`data-cta-pos="steps"`).

### 4.6 Before and after (H2): only with real photos
`counter.beforeAfter.length` > 0 renders it, otherwise the heading is absent from the HTML. Eyebrow `Efekty` · **H2** `Kanapy przed i po praniu`. Real jobs only, with the customer's consent.

### 4.7 Drying (H2): same inline pattern as the stroller "seats" band (`bg-muted`)
- Eyebrow `Czas i przygotowanie` · **H2** `Ile schnie kanapa po praniu?`
- Points:
  - `Samo pranie trwa zwykle 1–2 godziny.`
  - `Kanapa schnie 4–8 godzin, zależnie od tkaniny i wietrzenia.`
  - `Zimą otwórz okno lub włącz wentylację, wtedy schnie szybciej.`
  - `Przygotuj dostęp do wody i gniazdka oraz trochę miejsca wokół mebla. Resztę przywozimy.`
- (Sources: price list "upholstery needs 4–8 hours to dry"; customer-stories FAQ "1–2 godziny"; competitor audit.)

### 4.8 Reviews (H2): only with real reviews
Renders only when `counter.reviews.length` > 0. Eyebrow `Opinie` · **H2** `Co mówią klienci`. No invented names, counts or ratings.

### 4.9 FAQ (H2): `CounterFaq`, data from the DB `sofa` entry
Eyebrow `Pytania` · **H2** `Najczęstsze pytania`. Answers in the seed use `{price:key}` tokens. Text identical in the visible FAQ and in the FAQPage markup.

| # | Question | Answer |
|---|---|---|
| 1 | Ile kosztuje pranie kanapy? | `Kanapa 2-osobowa od {price:sofa-2}, 3-osobowa od {price:sofa-3}, narożnik od {price:sofa-corner}, fotel od {price:armchair}. Dokładną cenę podajemy ze zdjęć, zanim przyjedziemy.` |
| 2 | Ile kosztuje pranie kanapy 3-osobowej? | `Od {price:sofa-3}, z dojazdem w Strefie 1. Przy kilku meblach w jednej wizycie jest taniej: zobacz pakiety w cenniku.` |
| 3 | Ile trwa pranie i ile schnie kanapa? | `Samo pranie trwa zwykle 1–2 godziny. Kanapa schnie 4–8 godzin, zależnie od tkaniny i wietrzenia. Zimą otwórz okno lub włącz wentylację.` |
| 4 | Czy odkurzanie jest w cenie? | `Tak. Zawsze najpierw dokładnie odkurzamy na sucho, a dopiero potem pierzemy.` |
| 5 | Czy usuniecie każdą plamę? | `Większość tak, także stare plamy. Niektóre (stary tusz, wybielacz, pleśń) mogą nie zejść całkowicie, i powiemy to uczciwie przed rozpoczęciem.` |
| 6 | Czy usuniecie zapach moczu po psie lub kocie? | `Tak. Stosujemy środek enzymatyczny, który rozkłada mocz u źródła, a nie tylko maskuje zapach. Silne zabrudzenia wyceniamy ze zdjęć.` (**open question 4**; remove if not confirmed) |
| 7 | Czy środki są bezpieczne dla dzieci i zwierząt? | `Tak. Używamy środków hipoalergicznych. Po wyschnięciu tapicerka jest bezpieczna dla całej rodziny.` |
| 8 | Czy warto prać kanapę, zamiast kupować nową? | `Zwykle tak, jeśli konstrukcja jest w dobrym stanie: pranie kosztuje ułamek ceny nowej kanapy, a usuwa plamy, kurz i zapachy. Ocenimy to uczciwie ze zdjęć.` |
| 9 | Co muszę przygotować? | `Wystarczy dostęp do wody i gniazdka oraz trochę miejsca wokół mebla. Sprzęt i środki przywozimy ze sobą.` |

Not included until the owner supplies the answer (open question 6): fabric safety (will it shrink or discolour), leather sofas, insurance (OC) and invoices, "co ile prać kanapę". They are real questions (customer-questions.md); a guessed answer is worse than none.

### 4.10 Area (H2, `band`): `CounterSection band` + `CounterZones`
Eyebrow `Obszar działania` · **H2** `Gdzie dojeżdżamy` · lede `Poznań i okolice, tam gdzie mieszkają rodziny. W Strefie 1 dojazd jest gratis.` + link `Pełna lista miejscowości i stref` only when `siteLinks.serviceArea` is set (not at launch). Zones from data. Town names appear once, here, as text.

### 4.11 Final CTA, footer, sticky bar
Reuse `CounterFinalCta` (`id="kontakt"`, **H2** `Wyślij 2–3 zdjęcia. Cenę podamy dziś.`, promise `t('brand.promise')`, buttons, SMS line `Nie masz WhatsAppa? Wyślij zdjęcia SMS-em na ten sam numer.`, hours line as on the stroller page), `CounterFooter`, `CounterStickyBar` and `CookieBanner` unchanged. Page wrapper as the stroller page: `<div class="pb-[76px] min-[900px]:pb-0" data-counter="sofa">`.

**WhatsApp message** (all buttons on this page; new key `counters.sofa.whatsappMessage`): `Dzień dobry, proszę o wycenę prania kanap, narożników lub foteli. Wysyłam zdjęcia. Miejscowość: ` (trailing space kept; the same wording as the homepage's sofa row, so one message per service).

## 5. Internal links

| From | To | Anchor text | When |
|---|---|---|---|
| **This page** hero/header logo | `/` | logo `alt="Nowiutko"` | always |
| This page, headache card 2 and price note | `/poznan/pranie-wozkow-i-fotelikow` | `pranie wózków i fotelików` / `Pranie wózków i fotelików` | always (stroller page is live at launch) |
| This page, area lede | `/poznan/obszar-dzialania` | `Pełna lista miejscowości i stref` | when `siteLinks.serviceArea` is set |
| This page, price note | `/cennik` | `Pełny cennik` | when `siteLinks.priceList` is set |
| This page, drying band or FAQ 6 | pets and mattress counters | descriptive | when those pages exist; not before |
| **Homepage**, services block | `/poznan/pranie-kanap` | `Pranie kanap i narożników` | the day this page goes live: the sofa row (`Kanapy, narożniki i fotele — Wycena na WhatsApp`) stops being a WhatsApp row and becomes a link row (designer's `homepage-v0` screens 09–10; homepage spec §4.3 "when a counter ships"): set `pagePath: '/poznan/pranie-kanap'` and the row name to `Pranie kanap i narożników` in the services data; the WhatsApp label goes. Armchairs stay covered by the page. |
| **Stroller page**, price section | `/poznan/pranie-kanap` | `Pranie kanap i narożników` | the same day: add the line `Kanapa po maluchu? Pranie kanap i narożników.` after the price note, shown only when `siteLinks.sofa` is set (new key; stays `null` until launch) |
| Stroller page, package card "Rodzinny" | `/poznan/pranie-kanap` | optional | not required |

**Must not appear before it exists:** links to `/cennik`, `/poznan/obszar-dzialania`, `/poznan/wycena`, `/regulamin`, `/cookies`, pets or mattress counters; `href="#"`. No "wkrótce" or "coming soon" anywhere. Contact links as on the stroller page: `wa.me/48736369704`, `tel:+48736369704`, `sms:+48736369704`, `rel="noopener"`, no `nofollow`.

## 6. Structured data (one JSON-LD graph, server-rendered, as on the stroller page)

`useSchemaOrg`, same pattern as `pranie-wozkow-i-fotelikow.vue`; `provider` points to the shared LocalBusiness node (`https://nowiutko.pl/#business`, from `useBusinessSchema()` as in the homepage spec §8). Values below are the current price list; **the page generates them from data** (`areaServed(city.name, zones)`, offers from `counter.priceItems`, FAQ from `counter.faq`), never typed.

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "BreadcrumbList",
      "itemListElement": [
        { "@type": "ListItem", "position": 1, "name": "Strona główna", "item": "https://nowiutko.pl/" },
        { "@type": "ListItem", "position": 2, "name": "Pranie kanap i narożników" }
      ]
    },
    {
      "@type": "Service",
      "name": "Pranie kanap i narożników",
      "serviceType": "Pranie kanap i narożników",
      "provider": { "@id": "https://nowiutko.pl/#business" },
      "areaServed": [
        { "@type": "City", "name": "Poznań" },
        { "@type": "Place", "name": "Suchy Las" }
      ],
      "offers": [
        { "@type": "Offer", "name": "Fotel", "priceCurrency": "PLN", "price": "90.00",
          "priceSpecification": { "@type": "PriceSpecification", "priceCurrency": "PLN", "minPrice": "90.00" } },
        { "@type": "Offer", "name": "Krzesło", "priceCurrency": "PLN", "price": "25.00",
          "priceSpecification": { "@type": "PriceSpecification", "priceCurrency": "PLN", "minPrice": "25.00" } },
        { "@type": "Offer", "name": "Kanapa 2-osobowa", "priceCurrency": "PLN", "price": "150.00",
          "priceSpecification": { "@type": "PriceSpecification", "priceCurrency": "PLN", "minPrice": "150.00" } },
        { "@type": "Offer", "name": "Kanapa 3-osobowa", "priceCurrency": "PLN", "price": "180.00",
          "priceSpecification": { "@type": "PriceSpecification", "priceCurrency": "PLN", "minPrice": "180.00" } },
        { "@type": "Offer", "name": "Narożnik", "priceCurrency": "PLN", "price": "260.00",
          "priceSpecification": { "@type": "PriceSpecification", "priceCurrency": "PLN", "minPrice": "260.00" } }
      ]
    },
    {
      "@type": "FAQPage",
      "mainEntity": [
        { "@type": "Question", "name": "Ile kosztuje pranie kanapy?",
          "acceptedAnswer": { "@type": "Answer", "text": "Kanapa 2-osobowa od 150 zł, 3-osobowa od 180 zł, narożnik od 260 zł, fotel od 90 zł. Dokładną cenę podajemy ze zdjęć, zanim przyjedziemy." } },
        { "@type": "Question", "name": "Ile trwa pranie i ile schnie kanapa?",
          "acceptedAnswer": { "@type": "Answer", "text": "Samo pranie trwa zwykle 1–2 godziny. Kanapa schnie 4–8 godzin, zależnie od tkaniny i wietrzenia. Zimą otwórz okno lub włącz wentylację." } }
      ]
    }
  ]
}
```

(`areaServed` and the FAQ list are shortened here for reading: the real output has the full town list and all nine questions, word for word as in §4.9.)

Rules:
- **Offers follow the visible price list, exactly**: the markup must match what the page shows. `price` and `minPrice` come from the owner's data; the page does not go live until the owner has confirmed the sofa prices (open question 2). `sofa-3`, `sofa-corner` and `dining-chair` are marked "Estimate" in the price list.
- **No** `AggregateRating`, `Review`, `aggregateRating` anywhere, until real reviews are entered by the owner.
- FAQPage only with the visible FAQ; text identical. Google shows FAQ rich results only for a few sites now, so no result enhancement is expected; the markup is for AI answers.
- BreadcrumbList item 1 is the absolute production URL, the last item has no `item` (as on the stroller page, SEO fix #3).
- Service `provider` is the `@id` reference, not a second LocalBusiness copy. Validate the **rendered** HTML in the Rich Results Test.

## 7. Images and alt text

No photos at launch (no stock, no placeholders). Slots the template already supports: the four headache photos (all four or none), the before/after pairs, the review strip. When the owner supplies real photos of sofa jobs: descriptive Polish file names (`pranie-naroznika-przed-po.webp` style, hyphenated, no diacritics), alt text that says what the picture shows (`Narożnik szary przed i po praniu, plama po kawie zeszła` only if true), AVIF/WebP, `width`/`height`, lazy-loaded below the fold. Icons: Lucide with `aria-hidden="true"`; the header logo `alt="Nowiutko"`.

## 8. Indexing, sitemap, robots

`index, follow` once launched; self-canonical; listed in `sitemap.xml` only when live; `robots.txt` unchanged (homepage spec §11). Until the owner says go: the path is in `notLaunched` in `server/data/launch.ts` (production answers 404, out of the sitemap, no link anywhere); staging and local show it.

## 9. Components and data (cleaning-sell-system)

| Need | Where | Action |
|---|---|---|
| Page | new `app/pages/poznan/pranie-kanap.vue` | Copy the structure of `pranie-wozkow-i-fotelikow.vue` (it reads `/api/counters/poznan/sofa`, 404 when missing). Prefer extracting the shared head/JSON-LD/section logic into a composable or `CounterPage` component rather than a 300-line duplicate; developer's call, behaviour must match |
| Copy | `i18n/locales/pl.json` → `counters.sofa` (`meta`, `skipLink`, `whatsappMessage`, `hero`, `proof`, `headache`, `price`, `steps`, `beforeAfter`, `drying`, `reviews`, `faq`, `area`, `final`) | Strings from §4; steps, area and final reuse the stroller strings |
| Layout | `server/data/counters.ts` → `counterLayouts.poznan.sofa` | `heroItemKeys: ['sofa-2','sofa-3','sofa-corner','armchair']`, `priceGroup: 'upholstery'`, `packageKeys: ['pack-family','pack-home-refresh','pack-home']`, `featuredPackageKey: 'pack-home-refresh'`, `slotItemKey: 'sofa-2'`, `reviews: []`, `beforeAfter: []`, `photos: {}` |
| Page + FAQ in the city data | `server/data/poznan.seed.ts` → `pages` (`{ slug: 'pranie-kanap', kind: 'counter', key: 'sofa', published: true }`) and `faq.sofa` (§4.9, with `{price:…}` tokens) | The production database is already seeded (#11), so add a migration or admin import so the new page and FAQ exist there too |
| Launch gate | `server/data/launch.ts` → `notLaunched` | add `'/poznan/pranie-kanap'` until the owner says go, then remove |
| Links | `app/utils/siteLinks.ts` | add `sofa` (null until launch); stroller page shows the new line only when set |
| Homepage row | services data of the homepage (`pagePath`) | flip on launch (§5) |
| Reused unchanged | `CounterHeader`, `CounterHero`, `CounterHeroPriceCard`, `CounterProofBar` (icons fixed by position), `CounterSection`, `CounterProblemCard`, `CounterPriceList`, `CounterSafetyPanel`, `CounterPackageCard`, `CounterSteps`, `CounterBeforeAfter`, `CounterReviews`, `CounterFaq`, `CounterZones`, `CounterFinalCta`, `CounterFooter`, `CounterStickyBar`, `CookieBanner` | |
| Visual | no new design | no sofa-specific accent colour or icon until the designer returns (brand.md allows a light accent per service; not needed for launch) |

## 10. Developer checklist

- [ ] `pranie-kanap.vue` + `counters.sofa` copy + `counterLayouts.poznan.sofa` + seed `pages` and `faq.sofa` + production data migration
- [ ] Title, description, canonical, OG, Twitter as §2 (`titleTemplate: '%s'`, price from `sofa-2`)
- [ ] One `<h1>`, outline exactly §3; before/after and reviews sections absent from the HTML when empty
- [ ] Prices only from data; the hero card, price list, FAQ and JSON-LD agree
- [ ] JSON-LD as §6, validated on the rendered HTML; no rating nodes
- [ ] The two links to the stroller page (card 2, price note); no links to unbuilt pages
- [ ] WhatsApp message as §4.11 on every button; `data-cta` / `data-cta-pos` as the stroller page; analytics only after consent
- [ ] Hours line, final CTA, sticky bar, cookie banner behave as on the stroller page; 320 to 1440 px, no horizontal scroll, no layout shift
- [ ] Gate: `notLaunched` entry on production until the owner says go; then remove it, set `siteLinks.sofa`, flip the homepage row, add to the sitemap (automatic)
- [ ] Tests: add the page to the JSON-LD e2e test (`provider.@id` equals the LocalBusiness `@id`; zero `AggregateRating`)

## 11. Acceptance criteria (SEO desk checks on staging, then production)

1. `curl -s https://nowiutko.pl/poznan/pranie-kanap` returns 200 after launch (404 before), `<html lang="pl-PL">`, one `<h1>` with the exact text, title and description as §2 (49 / 130 characters with the current price), self-canonical.
2. Heading order as §3; "Kanapy przed i po praniu" and "Co mówią klienci" absent from the HTML when there are no photos or reviews.
3. Every number on the page (hero card, price list, packages, FAQ, JSON-LD) equals the price list in the admin.
4. The HTML contains `href="/poznan/pranie-wozkow-i-fotelikow"` and no link to `/cennik`, `/poznan/obszar-dzialania`, `/poznan/wycena`, `/regulamin`, `/cookies` or any page that answers non-200.
5. Rendered JSON-LD: BreadcrumbList (absolute item 1), Service with `provider.@id` = `https://nowiutko.pl/#business`, one Offer per visible price row, FAQPage text identical to the visible FAQ; **0** hits for `AggregateRating` and `Review`.
6. The words "tego samego dnia" and "wkrótce" do not appear on the page; drying is stated as 4–8 godzin.
7. WhatsApp links use the §4.11 message; the phone number is `736 369 704` / `+48736369704`; no `500 000 000`.
8. Staging stays `noindex`; production indexable only after the gate is removed; in `sitemap.xml` only when live.
9. On the launch day: the homepage sofa row is a link with the anchor `Pranie kanap i narożników`, the stroller page shows the new sofa line, and both links return 200.
10. PageSpeed mobile on the live URL: LCP under 2.5 s, CLS under 0.1, INP under 200 ms (otherwise a separate "SEO fix").
11. Search Console 4 to 8 weeks after launch: indexed; impressions for "pranie kanapy poznań" and the secondary queries; click-through on the title. Targets, not forecasts.

## 12. Conflicts and decisions to check

| Item | Finding | Decision in this spec |
|---|---|---|
| URL | strategy and developer issue #49 say `/poznan/pranie-kanap`; keyword map and digital-home-plan say `/poznan/pranie-kanap-i-dywanow` | `/poznan/pranie-kanap` (§1). The keyword map's "sofa & rug" assignment should be corrected after approval (rugs: homepage WhatsApp row, later decision) |
| Launch timing | The early launch (#8) is the stroller page, homepage and privacy page; the sofa counter is #49 (P0 for the full launch) | Build after 20 Nov, gated by `notLaunched` until the owner says go |
| Homepage sofa row | Today a "Wycena na WhatsApp" row (owner, 17 Nov) | Becomes a link row on the day this page goes live (§5); until then it stays as it is |
| Booking | Quote form not live; WhatsApp and phone only | Same CTAs as the stroller page |
| Prices | Sofa 2-seat 150 and armchair 90 are "Market" in the price list; 3-seat 180, corner 260, chair 25 are "Estimate" and the price list says to check them against 5 to 10 competitors before publishing | Page and Offers show whatever the owner has entered; **blocked on confirmation** (open question 2) |
| "tego samego dnia" | A sofa dries in 4 to 8 hours | Not used (§1 header, acceptance 6) |
| Design | No sofa design exists, the designer is paused | Template reuse only (§9) |

## 13. Open questions for the owner

1. **URL:** `/poznan/pranie-kanap` (recommended) or `/poznan/pranie-kanap-i-dywanow`? Decide before the build.
2. **Sofa prices:** confirm 150 zł (2-seat), 180 zł (3-seat), 260 zł (corner), 90 zł (armchair) and 25 zł (chair), after checking competitors as the price list asks. The page and the markup show them to the public. (Competitors seen in the audit: sofa from about 150 to 160 zł, corner from about 200 to 270 zł, net or gross not always stated.)
3. **When should it go live?** The Christmas push (`customer-stories-and-copy.md`, "Goście na Święta?") needs the page indexed weeks before the December rush; the sooner after 20 Nov the better. A seasonal line such as "zarezerwuj termin do 15 grudnia" is in the source copy but is **not in this spec**: it needs a real cutoff from you.
4. **Urine and enzyme treatment:** the price list's own checklist says to promise only what you will do. Do you use an enzyme product for pet urine? (Affects headache card 3 and FAQ 6.)
5. **Surcharge for heavy soiling and pets, 20 to 30%:** OK to show it publicly in the price note? (Source: price list "Add-ons and terms".)
6. **Answers I need for the FAQ** (left out until then): will the fabric shrink or discolour and what do you check first; do you clean leather sofas; OC insurance and invoices; how often should a sofa be cleaned ("co ile prać kanapę").
7. **Drying and cleaning times:** "pranie 1 do 2 godzin, schnięcie 4 do 8 godzin" come from the price list and the source copy. Still true, also in winter?
8. **Photos:** real before/after photos of sofa jobs, with the customer's consent, when you have them. The sections stay hidden until then.

## 14. What the "Page spec: sofa counter" issue will contain (once approved)

- Repo cleaning-sell-system, label `page-spec`, P1: after the 20 Nov launch, before the December rush.
- Link to `seo/pages/sofa-counter.md` (source of truth), the know-first list (URL decision; gated by `notLaunched`; no "tego samego dnia" or "wkrótce"; prices only from data; reuse of the stroller components), the component and data table (§9), the checklist (§10), the acceptance criteria (§11) and the JSON-LD (§6).
- Launch-day tasks (§5): homepage sofa row, stroller-page sofa line, `siteLinks.sofa`, remove the gate.
- After the build: the developer files "Ready for SEO review: sofa counter"; the SEO desk audits staging against §11, then production.

## Sources (read 17 Nov 2026)

`CLAUDE.md`, `seo/strategy.md`, `seo/keywords/keyword-map.md` (autocomplete 8 Nov), `seo/pages/homepage.md`, `docs/prd.md` (S2, S3, S9), `docs/source/customer-questions.md` ("Sofas, carpets and upholstery"), `competitor-audit.md` (rankings 5 Nov), `customer-stories-and-copy.md` (FAQ, "Why us"), `price-list.md`, `digital-home-plan.md`. Read-only: cleaning-sell-system at `af390c4` (`pranie-wozkow-i-fotelikow.vue`, `app/components/counter/*`, `server/data/counters.ts`, `poznan.seed.ts`, `launch.ts`, `siteLinks.ts`, `i18n/locales/pl.json`, `docs/issues.md` #49); cleaning-design `handoff/pages/homepage-v0/README.md`; GitHub issues cleaning-sell-system #8, #12, #13 and cleaning-design #6, #7, #8 (comments read 17 Nov). Nothing here was tested on a live page.
