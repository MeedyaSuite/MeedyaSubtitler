# HANDOFF — pick up here

> **Last updated:** 2026-09-28 (by a Claude Code economy-tier builder session, Sonnet)
> **Working branch:** `feature/bcp47-language-policy` (cut from `claude/keen-pascal-shoj9x`; will go to `alpha` in a single PR, same as the branch it came from)

## Starting a fresh session? Do this
1. Check out branch `feature/bcp47-language-policy` (or `claude/keen-pascal-shoj9x` if picking up the earlier, still-unmerged bootstrap work instead) and pull the latest.
2. Read `.claude/STANDING-RULES.md` (the rules always apply), then this file, then `.claude/CONTEXT.md`.
3. Deal with the **open questions** below (ask the owner if they are still unanswered).
4. Continue with the **next steps** queue.

## What this session (2026-09-28) did

Adopted the shared **MWBM-MEDIA-LANG 1.0.0** language policy from
`MWBMPartners/MeedyaSuite-core`. Local commits only, **not pushed** (that's
for a later session, alongside answering open question 1 below about
`alpha`):

1. Created `docs/` (didn't exist yet) with a short README, and placed
   byte-identical copies of the policy document, its conformance test
   cases and schema, the reference language data and its schema, and the
   checker script itself under `docs/standards/` and `Tests/Fixtures/`,
   with `docs/standards/MWBM-MEDIA-LANG.lock` recording which commit they
   came from. Currently pinned to
   `f2e106a9d025c95d679eed825ab0f78a6b23ebe7` (moved once during this
   session as the master document was still being reviewed elsewhere — no
   rule ID changed, only wording and a test-harness clarification).
2. Added `.github/workflows/policy-copies.yml` — the repo's **first** CI
   workflow — running the checker on every PR and push. Passes
   `actionlint`.
3. Added `.gitattributes` so the copies are never line-ending-converted.
4. Pointed `AGENTS.md`, `.claude/CLAUDE.md` and `.OpenAI/CONTEXT.md` at the
   policy document (the policy itself requires this — section 8.3 — and
   forbids pasting the rules in instead). There is no root `CLAUDE.md` or
   `GEMINI.md` in this repo, so those two weren't touched.
5. Read and commented on four open issues that already describe behaviour
   the policy would not allow, without rewriting them:
   [#6](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6) (the
   canonical `SubtitleDocument` model has one untyped `language` field and
   no structured roles), [#14](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/14)
   (cross-app handoff identifies a track by position only),
   [#8](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/8) (defaults
   the waveform's audio track to "track 0" rather than the main-programme
   track), and [#5](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/5)
   (a note that the shared Swift implementation of this policy lives in
   MeedyaConverter for now, and none of the four planned SPM modules is an
   obvious home for it).
6. **Not done yet:** the Codex review this branch is owed (rule R5) —
   nobody has reviewed this work with a different AI system yet. Do that
   before pushing.

## Where we are (state of play)
- The project is at **planning stage**. There is no app code yet: just README, LICENSE, .gitignore, `docs/` (new this session — see above), and the planning issues #1 to #15.
- **No pull requests** exist. **No `alpha` branch** exists yet.
- The previous session set up the project's "working memory":
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
| 11 | Adopt MWBM-MEDIA-LANG 1.0.0 language policy (2026-09-28) | ✅ Done — see "What this session did" above; not pushed |
| 12 | Codex review of the language-policy branch | ⏳ Owed — nobody has reviewed this with a different AI system yet |

## Open questions for the owner
1. **`alpha` branch:** it doesn't exist yet. Should we create it from `main` so the single PR has something to target? (Suggested: yes, when we are ready to open the PR.) This also now blocks pushing `feature/bcp47-language-policy` — it has nowhere to open a PR against either.
2. **"00:08 Codex review":** nothing in this repo is waiting on it. Does it relate to MeedyaSubtitler, or to a different project? If it's this repo, review the `claude/keen-pascal-shoj9x` branch.
3. **Where Codex reviews run:** cloud sessions don't have Codex or dev-team-plugins installed. Should reviews be run on your own machine, or should we try to install them in the cloud environment's setup script?

## Next steps (in order)
1. Run the owed Codex review on `feature/bcp47-language-policy` (task 12) and on `claude/keen-pascal-shoj9x` (task 8), and fix anything found in either.
2. Get answers to the open questions.
3. Once question 1 is answered and both branches are Codex-clean, push and combine into **one** PR (no PR stacking) rather than opening two.
4. Start phase 0: issue #5 (project foundation: Swift 6.3/SwiftUI project skeleton) → #14 (handoff with MeedyaConverter). Do deep planning first with sequential Opus agents (R3), then build with Sonnet/Haiku, then run the Codex review loop (R5). Bear in mind the language-policy comments left on #5, #6, #8 and #14 when this work starts.
