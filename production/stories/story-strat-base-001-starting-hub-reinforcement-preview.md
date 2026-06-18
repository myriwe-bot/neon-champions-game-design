---
title: STORY-STRAT-BASE-001 Starting Hub Reinforcement Preview
type: story
status: done
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
approval: approved
---

# STORY-STRAT-BASE-001 Starting Hub Reinforcement Preview

## Status

DONE / merged. Human approval recorded 2026-06-18 from chat: `STORY-STRAT-BASE-001 approved`. Unity PR #56 merged 2026-06-18 as `c49c52d86043bb2fdd0095223e3bcb890ea5dec6`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27751021572

Approved scope was one narrow starting-hub reinforcement preview that makes the owned start/base-like site show a fixed replenish/reinforce affordance using existing recruitment/resource/army state, without adding a town-building tree, garrison management, stock-refresh economy, or new base system.

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

Status: PASS. Human approval recorded 2026-06-18.

Human-approved answers:

1. Approved as the next implementation packet.
2. Approved fixed-prototype direction: one starting-hub reinforcement affordance only, not a general base system.

Approved assumptions:

- This is a single fixed prototype reinforcement affordance at the owned starting hub/base-like site.
- It may reuse existing recruitment/resource/army infrastructure but must keep recruitment-site behavior distinct.
- Exact labels and placeholder unit/effect values may be implementation-owned if they satisfy the acceptance criteria and remain clearly prototype-scoped.

Out of scope:

- Full base system, town-building, garrisons, reserves/caravans, stock economy, new unit roster/balance, topology/presentation migration, tactical rules, final content/art.

Allowed stubs/mocks:

- One fixed prototype offer and placeholder presentation strings/icons/markers.

Human-approved exceptions:

- None. Story scope remains narrow and does not authorize a general base system.

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
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists: `production/evidence/STORY-STRAT-BASE-001/` in the Unity repo.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented in Unity PR #56.
- [x] PR/code review is complete: https://github.com/myriwe-bot/neon-champions-unity/pull/56
- [x] CI passes: PR exact-head Unity Foundation CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27750164280 and post-merge main CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27751021572
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged.
