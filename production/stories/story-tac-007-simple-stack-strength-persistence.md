---
title: STORY-TAC-007 Simple Stack HP/Strength Persistence
type: story
status: ready
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
    production/stories/story-obj-002-guarded-site-defender-strength-tiers,
  ]
approval: approved
---

# Story: STORY-TAC-007 Simple Stack HP/Strength Persistence

## Status

READY / approved for implementation. Human approved on 2026-06-11, with zero-count stacks removed from the active army as the intended rule and with explicit visual-layer/battle-result feedback included in scope.

## Story type

Tactical Logic + Strategic Result Integration + UI/Smoke + Data/Validation.

## Estimate

- Size: M.
- Basis: persists simple stack count/strength deltas through existing tactical result/application plumbing, updates strategic army summaries and visible battle-result feedback, adds tests and evidence, but does not add a full casualty/healing economy.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes.md`.

## User/player/system value

As a player testing the vertical slice, I need tactical losses to remain visible after battle so attacking guarded sites feels consequential instead of resetting to a disposable fight scene.

## Source requirements

- `design/gdd/tactical-combat.md` §§3, 4, 5, 6.1, 6.2, 6.5, and 5.10/post-battle resolution language for stacks-first combat, battle end, losses, and strategic result update.
- `design/gdd/strategic-map.md` §§8, 10, 11, 12, 13, 14 for site control, objective hooks, army/status readability, and tactical battle result application.
- `design/gdd/faction-unit-rosters.md` is a draft/pending source and is allowed by human-approved exception only as a non-authoritative placeholder/unit-fixture reference. Do not implement final roster, names, balance, recovery, or casualty lore from it.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-003`.
- Baseline: Unity `main` after PR #29 / merge commit `7b6807b5fe3b0b231102d293d12abd54e98acafd`.

## Problem statement

`STORY-OBJ-002` makes guarded-site difficulty visible and deterministic, but tactical casualties still do not persist as meaningful strategic state. The player can win or lose the site, yet surviving stack strength is not clearly carried forward as a visible consequence.

## In scope

- Add a minimal post-battle stack strength persistence contract for participating attacker stacks.
- Persist simple surviving stack count/strength from tactical result back onto the strategic Champion army when a guarded-site battle result is applied.
- Preserve stack identity by stable stack/unit IDs already present in the setup/result path; if an existing result lacks enough identity, add only the minimal DTO field needed for this story.
- Clamp or reject invalid surviving counts so persistence never creates negative, over-maximum, unknown, or duplicate stack state.
- Update readable strategic army summaries/status feedback after battle result application so the changed stack count is visible.
- Add a minimal visual layer for stack strength and battle results, using placeholder text/UI only: the player must see which stack count changed and that the battle result caused it.
- Cover objective-site and non-objective guarded-site result application where the current path supports both.
- Add automated tests for attacker stack persistence, invalid result rejection, objective victory regression, and existing recruitment-to-capture loop regression.
- Add PlayMode smoke and PNG evidence showing changed strategic army strength after resolving a guarded battle.

## Out of scope

- Defender army persistence after site capture.
- Healing, resurrection, replacement, reinforcement, recovery timers, hospitals, reserves, caravan logistics, or casualty economy.
- Per-unit HP bars, wounds, morale, rout, ammo, status effects, or detailed damage model changes.
- Champion-vs-Champion encounter routing.
- Strategic AI or enemy autonomous contest.
- New tactical abilities, cover, LOS, healing, morale, or final combat balance.
- Final unit names/content/lore, faction-specific casualty rules, or final UI/art/accessibility beyond the minimal visual feedback required for this story.
- Save/load or campaign progression.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Simple integer surviving stack count/strength per attacker stack.
- Existing placeholder unit IDs/localization keys and stack IDs. Use the draft roster GDD only to avoid contradicting placeholder unit/stack fixture direction; it does not authorize final roster/content implementation.
- Deterministic tactical smoke outcomes that reduce one participating stack enough to prove persistence.
- Primitive Canvas/HUD summary text such as `unit_placeholder_infantry 7`.
- Minimal battle-result feedback text/panel that reports stack count changes, e.g. `Infantry 10 -> 7` using placeholder localization/IDs where final copy is unavailable.

Not allowed:

- Hidden reset/default behavior that discards battle casualties while claiming persistence.
- Invented final casualty, healing, or replacement economy.
- Presentation code directly mutating canonical strategic army state.
- Allowing invalid result data to partially mutate strategic state.
- Broad BattleResult/DTO redesign beyond the minimal fields needed for stable stack persistence.

## Dependencies

- Required prior story:
  - `STORY-OBJ-002` DONE / merged in Unity PR #29.
- Required data/assets:
  - Existing larger-map guarded-site/objective smoke scenario and placeholder stack fixtures.
- Required architecture decisions:
  - Current Unity data/runtime/presentation boundaries remain binding.
  - Existing battle setup/result/application path remains the integration seam.

## Acceptance criteria

- [ ] Given a guarded-site battle resolves with reduced surviving attacker stack count, applying the battle result updates the matching strategic Champion army stack count.
- [ ] Given a battle result references an unknown attacker stack, unknown unit, duplicate stack entry, negative count, or count above maximum, result application fails with diagnostics and does not partially mutate strategic state.
- [ ] Given a battle result reduces a stack to zero, that stack is removed from the active strategic army, and this rule is documented and tested.
- [ ] Given the central objective battle is won, objective completion/victory flow from `STORY-OBJ-001` still works after stack persistence is applied.
- [ ] Given non-objective guarded-site battle is won, site capture and reward/result feedback still work after stack persistence is applied.
- [ ] Given the larger-map recruitment-to-capture loop runs, recruited multi-stack attacker armies persist post-battle stack counts without losing unrelated stacks.
- [ ] Given strategic UI/readable summaries refresh after battle result application, the player can see the changed army strength/count after returning from tactical view.
- [ ] Given a battle result is applied, a minimal visual battle-result layer communicates stack count changes before or during return to the strategic map.
- [ ] Existing defender tier behavior from `STORY-OBJ-002` still works.
- [ ] Persistence contract and invalid-result rejection are covered by automated tests where feasible.
- [ ] PlayMode smoke and PNG evidence show changed strategic army strength after battle.
- [ ] CI passes.

## Verification requirements

- Unit/EditMode tests: Required for stack persistence, invalid result rejection/no partial mutation, objective victory regression, and recruitment/multi-stack regression.
- Unity PlayMode tests: Required for visible changed army summary and minimal battle-result feedback after a guarded battle result.
- Integration/data validation tests: Existing validators must remain passing.
- Manual Unity scene/prefab checks: Required if scene/prefab assets change.
- Screenshot/video evidence: PNG evidence required under `production/evidence/STORY-TAC-007/` or equivalent story evidence path, showing both changed strategic army strength and battle-result feedback.
- Performance budget: N/A; no expensive simulation or rendering changes.
- CI evidence: Required on PR branch and post-merge main if merged.
- Playtest evidence: Supplemental checklist that a tester can see army strength changed after battle and can identify that the battle result caused the change.
- TDD evidence required? Yes for persistence and invalid-result rejection.
- Automation deferred? No, except manual visual judgment is supplemental and must be documented.

## Ambiguity Check

Status: PASS.

Open questions:

- None blocking.

Human decisions recorded on 2026-06-11:

- Approved as next implementation packet.
- Zero-count stack handling: remove zero-count stacks from the active army.
- Include a minimal visual layer for stack strength and battle-result feedback so the player can see stack changes and understand that the battle result caused them.
- Human-approved source-status exception: `design/gdd/faction-unit-rosters.md` is still `status: draft` / `approval: pending`, but TAC-007 may read it only as a non-authoritative placeholder fixture reference. It may not be used to implement final roster names, balance, recovery, lore, faction identity, or content.

Assumptions for review:

- "HP/strength" for this story means simple stack count/strength persistence, not a per-unit HP model.
- The visual layer means minimal placeholder UI/text feedback only, not final art or accessibility.
- Persistence applies first to attacker/Champion army stacks because that is the player-visible vertical-slice consequence.
- Defender persistence is deferred because captured neutral guards do not become a continuing army in the current slice.

Out of scope:

- Healing/recovery economy, Champion-vs-Champion, strategic AI, final balance/content/lore, detailed damage model.

Allowed stubs/mocks:

- Placeholder surviving-count deltas and deterministic tactical smoke outcomes.
- Placeholder visual feedback text/panels for stack-count deltas and battle results.

Human-approved exceptions:

- Human approved this story for implementation on 2026-06-11 with zero-count stack removal and minimal visual stack/battle-result feedback included.
- Human-approved exception: `design/gdd/faction-unit-rosters.md` remains draft/pending and is permitted only as a non-authoritative placeholder fixture reference for existing unit/stack IDs. If implementation needs roster/balance/content authority beyond placeholder fixtures, stop instead of using the draft GDD as authority.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-007-simple-stack-strength-persistence`
- PR title: `STORY-TAC-007 Simple stack strength persistence`
- Required linked story ID: `STORY-TAC-007`
- Required linked GDD/ADR/control docs: strategic-map, tactical-combat, control-manifest, testing-strategy, CI/build automation. `faction-unit-rosters` is linked under the human-approved draft-source exception above and may be read only as a placeholder fixture reference.
- Required root/scoped AGENTS.md instructions: Unity repo root/scoped AGENTS.md.
- Required evidence summary: stack persistence contract, invalid-result rejection, zero-count stack removal, visible army summary update, visual battle-result feedback, tests/checks, CI, omissions.
- Required omissions section: no healing/recovery economy, no defender persistence, no Champion-vs-Champion routing, no strategic AI, no final balance/content/lore, no final UI/art.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked; the only draft/pending source (`faction-unit-rosters`) has a narrow human-approved exception for placeholder fixture reference only.
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

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY / approved for implementation. Codex may implement exactly this packet from the checked-in prompt file `production/sprints/codex-story-tac-007.prompt.txt` after preflight confirms status/approval/PASS.
