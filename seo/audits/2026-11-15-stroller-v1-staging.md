# SEO audit: stroller counter, `stroller-v1` on staging

| | |
|---|---|
| Page | https://nw-st-7k2.codigo-studio.com/poznan/pranie-wozkow-i-fotelikow |
| Request | cleaning-seo #1 "Ready for SEO review: stroller-v1 on staging" |
| Built from | cleaning-design `stroller-v1` (`3ad46b2`); cleaning-sell-system `main` at `dbf33d2` (repo now at `04be221`) |
| Checked against | `seo/briefs/stroller-counter.md`; `docs/seo-requirements.md` in cleaning-sell-system |
| Date / method | 15 Nov 2026. Browser on the owner's computer (the cloud can't reach staging). Raw server HTML fetched without JavaScript; JSON-LD parsed; duplicate URLs fetched; phone check at 375×812. |
| Status | **Draft, for the owner's review.** No "SEO fix" issues filed yet. |

## Verdict

**No launch blockers (P0) on this page.** It follows the brief closely: title, meta, H1, H2 order, prices as text, FAQ as real HTML, the right structured data types and no invented ratings. Staging is hidden properly. Two P1 schema fixes and two P2 tidy-ups below, plus three content facts the owner needs to confirm.

## What passes

| Check | Result |
|---|---|
| Staging hidden | `robots.txt` → `Disallow: /`; `<meta name="robots" content="noindex, nofollow">`; `X-Robots-Tag: noindex, nofollow` header. ✅ |
| Server rendering | All headings, prices and all 7 FAQ answers are in the HTML without JavaScript (61 KB document, ~965 words). ✅ |
| Title | `Pranie wózków i fotelików Poznań – u Ciebie, od 80 zł` (53 chars), brief option 1. ✅ |
| Meta description | Brief option 1 (142 chars). ✅ |
| H1 | One: `Pranie wózków i fotelików dziecięcych w Poznaniu i okolicach` (option a, as an eyebrow). ✅ |
| H2 order | Headache → price → steps → car seats by brand → FAQ → area → final call. Before/after and reviews are absent from the HTML, so there are no empty headings. ✅ |
| Prices | Text, gross "od" values from data; no image in the hero. ✅ |
| FAQ | 7 native `<details>`; text identical to the FAQPage markup. ✅ |
| Structured data | One JSON-LD graph: WebSite, WebPage, BreadcrumbList, Service with 6 Offers, FAQPage. No AggregateRating or Review. ✅ (two fixes below) |
| Canonical | Self-referencing; the variants with a trailing slash, a capital `P` and `?utm_source=` all point to the clean URL. ✅ |
| Language | `<html lang="pl-PL">`, `og:locale pl_PL`. ✅ |
| Phone layout (375 px) | No sideways scroll; 16 px body text; H1, headline and the first price card on the first screen. ✅ |
| Speed (indicative) | TTFB 0.2 s, LCP 0.32 s (the headline text), CLS 0, measured on the owner's computer and network. **Not** a 4G mid-range phone; a PageSpeed Insights run is still needed (see "Not checked"). |

## Findings

### P1: fix before launch

**1. BreadcrumbList uses a relative URL.**
- *Evidence:* `itemListElement[0].item` is `"/"`.
- *Why it matters:* Google needs a full URL for every breadcrumb item except the last; a relative one can make the breadcrumb invalid in the Rich Results Test.
- *Fix:* output the absolute URL (`https://nowiutko.pl/` on production), built from the site URL setting so it follows the domain.

**2. Service markup: area too narrow, no provider.**
- *Evidence:* `Service.areaServed` is a single `City: Poznań`; there's no `provider`.
- *Why it matters:* the core market is the suburbs. The brief asked for Poznań plus the Zone 1 and Zone 2 towns, and without `provider` the Service isn't tied to the business.
- *Fix:*
  - `areaServed` = a list of `City`/`Place` entries generated from the towns list (Poznań + Zone 1 + Zone 2), so it stays editable by the owner.
  - `provider` = `{ "@id": "https://nowiutko.pl/#business" }`, pointing at the LocalBusiness node coming in #45. The `provider` half can land with #45.

### P2: should fix, doesn't block launch

**3. URL variants answer 200 instead of redirecting.**
- *Evidence:* `/poznan/pranie-wozkow-i-fotelikow/` and `/Poznan/pranie-wozkow-i-fotelikow` both return 200. The canonical is correct, so there's no indexing harm.
- *Why it matters:* `seo-requirements.md` asks for "no trailing-slash duplicates", and a single URL per page keeps links and analytics clean.
- *Fix:* 301 the trailing-slash and upper-case variants to the lowercase, no-slash URL. Do it in the same place as the other redirects (#45), without chains.

**4. Header phone link is a small tap target.**
- *Evidence:* the `500 000 000` link in the header measures 99×19 px at 375 px wide.
- *Why it matters:* the PRD sets 44 px tap targets (WCAG 2.2 AA in PRD §6). It's also the main call button for some visitors.
- *Fix:* pad the link to at least 44 px high. The visual size can stay the same.

### Note: harmless module defaults (no action needed)
`WebPage.potentialAction: ReadAction` and an empty `WebSite.workTranslation: []` come from the SEO module's defaults. They're valid and do nothing; drop `workTranslation` if it's a one-line config change.

## For the owner to confirm (content, not code)

These are claims on the page that only you can vouch for:
1. **Car-seat brands named in the H2 and FAQ:** *Cybex, Maxi-Cosi, Britax i Avionaut*. The brief says to name only brands whose cleaning manuals you've checked. I checked Maxi-Cosi's and Cybex's published guidance (cover per label, harness wiped, no harsh chemicals); Britax and Avionaut are unchecked. Keep them only if you've read their manuals.
2. **Mould answer:** "Często tak, ale stare przebarwienia po pleśni mogą nie zejść w całości." Is that what you can deliver?
3. **Drying time:** "schnięcie trwa 3–5 godzin". This is a new, specific number, not in the brief or price list ("usable the same day"). Fine if it's your real experience.

## Observation for the designer (not an SEO fix)

On a phone, the cookie banner covers the bottom quarter of the first screen, including the price card, until the visitor answers it. That doesn't hurt SEO (Google doesn't penalise consent banners), but the price is the page's main hook. Worth a look at a slimmer banner. The owner decides whether to raise it.

## Answers to the developer's two questions

1. **AI crawlers: recommended on for production.**
   - `llms.txt` and Markdown copies: yes. They're cheap, and they fit the strategy's AI-answers priority (clear facts about area, prices and drying times). Honestly, the evidence that `llms.txt` changes AI citations is thin, so treat it as low-cost, not a lever.
   - `Content-Signal` in robots.txt: suggested `search=yes, ai-input=yes`, so search and AI answers may use and cite the pages.
   - `ai-train` (use for model training) is a business choice, not an SEO one. **Owner decides**; `no` is a reasonable default.
2. **Offer shape for "od" prices: keep it.** `price` + `priceSpecification.minPrice` in PLN is valid and honest for from-prices. No change.

## Not checked yet (do at the production audit)

From #45 and the developer's known-gaps list:
- LocalBusiness node (service-area business, no street address), `og:image`, redirects.
- Sitemap rules: the sitemap currently lists the placeholder homepage. On production, list only real, indexable pages, and add `Sitemap:` to robots.txt.
- Canonical and `og:url` on `https://nowiutko.pl`; robots/noindex lifted only there.
- Image file names and alt text (no photos yet); internal links to `/cennik`, `/poznan/obszar-dzialania` and the quote form (pages not built).
- Real phone/WhatsApp number; analytics after consent; Search Console verification.
- **Core Web Vitals in the lab:** a PageSpeed Insights mobile run, once the page is reachable for it (staging may not be).
- Rich Results Test on the rendered production page.

## Proposed issues (filed only after the owner says "go")

| Issue in cleaning-sell-system | Label | Priority |
|---|---|---|
| SEO fix: BreadcrumbList item must be an absolute URL | `seo-fix` | P1 |
| SEO fix: Service areaServed from the towns list + provider link to LocalBusiness | `seo-fix` | P1 |
| SEO fix: 301 trailing-slash and upper-case URL variants | `seo-fix` | P2 |
| SEO fix: header phone link tap target ≥ 44 px | `seo-fix` | P2 |
| Comment on cleaning-seo #1 | — | Answers to the two questions + summary; keep #1 open until the P1s are fixed |
