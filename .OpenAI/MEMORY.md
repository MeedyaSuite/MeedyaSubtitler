# Codex / OpenAI memory — MeedyaSubtitler

## Log
- 2026-09-23: Project memory set up (standing rules, handoff, context). No code yet. A Codex review of these documentation files is owed.
- 2026-09-28: New branch `feature/bcp47-language-policy` adopted the shared MWBM-MEDIA-LANG 1.0.0 language policy (copies under `docs/standards/`, checker + first CI workflow, agent pointers in AGENTS.md/.claude/CLAUDE.md/.OpenAI/CONTEXT.md, comments on issues #5/#6/#8/#14). In order, the same day: a first review and its fixes, then a copy-update sweep to core `aaaa585` (umbrella issue #16), then more review-and-fix rounds. CI and review status: `.claude/HANDOFF.md`, "Review history".
- 2026-10-04: Codex's catch-up review of the whole branch (`53bbc0f..44cf095`) was done (done 2026-09-28), and acted on in `415aa4c` (one finding, shared with MeedyaPlayer). It covered the 2026-09-23 documentation files (`6a4690e`), so the review noted as owed on 2026-09-23 is no longer owed.

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
