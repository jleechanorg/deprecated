# Nextsteps — NPC and scene generation — 2026-11-18

Canonical copy: https://github.com/jleechanorg/roadmap/blob/main/nextsteps-npc-scene-generation-2026-11-18.md

## Table of contents

- [Executive summary](#executive-summary)
- [Context](#context)
- [Bead index](#bead-index)
- [Work queue](#work-queue)
- [Decisions needing Jeffrey](#decisions-needing-jeffrey)
- [Timeline and parallel lanes](#timeline-and-parallel-lanes)
- [PR / merge state](#pr--merge-state)
- [Learnings pointer](#learnings-pointer)
- [Roadmap pointer](#roadmap-pointer)

## Executive summary

- **Mode:** default (beads + roadmap). Run from the Grok Scenes box at 4:57 PM PT on 2026-11-18 (America/Los_Angeles). Live GitHub state was refreshed with `gh` in this same run before writing.
- **Outcomes:** Nine scene-generation PRs have merged since Nov 12, ending with [#11414](https://github.com/jleechanorg/worldarchitect.ai/pull/11414) (mobile 640px JPEG preview, desktop full image) at 1:30 AM PT today. Grok Scenes is driving [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233) (anime portrait style routing) at stage 3. A reviewer-fix commit landed at 4:52 PM PT (head `8c018bf7a299`): the Jev classify wait is now bounded so the worst case is 136s, under the 140s client timeout, and several P2s are addressed. Two cold `/static-review` seats had WITHHELD at the previous head `7d0f14d7dd49` (coverage / 600s deadline). Those seats, an independent `/er`, and visual sign-off have not yet been rerun at `8c018bf7a299`. A Mac/Linux audit (`/Users/jleechan/roadmap/npc-scene-generation-pr-audit-2026-11-18.md`) reported nothing stranded locally; that file is not in this git repo and was not re-read from this box.
- **Risks / blockers:** [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233) still needs two cold seats, `/er`, visual approval of `anime_hana.png` and `western_brom.png`, and Jeffrey's `MERGE APPROVED` (prod delta is over 150 lines). [#11053](https://github.com/jleechanorg/worldarchitect.ai/pull/11053) is the next closest to approval but is `CONFLICTING` against current main and last moved on Nov 1. Several other open PRs are blocked on paid validation, an operator hold, a billing policy, merge conflicts, or Root write-custody. Jeffrey granted a **$20** paid-provider cap; how to allocate it is still an open decision.
- **Next:** Rerun the two cold seats and `/er` plus visual sign-off on [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233) at `8c018bf7a299`. In parallel, rebase [#11053](https://github.com/jleechanorg/worldarchitect.ai/pull/11053) onto main. Do not merge [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233) or spend the $20 until Jeffrey decides. Status updates every 10 minutes until 11:00 PM PT tonight.
- **Beads:** Not updated. This box has no `br` CLI. No open beads in the local `.beads` snapshot were found whose titles track these PRs. Recommended creates are listed in [Bead index](#bead-index).

## Context

This `/nextsteps` default-mode run follows a work block on NPC and scene generation in `jleechanorg/worldarchitect.ai`, plus [worldai_frontend #602](https://github.com/jleechanorg/worldai_frontend/pull/602). The living request is to persist the plan on this roadmap repo's `origin/main`, keep driving authorized PR work, report every 10 minutes, use parallel lanes, and surface the decisions that need Jeffrey — including how to spend the $20 paid-provider cap.

This box has no `br` and no `~/roadmap`. Publication target is `/workspace/worldarchitect-roadmap` (`jleechanorg/worldarchitect-roadmap`), already at `origin/main` `5a3fc03` after `git fetch`. The repo has no `AGENTS.md`; the expected-head, direct-`origin/main` workflow from `jleechanorg/roadmap`'s `AGENTS.md` (2026-11-01 / 2026-11-16) was applied instead. That same `AGENTS.md` now calls `jleechanorg/roadmap` the canonical roadmap and marks `worldarchitect-roadmap` deprecated; this run still publishes here because that was the explicit box instruction. No roadmap PR was opened.

Scope: assessment and roadmap artifacts only in this commit. Code-repository merges and paid provider calls are not authorized by this publication. [#10953](https://github.com/jleechanorg/worldarchitect.ai/pull/10953) remains Root-owned for writes unless Jeffrey grants Grok Scenes custody.

## Bead index

Beads were **not updated**. There is no `br` CLI on this box, so the default-mode bead write could not be performed. The local issues snapshot at `/workspace/wt11233-main/.beads/issues.jsonl` (content last meaningfully from about Nov 11, even though the file mtime is Nov 18) has **no open beads whose titles track these PRs**. Hits on numbers such as `11233` were false positives inside unrelated closed or tombstoned beads (`rev-rfvnk`, `rev-9wh01`, `rev-gje0b`, `rev-1vtuw`, `rev-qvecs`, `rev-83t5s`, `rev-rh5z5.5`, `rev-bbsv`) and should not be touched.

When `br` is available on a publisher host, these beads should be **created** (or updated if a canonical id already exists outside this snapshot):

| Suggested bead | Title | Priority / status | Link |
|----------------|-------|-------------------|------|
| *(create)* | Drive [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233) from stage 3 to stage 5 at head `8c018bf7a299` (cold seats, `/er`, visual, then MERGE APPROVED) | p1 / open | no id yet — use `br show` after create |
| *(create)* | Rebase and finish [#11053](https://github.com/jleechanorg/worldarchitect.ai/pull/11053) (conflicts vs main; stage 3; `/advice` quorum not established) | p1 / open | no id yet |
| *(create)* | Allocate Jeffrey's $20 paid-provider budget across [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233) real-run refresh, [#10953](https://github.com/jleechanorg/worldarchitect.ai/pull/10953) validation, and/or [#11151](https://github.com/jleechanorg/worldarchitect.ai/pull/11151) | p1 / blocked on Jeffrey | no id yet |
| *(create)* | [#11425](https://github.com/jleechanorg/worldarchitect.ai/pull/11425) automatic paid regeneration billing policy | p1 / blocked on Jeffrey | no id yet |
| *(create)* | Release or keep `hold:operator` on [#10882](https://github.com/jleechanorg/worldarchitect.ai/pull/10882) | p2 / blocked on Jeffrey | no id yet |
| *(create)* | Custody decision for Root-owned [#10953](https://github.com/jleechanorg/worldarchitect.ai/pull/10953) (paid validation still blocked) | p1 / blocked on Jeffrey | no id yet |
| *(create)* | Send the `#dot-coordination` review card for [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233) | p2 / blocked on Jeffrey (outgoing message) | no id yet |

## Work queue

1. **Rerun stage-3 gates on [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233) at `8c018bf7a299`.** Goal: two independent cold `/static-review` seats that actually finish the changed files, an independent `/er`, and `VISUAL APPROVED at 8c018bf7a299` for `anime_hana.png` and `western_brom.png`. Acceptance: both seats vote at this exact head (not `7d0f14d7dd49`); `/er` names that SHA; visual sign-off names that SHA. Files/areas: `mvp_site/user_portrait_service.py`, `mvp_site/avatar_image_gen.py`, `mvp_site/portrait_generator_agent.py`, `mvp_site/agent_prompts.py`, `mvp_site/tests/test_portrait_style_routing.py`, evidence gist https://gist.github.com/jleechan2015/f3ab7a81bc753c3e558e192a9e559cda (refresh if the head moved). Blocker: prior seats WITHHELD because large files such as `agent_prompts.py` could not be fully read within the 600s deadline — use saved-material packets scoped to changed regions; `knowledgeWork` subagents give truly cold seats. Do not merge in this step.

2. **Stop at stage 5 for Jeffrey's `MERGE APPROVED` on [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233).** Prod delta is +277/-23 (over 150 lines). Acceptance: stage-5 checklist complete at the then-current head, then an explicit human `MERGE APPROVED`. Do not merge without it.

3. **Rebase [#11053](https://github.com/jleechanorg/worldarchitect.ai/pull/11053) onto current `main` and re-verify stage 3.** Goal: clear `CONFLICTING`, then complete the missing second `/advice` seat (a Nov 1 review that claimed `/advice APPROVED` was corrected in-thread: one reviewer is not a quorum). Acceptance: mergeable, current-head CI, two independent advice votes, `/er` at the new head. Files/areas: `mvp_site/scene_illustration_policy.py`, `mvp_site/scene_presence.py`, `mvp_site/scene_illustration_worker.py`. Last updated Nov 1, 2:02 PM PT, so treat labels and evidence as stale until refreshed. This is next after, or in parallel with, #11233 because the branches do not share exclusive write scope.

4. **Hold paid evidence until the $20 allocation is decided.** Candidates: a small real-run refresh of #11233 style routing at the current head; #10953 validation (3 Gemini schema checks + 1 story turn) but Root owns writes; #11151 grounding evidence (audit said the Gemini cap was 880/880 — not re-verified live this run; last on-PR usage note seen was 436/500 on Nov 6). Acceptance: Jeffrey names the split; then run only that work.

5. **Do not write [#10953](https://github.com/jleechanorg/worldarchitect.ai/pull/10953) unless Jeffrey grants Grok Scenes custody.** It is draft, stage 1, `CONFLICTING`, blocked on paid validation. Root remains the write owner.

6. **Leave [#10882](https://github.com/jleechanorg/worldarchitect.ai/pull/10882) and [#11425](https://github.com/jleechanorg/worldarchitect.ai/pull/11425) parked** until Jeffrey releases `hold:operator` and sets the auto-paid-regen billing policy. Both also have merge conflicts.

7. **Queue, do not expand into, the remaining open scene PRs** unless a lane frees up and no gate is missing: [#11651](https://github.com/jleechanorg/worldarchitect.ai/pull/11651) (active today, stage 2, mergeable), [#11373](https://github.com/jleechanorg/worldarchitect.ai/pull/11373), [#11388](https://github.com/jleechanorg/worldarchitect.ai/pull/11388), [#11396](https://github.com/jleechanorg/worldarchitect.ai/pull/11396), [#11068](https://github.com/jleechanorg/worldarchitect.ai/pull/11068), [#11359](https://github.com/jleechanorg/worldarchitect.ai/pull/11359), [worldai_frontend #602](https://github.com/jleechanorg/worldai_frontend/pull/602) (conflicts).

8. **Status cadence:** post a short status every 10 minutes until 11:00 PM PT tonight while work is active. This is a non-blocking progress report, not an approval checkpoint.

## Decisions needing Jeffrey

1. **How to allocate the $20 paid-provider budget** granted this afternoon. Candidates: (a) #11233 real-run refresh at current head (small); (b) #10953 validation — 3 Gemini schema checks + 1 story turn — but Root owns writes; (c) #11151 grounding evidence. Grok Scenes will not spend it until you name the split.
2. **[#11425](https://github.com/jleechanorg/worldarchitect.ai/pull/11425) billing policy:** may a stalled scene poll spend one automatic paid regeneration?
3. **Release or keep `hold:operator` on [#10882](https://github.com/jleechanorg/worldarchitect.ai/pull/10882)** (portrait reference refresh immediately before scene generation; stage 4, still draft, conflicts).
4. **`MERGE APPROVED` for [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233)** once it actually reaches stage 5 (prod > 150 lines). Not asked for now; asked only after the new-head seats, `/er`, and visual sign-off land.
5. **May Grok Scenes take write custody of Root-owned [#10953](https://github.com/jleechanorg/worldarchitect.ai/pull/10953)?** Without that, Grok Scenes can only report, not push.
6. **Send the `#dot-coordination` review card for [#11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233)?** An outgoing Slack/message draft is waiting; sending it needs your approval of recipient and text.

## Timeline and parallel lanes

Execution start for the continued drive: 4:57 PM PT, 2026-11-18 (America/Los_Angeles). Status window ends 11:00 PM PT tonight. The user cadence is every 10 minutes; the skill's 20-minute milestones and hourly rollups still apply as a subset (no duplicate reports at :20/:40/:00 if a 10-minute update already went out).

| Elapsed estimate | Lane / owner | Scope / dependencies | Deliverable / proof |
|---|---|---|---|
| 0–40m | Lane A — Grok Scenes on #11233 | Exclusive write: `feat/user-portrait-1k-and-anime-flash-lite-20261107`. Launch two cold `/static-review` seats at `8c018bf7a299` with changed-region packets. Independent of Lane B. | Two seat receipts naming `8c018bf7a299` |
| 0–30m | Lane B — Grok Scenes on #11053 rebase | Exclusive write: `fix/scene-figures-followups-20261101`. Merge or rebase onto current `main`, resolve conflicts, push. Do not touch #11233 files. | PR becomes `MERGEABLE`; new head SHA |
| 40–90m | Lane A continued | `/er` + visual sign-off of `anime_hana.png` and `western_brom.png` at the same #11233 head (or a newer fix head if seats require a follow-up commit). $20 spend only if Jeffrey allocated it to this refresh. | `/er` verdict + `VISUAL APPROVED at <sha>` |
| 30–90m | Lane B continued | After rebase: refresh evidence if needed; second `/advice` seat (quorum). | Two advice votes; `/er` at new head |
| Continuous to 11:00 PM PT | Lane C — status | No exclusive code writes. Every 10 minutes: elapsed time, heads, lane state, blockers, next milestone. Hourly rollup at 5:57, 6:57, 7:57, 8:57, 9:57, 10:57 PM PT. | Status notes in-session; no extra roadmap commit required per tick |
| After stage-5 gates | Lane A stop | Jeffrey `MERGE APPROVED` is a user-only gate. | No merge until that word |

- **Critical path:** #11233 cold seats → `/er` + visual → Jeffrey `MERGE APPROVED`. #11053 is important but not on that merge path.
- **Concurrency ceiling (provisional):** 3 useful lanes (A, B, C). Binding limits are exclusive branch writes, cold-review seat runtime (600s), and the unallocated $20 provider cap. Reassess before launching paid runs or a third write lane (#11651 is mergeable and active, but do not start it until A/B have spare capacity and no new authority is required).
- **Do not start:** paid provider calls, #10953 writes, #10882/#11425 unblocking, or sending the `#dot-coordination` card, until the matching Jeffrey decision lands.
- Milestones while active: +10m, +20m, +30m, +40m, +50m, +60m (hourly rollup), then every 10 minutes through 11:00 PM PT. Finish promptly if the authorized work ends earlier; do not pad the clock.

## PR / merge state

Live `gh pr view` + `gh api repos/.../pulls/<n>/files` in this run (snapshot 4:57 PM PT, 2026-11-18, America/Los_Angeles). Status words below are from that same-session check.

**LOC heuristic (same as the 2026-10-31 handoff):** non-prod = `tests/`, `testing_*`, `docs/`, `roadmap/`, `specs/`, `*.md`, `*.json`; prod = everything else. PR-body figures are noted when they differ, usually because a body counted prompt/schema/YAML/scripts the other way.

### Merged since Nov 12 (`jleechanorg/worldarchitect.ai`)

- [PR #11361](https://github.com/jleechanorg/worldarchitect.ai/pull/11361): **MERGED** Nov 12, 12:34 PM PT. API for recent scene images used by the library hero banner. Prod +91/-0, non-prod +261/-3. Label still `stage:1-coding` (historical). Head `4defec770ece`.
- [PR #11353](https://github.com/jleechanorg/worldarchitect.ai/pull/11353): **MERGED** Nov 12, 8:06 PM PT. Turns off scene images for marked test users. Prod +320/-5 (includes `scripts/backfill_test_user_flags.py` +147; remaining app code +173/-5), non-prod +859/-1. Label still `stage:2-evidence`. Head `af5d6ee2929f`.
- [PR #11417](https://github.com/jleechanorg/worldarchitect.ai/pull/11417): **MERGED** Nov 13, 10:52 PM PT. Logging to diagnose the Nov 13 scene-job stall (Cloud Run instance + job lifecycle only). Prod +98/-1, non-prod +69/-0. No stage label. Head `454cfb1f8b87`.
- [PR #11398](https://github.com/jleechanorg/worldarchitect.ai/pull/11398): **MERGED** Nov 14, 6:13 PM PT. Library hero scenes chosen by the backend from any illustrated campaign (up to 15 scenes from 8 campaigns). Prod +165/-59, non-prod +464/-112. `stage:5-final-approval`. Head `06f1d8978ad3`.
- [PR #11458](https://github.com/jleechanorg/worldarchitect.ai/pull/11458): **MERGED** Nov 15, 5:13 AM PT. Scene images default to off for test accounts that never saved a preference (read-time settings default). Prod +24/-1, non-prod +135/-0. No stage label. Head `804cb67ed812`.
- [PR #11475](https://github.com/jleechanorg/worldarchitect.ai/pull/11475): **MERGED** Nov 15, 1:21 PM PT. `scene_illustration_request_count` metric + `SCENE_ILLUSTRATION_REQUEST` log line. Heuristic prod +248/-1 (app `portrait_bq_logging.py` +65/-1; monitoring deploy/yaml/verify +183/-0), non-prod +316/-0 (includes Grafana JSON). No stage label. Head `cc36f9ada6d0`.
- [PR #11354](https://github.com/jleechanorg/worldarchitect.ai/pull/11354): **MERGED** Nov 15, 4:12 PM PT. Estimated scene-image cost in the daily report. Prod +100/-0, non-prod +191/-2. Label still `stage:1-coding`. Head `8f235a827a3f`.
- [PR #11476](https://github.com/jleechanorg/worldarchitect.ai/pull/11476): **MERGED** Nov 15, 4:25 PM PT. Scene lifecycle metrics + `SCENE_ILLUSTRATION_SKIPPED` log + Grafana panels. Heuristic prod +109/-0 (worker +7/-0; monitoring metric YAML +102/-0), non-prod +256/-0. No stage label. Head `4710dbd47f2a`.
- [PR #11414](https://github.com/jleechanorg/worldarchitect.ai/pull/11414): **MERGED** Nov 18, 1:30 AM PT. Serve a 640px JPEG preview to mobile and the full image to desktop. Prod +231/-13, non-prod +592/-3. `stage:5-final-approval`. Head `32eb98296b6b`.

### Open — driven by Grok Scenes now

- [PR #11233](https://github.com/jleechanorg/worldarchitect.ai/pull/11233): **OPEN** (not draft, `MERGEABLE`). Anime / style routing: portraits with no style go through a TypeSafe Jev classifier; anime-style ones use Gemini's image model, everything else stays on Grok. Stage 3 (`stage:3-evidence-review`). Prod +277/-23, non-prod +721/-7 (PR body still says +297/-23 / +701/-7 and is slightly stale). Head **`8c018bf7a299`** (4:52 PM PT: bound Jev to 2s connect + 4s read so worst case is 136s < 140s client timeout; billing key matches the image path; compact classifier context; first valid style key wins; no fabricated `avatar` style). Prior head `7d0f14d7dd49` (4:45 PM PT checkpoint): both cold seats WITHHELD for coverage. Remaining: rerun seats + `/er` + visual at the new head; then Jeffrey `MERGE APPROVED`. Preview deploys failed earlier this afternoon (runner/gcloud credentials), not treated as a diff failure.
- [PR #11053](https://github.com/jleechanorg/worldarchitect.ai/pull/11053): **OPEN** (not draft, **`CONFLICTING`**). Keeps absent cast unsupplied, reuses `scene_presence` matching, stops truncating scene figures. Stage 3. Prod +31/-51, non-prod +138/-18 (body +35/-55 / +134/-14; difference is prompt/schema counted as non-prod here). Head `9b8cfc045e56`, last updated Nov 1, 2:02 PM PT. `/advice APPROVED` from that day is **not** established (only one reviewer; corrected in-thread). Next after #11233 once conflicts are cleared.

### Other open

- [PR #10953](https://github.com/jleechanorg/worldarchitect.ai/pull/10953): **OPEN**, draft, **`CONFLICTING`**, stage 1 (`stage:1-coding`). Auto-generates portraits for present NPCs behind the admin setting. Prod +413/-103, non-prod +5742/-2319 (body +447/-110 / +5708/-2312; the Nov 18 audit's +4086/-2201 prod is a different base and should not be used). Head `4fc696b71db8`, last updated Nov 5, 9:33 AM PT. Root-owned writes; blocked on paid validation. A Grok Scenes custody grant is a Jeffrey decision.
- [PR #11068](https://github.com/jleechanorg/worldarchitect.ai/pull/11068): **OPEN**, draft, `MERGEABLE`, stage 3. Persists `present_npcs` on story entries and turn payloads. Prod +31/-0, non-prod +534/-0. Head `5f1d87d872d7`, last updated Nov 2, 3:36 PM PT.
- [PR #11151](https://github.com/jleechanorg/worldarchitect.ai/pull/11151): **OPEN**, draft, **`CONFLICTING`**, stage 2 (`stage:2-evidence`). Grounds captured NPC availability before scene generation. Prod +134/-8, non-prod +3729/-106 (body +186/-29 / +3677/-85; prompts/schemas counted as non-prod here). Head `d862f23701dd`, last updated Nov 7, 12:04 PM PT. The Nov 18 audit said the Gemini spend cap was 880/880; that cap was not re-verified live in this run.
- [PR #10882](https://github.com/jleechanorg/worldarchitect.ai/pull/10882): **OPEN**, draft, **`CONFLICTING`**, stage 4 (`stage:4-ci-undraft`) plus **`hold:operator`**. Refreshes the portrait reference immediately before scene generation. Heuristic prod +607/-1 (worker +66/-1; `scripts/package_scene_evidence.py` +541/-0), non-prod +1079/-7 (body/audit used prod +66/-1 / +62/-1). Head `bfc3bc6ee16b`, last updated Oct 30, 8:06 PM PT. Parked until the hold is released.
- [PR #11359](https://github.com/jleechanorg/worldarchitect.ai/pull/11359): **OPEN**, draft, `MERGEABLE`, stage 2. Requests coherent scene head/body proportions. Heuristic prod +0/-0, non-prod +35/-3 (body +3/-3 / +32/-0: the three production lines are `scene_image.md` + `prompt_tool_contracts.json`, counted as non-prod here). Head `7f2cc1d5240b`, last updated Nov 11, 4:29 PM PT. Audit: blocked on real-provider generated-image validation.
- [PR #11388](https://github.com/jleechanorg/worldarchitect.ai/pull/11388): **OPEN**, not draft, `MERGEABLE`, no stage label. Only publishes the pending “Painting scene…” placeholder when cadence actually selects the scene. Prod +103/-24, non-prod +351/-4. Head `f60f0710974d`, last updated Nov 13, 5:30 AM PT.
- [PR #11396](https://github.com/jleechanorg/worldarchitect.ai/pull/11396): **OPEN**, not draft, **`CONFLICTING`**, no stage label. Bounded moderation fallback + skip semantics for scene illustrations. Prod +310/-34, non-prod +702/-6 (body +348/-36 / +655/-6). Head `0b2184294a43`, last updated Nov 16, 9:52 AM PT.
- [PR #11425](https://github.com/jleechanorg/worldarchitect.ai/pull/11425): **OPEN**, not draft, **`CONFLICTING`**, no stage label. A stalled scene poll may propose one automatic paid regeneration. Prod +215/-3, non-prod +324/-0. Head `21044bf8ffcb`, last updated Nov 16, 10:14 AM PT. Waiting on Jeffrey's billing decision. No merge without it.
- [PR #11651](https://github.com/jleechanorg/worldarchitect.ai/pull/11651): **OPEN**, not draft, `MERGEABLE`, stage 2 (`stage:2-evidence`). Smaller legacy scene and portrait assets on delivery (web + small portrait slots). Prod +307/-40, non-prod +807/-10. Head `38f711404b8d`, updated today 4:48 PM PT.
- [PR #11373](https://github.com/jleechanorg/worldarchitect.ai/pull/11373): **OPEN**, not draft, `MERGEABLE`, no stage label (`backend`, `cost`). Hardcodes free opening scene images for canonical Dragon Knight. Prod +189/-8, non-prod +347/-0. Head `72e5438e52a6`, last updated Nov 14, 12:13 PM PT.
- [worldai_frontend PR #602](https://github.com/jleechanorg/worldai_frontend/pull/602): **OPEN**, not draft, **`CONFLICTING`**, no stage label on GitHub (the Nov 18 audit called this stage 4). Shared avatar-generation progress bar and slow-loading status. Prod +353/-32, non-prod +509/-0. Head `805a0f4944a9`, last updated Nov 12, 10:59 AM PT.

No merge-order advice of the form “land A then rebase B” is active among these open PRs. Merged PRs above are already on `main`; rebase any conflicting open branch onto current `main` rather than trying to land a already-merged dependency.

## Learnings pointer

- [learnings-2026-11.md](learnings-2026-11.md) — section `2026-11-18 — Cold static-review seats WITHHOLD on large files within 600s`. One-line: seats reviewing #11233 at `7d0f14d7dd49` withheld for coverage because files such as `agent_prompts.py` could not be fully read before the deadline; use changed-region packets and `knowledgeWork` subagents for truly cold seats.

## Roadmap pointer

- Created [activity/2026-11-18.md](activity/2026-11-18.md) and prepended a date link under `## Recent activity (by day)` in [README.md](README.md) (that heading did not exist yet; the existing 2026-10-31 bullet was kept under it).
- Independent summary: this file, `nextsteps-2026-11-18.md` (no prior `nextsteps-*.md` existed in this repo; the last related doc was [2026-10-31-npc-portraits-stack-handoff.md](2026-10-31-npc-portraits-stack-handoff.md), left unchanged as a historical record).
