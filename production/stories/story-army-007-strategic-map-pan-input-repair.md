---
title: STORY-ARMY-007 Strategic Map Pan Input Repair
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
    production/stories/story-qa-011-epic-008-second-repair-playtest-and-closeout-review,
    production/stories/story-army-006-map-camera-recruitment-and-tactical-stack-interaction-repair,
    design/gdd/strategic-map,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-ARMY-007 Strategic Map Pan Input Repair

## Status

READY-candidate / approval pending. Human playtest note recorded 2026-06-25 after ARMY-006 + PR #76: `The pan is now not working at all. Otherwise, it seems to look better.`

This is the proposed single narrow follow-up before EPIC-008 closeout can be reconsidered.

## Story type

Unity bugfix / input repair / playability repair.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As a player, I need strategic-map panning to work reliably so the repaired recruitment and tactical-drone loop can be evaluated without losing map control. If panning is dead, EPIC-008 still cannot close even if the army/recruitment/tactical surfaces look better.

## Human playtest authority

Human note, 2026-06-25:

> The pan is now not working at all. Otherwise, it seems to look better.

## Problem statement

ARMY-006 fixed camera-state persistence across UI refreshes, but the current playable build now fails the more basic player-facing requirement: strategic-map panning itself does not work. The repair must restore actual player pan input and preserve the ARMY-006 guarantee that pan/zoom state does not reset after ordinary UI button clicks.

## In scope

- Restore player-facing strategic-map pan input on the strategic view.
- Support the intended prototype pan affordance explicitly:
  - keyboard/WASD or arrow-key pan must work when the strategic view is active;
  - mouse/touch drag pan should work if that was the only natural/player-discoverable pan route available in the current scene, or if keyboard-only panning proves insufficient for the player-facing complaint.
- Ensure pan input does not fire while tactical view is active.
- Ensure pan input does not accidentally trigger strategic object selection/clicks while dragging.
- Preserve ARMY-006 camera persistence: after a successful pan and/or zoom, story-scoped UI button clicks must not reset camera position/zoom.
- Add or repair automated coverage for actual input-driven pan, not only direct `PanStrategicMap(...)` method calls, where feasible in Unity PlayMode/InputSystem tests.
- Capture evidence under Unity `production/evidence/STORY-ARMY-007/` proving pan works and remains persistent after UI interactions.

## Out of scope

- No final map replacement or realistic map implementation.
- No broad camera framework rewrite unless strictly necessary for this narrow input bug.
- No changes to recruitment rules, tactical stack rules, tactical AI, balance, unit rosters, Champion progression, Intel upgrades, assets, packages, or ProjectSettings.
- No new zoom feature beyond preserving existing zoom behavior.
- No redesign of the HUD layout except minimal changes required to stop UI from swallowing intended pan input.

## Acceptance criteria

- [ ] On the strategic view, the player can pan the map from the default camera position using the supported player-facing input path.
- [ ] If keyboard pan is supported, WASD and/or arrow keys move the camera visibly within bounds.
- [ ] If pointer drag pan is supported, dragging on non-UI strategic map space moves the camera visibly within bounds.
- [ ] Dragging/panning does not also select a Champion/site/route/node by accident.
- [ ] Panning is clamped to existing map bounds and cannot lose the playable map.
- [ ] Panning is disabled or ignored while tactical view is active.
- [ ] After panning and/or zooming, clicking/selecting story-scoped UI buttons does not reset camera position/zoom.
- [ ] Existing recruitment truthfulness and tactical drone select/detail/actionability tests remain green.
- [ ] Evidence includes before/after notes or screenshot/GIF/video proving pan works in the current player-facing build.

## Verification requirements

Required unless a blocker is documented in the PR evidence:

- PlayMode or integration coverage for input-driven pan, preferably simulating the real InputSystem path rather than only calling `PanStrategicMap(...)` directly.
- Regression coverage that pan/zoom persistence across UI refreshes still passes.
- Regression coverage or explicit smoke evidence that tactical view does not accept strategic pan input.
- Manual or automated visual evidence in `production/evidence/STORY-ARMY-007/`.
- Unity Foundation CI must pass on exact PR head before merge and on `main` after merge.

## Ambiguity Check

Status: PASS for READY-candidate.

Approved defaults for human review:

- Treat `pan is now not working at all` as a hard closeout blocker.
- Keep the repair pan-only unless a tiny input gating fix is required to prevent drag from selecting map objects.
- Do not broaden into map readability, layout polish, recruitment, or tactical changes.

Open human decision:

- Approve this narrow pan-input repair packet, or provide a different intended pan affordance if keyboard/drag defaults are wrong.

## Branch / PR requirements

Use branch:

- `story/STORY-ARMY-007-strategic-map-pan-input-repair`

PR must include:

- story link;
- exact head SHA;
- evidence path;
- CI run URLs;
- explicit supported pan input path(s);
- explicit omissions/deferred work.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact human playtest authority is preserved.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check status is PASS for candidate.
- [ ] Human approval recorded.

## Verdict

READY-candidate / approval pending. Recommended as the next and only implementation repair before another EPIC-008 closeout attempt.
