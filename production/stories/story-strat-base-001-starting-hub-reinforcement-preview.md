---
title: STORY-STRAT-BASE-001 Starting Hub Reinforcement Preview
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-18
updated: 2026-06-18
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation,
    production/stories/story-strat-read-002-strategic-map-readability-pass,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-STRAT-BASE-001 Starting Hub Reinforcement Preview

## Status

READY-candidate / approval pending. This is the proposed second EPIC-007 implementation packet after `STORY-STRAT-READ-002` merged.

Do not implement until human approval promotes this story to READY / approved.

Recommended approval question: approve one narrow starting-hub reinforcement preview that makes the owned start/base-like site show a fixed replenish/reinforce affordance using existing recruitment/resource/army state, without adding a town-building tree, garrison management, stock-refresh economy, or new base system?

## Story type

Strategic Rules + UI / Base Affordance / Reinforcement Preview.

## Parent epic

- [EPIC-VSLICE-MVP-007 Strategic Map Readability, Bases, and Spatial Presentation](../epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation.md)

## User/player/system value

As a player, I want my starting hub/base-like owned site to clearly show whether it can reinforce my active Champion, what it would cost, and what it would change, so bases begin to matter as a readable strategic affordance without expanding into full town management.

## Source requirements

Exact source references:

- Parent epic:
  - `production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation.md` child story target: `STORY-STRAT-BASE-001 Starting Hub Reinforcement Preview`.
- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §§10-11 for site control, resources, recruitment/reinforcement, fixed offers, rewards/cost previews, and base-like starting hub context.
  - `design/gdd/strategic-map.md` §12 for Champion army state, major interaction availability, recruitment/reinforcement as a major site interaction, and active Champion army update boundaries.
  - `design/gdd/strategic-map.md` §13 for turn refresh and start-of-turn constraints if existing turn state is displayed.
- ADR / architecture / control:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Prior prerequisite:
  - `production/stories/story-strat-read-002-strategic-map-readability-pass.md` DONE / merged.

## In scope

Concrete implementation tasks proposed by this story:

- Treat the existing owned starting hub/base-like site as the first minimal reinforcement surface.
- Add a preview-visible reinforcement affordance for the active Champion when at the owned start/base-like site.
- Use one fixed prototype reinforcement offer or reuse an existing fixed recruitment/reinforcement offer if the current code already has one suitable path.
- Preview before commitment, at minimum:
  - offer/action label;
  - unit/stack or restore/add effect;
  - Credits/Materials/Intel cost if any;
  - affordability/availability;
  - resulting army/resource change summary where practical.
- Apply the reinforcement only through strategic-layer state, not tactical code.
- Preserve the existing recruitment-site flow; this story adds a starting-hub affordance, not a replacement for recruitment sites.
- Add focused EditMode tests for preview/apply validation and state mutation.
- Add PlayMode smoke/evidence showing the starting hub/base-like reinforcement preview and the post-apply summary.

## Out of scope

Not authorized by this story:

- No full base/town-building system, building tree, construction queue, upgrade tiers, garrison management, market, population, or production economy.
- No recurring stock refresh unless an already-existing stock rule can be reused without new economy semantics.
- No faction-wide reserves, caravans, detached armies, or multiple Champions.
- No new unit roster/balance pass beyond the single fixed prototype reinforcement offer.
- No new strategic topology, region/tile map, base art, final icons, VFX, audio, animation, localization, or lore/content pass.
- No new tactical combat rules.

## Allowed stubs, mocks, placeholders, or temporary data

- One fixed prototype starting-hub reinforcement offer is allowed.
- Placeholder labels/icons/markers are allowed if clear and covered by tests/evidence.
- Existing Credits/Materials/Intel resources and current Champion army data should be reused where possible.

## Dependencies

- Required prior stories:
  - `STORY-STRAT-READ-002` DONE / merged.
- Required data/assets:
  - Existing start/base-like owned site, active Champion, army state, resource state, strategic UI/presentation surfaces.
- Required architecture decisions:
  - Existing Unity technical scheme/control manifest; no new ADR required if this remains one fixed prototype affordance.
- Required Unity/package setup:
  - Existing Unity project and CI.

## Acceptance criteria

- [ ] Given the active Champion is at the owned starting hub/base-like site, the strategic UI visibly shows a reinforcement preview/action rather than treating the hub as only a label.
- [ ] Given the reinforcement preview is visible, it states the offer/effect, cost, affordability/availability, and likely army/resource change before commitment.
- [ ] Given the player commits an affordable reinforcement, strategic state updates deterministically: resources/costs and active Champion army change according to the fixed offer.
- [ ] Given the offer is unaffordable, unavailable, guarded/invalid, wrong-faction, or the Champion is not at the start hub, the action is denied with visible specific text and no partial mutation.
- [ ] Existing recruitment-site preview/apply flow remains green and semantically distinct from starting-hub reinforcement.
- [ ] Existing strategic movement, site interaction, battle return, objective, Intel/cache, Champion encounter, and tactical handoff/return smoke behavior is not intentionally regressed.

## Verification requirements

- Unit tests: Required only if new pure formatting/state projection helpers are introduced.
- Unity edit-mode tests: Required for reinforcement preview/apply validation, affordability, no-partial-mutation invalid cases, and recruitment no-regression.
- Unity play-mode tests: Required for visible starting-hub reinforcement preview and post-apply summary.
- Integration/data validation tests: Existing placeholder validator must remain green; add validation only if new authored data files are introduced.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-STRAT-BASE-001/` in the Unity repo.
- Performance budget or N/A: N/A; fixed offer preview/apply must be deterministic and cheap.
- CI evidence: Unity Foundation CI exact-head before merge.
- TDD evidence required? Yes for preview/apply/invalid-state behavior where practical.
- Automation deferred? No broad exception approved.

## Ambiguity Check

Status: PASS for READY-candidate, pending human approval.

Open questions before READY:

1. Human must approve this story as the next implementation packet.
2. Human should accept the fixed-prototype direction: one starting-hub reinforcement affordance only, not a general base system.

Assumptions proposed for approval:

- This is a single fixed prototype reinforcement affordance at the owned starting hub/base-like site.
- It may reuse existing recruitment/resource/army infrastructure but must keep recruitment-site behavior distinct.
- Exact labels and placeholder unit/effect values may be implementation-owned if they satisfy the acceptance criteria and remain clearly prototype-scoped.

Out of scope:

- Full base system, town-building, garrisons, reserves/caravans, stock economy, new unit roster/balance, topology/presentation migration, tactical rules, final content/art.

Allowed stubs/mocks:

- One fixed prototype offer and placeholder presentation strings/icons/markers.

Human-approved exceptions:

- None yet.

If status is FAIL, this story is not READY.

## Branch / PR requirements

- Branch name: `story/STORY-STRAT-BASE-001-starting-hub-reinforcement-preview`.
- PR title: `STORY-STRAT-BASE-001 Starting hub reinforcement preview`.
- Required linked story ID: `STORY-STRAT-BASE-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Application/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, PlayMode/PNG evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS for candidate; human approval remains pending.
- [x] Branch / PR / CI traceability requirements are stated.
- [ ] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY-candidate / approval pending.
