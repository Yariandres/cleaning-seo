# SEO note: early launch (stroller page on nowiutko.pl)

| | |
|---|---|
| Status | **Draft 16 Nov 2026, for the owner's review.** Not sent. After "go": Part A becomes the body of one issue "SEO note: early launch" (`seo-note`) in cleaning-sell-system; Part B becomes a comment on cleaning-seo #2. |
| For | Developer, cleaning-sell-system [#8](https://github.com/Yariandres/cleaning-sell-system/issues/8) point 5 (the #45 subset). Owner priority: cleaning-seo [#2](https://github.com/Yariandres/cleaning-seo/issues/2). |
| Target | Live by Fri 20 Nov 2026 |
| Read for this | `docs/seo-requirements.md`, `docs/issues.md`, `docs/HANDOFF.md`, `nuxt.config.ts`, `server/data/launch.ts`, `server/middleware/canonical-url.ts` in cleaning-sell-system at `cfaf569`; SEO fixes #3–#6; design handover `stroller-v1.1` §9–10; staging audit `seo/audits/2026-11-15-stroller-v1-staging.md`. **Nothing here was tested on production: it isn't live yet.** |

---

## Part A. Issue body for the developer

This is the part of `docs/seo-requirements.md` that must be true on **https://nowiutko.pl** on day one. It builds on what is already done (staging hidden, canonical, SEO fixes #3, #5, #6, `areaServed` half of #4, brand-host 301s, launch gate) and doesn't repeat it, except where it must be re-checked on the production host.

**P0** = must be true when the site goes live. **P1** = within a few days of go-live. I run the production audit the same day (Rich Results Test, PageSpeed, Search Console).

Live pages at this launch:

| Page | Indexable | In sitemap | robots.txt |
|---|---|---|---|
| `/poznan/pranie-wozkow-i-fotelikow` | yes | yes | allowed |
| `/` (homepage v0) | yes | yes | allowed |
| Privacy page | yes | yes | allowed |
| `/admin/**` | **no** (`X-Robots-Tag: noindex`, as now) | no | `Disallow: /admin` |
| `/poznan/wycena`, `/api/quote` | 404 on production (launch gate, as now) | no | not listed |
| Everything else (`/cennik`, `/poznan/obszar-dzialania`, `/cookies`, `/regulamin`, other counters) | real **404** status | no | not listed |

### P0: blocks go-live

**1. Production is indexable, and only on nowiutko.pl.**
- On `https://nowiutko.pl`: no `noindex` in the meta robots tag and no `X-Robots-Tag: noindex` header on the three public pages.
- Staging stays exactly as it is (robots.txt `Disallow: /`, meta and header `noindex, nofollow`).
- No other host serves the production app with a 200: only the four brand hosts are attached in Dokploy; no auto-generated or test domain.
- *Check:* `curl -sI https://nowiutko.pl/poznan/pranie-wozkow-i-fotelikow | grep -i x-robots` returns nothing; `curl -s … | grep -i 'name="robots"'` shows no `noindex`; the same two commands on staging still show `noindex, nofollow`.

**2. Nothing unbuilt is reachable, linked or listed.**
- No link on any live page points to a URL that isn't live (quote form, `/cennik`, `/poznan/obszar-dzialania`, `/cookies`, `/regulamin`). Both privacy links (footer, cookie banner "Szczegóły") resolve.
- Unbuilt URLs answer with a real 404 status, not a 200 "not found" page and not a redirect to the homepage.
- *Check:* `curl -sI https://nowiutko.pl/cennik` and `/poznan/wycena` → `404`. Crawl the three pages (the module's link checker, or by hand) → zero internal links to a non-200 URL.

**3. `/` answers 200 with a real page on the same day.**
- The logo and the breadcrumb point at `/`. Preferred: homepage v0 (brief follows as "SEO brief: homepage-v0").
- If homepage v0 is late: keep a simple page at `/` that answers 200, is indexable, and has a normal text link to the stroller page. The current placeholder has no link, and it only says the site is coming; ask the designer for the wording. **Don't** 301 `/` to the stroller page (a permanent redirect of the homepage is slow to undo in Google). A 302 is the last resort; if you use it, leave BreadcrumbList out until `/` is a page.
- *Check:* `curl -sI https://nowiutko.pl/` → `200`; the HTML contains `href="/poznan/pranie-wozkow-i-fotelikow"`.

**4. Canonical: absolute, apex, HTTPS, self-referencing.**
- Every public page: `<link rel="canonical" href="https://nowiutko.pl/…">`, no `www`, no trailing slash (except `/`), no query string. `og:url` is the same URL.
- *Check:* view source on each page; also load the stroller page with `?utm_source=test` → canonical unchanged. No staging host name anywhere in the production HTML: `curl -s https://nowiutko.pl/poznan/pranie-wozkow-i-fotelikow | grep -c codigo-studio` → `0`.

**5. Redirects: one 301, straight to the final URL.**

| Request | Answer |
|---|---|
| `https://www.nowiutko.pl/x` | 301 → `https://nowiutko.pl/x` |
| `https://nowiutko.com/x`, `https://www.nowiutko.com/x` | 301 → `https://nowiutko.pl/x` |
| `http://nowiutko.pl/x` | 301 or 308 → `https://nowiutko.pl/x` |
| `http://www.nowiutko.pl/x`, `http://nowiutko.com/x` | ideally one hop to `https://nowiutko.pl/x`. Two hops (HTTPS first, then host) are acceptable if Traefik forces them; never more, and never a 302. |

- Path and query string are kept. Certificates are valid on all four hosts (a certificate error on `www` or `.com` breaks the redirect for visitors).
- Trailing-slash and upper-case 301s (#5) must not add a hop on top of a host redirect.
- *Check:* `curl -sIL` on each row; count the `HTTP/` lines and read each `location:`.

**6. Sitemap and robots.txt list live pages only.**
- `https://nowiutko.pl/sitemap.xml`: exactly the three indexable URLs in the table above, absolute, on the apex, each answering 200. Add a page to it only when it ships. `lastmod` only if it is the real change date.
- `https://nowiutko.pl/robots.txt`:
  ```
  User-agent: *
  Disallow: /admin

  Sitemap: https://nowiutko.pl/sitemap.xml
  ```
  Nothing the public pages need to render is disallowed (`/_nuxt/`, fonts, images, and any `/api/` call a public page makes in the browser).
- `Content-Signal` line: add it when the owner has decided the last value. Until then leave the line out; it doesn't block go-live.
  ```
  Content-Signal: search=yes, ai-input=yes, ai-train=<owner's call: yes or no>
  ```
- *Check:* open both files; every `<loc>` → 200 and carries a self-canonical.

**7. Structured data: LocalBusiness node, and Service `provider` pointing at it (closes SEO fix #4).**
One JSON-LD graph, server-rendered, on the stroller page (and the same LocalBusiness node on the homepage):

| Node | Requirement |
|---|---|
| **LocalBusiness** | `@id`: `https://nowiutko.pl/#business` · `name`: `Nowiutko` (exactly; no city, no keywords) · `url`: `https://nowiutko.pl/` · `telephone`: `+48736369704` from `{business:phone}` · `areaServed`: the same generated list as the Service (Poznań + Zone 1 + Zone 2 towns) · `address`: `PostalAddress` with **only** `addressLocality: "Poznań"`, `addressRegion: "wielkopolskie"`, `addressCountry: "PL"`. No `streetAddress`, no `postalCode`, no `geo` pin: the business has no public address and we don't invent one. · `logo`/`image`: the brand logo, absolute URL. |
| | Leave out for now: `openingHoursSpecification` (no hours are set), `priceRange`, `sameAs` (no profiles yet), `aggregateRating`, `review`. |
| **Service** | Add `provider: {"@id": "https://nowiutko.pl/#business"}`. Everything else as on staging (`areaServed` list from #4, six Offers). |
| **Offer** | Unchanged: `price` + `priceSpecification.minPrice`, `priceCurrency: "PLN"`, from the production price list. |
| **FAQPage** | Unchanged: 7 questions, text identical to the visible answers. |
| **BreadcrumbList** | Unchanged from #3: item 1 `https://nowiutko.pl/` (absolute, production host), last item without `item`. |
| **AggregateRating / Review** | Absent, everywhere, until the owner enters real reviews. |

- Note on `address`: Google's LocalBusiness page lists `address` as required and says nothing about businesses without premises. A locality-only address is the honest version. If the Rich Results Test reports it as an error, tell me before adding anything to it.
- *Check:* [Rich Results Test](https://search.google.com/test/rich-results) on the live URL: Breadcrumbs and FAQ detected, no errors; in the rendered JSON-LD the Service's `provider.@id` equals the LocalBusiness `@id` in the same graph; search the HTML for `AggregateRating` → 0 hits. Please add the `provider` check to the existing JSON-LD e2e test.

**8. Real business data in the production database before go-live.**
- Production seeds the placeholder phone 500 000 000. The real number (+48 736 369 704) must be in the header, hero, final section, sticky bar, `tel:`, `sms:`, `wa.me` links and JSON-LD before the page is indexable. Google and the Business Profile must see the same number.
- Title and meta description render the price from production data (`…od 80 zł`), not an empty or staging value.
- *Check:* `curl -s … | grep -c '500 000 000\|500000000'` → `0`; `grep -c 48736369704` > 0; read `<title>` and the meta description.

**9. Open Graph tags** (the link will be shared on WhatsApp and Facebook from day one).
- On each public page: `og:title`, `og:description`, `og:url` (= canonical), `og:type` (`website`), `og:site_name` (`Nowiutko`), `og:locale` (`pl_PL`), `twitter:card` (`summary_large_image`).
- *Check:* view source. (Image: P1, item 12.)

**10. Unchanged on-page elements survive the v1.1 build.**
- Title, meta description, one `<h1>` (the eyebrow), H2 order and the seven FAQ answers as in the audit; all in the server HTML without JavaScript; hidden sections (before/after, reviews, next free slot) absent from the HTML, not just hidden with CSS. `<html lang="pl-PL">`.
- The WhatsApp, `tel:` and `sms:` links are plain `<a href>`; `wa.me` links carry no `nofollow` (see Part B).
- *Check:* `curl` the page and read it; I repeat this in the production audit.

**11. Search Console (owner's step; nothing to build, but day one).**
- Owner: add a **Domain property** for `nowiutko.pl` and enter its TXT record at GoDaddy together with the other DNS records (HANDOFF owner step 7 already says this). A Domain property covers `www`, the apex, HTTP and HTTPS in one, and DNS is its only verification method. Add the TXT record next to any existing TXT (SPF); don't replace it. It can take a day or two to be picked up, and it must stay in DNS afterwards.
- On go-live day: submit `https://nowiutko.pl/sitemap.xml`, then URL Inspection → "Request indexing" for the stroller page and `/`. I'll walk the owner through it in the production audit.
- No verification meta tag or HTML file is needed in the app.

### P1: within days of go-live

**12. `og:image`.** One static 1200×630 image (JPG or PNG, under ~300 KB), absolute HTTPS URL on nowiutko.pl, with `og:image:width`, `og:image:height`, `og:image:alt`. Use the designer's final share image (cleaning-design #5 scope item 3). If it is ready by Friday, ship it with the launch: Facebook and WhatsApp cache the first preview they fetch. The dynamic `ogImage` module can stay off. *Check:* [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/) shows the image, title and description.

**13. Contact-click events.** With no form, these are the only conversion signal. Send one GA event per click on the `data-cta` links (suggested names: `contact_click` with parameters `method` = `whatsapp|phone|sms` and `position` = `header|hero|steps|final|sticky`), **only after analytics consent**. *Check:* GA DebugView after accepting cookies; nothing sent after declining.

**14. Photos, if they arrive.** Each photo: descriptive Polish file name, the owner's alt text, AVIF/WebP, `width`/`height` set, lazy-loaded below the fold (brief §6). No stock photos, no placeholders in production.

**15. Speed on a phone.** I run PageSpeed Insights (mobile) on the live URL and file anything outside LCP < 2.5 s, CLS < 0.1, INP < 200 ms as a separate "SEO fix". Watch the cookie banner and sticky bar for layout shift.

**16. `Content-Signal` line** (item 6) once the owner decides `ai-train`.

**17. Close SEO fix #4** once item 7 is live and the Rich Results Test passes; I then close review cleaning-seo #1.

### Deferred: not for this launch (so nobody guesses)

- In-content links to `/cennik` and `/poznan/obszar-dzialania`: restore each when its page ships (handover §9).
- Quote form `/poznan/wycena`: stays 404 on production, out of the sitemap; `noindex, follow` when it launches.
- `llms.txt` and Markdown copies (`aiReady`): stay off until the homepage and at least one more counter exist; turn on only if it lists live pages only.
- `AggregateRating` / `Review` markup and the review strip: only with real reviews entered by the owner.
- `sameAs`, `openingHoursSpecification`, `priceRange` on LocalBusiness: when the Business Profile, Facebook Page and working hours exist.
- Town pages, the other counters, the price-list and service-area pages, their sitemap entries.
- Dynamic per-page share images; `hreflang` (one language, not needed); removing the module's empty `WebSite.workTranslation` (cosmetic).
- Bing Webmaster Tools and Apple Business Connect: owner steps, in the Google Business Profile plan.
- The rest of `docs/seo-requirements.md` and #45 stays open for the full launch. I update `docs/seo-requirements.md` after this launch with what was learned here.

---

## Part B. Answers to the designer

Questions from the comment on cleaning-seo #2 (`stroller-v1.1`). Google documentation read 16 Nov 2026.

**1. Removing the links to `/cennik` and `/poznan/obszar-dzialania` until those pages ship: acceptable?**
**Yes.** A link to a page that doesn't exist is worse than no link, and the page already carries the prices and the town list as text, so nothing a searcher needs is lost. Keep the note in the handover: each link comes back, with descriptive anchor text, the day its page ships. Until then the stroller page depends on one inbound link, from homepage v0; that goes in the homepage-v0 brief.

**2. Should the `wa.me` links carry `rel="nofollow"`?**
**No.** Google asks for `nofollow` only where you don't want your site associated with the linked page, and says regular links need no `rel` at all ([Qualify your outbound links to Google](https://developers.google.com/search/docs/crawling-indexing/qualify-outbound-links)). The WhatsApp link is our own contact channel, not an ad or user content. Keep `rel="noopener"` as it is; no `sponsored`, no `ugc`.

**3. `telephone` or `contactPoint` on LocalBusiness?**
**`telephone`, on the LocalBusiness node: `"+48736369704"`,** from `{business:phone}`. Google's [LocalBusiness documentation](https://developers.google.com/search/docs/appearance/structured-data/local-business) lists `telephone` as a recommended property (the primary customer number, with country code) and doesn't use `contactPoint` at all. One number in one place also keeps it identical to the page and the Google Business Profile. No `contactPoint`.

**4. Is BreadcrumbList safe if `/` isn't live the same day?**
**Safe only if `/` answers 200 that day, so make that the rule.** Google's [Breadcrumb documentation](https://developers.google.com/search/docs/appearance/structured-data/breadcrumb) doesn't say the linked URL must be live, but it does require at least two items, so the trail can't be cut down to the current page alone. If homepage v0 is late, a simple page at `/` with a link to the stroller page keeps the breadcrumb valid (checklist item 3). If `/` would be a 404 or a redirect to the stroller page, leave BreadcrumbList out until the homepage exists; the other markup isn't affected.
