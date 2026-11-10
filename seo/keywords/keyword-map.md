# Keyword map — Poznań

| | |
|---|---|
| Status | Draft v1, 8 Nov 2026 — seeds from `seo/strategy.md` validated |
| Method | Google autocomplete (`hl=pl`, `gl=pl`), read 8 Nov 2026 from the browser on the owner's computer; Google results pages for the two stroller queries, same day; "Ludzie pytają też" from those pages and from `docs/source/customer-questions.md` (5 Nov) |
| Not yet | **No search volumes.** Autocomplete shows that a query is searched, not how often. Next step: a Google Keyword Planner export from the owner (free Google Ads account) for the queries below. |

## How to read this

- **Validated** = the query or a close variant appears in Google autocomplete for Polish searches.
- **Weak** = only a spelling variant appears (e.g. without Polish letters), or only the generic form without the town.
- **Not found** = no autocomplete suggestion. That doesn't mean zero searches; the query can still be a good FAQ question if it came up in "Ludzie pytają też" or in customer research.
- One **primary** query per page. A query listed under one page is not targeted by any other.

## 1. Seed check (all pages)

| Page | Seed in strategy | Verdict | What autocomplete shows instead / as well |
|---|---|---|---|
| Stroller counter | pranie wózka dziecięcego Poznań | Validated | "pranie wozka dzieciecego poznan", "pranie wózków dziecięcych poznań", "pranie wozkow poznan" |
| | pranie wózków Poznań | Validated | Same group. Also "czyszczenie wózków dziecięcych poznań" |
| | czyszczenie wózka | Validated | "czyszczenie wózka dziecięcego (cena)", "czyszczenie wozka dzieciecego poznan", "czyszczenie gondoli wózka", "czyszczenie kół wózka", "czyszczenie wozka cybex" |
| | pranie fotelika samochodowego | Validated | "pranie fotelika samochodowego cena", "pranie fotelików samochodowych", city variants for Warszawa, Łódź, Wrocław — **no Poznań variant in autocomplete** (the Poznań query still returns a map pack, see brief) |
| | jak prać fotelik Cybex / Maxi-Cosi | Validated, strong | "jak prać fotelik cybex (sirona)", "jak prać fotelik maxi cosi", "jak prać fotelik avionaut pixel", "jak prać fotelik britax romer", "jak prać fotelik samochodowy joie", "jak prać pasy w foteliku", "jak prać pokrowiec z fotelika …" |
| | ile kosztuje wypranie wózka | Validated | "ile kosztuje pranie wózka dziecięcego", "ile kosztuje czyszczenie wózka dziecięcego"; also in "Ludzie pytają też" |
| Sofa counter | pranie kanapy Poznań | Validated | "pranie kanapy poznań cena", "pranie kanapy poznań olx", "pranie tapicerki kanapy poznań" |
| | pranie tapicerki Poznań | Validated, **shared with car** | Autocomplete mixes furniture and car: "pranie tapicerki meblowej poznań" vs "pranie tapicerki samochodowej poznań" |
| | pranie narożnika Poznań | Validated (plural) | "pranie narożników poznań" |
| | ile kosztuje pranie kanapy | Validated | "… z dojazdem", "… trzyosobowej", "… narożnej", "… w domu", "… poznan" |
| | ile schnie kanapa po praniu | Validated | "… po praniu karcherem", "… po praniu odkurzaczem piorącym" |
| | czy warto prać kanapę | Not found | Keep as an FAQ (came up in customer research) |
| Pets counter | usuwanie zapachu moczu z kanapy | Validated | "… moczu kota z kanapy", "… moczu psa z kanapy", "usuwanie moczu z kanapy" |
| | plama z moczu kota kanapa | Validated (shorter) | "plama po moczu kota", "plama po kocim moczu" — mostly DIY intent |
| | pranie kanapy po psie Poznań | Weak | Without Poznań: "pranie kanapy po kocie", "… po sikach kota", "… po moczu" |
| Mattress counter | pranie materaca Poznań | Validated | "pranie materacy poznań", "pranie pokrowca na materac poznan" |
| | ile kosztuje pranie materaca | Validated | "… 160x200", "… w domu", "… w pralni" |
| | czy pranie usuwa roztocza | Not found | Keep as an FAQ (customer research) |
| | ile schnie materac | Validated | "ile schnie materac po praniu" |
| Car counter | pranie tapicerki samochodowej Poznań | Validated | "… poznań cennik", "… poznań cena", "… poznań rataje" |
| | mobilny detailing Poznań | Validated, **caution** | Led by a competitor brand (Detailmann); "detailing" implies exterior work too. Use as a secondary term only, with "wnętrze" made clear |
| | ile schnie tapicerka samochodowa | Validated | "… po praniu", "… w aucie" |
| Service area | pranie kanapy Swarzędz | Validated | "pranie tapicerki swarzędz", "pranie tapicerki meblowej swarzędz", "pranie tapicerki samochodowej swarzędz" |
| | pranie kanapy Komorniki | Validated (as tapicerka) | "pranie tapicerki komorniki", "pranie mebli komorniki", "czyszczenie kanapy komorniki" |
| | pranie kanapy Luboń | Weak | Only "pranie kanapy lubon" |
| | pranie kanapy Suchy Las | Not found | — |
| Homepage | pranie tapicerki Poznań i okolice | Not found as written | Fine as a broad phrase on the homepage; don't build anything on it |

**New queries worth adding** (not in the seeds): "pranie tapicerki z dojazdem do klienta" (exists, matches the mobile model; for the homepage), "jak odświeżyć używany wózek" (second-hand stroller angle, stroller page), "pranie gondoli (wózka)" (stroller page).

## 2. Assignment: one primary per page

| Page (URL — see note) | Primary | Secondary (same page) |
|---|---|---|
| Stroller & car seat counter `/poznan/pranie-wozkow-i-fotelikow` | **pranie wózków dziecięcych poznań** | pranie wózka dziecięcego poznań · pranie wózków poznań · czyszczenie wózków dziecięcych poznań · czyszczenie wózka dziecięcego poznań · pranie fotelika samochodowego poznań · czyszczenie fotelika samochodowego · pranie gondoli |
| Sofa & rug counter `/poznan/pranie-kanap-i-dywanow` | **pranie kanapy poznań** | pranie tapicerki meblowej poznań · pranie narożników poznań · pranie dywanów poznań (drop-off rug laundries dominate this one) |
| Pets counter `/poznan/usuwanie-zapachu-po-zwierzetach` | **usuwanie zapachu moczu z kanapy** (+ Poznań on page) | usuwanie zapachu moczu kota / psa z kanapy · pranie kanapy po kocie |
| Mattress counter `/poznan/pranie-materaca` | **pranie materaca poznań** | pranie materacy poznań · ile kosztuje pranie materaca 160x200 |
| Car counter `/poznan/pranie-tapicerki-samochodowej` | **pranie tapicerki samochodowej poznań** | pranie tapicerki samochodowej poznań cennik · mobilny detailing wnętrza (secondary only) |
| Service area `/poznan/obszar-dzialania` | **pranie tapicerki z dojazdem poznań i okolice** | town names as plain text |
| Town page (only with real local proof) `/poznan/swarzedz` | **pranie tapicerki swarzędz** | pranie kanapy swarzędz · pranie tapicerki samochodowej swarzędz |
| Homepage `/` | brand name + **pranie tapicerki poznań** | pranie tapicerki z dojazdem do klienta |

**Conflicts settled:**
- "pranie tapicerki poznań" → homepage (broad). Sofa counter takes "pranie kanapy" + "tapicerki meblowej"; car counter takes "tapicerki samochodowej". Neither counter uses the bare phrase as its H1.
- Child car seats ("fotelik samochodowy") → stroller counter, never the car counter. The car counter links across.
- Price questions ("ile kosztuje …") stay on each counter's FAQ. No separate "cennik" page targets them; `/cennik` is navigational.

**URL note:** decided by the owner 10 Nov 2026: `/poznan/pranie-wozkow-i-fotelikow` (the page serves both stroller and car-seat queries). The PRD still says `/poznan/pranie-wozkow`; the change goes to the developer in the "SEO note: baseline".

## 3. How-to queries: not for the counter

"jak prać fotelik cybex / maxi cosi / avionaut / britax", "jak prać pasy w foteliku", "pranie fotelika samochodowego w pralce", "jak wyczyścić wózek z pleśni" are strong but DIY. A sales page won't rank for them and shouldn't try. Later (after launch, not v1): one guide, "Jak prać fotelik samochodowy — Cybex, Maxi-Cosi, Avionaut, Britax", written from the manufacturers' manuals, linking to the counter. Owner's call when there's time to write it.

## 4. Changes to `seo/strategy.md` — approved by the owner and applied 10 Nov 2026

1. **"Nobody owns strollers" is out of date.** On 8 Nov the Google results page for "pranie wózków dziecięcych poznań" shows Poznań pages, not Warsaw specialists: two drop-off laundry pages from Zawsze Czysto (from 30–35 zł, about 3 days), CleanWhale's Poznań stroller page ("od 99 zł" in the title), Kubus Serwis (stroller repair and cleaning, Facebook), Marek Pluta (page under construction) and OLX. The niche is **contested but weak**: none of them offers same-day cleaning at the customer's door with prices, brand-specific car-seat care and a real FAQ. Suggested wording: "Stroller pages exist but are weak: drop-off laundries, a booking platform and an empty page. Nobody offers same-day cleaning at your door with brand-specific car-seat care."
2. **Stroller URL** → `/poznan/pranie-wozkow-i-fotelikow` (see note above).
3. **Suburbs:** autocomplete supports Swarzędz and Komorniki (as "pranie tapicerki …"); Luboń is weak and Suchy Las doesn't appear. If a first town page is earned, Swarzędz is the likeliest.
