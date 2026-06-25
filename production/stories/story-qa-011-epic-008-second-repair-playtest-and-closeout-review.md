---
title: STORY-QA-011 EPIC-008 Second Repair Playtest and Closeout Review
type: story
status: done
phase: production
owner: shared
created: 2026-06-25
updated: 2026-06-25
source_lore: [greenland, qxz-meridian, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity,
    production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan,
    production/stories/story-army-006-map-camera-recruitment-and-tactical-stack-interaction-repair,
    production/stories/story-qa-010-epic-008-repair-playtest-and-closeout-review,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/faction-unit-rosters,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: recorded
---

# STORY-QA-011 EPIC-008 Second Repair Playtest and Closeout Review

## Status

DONE / one narrow follow-up. Human playtest after `STORY-ARMY-006` + PR #76 reported: `The pan is now not working at all. Otherwise, it seems to look better.` Closeout remains blocked by strategic-map pan input; `STORY-ARMY-007` is drafted as the narrow repair candidate.

## Story type

QA / Human Playtest / Closeout Decision.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As project director, I need to replay the repaired camera/recruitment/tactical-drone loop and decide whether EPIC-008 can close, needs one final narrow repair, or remains too unclear to judge.

## Source requirements

- `STORY-ARMY-006` merged in Unity PR #74 with post-merge CI success.
- Unity README current-task pointer cleanup merged in PR #75 with post-merge CI success.
- Tactical selection/AP follow-up fix merged in Unity PR #76 with post-merge CI success.
- Human QA-010 blockers that ARMY-006 was meant to repair:
  - pan/zoom reset after button clicks;
  - recruitment appears available after it stops changing drone count;
  - tactical drones cannot be selected, moved, or utilized;
  - stack info is not shown on tactical click;
  - follow-up review risk: selecting tactical stacks must not refresh spent AP or bypass turn/activation limits.

## In scope

- Human playtest instructions for current Unity `main` after ARMY-006.
- Review of the exact repaired surfaces:
  - strategic pan/zoom persistence after UI button clicks;
  - recruitment consumed/unavailable truthfulness or repeatable real count increase;
  - recruited drone visibility in tactical combat;
  - tactical drone selection;
  - tactical selected-stack detail/status display on click;
  - tactical drone movement or currently approved actionability;
  - tactical stack re-selection does not refresh spent AP or grant extra actionability.
- Re-check the broader EPIC-008 proof:
  - army state is understandable;
  - recruitment changes composition clearly;
  - composition can be inspected in tactical combat;
  - unit/stack roles are understandable enough to judge whether composition matters.
- Closeout verdict with one of:
  - `CLOSE EPIC-008`;
  - `ONE NARROW FOLLOW-UP`;
  - `REJECT CLOSEOUT`.
- If a follow-up is needed, identify exactly one dominant blocker category and preserve the human complaint text.
- If EPIC-008 closes, choose the next implementation direction only as a human decision; do not promote a new implementation story automatically.

## Out of scope

- No Unity runtime, test, scene, prefab, asset, package, or ProjectSettings changes.
- No new recruitment economy, town/dwelling system, unit upgrades, balance pass, tactical AI expansion, Champion progression, Intel upgrades, or realistic strategic-map replacement.
- No next-epic implementation story promotion without explicit human approval.

## Playtest protocol

1. Pull latest `main` in both repos.
2. Open Unity and play the current strategic map loop.
3. Pan and zoom the strategic map away from default.
4. Click/select story-scoped UI buttons: Champion, route/node, recruitment site, recruitment action, tactical entry/interact where available.
5. Confirm pan/zoom persists unless using an explicit focus/zoom control.
6. Recruit drones and check whether the UI is truthful:
   - repeat use actually increases the relevant stack count; or
   - the offer becomes visibly consumed/unavailable after use.
7. Enter tactical combat after recruitment.
8. Confirm the recruited drone stack appears.
9. Click/select the drone stack and confirm stack info/details/status appear.
10. Move or otherwise use the drone stack where current tactical rules allow.
11. Re-click/reselect the same drone stack after movement/use and confirm it does not regain spent AP or extra movement/action.
12. Judge whether army composition is now understandable enough to evaluate gameplay choices.

## Decision questions

1. EPIC-008 verdict:
   - A. Close EPIC-008 now.
   - B. One narrow follow-up before closing.
   - C. Reject closeout; the loop is still too unclear to judge.
2. If B or C, choose the single dominant blocker:
   - A. Strategic camera / map focus still unstable.
   - B. Recruitment availability/result is still misleading.
   - C. Tactical drone selection/details/actionability still fails.
   - D. Broader army composition readability is still insufficient.
   - E. Composition consequences are still not visible enough.
3. If A, choose next direction for a later story packet:
   - A. Champion Assets / Operations deeper identity layer.
   - B. Intel / upgrades.
   - C. Deeper tactical systems.
   - D. Strategic economy / bases / realistic-map direction.

## Acceptance criteria

- [x] Human playtest notes explicitly address the ARMY-006 repaired surfaces.
- [x] Verdict is recorded as `ONE NARROW FOLLOW-UP`.
- [x] If any blocker remains, the blocker is narrowed to one next story candidate rather than a broad polish bucket.
- [x] No next implementation story is promoted to READY without explicit human approval.

## Verification requirements

- Human playtest notes required.
- Unity CI evidence is inherited from ARMY-006 and pointer cleanup; no new Unity code evidence is required unless this story is later converted into a Codex QA-review task.
- Design-control updates required after the human verdict.

## Ambiguity Check

Status: PASS for READY-candidate.

Open human decision:

- Approve this QA/playtest closeout packet as the next step, or give direct playtest verdict in chat and skip a formal Codex QA story.

## Branch / PR requirements

- No Unity branch is authorized by this story as written.
- If later promoted to a Codex QA-review packet, branch name should be `story/STORY-QA-011-epic-008-second-repair-playtest-closeout-review` and runtime changes remain out of scope.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact source authority is linked.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check status is PASS for candidate.
- [ ] Human approval recorded.

## Verdict

DONE / ONE NARROW FOLLOW-UP. Strategic pan input is now the sole reported closeout blocker; `STORY-ARMY-007` is READY-candidate / approval pending.


## Human playtest result — 2026-06-25

Verdict: `ONE NARROW FOLLOW-UP`.

Human note:

> The pan is now not working at all. Otherwise, it seems to look better.

Decision:

- Do not close EPIC-008 yet.
- Treat strategic-map pan input as a hard closeout blocker.
- Draft one narrow repair candidate: `STORY-ARMY-007 Strategic Map Pan Input Repair`.
- Preserve the positive signal that the rest of ARMY-006 appears better; do not broaden the follow-up into recruitment or tactical changes unless new evidence appears.
