---
title: STORY-ARMY-006 Map Camera, Recruitment, and Tactical Stack Interaction Repair
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
    production/stories/story-qa-010-epic-008-repair-playtest-and-closeout-review,
    production/stories/story-army-005-army-recruitment-and-map-readability-repair,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-ARMY-006 Map Camera, Recruitment, and Tactical Stack Interaction Repair

## Status

DONE / merged. Unity PR #74 merged as `50abc93aa88305c9a89f239de54668e9eb2b1147`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28184379301. Unity current-task pointer cleanup merged in PR #75 as `5a3692b5c445373eb5bd1ddf4371fe2029a273f0`; post-merge CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28185218400. Independent review found a tactical selection AP-refresh risk after merge; follow-up PR #76 merged as `682e574e014603a340a5b1281e1d3739229b3670`; post-merge CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28186926534.

## Story type

Unity bugfix / playability repair / UI interaction.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As a player, I need the repaired army/recruitment loop to preserve my map focus, make repeated recruitment availability truthful, and let recruited tactical stacks be selected, inspected, moved, and used. Without this, EPIC-008 still cannot prove that army composition matters.

## Human playtest authority

Human `STORY-QA-010` notes recorded 2026-06-25:

- "the pan resets to the default position after a button is clicked. It does not remember the location or the zoom. This should not happen."
- "the recruitment only increases drones once, even though the action seems to be available more times."
- "in the tactical view, the drones cannot be selected or moved or utilized at all."
- "Stack info is not shown on click in the tactical view."

## Problem statement

`STORY-ARMY-005` improved labels and summaries but the playable interaction loop still breaks in three places:

1. Strategic map camera state is volatile across UI button clicks.
2. Recruitment availability is misleading when a recruitment action appears usable after it can no longer change the army.
3. Tactical stack interaction does not support the recruited drone stack as a normal usable stack, and selected-stack details are absent on click.

## In scope

- Preserve strategic map pan and zoom state across story-scoped UI button interactions, including recruitment and tactical-entry/interact buttons when returning to the strategic view.
- Fix recruitment action availability/result truthfulness for the drone/recruitment path:
  - either repeated available actions must keep increasing the relevant stack according to the approved fixed-offer model;
  - or the action must visibly become unavailable/consumed once it can no longer change the army.
- Ensure recruited drone stacks in tactical view can be selected through the normal player-facing tactical input path.
- Ensure selected recruited drone stacks show stack details/status on click, matching the selected-stack detail intent from ARMY-005.
- Ensure recruited drone stacks can perform their currently approved tactical role/action path if they are player-controlled and actionable in the battle setup.
- Add/repair automated coverage where feasible for camera persistence, recruitment availability/result consistency, tactical stack selection/details, and drone actionability.
- Capture updated evidence under Unity `production/evidence/STORY-ARMY-006/`.

## Out of scope

- No new recruitment economy, costs, weekly growth, town/dwelling tree, or upgraded units.
- No final strategic map replacement or realistic map implementation.
- No new drone unit design beyond making the already-approved drone stack truthful, selectable, inspectable, and usable.
- No broad tactical AI expansion, balance pass, new faction roster, Champion progression, assets/operations, or Intel upgrade system.
- No generalized camera framework rewrite unless strictly necessary for the listed UI-state persistence bug.

## Acceptance criteria

- [x] After the player pans and/or zooms the strategic map, clicking story-scoped UI buttons does not reset the map to its default pan/zoom.
- [x] Recruitment UI cannot advertise a repeatable action that no longer changes the army.
- [x] If recruitment remains available more than once, each successful use visibly updates the exact relevant stack count, or the offer is consumed/disabled.
- [x] If recruitment is one-time/consumed, the UI makes that consumed/unavailable state visible and prevents misleading repeat activation.
- [x] A recruited drone stack appears in tactical combat when recruited before battle.
- [x] The recruited drone stack can be selected by the player in tactical view.
- [x] Clicking/selecting the recruited drone stack shows stack info/details/status.
- [x] The recruited drone stack can be moved or otherwise use its currently approved tactical role/action when action rules allow.
- [x] Evidence includes before/after notes or screenshots/GIF/video proving camera persistence, recruitment truthfulness, and tactical drone select/details/actionability.

## Verification requirements

Required unless a blocker is documented in the PR evidence:

- EditMode/domain tests for recruitment availability/result consistency if the behavior is domain-backed.
- PlayMode or integration tests for strategic camera pan/zoom persistence across UI button clicks.
- PlayMode or integration tests for tactical drone stack selection and selected-stack detail display.
- Manual or automated visual evidence in `production/evidence/STORY-ARMY-006/`.
- Unity Foundation CI must pass on exact PR head before merge and on `main` after merge.

## Ambiguity Check

Status: PASS.

Human approval recorded 2026-06-25. Approved defaults:

- The bug is not acceptable as-is: pan/zoom reset after ordinary UI button clicks should be fixed.
- Recruitment availability must be truthful. The implementation may choose the smallest story-scoped fix: repeatable-with-real-count-increase or consumed/disabled-after-use, whichever matches the existing fixed-offer model with least scope.
- Drones already present through the approved recruitment/composition path must be normal player-usable tactical stacks where current tactical rules allow.


## Branch / PR requirements

Use branch:

- `story/STORY-ARMY-006-map-camera-recruitment-tactical-stack-repair`

PR must include:

- story link;
- exact head SHA;
- evidence path;
- CI run URLs;
- explicit omissions/deferred work.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact human playtest authority is preserved.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check status is PASS.
- [x] Human approval recorded.

## Verdict

DONE / merged, including follow-up AP-selection fix PR #76. EPIC-008 now needs another human repair-playtest / closeout decision before any new implementation direction is promoted.
