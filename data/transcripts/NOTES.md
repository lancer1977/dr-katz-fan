# Transcript sourcing notes

**Coverage: 81/81 episodes.**

78 files were scraped from Forever Dreaming
(`transcripts.foreverdreaming.org/viewforum.php?f=2639`) on 2026-08-19, via
an authenticated browser session (the forum sits behind an Anubis
proof-of-work bot-check that a plain HTTP fetch can't pass — see
`../transcript-sources.md` for the full investigation).

- One `.txt` file per episode, named `S{season}E{episode}-{slug}.txt`,
  containing the raw unattributed dialogue text as posted on Forever
  Dreaming (no speaker labels — consistent with a closed-caption-derived
  source, likely the 2007 Complete Series DVD).
- `manifest.json` maps every file to its season/episode/title, source, and
  (for the Forever Dreaming files) the topic ID and source URL.
- **Numbering quirk**: Forever Dreaming has two topics both labeled
  `02x17` — "Henna" and "Theory of Intelligence". This is preserved as-is
  from the source (both are included, under different filenames) rather
  than guessed at; one of them is likely mislabeled upstream (plausibly
  `02x18`), but nothing in the source itself resolves which.
- Cross-reference against `../episodes.json` (episode/comedian metadata,
  81 episodes total) by season+episode number where both exist.

## The remaining 3: S01E01–S01E03

Not present on Forever Dreaming at all (their board starts at `01x04`). The
user owns these episodes as local video files
(`/mnt/syn2/Video/TV Shows/Dr  Katz, Professional Therapist/Season 01/` —
note the double space in "Dr  Katz" in the real path) and had them
transcribed locally rather than relying on any third-party source:

- Audio extracted with `ffmpeg` (mono, 16kHz PCM) from the `.mp4` files.
- Transcribed with `faster-whisper` (`base` model, `int8`, CPU) — no GPU
  was available in the environment that did this. An initial attempt with
  the `small` model loaded fine but the actual transcription process
  vanished silently (empty log, process gone) under heavy host memory
  pressure (~361Mi free / 45Gi of 63Gi swap in use at the time); dropping to
  `base` and re-running as a properly tracked background job completed
  cleanly in a few minutes.
- These three are lower-confidence than the Forever Dreaming set: ASR
  output on overlapping, mumbled, improvised stand-up-style dialogue (this
  show's whole aesthetic) is inherently noisier than a CC-derived
  transcript, and the `base` model is the least accurate tier practical
  here. Worth a human pass or a re-run with a larger model if this project
  gets serious about accuracy.
