# HANDOFF — pick up here

> **Last updated:** 2026-09-23 ~20:10 UTC
> **Last session:** https://claude.ai/code/session_016oWLSLynER52w6bKL8FsAM (Claude Code, cloud)
> **Working branch:** `claude/keen-pascal-shoj9x` (will later go to `alpha` in a single PR)

## Starting a fresh session? Do this
1. Check out branch `claude/keen-pascal-shoj9x` and pull the latest.
2. Read `.claude/STANDING-RULES.md` (the rules always apply), then this file, then `.claude/CONTEXT.md`.
3. Deal with the **open questions** below (ask the owner if they are still unanswered).
4. Continue with the **next steps** queue.

## Where we are (state of play)
- The project is at **planning stage**. There is no app code yet: just README, LICENSE, .gitignore and the planning issues #1 to #15.
- **No pull requests** exist. **No `alpha` branch** exists yet.
- This session set up the project's "working memory":
  - `.claude/STANDING-RULES.md`: standing rules R1 to R10 and standing tasks T1 and T2, revised to the owner's latest list
  - `.claude/HANDOFF.md`: this file
  - `.claude/CONTEXT.md` and `.claude/CLAUDE.md`: project context, loaded automatically by Claude Code
  - `.OpenAI/CONTEXT.md` and `.OpenAI/MEMORY.md`, plus a root `AGENTS.md`: the same information for Codex and other AI tools
- The AI fallback rule (R7) was also written to the **device-wide** files (`~/.claude/CLAUDE.md`, `~/.codex/AGENTS.md`). ⚠️ In a cloud session those files are **wiped when the session ends**, so the lasting copy lives in this repo. The owner should copy the rule onto their own machine(s) (text is in `.OpenAI/MEMORY.md`, section "Device-wide rule").
- Documentation pass (T2): the README is accurate for the planning stage. There is **no API** (so no Swagger), **no web part** (so no Swagger UI) and **no app** (so no in-app help) yet. Nothing more to do until code exists.
- Codex review (R5): this session only changed documentation, and the Codex CLI isn't installed in the cloud session. **A Codex review of these files is still owed.** Run it from a machine that has Codex (see the next steps).

## Task queue
| # | Task | Status |
|---|---|---|
| 1 | Revise standing rules and tasks | ✅ Done |
| 2 | Add the plain-English rule (R1) | ✅ Done |
| 3 | Add the AI-fallback rule, for this repo and device-wide (R7) | ✅ Done (device copy needs setting up on the owner's machine) |
| 4 | Create and update the handoff | ✅ Done |
| 5 | Claude and Codex memory/context files | ✅ Done |
| 6 | Thorough documentation update | ✅ Done (nothing else applies yet: no code, API or web part) |
| 7 | Commit and push to the working branch | ✅ Done |
| 8 | Codex review of this session's changes | ⏳ Owed: Codex isn't available in the cloud session |
| 9 | The Codex review the owner mentioned for **00:08** | ❓ Not visible from this repo (see open question 2) |
| 10 | Start phase 0 work (#5 foundation, then #14) | ⏸ Waiting for the owner's go-ahead |

## Open questions for the owner
1. **`alpha` branch:** it doesn't exist yet. Should we create it from `main` so the single PR has something to target? (Suggested: yes, when we are ready to open the PR.)
2. **"00:08 Codex review":** nothing in this repo is waiting on it. Does it relate to MeedyaSubtitler, or to a different project? If it's this repo, review the `claude/keen-pascal-shoj9x` branch.
3. **Where Codex reviews run:** cloud sessions don't have Codex or dev-team-plugins installed. Should reviews be run on your own machine, or should we try to install them in the cloud environment's setup script?

## Next steps (in order)
1. Run the owed Codex review on this branch (task 8), and fix anything it finds.
2. Get answers to the open questions.
3. Start phase 0: issue #5 (project foundation: Swift 6.3/SwiftUI project skeleton) → #14 (handoff with MeedyaConverter). Do deep planning first with sequential Opus agents (R3), then build with Sonnet/Haiku, then run the Codex review loop (R5).
