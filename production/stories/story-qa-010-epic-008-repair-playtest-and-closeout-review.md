---
title: STORY-QA-010 EPIC-008 Repair Playtest and Closeout Review
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-25
updated: 2026-06-25
source_lore: [greenland, qxz-meridian, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity,
    production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan,
    production/stories/story-army-005-army-recruitment-and-map-readability-repair,
    production/stories/story-qa-009-epic-008-playtest-and-closeout-review,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/faction-unit-rosters,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-QA-010 EPIC-008 Repair Playtest and Closeout Review

## Status

READY-candidate / approval pending. This is the proposed next story after `STORY-ARMY-005` merged. It is not a Unity runtime implementation task until explicitly approved.

## Story type

QA / Human Playtest / Closeout Decision.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As project director, I need to replay the repaired army/recruitment/tactical-role loop and decide whether EPIC-008 can close, needs one more narrow repair, or remains too unclear to judge.

## Source requirements

- `STORY-ARMY-005` merged in Unity PR #72 with post-merge CI success.
- Human playtest rejection that drove ARMY-005: army visibility, recruitment clarity, tactical role visibility, map panning/focus, and top-objective contrast.
- EPIC-008 capability goal: recruitment and army composition must be understandable enough to judge whether composition matters.

## In scope

- Human playtest instructions for the current Unity `main` build after ARMY-005.
- Review of the exact repaired surfaces:
  - selected-Champion bottom hero bar;
  - unit names/counts/role hints in army slots;
  - recruitment preview/result copy;
  - changed army after recruitment;
  - tactical compact labels and selected-stack details/status;
  - strategic map panning/focus and objective contrast.
- Closeout verdict with one of:
  - `CLOSE EPIC-008`;
  - `ONE NARROW FOLLOW-UP`;
  - `REJECT CLOSEOUT`.
- If a follow-up is needed, identify exactly one blocker category and preserve the human complaint text.
- If EPIC-008 closes, choose the next implementation direction only as a human decision; do not promote a new implementation story automatically.

## Out of scope

- No Unity runtime, test, scene, prefab, asset, package, or ProjectSettings changes.
- No realistic strategic-map replacement implementation.
- No new recruitment economy, town/dwelling system, unit upgrades, balance pass, tactical AI expansion, or Champion progression system.
- No next-epic implementation story promotion without explicit human approval.

## Playtest protocol

1. Update local repos:
   - pull latest `main` in `neon-champions-game-design`;
   - pull latest `main` in `neon-champions-unity`.
2. Open Unity and play the current strategic map loop as a player.
3. Select the active Champion and inspect the bottom hero bar.
4. Move to a recruitment source, inspect the preview, and recruit.
5. Confirm the result explains the exact unit/count and that the hero bar reflects the changed army.
6. Pan/focus the strategic map and check whether objective/HUD text remains readable.
7. Enter tactical combat with the changed army.
8. Inspect always-visible stack labels and selected-stack detail/status text.
9. Try to judge whether army composition is now understandable enough to evaluate gameplay choices.

## Decision questions

1. EPIC-008 verdict:
   - A. Close EPIC-008 now.
   - B. One narrow follow-up before closing.
   - C. Reject closeout; the loop is still too unclear to judge.
2. If B or C, choose the single dominant blocker:
   - A. Strategic map / objective / panning clarity.
   - B. Hero bar / army composition clarity.
   - C. Recruitment / dwelling clarity.
   - D. Tactical stack role/status clarity.
   - E. Composition consequences are still not visible enough.
3. If A, choose next direction for a later story packet:
   - A. Champion Assets / Operations deeper identity layer.
   - B. Intel / upgrades.
   - C. Deeper tactical systems.
   - D. Strategic economy / bases / realistic-map direction.

## Acceptance criteria

- [ ] Human playtest notes explicitly address the ARMY-005 repaired surfaces.
- [ ] Verdict is recorded as `CLOSE EPIC-008`, `ONE NARROW FOLLOW-UP`, or `REJECT CLOSEOUT`.
- [ ] If any blocker remains, the blocker is narrowed to one next story candidate rather than a broad polish bucket.
- [ ] No next implementation story is promoted to READY without explicit human approval.

## Verification requirements

- Human playtest notes required.
- Unity CI evidence is inherited from ARMY-005 and pointer cleanup; no new Unity code evidence is required unless this story is later converted into a Codex QA-review task.
- Design-control updates required after the human verdict.

## Ambiguity Check

Status: PASS for READY-candidate.

Open human decision:

- Approve this QA/playtest closeout packet as the next step, or give direct playtest verdict in chat and skip a formal Codex QA story.

## Branch / PR requirements

- No Unity branch is authorized by this story as written.
- If later promoted to a Codex QA-review packet, branch name should be `story/STORY-QA-010-epic-008-repair-playtest-closeout-review` and runtime changes remain out of scope.

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

READY-candidate / approval pending. Recommended next step is human playtest using this protocol before choosing any new implementation direction.
