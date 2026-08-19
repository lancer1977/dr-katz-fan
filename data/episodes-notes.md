# episodes.json — sourcing notes

Built for GitHub issue #1, item 1 (episode/comedian data set).

## Coverage

All 81 episodes across all 6 seasons (1995–2002) are present. No `null`
fields were needed — season, episode number, title, air date, and at least
one comedian were recoverable for every episode.

## Sources used

- **The Dr.Katz Fandom wiki** (the primary source requested in the task)
  returned HTTP 402/403 on every fetch attempt — direct page, MediaWiki API,
  and a sibling Fandom wiki (`ccarchive.fandom.com`) were all blocked for
  this environment's fetcher. Could not be used directly.
- **Wikipedia** — `https://en.wikipedia.org/wiki/List_of_Dr._Katz,_Professional_Therapist_episodes`
  supplied the canonical season/episode-number/title/air-date structure
  (verified twice via independent fetches, byte-for-byte consistent both
  times, including production codes). Wikipedia's episode table does not
  include guest comedian names.
- **IMDb** (`imdb.com/title/tt0111942/episodes/`) also 403'd on direct
  fetch; used only indirectly via web search snippets for spot-checks.
- **Guest/comedian names** came from two independent fan-maintained
  episode guides: "The Many Faces of Dr. Katz" (jeffsass.com/katz) and a
  second complete index at chafecity.neocities.org/drkatz. The two agree on
  nearly every episode; where they diverged on a comedian's name spelling
  (e.g. "Rich Snyder" vs "Ritch Shydner", "Robert Shimmer" vs "Robert
  Schimmel", "Emo Phillips" vs "Emo Philips", "Mark Maron" vs "Marc Maron"),
  the correctly-spelled real comedian name was used and confirmed via a
  targeted web search.
- The final three Season 6 episodes ("Bakery Ben", "Uncle Nothing",
  "Lerapy" — the "Final Three," first aired Feb 13, 2002) are missing from
  both fan guides (which predate that broadcast). Their guest lists were
  confirmed independently via web search against IMDb/synopsis sources.

## Known quirks preserved as-is (not errors)

- **Nine Season 6 episodes share the air date 1999-12-24.** Comedy Central
  burned off episodes 606–614 (prod codes) in a same-day "Dr. Katz's Final
  Case Files" marathon on Christmas Eve 1999. Confirmed via web search, not
  a scraping artifact.
- **`episodeNumber` is the number within its season**, not the overall
  series episode number (1–81 overall; season 5 and 6 each run 1–18, etc.),
  matching the shape of the JSON contract's example (`season` + separate
  `episodeNumber`).
- **Todd Barry** appears as a "guest" on many season 2, 4, 5, and 6
  episodes — he had a recurring role (the office temp "Todd") in addition
  to guest-patient appearances, and both fan sources credit him per-episode
  where he appears, so he's included in `comedians` for those.
- Episode air-date **order sometimes differs from production-code order**
  (e.g. Season 3's "Studio Guy," prod code 309, aired Jan 19 1997 — before
  "Mourning Person," prod code 308, which aired Jan 26 1997). `episodeNumber`
  here follows air-date order, per Wikipedia's episode list table, not
  production code.
