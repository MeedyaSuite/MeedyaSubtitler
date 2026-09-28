# Codex / OpenAI memory — MeedyaSubtitler

## Log
- 2026-09-23: Project memory set up (standing rules, handoff, context). No code yet. A Codex review of these documentation files is owed.
- 2026-09-28: New branch `feature/bcp47-language-policy` adopted the shared MWBM-MEDIA-LANG 1.0.0 language policy (copies under `docs/standards/`, checker + first CI workflow, agent pointers in AGENTS.md/.claude/CLAUDE.md/.OpenAI/CONTEXT.md, comments on issues #5/#6/#8/#14). Committed and **pushed; CI passed on the last commit of each push (earlier commits in a push were checked only as part of it)**.
- 2026-09-28 (later): Core copy-update sweep: re-pinned from `f2e106a` to `aaaa585` (268 → 290 conformance cases, eight clarified rules, none changing an existing answer). See `.claude/HANDOFF.md`, "Copy-update sweep".
- Four rounds of fallback review have run since (each a fresh Opus agent standing in for Codex, per "Independent review" / "Second independent review" / "Third independent review" and this round) — see `.claude/HANDOFF.md`, "Review history," for the one table of what each round covered and found; not restated here so it can't drift out of sync with that table again.

## Device-wide rule (copy into `~/.codex/AGENTS.md` and `~/.claude/CLAUDE.md` on each machine)

```
## AI fallback (all projects)
If an AI service (Claude Code, Codex, or any other) or its agents becomes unavailable
or runs out of tokens/credits, hand the work to another suitable AI tool, provided this
can be done without losing context or progress. Switch back to the main AI tool as soon
and as often as possible, and run a full review of the interim work once it is back.
Keep the project's handoff document up to the minute so any tool can pick up at any time.
Not tied to specific tools: use whatever suitable AI tools are available.
Explain things in plain English, without technical jargon.
```
