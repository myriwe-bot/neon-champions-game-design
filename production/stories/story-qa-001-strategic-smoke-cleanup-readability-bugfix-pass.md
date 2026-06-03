---
title: STORY-QA-001 Strategic Smoke Cleanup, Readability, and Bugfix Pass
type: story
status: ready-candidate
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
  ]
approval: pending
---

# Story: STORY-QA-001 Strategic Smoke Cleanup, Readability, and Bugfix Pass

## Status

READY-candidate. Prepared after STORY-LOOP-001 merge because the first playable smoke exposed usability and clarity problems. Requires explicit human approval before Codex implementation.

## Story type

QA + UI/UX Readability + Bugfix.

Primary layer: cleanup pass for the crude strategic-map smoke scene after the first end-to-end LOOP-001 implementation.

## Estimate

- Size: M.
- Basis: focused cleanup/fix pass across existing strategic presentation/input/HUD tests and evidence only; no final UI architecture or new gameplay systems.

## Parent epic

- Epic ID/path: [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop|EPIC-STRAT-MVP-001 Strategic MVP Core Loop]].

## User/player/system value

As a human tester of the first local-hotseat strategic loop, I need the screen to be readable, controls not to overlap, and the map/HUD/status to make clear who is acting and what just happened, so that playtest feedback is about the game loop rather than confusion caused by placeholder presentation defects.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §2 Approved MVP Direction, rules 1-8.
  - `design/gdd/strategic-map.md` §6 Core Loop Contract, steps 1-4 and 9-10.
  - `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft, especially active faction/controller, active Champion, movement/reachable sites, whose turn is next, and status feedback.
  - `design/gdd/strategic-map.md` §9 Strategic Map Topology and §12 Champion/Army Strategic State and Movement Allowance as implemented by prior stories.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/unity-technical-scheme.md` §Project Layout Standard and §Assembly Boundary Standard.
  - `docs/architecture/control-manifest.md` §§1, 2, 3, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md` — QA, PlayMode/smoke, screenshot evidence, and regression requirements.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements.
- UX/content/art/worldbuilding:
  - Placeholder readability only. No final art, final lore text, localization framework, or UI system overhaul.

## Problem statement / observed issues

The current strategic smoke is technically playable but still too hard to read:

- buttons and HUD/status elements can visually crowd or overlay each other;
- the screen can feel crumpled together, especially around the map/HUD/status rows;
- it is not always obvious who is acting now;
- it is not always obvious what happened after selection, movement, invalid action, and End Turn;
- the map does not yet provide enough crude visual language for active Champion, inactive Champion, selected Champion, reachable route/node, current position, and next actor.

## In scope

- Audit the current `StrategicMap` smoke scene after LOOP-001 on current Unity `main`.
- Fix obvious placeholder UI/HUD/layout issues that make the smoke hard to read:
  - prevent End Turn and HUD/status labels from overlapping;
  - separate top-level HUD, map area, selected Champion info, and status feedback;
  - improve camera/map framing if needed;
  - improve placeholder contrast/scale/spacing where it directly affects readability.
- Improve crude feedback clarity using existing data only:
  - active faction/controller and active Champion;
  - selected Champion;
  - reachable node/route;
  - invalid action diagnostics;
  - successful movement diagnostics;
  - End Turn and round increment diagnostics;
  - explicit smoke-only unavailable systems note.
- Add regression tests where feasible for layout/feedback invariants.
- Add/update PlayMode screenshot evidence and a filled QA checklist.
- Record any remaining known issues as follow-up candidates.

## Out of scope

- Final UI art, animation, audio, UI Toolkit/Canvas architecture migration, localization implementation, accessibility polish beyond minimal readability, or new packages.
- New gameplay mechanics, site interaction, battle trigger, rewards, victory/loss, recruitment, resources, strategic AI, save/load, or tactical systems.
- Expanding map content, balance, lore, names, or final copy.
- Large scene/prefab architecture refactor unless a blocking bug proves it is unavoidable; stop and report before doing that.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Raw IDs/display keys and placeholder labels.
- Primitive shapes, lines, TextMesh labels, simple colors, simple debug/status panels.
- Existing smoke scenario data.

Not allowed:

- Fake green evidence by bypassing domain/application services.
- Presentation code mutating canonical gameplay state directly.
- New final UI/lore/content decisions.
- Hidden implementation of deferred systems.

## Dependencies

- Required prior implementation:
  - STORY-LOOP-001 merged to Unity `main`.
- Required architecture decisions:
  - Approved Unity technical scheme, control manifest, testing strategy, and CI/build automation.
- Required evidence:
  - Current LOOP-001 CI/evidence artifacts are available for comparison.

## Acceptance criteria

- [ ] Given the strategic smoke scene starts, when viewed at the default test resolution, then End Turn, active actor, turn/round, next faction, selected Champion, and status/deferred-system text are not visibly overlapping.
- [ ] Given the scene starts, when a human looks at the screen without console logs, then it is clear which faction and Champion are acting now.
- [ ] Given a Champion is selected, when reachable movement is available, then the selected Champion and reachable route/node are visually distinguishable from inactive/non-reachable elements.
- [ ] Given a valid move is applied, when the scene refreshes, then the Champion marker, HUD, and status text all agree on the new node and remaining movement.
- [ ] Given an invalid action occurs, when the scene refreshes, then the status feedback is readable and the map/HUD do not falsely imply the action succeeded.
- [ ] Given End Turn is pressed, when the next faction becomes active, then the active actor, next faction, selected Champion, and status feedback update coherently.
- [ ] Given site/battle/reward/victory systems remain deferred, when the smoke is run, then the UI/status clearly does not imply those systems are available.
- [ ] Automated PlayMode/regression coverage exists for objective layout/feedback invariants where feasible.
- [ ] Screenshot evidence before and after the cleanup shows the improved readability, with a filled checklist.
- [ ] PR evidence lists remaining known issues and confirms no new gameplay systems were added.

## Verification requirements

- Unit tests: N/A unless pure formatter/layout helper logic is added.
- Unity edit-mode tests: Required for added pure helper logic if applicable.
- Unity play-mode tests: Required for objective smoke/layout/feedback regression checks where feasible.
- Manual Unity scene checks: Required.
- Screenshot/video evidence: Required, showing initial state, selection/reachable state, movement result, invalid action, and after End Turn.
- CI evidence: Required on implementation PR.
- Performance budget or N/A: N/A for crude MVP smoke; do not add expensive effects.
- TDD evidence required? Yes for bug fixes and helper/application logic; PlayMode/manual evidence for presentation-only fixes.

## Ambiguity Check

Status: PASS as READY-candidate.

Open questions before approval:

- Should this pass remain a placeholder readability cleanup only, or may it introduce a small formal presentation layout helper if that is the cleanest way to prevent overlap? Default: placeholder readability cleanup only; helper allowed only if covered by tests and no architecture drift.

Assumptions:

- The user wants this cleanup before moving deeper into tactical/site stories.
- Raw IDs/display keys are still acceptable placeholders if spacing, hierarchy, and feedback are clear.

Out of scope:

- Same as story Out of scope section.

## Codex implementation notes

- Branch suggestion: `story/qa-001-strategic-smoke-cleanup-readability`
- Start from Unity `main` after PR #9 / STORY-LOOP-001 merge.
- Use the generated LOOP-001 evidence artifacts as baseline; do not rely only on code review.
- Stop if fixes require final UI architecture/art/localization, new packages, or gameplay beyond existing smoke behavior.

## Branch / PR requirements

- Branch name: `story/qa-001-strategic-smoke-cleanup-readability`
- PR title: `STORY-QA-001 Strategic smoke cleanup and readability pass`
- Required linked story ID: `STORY-QA-001`
- Required linked GDD/ADR/control docs: use the exact source references listed above.
- Required root/scoped AGENTS.md instructions: Unity repo root `AGENTS.md` and scoped source/test `AGENTS.md` under touched paths.
- Required evidence summary: issue list found, fixes made, tests added/changed, CI links/status, screenshots/video, and remaining known issues.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

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
- [x] Ambiguity Check status is PASS as candidate.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Estimate is recorded.
- [ ] Human approval has been given or delegated gate approval is recorded.

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

READY-candidate. Gate blocker: explicit human approval is still required before implementation.
