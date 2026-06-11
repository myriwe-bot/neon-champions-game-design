---
title: STORY-OBJ-001 Scenario Objective State and Victory Feedback
type: story
status: implemented
phase: production
owner: shared
created: 2026-06-10
updated: 2026-06-11
source_lore: []
related:
  [
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes,
  ]
approval: approved
---

# Story: STORY-OBJ-001 Scenario Objective State and Victory Feedback

## Status

DONE / merged. Implemented in Unity PR #28 and merged to `main` as `69be356e2f0a4dbbb2d9cd1789b9c101dc1ab034` on 2026-06-11. Post-merge main CI passed: Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests.

This story was intentionally first and narrow: it established the scenario objective spine only. It did not implement defender tiers, HP/strength persistence, or Champion-vs-Champion combat.

## Story type

Logic + UI/Integration + UX/Smoke + Config/Data.

## Estimate

- Size: M.
- Basis: requires a minimal objective state/path, visible objective UI, victory/result feedback, and PlayMode/evidence coverage, but should not require new tactical rules.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes.md`.

## User/player/system value

As a player testing the vertical slice, I need a visible objective and clear victory feedback so I understand why I am moving, recruiting, and fighting instead of merely exercising disconnected prototype systems.

## Source requirements

- `design/gdd/strategic-map.md` §§6, 8, 10, 11, 12, 13, 14 for map sites, control/capture, resources/recruitment context, objective hooks, and tactical battle handoff.
- `design/gdd/tactical-combat.md` existing MVP handoff/result expectations; no new tactical mechanics in this story.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-003`.
- Baseline: Unity `main` after PR #27 / merge commit `d7661bf0e1fe7edca0704ac928994489e93ad337`.

## Problem statement

The current vertical slice has movement, recruitment, guarded-site combat, capture, and readable-enough UI, but it still lacks a clear scenario goal. The player can perform actions but is not explicitly told what they are trying to accomplish or when the slice is won.

## In scope

- Add one central guarded objective site or mark an existing central guarded site as the objective target.
- Add minimal objective state, e.g. incomplete / complete.
- Show objective status in the prototype UI, using the existing readable Canvas approach from QA-004 where applicable.
- Completing/capturing the objective target marks the objective complete.
- Show visible victory/success feedback when complete.
- Add tests for objective incomplete/complete state and victory feedback path.
- Add PlayMode smoke evidence and PNG screenshot evidence.

## Out of scope

- Defender strength tiers (`weak / standard / strong`).
- Simple HP/strength persistence.
- Champion-vs-Champion combat implementation.
- Strategic AI or enemy autonomous objective contest.
- Multiple objective archetypes.
- Campaign progression or save/load.
- Full victory/loss framework.
- Final UI/art/accessibility.
- New final names/content/lore.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder objective ID such as `objective_central_site` or localization key.
- Existing placeholder site/champion/unit IDs.
- Primitive objective tracker panel and victory text.
- Deterministic test/setup path.

Not allowed:

- Fake objective completion that bypasses runtime/application state.
- Presentation code directly mutating canonical gameplay state.
- Final content/lore names.
- Tactical rules or casualty model changes.

## Dependencies

- Required prior stories/epics:
  - `EPIC-VSLICE-MVP-002` DONE / closed.
  - `STORY-QA-004` DONE / merged.
- Required data/assets:
  - Existing larger-map site/control/tactical placeholder data.
- Required architecture decisions:
  - Current Unity data/runtime/presentation boundaries remain binding.

## Acceptance criteria

- [ ] Given the scenario starts, the UI visibly shows the current objective.
- [ ] Given the central objective site is not captured/complete, objective state is visibly incomplete.
- [ ] Given the player captures/completes the central objective site through the existing battle/capture path, objective state becomes complete.
- [ ] Given objective state becomes complete, the UI shows clear victory/success feedback.
- [ ] Existing larger-map recruitment-to-capture loop behavior still works.
- [ ] Existing tactical handoff/result path remains intact; no new tactical mechanics are introduced.
- [ ] Objective state and victory feedback are covered by automated tests where feasible.
- [ ] PlayMode smoke and PNG evidence show objective start, objective completion, and victory feedback.
- [ ] CI passes.

## Verification requirements

- Unit/EditMode tests: Required for objective state transitions and validation helpers.
- Unity PlayMode tests: Required for visible objective/victory smoke path.
- Integration/data validation tests: Existing validators must remain passing.
- Manual Unity scene/prefab checks: Required if scene/prefab assets change.
- Screenshot/video evidence: PNG evidence required under `production/evidence/STORY-OBJ-001/` or equivalent story evidence path.
- Performance budget: N/A; avoid expensive effects or rendering systems.
- CI evidence: Required on PR branch and post-merge main if merged.
- Playtest evidence: Supplemental checklist that a tester can tell what the objective is and when it is complete.
- TDD evidence required? Yes for objective state and result logic.
- Automation deferred? No, except manual visual judgment is supplemental and must be documented.

## Ambiguity Check

Status: PASS.

Open questions:

- None blocking for this narrow objective-state story if the user approves the packet.

Assumptions:

- The objective target is a central guarded site.
- Champion-vs-Champion combat, defender tiers, and HP/strength persistence are approved epic direction but intentionally deferred to later child stories.
- Placeholder objective names/IDs are acceptable.

Out of scope:

- Full victory/loss framework, strategic AI, defender tiers, casualties, Champion-vs-Champion combat.

Allowed stubs/mocks:

- Primitive objective tracker and victory text.
- Placeholder objective/site IDs.

Human-approved exceptions:

- Human direction recorded on 2026-06-10: objective type is central guarded site capture, while allowing Champion-vs-Champion combat later. Defender tier names are `weak / standard / strong`; casualty persistence target is simple per-stack HP/strength, both deferred from this first story.

## Branch / PR requirements

- Branch name: `story/STORY-OBJ-001-scenario-objective-victory-feedback`
- PR title: `STORY-OBJ-001 Scenario objective state and victory feedback`
- Required linked story ID: `STORY-OBJ-001`
- Required linked GDD/ADR/control docs: strategic-map, tactical-combat, control-manifest, testing-strategy, CI/build automation.
- Required root/scoped AGENTS.md instructions: Unity repo root/scoped AGENTS.md.
- Required evidence summary: objective start/incomplete state, objective completion/victory feedback, tests/checks, CI, omissions.
- Required omissions section: no defender tiers, no HP/strength persistence, no Champion-vs-Champion implementation, no strategic AI, no final UI/art, no final content.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/art/worldbuilding references are linked if relevant or explicitly N/A.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied or marked blocking.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed, or approved exceptions are documented.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given for implementation / READY promotion.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence pass, or human-approved exceptions are documented.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes or human-approved exceptions are documented.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged. Unity implementation is complete in PR #28; the checked-in prompt file is retained for audit only.
