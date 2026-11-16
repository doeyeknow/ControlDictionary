# ControlDictionary

The word dictionary for Control Launcher's message shorthand. The
launcher fetches this file in the background and builds its local
dictionary from it, so common words travel as short codes instead
of spelled-out text on the mesh, Bluetooth, and relay roads.

## Files

- `dictionary.txt` — one word per line, UTF-8, LF endings. The
  order IS the code table: a word's code is derived from its line
  number. The first 1,200 lines are the frozen v1 order shipped
  in Control Launcher 1.28 (including the "I" forms in their
  canonical capitals — `I`, `I'm`, `I'll`, `I'd`, `I've` — which
  the codec relies on); everything after is the tail, lowercase.
- `version.json` — `{"version", "count", "sha256", "format"}`.
  The app fetches this first, then `dictionary.txt`, and refuses
  a download whose SHA-256 does not match.

## APPEND-ONLY — read this before editing

Entries are NEVER reordered, removed, or edited in place. Codes
are positional: moving a line changes every code after it and
breaks every coded message already sent. To grow the dictionary,
append new words at the end, bump `version` in `version.json`,
and update `count` and `sha256` to match the new file.

## No writes from phones

The launcher only ever READS this repo (public raw URLs, no
login). Nothing in the app holds a credential that can write
here — a write key baked into an app can be pulled out by
anyone holding the app. Merges happen off-phone only, by the
repo owner, through the normal GitHub flow.

## Word list source

Tail words come from `words_alpha.txt` in
[dwyl/english-words](https://github.com/dwyl/english-words)
(MIT licensed), deduplicated, with any word already present in
the frozen head dropped. The head is the hand-ordered
frequency list from Control Launcher 1.28.
