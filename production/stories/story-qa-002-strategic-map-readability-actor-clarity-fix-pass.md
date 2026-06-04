---
title: STORY-QA-002 Strategic Map Readability and Actor-Clarity Fix Pass
type: story
status: approved
phase: production
owner: shared
created: 2026-06-03
updated: 2026-06-03
source_lore: []
related:
  [
    design/gdd/strategic-map,
    docs/architecture/unity-technical-scheme,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke,
    production/stories/story-qa-001-strategic-smoke-cleanup-readability-bugfix-pass,
    production/stories/story-tac-001-battle-setup-result-dto-contracts,
  ]
approval: approved
---

# Story: STORY-QA-002 Strategic Map Readability and Actor-Clarity Fix Pass

## Status

DONE. Human approval recorded on 2026-06-03. Implemented in Unity PR #12 and merged on 2026-06-04.

This packet was drafted in response to human feedback after TAC-001 merge that the current strategic smoke remains too crumpled and hard to read: buttons overlap, screen elements crowd together, and it is unclear who is acting or what is happening on the map.

## Story type

QA + UI/UX Readability + Bugfix + Visual/Feel regression.

Primary layer: second cleanup pass over the existing crude strategic-map smoke loop after STORY-LOOP-001, STORY-QA-001, and STORY-TAC-001.

## Estimate

- Size: M.
- Basis: focused layout/readability/action-feedback improvements over existing placeholder presentation and tests; includes baseline capture, automated layout/PlayMode regression checks, and before/after screenshot evidence.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## User/player/system value

As a human tester of the earliest local-hotseat strategic loop, I need the screen to be readable at a glance, with non-overlapping controls, obvious acting-side/Champion state, and clear map feedback after each action, so that I can understand and evaluate the strategic loop instead of fighting the placeholder UI.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §2 Approved MVP Direction, rules 1-8.
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, especially steps 1-4 and 9-10 for current smoke-loop behavior.
  - `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft, especially active faction/controller, active Champion, movement/reachable sites, whose turn is next, and status feedback.
  - `design/gdd/strategic-map.md` §9 Strategic Map Topology and §12 Champion/Army Strategic State and Movement Allowance as already implemented by prior strategic stories.
  - `design/gdd/strategic-map.md` §14 Strategy-to-Tactical DTOs is background only; QA-002 must not implement site-to-battle flow, tactical combat, or result application.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` §Core Technical Principle, §Project Layout Standard, and §Assembly Boundary Standard.
  - `docs/architecture/control-manifest.md` §§1, 2, 3, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — QA, PlayMode/smoke, screenshot evidence, and regression requirements.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - Placeholder readability only. Raw IDs/display keys are acceptable where useful for evidence/debugging.
  - No final art, final lore text, final names, localization framework, UI Toolkit/Canvas migration, or final UI architecture.

## Problem statement / observed issues

The current strategic smoke is technically further along but still fails the basic player-readability test:

- buttons/controls can overlay each other or sit too close to labels;
- the screen feels crumpled together, with HUD, controls, status, map markers, and labels competing for the same space;
- it is unclear who is acting now;
- it is unclear whether the selected Champion is the acting Champion or merely selected;
- it is unclear what changed on the map after selecting, moving, attempting an invalid action, or pressing End Turn;
- map labels, route indicators, Champion markers, reachable hints, and status text need a clearer visual hierarchy;
- deferred systems should remain obvious as unavailable so players do not mistake missing site/battle behavior for broken interaction.

## In scope

### Baseline / audit

- Start from current Unity `main` after TAC-001 merge.
- Capture current baseline evidence before changing layout.
- Audit the existing strategic smoke scene and presentation code for:
  - overlapping labels/buttons;
  - unreadable spacing/scale/contrast;
  - ambiguous active/selected/acting state;
  - ambiguous map feedback after player actions;
  - screenshot/evidence gaps.

### Layout and hierarchy fixes

- Prevent visible overlap among:
  - active actor banner/HUD;
  - turn/round/next-faction labels;
  - End Turn button/control;
  - selected Champion row;
  - status/action-feedback row;
  - deferred-systems note;
  - map node labels;
  - Champion markers;
  - reachable-route/node indicators.
- Separate the screen into crude but explicit placeholder zones:
  - top actor/turn information;
  - distinct End Turn control area;
  - central map area;
  - selected Champion / reachable-action information;
  - bottom status/action-feedback area;
  - deferred-systems note if needed.
- Adjust placeholder text size, position, contrast, or map framing only where it directly improves readability.
- A small named `StrategicMapPlaceholderLayout` expansion/helper is allowed if it keeps the layout testable and does not become a final UI framework.

### Actor clarity

- Make the currently acting side obvious at all times:
  - active faction ID/display key;
  - active controller;
  - active Champion ID/display key;
  - current turn/round;
  - next faction or next actor if already available from current data.
- Make selected Champion distinct from acting Champion:
  - if selected == acting, show that clearly;
  - if selection is absent/invalid/inactive, avoid implying the inactive Champion can act.
- Make active/inactive Champion map markers visually different using placeholder shapes/colors/halos/labels.

### Map and action feedback

- Selection feedback:
  - selected Champion marker/ring/label is visible;
  - reachable route/node indicators appear without hiding map topology.
- Valid movement feedback:
  - marker moves to the new node;
  - HUD/status agrees on Champion, node, and remaining movement;
  - action status states the route/node change in compact placeholder form.
- Invalid action feedback:
  - marker does not move;
  - status message is readable and compact;
  - map/HUD do not falsely imply success.
- End Turn feedback:
  - active actor banner updates;
  - selected/acting state is coherent after faction switch;
  - status text explicitly says turn advanced/passed;
  - round increment is clear when turn order wraps.
- Deferred-system feedback:
  - site/battle/reward/victory systems remain visibly unavailable or out-of-scope in smoke, without suggesting a broken clickable site.

### Regression tests and evidence

- Add automated EditMode tests for objective layout invariants where feasible.
- Add PlayMode tests for actor-state/map-feedback invariants where feasible.
- Capture before/after screenshots under a story-specific evidence directory.
- Fill evidence README with:
  - user-observed issues;
  - baseline screenshots;
  - fixes made;
  - tests/checks run;
  - after screenshots;
  - remaining known issues/follow-up candidates.

## Out of scope

- Final UI framework, UI Toolkit migration, Canvas architecture migration, final UI art, animation, audio, VFX, localization, accessibility pass beyond minimum readability, or new packages.
- New gameplay mechanics or content:
  - site interaction;
  - guarded battle trigger;
  - tactical combat;
  - battle result application;
  - rewards;
  - recruitment;
  - resources/economy;
  - victory/loss;
  - strategic AI;
  - save/load;
  - networking.
- Expanding map content, balance/tuning, lore, names, final copy, or scenario design.
- Large scene/prefab architecture refactor unless a blocking bug proves it is unavoidable; if so, stop and request separate approval.
- Changing package manifests, project settings, input-system architecture, camera stack, or render pipeline unless explicitly approved in the PR as an unavoidable bugfix.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Raw IDs/display keys such as `faction_1`, `champion_1`, `node_start_a`.
- Primitive shapes, TextMesh labels, simple lines, simple colors, rings/halos, debug panels, and placeholder status text.
- Existing smoke scenario data and prior story application/domain services.
- Screenshot evidence generated from the current placeholder smoke scene.

Not allowed:

- Fake evidence by bypassing domain/application services.
- Presentation code directly mutating canonical gameplay state.
- Hidden implementation of deferred systems.
- New final UI/lore/content decisions.
- Pixel-perfect brittle screenshot assertions as the only regression mechanism.

## Dependencies

- Required prior implementation:
  - STORY-LOOP-001 merged to Unity `main` in PR #9.
  - STORY-QA-001 merged to Unity `main` in PR #10.
  - STORY-TAC-001 merged to Unity `main` in PR #11.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required evidence patterns:
  - Existing Unity `production/evidence/STORY-QA-001/` conventions.
  - Existing PlayMode screenshot/evidence capture conventions.
- Required local source reading at implementation time:
  - Unity repo root `AGENTS.md` and scoped `AGENTS.md` under touched paths.

## Acceptance criteria

- [ ] Given the strategic smoke scene starts at the target evidence/default test resolution, when viewed without console logs, then top HUD, active actor display, End Turn control, selected Champion row, status row, deferred-system note, map markers, node labels, route labels/lines, and reachable indicators do not visibly overlap.
- [ ] Given the scene starts, when a human looks at the screen for a few seconds, then it is clear which faction/controller and Champion are acting now.
- [ ] Given no Champion is selected or selection changes, when the screen refreshes, then selected Champion state is visibly separate from active/acting Champion state and does not imply the wrong Champion can act.
- [ ] Given the active Champion is selected, when reachable movement is available, then the selected Champion and reachable route/node are visually distinguishable from inactive/non-reachable elements without hiding the route network.
- [ ] Given a valid move is applied, when the scene refreshes, then the Champion marker, HUD, and status text all agree on the Champion's new node and remaining movement.
- [ ] Given an invalid move/action occurs, when the scene refreshes, then the status feedback is readable, the Champion marker remains at the previous valid node, and the HUD/map do not falsely imply success.
- [ ] Given End Turn is pressed, when the next faction becomes active, then active actor, turn/round, next faction, selected Champion state, and status feedback update coherently.
- [ ] Given both factions advance through one local-hotseat round, when turn order wraps, then the round increment is visible and does not overlap with other HUD/status elements.
- [ ] Given site/battle/reward/victory systems remain deferred, when the smoke is run, then the UI/status clearly does not imply those systems are currently available.
- [ ] Automated EditMode regression coverage exists for objective layout/spacing invariants where feasible.
- [ ] Automated PlayMode/smoke coverage exists for actor clarity and action-feedback invariants where feasible.
- [ ] Screenshot evidence includes before-cleanup baseline and after-cleanup states for initial, selected/reachable, valid move, invalid move, and after End Turn.
- [ ] PR evidence lists remaining known issues and confirms no new gameplay systems, final UI/art/content, packages, or architecture migration were added.

## Verification requirements

- Unit tests: N/A unless pure non-Unity helper logic is added.
- Unity EditMode tests: Required for new/changed layout helper, formatter, or presentation-snapshot helper logic where feasible.
- Unity PlayMode tests: Required for objective smoke/layout/feedback regression checks where feasible.
- Manual Unity scene checks: Required.
- Screenshot/video evidence: Required.
- CI evidence: Required on implementation PR.
- Performance budget or N/A: N/A for crude MVP smoke; do not add expensive effects.
- TDD evidence required? Yes for bug fixes and helper/application logic; PlayMode/manual evidence acceptable for presentation-only visual placement.
- Automation deferred? Any manual-only gap requires explicit explanation in evidence and PR.

## Evidence package requirements

Evidence directory:

`production/evidence/STORY-QA-002/`

Required contents:

- `README.md` containing:
  - source story/GDD/ADR/control docs read;
  - baseline problems observed;
  - fixes made;
  - test/check commands and results;
  - screenshot inventory;
  - remaining known issues/follow-ups;
  - omissions/deferred systems.
- Baseline screenshots before cleanup, preferably under:
  - `production/evidence/STORY-QA-002/baseline-before-cleanup/`
- Generated after-cleanup screenshots, preferably under:
  - `production/evidence/STORY-QA-002/generated/`

Minimum screenshot set:

- baseline initial state from current `main` before changes;
- after cleanup: initial state;
- after cleanup: active Champion selected and reachable routes/nodes visible;
- after cleanup: valid move result;
- after cleanup: invalid move result;
- after cleanup: after End Turn / next faction active;
- after cleanup: round-wrap state if the PlayMode smoke reaches it cheaply.

## Implementation notes

Likely Unity files to inspect/touch, subject to current repo state and `AGENTS.md`:

- `Assets/NeonChampions/Runtime/Presentation/StrategicMapBootstrap.cs`
- `Assets/NeonChampions/Runtime/Presentation/StrategicMapPlaceholderLayout.cs`
- `Assets/NeonChampions/Runtime/Presentation/StrategicMapRenderedElement.cs`
- `Assets/NeonChampions/Runtime/Application/Strategic/StrategicMapPresentationSnapshot.cs`
- `Assets/NeonChampions/Runtime/Application/Strategic/StrategicMapInputSession.cs`
- `Assets/NeonChampions/Runtime/Application/Strategic/StrategicMapPresentationSmokeScenario.cs`
- `Assets/NeonChampions/Tests/EditMode/Strategic/StrategicMapPlaceholderLayoutTests.cs`
- `Assets/NeonChampions/Tests/EditMode/Strategic/StrategicMapPresentationSnapshotTests.cs`
- `Assets/NeonChampions/Tests/EditMode/Strategic/StrategicMapInputSessionTests.cs`
- `Assets/NeonChampions/Tests/PlayMode/PlayModeSmokeTests.cs`
- `production/evidence/STORY-QA-002/README.md`

Preferred implementation approach:

1. Capture baseline screenshots/evidence before changing layout.
2. Add failing layout/spacing/readability tests where objective invariants are measurable.
3. Replace ad-hoc crumpled positions with named placeholder layout zones.
4. Improve active actor banner and End Turn separation.
5. Improve selected vs acting Champion visual language.
6. Improve reachable/valid/invalid/end-turn map and status feedback.
7. Add screenshot capture and evidence README updates.
8. Run full story-required validation and CI.

## Branch / PR requirements

- Branch name: `story/qa-002-strategic-map-readability-actor-clarity`
- PR title: `STORY-QA-002 Strategic map readability and actor clarity fix pass`
- Required linked story ID: `STORY-QA-002`
- Required linked GDD/ADR/control docs: use the exact source references listed above.
- Required root/scoped AGENTS.md instructions: Unity repo root `AGENTS.md` and scoped source/test `AGENTS.md` under touched paths.
- Required evidence summary:
  - baseline issue list;
  - fixes made;
  - tests added/changed;
  - CI links/status;
  - before/after screenshots/video;
  - remaining known issues.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Codex implementation prompt

Prompt file prepared at:

`production/sprints/codex-story-qa-002.prompt.txt`

Codex may use it now that this story is approved.

## Ambiguity Check

Status: PASS.

Open questions:

- None blocking for a placeholder readability/actor-clarity pass.

Assumptions:

- The user wants this cleanup before deeper guarded-site/battle/result stories because current readability defects will hide future gameplay problems.
- Placeholder visual elements are acceptable if they become legible and testable.
- Final UI architecture remains deferred unless this pass proves placeholders cannot carry the smoke loop.

Out of scope:

- Same as story Out of scope section.

Allowed stubs/mocks/placeholders:

- Same as Allowed stubs section.

Human-approved exceptions:

- None.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/art/worldbuilding references are linked if relevant or explicitly N/A.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are either disallowed or explicitly listed.
- [x] Dependencies are listed.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Required automated tests/validators/PlayMode evidence are listed or N/A.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Estimate is recorded.
- [x] Human approval has been given or delegated gate approval is recorded.
  - Approved by human on 2026-06-03 in response to the READY-candidate packet.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests and CI pass or approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are documented.
- [ ] PR/code review is complete.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

APPROVED / READY. Gate blockers: none. Implement before guarded-site/battle/result stories unless the human explicitly defers this cleanup.
