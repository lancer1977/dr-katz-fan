# Transcript sourcing notes

All 78 files here were scraped from Forever Dreaming
(`transcripts.foreverdreaming.org/viewforum.php?f=2639`) on 2026-08-19, via
an authenticated browser session (the forum sits behind an Anubis
proof-of-work bot-check that a plain HTTP fetch can't pass — see
`../transcript-sources.md` for the full investigation).

- One `.txt` file per episode, named `S{season}E{episode}-{slug}.txt`,
  containing the raw unattributed dialogue text as posted on Forever
  Dreaming (no speaker labels — consistent with a closed-caption-derived
  source, likely the 2007 Complete Series DVD).
- `manifest.json` maps every file to its season/episode/title, Forever
  Dreaming topic ID, character length, and source URL.
- **Coverage gap**: episodes `01x01`–`01x03` are not present on Forever
  Dreaming's board at all (their listing starts at `01x04`).
- **Numbering quirk**: Forever Dreaming has two topics both labeled
  `02x17` — "Henna" and "Theory of Intelligence". This is preserved as-is
  from the source (both are included, under different filenames) rather
  than guessed at; one of them is likely mislabeled upstream (plausibly
  `02x18`), but nothing in the source itself resolves which.
- Cross-reference against `../episodes.json` (episode/comedian metadata,
  81 episodes total) by season+episode number where both exist.
