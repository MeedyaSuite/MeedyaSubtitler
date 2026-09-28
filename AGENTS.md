# Instructions for AI agents (Codex and others)

Read these before doing anything:
1. `.claude/STANDING-RULES.md`: standing rules and tasks (they apply to every AI tool)
2. `.claude/HANDOFF.md`: current state and next steps (keep it updated as you go)
3. `.OpenAI/CONTEXT.md` and `.claude/CONTEXT.md`: project context

## Languages, tracks, subtitles and lyrics — mandatory

Any work touching BCP 47 language tags, languages, translations, audio or
subtitle tracks, lyrics, track order or naming, language preferences, or
accessibility roles (SDH, audio description, forced, commentary) MUST read
and follow `docs/standards/media-language-bcp47-policy.md` (policy
`MWBM-MEDIA-LANG`). It is normative and is not repeated here. Its
conformance cases (`Tests/Fixtures/bcp47-language-policy-v1.json`) must
pass once code exists; the Swift implementation to reuse is in
MeedyaConverter until a shared package exists. The copies are checked
against the master in MWBMPartners/MeedyaSuite-core by
`scripts/media-lang/check_copies.py`; never edit the copies — change the
master.
