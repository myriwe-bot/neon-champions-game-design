---
title: Prototype Readability and Map Next Steps — 2026-06-15
aliases: [Prototype Readability Next Steps, Tactical Readability Plan]
type: implementation-plan
status: draft
phase: pre-production
owner: agent
created: 2026-06-15
updated: 2026-06-15
related:
  - design/research/homm-like-tactical-battle-ui-reference
  - design/research/homm-like-strategic-map-topology-reference
  - design/gdd/tactical-combat
  - design/gdd/tactical-combat/ap-actions-and-reactions
  - design/gdd/strategic-map
---

# Prototype Readability and Map Next Steps — 2026-06-15

> Draft planning note. This does not authorize Unity implementation by itself. A READY story still needs exact scope, acceptance criteria, evidence requirements, and human approval.

## Current diagnosis

The prototype is proving a lot of systems, but it is not yet communicating the player's immediate tactical questions cleanly enough.

The highest-priority problem is not missing depth. It is readability:

1. What unit/stack is acting?
2. How many units are in each stack?
3. Where can the active stack move?
4. What can it attack?
5. What happened after an attack?
6. Did the defender retaliate?
7. Why was an action unavailable?
8. What did the battle change on the strategic map?

Current repo inspection found that default melee retaliation is designed in the GDD but not implemented in Unity yet. `TacticalBoard.AttackCurrentStack` currently applies fixed attack damage to the target stack count; no default counterattack/retaliation state or once-per-round resource was found.

## Reference summary

See:

- [[design/research/homm-like-tactical-battle-ui-reference]]
- [[design/research/homm-like-strategic-map-topology-reference]]

Key reference lessons:

- HoMM3 makes stack combat readable through stack counts, clear turn order, clean attack/retaliation outcomes, and simple player-facing actions like Wait/Defend.
- HoMM3 retaliation is a default melee counterattack once per round, with explicit exceptions.
- Songs of Conquest is a useful modern reference for visible tactical affordances and map/battlefield readability.
- Olden Era reinforces that modern HoMM-likes still expect towns/bases, resources, garrisons, world structures, and separate tactical battlefields.
- The strategic map should probably evolve from pure nodes toward a region/site or tile-like presentation, but not before the tactical readability debt is reduced.

## Recommended order

### 0. Close the current gate explicitly

Before implementation, mark the previous repair train/epic state clearly:

- EPIC-005 repair train is exhausted.
- No current Unity implementation story is approved.
- The next train should be a readability-first tactical/strategic clarity train, not a broad new mechanics train.

Output:

- One closeout/direction note or epic update.
- Human approval for the first READY story.

### 1. Tactical combat event log and stack labels

Goal:

- Make attacks understandable before adding many new mechanics.

Scope:

- Add/upgrade tactical stack labels:
  - unit display label or placeholder display key;
  - stack count;
  - side/faction color;
  - current acting highlight.
- Add a compact tactical event feed:
  - move line;
  - attack line;
  - damage/perish line;
  - defeated line;
  - denial line for invalid commands.
- Use HoMM-like natural language:
  - `Polar Security Team attacks QXZ Survey Drones for 3 damage. 3 drones perish.`
  - `QXZ Survey Drones are defeated.`

Out of scope:

- Full damage formula UI.
- Final unit names/art/icons.
- AP economy.
- Retaliation if this story is kept purely UI/readability.

Why first:

- If the battle log cannot explain current fixed-damage attacks, it will not explain retaliation/AP later.

### 2. Minimal melee retaliation

Goal:

- Fix the current asymmetry where defenders do not automatically answer melee attacks.

Scope:

- Add per-stack retaliation availability, default one per round.
- On adjacent/basic melee attack, if the defender survives and can retaliate, defender counterattacks after attacker damage.
- Retaliation does not cost AP.
- Add event-feed lines:
  - `QXZ Survey Drones retaliate for 1 damage. 1 attacker perishes.`
  - `No retaliation: target was defeated.`
  - `No retaliation: retaliation already spent.`
- Refresh retaliation at round boundary or simplest equivalent available in current tactical activation model.

Out of scope:

- Zone of Control opportunity attacks.
- First Strike / No Retaliation / Unlimited Retaliation traits, except as explicit future-ready fields if cheap.
- Full AP implementation.

Why second:

- It directly answers the user's concern and aligns the prototype with the approved GDD.

### 3. Movement and attack affordance pass

Goal:

- Make legal movement and attack range obvious before committing actions.

Scope:

- Highlight legal move hexes for the active stack.
- Highlight legal attack targets separately.
- Show selected stack movement range and attack range in the tactical side panel/card.
- Add denial explanations:
  - occupied hex;
  - out of movement range;
  - target out of attack range;
  - wrong side / defeated target.

Out of scope:

- Cover/LOS/range falloff.
- Terrain bonuses.
- Overwatch/ZoC.

Why third:

- The player must understand available actions before deeper rules matter.

### 4. Minimal unit definition data

Goal:

- Stop hardcoding every tactical stack as the same movement/range/damage shape.

Scope:

- Add small data-driven unit definitions:
  - stable unit ID;
  - display key/name;
  - movement range;
  - attack range;
  - attack damage;
  - melee-capable flag;
  - can-retaliate flag;
  - optional role tag.
- Keep placeholder unit IDs/content where necessary.
- Tactical board factory reads stack stats from definitions.

Out of scope:

- Full faction roster implementation.
- Damage types/armor/shields.
- Final balance.

Why fourth:

- Real readability needs different units to behave differently, but adding unit variety before labels/log/range clarity will only create more confusion.

### 5. Minimal AP + Defend bonus

Goal:

- Align current controls with the tactical GDD's 2 AP baseline and meaningful Defend action.

Scope:

- Add activation AP: max/current AP = 2.
- Move and basic attack cost 1 AP.
- Defend ends activation and applies visible `Defending` state.
- If Armor is not ready, implement a simple prototype damage reduction only if explicitly approved; otherwise show the state but avoid pretending hidden armor exists.
- Event feed explains AP spend and Defend.

Out of scope:

- Heavy/signature 2 AP actions beyond existing command actions.
- Initiative manipulation.
- AP carryover.

Why fifth:

- AP changes how every action feels. It should come after the player can read basic outcomes and ranges.

### 6. Neutral guard combat AI

Goal:

- Let defender/neutral sides act without requiring the player to manually operate both sides in simple guarded battles.

Scope:

- If adjacent attack exists, attack.
- Else move one legal step toward nearest enemy.
- Else pass/defend.
- Log AI actions in the same event feed.

Out of scope:

- Strategic AI.
- Personality or faction-specific AI.
- Ability planning.

Why sixth:

- This makes guarded-site battles feel like battles rather than board-state demos.

### 7. Strategic map readability pass

Goal:

- Make the current node-route strategic map communicate like a map, while preserving the approved graph model.

Scope:

- Reachable site/route highlighting from movement points.
- Path cost preview before movement.
- Clear site labels/icons for base/resource/recruitment/guarded/objective/cache.
- Interaction preview: move, battle, recruit, collect, contest, blocked.
- Stronger post-battle return summary: losses, rewards, capture, objective countdown.

Out of scope:

- Full tile/hex strategic topology.
- Fog/logistics/weather/supply.
- Map editor.

Why seventh:

- Tactical readability should be stabilized first because strategic decisions currently lead into confusing battles.

### 8. Bases and recruitment as a small next epic

Goal:

- Make bases matter without jumping to full HoMM town trees.

Scope:

- Starting hubs become visible home bases.
- At own base, show one simple reinforcement/recruitment affordance.
- Optional fixed stock/cost refresh per turn or scenario-defined stock.
- Show garrison/army summary if technically cheap.

Out of scope:

- Building construction.
- Full economy simulation.
- Multiple towns.
- Deep upgrade trees.

Why later:

- Bases and unit growth are important, but not more urgent than battle readability.

### 9. Region/site map evolution

Goal:

- Move the strategic presentation away from pure nodes toward a more HoMM-like map feel.

Recommended direction:

- Region/site hybrid first, not full tile map immediately.
- Keep graph rules internally.
- Add visible regions, roads/corridors, bases, guarded sites, and ownership overlays.
- Preserve future migration path to square/hex tiles by adding data fields rather than rewriting the core strategic model.

Out of scope for first pass:

- Full square/hex movement.
- Terrain pathfinding.
- Procedural map generation.
- Map editor.

Why later:

- This is a larger presentation/data shift and should be informed by playtesting after the immediate tactical readability fixes.

## Proposed first READY story candidate

Recommended first story:

`STORY-TAC-READ-002 Tactical Stack Labels and Combat Event Feed`

Purpose:

- Make current tactical combat understandable with HoMM-like stack labels and event text.

Acceptance criteria draft:

- Each visible tactical stack displays stack count and readable label/key.
- Current acting stack is visually distinct.
- Legal move and legal attack targets remain visible or are improved.
- Attacks produce one compact event line naming attacker, defender, damage, and units lost.
- Defeated stacks produce a clear defeat line.
- Invalid commands produce visible denial reasons.
- Existing tactical EditMode/PlayMode tests pass.
- Evidence includes a screenshot or PlayMode artifact showing a move, an attack, and the event feed.

Then follow with:

`STORY-TAC-RET-001 Minimal Melee Retaliation`

## Non-recommendations

Do not do these next:

1. Do not add many new units before stack labels, event feed, and unit data definitions exist.
2. Do not jump straight to a full strategic tile map before proving whether region/site presentation solves the readability problem.
3. Do not implement full AP, ZoC, Overwatch, cover, LOS, armor, and damage types in one story.
4. Do not treat more UI text as the solution if the core visual affordances remain unclear.
5. Do not let the prototype continue with defender passivity; HoMM-like melee needs retaliation/counterpressure.

## Human decision needed

Recommended approval path:

1. Approve the direction: readability-first tactical train.
2. Authorize the first READY story: tactical stack labels + combat event feed.
3. After that merges, authorize minimal melee retaliation.
4. Re-play the prototype before deciding whether the next epic is tactical AP/unit data, neutral AI, bases/recruitment, or strategic region-map presentation.
