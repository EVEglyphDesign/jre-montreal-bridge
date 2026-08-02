# Retrieval log

Append-only. Every route attempted, including the ones that failed. Recorded so an outsider
can re-run the ingestion and get the same bytes, and so the failures are not silently
re-attempted at cost.

**Ingested** 2026-08-02T11:05:05Z

## Routes attempted

| # | Route | Result |
|---|---|---|
| 1 | [Spotify episode page](https://open.spotify.com/episode/1JGZOWkjNkNeDwS24ah9md) direct fetch | **Failed** — client error, no server-rendered transcript |
| 2 | `yt-dlp --write-auto-sub` against YouTube | **Failed** — bot challenge, no captions returned |
| 3 | [VideoHighlight](https://videohighlight.com/v/RCu9Hlpmoi0?mediaType=youtube&language=en&summaryType=default&aiFormatted=false) | **Partial** — chapter list and indexed summary only, no verbatim captions. Used for the first pass, superseded by route 4 |
| 4 | [youtubetotranscript.com](https://youtubetotranscript.com/transcript?v=RCu9Hlpmoi0) via browser, Cloudflare passed, **Timestamp toggled ON** | **Succeeded** — 983 timestamped caption lines, 00:00:00 to 01:39:14 |
| 5 | YouTube video page, title and channel confirmation | **Succeeded** for identity; playback blocked by a sign-in-to-confirm-you-are-not-a-bot wall, so runtime is taken from the last caption rather than the player |

## Identity confirmation

Video ID `RCu9Hlpmoi0` was confirmed by opening the watch page and matching the title and
channel, not inferred from search. Title, channel, subscriber count, publish date and the
"52nd episode" statement were all read from the page.

## Known limits

- Captions are **auto-generated**, not a human transcript. Proper nouns are unreliable;
  timings are accurate to roughly the caption cadence of five to six seconds.
- The source does **not** label speakers. Host and guest alternate inside the running text.
- Caption artefacts are preserved verbatim. See the note at the head of the transcript.
- The chapter list is the host's, from the description. It is navigation, not caption data.

## Content hashes

| File | SHA-256 |
|---|---|
| `transcript_full.md` | `09d15ecd2f747e5019b99c2cf0d5464f395a0c8db70dc9ff8cefa73880334415` |
| `segment_1200_2200_scripting.md` | `34b5c91e93f2d336788b492f4b5d12d7854748d292ea2e22b8497791e478e255` |

---

© 2026 Dany Theriault. EVE "digital stem cell" glyph and glyph-based design principles — all rights reserved. Stewardship of rights of use and assignment for large public and institutional usage rests with the Pacific Utilities Design Council. Published as a time-stamped record of authorship and intent.
