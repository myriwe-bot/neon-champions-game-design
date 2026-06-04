---
title: Tactical Combat
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-28
updated: 2026-05-30
source_lore: []
related:
  [
    design/gdd/game-concept,
    design/gdd/game-pillars,
    design/gdd/systems-index,
    design/gdd/faction-unit-rosters,
    design/gdd/intel-resource,
    design/research/tactical-combat-deep-reference,
    design/research/commander-spellbook-reference,
  ]
approval: pending
---

# Tactical Combat

> Status: Draft. Use this as the active first-read GDD for design and AI implementation planning. The older long-form packet notes are preserved in [[design/research/tactical-combat-deep-reference]].

## 1. Summary

Neon Champions tactical combat is a HoMM-readable stack battle system with cyberpunk, XCOM-lite positioning and operations. The MVP should feel fast, readable, and repeatable: active army stacks deploy onto a flat grid, spend simple AP, attack, reposition, contest objectives, suffer morale pressure, and receive limited off-board Champion support.

The design goal is not to simulate every firefight. Tactical combat exists to make faction rosters, Champion doctrine, army composition, Intel, infrastructure, and strategic preparation matter in a way that can later be implemented and tested by AI agents.

Quick reference:

| Field            | Value                                                                                                   |
| ---------------- | ------------------------------------------------------------------------------------------------------- |
| Layer            | Core                                                                                                    |
| Priority         | MVP                                                                                                     |
| Player fantasy   | Command a politically loaded cyberpunk army through clear tactical battles, not squad micro-simulation. |
| Main references  | HoMM active stacks + Shadowrun Returns tactical simplicity + limited non-magic commander operations.    |
| Key dependencies | Champions, faction rosters, strategic map, resources, Intel, objectives, UI/HUD, save/load.             |
| Main risk        | Scope explosion from too many tactical subsystems.                                                      |

## 2. Readability Rules for This GDD

For humans:

1. Read Sections 1-6 first. They define the playable combat loop.
2. Read Sections 7-10 when designing implementation stories.
3. Use the deep reference only for rationale, not as the normal design surface.

For LLM/agent work:

1. Treat numbered rules and tables in this file as stronger than prose in older notes.
2. If a rule is missing here, do not infer it from memory. Ask for a design packet or consult the linked reference and propose a distilled rule.
3. Do not add Full Vision mechanics to MVP stories unless the user explicitly accepts the scope.
4. Stories must cite exact section names and acceptance criteria from this GDD.

## 3. Design Principles

| Principle                   | Meaning                                                                                 | Implementation consequence                                                                       |
| --------------------------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Fast repeated battles       | The strategy layer can generate many fights.                                            | Avoid long setup, deep per-unit menus, heavy simulation, and universal interrupt rules.          |
| Stacks first                | Board entities are unit stacks, not individual soldiers.                                | Stack count affects damage/survivability, not AP or number of actions.                           |
| Champions command, not duel | Champions are normally off-board commanders.                                            | Champion impact comes through Command, Operations, Doctrine, Assets, and skills.                 |
| Simple AP, rare exceptions  | The baseline economy must be predictable.                                               | AP-breaking effects are signature abilities, not default speed scaling.                          |
| Cyberpunk clarity           | Hacking, Signal, drones, bodies, morale, and propaganda matter, but must stay readable. | Use explicit statuses and UI explanations instead of hidden simulation.                          |
| MVP flatness                | Tactical depth comes from roles/objectives, not verticality.                            | No elevation/high-ground rules in MVP.                                                           |
| Data-driven implementation  | AI agents need stable contracts.                                                        | Tunables, statuses, effects, and objectives must be represented as data, not hardcoded one-offs. |

## 4. MVP Scope

### In Scope

- Flat square or hex grid battlefield; final grid type remains a technical/design decision.
- HoMM-style active army stacks as tactical entities.
- 7 active army slots as the working baseline.
- All surviving active-army stacks deploy by default.
- Simple AP turn model.
- Movement, melee attack, ranged attack, ability use, defend/brace, wait, and objective interaction.
- Unit movement values and role differences.
- Ammo, charge, heat, cooldown, or capacity only where a unit role needs it.
- Basic line of sight and range bands.
- Simple cover/defense if it improves readability without XCOM-level complexity.
- Basic morale/rout/Rally.
- Limited Champion operations/commands from off-board.
- Post-battle summary: result, losses, rewards, secured objectives, missed major rewards, and asset consequences if assets exist.
- Data contracts for abilities, statuses, objectives, battle setup, save/load, and replay/debug.

### Out of Scope for MVP

- Height/elevation/high ground.
- Multi-floor maps.
- Full XCOM simulation stack.
- Universal overwatch for all ranged units.
- Hacking minigames inside every battle.
- General prisoner/capture economy.
- General resurrection/recovery economy.
- Tactical reserve bench before every ordinary fight.
- Champions as normal battlefield units.
- Broad weapon-tag taxonomies unless they clearly improve player/design readability.

## 5. Core Combat Loop

1. Strategic layer determines the battle context: attacker, defender, site/objective, scouting information, terrain family, and active armies.
2. Player reviews estimated enemy information if scouting/intel supports it.
3. Active army is locked when the player commits to the battle-triggering action.
4. Deployment uses map/battle-type rules. Prepared battles may allow quick reorder/formation choices; ambushes may restrict or disrupt deployment.
5. Stacks take turns or activations according to the initiative/turn model.
6. On activation, a stack spends AP on movement, attacks, abilities, defend/brace, wait, or objective interaction.
7. Champion commands/operations may affect the battle through a limited cadence/resource model.
8. Morale, statuses, damage, deaths, objectives, and routing update after actions.
9. Battle ends when victory/defeat/objective conditions are met.
10. Post-battle resolution updates losses, rewards, assets, morale consequences, and strategic map state.

## 6. Core Rules

### 6.1 Tactical Entities

| Rule              | Contract                                                                                                          |
| ----------------- | ----------------------------------------------------------------------------------------------------------------- |
| Default entity    | A tactical entity is a stack: multiple units of one unit type acting together.                                    |
| Champion presence | Champions are not normal board units in the baseline design.                                                      |
| Stack size        | Larger stacks gain durability and output, not extra AP/actions.                                                   |
| Stack composition | Composition normally locks at battle start.                                                                       |
| Exceptions        | Summons, drones, decoys, split-offs, Echo effects, or faction-specific fragments may exist as explicit abilities. |

### 6.2 Active Army and Deployment

| Rule            | Contract                                                                                     |
| --------------- | -------------------------------------------------------------------------------------------- |
| Active slots    | The working default active army size is 7 stack slots.                                       |
| Participation   | All surviving active-army stacks normally deploy.                                            |
| No bench        | MVP has no ordinary tactical reserve bench.                                                  |
| Stack splitting | Legal in army management; each split stack consumes a real active slot.                      |
| Tiny stacks     | 1-unit stacks are legal but flagged for playtest abuse.                                      |
| Deployment      | Fast formation/reorder choices are allowed in prepared battles; battle type owns exceptions. |
| Scouting        | UI must distinguish confirmed enemy information from estimates.                              |

### 6.3 AP and Actions

| Rule                    | Contract                                                                                                 |
| ----------------------- | -------------------------------------------------------------------------------------------------------- |
| Baseline AP             | Most stacks use a simple fixed AP budget. Working assumption: 2 AP baseline until prototyped.            |
| Movement                | Movement costs AP and uses unit-specific movement range.                                                 |
| Attacks                 | Standard attacks usually cost 1 AP unless tagged as heavy/signature.                                     |
| Heavy/signature actions | Powerful attacks or operations may cost 2 AP, consume capacity, or use cooldowns.                        |
| No AP spam              | Faster units should usually gain movement/initiative advantages, not extra baseline AP.                  |
| AP carryover            | No default AP carryover. Exceptions must be explicit.                                                    |
| Wait                    | Wait delays activation according to the final initiative model; it must not create hidden extra actions. |
| Defend/Brace            | Defensive fallback action for stacks without good attacks or movement.                                   |

### 6.4 Movement, ZOC, Retaliation, and Overwatch

| Topic           | MVP direction                                                                                                           |
| --------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Zone of Control | Use simple, readable engagement rules. Tiny stacks exert ZOC by default but this is a playtest flag.                    |
| Retaliation     | HoMM-like retaliation/counterattack texture is allowed; retaliation-baiting with tiny stacks is intentionally testable. |
| Overwatch       | Not universal. Use only for specific units/abilities if it earns the complexity.                                        |
| Forced movement | Allowed as explicit ability text with clear collision, edge, and objective rules.                                       |

### 6.5 Attacks, Damage, and Defense

Keep taxonomy orthogonal:

| Concept     | Meaning                                           | Example                                                    |
| ----------- | ------------------------------------------------- | ---------------------------------------------------------- |
| Damage type | What kind of harm/disruption is caused.           | Kinetic, thermal, chemical, bio, signal, morale/cohesion.  |
| Delivery    | How the effect reaches the target.                | Melee, direct ranged, indirect, area, line, cone, network. |
| Rule text   | Special behavior written directly on the ability. | Ignores shield, cannot retaliate, bonus vs drones.         |

Design guardrail: do not create a formal `Piercing` damage type or broad weapon-tag layer unless the user reopens that decision. Use explicit rule text for armor/shield bypass and special counters.

### 6.6 Information, LOS, Range, and Cover

| Topic                 | MVP direction                                                                                   |
| --------------------- | ----------------------------------------------------------------------------------------------- |
| LOS                   | Use simple line-of-sight checks sufficient for clear ranged play.                               |
| Range bands           | Prefer readable bands such as melee / short / medium / long over highly granular ballistics.    |
| Minimum range         | Optional per-unit weakness for specific heavy/indirect units.                                   |
| Cover                 | Keep cover shallow if used. It should improve positioning without forcing full XCOM cover math. |
| Smoke/vision blocking | Allowed as explicit status/terrain effect. UI must show blocked/uncertain targeting.            |

### 6.7 Status Effects

MVP statuses should be few, visible, and data-driven.

| Status family        | Purpose                                                  | MVP posture                                       |
| -------------------- | -------------------------------------------------------- | ------------------------------------------------- |
| Suppressed           | Reduce offensive freedom / punish exposed movement.      | Good MVP candidate if UI is clear.                |
| Jammed               | Disable or tax Signal/network abilities.                 | Use for Signal-counterplay units.                 |
| Hacked               | Temporary hostile control, debuff, or system disruption. | Keep rare and bounded. No hacking minigame.       |
| Marked / Sensor Lock | Improve focus fire, reveal, or operation targeting.      | Strong MVP candidate.                             |
| Stealth / Reveal     | Hidden or obscured units and their counters.             | Use sparingly; avoid hidden-information overload. |
| Smoke / Vision Block | Block or degrade targeting.                              | Good if map readability survives.                 |
| Morale state         | Confident, shaken, routing, etc.                         | MVP includes basic morale/rout/Rally.             |

### 6.8 Morale and Rout

| Rule      | Contract                                                                                               |
| --------- | ------------------------------------------------------------------------------------------------------ |
| Purpose   | Morale makes losses, isolation, leadership, intimidation, and faction identity matter.                 |
| MVP model | Use visible morale bands and major event triggers, not a deep hidden psychology sim.                   |
| Rout      | A routing stack loses normal player control and attempts to flee or collapse according to clear rules. |
| Rally     | Champion or unit abilities may restore control or morale through a limited action/resource.            |
| UI        | Player must be able to predict major morale risks before committing obvious morale-impacting actions.  |

### 6.9 Champion Commands and Operations

| Rule           | Contract                                                                                                                         |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Off-board role | Champions influence combat through command-layer actions, not tile presence.                                                     |
| Cadence        | Operation use must be limited by turn/round cadence, Command resource, cooldown, prepared loadout, Intel, or channel rules.      |
| Channels       | Current vocabulary: Signal, Logistics, Fire Support, Doctrine, Covert, Bio, Echo. Bio/Echo are special/factional.                |
| Build poles    | Marshal leans direct combat command and army performance; Operator leans operations, Signal, covert, assets, and infrastructure. |
| Guardrail      | Champion powers should not make unit roster tactics irrelevant.                                                                  |

### 6.10 Post-Battle Resolution

| Output           | Requirement                                                                                              |
| ---------------- | -------------------------------------------------------------------------------------------------------- |
| Outcome category | Win/loss/retreat/surrender/rout/objective result.                                                        |
| Losses           | Show destroyed, damaged, routed, preserved, or recovered stacks as applicable.                           |
| Rewards          | Show gained resources, Intel, assets, recruitment access, site control, and missed major rewards.        |
| Consequences     | Show morale, asset, Champion, faction, and strategic map consequences.                                   |
| MVP cut          | Keep resurrection, capture, and rare recovery as faction/authored exceptions unless explicitly designed. |

## 7. MVP Content Slice

The first playable combat slice should be intentionally small.

| Content            | Target                                                                                                                       |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| Factions           | 2 factions for contrast. Current candidate direction: Barents-aligned force vs Janus-Kestrel/corporate-security style force. |
| Units per faction  | 4-6 unit lines for prototype; not full roster.                                                                               |
| Abilities per unit | 1 standard attack + 0-2 defining abilities.                                                                                  |
| Champions          | 1 Marshal-like and 1 Operator-like test profile if needed.                                                                   |
| Battle types       | Prepared field battle + one objective battle.                                                                                |
| Objectives         | Kill/route enemy, control point/upload, extraction/raid, or site defense. Pick one non-kill objective first.                 |
| Terrain            | Flat grid with blockers, lanes, soft/hard cover if used, and simple hazards.                                                 |
| Statuses           | Marked/Sensor Lock, Suppressed, Jammed or Hacked, Morale state. Do not include every status family at once.                  |

## 8. Data and Implementation Contracts

### 8.1 Ability Contract

Every tactical ability should be representable as data with:

| Field        | Purpose                                                                    |
| ------------ | -------------------------------------------------------------------------- |
| id/name      | Stable key and display name.                                               |
| owner        | Unit, Champion operation, asset, objective, or scenario rule.              |
| cost         | AP, cooldown, ammo/charge/heat, Command, Intel, or other resource.         |
| targeting    | Self, ally, enemy, tile, area, line, cone, objective, off-board.           |
| delivery     | Melee/direct/indirect/area/network/etc.                                    |
| effects      | Damage, status, movement, morale, objective progress, resource change.     |
| restrictions | LOS, range, unit tags, terrain, status requirements, once-per-battle, etc. |
| UI preview   | What the player sees before confirming.                                    |
| AI hint      | Role weight: damage, control, objective, rescue, setup, finisher, denial.  |

### 8.2 Status Contract

Every status needs:

| Field             | Purpose                                                        |
| ----------------- | -------------------------------------------------------------- |
| id/name           | Stable key and display name.                                   |
| visible_to_player | Whether and how it is shown.                                   |
| duration          | Turns, rounds, until condition, battle-long, or permanent.     |
| stacking          | None, refresh, intensity, independent instances.               |
| timing            | When it applies and expires.                                   |
| effects           | Exact stat/action/AI/objective modifications.                  |
| counters          | Cleanse, reveal, repair, rally, wait, operation, terrain, etc. |
| save/replay data  | Minimum state required for deterministic restore.              |

### 8.3 Objective Contract

Every tactical objective needs:

| Field              | Purpose                                                           |
| ------------------ | ----------------------------------------------------------------- |
| id/name            | Stable key and display name.                                      |
| win/loss relation  | Primary victory, optional reward, escape, denial, fail state.     |
| eligible actors    | Which stacks/units/statuses can interact.                         |
| interaction cost   | AP, turns, channeling, item, Signal, Intel, or none.              |
| progress model     | Instant, counter, contested control, timed hold, extraction.      |
| interruption rules | Damage, ZOC, suppression, jam, death, movement, end of round.     |
| UI preview         | Clear state, remaining work, risks, and reward/consequence.       |
| AI priority        | How enemies value contesting, defending, rushing, or ignoring it. |

### 8.4 Save / Replay / Debug Contract

Implementation should support:

- deterministic battle setup from seed + authored battle data;
- serializable stack state, AP, position, statuses, cooldowns, ammo/charge, morale, objective progress, and Champion resource state;
- debug logs for action chosen, target, RNG roll if any, result, and triggered statuses;
- no hidden mutable state that cannot be inspected in tests.

## 9. Tuning Knobs

| Parameter            | Current posture    | Safe MVP range / note                                          |
| -------------------- | ------------------ | -------------------------------------------------------------- |
| active_army_slots    | 7 working baseline | 5-7 likely readable; prototype before changing.                |
| base_ap              | 2 working baseline | Keep fixed for most stacks.                                    |
| movement_range       | Unit-specific      | Faster units gain movement/initiative, not more AP by default. |
| standard_attack_cost | 1 AP               | Heavy/signature actions may cost 2 AP.                         |
| morale_bands         | Few visible bands  | Avoid fine-grained hidden morale.                              |
| operation_cadence    | Limited            | Once/round, cooldown, loadout, Command, or channel limit.      |
| status_count         | Small              | Prefer 3-5 MVP statuses over full taxonomy.                    |
| objective_complexity | Low                | One non-kill objective type first.                             |

## 10. UX and Readability Requirements

| Need                | Requirement                                                                                                           |
| ------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Action preview      | Before confirmation, show AP cost, target validity, expected damage/effects, and major morale/objective consequences. |
| Enemy information   | Label confirmed vs estimated scouting information.                                                                    |
| Stack readability   | Show unit type, count/strength, health, AP, morale, key statuses, and role.                                           |
| Champion operations | Show cadence/resource limits and why an operation is unavailable.                                                     |
| Objective state     | Show who controls/contests it, progress remaining, eligible actors, and reward/fail consequence.                      |
| Status explanations | Tooltip/status panel must state what the status does and when it expires.                                             |
| Post-battle clarity | Result screen must explain what happened and what changed on the strategic map.                                       |

## 11. Acceptance Criteria for First Implementation Slice

A first tactical prototype is useful only if all of these can be demonstrated:

- [ ] A battle can be launched from deterministic test data with two small armies.
- [ ] All active stacks deploy; no unplanned reserve bench appears.
- [ ] A stack can move, attack, wait, defend/brace, and use one data-defined ability.
- [ ] Larger stack size affects output/survivability but does not create extra AP/actions.
- [ ] At least one ranged unit uses LOS/range validation.
- [ ] At least one objective can be progressed, contested, completed, and displayed in UI/debug output.
- [ ] At least one visible status can be applied, expire, save/load, and affect action logic.
- [ ] Basic morale/rout/Rally can be simulated or explicitly stubbed with testable hooks.
- [ ] One Champion command/operation can affect combat through a limited cadence/resource rule.
- [ ] Post-battle resolution produces losses, winner, rewards/consequences, and strategic-state deltas.
- [ ] All tunable values used by combat are data-defined or intentionally marked as prototype constants.
- [ ] Automated tests can validate core rules without relying on Unity scene visuals.

## 12. Open Questions

These are real design gaps, not permission for agents to guess.

| Question                 | Why it matters                                                     | Suggested packet               |
| ------------------------ | ------------------------------------------------------------------ | ------------------------------ |
| Square vs hex grid       | Affects movement, targeting, UI, and map authoring.                | Tactical Grid Packet.          |
| Initiative model         | Determines Wait, morale events, Champion cadence, and AI planning. | Initiative/Turn Packet.        |
| Exact defense formula    | Needed for damage tuning and data schema.                          | Damage/Defense Formula Packet. |
| Cover depth              | Can improve positioning or create XCOM scope creep.                | Cover MVP Packet.              |
| First non-kill objective | Determines UI and AI priority model.                               | Objective MVP Packet.          |
| First faction pair       | Needed for playable content slice.                                 | Faction Pair Lock Packet.      |
| Morale numeric model     | Needed after the prototype proves morale is worth keeping.         | Morale Tuning Packet.          |

## 13. Detailed Split Articles

The original design-session work is preserved in smaller readable articles. Use these when a story, packet, or implementation prompt needs more detail than this overview.

| Need                                                                                                       | Read                                                               |
| ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Preservation map for all original top-level sections                                                       | [[design/gdd/tactical-combat/section-map]]                         |
| Overview, MVP scope, tactical entity model                                                                 | [[design/gdd/tactical-combat/overview-and-scope]]                  |
| Active army slots, stack splitting, deployment, scouting, AI valuation                                     | [[design/gdd/tactical-combat/army-deployment-and-stacks]]          |
| AP, initiative, wait, defend, base actions, counterattacks, ZOC, overwatch                                 | [[design/gdd/tactical-combat/ap-actions-and-reactions]]            |
| LOS, cover, range, damage types, attack model, defenses                                                    | [[design/gdd/tactical-combat/targeting-damage-and-defense]]        |
| Status taxonomy, suppression, jammed, hacked, marked, stealth, smoke, terrain, forced movement, objectives | [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]     |
| Retreat, surrender, morale, rout, rally, cohesion, morale UI                                               | [[design/gdd/tactical-combat/morale-rout-and-cohesion]]            |
| Battle outcomes, losses, rewards, capture/recovery exceptions, result UI                                   | [[design/gdd/tactical-combat/post-battle-resolution]]              |
| Ammo, charges, cooldowns, logistics, reload/recharge, indirect/area attacks                                | [[design/gdd/tactical-combat/ammo-capacity-and-logistics]]         |
| Champion operations, doctrine, progression, builds, assets, secondary skills, AP abilities                 | [[design/gdd/tactical-combat/champion-operations-and-progression]] |
| MVP cut, implementation contracts, ability/effect schema, status/objective/info/save/replay contracts      | [[design/gdd/tactical-combat/implementation-contracts]]            |
| MVP content matrix, faction-pair candidates, Barents role/stat/ability skeletons                           | [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]     |
| Stack action principle, deferred elevation, open questions                                                 | [[design/gdd/tactical-combat/deferred-and-open-questions]]         |

## 14. Other Cross-References

| Need                                   | Read                                               |
| -------------------------------------- | -------------------------------------------------- |
| Raw historical packet backup           | [[design/research/tactical-combat-deep-reference]] |
| Commander/operation reference research | [[design/research/commander-spellbook-reference]]  |
| Faction roster concepts                | [[design/gdd/faction-unit-rosters]]                |
| Intel resource                         | [[design/gdd/intel-resource]]                      |
| Systems map                            | [[design/gdd/systems-index]]                       |
| Pillars and anti-pillars               | [[design/gdd/game-pillars]]                        |
