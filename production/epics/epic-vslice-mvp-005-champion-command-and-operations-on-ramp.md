---
title: EPIC-VSLICE-MVP-005 Champion Command and Operations On-Ramp
type: epic
status: draft
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-13
source_lore: [champions, digital-net, greenland, blue-monday]
related:
  [
    design/gdd/game-pillars,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/champion-operations-and-progression,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-004-intel-resource-on-ramp,
    production/stories/story-cmd-001-champion-command-archetype-state-and-tactical-hud,
  ]
approval: pending
---

# Epic: EPIC-VSLICE-MVP-005 Champion Command and Operations On-Ramp

## Status

DRAFT / approved-candidate. Human closed EPIC-004 on 2026-06-13 and selected direction A: Champion Command / Operations. Human also requested that the next slice try to support both Champion poles, **Marshals** and **Operators**, rather than implementing only one archetype path.

This epic is not direct implementation authority. Agents and Codex may only implement READY child stories.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Related systems

- Tactical Combat.
- Champions.
- Command.
- Operations.
- Doctrine.
- Tactical UI/HUD.
- Strategic-to-tactical battle setup/result flow.

## Capability goal

Give the player the first visible Champion command loop: Champions enter tactical combat with finite battle-level Command, the prototype distinguishes Marshal-like and Operator-like command profiles, and the player can see that Champions are commanders with different intervention identities rather than only map actors carrying stacks.

## Player / design value

The previous slices made movement, site capture, tactical stakes, recruitment, objectives, and Intel matter. This slice starts making **Champions** matter as command identities.

Relevant pillars:

- [x] Cyberpunk strategy/RPG.
- [x] Champions as command, identity, and legitimacy.
- [x] HoMM-like exploration, capture, and tactical escalation.
- [x] Factions as evolutionary philosophies, if faction-linked Champion profiles are used.
- [ ] Dirty information.
- [ ] Full Intel-as-operations economy.

## Source requirements

- GDDs:
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§29-80 for Marshal/Operator poles, Command, Operations, and Doctrine framing.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§98-155 for finite Command economy and Major Operation / Minor Command cadence direction.
  - `design/gdd/tactical-combat.md` and split tactical-combat articles for active tactical battle scope and constraints.
  - `design/gdd/strategic-map.md` §§6, 7, 14 for strategic-to-tactical setup/result boundaries and Champion/army state context.
  - `design/gdd/game-pillars.md` for Champion identity and cyberpunk strategy/RPG pillars.
- ADRs / architecture docs / control-manifest sections:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Parent milestone:
  - `EPIC-VSLICE-MVP-004` DONE / closed.

Source authority note: the Champion Operations split article currently has draft/pending front matter while preserving approved design-session direction internally. Before any child story becomes READY, the child story must either cite an approved GDD section or record a narrow human-approved exception for the specific Marshal/Operator + Command sections it uses.

## Scope

### In scope

- Minimal Champion command profile support for both archetype poles:
  - Marshal-like command identity.
  - Operator-like command identity.
- Finite per-battle Command state.
- Tactical HUD/status feedback that shows Champion command profile and remaining Command.
- One narrow Marshal-like command and one narrow Operator-like operation, if approved as child stories.
- Tests and PlayMode evidence proving state, display, spend limits, and no unbounded operation system.

### Out of scope

- Full Champion skill trees, levels, classes, perks, loadouts, or progression UI.
- Full Operations spellbook.
- Full Doctrine/passive build system.
- More than one Marshal command and one Operator operation.
- Bio/Echo special channels.
- Command regeneration, complex cooldowns, reaction windows, interrupts, or per-round operation cadence beyond what a child story explicitly approves.
- Final Champion names, lore copy, portraits, voice, animations, icons, or VFX.
- Intel-paid operation upgrades or Field Upgrade replacement, unless later child stories explicitly approve that bridge.
- Legitimacy/public-narrative systems, death/Echo identity systems, capture/recovery, or campaign persistence.

### Deferred

- Operation channel taxonomy beyond the first placeholders.
- Champion progression and Doctrine.
- Intel spend integration into Command/Operations.
- Faction-locked Champion operation suites.
- Dirty information / feed manipulation as a full system.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-CMD-001 Champion Command Archetype State and Tactical HUD](../stories/story-cmd-001-champion-command-archetype-state-and-tactical-hud.md) | READY-candidate / approval pending | Tactical Domain + UI/Integration | EPIC-004 DONE | Command profile/state tests, BattleSetup/tactical-state propagation tests, PlayMode HUD evidence, CI |
| STORY-CMD-002 First Marshal and Operator Command Pair | Draft placeholder | Tactical Rules + UI/Integration | CMD-001 DONE | Spend/limit tests, one Marshal command, one Operator operation, PlayMode evidence, CI |
| STORY-CMD-003 Command On-Ramp Closeout Smoke | Draft placeholder | Connected Smoke + Evidence | CMD-001/002 DONE | Strategic -> tactical -> command use -> battle result smoke, PNG evidence, CI |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - `EPIC-VSLICE-MVP-004` DONE / closed.
- Required GDDs:
  - Tactical combat GDD and Champion Operations split sections, with source-authority status resolved before READY implementation.
- Required technical decisions:
  - Existing Unity technical scheme and control manifest.
- Required testing/evidence strategy:
  - Strict layered tests, PlayMode smoke, PNG evidence, CI.
- Required CI/build automation:
  - Existing Unity Foundation CI.
- Required agent instruction scopes / AGENTS.md updates:
  - Unity root and scoped AGENTS.md at implementation time.
- Required data/assets:
  - Placeholder IDs and text only.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
| --- | --- | --- | --- |
| Command expands into a full spellbook too early | Scope | Story becomes design-heavy and unmergeable | Limit CMD-001 to state/HUD; CMD-002 to exactly one Marshal command and one Operator operation / shared |
| Marshal/Operator becomes rigid final class system | Design | Prematurely locks Champion identity | Treat them as archetype poles and placeholder command profiles, not final classes / shared |
| Operator becomes only hacking | Design | Narrows cyberpunk fantasy too much | First Operator effect may be Signal-like, but epic keeps Logistics/Covert/Fire Support/Doctrine open later / shared |
| Tactical UI becomes unclear | UX | Player cannot tell what Command is or what changed | Require PlayMode HUD evidence and concise status text / reviewer |
| Draft source authority blocks Codex | Process | Implementation agent correctly stops | Resolve with narrow approval/exception before promoting child story to READY / human/shared |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Relevant GDD sections exist as draft/preserved approved direction.
- [x] Relevant technical decisions exist or are explicitly N/A.
- [x] Required test/evidence layers are known for expected child story types.
- [x] Required CI/build checks are known.
- [x] Required agent instruction scopes / AGENTS.md updates are known.
- [x] Scope and out-of-scope are explicit.
- [x] Child stories are identified.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [ ] At least one child story can pass the Story Readiness Standard after source-authority approval/exception.

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

DRAFT / approved-candidate for the next vertical-slice capability container. Recommended next action: resolve the narrow source-authority question for Champion Operations sections and, if accepted, promote `STORY-CMD-001` from READY-candidate to READY.
