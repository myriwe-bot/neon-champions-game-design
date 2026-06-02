---
title: STORY-STRAT-UI-001 Minimal Hotseat HUD
type: story
status: in-review
phase: production
owner: shared
created: 2026-06-02
updated: 2026-06-02
source_lore: []
related: [design/gdd/strategic-map, docs/architecture/unity-technical-scheme, docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, production/epics/epic-strat-mvp-001-strategic-mvp-core-loop, production/stories/story-strat-001-scenario-map-graph-state, production/stories/story-strat-002-hotseat-turn-ownership, production/stories/story-strat-003-champion-route-movement, production/stories/story-strat-vis-001-minimal-strategic-map-presentation, production/stories/story-strat-input-001-select-champion-and-route-move]
approval: pending
---

# Story: STORY-STRAT-UI-001 Minimal Hotseat HUD

## Status

READY-candidate. Requires explicit human approval before Codex implementation.

## Story type

UI + Integration.

Primary layer: minimal Unity HUD adapter for hotseat turn state and selected Champion movement state.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## User/player/system value

As a local hotseat player, I want a crude HUD that tells me whose turn it is, what my selected Champion can still do, and lets me end the turn, so that the early strategic loop can be played without developer guidance.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §2 Approved MVP Direction, rules 1-8.
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 2-4 and 9-10.
  - `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft, especially active faction/controller, active Champion, reachable sites, resource stockpiles if available, whose turn is next.
  - `design/gdd/strategic-map.md` §13 Turn/Scenario/Victory Structure, start/end faction turn behavior used by STORY-STRAT-002.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` §Project Layout Standard and §Assembly Boundary Standard.
  - `docs/architecture/control-manifest.md` §§1, 2, 3, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — UI/integration and PlayMode/smoke evidence requirements.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - Minimal usability/readability only. No final UI skin, lore text, localization, or art direction.

## In scope

- Add a crude HUD to the minimal strategic-map scene showing:
  - active faction ID/display key;
  - current turn number and round number;
  - next faction if available;
  - selected Champion ID/display key and remaining movement points if selected;
  - visible diagnostic/status line for rejected or successful basic actions.
- Add an End Turn button/control that calls STORY-STRAT-002's approved turn service.
- After End Turn:
  - active faction changes;
  - turn/round display updates;
  - active faction Champion movement/action state resets according to domain rules;
  - selected Champion state is cleared or updated in a documented way.
- Add PlayMode tests where feasible for HUD initialization, End Turn state update, and selected Champion movement-point display update.
- Keep UI as a thin adapter; domain/application services own rules.

## Out of scope

- Full resource panel, site interaction panel, battle preview panel, victory screen, options menu, remapping, accessibility polish, localization implementation, final UI art, animation, audio, or UI framework overhaul.
- Movement implementation beyond reflecting existing movement state from STORY-STRAT-003.
- Site rewards, recruitment, tactical transition, battle result display, or victory evaluation.
- Strategic AI, save/load, networking, or final data-authoring pipeline.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder labels/buttons using raw IDs or display keys.
- Simple debug/status line.
- Minimal Canvas/UI Toolkit implementation consistent with existing Unity repo conventions.

Not allowed:

- UI code that directly changes turn/movement state without approved domain/application services.
- New economy, reward, site, or victory behavior.
- Final player-facing copy/lore decisions.

## Dependencies

- Required prior stories:
  - STORY-STRAT-001 scenario/map graph state.
  - STORY-STRAT-002 hotseat turn ownership.
  - STORY-STRAT-003 champion route movement.
  - STORY-STRAT-VIS-001 minimal strategic-map presentation.
  - STORY-STRAT-INPUT-001 select Champion and route move is recommended before implementation, but HUD can be implemented earlier if selected-Champion state is handled as N/A or test-selected.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required Unity/package setup:
  - Existing Unity UI approach. If no UI approach is established, use the smallest built-in approach already available; stop before adding packages or changing project settings.

## Acceptance criteria

- [ ] Given the minimal strategic-map scene starts, when the HUD initializes, then it displays the active faction, turn number, round number, and next faction if available.
- [ ] Given a Champion is selected, when the HUD refreshes, then it displays the selected Champion and remaining movement points.
- [ ] Given movement succeeds through STORY-STRAT-INPUT-001, when the HUD refreshes, then remaining movement points update to match domain state.
- [ ] Given the player presses End Turn, when the turn service applies end-turn behavior, then active faction, turn number, and round number update according to STORY-STRAT-002.
- [ ] Given End Turn wraps from the last faction to the first faction, when the HUD refreshes, then round number increments visibly.
- [ ] Given a rejected action occurs, when the HUD/status line refreshes, then a crude diagnostic is visible without requiring console inspection.
- [ ] UI/presentation code compiles without adding UnityEngine/UI dependencies to domain code.
- [ ] PlayMode/smoke evidence covers HUD startup and End Turn update, or documents a human-approved automation exception.

## Verification requirements

- Unit tests: N/A unless pure HUD formatting/presenter helpers are added.
- Unity edit-mode tests: Required for pure presenter/formatting helpers if added.
- Unity play-mode tests: Required where feasible for HUD startup and End Turn update.
- Manual Unity scene/prefab checks: Required.
- Screenshot/video evidence: Required, showing HUD before and after End Turn.
- Performance budget or N/A: N/A for minimal static HUD.
- CI evidence: Required on implementation PR.
- Playtest evidence: Optional before STORY-LOOP-001; not required here.
- TDD evidence required? Yes for helper/application behavior; PlayMode/manual evidence for UI wiring.
- Automation deferred? Only with documented Unity UI automation limitation and manual protocol.

## Ambiguity Check

Status: PASS.

Open questions:
- None for crude hotseat HUD.

Assumptions:
- Early loop readability is more important than UI polish.
- Raw IDs/display keys are acceptable placeholders until localization/content stories exist.

Out of scope:
- Same as story Out of scope section.

## Codex implementation notes

- Branch suggestion: `story/strat-ui-001-minimal-hotseat-hud`.
- Stop if the task requires final UI architecture, asset/style decisions, localization framework, or new gameplay rules.
