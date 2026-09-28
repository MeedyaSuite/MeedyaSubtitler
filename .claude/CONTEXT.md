# Project context & memory — MeedyaSubtitler

## What this project is
A native subtitle editor for Apple devices (macOS, iPadOS, iOS, visionOS); Windows and Linux will follow later. It is inspired by Subtitle Edit on Windows. It works alongside **MeedyaConverter**: converting, adding subtitles to video files and syncing them stay in MeedyaConverter, and editing happens here. The two apps pass documents to each other.

- Owner: MWBM Partners Ltd. All rights reserved; the licence is still to be decided.
- GitHub repo: `meedyasuite/meedyasubtitler`
- Planned technology (from issue #5): Swift 6.3 and SwiftUI, Apple-first, sold through two channels (dual distribution). It will share Rust code from MeedyaSuite-core.

## Current stage
**Pre-alpha / planning.** There is no app code yet. The plan is set out in 15 GitHub issues, grouped into phases:

| Phase | Issues |
|---|---|
| 0: Foundation | #5 Project foundation · #14 Handoff between MeedyaConverter and this app |
| 1: Formats | #6 Reading and writing all major subtitle formats |
| 2: Editing | #2 List/table editing view · #4 Raw text editor with colour highlighting |
| 3: Core tools | #1 Find & replace (with regex) · #3 Timing operations · #7 Format conversion |
| 4: Video/audio | #8 Audio waveform sync · #11 Click-to-set timing · #12 Video preview with subtitle overlay |
| 5: Quality | #9 Auto-fix common errors · #10 OCR (reading text from image subtitles) · #13 Quality checks and statistics |
| 6: Styling | #15 Styling for ASS/SSA subtitles |

## Branches
- `main`: contains only the first commit (README, .gitignore, LICENSE).
- `claude/keen-pascal-shoj9x`: the earlier working branch (standing rules, handoff, memory files). Will later go to `alpha` in one PR.
- `feature/bcp47-language-policy`: cut from the branch above, 2026-09-28. Adopts the shared MWBM-MEDIA-LANG 1.0.0 language policy (see HANDOFF.md). Not pushed.
- `alpha`: **does not exist yet** (see the open question in HANDOFF.md).

## Shared language policy (MWBM-MEDIA-LANG)

Adopted 2026-09-28. `docs/standards/media-language-bcp47-policy.md` is a
byte-identical copy of the master document in
`MWBMPartners/MeedyaSuite-core`, checked against it by
`scripts/media-lang/check_copies.py` (run in CI via
`.github/workflows/policy-copies.yml`). **Never edit the copy** — change
the master and run `--update`. MeedyaSubtitler's profile under this policy
is "canonical and text" (it writes subtitle languages, roles and sidecar
names) plus a small presentation part (its language pickers) — see the
policy document's section 2 for what that means precisely. Any work
touching languages, tracks, subtitles, lyrics or accessibility roles must
read and follow it; see `AGENTS.md` / `.claude/CLAUDE.md` for the pointer.

## Things to remember
- Owner preferences: plain English; cost-aware choice of AI models; reviews done by a different AI; one PR only; keep the handoff always up to date.
- Cloud sessions do **not** have the Codex CLI or dev-team-plugins installed, so Codex reviews must be run from a machine that has them.
