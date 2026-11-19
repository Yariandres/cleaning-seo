# Homepage snippet rewrite and privacy-page date (19 Nov 2026)

Source: owner's `site:nowiutko.pl` check, 18 Nov. Pages fetched with `curl` on 19 Nov. I have **not** seen the live results page, only the owner's report.

## 1. Privacy page "in 2 days" — filed

Cause: visible text `Obowiązuje od 20 listopada 2026 r.` under the H1. No `<time>`, no JSON-LD date, no `Last-Modified`. Google took the only date on the page. Filed as **cleaning-sell-system #15** (use the real publish date in `<time datetime>`, never a future one).

## 2. Homepage snippet ends "736 369 704 2–3" — filed as #16

**What the page has:** the meta description is as in the spec (142 characters, fits). Google is allowed to ignore it and often does, so a rewrite is not an error by itself. It picks text from the page that fits the query.

**Why this text:** the first visible words in the HTML are the call-to-action blocks, not sentences:
1. header phone link: `736 369 704`
2. hero buttons: `Wyślij zdjęcia na WhatsApp`, `Zadzwoń: 736 369 704`
3. promise line: `2–3 zdjęcia wystarczą. Cenę podamy dziś.`

Buttons and the line carry no punctuation between them, so Google joins them into `… 736 369 704 2–3 …`. This is the likely cause (from the HTML order; I can't see Google's reasoning). The page has no `data-nosnippet` anywhere. The good descriptive sentence ("Przyjeżdżamy z własnym sprzętem i pierzemy u Ciebie, na miejscu: wózki, foteliki, kanapy, …") comes after the buttons.

**Proposed fix (developer, small, P2):**
- Put `data-nosnippet` on the elements that are only calls to action: header phone link, hero buttons row, the promise line and hours line, the sticky or floating CTA if there is one, and the WhatsApp rows in the "Wycena na WhatsApp" section. Google's `data-nosnippet` works on `span`, `div` and `section`, so wrap the link in a `span` if needed. Visible text and layout do not change.
- Keep the hero paragraph ("Przyjeżdżamy z własnym sprzętem …") and the H1 snippet-eligible. Optional: in the source order, put that paragraph before the buttons if the design allows it (visual order can stay).
- Do **not** rewrite the meta description. It already says what we do, where, and the WhatsApp offer.
- No change to the robots meta: `max-snippet:-1` stays.

**Expected result:** Google will have no phone number or button text to pick, so it falls back to the hero paragraph or the description. It is a hint, not a guarantee, and it takes a recrawl (days to weeks). Recheck with `site:nowiutko.pl` and a search for `nowiutko` on about 3 Dec.

**Filed 19 Nov as cleaning-sell-system #16.**

## 3. Favicon recheck — about 3 Dec 2026

State on 19 Nov (production): `/favicon.svg` (declared first, `sizes="any"`), `/favicon-32.png`, `/apple-touch-icon.png` (180×180), and `/favicon.ico` (200, contains 16×16 and 32×32).

Google asks for a favicon whose size is a multiple of 48 px (SVG is allowed). Our PNG and ICO are 32 px and smaller; the SVG should count. On 3 Dec check the favicon next to the result for `nowiutko`. If it is still the grey globe, propose a `favicon-48.png` (or 96 px) plus an `<link rel="icon" href="/favicon.ico" sizes="48x48">` fix to the developer. Not before: Google's favicon refresh is slow.
