# MeedyaSubtitler — Claude Code instructions

Before doing anything in a new session, read these in order:

1. @.claude/STANDING-RULES.md — standing rules and standing tasks (they always apply)
2. @.claude/HANDOFF.md — where we are right now, and what to do next
3. @.claude/CONTEXT.md — project background and memory

Keep `.claude/HANDOFF.md` updated **as you go** (rule R2). Explain everything in plain English (rule R1).

## Languages, tracks, subtitles and lyrics — mandatory

Any work touching BCP 47 language tags, languages, translations, audio or
subtitle tracks, lyrics, track order or naming, language preferences, or
accessibility roles (SDH, audio description, forced, commentary) MUST read
and follow `docs/standards/media-language-bcp47-policy.md` (policy
`MWBM-MEDIA-LANG`). It is normative and is not repeated here. Its
conformance cases (`Tests/Fixtures/bcp47-language-policy-v1.json`) must
pass once code exists; the Swift implementation is in MeedyaConverter for
now (on a work-in-progress branch there, not yet on its `alpha`) and moves
to a shared package once MeedyaPlayer or MeedyaSubtitler has code (policy
section 9). The copies are checked against the master in
MWBMPartners/MeedyaSuite-core by `scripts/media-lang/check_copies.py`;
never edit the copies — change the master.
