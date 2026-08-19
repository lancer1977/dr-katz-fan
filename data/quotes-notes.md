# Quote-collection notes

## TV Tropes — unfetchable, zero quotes pulled

`https://tvtropes.org/pmwiki/pmwiki.php/Quotes/DrKatzProfessionalTherapist`

The page is real and does exist (its `<head>` meta tags — title, description —
confirm the URL resolves), but the actual article body is replaced site-wide
by an anti-adblock interstitial ("Looks like you're using an ad blocker...")
for every fetch method tried:

- `WebFetch` tool: returned only the interstitial text.
- Chrome browser (rendered DOM, `get_page_text`, `read_page`, and raw
  `outerHTML` inspection via `javascript_tool`): same interstitial. The real
  quote content is not present anywhere in the DOM (confirmed by searching
  for "Katz" — the only hits are in `<head>` meta tags, not the article body),
  so this isn't just a CSS overlay hiding content underneath; the content
  genuinely isn't delivered.
- Wayback Machine: checked both a snapshot view (`web.archive.org/web/2023/...`)
  and the CDX API directly (exact-match and prefix-match queries against
  `tvtropes.org/pmwiki/pmwiki.php/Quotes/DrKatzProfessionalTherapist`) — zero
  snapshots exist. TV Tropes is known to block/discourage archive.org
  crawling of its wiki pages, which is consistent with this result.

Net: **0 quotes** came from TV Tropes for this collection pass. If this page
matters enough to revisit, the practical options are a logged-in TV Tropes
account with ads allowed/subscription active, or a proxy/service that
already has a cached copy.

## Quote Catalog — thin but real (3 quotes, 3 total confirmed by the site itself)

`https://www.quotecatalog.com/source/dr-katz-professional-therapist` shows
"(3 total)" — the source page is not paginated or truncated beyond that; all
3 are in `quotes.json`. Two of the three come from the same episode
("Pot-Bellied Pigs"); the third is unattributed to an episode on Quote
Catalog itself but cross-references exactly against IMDb's per-episode quote
page for the same episode (tt0565084), so `episode` was set to
"Pot-Bellied Pigs" on reasonable confidence rather than left `null`.

One card on the source page was itself truncated with "…" (Quote Catalog's
own display truncation, not a fetch artifact); the full text was recovered
from that quote's dedicated page
(`https://www.quotecatalog.com/quote/loren-bouchard-bdr-katzb`), which also
supplied the episode name.

## IMDb — good yield (15 quotes across the main title page + 3 episode pages)

`WebFetch` 403'd on all `imdb.com` URLs; all IMDb content was pulled via the
Chrome browser tools instead (`javascript_tool` reading `<ul>`/`<li>` DOM
nodes directly — IMDb's page renders quotes as list items with an `<a>` tag
per speaker).

- Main title quotes page (`/title/tt0111942/quotes/`): 7 quote
  blocks/exchanges, no episode attribution given by IMDb at that level.
- Followed the episode list (`/title/tt0111942/episodes/`) to individual
  episodes' own `/quotes/` pages, per the task's suggestion. Checked 6
  episode IDs; 3 had quote content (Ben Treats, Pot-Bellied Pigs,
  Pretzelkins — 3 more content blocks), 3 had none (Bees and SIDS, Bully,
  and one more not deeply logged). Did not exhaustively check all ~65
  episodes in the run — this was a sampling pass, not a full episode sweep.
  Revisiting to check the remaining episode quote pages would likely surface
  more material if this collection ever needs to grow.

## General fetch-method note

`WebFetch` failed outright (403) on both `tvtropes.org` and `imdb.com` for
every URL tried. The Chrome browser tools (`claude-in-chrome`) worked for
IMDb but not TV Tropes (see above) — worth defaulting to the browser first
for future scrapes of either site.
