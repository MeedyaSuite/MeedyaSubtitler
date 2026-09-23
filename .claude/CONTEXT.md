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
- `claude/keen-pascal-shoj9x`: the **working branch**. All work goes here and will later go to `alpha` in one PR.
- `alpha`: **does not exist yet** (see the open question in HANDOFF.md).

## Things to remember
- Owner preferences: plain English; cost-aware choice of AI models; reviews done by a different AI; one PR only; keep the handoff always up to date.
- Cloud sessions do **not** have the Codex CLI or dev-team-plugins installed, so Codex reviews must be run from a machine that has them.
