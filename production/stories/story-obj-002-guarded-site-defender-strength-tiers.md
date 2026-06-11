---
title: STORY-OBJ-002 Guarded Site Defender Strength Tiers
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
    design/gdd/faction-unit-rosters,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes,
    production/stories/story-obj-001-scenario-objective-state-and-victory-feedback,
  ]
approval: approved
---

# Story: STORY-OBJ-002 Guarded Site Defender Strength Tiers

## Status

DONE / merged. Implemented in Unity PR #29 and merged to `main` as `7b6807b5fe3b0b231102d293d12abd54e98acafd` on 2026-06-11. Post-merge main CI passed: Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests.

Implementation retained placeholder weak/standard/strong tier mappings, central objective tier `standard`, and deterministic placeholder defender setup only; no final balance was approved.

## Story type

Logic + Config/Data + UI/Integration + UX/Smoke.

## Estimate

- Size: M.
- Basis: adds a small defender-tier data contract and deterministic placeholder setup mapping, plus validation, UI/readability surfacing, tests, CI, and evidence. It should not change tactical rules or casualty persistence.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes.md`.

## User/player/system value

As a player testing the vertical slice, I need guarded sites to communicate whether I am attacking a weak, standard, or strong defender so objective and side-site choices feel intentional instead of identical placeholder fights.

## Source requirements

- `design/gdd/strategic-map.md` §§6, 8, 10, 11, 12, 13, 14 for map sites, control/capture, objective hooks, and battle handoff context.
- `design/gdd/tactical-combat.md` §§3-7 and existing MVP guarded-site setup/result expectations for placeholder stack setup only; no new tactical mechanics in this story.
- `design/gdd/faction-unit-rosters.md` for placeholder unit/stack fixture constraints; do not invent final roster, unit names, balance, or lore.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-003`.
- Baseline: Unity `main` after PR #28 / merge commit `69be356e2f0a4dbbb2d9cd1789b9c101dc1ab034`.

## Problem statement

`STORY-OBJ-001` makes the central objective visible and winnable, but all guarded encounters still read as generic guarded sites. The epic direction calls for `weak / standard / strong` defender tiers before adding casualty persistence or Champion-vs-Champion routes.

## In scope

- Add a minimal defender strength tier contract for guarded sites with exactly these values: `weak`, `standard`, `strong`.
- Assign deterministic placeholder tiers to the current guarded-site smoke scenario, including central objective tier `standard`.
- Map each tier to deterministic placeholder defender stack setup using existing tactical setup/result plumbing.
- Surface the tier in strategic preview/HUD/readable UI where guarded-site attack information is shown.
- Validate missing/invalid tier data for guarded sites and objective guarded sites.
- Add automated tests for tier validation, tier-to-defender setup, and visible preview/status text.
- Add PlayMode smoke and PNG evidence showing at least one visible tier before a guarded interaction.

## Out of scope

- Simple HP/strength persistence after battle.
- Champion-vs-Champion encounter routing.
- Strategic AI or enemy autonomous contest.
- New tactical abilities, cover, LOS, morale, healing, reinforcement, or full casualty economy.
- Full roster/balance pass or final unit names/content/lore.
- Multiple objective archetypes.
- Campaign progression, save/load, or full victory/loss framework.
- Final UI/art/accessibility.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder enum/string tier values `weak`, `standard`, `strong`.
- Existing placeholder unit IDs and localization keys.
- Deterministic stack-count/strength differences sufficient to prove tier mapping.
- Primitive tier labels in the existing readable Canvas UI.

Not allowed:

- Final balance claims.
- Final roster, unit, site, faction, or lore names.
- Tactical rule changes beyond defender setup input data.
- Presentation code directly mutating canonical gameplay state.
- Hidden fallback behavior that treats missing/invalid tier data as valid.

## Dependencies

- Required prior story:
  - `STORY-OBJ-001` DONE / merged in Unity PR #28.
- Required data/assets:
  - Existing larger-map guarded site and objective site placeholders.
- Required architecture decisions:
  - Current Unity data/runtime/presentation boundaries remain binding.

## Acceptance criteria

- [ ] Given the smoke scenario starts, every guarded site has exactly one defender tier: `weak`, `standard`, or `strong`.
- [ ] Given guarded-site interaction is previewed, the UI/readable preview shows the defender tier before battle launch.
- [ ] Given a weak / standard / strong guarded site launches a battle, the generated defender setup is deterministic and differs by tier in a simple placeholder way.
- [ ] Given a guarded site has missing, blank, or unsupported tier data, validation fails instead of silently defaulting.
- [ ] Existing objective completion/victory flow from `STORY-OBJ-001` still works.
- [ ] Existing larger-map recruitment-to-capture loop behavior still works.
- [ ] Existing tactical handoff/result path remains intact; no new tactical mechanics are introduced.
- [ ] Tier contract and defender setup mapping are covered by automated tests where feasible.
- [ ] PlayMode smoke and PNG evidence show visible tier feedback.
- [ ] CI passes.

## Verification requirements

- Unit/EditMode tests: Required for tier validation and tier-to-defender setup mapping.
- Unity PlayMode tests: Required for visible tier preview/status path.
- Integration/data validation tests: Existing validators must remain passing.
- Manual Unity scene/prefab checks: Required if scene/prefab assets change.
- Screenshot/video evidence: PNG evidence required under `production/evidence/STORY-OBJ-002/` or equivalent story evidence path.
- Performance budget: N/A; avoid expensive effects or rendering systems.
- CI evidence: Required on PR branch and post-merge main if merged.
- Playtest evidence: Supplemental checklist that a tester can see whether a guarded site is weak, standard, or strong before attacking.
- TDD evidence required? Yes for tier validation and defender setup mapping.
- Automation deferred? No, except manual visual judgment is supplemental and must be documented.

## Ambiguity Check

Status: PASS.

Resolved user decisions, 2026-06-11:

- `STORY-OBJ-002` is approved as READY.
- Use placeholder `weak` / `standard` / `strong` defender mappings; this does not approve final balance.
- Set the central objective tier to `standard` for now.

Assumptions:

- The tier names are already approved at the epic level: `weak`, `standard`, `strong`.
- Tier mapping may use placeholder stack count/strength differences only; no final balance is being approved here.

Out of scope:

- HP/strength persistence, Champion-vs-Champion combat, strategic AI, final balance/content/lore.

Allowed stubs/mocks:

- Placeholder tier labels and deterministic placeholder defender setups.

Human-approved exceptions:

- Human approved implementation on 2026-06-11 with central objective tier `standard` and placeholder tier mappings only.

## Branch / PR requirements

- Branch name: `story/STORY-OBJ-002-guarded-site-defender-strength-tiers`
- PR title: `STORY-OBJ-002 Guarded site defender strength tiers`
- Required linked story ID: `STORY-OBJ-002`
- Required linked GDD/ADR/control docs: strategic-map, tactical-combat, faction-unit-rosters, control-manifest, testing-strategy, CI/build automation.
- Required root/scoped AGENTS.md instructions: Unity repo root/scoped AGENTS.md.
- Required evidence summary: tier data/validation, tier-to-defender setup, visible tier preview, tests/checks, CI, omissions.
- Required omissions section: no HP/strength persistence, no Champion-vs-Champion implementation, no strategic AI, no final balance/content/lore, no final UI/art.

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

DONE / merged. Unity implementation is complete in PR #29; the checked-in prompt file is retained for audit only.
