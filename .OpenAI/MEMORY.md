# Codex / OpenAI memory — MeedyaSubtitler

## Log
- 2026-09-23: Project memory set up (standing rules, handoff, context). No code yet. A Codex review of these documentation files is owed.
- 2026-09-28: New branch `feature/bcp47-language-policy` adopted the shared MWBM-MEDIA-LANG 1.0.0 language policy (copies under `docs/standards/`, checker + first CI workflow, agent pointers in AGENTS.md/.claude/CLAUDE.md/.OpenAI/CONTEXT.md, comments on issues #5/#6/#8/#14). Committed and **pushed; CI passed on the last commit of each push (earlier commits in a push were checked only as part of it)**. A fresh Opus agent then reviewed it in Codex's place (Codex was out of allowance) and found several inaccuracies — see `.claude/HANDOFF.md`, "Independent review". **Those fixes are themselves not yet reviewed** — that review is still owed.
- 2026-09-28 (later): Core copy-update sweep: re-pinned from `f2e106a` to `aaaa585` (268 → 290 conformance cases, eight clarified rules, none changing an existing answer). The docs' own text needed no edit, but the reasoning recorded about why (see the next entry) was itself wrong. See `.claude/HANDOFF.md`, "Copy-update sweep". Still not independently reviewed.
- 2026-09-28 (later still): A second fresh Opus agent reviewed the copy-update sweep, again standing in for Codex: not clean (4 should-fix, 2 minor). The main one: sidecar naming was wrongly said to "belong to a player" — it's this app's own job (TEXT-030); only automatic selection belongs to a player. Fixed the same day, including four more short GitHub comments (on #16, #14, #8, #6); see `.claude/HANDOFF.md`, "Second independent review". These fixes are Sonnet's, not Opus's — the two earlier commits' `Co-Authored-By` line is wrong in the same way and is left as-is, per the note in that section. Not yet reviewed by anyone.
- 2026-09-28 (later still): A third fresh Opus agent reviewed the second review's fixes, again standing in for Codex: not clean (some should-fix, some minor — almost all a fix applied in one place but missed a second copy elsewhere). Fixed the same day by a Sonnet builder session, including two more short GitHub comments (on #14 and #6); see `.claude/HANDOFF.md`, "Third independent review". Not yet reviewed by anyone.

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
