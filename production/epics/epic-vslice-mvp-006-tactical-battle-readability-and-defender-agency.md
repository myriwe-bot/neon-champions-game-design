---
title: EPIC-VSLICE-MVP-006 Tactical Battle Readability and Defender Agency
type: epic
status: approved
phase: production
owner: shared
created: 2026-06-15
updated: 2026-06-15
source_lore: [champions, greenland, blue-monday]
related:
  [
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/ap-actions-and-reactions,
    design/gdd/tactical-combat/army-deployment-and-stacks,
    design/research/homm-like-tactical-battle-ui-reference,
    production/planning/prototype-readability-and-map-next-steps-2026-06-15,
    production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed,
    production/stories/story-tac-ret-001-minimal-melee-retaliation,
    production/stories/story-tac-afford-001-movement-and-attack-affordance-pass,
    production/stories/story-tac-unit-001-minimal-unit-definition-stats,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-006 Tactical Battle Readability and Defender Agency

## Status

APPROVED / IN PRODUCTION. Human approval recorded 2026-06-15: split the next work into two epics, with this epic covering tactical readability and defender agency. `STORY-TAC-READ-002`, `STORY-TAC-RET-001`, and `STORY-TAC-AFFORD-001` are DONE / merged; current READY child story: `STORY-TAC-UNIT-001 Minimal Unit Definition Stats`.

This epic is not direct implementation authority. Agents and Codex may only implement READY child stories.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Related systems

- Tactical Combat.
- Tactical UI/HUD.
- Stack combat.
- Retaliation / defender agency.
- AP, Wait, Defend.
- CombatAI.

## Capability goal

Make tactical battles readable, stack-based, and visibly two-sided: the player can tell who is acting, how many units are in each stack, where the active stack can move, what it can attack, what happened after an attack, and when defenders answer through retaliation or later AI control.

## Player / design value

The prototype currently communicates many internal facts but not the right player-facing facts. This epic fixes tactical comprehension before adding broader unit, base, or strategic-map complexity.

Relevant pillars:

- [x] Cyberpunk strategy/RPG.
- [x] HoMM-like exploration, capture, and tactical escalation.
- [x] Champions as command, identity, and force projection.
- [x] Factions as evolutionary philosophies, once unit definitions expand.
- [ ] Dirty information.
- [ ] Full Intel-as-operations economy.

## Source requirements

- GDDs:
  - `design/gdd/tactical-combat.md` for active tactical combat first-read authority.
  - `design/gdd/tactical-combat/army-deployment-and-stacks.md` for stack/army presentation context.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§28-91 for activation/AP/Wait/Defend/base actions.
  - `design/gdd/tactical-combat/ap-actions-and-reactions.md` §§119-195 for Retaliation, Zone of Control, and Overwatch sequencing.
  - `design/gdd/tactical-combat/implementation-contracts.md` for tactical implementation constraints.
- References:
  - `design/research/homm-like-tactical-battle-ui-reference.md` for stack counts, event-feed language, movement/attack affordances, and retaliation reference lessons.
  - `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` for approved ordering.
- ADRs / architecture docs / control-manifest sections:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Prior state:
  - `EPIC-VSLICE-MVP-005` repair train is complete and closeout accepted for purposes of starting this new epic.

## Scope

### In scope

- Tactical stack labels and current-stack readability.
- Combat event feed using concise HoMM-like natural language.
- Minimal melee retaliation in a child story after event feed readability exists.
- Movement and attack affordance pass.
- Minimal unit definition data to stop hardcoding tactical stats.
- Minimal AP + visible Defend state/bonus implementation.
- Functional neutral guard CombatAI.

### Out of scope

- Full final tactical UI skin, final icons, animation, VFX, audio, portraits, or final lore copy.
- Full faction roster implementation.
- Full damage types, armor/shield/cover/LOS/range-falloff implementation unless promoted by a later child story.
- Zone of Control opportunity attacks in the first retaliation story.
- Overwatch implementation.
- Full strategic AI.
- Strategic map topology redesign.
- Bases/recruitment expansion beyond what prior stories already implemented.

### Deferred

- Full square/hex strategic-map migration.
- Full faction rosters and upgraded unit lines.
- Advanced tactical AI personalities.
- Final battle animation/VFX/audio pass.
- Full tactical terrain system.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-TAC-READ-002 Tactical Stack Labels and Combat Event Feed](../stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed.md) | DONE / merged | Tactical UI + Playability Repair | EPIC-005 repair train DONE; current prototype tactical combat | Unity PR #48; post-merge CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27543258160 |
| [STORY-TAC-RET-001 Minimal Melee Retaliation](../stories/story-tac-ret-001-minimal-melee-retaliation.md) | DONE / merged | Tactical Rules + UI | TAC-READ-002 DONE | Unity PR #49; post-merge CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27552604744 |
| [STORY-TAC-AFFORD-001 Movement and Attack Affordance Pass](../stories/story-tac-afford-001-movement-and-attack-affordance-pass.md) | DONE / merged | Tactical UI | TAC-READ-002 and TAC-RET-001 DONE | Unity PR #50; post-merge CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27562547868 |
| [STORY-TAC-UNIT-001 Minimal Unit Definition Stats](../stories/story-tac-unit-001-minimal-unit-definition-stats.md) | READY / approved | Data + Tactical Domain | readability and affordance baseline | Unit-definition tests and tactical setup evidence |
| STORY-TAC-AP-001 Minimal Tactical AP and Defend State | Draft target | Tactical Rules + UI | unit/stat baseline or accepted prototype exception | AP spend/Defend tests and evidence |
| STORY-TAC-AI-001 Neutral Guard One-Step CombatAI | Draft target | Tactical AI | readable feedback/event feed | AI action tests and guarded-battle PlayMode evidence |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - `EPIC-VSLICE-MVP-005` DONE / closeout accepted for new direction.
- Required GDDs:
  - Tactical combat split GDDs cited above.
- Required technical decisions:
  - Existing Unity technical scheme and control manifest.
- Required testing/evidence strategy:
  - Strict layered tests, PlayMode smoke, PNG/manual evidence where needed, CI.
- Required CI/build automation:
  - Existing Unity Foundation CI.
- Required agent instruction scopes / AGENTS.md updates:
  - Unity root and scoped AGENTS.md at implementation time.
- Required data/assets:
  - Placeholder labels/text are allowed where final content is unavailable.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
| --- | --- | --- | --- |
| Adding mechanics before readability is fixed | UX / Scope | More opaque prototype | First story is labels/event feed only / shared |
| Event feed becomes noisy debug output | UX | Player still cannot parse battle | Require concise HoMM-like natural language and details-on-demand posture / shared |
| Retaliation expands into ZoC/Overwatch | Scope | Story becomes too large | Retaliation story excludes ZoC/Overwatch unless separately approved / shared |
| Unit definitions become full roster design | Scope / Design | Premature content lock | Minimal stats only; final faction rosters deferred / shared |
| AP breaks current command actions | Technical | Regressions in existing command stories | Implement after readability and with focused regression tests / implementation agent |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Relevant GDD sections exist.
- [x] Relevant technical decisions exist.
- [x] Required test/evidence layers are known.
- [x] Required CI/build checks are known.
- [x] Required agent instruction scopes / AGENTS.md updates are known.
- [x] Scope and out-of-scope are explicit.
- [x] Child stories are identified.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [x] At least one child story passes the Story Readiness Standard.

## Epic DONE gate

- [ ] Required child stories are DONE or explicitly deferred by human closeout.
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

## Verdict

APPROVED / IN PRODUCTION. `STORY-TAC-READ-002`, `STORY-TAC-RET-001`, and `STORY-TAC-AFFORD-001` are DONE / merged. Implement `STORY-TAC-UNIT-001` next. Do not start AP, AI, ZoC, Overwatch, Defend bonus, or strategic-map work until the relevant child story is promoted to READY.
