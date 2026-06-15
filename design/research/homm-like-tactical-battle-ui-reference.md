---
title: HoMM-like Tactical Battle UI Reference
aliases: [Tactical Battle UI Reference, Combat Readability Reference]
type: reference
status: draft
phase: pre-production
owner: agent
created: 2026-06-15
updated: 2026-06-15
canon: reference
sources:
  - https://heroes.thelazy.net/index.php/Combat
  - https://heroes.thelazy.net/index.php/Creature
  - https://heroes.thelazy.net/index.php/Retaliation
  - https://heroes.thelazy.net/images/7/7a/Siege_combat.png
  - https://heroes.thelazy.net/images/thumb/5/5c/HOMM3_Battlefield.jpg/300px-HOMM3_Battlefield.jpg
  - https://store.steampowered.com/app/3105440/Heroes_of_Might_and_Magic_Olden_Era/
  - https://www.songsofconquest.com/
related:
  - design/gdd/tactical-combat
  - design/gdd/tactical-combat/ap-actions-and-reactions
  - design/gdd/tactical-combat/army-deployment-and-stacks
  - production/planning/prototype-readability-and-map-next-steps-2026-06-15
---

# HoMM-like Tactical Battle UI Reference

> Reference only. This note captures UI/readability lessons from HoMM-like tactical battles for Neon Champions prototype planning. It is not a final UI spec and does not override the active tactical GDD.

## Why this note exists

Current prototype feedback: the tactical prototype is communicating many internal/system facts, but not the right player-facing facts. The immediate model should be closer to HoMM3's readable battle language: stack counts visible, legal moves/attacks obvious, combat outcomes summarized in human language, and detailed numbers available on demand.

## Source observations

### Heroes of Might and Magic III

Sources:

- Combat rules: <https://heroes.thelazy.net/index.php/Combat>
- Creature/stack model: <https://heroes.thelazy.net/index.php/Creature>
- Retaliation: <https://heroes.thelazy.net/index.php/Retaliation>
- Example combat screenshots hosted by the wiki:
  - Siege combat: <https://heroes.thelazy.net/images/7/7a/Siege_combat.png>
  - Battlefield screenshot: <https://heroes.thelazy.net/images/thumb/5/5c/HOMM3_Battlefield.jpg/300px-HOMM3_Battlefield.jpg>

Relevant rules and presentation lessons:

1. Battles happen on a separate 11 by 15 hex battlefield. The strategic map hands off into a dedicated tactical surface.
2. Units are stacks. The creature page describes stacks as groups where stack damage kills individual creatures as HP is exhausted, and a stack's damage scales with number of creatures.
3. Stack size is a first-class visible concept. Even when exact overworld wandering-creature counts are hidden, combat is stack-based and counts matter constantly.
4. Combat proceeds in rounds and phases; speed/initiative determines order. The important UI lesson is not to expose every phase detail first, but to make the current acting stack and next activation understandable.
5. Defend is simple and legible: skip the rest of the turn and gain a defensive bonus. The H3 page states defend grants a 20% defense bonus.
6. Retaliation is default and expected. The retaliation page states that retaliation is the counterattack of a stack targeted by a melee attack and that all creatures normally have one retaliation per combat round, with exceptions.
7. Special exceptions are explicit: no enemy retaliation, more/unlimited retaliation, and special modified retaliation. This supports the Neon Champions rule that exceptions should be written on unit/attack traits, not hidden in broad categories.

UI/readability takeaways:

- The player should see the stack count on or near the stack, not only in an inspection panel.
- An attack should produce one compact outcome line, e.g. `Pikemen attack Swordsmen for 100 damage. 3 Swordsmen perish.`
- If the defender retaliates, it should get its own clear line immediately after the attack line.
- If retaliation does not happen, the reason should be visible when relevant: defeated, already retaliated this round, ranged attack, no-retaliation trait, disabled, or out of melee reach.
- Hover/click detail can show formulas, but the default battle feed should be clean natural language.
- Movement and attack affordances should be highlighted before commitment: reachable hexes, valid targets, and denial reasons.

### Heroes of Might and Magic: Olden Era

Source:

- Steam page and media: <https://store.steampowered.com/app/3105440/Heroes_of_Might_and_Magic_Olden_Era/>

Relevant public-page observations:

1. Olden Era explicitly returns to the HoMM formula: grand armies, spells, towns, resources, garrisons, world structures, and separate tactical battlefields.
2. The page references quick tactical battles with unit abilities and battlefield positioning. Steam media provides current screenshots, but UI details may change because the title is recent/active.
3. The important design lesson is conservative: modern HoMM-like games still keep the readable stack-army + separate-battlefield grammar, but modernize affordances and presentation.

Neon implication:

- Use Olden Era as a modern presentation reference, not as a locked mechanical source. If copying anything, copy its likely readability posture: high-contrast unit cards/counts, obvious battle-side state, and crisp interaction affordances.

### Songs of Conquest

Source:

- Official site: <https://www.songsofconquest.com/>

Relevant official text:

- `Explore a wide variety of maps with diverse enemies and valuable loot.`
- `Manage resources, research new advancements and expand your kingdom.`
- `Dive into a deep combat system utilizing troop abilities and powerful magic.`
- `Use the battlefield to your advantage by claiming high ground and protecting bottlenecks.`

UI/readability takeaways:

- Songs of Conquest keeps the HoMM-like strategic/tactical split but uses more modern readable battle spaces.
- Tactical terrain affordances such as high ground and bottlenecks are player-visible ideas, not hidden formulas.
- It is a good reference for showing tactical affordances cleanly without drowning the player in raw systems text.

## Current Neon Champions implementation gap check

Local repo inspection on 2026-06-15 found:

- `Assets/NeonChampions/Runtime/Domain/Tactical/TacticalBoard.cs` has legal move and legal attack calculation, but basic attack currently subtracts fixed damage from target count.
- No implemented default retaliation/counterattack logic was found.
- `Wait` and `Defend` exist as controls/session pass variants, but Defend does not yet apply the GDD's defensive bonus.
- AP is in the GDD, but not implemented as real tactical stack action points.
- Stack state is still placeholder-simple: unit ID plus current/max count on the strategic side; tactical placed stacks have count/range/movement/damage defaults rather than full unit definitions.

So the user's suspicion is correct: defenders do not appear to attack back in the current implementation, except when separately activated by player/session control. Default melee retaliation is designed, but not implemented.

## Minimum UI contract for the next tactical readability slice

For the next implementation pass, prefer these player-facing facts before deeper mechanics:

1. Stack label on each tactical marker:
   - display name or short unit key;
   - stack count;
   - current side/faction color;
   - current acting stack highlight.
2. Reachability overlay:
   - legal move hexes;
   - legal attack targets;
   - blocked/occupied hexes if inspected;
   - range/adjacency distinction.
3. Combat event feed:
   - one line per important result;
   - natural language first, numeric detail second;
   - example: `Polar Security Team attacks QXZ Survey Drones for 3 damage. 3 drones perish.`
   - example retaliation line: `QXZ Survey Drones retaliate for 1 damage. 1 attacker perishes.`
4. Detail disclosure:
   - hover/click stack card shows exact count, max count, movement, attack range, attack damage, retaliation available/spent, defend state, controller.
   - formula/detail can stay in tooltip or side panel, not in the main feed.
5. Defender agency:
   - melee defenders should retaliate by default once per round if alive and able.
   - if no retaliation occurs, the UI should explain only when the player would reasonably expect one.

## Design stance

Neon Champions should not copy fantasy UI chrome. It should copy the information hierarchy:

- first: who acts, where they can go, who they can hit;
- second: stack size and tactical state;
- third: clean outcome sentence;
- fourth: detailed numbers/formula/tooltips on demand.

That hierarchy fits the cyberpunk skin: clean command-console language, concise event feed, and inspectable tactical dossiers.
