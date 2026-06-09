---
title: STORY-TAC-006 Multi-Stack Attacker Tactical Setup
type: story
status: implemented
phase: production
owner: shared
created: 2026-06-09
updated: 2026-06-09
source_lore: []
related:
  [
    design/gdd/tactical-combat,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat,
    production/stories/story-tac-002-minimal-hex-board-and-stack-placement,
    production/stories/story-tac-005-basic-tactical-player-controls,
    production/stories/story-strat-006-simple-recruitment-site-fixed-offer,
    production/stories/story-loop-003-larger-map-recruitment-and-neutral-capture-vertical-slice,
  ]
approval: approved
---

# Story: STORY-TAC-006 Multi-Stack Attacker Tactical Setup

## Status

DONE / merged. Unity PR #23 squash-merged on 2026-06-09 as commit `ca41ca3d4d0f3ccfac3fc31b154cb19eeffbe8ee`; post-merge `main` CI passed for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests.

This removes the tactical setup prerequisite blocker for `STORY-LOOP-003`; LOOP-003 can be retried without weakening recruitment or tactical handoff.

## Story type

Logic + Integration + Tactical UI/Smoke.

## Estimate

- Size: S/M.
- Basis: expand existing tactical setup/board placement from a one-attacker-stack MVP limitation to a deterministic multi-stack attacker placement path, without adding new tactical actions, abilities, AI, balance, deployment UI, or final content.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat.md`.

## User/player/system value

As a player/designer, I want recruited Champion armies with more than one stack to enter the existing tactical battle handoff, so recruitment can feed the guarded-site capture loop without hidden merging, fake smoke paths, or tactical scope expansion.

## Source requirements

- `design/gdd/tactical-combat.md` §§3, 4, 5, 6.0, 6.1, 6.2.
- `design/gdd/tactical-combat.md` Source Authority Note for story-scoped tactical implementation.
- `design/gdd/strategic-map.md` §§4, 6, 12, 14.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-002`.

## In scope

- Remove the current one-attacker-stack tactical setup blocker for valid attacker armies with multiple active stacks.
- Support deterministic tactical board setup for at least the currently expected recruited Champion army shape: existing starting attacker stack + one newly recruited placeholder stack.
- Place multiple attacker stacks onto legal attacker deployment hexes using existing board/deployment concepts.
- Preserve existing single-attacker-stack setup behavior and snapshots.
- Preserve defender/guard setup behavior for existing guarded-site battles.
- Reject invalid or unsupported setup inputs cleanly without partial accepted board state, including:
  - null/empty attacker army;
  - null stack entries;
  - stacks with missing/blank IDs or unit references;
  - unsupported stack counts beyond available deployment hexes;
  - duplicate tactical entity IDs if the existing model requires uniqueness;
  - invalid battle side/controller/faction references already covered by prior DTO/placement rules.
- Add or update EditMode tests for valid two-stack attacker setup and invalid multi-stack edge cases.
- Add or update PlayMode/smoke coverage proving a recruited two-stack attacker army can launch the existing tactical handoff far enough to render or initialize the tactical board.
- Add evidence under `production/evidence/STORY-TAC-006/README.md`.

## Out of scope

- Full tactical deployment phase, formation selection, reorder UI, Tactics skill, scouting preview, reserve bench, garrison logic, reinforcement waves, initiative redesign, new tactical actions, new abilities, tactical AI changes, combat balance, new unit content, final art/audio/animation, save/load format changes, or completing `STORY-LOOP-003` itself.
- Changing recruitment to merge stacks, suppress the recruited stack, or otherwise hide the multi-stack army shape.
- Broad support for all seven active army slots unless the existing implementation makes that simpler than a two-stack path; if broad support is added, it must remain deterministic placement only, not a deployment UI/system.
- Enemy-faction site contests or strategic economy changes.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Existing placeholder attacker, recruited, defender, site, unit, and faction IDs.
- Deterministic placement order based on existing army stack order.
- Minimal placeholder labels/evidence screenshots.

Not allowed:

- Fake tactical board state that bypasses `BattleSetup` / tactical setup contracts.
- Silently dropping, merging, benching, or ignoring extra attacker stacks to satisfy the smoke.
- New final content names or lore-facing labels.

## Dependencies

- Required prior stories:
  - `STORY-TAC-002` DONE / merged: minimal hex board and stack placement.
  - `STORY-TAC-005` DONE / merged: basic tactical player controls.
  - `STORY-STRAT-006` DONE / merged: recruitment adds a new placeholder stack.
  - `STORY-LOOP-003` READY but BLOCKED by the one-stack tactical setup limitation discovered during implementation.
- Required data/assets:
  - Existing deterministic tactical board and placeholder stack definitions.
- Required architecture decisions:
  - Current Unity data/runtime/presentation boundaries remain binding.
- Required Unity/package setup:
  - Existing Unity CI and Windows self-hosted runner path.

## Acceptance criteria

- [ ] Given a valid guarded-site `BattleSetup` where the attacker Champion army has two active stacks, tactical setup succeeds and creates two attacker tactical entities on distinct legal attacker deployment hexes.
- [ ] Given the same battle with one attacker stack, existing one-stack setup behavior and tests remain valid.
- [ ] Given the defender/guard side from existing guarded-site battles, defender setup behavior remains valid.
- [ ] Given invalid attacker stack data such as null entries, blank IDs, missing unit references, duplicate tactical entity IDs where disallowed, or more stacks than available deployment slots, setup is rejected with readable diagnostics and no partial accepted tactical board state.
- [ ] Given a recruited two-stack attacker army reaches a guarded neutral site through existing strategic handoff code, PlayMode smoke can initialize/render the tactical board without `tactical-board-unsupported-stack-count`.
- [ ] Given this story completes, no new tactical actions, abilities, AI, deployment UI, recruitment changes, save/load changes, or final content are introduced.
- [ ] CI passes.

## Verification requirements

- Unity EditMode tests: Required for valid two-stack attacker placement, one-stack regression, defender regression, and invalid multi-stack setup rejection/no-partial-state cases.
- Unity PlayMode tests: Required for a strategic guarded-site handoff using a recruited two-stack attacker army to reach tactical board initialization/rendering.
- Integration/data validation tests: Existing validators must pass; add targeted validation only if data shape changes are introduced.
- Manual Unity scene/prefab checks: Required only if scene/prefab assets change; prefer no scene/prefab changes.
- Screenshot/video evidence: Screenshot preferred if tactical board rendering changes or if PlayMode evidence captures visible two-stack attacker placement. Otherwise test/evidence logs may suffice for non-visual setup changes.
- Performance budget: N/A for this small setup story.
- CI evidence: Required on PR branch and post-merge main.
- Playtest evidence: N/A; this is a prerequisite setup story, not a playtest story.
- TDD evidence required? Yes for new setup/placement logic and regression fixes.
- Automation deferred? No known exception at draft time.

## Ambiguity Check

Status: PASS.

Resolved user decision, 2026-06-09:

- `STORY-TAC-006` is approved as the next implementation packet.
- The goal is narrow tactical setup support for recruited multi-stack attacker armies, not broader tactical mechanics.
- Do not weaken `STORY-LOOP-003` by merging/hiding the recruited stack.

Assumptions:

- The minimum required support is two attacker stacks: the pre-existing attacker stack plus one recruited placeholder stack.
- Deterministic placement order should follow existing army stack order unless existing code already defines a stronger ordering contract.
- If available attacker deployment hexes already support more than two stacks, Codex may generalize placement to available slots, but only as deterministic setup plumbing.

Out of scope:

- Full deployment/reorder UI, new tactical actions, balance, tactical AI, save/load, and final content.

Allowed stubs/mocks:

- Existing placeholders from prior stories only.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-006-multi-stack-attacker-tactical-setup`
- PR title: `STORY-TAC-006 Multi-stack attacker tactical setup`
- Required linked story ID: `STORY-TAC-006`
- Required linked GDD/ADR/control docs: tactical-combat §§3, 4, 5, 6.0, 6.1, 6.2; strategic-map §§4, 6, 12, 14; control-manifest; testing strategy; CI/build automation.
- Required root/scoped AGENTS.md instructions: game-design repo `AGENTS.md`; Unity root/scoped `AGENTS.md` files for touched tactical runtime, strategic handoff, tests, and evidence paths.
- Required evidence summary: two-stack setup checklist, tests, screenshot/video status if visual evidence changes, CI, omissions/stubs, and explicit statement that LOOP-003 remains deferred until this lands.
- Required omissions section: no deployment UI, no tactical mechanics expansion, no recruitment changes, no final content/balance.

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
- [x] Dependencies are listed.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded.

## DONE gate

A story may be marked DONE only when all items are true:

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes or human-approved exceptions are documented.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE. Unity PR #23 merged and post-merge main CI passed on 2026-06-09. This verified recruited two-stack attacker armies can initialize/render tactical board setup, unblocking `STORY-LOOP-003`.
