---
title: STORY-INTEL-003 Guarded Data Site Intel Reward
type: story
status: done
phase: production
owner: shared
created: 2026-06-12
updated: 2026-06-12
source_lore: [digital-net, greenland, blue-monday]
related:
  [
    design/gdd/intel-resource,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-004-intel-resource-on-ramp,
    production/stories/story-intel-001-faction-intel-and-data-cache-pickup,
    production/stories/story-intel-002-first-intel-spending-sink-field-upgrade,
  ]
approval: approved
---

# Story: STORY-INTEL-003 Guarded Data Site Intel Reward

## Status

DONE / merged. Implemented in Unity PR #35 and squash-merged to `main` as `e8640ba8120fc7f6c31d6014fd40d4133fe6f95b` on 2026-06-12. PR-gate Unity Actions passed for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests on exact PR head `4a5d7e28c2373972e7086ef107c55efef3a21a2e`; post-merge `main` Unity Actions also completed successfully at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27423740025.

This packet continues the Intel on-ramp after `STORY-INTEL-002` by proving one risk-gated Intel reward path: a guarded site yields Intel only after successful guarded-site capture / battle-result return.

## Story type

Tactical/Strategic Integration + Economy + Smoke.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-004-intel-resource-on-ramp.md`.

## User/player/system value

As a vertical-slice tester, I need one guarded data site or guarded reward path to grant Intel only after resolving combat, so Intel can be earned from a higher-risk interaction rather than only a free cache.

## Source requirements

- `design/gdd/intel-resource.md` for Intel as secrets turned into power and for broader reward concepts; note that the broader GDD remains draft/pending.
- `design/gdd/strategic-map.md` for guarded sites, site interaction, control, resources, and battle handoff.
- `design/gdd/tactical-combat.md` for existing tactical resolution boundaries.
- `docs/architecture/control-manifest.md`.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Required prior stories:
  - `STORY-INTEL-001` DONE / merged.
  - `STORY-INTEL-002` DONE / merged.

Authority note: human approval on 2026-06-12 authorizes only this bounded guarded Intel reward subset. Broader Intel rewards, tactical optional objectives, hidden information, dirty information, recurring economy, and final content remain unapproved.

## Problem statement

`STORY-INTEL-001` made Intel collectible from a free data cache. `STORY-INTEL-002` proved one spend sink. The next slice is a single guarded data reward: successfully capture/resolve one guarded site through the existing battle-result return path, then award a small amount of Intel through the existing strategic result path.

## In scope

- Add exactly one guarded data reward path: reuse an existing guarded site if technically clean; otherwise add one placeholder guarded data site.
- Reward exactly `5 Intel` to the active/claiming faction only after successful guarded-site capture / battle-result return.
- Preview/communicate that the guarded site can yield `5 Intel` without adding hidden/fog/dirty-information systems.
- Award Intel exactly once, reject duplicates, and prevent partial mutation.
- Preserve existing `STORY-INTEL-001` free cache and `STORY-INTEL-002` field upgrade behavior.
- Add EditMode/application/domain tests for reward preview/commit, tactical/result gating, duplicate rejection, invalid data, resource mutation, and turn persistence.
- Add PlayMode smoke and PNG evidence for before guarded reward, reward preview/encounter, after reward, and persisted Intel total.
- Keep existing objective/combat/recruitment/Intel regressions green.

## Out of scope

- Multiple data vaults, tactical optional objectives, post-battle loot tables, recurring Intel economy, Intel subtypes, fog/hidden information, dirty information, counter-intel cleanup, operations/hacks/doctrine systems, upgrade trees, asset inventory, final content/art/UI redesign, save/load, or strategic AI spending.

## Ambiguity Check

Status: PASS.

Human-approved decisions recorded on 2026-06-12:

1. Continue EPIC-004 with this guarded Intel reward story.
2. Reuse an existing guarded site if technically clean; otherwise add one placeholder guarded data site.
3. Award Intel only after successful guarded-site capture / battle-result return, not merely preview or battle launch.
4. Fixed reward amount is exactly `5 Intel`.
5. Current crude PlayMode PNG evidence is sufficient for this story; defer broader UX/playtest unless evidence shows the loop is unreadable.

## Branch / PR requirements if later approved

- Branch name: `story/STORY-INTEL-003-guarded-data-site-intel-reward`
- PR title: `STORY-INTEL-003 Guarded data site Intel reward`
- Required linked story ID: `STORY-INTEL-003`
- Required omissions section: no recurring economy, Intel subtypes, fog/hidden information, dirty information, tactical optional objectives beyond the approved single path, operations/hacks/doctrine, upgrade trees, asset inventory, final content/art/UI redesign, save/load, or strategic AI spending.

## Story readiness gate

- [x] Stable ID, title, type, status, and parent epic exist.
- [x] User/player/system value is clear.
- [x] Prior dependencies are listed.
- [x] Candidate scope is bounded.
- [x] Out-of-scope work is explicit.
- [x] Human approval has been given for implementation / READY promotion.
- [x] Ambiguity Check status is PASS.
- [x] Exact reward amount and success condition are approved.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence pass.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes on PR branch and post-merge `main`.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged. No further implementation is authorized under this story; use `STORY-INTEL-004` only after human approval promotes it from DRAFT / READY-candidate to READY / approved.
