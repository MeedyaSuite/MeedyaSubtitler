# HANDOFF — pick up here

> **Last updated:** 2026-10-04
> **Working branch:** `feature/bcp47-language-policy` (cut from, and containing every commit of, `claude/keen-pascal-shoj9x`; will go to `alpha` in a single PR). It adopts the shared language policy — see "The language-policy work". CI and review status are in "Review history". The round 5 fixes removed the sections that told the story of each review round; the commit messages keep that record.

## Starting a fresh session? Do this
1. Check out branch `feature/bcp47-language-policy` (it already contains everything that is on `claude/keen-pascal-shoj9x`, so there is no separate branch to pick up) and pull the latest.
2. Read `.claude/STANDING-RULES.md` (the rules always apply), then this file, then `.claude/CONTEXT.md`.
3. Deal with the **open questions** below (ask the owner if they are still unanswered).
4. Continue with the **next steps** queue.

## The language-policy work

The branch adopts the shared **MWBM-MEDIA-LANG 1.0.0** language policy from
`MWBMPartners/MeedyaSuite-core`. There is still no app code, so it is
documents and one check:

- `docs/` (new) with a short README, and byte-identical copies of the
  policy, its conformance cases and schema, the reference language data and
  its schema, and the checker script, under `docs/standards/`,
  `Tests/Fixtures/` and `scripts/media-lang/`.
  `docs/standards/MWBM-MEDIA-LANG.lock` records which core commit they came
  from, and `.gitattributes` stops line-ending conversion, filters, encoding
  conversion and `$Id$` expansion. Never edit a copy — change the master in
  core, then run the checker's `--update` here.
- `.github/workflows/policy-copies.yml`, the repo's first CI workflow. It
  runs the checker on every pull request and push, with read-only
  permissions, the job's own token handed to the checker, and
  `actions/checkout` pinned to v6.1.0 by full commit.
- A pointer to the policy, not a copy of its rules, in `AGENTS.md`,
  `.claude/CLAUDE.md` and `.OpenAI/CONTEXT.md` (policy section 8.3). There
  is no root `CLAUDE.md` or `GEMINI.md` in this repo.
- Comments on four issues (links under "GitHub comments" below): #6 is a
  real conflict with the policy (the `SubtitleDocument` model it proposes
  has no structured field for a subtitle track's roles, such as forced, SDH
  and commentary; its single `language` field is fine as long as it always
  holds a canonical tag); #14 and #8 carry recommendations, not
  requirements, because automatic track selection is a player's job
  (section 8.1); #5 notes that the shared Swift implementation lives in
  MeedyaConverter for now and that none of the four planned SPM modules is
  an obvious home for it.

**What the policy asks of this app** (`docs/README.md` has the same
summary): its profile is canonical and text — it writes subtitle
languages, roles and sidecar file names — plus a small presentation part
for its own language pickers, which follow Part B's menu rules. Matching
(MATCH-010 to MATCH-040) is needed by the text profile too (section 8.1).
Automatic track selection (AUTO-010 to AUTO-040) is a player's job, not
this app's. Writing sidecar names IS this app's job (TEXT-030): a future
sidecar writer reads the language it is given with LANG-002's reader
(`fre` → `Film.fr.srt`, unrecognised → `Film.und.srt`).

**Pin history:** the first pin was core `968d820`, which already had the
rule that builders refuse a sidecar number above nine digits. The adoption
session moved it once, to `f2e106a`; its note that no rule ID changed and
the move was only wording and a test-harness clarification was essentially
accurate (the policy text gained one sentence on how a test harness treats
refusal cases, the case schema gained an `error` field for them, and the
case file gained six refusal cases, 262 → 268). The copy-update sweep then
moved it to `aaaa585` (268 → 290 cases; among other changes it settled eight
points the text had left open, listed in the policy's own 1.0.0 changelog).
No rule ID changed at any step.

**GitHub comments** (later ones correct earlier ones; none was edited or
deleted):
- [#6](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6#issuecomment-5862052155), corrected in [one](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6#issuecomment-5862570556), [two](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6#issuecomment-5868496112), [three](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6#issuecomment-5869142026)
- [#14](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/14#issuecomment-5862052451), corrected in [one](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/14#issuecomment-5862571712), [two](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/14#issuecomment-5868493447), [three](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/14#issuecomment-5869135447)
- [#8](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/8#issuecomment-5862052749), corrected in [one](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/8#issuecomment-5862572996), [two](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/8#issuecomment-5868493744)
- [#5](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/5#issuecomment-5862053064)
- [#16 — Language policy (MWBM-MEDIA-LANG) adoption and conformance tracking](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/16) is the umbrella issue for this work and future re-pins (every commit from the copy-update sweep on carries `Refs #16` except `415aa4c`, `8dfa024`, `46c7501` and `fa7cd79`); its [comment](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/16#issuecomment-5868498537) records that writing sidecar names is this app's job.

## Review history

The one place review status is kept. Round N's fixes act on review N's findings. The third to ninth, and eleventh to sixteenth, reviews each gave one count for MeedyaSubtitler and MeedyaPlayer together (their rows say so).

| Round | Commits | What the round did | Covered by which review (range) | Result |
| --- | --- | --- | --- | --- |
| Adoption build | `fbae4a1` … `58d8f1b` | Adopted the policy: copies, first CI workflow, agent pointers, comments on #6/#14/#8/#5 | First stand-in review | Not clean (no numeric tally was recorded); fixed in round 1 |
| Round 1 fixes + copy-update sweep | `fc211a1`, `bf48908` | Fixed review 1's findings; re-pinned the copies to core `aaaa585` | Second stand-in review, `58d8f1b..bf48908` | Not clean — 4 should-fix, 2 minor findings; fixed in round 2 |
| Round 2 fixes | `970f8f4` | Fixed review 2's findings | Third stand-in review, `bf48908..970f8f4` | Not clean — across both repositories, 0 must-fix, 3 should-fix, 12 minor findings (this repository's own should-fix share: 2); fixed in round 3 |
| Round 3 fixes | `1263d79` | Fixed review 3's findings | Fourth stand-in review, `970f8f4..1263d79` | Not clean — across both repositories, 0 must-fix, 1 should-fix, 7 minor, 2 nits, almost all wrong statements about review history rather than wrong policy substance; fixed in round 4 |
| Round 4 fixes | `5b09c30` | Put review status into this one table; fixed the wrong statements the fourth review found | Fifth stand-in review, `1263d79..5b09c30` | Not clean — across both repositories, 1 should-fix, 9 minor, 3 nits and 1 follow-up; it confirmed this table's rows; fixed in round 5 |
| Round 5 fixes | `48de926` | cut the review narrative | sixth stand-in review (`5b09c30..48de926`) | not clean: 0 must, 0 should, 2 minor, 1 nit (across both repositories) |
| Round 6 fixes | `a2a860b` | completed the wrong-message lists | seventh stand-in review (`48de926..a2a860b`) | not clean: 0 must, 0 should, 2 minor, 3 nits (across both repositories) — wording and table upkeep only |
| Round 7 fixes | `a7b77c0`, `10b7b8b` | kept this table current; "Last updated" gives the date only | eighth stand-in review (`a2a860b..10b7b8b`) | not clean: 0 must, 1 should, 2 minor (across both repositories) |
| Round 8 fixes | `e284012` | the CI line states the rule instead of listing runs | ninth stand-in review (`10b7b8b..e284012`) | not clean: 0 must, 0 should, 2 minor (across both repositories) |
| Round 9 fixes | `44cf095` | recorded the eighth and ninth reviews in the table; said when CI began | Codex catch-up review, `53bbc0f..44cf095` (the first review of it) | covered by the next row |
| Codex catch-up (the tenth review) | up to `44cf095` | The first review by the actual, usual reviewer (Codex) — every review before this one was a fresh Opus agent standing in for it. It covered the whole branch as one piece rather than just the diff since the last review, so it also reached the commit before the adoption work (`6a4690e`) | Codex catch-up review, `53bbc0f..44cf095` | not clean — one finding, the `.gitattributes` protection gap (shared with MeedyaPlayer, which also had 7 findings of its own); acted on by `415aa4c` (round 10 fixes) |
| Round 10 fixes | `415aa4c` | Acted on the Codex catch-up review's finding | Eleventh review, a fresh Opus agent standing in for Codex, `44cf095..415aa4c` | not clean — 3 serious, 4 medium, 2 minor (across both repositories); acted on by `8dfa024` (round 11 fixes) |
| Round 11 fixes | `8dfa024`, `46c7501` | Acted on the eleventh review's findings; `46c7501` removed a trailing space | Twelfth review, a fresh Opus agent standing in for Codex, `415aa4c..46c7501` | not clean — 1 high, 2 medium, 5 low, 7 nits (across both repositories); acted on by `fa7cd79` (round 12 fixes) |
| Round 12 fixes | `fa7cd79` | Acted on the twelfth review's findings | Thirteenth review, a fresh Opus agent standing in for Codex, `46c7501..fa7cd79` | not clean — 0 high, 1 medium, 7 low, 12 nits (across both repositories); acted on by `8817667` (round 13 fixes) |
| Round 13 fixes | `8817667` | Acted on the thirteenth review's findings | Fourteenth review, a fresh Opus agent standing in for Codex, `fa7cd79..8817667` | not clean — 0 high, 1 medium, 2 low, 13 nits (across both repositories); acted on by `c2e4ef9` (round 14 fixes) |
| Round 14 fixes | `c2e4ef9` | Acted on the fourteenth review's findings | Fifteenth review, a fresh Opus agent standing in for Codex, `8817667..c2e4ef9` | not clean — 0 high, 0 medium, 7 low, 8 nits (across both repositories); acted on by the round 15 fixes, not yet reviewed |
| Round 15 fixes | `29e1ce5` | Acted on the fifteenth review's findings | Sixteenth review, a fresh Opus agent standing in for Codex, `c2e4ef9..29e1ce5` | not clean — 0 high, 0 medium, 3 low, 5 nits (across both repositories); acted on by the round 16 fixes, not yet reviewed |

Commits after `29e1ce5` are not yet reviewed. This table records finished reviews only.

- Every review except the Codex catch-up review (up to and including the ninth, then the eleventh to sixteenth) was a fresh Opus agent standing in for Codex. The Codex catch-up review is the only review by the actual, usual reviewer; commits after `29e1ce5` still await a review.
- `fc211a1` (round 1 fixes) and `bf48908` (copy-update sweep) say `Co-Authored-By: Claude Opus 5.5`, though a Sonnet builder made them. The other commits this work added before round 5 name Sonnet, which built them; round 5 was built by Opus and says so.
- Two commit messages carry claims later found wrong: `bf48908` says sidecar naming is a player's job, outside this app's profile (it is this app's job, TEXT-030; only automatic selection is a player's), and `970f8f4` says the branch has 'CI green on every commit' (see the CI line below) and that 'the full Part B menu and automatic selection are a player's job' (only automatic selection is; this app's own language pickers follow Part B's menu rules).
- `8dfa024` (`61985e1` in MeedyaPlayer) says it acts on "the stand-in review of round 11"; in this table that review is the eleventh (of the round 10 fixes).
- `46c7501`'s body says only "Not yet reviewed"; it does not say which review it acts on (it follows `8dfa024`, which acts on the eleventh review, and fixes a trailing space that commit left).
- `8817667`'s and `c2e4ef9`'s messages do not list every change they made (found by the fourteenth and fifteenth reviews).
- Neither the attribution nor these messages (`bf48908`, `970f8f4`, `46c7501`, `8dfa024`, `8817667`, `c2e4ef9`) is corrected in the commits themselves: pushed commits are not rewritten.
- **CI:** the workflow arrived with `19aad9d`, so commits from before it (such as `fbae4a1`, `6a4690e` and `53bbc0f`) have no check run. From `19aad9d` on, GitHub runs it on the last commit of each push; a commit pushed together with a later one has no run of its own (for example `19aad9d`, `80bbb02` and `6f198b6`, which went up with `58d8f1b` in the first push). GitHub's Actions page is the record of each run — this file deliberately does not list them, because such a list goes out of date with every push.

## Where we are (state of play)
- The project is at **planning stage**. There is no app code yet: just README, LICENSE, .gitignore, `docs/` (added by the language-policy work — see above), and the planning issues #1 to #15.
- **No pull requests** exist. **No `alpha` branch** exists yet.
- The previous session set up the project's "working memory":
  - `.claude/STANDING-RULES.md`: standing rules R1 to R10 and standing tasks T1 and T2, revised to the owner's latest list
  - `.claude/HANDOFF.md`: this file
  - `.claude/CONTEXT.md` and `.claude/CLAUDE.md`: project context, loaded automatically by Claude Code
  - `.OpenAI/CONTEXT.md` and `.OpenAI/MEMORY.md`, plus a root `AGENTS.md`: the same information for Codex and other AI tools
- The AI fallback rule (R7) was also written to the **device-wide** files (`~/.claude/CLAUDE.md`, `~/.codex/AGENTS.md`). ⚠️ In a cloud session those files are **wiped when the session ends**, so the lasting copy lives in this repo. The owner should copy the rule onto their own machine(s) (text is in `.OpenAI/MEMORY.md`, section "Device-wide rule").
- Documentation pass (T2): the README is accurate for the planning stage. There is **no API** (so no Swagger), **no web part** (so no Swagger UI) and **no app** (so no in-app help) yet. Nothing more to do until code exists.
- Codex review (R5): the 2026-09-23 session only changed documentation, and the Codex CLI wasn't installed in the cloud session. Its files (commit `6a4690e`) were covered later by the Codex catch-up review, `53bbc0f..44cf095` — see "Review history".

## Task queue
| # | Task | Status |
|---|---|---|
| 1 | Revise standing rules and tasks | ✅ Done |
| 2 | Add the plain-English rule (R1) | ✅ Done |
| 3 | Add the AI-fallback rule, for this repo and device-wide (R7) | ✅ Done (device copy needs setting up on the owner's machine) |
| 4 | Create and update the handoff | ✅ Done |
| 5 | Claude and Codex memory/context files | ✅ Done |
| 6 | Thorough documentation update | ✅ Done (nothing else applies yet: no code, API or web part) |
| 7 | Commit to the working branch | ✅ Done |
| 8 | Codex review of this session's changes | ✅ Covered by the Codex catch-up review (`53bbc0f..44cf095`, which includes `6a4690e`); see "Review history" |
| 9 | The Codex review the owner mentioned for **00:08** | ❓ Not visible from this repo (see open question 2) |
| 10 | Start phase 0 work (#5 foundation, then #14) | ⏸ Waiting for the owner's go-ahead |
| 11 | Adopt MWBM-MEDIA-LANG 1.0.0 language policy (2026-09-28) | ✅ Done — see "The language-policy work" above |
| 12 | Stand-in reviews of the language-policy branch, and their fixes (fresh Opus agents standing in for Codex) | See "Review history" — one table for every round |
| 13 | Codex review of the language-policy branch | ✅ Done for `53bbc0f..44cf095` (the Codex catch-up review); the commits after `44cf095` still await one — see "Review history" |
| 14 | Copy-update sweep: re-pin to core `aaaa585` (2026-09-28, later the same day) | ✅ Done — see "Pin history" above |

## Open questions for the owner
1. **`alpha` branch:** it doesn't exist yet. Should we create it from `main` so the single PR has something to target? (Suggested: yes, when we are ready to open the PR.) `feature/bcp47-language-policy` (review status: see "Review history") still has nowhere to open a PR against until this is answered.
2. **"00:08 Codex review":** nothing in this repo is waiting on it. Does it relate to MeedyaSubtitler, or to a different project?
3. **Where Codex reviews run:** cloud sessions don't have Codex or dev-team-plugins installed. Should reviews be run on your own machine, or should we try to install them in the cloud environment's setup script?

## Next steps (in order)
1. Review only the commits after `29e1ce5` — Codex if it has allowance, otherwise a fresh independent agent, saying which one was used. "Review history" shows what each earlier review covered (`claude/keen-pascal-shoj9x`'s only commit beyond `main`, `6a4690e`, is already inside the Codex catch-up range). Fix anything found.
2. Correct the [first comment on #6](https://github.com/MeedyaSuite/MeedyaSubtitler/issues/6#issuecomment-5862052155) (checked 2026-09-28: none of the later comments does): it says "SDH/commentary must be preserved through every conversion (rule TRACK-040)", but TRACK-040 lists only "SDH, captions, audio description and text descriptions"; keeping a commentary flag rests on COMPAT-030 ("Valid existing language data, flags and titles MUST be preserved when a file or record is touched for another reason"). MeedyaPlayer #3 had the same slip and was corrected in MeedyaPlayer's round 5 fixes.
3. Get answers to the open questions.
4. Once question 1 is answered and the branch is clean, open **one** PR from `feature/bcp47-language-policy` (no PR stacking). `claude/keen-pascal-shoj9x` has nothing the feature branch lacks — its only commit beyond `main`, `6a4690e`, is already on it — so there is nothing separate to combine.
5. **After MeedyaSuite-core's `feature/bcp47-language-policy` branch merges to its `main`:** the lock here pins core commit `aaaa585aa145634c057c0bbdd9bd5fc11c3274a0`, which (checked 2026-09-28) is still only on that core branch, not an ancestor of core's `main`. If that branch is squash-merged and then deleted, the pinned commit can stop being reachable from GitHub's API, and the copy checker would start failing with nothing in this repo having changed. Once core merges, run `GITHUB_TOKEN=$(gh auth token) python3 scripts/media-lang/check_copies.py --update <the commit on core's main>` here to re-pin against a commit that will stay reachable.
6. Start phase 0: issue #5 (project foundation: Swift 6.3/SwiftUI project skeleton) → #14 (handoff with MeedyaConverter). Do deep planning first with sequential Opus agents (R3), then build with Sonnet/Haiku, then run the Codex review loop (R5). Bear in mind the language-policy comments left on #5, #6, #8 and #14 when this work starts.
