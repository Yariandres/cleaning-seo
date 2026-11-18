# Audit: homepage v0 and stroller-v1.4, staging and production (18 Nov 2026)

| | |
|---|---|
| Pages | `/` and `/poznan/pranie-wozkow-i-fotelikow` |
| Hosts | staging `nw-st-7k2.codigo-studio.com`, production `nowiutko.pl` (already live and indexable) |
| Against | `seo/pages/homepage.md` §13, `seo/notes/early-launch-checklist.md` (cleaning-sell-system #10) |
| Review requests | cleaning-seo #3 (homepage + stroller-v1.3), #1; handoff cleaning-sell-system #14 (stroller-v1.4) |
| Method | `curl` and HTML/JSON-LD parsing, 18 Nov 2026. **Not run:** Rich Results Test, Schema Markup Validator, PageSpeed, Facebook Sharing Debugger, Search Console. |

## Passes

- **Homepage:** 200, `lang="pl-PL"`, one H1, outline as in spec §3, title and description as in §2, self-canonical and `og:url` on the host, OG/Twitter tags with the static share image (200). Stroller link in server HTML with anchor `Pranie wózków i fotelików`. Four "Wycena na WhatsApp" rows, hours line present, five example towns. No FAQ/Service/Offer/Breadcrumb/rating markup. No `500 000 000`; `48736369704` present; no staging host in production HTML.
- **Stroller page:** title `…od 80 zł`, one H1, canonical, OG with its own share image. JSON-LD: LocalBusiness, Service (`provider` → `#business`), Breadcrumb (absolute first item), FAQPage, 6 Offers, `areaServed` 22 entries. No AggregateRating/Review. Images: alt text, width/height, lazy below the fold.
- **Shared LocalBusiness node** identical on both pages (closes SEO fix #4, cleaning-sell-system #4).
- **Production:** indexable (meta and header). `robots.txt` and sitemap as decided (3 URLs; `Content-Signal` with `ai-train=yes`; no `Disallow: /admin`). `/admin` → `x-robots-tag: noindex, nofollow`. `/cennik`, `/poznan/wycena` → 404. `www` → one 301. Trailing-slash/uppercase → one hop. `/brand/logo.png` 200, 710×200.
- **Staging:** `noindex, nofollow` in meta and header, `Disallow: /`.

## PageSpeed Insights, mobile, production (18 Nov 2026, ~12:00; Lighthouse 13.6.0, Moto G Power, slow 4G)

| Page | Perf | A11y | Best pr. | SEO | LCP | TBT | CLS |
|---|---|---|---|---|---|---|---|
| `/` | 91 | 100 | 100 | 100 | 2.4 s | 220 ms | 0 |
| `/poznan/pranie-wozkow-i-fotelikow` | 92 | 100 | 92 | 100 | 2.6 s | 120 ms | 0.002 |

LCP < 2.5 s: homepage passes, stroller page is 0.1 s over in the lab (slow-4G emulation); CLS < 0.1 passes. INP is not measured in the lab and there is no field data yet ("No Data"), so INP is unchecked. Top opportunities on both: render-blocking requests (est. 1.4 s), unused JS (~160 KiB) and CSS (~70 KiB), cache lifetimes. Stroller page also: image delivery (63 KiB), and Best Practices 92 (cause not read). No SEO fix filed: all scores are above 90 and the LCP miss is marginal; recheck after real photos replace the generated ones and once CrUX data exists (about 4 weeks).

## Findings

| # | Pri | Finding | Owner of fix |
|---|---|---|---|
| 2 | Accepted | Generated images are shown as real work (before/after pair, four problem photos) with no "Ilustracja" label and real-work alt text. Conflicts with "no fake content". **Owner override for launch (18 Nov):** leave as is; the owner replaces them with real photos as jobs come in, same file names (handoff #14). | Owner, as real photos arrive |
| 3 | Closed | `http://nowiutko.pl/x` → one `308 Permanent Redirect` to HTTPS, path kept. | none |
| 4 | P2 | `http://www.nowiutko.pl/` takes two hops. Accepted by the checklist. | none |
| 5 | P2 | Title dash differs: stroller en dash, homepage em dash. Align on the next copy pass. | SEO desk (copy) |
| 6 | Note | Meta descriptions use "Gotowe tego samego dnia": allowed by the brand ruling of 17 Nov (cleaning-design #8). | none |
| 7 | Note | LocalBusiness `image` is a one-item list; WebPage keeps `potentialAction: ReadAction`. Accepted deviations. | none |

## Still to do

- Owner: Search Console Domain property, submit sitemap, "Request indexing" for `/` and the stroller page.
- Owner: registered name and NIP for the footer.
- SEO desk: Rich Results Test on production; Facebook Sharing Debugger. Desktop PageSpeed not run (not required).
- Owner: replace the generated photos with real ones as jobs come in; the SEO desk re-checks alt text then.
