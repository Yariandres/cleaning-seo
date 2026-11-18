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

## Findings

| # | Pri | Finding | Owner of fix |
|---|---|---|---|
| 1 | **P0** | `nowiutko.com` and `www.nowiutko.com` do not resolve (no DNS answer), so checklist item 5 (301 to `nowiutko.pl`) is not met. | Owner (DNS), then developer checks the redirect |
| 2 | P1 | Generated images are presented as real work: the before/after pair ("Wózki przed i po praniu") and the four problem photos have no "Ilustracja" label, and the alt text describes them as real. Conflicts with "no fake content". Owner decision: label them, or hide before/after until a real pair exists. | Owner decides, then page-spec copy fix to the developer |
| 3 | P1 | `http://nowiutko.pl/x` redirects once; the status code (301/308 vs 302) was not confirmed. Check with `curl -sI`. | SEO desk (re-check), developer if 302 |
| 4 | P2 | `http://www.nowiutko.pl/` takes two hops. Accepted by the checklist. | none |
| 5 | P2 | Title dash differs: stroller en dash, homepage em dash. Align on the next copy pass. | SEO desk (copy) |
| 6 | Note | Meta descriptions use "Gotowe tego samego dnia": allowed by the brand ruling of 17 Nov (cleaning-design #8). | none |
| 7 | Note | LocalBusiness `image` is a one-item list; WebPage keeps `potentialAction: ReadAction`. Accepted deviations. | none |

## Still to do

- Owner: Search Console Domain property, submit sitemap, "Request indexing" for `/` and the stroller page.
- Owner: registered name and NIP for the footer.
- SEO desk: PageSpeed mobile and Rich Results Test on production; Facebook Sharing Debugger.
- After finding 1 is fixed: re-check redirects on all four hosts.
