---
title: EPIC-VSLICE-MVP-014 Tactical Role Counterplay and Combat Decision Readability
type: epic
status: approved
phase: production
owner: shared
created: 2026-07-02
updated: 2026-07-02
source_lore: []
related:
  [
    design/gdd/game-pillars,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/planning/next-implementation-direction-brief-2026-07-02,
    production/epics/epic-vslice-mvp-013-scenario-pressure-and-victory-readability,
    production/stories/story-tac-role-001-tactical-role-counterplay-readability-smoke,
  ]
approval: approved
---

# EPIC-VSLICE-MVP-014 Tactical Role Counterplay and Combat Decision Readability

## Status

APPROVED / first story READY. Human approval recorded 2026-07-02: "approved" for the recommended Tactical role counterplay and combat decision readability direction from `production/planning/next-implementation-direction-brief-2026-07-02.md`. `STORY-TAC-ROLE-001 Tactical Role Counterplay Readability Smoke` is READY / approved as the current Unity implementation packet.

This epic is not direct implementation authority. Agents and Codex may only implement READY child stories.

## Capability goal

Make one tactical decision pattern visibly matter in the existing battle loop. A tester should understand what choice is available, why the target/role interaction matters, what happened after the action, and that the surrounding strategic-to-tactical loop still works.

## Player / design value

As a player/tester, I need tactical combat to show at least one readable role/counterplay decision instead of feeling like generic stack clicking, so battles can become an actual endpoint for strategic pressure, army composition, Champion preparation, and future economy choices.

## Source requirements

- `production/planning/next-implementation-direction-brief-2026-07-02.md` for approved direction/defaults.
- `design/gdd/tactical-combat.md` §§3-6 for MVP tactical principles, flat hex grid, stack entities, AP/action loop, movement/attack, retaliation, range, and readable statuses.
- `design/gdd/tactical-combat.md` §§6.2A, 6.3, 6.4, 6.5, and 6.6 for tactical battlefield readability, AP/actions, retaliation, attack/damage/defense, and information/range/cover boundaries.
- Existing merged tactical stories for AP/Defend, retaliation, range/threat readability, terrain readability, unit roles, and PlayMode tactical smoke evidence.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, and `docs/architecture/ci-build-automation.md`.

## Scope

### In scope

- One narrow tactical role/counterplay readability pass over existing tactical battle systems.
- Exactly one player-facing decision pattern, such as a marked/sensor-locked target, ranged threat choice, Defend tradeoff, focus-fire cue, or simple assault/support counter, chosen from what current implementation can support with the least new rules.
- Clear UI/event-feed/snapshot text explaining availability, target relevance, action result, and any denial/no-op state.
- Focused EditMode and PlayMode coverage plus generated evidence for before-choice, choice-available, action-result, and surrounding-loop-unbroken states.

### Out of scope

- Broad tactical AI, balance pass, initiative rewrite, LOS rewrite, cover system, universal overwatch, ability trees, faction-wide roster redesign, new tactical unit families, new strategic economy, campaign/meta systems, new map topology/content, final art/audio/VFX/icons/localization/accessibility framework.
- New dirty-information/PR/counter-intel systems.
- Champion spellbook/loadout/progression expansion.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story                                                                                                                                          | Status | Type                                  | Depends On                                                           | Evidence                                                                 |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [STORY-TAC-ROLE-001 Tactical Role Counterplay Readability Smoke](../stories/story-tac-role-001-tactical-role-counterplay-readability-smoke.md) | READY  | Tactical UX + rules/readability smoke | EPIC-013 DONE; tactical AP/range/terrain/readability baseline exists | Runnable prompt `production/sprints/codex-story-tac-role-001.prompt.txt` |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Risks

| Risk                                              | Type         | Impact                         | Mitigation                                          |
| ------------------------------------------------- | ------------ | ------------------------------ | --------------------------------------------------- |
| Counterplay expands into full tactical redesign   | Scope        | Unmergeable / untestable story | First story authorizes exactly one decision pattern |
| New rule is invisible or only debug-readable      | UX           | Does not improve playability   | Require player-facing text and PlayMode evidence    |
| Role mechanic bypasses data/control boundaries    | Architecture | Hard-to-maintain one-off       | Require control-manifest compliance and tests       |
| Tactical fixes sprawl into strategic/economy work | Scope        | Blurs epic boundary            | Explicit out-of-scope and stop conditions           |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Human approved direction/default.
- [x] Relevant source authority is explicit.
- [x] Scope and out-of-scope are bounded.
- [x] First child story is identified and READY / approved.
- [x] Required test/evidence layers are known.
- [x] No Unity implementation is authorized by the epic alone.

## Verdict

APPROVED / first story READY. Implement only `STORY-TAC-ROLE-001` until another child story is explicitly approved.
