# HANDOFF — pick up here

> **Last updated:** 2026-09-28 (by a Claude Code economy-tier builder session, Sonnet, acting on a second independent review)
> **Working branch:** `feature/bcp47-language-policy` (cut from, and containing every commit of, `claude/keen-pascal-shoj9x`; pushed, CI green on every commit; will go to `alpha` in a single PR). Reviewed twice by fresh Opus agents standing in for Codex (see "Independent review" and "Second independent review" below); core shipped more reviewed clarifications in between, so the copies here were moved forward to core's new commit `aaaa585` — see "Copy-update sweep" below. Neither review round's fixes has itself been reviewed yet.

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
   came from. Then pinned to
   `f2e106a9d025c95d679eed825ab0f78a6b23ebe7` (moved once during this
   session as the master document was still being reviewed elsewhere) —
   this is a record of that first pin, not the current one; it was moved
   forward again since, to `aaaa585`, see "Copy-update sweep" below.
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
   rewriting them: [#6](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6)
   (a genuine policy conflict — the canonical `SubtitleDocument` model has
   a single `language` field and no structured roles — corrected below,
   see "Independent review"), [#14](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/14)
   (a recommendation, not a requirement, per the second independent review
   below — cross-app handoff identifies a track by position only), and
   [#8](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/8) (also a
   recommendation, not a requirement, per the same review — defaults the
   waveform's audio track to "track 0" rather than the main-programme
   track) — and a fourth, [#5](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/5),
   which is neither: just a note that the shared Swift implementation of
   this policy lives in MeedyaConverter for now, and none of the four
   planned SPM modules is an obvious home for it.

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
  which section 8.1 assigns to the player part of the presentation
  profile — not to Part B as a whole, which also covers ordinary menu and
  matching rules this app's own small presentation part can share in.
  Follow-up comments reframe the advice as "in the spirit of" those rules
  rather than a requirement.
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
3. **Checked, nothing in the documents needed changing — but this line's own reasoning was wrong, see the second review below:** none of `docs/README.md`, `AGENTS.md`, `.claude/CLAUDE.md`, `.claude/CONTEXT.md` or `.OpenAI/CONTEXT.md` describes any of the eight points above in enough detail to have been wrong — they only say, in general terms, that MeedyaSubtitler writes subtitle languages, roles and sidecar names, without describing the sidecar-naming algorithm itself. **Correction:** writing sidecar names IS this app's job (section 2's table; TEXT-030) — only automatic selection belongs to a player, outside this app's profile (see the clarifications posted on #14 and #8 in the previous round). The original wording here lumped sidecar naming in with automatic selection as though neither applied, which was wrong for sidecar naming.
4. `python3 scripts/media-lang/check_copies.py` and `actionlint` both still pass (checked again after this update).
5. **Not settled by this update:** the pin still points at a commit that exists only on core's `feature/bcp47-language-policy` branch, not on core's `main` (confirmed again — see the Next steps item below, which now names the new commit rather than the one this replaces).
6. Opened [#16 — Language policy (MWBM-MEDIA-LANG) adoption and conformance tracking](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/16) as the umbrella issue this and future re-pins are recorded against (none existed before this sweep). Commits from this point on `Refs #16`.

## Second independent review, 2026-09-28 (a second fresh Opus agent, standing in for Codex again)

Codex was still unavailable, so a second fresh Opus agent with no memory of building the earlier sections reviewed the copy-update sweep. Verdict: not clean — 4 should-fix and 2 minor findings. **This is another fallback review, not the usual one**, and the fixes below have **not themselves been reviewed** — that review is still owed. The builder session that made these fixes is Sonnet, not Opus; the two earlier commits' `Co-Authored-By: Claude Opus 5.5` lines are wrong in the same way and are not being rewritten — see the note at the end of this section.

What it found and what this session fixed:

- Item 3 of the copy-update sweep, above, said the sidecar-naming algorithm "belongs to a player, outside this app's profile" — wrong. Writing sidecar names is this app's own job (section 2; TEXT-030); only automatic selection belongs to a player. Corrected above, and a comment recording this — plus the requirement that a future sidecar writer read its input with LANG-002's reader (`fre` → `Film.fr.srt`, unrecognised → `Film.und.srt`) — was posted on [#16](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/16#issuecomment-5868498537). **This same error is in the commit message of `bf48908`**, which cannot now be changed without rewriting pushed history — recorded here plainly instead.
- `docs/README.md` said the full Part B menu, matching and automatic-selection logic "belongs to a player, not an editor," and added a "that's not 'almost all of it'" aside. Corrected: the full Part B menu ordering and automatic track selection are a player's job, but matching (MATCH-010 to MATCH-040) is needed by the text profile too (section 8.1) — MeedyaSubtitler's own profile. The aside was dropped as redundant once the actual scope is stated plainly.
- The note on the comments for #14 and #8 said those rules are governed by "Part B — a player's job" — too broad; Part B also covers ordinary menu/matching rules this app's own small presentation part shares in. Narrowed to what's actually true: section 8.1 assigns *automatic selection* specifically to the player part of the presentation profile. Short follow-up comments posted on [#14](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/14#issuecomment-5868493447) (also dropping "an identifying decision," a paraphrase, in favour of AUTO-010's own wording) and [#8](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/8#issuecomment-5868493744).
- Item 5 of the adoption session, above, listed #6, #14 and #8 together as "three describing behaviour the policy would not allow" — only #6 is an actual policy conflict; #14 and #8 are recommendations, as the previous round's own follow-up comments already said. Corrected above.
- The second comment on [#6](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6#issuecomment-5862570556) cited LANG-001 as the source of "`und` when the language isn't known" — that's LANG-002/LANG-003's rule, not LANG-001's, and it also implied a malformed typed tag is silently turned into `und`, when LANG-026 actually says it keeps its own text and is reported. A third comment corrected both, posted on [#6](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6#issuecomment-5868496112).
- Several places still named a single commit as though it were the current pushed state (which goes stale the moment another commit is pushed) — the header, this section's own history, and `.claude/CONTEXT.md`/`.OpenAI/CONTEXT.md` were reworded to say the branch is pushed with CI green on every commit, without pinning that claim to one commit hash.

**On attribution:** the maintainer's own instruction for this round is that commits should credit the model actually doing the work — Claude Sonnet 5, this session — not the model that reviewed. The two earlier commits on this branch (`fc211a1`, `bf48908`) are `Co-Authored-By: Claude Opus 5.5`, which was the reviewer's name, not the builder's, and that mislabel is not being corrected by rewriting those commits (this project never rewrites pushed history without an explicit instruction to do so). This paragraph is that correction, in writing, for anyone reading the commit log afterwards.

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
| 11 | Adopt MWBM-MEDIA-LANG 1.0.0 language policy (2026-09-28) | ✅ Done — see "What the adoption session did" above; **pushed; CI green on every commit** |
| 12 | Independent review of the language-policy branch (fresh Opus agent, standing in for Codex) | ✅ Done — see "Independent review" above; its own fixes are not yet reviewed |
| 13 | Codex review of the language-policy branch (or another independent AI system, once Codex has allowance again) | ⏳ Owed — the review at task 12 was a fallback, not the usual one |
| 14 | Copy-update sweep: re-pin to core `aaaa585` (2026-09-28, later the same day) | ✅ Done — see "Copy-update sweep" above; also not yet reviewed |
| 15 | Second independent review (a second fresh Opus agent, standing in for Codex again) | ✅ Done — see "Second independent review" above; its own fixes are not yet reviewed |

## Open questions for the owner
1. **`alpha` branch:** it doesn't exist yet. Should we create it from `main` so the single PR has something to target? (Suggested: yes, when we are ready to open the PR.) `feature/bcp47-language-policy` is pushed and reviewed, but still has nowhere to open a PR against until this is answered.
2. **"00:08 Codex review":** nothing in this repo is waiting on it. Does it relate to MeedyaSubtitler, or to a different project? If it's this repo, review the `claude/keen-pascal-shoj9x` branch.
3. **Where Codex reviews run:** cloud sessions don't have Codex or dev-team-plugins installed. Should reviews be run on your own machine, or should we try to install them in the cloud environment's setup script?

## Next steps (in order)
1. Run the still-owed Codex review (task 13) — or another independent AI system if Codex remains unavailable — over all the fixes made so far (tasks 12 and 15 were both fallbacks, and neither has been checked by anyone else yet), and on `claude/keen-pascal-shoj9x` (task 8). Fix anything found.
2. Get answers to the open questions.
3. Once question 1 is answered and both branches are clean, combine into **one** PR (no PR stacking) rather than opening two — both branches are already pushed.
4. **After MeedyaSuite-core's `feature/bcp47-language-policy` branch merges to its `main`:** the lock here pins core commit `aaaa585aa145634c057c0bbdd9bd5fc11c3274a0` (moved forward from `f2e106a9d025c95d679eed825ab0f78a6b23ebe7` by the 2026-09-28 copy-update sweep, above) — as of this sweep it still exists only on that core branch, confirmed again by walking core's history (not yet an ancestor of core's `main`). This sweep does **not** settle that: core has not merged yet, so the risk is unchanged — if that branch is squash-merged and then deleted, the pinned commit can stop being reachable from GitHub's API, and the copy checker would start failing with nothing in this repo having changed. Once core merges, run `python3 scripts/media-lang/check_copies.py --update <the commit on core's main>` here to re-pin against a commit that will stay reachable.
5. Start phase 0: issue #5 (project foundation: Swift 6.3/SwiftUI project skeleton) → #14 (handoff with MeedyaConverter). Do deep planning first with sequential Opus agents (R3), then build with Sonnet/Haiku, then run the Codex review loop (R5). Bear in mind the language-policy comments left on #5, #6, #8 and #14 when this work starts.
