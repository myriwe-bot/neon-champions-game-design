---
title: EPIC-VSLICE-MVP-003 Scenario Objective, Champion Combat, and Casualty Stakes
type: epic
status: approved
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
    production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-003 Scenario Objective, Champion Combat, and Casualty Stakes

## Status

APPROVED. Direction was selected by the user on 2026-06-10 after closing `EPIC-VSLICE-MVP-002`: central guarded objective capture, allow Champion-vs-Champion combat, defender tiers named `weak / standard / strong`, and simple per-stack HP/strength persistence. The user approved implementation prep for the first child story, `STORY-OBJ-001`, on 2026-06-10.

`STORY-OBJ-001`, `STORY-OBJ-002`, and `STORY-TAC-007` are DONE / merged. `STORY-TAC-008` is the next READY-candidate / approval-pending review packet; it is not READY until the Champion encounter trigger semantics are approved.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Related systems

- Strategic Map.
- Tactical Combat.
- Faction Unit Rosters.
- UI/HUD/readability.
- Scenario objective / victory feedback.

## Capability goal

Give the current strategic/tactical vertical slice a visible scenario goal and make combat outcomes persist enough that tactical fights matter.

The player should be able to:

1. See a central guarded objective site.
2. Understand that capturing it is the primary route to victory.
3. See defender tier: `weak`, `standard`, or `strong`.
4. Enter tactical combat from the objective site.
5. Persist simple stack HP/strength after the battle.
6. See objective victory feedback when the objective is captured.
7. Have the design/runtime path allow Champion-vs-Champion combat through the same tactical encounter/result model, without requiring strategic AI yet.

## Player / design value

This epic should turn the current prototype from "a capture loop exists" into "the player knows why they are moving, recruiting, and fighting." It also starts making tactical losses matter at a small, controlled level without opening the full tactical-combat design floodgate.

Relevant pillars:

- [x] Cyberpunk strategy/RPG.
- [x] Infrastructure-first conflict.
- [x] Champions as legitimacy and force projection.
- [x] HoMM-like exploration, capture, and tactical escalation.
- [ ] Intel as secrets turned into power.
- [ ] Dirty information.

## Source requirements

- GDDs:
  - `design/gdd/strategic-map.md` §§6, 8, 10, 11, 12, 13, 14 for sites, control, resources, recruitment, victory/objective hooks, and battle handoff.
  - `design/gdd/tactical-combat.md` §§3-7 and relevant post-battle/result sections for stack combat, battle resolution, and return to strategic state.
  - `design/gdd/faction-unit-rosters.md` for unit/stack fixtures; if insufficient, child stories must use clearly labeled placeholder units and avoid final roster/balance claims.
- ADRs / architecture docs / control-manifest sections:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Parent milestone:
  - `EPIC-VSLICE-MVP-002` DONE / closed.
- Worldbuilding/lore-facing content:
  - No new final city/base/site/unit names unless separately approved. Placeholder/localization keys only.

## Scope

### In scope

- One central guarded objective site.
- Objective tracker / status panel.
- Objective incomplete / complete state.
- Objective victory/success feedback.
- Defender tier values: `weak`, `standard`, `strong`.
- Tier-to-defender-setup mapping for placeholder tactical battles.
- Simple per-stack HP/strength persistence after tactical battle.
- Champion-vs-Champion combat as an allowed tactical encounter type/path.
- End-to-end PlayMode smoke and PNG evidence.

### Out of scope

- Strategic AI or enemy autonomous pursuit.
- Full PvE/PvP encounter system.
- Campaign victory/loss structure.
- Multiple objective archetypes.
- Full roster/balance pass.
- Tactical ability catalogue.
- Cover/LOS/terrain depth.
- Healing/reinforcement economy.
- Save/load.
- Final UI/art/accessibility.
- Deep Intel/economy systems.

### Deferred

- Strategic AI initiation of Champion-vs-Champion battles.
- Multiple objective types.
- Faction-specific objective rules.
- Full casualty, healing, and recovery economy.
- Tactical abilities / operations / morale / cover / LOS.
- Intel/dirty-information objective variants.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-OBJ-001 Scenario Objective State and Victory Feedback](../stories/story-obj-001-scenario-objective-state-and-victory-feedback.md) | DONE / merged PR #28 (`69be356`) | Logic + UI/Integration + UX/Smoke | EPIC-002 closed, current readable vertical slice | Objective-state tests, PlayMode smoke, PNG evidence, CI |
| [STORY-OBJ-002 Guarded Site Defender Strength Tiers](../stories/story-obj-002-guarded-site-defender-strength-tiers.md) | DONE / merged PR #29 (`7b6807b`) | Logic + Config/Data + UI/Integration | OBJ-001 DONE | Tier validation, deterministic defender setup tests, visible tier evidence, CI |
| [STORY-TAC-007 Simple Stack HP/Strength Persistence](../stories/story-tac-007-simple-stack-strength-persistence.md) | DONE / merged PR #30 (`d822018`) | Tactical Logic + Strategic Result Integration + UI/Smoke | OBJ-002 DONE | Battle-result persistence tests, zero-count removal tests, visual battle-result evidence, invalid-result tests, CI |
| [STORY-TAC-008 Champion-vs-Champion Tactical Encounter Path](../stories/story-tac-008-champion-vs-champion-tactical-encounter-path.md) | READY-candidate / approval pending | Tactical Integration + Strategic Encounter Routing | TAC-007 DONE | Deterministic Champion encounter smoke, result persistence evidence |
| [STORY-LOOP-004 Objective, Champion Combat, and Casualty Stakes Smoke](../stories/story-loop-004-objective-champion-combat-and-casualty-stakes-smoke.md) | Draft | Playtest + Integration + UX/Smoke | OBJ-001, OBJ-002, TAC-007, TAC-008 as scoped | End-to-end objective/casualty/champion evidence, CI |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - `EPIC-VSLICE-MVP-002` DONE / closed.
- Required GDDs:
  - Strategic Map approved sections.
  - Tactical Combat MVP sections and post-battle/result sections.
- Required technical decisions:
  - Existing Unity technical scheme and control manifest.
- Required testing/evidence strategy:
  - TDD for logic, EditMode tests for domain, PlayMode/smoke and PNG evidence for visible slice.
- Required CI/build automation:
  - Existing Unity CI and design-site CI.
- Required agent instruction scopes / AGENTS.md updates:
  - Unity root and scoped AGENTS.md at implementation time.
- Required data/assets:
  - Placeholder/localized IDs only unless content is separately approved.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
| --- | --- | --- | --- |
| Objective/victory becomes full campaign mode | Scope | Epic expands beyond MVP slice | One objective type only; no campaign progression / shared |
| Champion-vs-Champion implies strategic AI | Scope/Design | Agents build AI/pursuit instead of encounter path | Deterministic player/test-triggered encounter first; AI out of scope / shared |
| HP persistence becomes full casualty/healing economy | Scope | Tactical result model expands too early | Simple per-stack HP/strength only; no healing/recovery economy / shared |
| Defender tiers become balance design | Scope/Content | Agents invent final rosters/numbers | Placeholder deterministic tiers only; no final balance claims / shared |
| UI readability regresses | UX | Objective/stakes are unreadable | Reuse QA-004 Canvas approach and require PNG evidence / reviewer |

## Epic readiness gate

An epic may enter production only when all items are true:

- [x] Capability goal is clear.
- [x] Relevant GDD sections exist.
- [x] Relevant technical decisions exist or are explicitly N/A.
- [x] Required test/evidence layers are known for expected child story types.
- [x] Required CI/build checks are known for expected child story types, or explicitly N/A with reason.
- [x] Required agent instruction scopes / AGENTS.md updates are known, or explicitly N/A with reason.
- [x] Scope and out-of-scope are explicit.
- [x] Child stories are identified as candidates/placeholders.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [x] At least one child story can plausibly pass the Story Readiness Standard: `STORY-OBJ-001`.

## Epic DONE gate

- [ ] All required child stories are DONE.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, PlayMode/smoke evidence, and manual/PNG evidence are complete or accepted as documented exceptions.
- [ ] Unresolved omissions are documented.
- [ ] Docs have been updated in the correct source-of-truth layer.
- [ ] Playtest/QA evidence exists if required.
- [ ] No open blocker remains hidden.
- [ ] Human review accepts the epic as complete.

## Anti-pattern check

Invalid epic behavior:

- [ ] This epic authorizes production implementation directly.
- [ ] This epic replaces READY stories.
- [ ] This epic hides ambiguous design decisions.
- [ ] This epic bundles unrelated work for convenience.
- [ ] This epic asks agents to figure out missing details.

If any box above is checked, the epic needs revision.

## Verdict

APPROVED for production story train. `STORY-OBJ-001`, `STORY-OBJ-002`, and `STORY-TAC-007` are DONE / merged. `STORY-TAC-008` is prepared as READY-candidate / approval pending; next human decision is to approve or revise its Champion encounter trigger semantics before implementation.
