# Codex / OpenAI context — MeedyaSubtitler

This folder is the Codex (and any non-Claude AI) copy of the project's memory. The **authoritative** files live in `.claude/`:

- `.claude/STANDING-RULES.md`: standing rules and tasks. **They apply to you too.**
- `.claude/HANDOFF.md`: where we are and what to do next. Read it first, and keep it updated as you go.
- `.claude/CONTEXT.md`: project background, phases and branches.

## Languages, tracks, subtitles and lyrics — mandatory

Any work touching BCP 47 language tags, languages, translations, audio or
subtitle tracks, lyrics, track order or naming, language preferences, or
accessibility roles (SDH, audio description, forced, commentary) MUST read
and follow [`docs/standards/media-language-bcp47-policy.md`](../docs/standards/media-language-bcp47-policy.md)
(policy `MWBM-MEDIA-LANG`). It is normative and is not repeated here. Its
conformance cases (`Tests/Fixtures/bcp47-language-policy-v1.json`) must
pass once code exists; the Swift implementation is in MeedyaConverter for
now (on a work-in-progress branch there, not yet on its `alpha`) and moves
to a shared package once MeedyaPlayer or MeedyaSubtitler has code (policy
section 9). The copies are checked against the master in
MWBMPartners/MeedyaSuite-core by `scripts/media-lang/check_copies.py`;
never edit the copies — change the master.

## Summary
- MeedyaSubtitler: a native Apple subtitle editor (Swift/SwiftUI), a companion to MeedyaConverter. Currently at the planning stage (issues #1 to #15, phases 0 to 6). No code yet.
- Working branch: `feature/bcp47-language-policy` (cut from, and containing every commit of, `claude/keen-pascal-shoj9x`; pushed, CI green on every commit, independently reviewed twice on 2026-09-28 — see `.claude/HANDOFF.md`, neither round's fixes reviewed yet). One PR into `alpha` later; never open extra PRs.
- Your usual role here: **reviewer** of work built by Claude Code. Review, fix what you find, and re-review until clean (rule R5). If Claude is unavailable, you may take over building (rule R7). Update `.claude/HANDOFF.md` as you go so Claude can switch back in.
- Explain everything in plain English (rule R1).
