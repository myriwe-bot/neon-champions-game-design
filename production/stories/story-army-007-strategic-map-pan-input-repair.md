---
title: STORY-ARMY-007 Strategic Map Pan Input Repair
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
    production/stories/story-qa-011-epic-008-second-repair-playtest-and-closeout-review,
    production/stories/story-army-006-map-camera-recruitment-and-tactical-stack-interaction-repair,
    design/gdd/strategic-map,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-ARMY-007 Strategic Map Pan Input Repair

## Status

DONE / merged. Unity PR #77 merged as `14f1312198958b971d24582302a0ac38d7cef6ae`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28191824791. Unity current-task pointer cleanup PR #78 merged as `f92ed63c0a8ae61bfbf685aa121b4cd0d15846ec`; post-cleanup main CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28192659752.

Human approval recorded 2026-06-25: `Approved` in response to the `STORY-ARMY-007` recommendation. Human playtest note recorded 2026-06-25 after ARMY-006 + PR #76: `The pan is now not working at all. Otherwise, it seems to look better.`

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

- [x] On the strategic view, the player can pan the map from the default camera position using the supported player-facing input path.
- [x] If keyboard pan is supported, WASD and/or arrow keys move the camera visibly within bounds.
- [x] If pointer drag pan is supported, dragging on non-UI strategic map space moves the camera visibly within bounds.
- [x] Dragging/panning does not also select a Champion/site/route/node by accident.
- [x] Panning is clamped to existing map bounds and cannot lose the playable map.
- [x] Panning is disabled or ignored while tactical view is active.
- [x] After panning and/or zooming, clicking/selecting story-scoped UI buttons does not reset camera position/zoom.
- [x] Existing recruitment truthfulness and tactical drone select/detail/actionability tests remain green.
- [x] Evidence includes before/after notes or screenshot/GIF/video proving pan works in the current player-facing build.

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

- Resolved 2026-06-25: approved as the narrow pan-input repair packet. Default pan affordances stand: keyboard pan must work; pointer drag may be added if needed for player-facing pan discoverability.

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
- [x] Human approval recorded.

## Verdict

DONE / merged. This was the final EPIC-008 closeout repair and no current Unity implementation packet remains active.


## Implementation result — 2026-06-25

- Unity PR #77: https://github.com/myriwe-bot/neon-champions-unity/pull/77
- Reviewed head: `384059151996050fe9e316fd83edb64ae19faf31`
- Merge commit: `14f1312198958b971d24582302a0ac38d7cef6ae`
- Exact-head PR CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28191077507
- Post-merge main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28191824791
- Unity current-task pointer cleanup PR #78: https://github.com/myriwe-bot/neon-champions-unity/pull/78
- Pointer cleanup merge commit: `f92ed63c0a8ae61bfbf685aa121b4cd0d15846ec`
- Pointer cleanup post-merge main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28192659752

Closeout decision: EPIC-008 can close. The final reported blocker, strategic-map pan input, has a narrow repair, evidence, exact-head CI, and post-merge main CI.
