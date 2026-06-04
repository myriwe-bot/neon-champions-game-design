---
title: Tactical Combat — Overview and Scope
type: system-gdd
status: approved
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-06-04
source_lore: []
related:
  [design/gdd/tactical-combat, design/research/tactical-combat-deep-reference]
approval: approved
---

# Tactical Combat — Overview and Scope

> Status: Approved support article for the MVP tactical-combat GDD. This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Summary
- Current Design Direction
- MVP Scope Constraints
- Tactical Entity Model

---

## Summary

Neon Champions tactical combat is intended to combine HoMM-style army/faction identity with cyberpunk XCOM-lite tactical choices. The MVP combat board is flat: no elevation or multi-level terrain. Tactical depth should come from brutally simple AP, movement, ranged/melee roles, ammo/charge pressure, basic morale/rout/Rally, Champion command abilities, and faction-specific rule bending.

> Quick reference — Layer: Core · Priority: MVP · Key deps: Champions, Factions, Faction Unit Rosters, Strategic Map, Resources

## Current Design Direction

- Avoid full XCOM complexity for MVP.
- Target feel: Shadowrun Returns / Dragonfall / Hong Kong tactical simplicity, with HoMM-like strategic battle frequency and army identity.
- AP is stable by default; breaking AP rules is a Champion/faction identity moment.
- Elevation/high ground is explicitly deferred.
- Combat should remain fast enough for repeated strategy-map encounters.

## MVP Scope Constraints

MVP grid decision: tactical combat uses a flat **hex grid**. The first implementation should be minimal and readable: hex coordinates, neighbors, movement range, occupancy, and basic target/range checks only. Elevation and multi-floor maps remain out of scope.

### In Scope

- Flat hex grid battlefield.
- Simple action point economy.
- Different movement values by unit/stack.
- Melee and ranged attacks.
- Ammo, magazine, charge, or heat limits for ranged/special units where useful.
- Basic morale/rout/Rally: visible morale bands, major morale events, rout, and Champion Rally.
- Post-battle resolution/result screen: outcomes, stack losses, basic rewards, secured objectives, missed major rewards, and asset consequences where assets exist.
- Champion abilities that can manipulate AP for allied stacks.
- Defensive fallback action.

### Out of Scope for MVP

- Height/elevation.
- Multi-floor tactical maps.
- Complex vertical pathfinding.
- Full XCOM-style simulation stack.
- Universal overwatch for every ranged unit.
- Deep hacking minigame inside every battle.
- General capture/prisoner economy; rare authored/faction-specific capture can still exist.
- Global recovery/resurrection/return mechanics; faction-specific return mechanics are decided during roster design.

## Tactical Entity Model

Approved direction:

1. Tactical combat uses **HoMM-style stacks** as the default board entities.
2. A stack represents a group of the same unit type acting as one tactical entity.
3. Champions do **not** appear as tactical board units in the baseline design.
4. Champions affect battles through Command, Operations, Doctrine, Assets, starting skills, and faction/archetype rules.
5. More bodies in a stack increase damage output and survivability, not AP or number of actions.
6. Stack composition is normally fixed once battle starts.
7. Stack splitting during tactical combat is not a default action, but specific abilities/assets may create split-offs, decoys, drones, swarm fragments, Echo tricks, or similar exceptions.

Reference-game rationale:

- HoMM-style games primarily use army stacks as tactical entities; heroes/champions act through army stats, spell/command layers, skills, and artifacts rather than standing as ordinary board units.
- Other strategy references do have alternatives: Age of Wonders-style hero units can appear directly in battle, and XCOM-like games use individual soldiers. Those models create more tactical character drama but also increase encounter complexity, lethality handling, animation burden, and action-count pressure.
- For Neon Champions, direct Champion board presence is a poor baseline fit because the game already leans on HoMM-like repeated strategic battles, army identity, Command/Operations, and Marshal/Operator distinction. Operators especially should not need to physically stand in every firefight to matter.

Design notes:

- This locks the combat model toward fast, readable army-stack battles rather than squad tactics.
- Champion defeat/persistence is therefore primarily strategic-layer handling, not tactical-board HP depletion.
- Individual special entities may still exist as authored exceptions, but they are not the normal Champion representation model.
