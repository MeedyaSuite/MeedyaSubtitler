# Standing Rules & Standing Tasks — MeedyaSubtitler

> These apply to **every** session and **every** AI tool (Claude Code, Codex, or any other) working on this repo.
> Read this file, then `.claude/HANDOFF.md`, before doing anything else.
> Last revised: 2026-09-23 (by the project owner's instruction).

---

## Standing rules

### R1. Plain English
When reporting back or explaining anything, **do not use technical jargon**. Explain in plain, easy-to-understand English — even technically skilled people can find jargon confusing. If a technical term can't be avoided, explain it in a few words.

### R2. Keep the handoff up to date — as you go
Update `.claude/HANDOFF.md` **during** the work, not just at the end, so we can pick up exactly where we left off at any moment (session restart, crash, running out of credits, switching AI tool). Treat it as the single source of truth for "where are we?".

### R3. How to think, plan and build (GIRFT — Get It Right First Time)
- Think hard ("ultrathink") about the work needed; use workflows to help plan and do the work.
- **Deep analysis and deep planning:** use Opus agents, run **one after another (sequentially), not in parallel**. (Reason: the newest Opus — Opus 5.5 at the time of writing — is cheaper and at least as good as the newest Fable.)
- **Building / implementation:** use Sonnet or Haiku, whichever suits the job. If the implementation is complex, use Opus.
- Aim: use tokens/credits efficiently **and** produce top-quality, correct code.

### R4. Use plugins, and cross-check with a different AI
- Feel free to use **dev-team-plugins** for any of this work, and for suggesting fixes, tweaks, enhancements and new features.
- Use a **different AI system to check the work** than the one that did it: e.g. plan and build with Claude Code → review with Codex (and vice versa).

### R5. Code review loop
All code goes through a **Codex review**. Any issues found are fixed automatically, then reviewed again by Codex — **repeat until the review finds no issues**.

### R6. No PR stacking
Do **not** create multiple pull requests (PRs). All work is committed to the **one working branch** (currently `claude/keen-pascal-shoj9x`), which will later be merged into `alpha` through a **single PR created later**. This avoids PRs clashing with each other when merged.

### R7. AI fallback (also applies device-wide)
If an AI service (e.g. Claude Code, Codex — or any other) or its agents become unavailable or run out of tokens/credits, **hand the work to another suitable AI tool**, as long as that can be done without losing context or progress. Then:
- **Switch back to the main AI tool as often as possible.**
- Once the main tool is back, run a **full review** of the work done in the meantime (the cross-AI reviews in R4/R5 catch differences in approach, but a full review is still required).
- This is why keeping the handoff up to the minute (R2) is crucial.
- Not tied to any specific tools — use whatever suitable AI tools are available.

### R8. Autonomy
Work through **all** queued tasks on your own. Only stop when you need an **explicit decision or approval** from the owner — and then say clearly, in simple words, what you need and why. **Raise all questions up front** (not one at a time as they come up), then carry on with every queued task.

### R9. Progress updates
Give frequent progress updates showing the task queue as a **table**, with the status of each task.

### R10. Work efficiently
You may reorder and bundle the standing tasks below to work efficiently.

---

## Standing tasks (after each piece of work)

### T1. After each task is completed
1. **Commit and push** to the working branch (the one that will later be merged into `alpha`).
2. **Update the related GitHub Issue(s)** — individually for each task.
3. **Update Claude memory and context** in `.claude/` (this folder).
4. **Update OpenAI/Codex memory and context** in `.OpenAI/`.
5. **Update the handoff** (`.claude/HANDOFF.md`) so we can easily pick up where we left off.

### T2. Thorough documentation update (when asked, and at milestones)
- Update **all** `.md` documentation files.
- Update **in-app help**, guides, etc. (once the app exists).
- Update Claude memory, context and everything else in `.claude/`.
- **If the project offers an API:** update its OpenAPI/Swagger documentation.
- **If the project has web-based parts and no Swagger UI:** add Swagger UI (a browsable page for the API documentation) that works on normal servers **and on shared hosting** (no Docker etc.).

---

## Where things live
| What | Where |
|---|---|
| Standing rules & tasks (this file) | `.claude/STANDING-RULES.md` |
| Handoff — "where are we right now" | `.claude/HANDOFF.md` |
| Claude memory & project context | `.claude/CONTEXT.md` (auto-loaded via `.claude/CLAUDE.md`) |
| Codex / OpenAI memory & context | `.OpenAI/CONTEXT.md` (auto-loaded via root `AGENTS.md`) |
