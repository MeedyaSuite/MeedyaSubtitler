# docs/

This folder holds standards MeedyaSubtitler depends on but does not own —
documents whose master copy lives in another repository, kept here so they
can be read from a plain checkout with no network and no submodule.

## What's here

- **`standards/`** — copies of the shared **MWBM-MEDIA-LANG** language
  policy (version 1.0.0), whose master copy is
  [`MWBMPartners/MeedyaSuite-core`](https://github.com/MWBMPartners/MeedyaSuite-core),
  `docs/standards/media-language-bcp47-policy.md`. It says how every Meedya
  app identifies, stores, orders, names, matches and selects languages.
  Per the policy's own section 2, MeedyaSubtitler's profile is
  **canonical** and **text** — it writes subtitle languages, roles (SDH,
  forced, commentary, and so on) and sidecar file names — plus a small
  **presentation** part for its own language pickers. The full Part B menu
  ordering and automatic track selection are a player's job; matching
  (MATCH-010 to MATCH-040) is needed by the text profile too (section
  8.1).
- **`../Tests/Fixtures/`** — byte-identical copies of the policy's
  conformance test cases and their schema (same lock as the files above).

## Why these are copies, not a link

The policy document itself explains this (section 8.3), but in short: a
link only works if you're online and the other repository is reachable. A
copy works from a plain `git clone`, on a plane, for a person or an AI tool
reading the code with nothing else open. Copies drift unless something
checks them, so alongside the copies is `docs/standards/MWBM-MEDIA-LANG.lock`
(recording exactly which commit of MeedyaSuite-core they came from, and each
file's checksum) and `scripts/media-lang/check_copies.py` (the script that
checks the lock matches both the files here and the real master files on
GitHub). That script runs in CI on every pull request and push — see
`.github/workflows/policy-copies.yml`.

**Never edit a copy by hand.** If the policy needs to change, change it in
`MWBMPartners/MeedyaSuite-core`, then run
`python3 scripts/media-lang/check_copies.py --update <new-commit>` here to
pull the change across.
