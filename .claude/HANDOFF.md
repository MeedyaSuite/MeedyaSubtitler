# HANDOFF — pick up here

> **Last updated:** 2026-09-28 (by a Claude Code economy-tier builder session, Sonnet, running a core copy-update sweep)
> **Working branch:** `feature/bcp47-language-policy` (cut from, and containing every commit of, `claude/keen-pascal-shoj9x`; pushed to `origin/feature/bcp47-language-policy` at `58d8f1b`, CI green, then reviewed by a fresh Opus agent and pushed again as `fc211a1`; will go to `alpha` in a single PR). Core then shipped more reviewed clarifications, so the copies here were moved to core's new commit `aaaa585` — see "Copy-update sweep" below.

## Starting a fresh session? Do this
1. Check out branch `feature/bcp47-language-policy` (or `claude/keen-pascal-shoj9x` if picking up the earlier, still-unmerged bootstrap work instead) and pull the latest.
2. Read `.claude/STANDING-RULES.md` (the rules always apply), then this file, then `.claude/CONTEXT.md`.
3. Deal with the **open questions** below (ask the owner if they are still unanswered).
4. Continue with the **next steps** queue.

## What the 2026-09-28 adoption session did

Adopted the shared **MWBM-MEDIA-LANG 1.0.0** language policy from
`MWBMPartners/MeedyaSuite-core`. Committed and **pushed** to
`origin/feature/bcp47-language-policy` at `58d8f1b`; CI (the new
policy-copies workflow) green. Answering open question 1 below about
`alpha` is still needed before a PR can be opened:

1. Created `docs/` (didn't exist yet) with a short README, and placed
   byte-identical copies of the policy document, its conformance test
   cases and schema, the reference language data and its schema, and the
   checker script itself under `docs/standards/` and `Tests/Fixtures/`,
   with `docs/standards/MWBM-MEDIA-LANG.lock` recording which commit they
   came from. Currently pinned to
   `f2e106a9d025c95d679eed825ab0f78a6b23ebe7` (moved once during this
   session as the master document was still being reviewed elsewhere).
   **Correction (see "Independent review" below):** an earlier version of
   this line said the move was "only wording and a test-harness
   clarification" — that move (core `968d820`) actually added a real rule,
   that builders must refuse a sidecar number above nine digits. No rule
   ID changed, but that's narrower than "only wording."
2. Added `.github/workflows/policy-copies.yml` — the repo's **first** CI
   workflow — running the checker on every PR and push. Passed
   `actionlint`; hardened further in the review below (permissions, a
   token for the checker, the checkout action's pin).
3. Added `.gitattributes` so the copies are never line-ending-converted.
4. Pointed `AGENTS.md`, `.claude/CLAUDE.md` and `.OpenAI/CONTEXT.md` at the
   policy document (the policy itself requires this — section 8.3 — and
   forbids pasting the rules in instead). There is no root `CLAUDE.md` or
   `GEMINI.md` in this repo, so those two weren't touched.
5. Read and commented on four open issues touching this policy, without
   rewriting them: three describing behaviour the policy would not allow —
   [#6](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6) (the
   canonical `SubtitleDocument` model has a single `language` field and no
   structured roles — corrected below, see "Independent review"),
   [#14](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/14)
   (cross-app handoff identifies a track by position only), and
   [#8](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/8) (defaults
   the waveform's audio track to "track 0" rather than the main-programme
   track) — and a fourth, [#5](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/5),
   which isn't a contradiction at all: just a note that the shared Swift
   implementation of this policy lives in MeedyaConverter for now, and none
   of the four planned SPM modules is an obvious home for it.

## Independent review, 2026-09-28 (fresh Opus agent, standing in for Codex)

Codex — the usual reviewer per rule R5 — was out of allowance, so a fresh
Opus agent with no memory of building the adoption reviewed it instead, per
rule R7 (AI fallback). **This is a fallback review, not the usual one**, and
the fixes below have **not themselves been reviewed yet** — that review is
still owed.

What it found and fixed:

- The pin-move note above overstated "only wording" (see item 1 above).
- The comment on #6 over-read TEXT-050 (it forbids collapsing distinct
  translations, not "a document must hold several languages") and
  mis-placed roles on individual cues rather than the whole track — a
  follow-up comment corrects both, and withdraws the word "untyped" used
  in an earlier internal note but never in the issue itself.
- The comments on #14 and #8 cited AUTO-010/AUTO-020 as though they bound
  MeedyaSubtitler directly; those rules govern *automatic selection*,
  which is Part B — a player's job, outside this app's canonical/text/
  small-presentation profile. Follow-up comments reframe the advice as "in
  the spirit of" those rules rather than a requirement.
- `docs/README.md` said MeedyaSubtitler "needs almost all of" the policy;
  section 2 actually gives it a much smaller slice (canonical, text, a
  small presentation part) and says explicitly that a project should not
  build the rest. Corrected, and the note now also points at
  `Tests/Fixtures/` for the case-file copies.
- The pointer sentence in `AGENTS.md`/`.claude/CLAUDE.md`/`.OpenAI/CONTEXT.md`
  said "reuse MeedyaConverter's implementation until a shared package
  exists" without saying where that implementation actually lives or what
  triggers the move — now matches policy section 9 exactly (MeedyaConverter,
  on a work-in-progress branch there, not yet on its own `alpha`; moves to
  a shared package once MeedyaPlayer or MeedyaSubtitler has code).
- `.claude/STANDING-RULES.md` R6 still named `claude/keen-pascal-shoj9x` as
  the one working branch while this handoff had already moved to
  `feature/bcp47-language-policy`; R6 only allows one. Fixed to say plainly
  that `feature/bcp47-language-policy` (which contains everything
  `claude/keen-pascal-shoj9x` has) is the one working branch until it
  merges.
- The CI workflow was missing `permissions: contents: read`, had no
  `GITHUB_TOKEN` for the checker (which hits GitHub's unauthenticated rate
  limit without one — reproduced as an HTTP 403), and pinned
  `actions/checkout` to an old v4 SHA on the deprecated Node 20 runtime.
  Fixed: explicit read-only permissions, the job's own token handed to the
  checker, and the checkout action re-pinned to v6.1.0.
- Several "not pushed" statements throughout this handoff, `.claude/CONTEXT.md`,
  `.OpenAI/CONTEXT.md` and `.OpenAI/MEMORY.md` were left stale once the
  branch was actually pushed. Corrected throughout.
- **Historical note, not a rewrite:** the four commits that adopted this
  policy (`fbae4a1`, `19aad9d`, `80bbb02`, `6f198b6`) did not themselves say
  they were unreviewed at the time they were made — they simply were not
  independently reviewed yet, which is what this section now records, not
  something being retroactively added to those commit messages.

## Copy-update sweep, 2026-09-28 (later the same day)

MeedyaSuite-core shipped several more reviewed clarifications on top of the
commit the copies were pinned to (`f2e106a9d025c95d679eed825ab0f78a6b23ebe7`).
This session moved the pin forward to core's new commit
`aaaa585aa145634c057c0bbdd9bd5fc11c3274a0`.

1. Ran `GITHUB_TOKEN=$(gh auth token) python3 scripts/media-lang/check_copies.py --update aaaa585aa145634c057c0bbdd9bd5fc11c3274a0`, then the checker again with no arguments: `MWBM-MEDIA-LANG 1.0.0: 6 copies match the master at MWBMPartners/MeedyaSuite-core@aaaa585aa145.` (exit 0). `.gitattributes` still lists all six copies — the file set didn't change, only their contents. The conformance case file went from 268 cases to 290; nothing in this repository's own prose named the old count, so there was nothing else to update for that.
2. Read what changed (eight clarified rules, all in the policy's own 1.0.0 changelog, none changing an existing case's answer): a malformed preference or menu value matches nothing, not even an identical malformed value, and a user whose preferences are all malformed counts as having none; "canonical order" in automatic selection means a track's position in full stored order among *every* track of its type; when every audio track is commentary or other, commentary is preferred; a forced-only subtitle search can match a forced track against a private-use or grandfathered audio tag; a sidecar builder reads what it's given with LANG-002's reader before writing the file name; a label lists each role once and leaves out an empty part along with its separator; and a malformed value keeps its text after LANG-001 step 1's trim.
3. **Checked, nothing to change:** none of `docs/README.md`, `AGENTS.md`, `.claude/CLAUDE.md`, `.claude/CONTEXT.md` or `.OpenAI/CONTEXT.md` describes any of the eight points above in enough detail to have been wrong — they only say, in general terms, that MeedyaSubtitler writes subtitle languages, roles and sidecar names, without describing the sidecar-naming algorithm or the automatic-selection rules (those belong to a player, outside this app's profile — see the clarifications posted on #14 and #8 in the previous round). So nothing here needed enriching or correcting this time.
4. `python3 scripts/media-lang/check_copies.py` and `actionlint` both still pass (checked again after this update).
5. **Not settled by this update:** the pin still points at a commit that exists only on core's `feature/bcp47-language-policy` branch, not on core's `main` (confirmed again — see the Next steps item below, which now names the new commit rather than the one this replaces).
6. Opened [#16 — Language policy (MWBM-MEDIA-LANG) adoption and conformance tracking](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/16) as the umbrella issue this and future re-pins are recorded against (none existed before this sweep). Commits from this point on `Refs #16`.

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
| 11 | Adopt MWBM-MEDIA-LANG 1.0.0 language policy (2026-09-28) | ✅ Done — see "What the adoption session did" above; **pushed** (`58d8f1b`, CI green) |
| 12 | Independent review of the language-policy branch (fresh Opus agent, standing in for Codex) | ✅ Done — see "Independent review" above; its own fixes are not yet reviewed |
| 13 | Codex review of the language-policy branch (or another independent AI system, once Codex has allowance again) | ⏳ Owed — the review at task 12 was a fallback, not the usual one |
| 14 | Copy-update sweep: re-pin to core `aaaa585` (2026-09-28, later the same day) | ✅ Done — see "Copy-update sweep" above; also not yet reviewed |

## Open questions for the owner
1. **`alpha` branch:** it doesn't exist yet. Should we create it from `main` so the single PR has something to target? (Suggested: yes, when we are ready to open the PR.) `feature/bcp47-language-policy` is pushed and reviewed, but still has nowhere to open a PR against until this is answered.
2. **"00:08 Codex review":** nothing in this repo is waiting on it. Does it relate to MeedyaSubtitler, or to a different project? If it's this repo, review the `claude/keen-pascal-shoj9x` branch.
3. **Where Codex reviews run:** cloud sessions don't have Codex or dev-team-plugins installed. Should reviews be run on your own machine, or should we try to install them in the cloud environment's setup script?

## Next steps (in order)
1. Run the still-owed Codex review (task 13) — or another independent AI system if Codex remains unavailable — over the fixes made in the "Independent review" section above (task 12 was itself a fallback and has not been checked by anyone else yet), and on `claude/keen-pascal-shoj9x` (task 8). Fix anything found.
2. Get answers to the open questions.
3. Once question 1 is answered and both branches are clean, combine into **one** PR (no PR stacking) rather than opening two — both branches are already pushed.
4. **After MeedyaSuite-core's `feature/bcp47-language-policy` branch merges to its `main`:** the lock here pins core commit `aaaa585aa145634c057c0bbdd9bd5fc11c3274a0` (moved forward from `f2e106a9d025c95d679eed825ab0f78a6b23ebe7` by the 2026-09-28 copy-update sweep, above) — as of this sweep it still exists only on that core branch, confirmed again by walking core's history (not yet an ancestor of core's `main`). This sweep does **not** settle that: core has not merged yet, so the risk is unchanged — if that branch is squash-merged and then deleted, the pinned commit can stop being reachable from GitHub's API, and the copy checker would start failing with nothing in this repo having changed. Once core merges, run `python3 scripts/media-lang/check_copies.py --update <the commit on core's main>` here to re-pin against a commit that will stay reachable.
5. Start phase 0: issue #5 (project foundation: Swift 6.3/SwiftUI project skeleton) → #14 (handoff with MeedyaConverter). Do deep planning first with sequential Opus agents (R3), then build with Sonnet/Haiku, then run the Codex review loop (R5). Bear in mind the language-policy comments left on #5, #6, #8 and #14 when this work starts.
