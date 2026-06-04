---
title: Tactical Combat — Champion Operations and Progression
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-05-30
source_lore: []
related:
  [design/gdd/tactical-combat, design/research/tactical-combat-deep-reference]
approval: pending
---

# Tactical Combat — Champion Operations and Progression

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Champion Operations and Doctrine
- Champion Progression Stats
- AP Abilities Group

---

## Champion Operations and Doctrine

### Champion Archetype Poles

Approved direction:

Neon Champions uses two broad Champion archetype poles inspired by HoMM's Might/Magic split:

1. **Marshal** — the Might analogue.
2. **Operator** — the Magic analogue.

These are poles, not necessarily rigid classes. Individual Champions may hybridize.

Marshal emphasis:

- Army improvement.
- Direct battle stats.
- Initiative.
- Retaliation and Zone of Control.
- Movement and positioning.
- Cohesion.
- Logistics discipline and endurance.
- Unit throughput and battlefield reliability.

Operator emphasis:

- Battle-level interventions.
- Disruption.
- Battlefield manipulation.
- Remote assets.
- Signal, logistics, covert, Echo, biotech, or infrastructure tricks.
- Effects that units alone cannot produce.

### Command, Operations, and Doctrine

Approved direction:

1. The universal battle-level Champion resource is **Command**.
2. The active spellbook-equivalent is **Operations**.
3. The passive/army-shaping Champion build layer is **Doctrine**.
4. Hacking/tech is one Operation channel, not the universal magic equivalent.

Definitions:

- **Command** — the Champion's limited battle-level capacity to issue meaningful interventions. Command represents operational leverage, authority, access, focus, and prepared battle control.
- **Operations** — active battle powers used by the Champion: the non-magic equivalent of spells.
- **Doctrine** — passive or conditional Champion identity effects that shape the army, comparable to a Might hero's army-wide strengths or a build-defining skill package.

Design notes:

- Avoid making every Operator a hacker/netrunner. Signal is important, but it must not swallow the entire magic-equivalent system.
- Tech/hacking should be a major channel because the setting is cyberpunk, but analogue, street, biotech, logistics, and Echo factions need equally valid Operation expressions.
- This preserves the high-tech vs analogue tradeoff: high-tech armies can access powerful Signal/network Operations, but are more vulnerable to spoofing, jamming, EMP, and system disruption.
- Marshal/Operator should echo HoMM's Might/Magic distinction without copying fantasy magic literally.

Candidate Operation channels/schools:

- **Signal** — hacking, spoofing, jamming, sensor lock, counter-hack, network intrusion.
- **Logistics** — resupply, recharge, repair, extraction, redeploy, emergency capacity.
- **Fire Support** — drone strike, artillery, missile call, White Sky-linked targeting, area denial.
- **Covert** — ambush, smoke, false flag, sabotage, decoys, informants, trap activation.
- **Doctrine** — rally, initiative shift, Cohesion restoration, coordinated attack, defensive formation.
- **Echo** — continuity override, afterimage action, identity disruption, death-state manipulation.
- **Bio** — pheromone trigger, growth surge, spore bloom, regeneration, contamination control.
- **Infrastructure / Systems** — doors, turrets, cameras, local grid, security state, battlefield objects.

Example framing:

- A Marshal spends Command to execute a clean military order: Rally, Forced March, Hold the Line, Emergency Resupply.
- An Operator spends Command to launch a battle-level Operation: Spoof Targeting, Sensor Blackout, Drone Strike, Echo Override, Spore Bloom, Trap Network.

### Command Economy

Approved direction:

1. Starting Command uses a hybrid calculation.
2. Command is primarily a finite battle pool.
3. By default, Command does not regenerate during battle.
4. Exceptions may exist later through specific Operations, Doctrines, units, objectives, faction mechanics, or scenario rules.
5. Major Operations have a cadence limit; minor Commands can be more frequent.
6. Marshals and Operators differ partly through Command economy and power profile: Operators get stronger/more flexible Command and Operations; Marshals get stronger Doctrine/passive army effects.

Starting Command candidate inputs:

- Champion level/build/archetype.
- Marshal vs Operator leaning.
- Army Cohesion.
- Army composition.
- Logistics/supply state.
- Strategic preparation.
- Battlefield/site context.

Cadence direction:

- Major Operations should not be spammable even if Command remains.
- Minor Commands may allow more frequent low-impact Champion expression.
- This preserves HoMM-like pacing while allowing cyberpunk command/intervention flavor.

Design notes:

- No-regeneration by default keeps MVP balance cleaner and makes Operations feel weighty.
- Exception-based Command generation leaves space for future Songs of Conquest-style army-generated resource, but avoids making that complexity core from day one.
- Operators should feel more like Magic heroes because they access stronger and more flexible Operations, not because every battle becomes operation spam.
- Marshals should feel more like Might heroes because their armies are more reliable, coherent, mobile, supplied, and dangerous even before spending Command.

### Operation Cadence and Action Types

Approved direction:

1. By default, a Champion can use **1 Major Operation per combat round**.
2. Major Operations may be used during any allied stack activation, subject to timing rules and Command cost.
3. **Minor Commands** are smaller Champion actions that may be used more than once per round.
4. Minor Commands may use Command, cooldowns, charges, trigger conditions, or a combination depending on the specific command.
5. Marshal identity leans more on Minor Commands and Doctrine; Operator identity leans more on Major Operations.

Definitions:

- **Major Operation** — a high-impact Champion battle intervention, similar to a spell in HoMM. Examples: Sensor Blackout, Drone Strike, Emergency Resupply, Echo Override, Spore Bloom, coordinated battlefield-wide Rally.
- **Minor Command** — a lower-impact Champion order or intervention. Examples: initiative bump, small Cohesion restore, targeted reload assist, Mark target, forced reposition order, brief defensive command.
- **Doctrine** — passive/conditional army-shaping rules that do not usually consume the Major Operation slot.

Design notes:

- Allowing Major Operations during allied stack activations makes the Champion feel reactive and commander-like without putting them on the battlefield.
- The 1 Major Operation per round limit prevents operation spam even when Command remains.
- Minor Commands must stay modest; they should not become a second AP system.
- Marshal Champions should feel active through reliable battlefield orders, formation discipline, Cohesion, logistics, and passive superiority.
- Operator Champions should feel active through fewer but more transformative battle-level interventions.

### Operation Channels

Approved direction:

1. Operation channels are **semi-formal categories** used for design, UI grouping, progression, and player comprehension. They are not rigid spell schools.
2. MVP should support **5 core channels**.
3. MVP core channels:
   - **Signal**
   - **Logistics**
   - **Fire Support**
   - **Doctrine**
   - **Covert**
4. **Bio** and **Echo** are important faction/special channels, not default universal MVP channels.
5. Bio and Echo should be treated as mutually exclusive or strongly opposed special channels by default.
6. Infrastructure / Systems is not its own channel for now; fold it into Signal, Logistics, or Covert depending on the specific Operation.
7. Channels are mostly universal in concept, but specific Operations may be faction-locked, Champion-locked, tech-locked, site-locked, or otherwise gated.

Core channel meanings:

- **Signal** — hacking, spoofing, jamming, sensor lock, counter-hack, network intrusion, targeting-feed manipulation.
- **Logistics** — resupply, recharge, repair, redeploy, extraction, emergency capacity, supply-state manipulation.
- **Fire Support** — drone strike, artillery, missile call, area denial, delayed/telegraphed indirect pressure.
- **Doctrine** — rally, initiative shift, Cohesion restoration, coordinated attack, defensive formation, disciplined execution.
- **Covert** — ambush, smoke, false flag, sabotage, decoys, informants, trap activation, hidden positioning.

Special/factional channels:

- **Bio** — biosplicing, forced adaptation, organic bolstering, regeneration, contamination, growth surge, battlefield organism control. Bio may play a necromancy-like role through body recovery, mutation, and organic reinforcement.
- **Echo** — continuity manipulation, identity persistence, afterimage action, death-state ambiguity, Echo disruption, post-mortem command traces. Echo may play a necromancy-like role from an informational/identity angle rather than a biological one.

Bio/Echo design note:

- Bio and Echo overlap thematically around death, persistence, replacement, and army bolstering, but they should approach those themes from opposite metaphysical/technical angles.
- Bio asks: what can be regrown, spliced, repaired, or repurposed as living matter?
- Echo asks: what persists as identity, command trace, simulation, memory, or continuity after bodily loss?
- Do not make them just two flavors of resurrection. Preserve the philosophical difference.

Design notes:

- Keep channels broad enough that analogue and low-tech factions can still have compelling Operations.
- Avoid making Signal the default answer to every Operator ability.
- Use Infrastructure / Systems as context: e.g. opening security doors may be Signal, emergency grid power may be Logistics, and booby-trapped local systems may be Covert.
- Semi-formal channels should help UI and progression, not force every Operation into a narrow taxonomy.

### Operation Example Vocabulary

Approved direction:

1. Draft a broader Operation vocabulary: **5 examples per core channel**.
2. Draft **5 Bio examples** and **5 Echo examples** as special/factional channels.
3. Include both tactical-combat and strategic-map Operations in the vocabulary.

These examples are provisional vocabulary, not final balance specs.

#### Signal Operations

| Operation         | Scope              | Type                                    | Concept                                                                                                                                  |
| ----------------- | ------------------ | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Sensor Lock       | Tactical           | Minor Command / Major Operation variant | Mark an enemy stack; allied ranged/indirect attacks gain accuracy or targeting access against it.                                        |
| Spoof Targeting   | Tactical           | Major Operation                         | Enemy stack's next ranged or indirect attack suffers accuracy penalty, target restriction, or may be redirected to invalid/decoy target. |
| Blackout Pulse    | Tactical           | Major Operation                         | Temporarily disables Overwatch, targeting assists, and some networked bonuses in an area.                                                |
| Counter-Intrusion | Tactical/Strategic | Minor Command / Reaction                | Cancel or reduce an enemy Signal Operation; strategic version protects army/site from hostile feed manipulation.                         |
| Feed Poisoning    | Strategic          | Major Operation                         | Corrupt local information state before battle: enemy starts with worse Cohesion, false scouting, or reduced starting Command.            |

#### Logistics Operations

| Operation          | Scope              | Type            | Concept                                                                                                      |
| ------------------ | ------------------ | --------------- | ------------------------------------------------------------------------------------------------------------ |
| Emergency Resupply | Tactical           | Major Operation | Restore Capacity to one or more allied stacks, especially ranged/heavy units.                                |
| Field Repair       | Tactical           | Major Operation | Restore HP to mechanical/cybernetic/armored stacks or repair Shield/Armor state.                             |
| Rapid Redeploy     | Tactical           | Major Operation | Move an allied stack without spending its AP, or reposition a limited distance under restrictions.           |
| Supply Corridor    | Strategic/Tactical | Major Operation | Improve battle Supply State or negate Cut Off/Strained penalties for a limited time.                         |
| Extraction Window  | Tactical/Strategic | Major Operation | Enable safe retreat, partial casualty recovery, evacuation of objective unit, or reduced post-battle losses. |

#### Fire Support Operations

| Operation            | Scope              | Type            | Concept                                                                                                             |
| -------------------- | ------------------ | --------------- | ------------------------------------------------------------------------------------------------------------------- |
| Drone Strike         | Tactical           | Major Operation | Direct or semi-indirect strike against a marked/visible target; moderate damage, high precision.                    |
| Suppression Barrage  | Tactical           | Major Operation | Area pressure that applies Suppressed, damages lightly, and punishes clumping.                                      |
| Delayed Missile Call | Tactical           | Major Operation | Telegraph a high-impact strike resolving later; enemies can move, jam, shield, or disable spotters.                 |
| Area Denial Pattern  | Tactical           | Major Operation | Create temporary danger tiles that discourage movement or protect a flank.                                          |
| Pre-Battle Fire Plan | Strategic/Tactical | Major Operation | Strategic preparation that starts combat with damaged cover, exposed enemies, or a first-round targeting advantage. |

#### Doctrine Operations

| Operation           | Scope              | Type                                    | Concept                                                                                                             |
| ------------------- | ------------------ | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Rally               | Tactical           | Minor Command / Major Operation variant | Restore Cohesion or remove a low-Cohesion penalty from selected allied stacks.                                      |
| Forced March        | Tactical/Strategic | Minor Command / Major Operation         | Tactical version grants movement/reposition; strategic version improves campaign movement or battle entry position. |
| Hold the Line       | Tactical           | Minor Command / Major Operation variant | Boost Defend, Retaliation readiness, ZoC reliability, or Shield/Armor for a defensive turn.                         |
| Coordinated Assault | Tactical           | Major Operation                         | One target becomes vulnerable to follow-up attacks from multiple allied stacks this round.                          |
| Battle Rhythm       | Tactical           | Major Operation                         | Adjust initiative timing, recover Wait positioning, or let a stack act earlier under constraints.                   |

#### Covert Operations

| Operation       | Scope              | Type                                    | Concept                                                                                                            |
| --------------- | ------------------ | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Smoke Break     | Tactical           | Major Operation                         | Create smoke/obscurement that blocks line of sight, weakens Overwatch, and enables disengage.                      |
| Ambush Cell     | Tactical/Strategic | Major Operation                         | Reveal hidden allied asset/stack, or start battle with a flanking/hidden position if prepared strategically.       |
| Sabotage Kit    | Tactical/Strategic | Major Operation                         | Disable a battlefield object, enemy supply source, turret, door, or heavy weapon for a limited time.               |
| False Flag      | Strategic          | Major Operation                         | Manipulate feed/legitimacy before or after battle; may alter enemy response, reinforcements, or public accounting. |
| Decoy Signature | Tactical           | Minor Command / Major Operation variant | Create false target/heat/signal/visual signature that soaks targeting or enables repositioning.                    |

#### Bio Operations — special/factional

| Operation          | Scope                | Type            | Concept                                                                                                                       |
| ------------------ | -------------------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Growth Surge       | Tactical             | Major Operation | Temporarily bolster a Bio stack's HP, Armor-like tissue, movement, or damage; may have post-effect decay.                     |
| Spore Bloom        | Tactical             | Major Operation | Area contamination that pressures cover, applies Chemical risk, or punishes enemies who remain clustered.                     |
| Tissue Reclamation | Tactical/Post-Battle | Major Operation | Recover losses from nearby organic casualties or convert battlefield biomass into healing/reinforcement.                      |
| Forced Adaptation  | Tactical/Strategic   | Major Operation | Grant temporary resistance or trait response after taking a damage type; strategic version prepares adaptation before battle. |
| Brood Signal       | Tactical             | Major Operation | Coordinate organic/swarm units: extra movement, Cohesion stabilization, or synchronized attack.                               |

#### Echo Operations — special/factional

| Operation         | Scope              | Type                                    | Concept                                                                                                                                 |
| ----------------- | ------------------ | --------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Afterimage Action | Tactical           | Major Operation                         | A recently damaged or destroyed stack leaves an Echo trace that performs a limited final action.                                        |
| Continuity Anchor | Tactical/Strategic | Major Operation                         | Reduce casualty permanence, stabilize Cohesion after losses, or preserve command identity through disruption.                           |
| Ghost Command     | Tactical           | Minor Command / Major Operation variant | Issue an order through an Echo trace, allowing a stack to ignore some Signal/Cohesion disruption or act from memory-pattern discipline. |
| Identity Fracture | Tactical           | Major Operation                         | Disrupt enemy Echo/networked/command-linked units; may reduce Cohesion, initiative, or Retaliation reliability.                         |
| Memorial Protocol | Strategic/Tactical | Major Operation                         | Convert fallen-unit memory into morale/Cohesion, recruitment legitimacy, or a battle-start Doctrine bonus.                              |

## Champion Progression Stats

### Primary Champion Stats

Approved direction:

Neon Champions uses **5 primary Champion stats** for now.

The stat model preserves the functional readability of HoMM's classic stat split while using setting-appropriate terms.

| Neon Champion Stat | HoMM Analogue                                  | Primary Role                                                                                                 |
| ------------------ | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Attack**         | Attack                                         | Improves army offensive performance.                                                                         |
| **Defense**        | Defense                                        | Improves army durability and defensive performance.                                                          |
| **Control**        | Spell Power                                    | Improves Operation strength, duration, radius, reliability, or penetration across all channels.              |
| **Command**        | Knowledge                                      | Increases starting Command pool and/or prepared operation capacity.                                          |
| **Logistics**      | Logistics / campaign skill elevated to primary | Improves supply, movement, capacity recovery, battle preparation, strategic reach, and post-battle recovery. |

Design rationale:

- Keep **Attack** and **Defense** because they are clear and avoid muddying terms like Command/Doctrine.
- **Command** should not mean generic unit efficiency. It is the Knowledge analogue: the size/reach of the Champion's battle-level Command pool.
- **Control** is the Spell Power analogue. It affects Operations broadly, not just hacking/Signal.
- **Logistics** is primary because ammo, capacity, supply state, strategic movement, and recovery are central to Neon Champions' combat/strategy loop.
- Champion stats describe off-board command influence, not personal battlefield combat.

Archetype leaning:

- **Marshal** Champions tend to favor Attack, Defense, and Logistics.
- **Operator** Champions tend to favor Command and Control.
- Hybrid Champions may combine army stats with limited but efficient Operations, or strong logistics with specialized operations.

Open tuning questions:

- Whether Attack/Defense are flat bonuses, percentage modifiers, trait unlock thresholds, or formula inputs.
- Whether Command increases only starting Command or also prepared Operation count/loadout flexibility.
- Whether Control affects all Operation channels identically or each Operation defines its own Control scaling.
- Whether Logistics affects tactical reload/recharge directly, strategic Supply State, campaign movement, post-battle recovery, or all of these.

### Primary Stat Scopes

Approved direction:

1. **Attack** improves offensive unit performance broadly.
2. **Defense** improves army durability and defensive reliability broadly.
3. **Command** increases starting Command pool and prepared Operation loadout.
4. **Control** scales Operation strength, duration, radius, reliability, penetration, or similar per Operation.
5. **Logistics** affects supply state, capacity recovery, deployment, retreat/extraction, post-battle recovery, and campaign movement.

Stat scope notes:

#### Attack

Attack may affect:

- Unit damage.
- Accuracy or hit reliability where relevant.
- Suppression output.
- Offensive retaliation strength.
- Conditional offensive bonuses from Doctrine, traits, or formations.

Attack should not directly improve Champion Operation damage unless a specific Operation says so.

#### Defense

Defense may affect:

- Armor and Shield effectiveness.
- Damage mitigation.
- Defend action strength.
- Cohesion stability under fire.
- Resistance to suppression, forced movement, or low-Cohesion penalties.
- Defensive Retaliation/ZoC reliability where appropriate.

Defense should represent army defensive performance, not the Champion's personal toughness.

#### Command

Command affects:

- Starting Command pool.
- Prepared Operation loadout size/flexibility.

Possible later extensions:

- Minor Command availability.
- Command retention under bad Cohesion.
- Operation readiness under poor Supply State.

#### Control

Control affects Operations per-operation rather than as a universal flat bonus.

Possible scaling knobs:

- Damage or healing.
- Duration.
- Radius / affected tiles.
- Number of affected stacks.
- Reliability / resistance penetration.
- Cooldown/charge efficiency.
- Strength of status effects.

Control applies across all Operation channels, not only Signal/hacking.

#### Logistics

Logistics affects:

- Strategic movement.
- Battle Supply State.
- Tactical Capacity recovery / reload-recharge access.
- Deployment and starting position advantages.
- Retreat, extraction, and casualty preservation.
- Post-battle recovery and readiness.
- Prepared supply corridors, field repair, and support assets.

- Logistics is a primary stat because Neon combat makes ammo/capacity/supply strategically important.

### Champion Leveling and Progression Structure

Approved direction:

1. Champion level-ups grant primary stat increases, like HoMM.
2. Champion archetype affects stat growth probabilities.
   - Marshals lean toward Attack, Defense, and Logistics.
   - Operators lean toward Command and Control.
3. Level-ups also offer skills, perks, Doctrines, and/or Operations.
4. Operations can be learned through multiple sources, but buildings/sites should be the dominant source.
5. Skill/channel progression is semi-linked: skills improve Operation channels, but Operations remain individual unlocks.

Progression sources:

- **Leveling** — primary stat gains, skill/perk choices, occasional Operation/Doctrine access.
- **Buildings / Sites** — main source of new Operations, analogous to spell guilds, training facilities, black sites, relays, clinics, field schools, archives, or faction institutions.
- **Faction tech / research** — unlocks operation families, upgrades, or channel access.
- **Artifacts / Assets** — grant specific Operations, modify Command/Control, or enable unusual channels.
- **Campaign events / quests** — unlock rare factional or narrative Operations, especially Bio/Echo or politically sensitive effects.

Design notes:

- Buildings/sites being the dominant Operation source preserves HoMM-like strategic map importance.
- Leveling should shape the Champion, but not replace the need to control/visit/build the right institutions.
- Semi-linked channels avoid rigid spell schools while still allowing progression identity: e.g. Signal Training improves Signal Operations, but Spoof Targeting remains its own unlock.
- Marshal progression should not be just worse Operator progression; Marshals need strong stat/passive/Doctrine growth and meaningful Minor Commands.
- Operator progression should feel like expanding a battle-intervention toolkit, gated by Command, Control, preparation, and strategic access.

### Operation Preparation and Loadout

Approved direction:

1. Use a hybrid known/prepared Operation model.
2. Basic/core Operations may be always available.
3. Advanced/special Operations require preparation into Operation slots.
4. **Command** affects Operation loadout size/flexibility.
5. Strategic Operations may be affected by pre-battle scouting, supply, and site context.
6. Marshals have fewer Major Operation slots but more Doctrine/Minor Command capacity.
7. Operators have more/flexible Major Operation preparation and stronger Operation scaling.
8. Faction/town/site buildings function like HoMM spell guilds for Operations, offering themed Operation unlocks.

Design notes:

- This preserves some HoMM spellbook collection appeal without allowing late-game Operators to answer every situation at once.
- Preparation should not become annoying inventory management. Use saved loadouts, recommendations, and clear warnings.
- Common fallback Operations prevent players from feeling punished for not preparing a basic tool.
- Advanced Operations should be powerful enough that choosing a loadout matters.
- Strategic Operations are more sensitive to scouting/supply/site context than ordinary tactical Operations.
- Command should not only be a spendable pool stat; it also governs how broad and flexible the prepared Operation kit can be.

Example structure:

- **Core Operations** — always available if the Champion/faction supports them: Rally, basic resupply, basic mark, baseline retreat/extraction.
- **Prepared Operations** — chosen before battle or during strategic preparation: Blackout Pulse, Drone Strike, Ambush Cell, False Flag, Continuity Anchor, Spore Bloom.
- **Site-granted Operations** — learned or temporarily available from faction buildings, map sites, black clinics, relay towers, firebases, archives, or local infrastructure.

### Operation Resistance and Counterplay

Approved direction:

1. Some Operations always succeed if paid and valid; hostile/disruptive Operations may be resisted.
2. Operation resistance is based on **Cohesion + traits + relevant defenses**, not one universal magic-resistance stat.
3. Counter-Operations exist, but should be limited and mostly passive, prepared, or reactive.
4. Enemy Command/Control affects Operation clashes mainly through Counter-Operations, not through every Operation resolution.
5. High-tech/networked armies are more vulnerable to some Operations but better at countering others.

Resistance model:

- Beneficial self/allied Operations usually succeed if valid.
- Logistics and Doctrine Operations usually succeed unless blocked by supply, disruption, or specific scenario conditions.
- Hostile Signal, Covert, Echo, Bio, suppression, manipulation, or control-style Operations may be resisted.
- Resistance should depend on the target's Cohesion, unit traits, defensive state, network/analogue status, and relevant active protections.
- Avoid a single generic “Magic Resistance” stat.

Counter-Operation examples:

- **Counter-Intrusion** — reacts to or reduces hostile Signal Operations.
- **Jamming Screen** — prepared protection against targeting, drones, indirect fire, or Signal effects.
- **Intercept Window** — prepared/passive response against Fire Support Operations.
- **Countermand** — Doctrine response that reduces enemy forced-movement, Cohesion, or initiative manipulation.
- **Bio-Quarantine** — prepared mitigation against contamination, spore, or biomass reclamation effects.
- **Continuity Firewall** — Echo-facing protection against identity disruption or post-mortem command interference.

High-tech tradeoff:

- High-tech/networked armies can access stronger Signal, targeting, drone, and counter-operation tools.
- They are also more exposed to spoofing, jamming, EMP/Shock disruption, hostile Signal Operations, and command-link attacks.
- Analogue/low-tech armies have fewer advanced channels but better baseline resistance to network-specific disruption.

Design notes:

- Counterplay should usually be prepared, positional, trait-based, or reactive; avoid making every Operation trigger a slow counterspell minigame.
- Operators should have meaningful duels, but Champion-vs-Champion clashes must not dominate every battle action.
- Counter-Operations are a way to make preparation matter without turning Operations into random failure rolls.

### Marshal / Operator Balance Guardrails

Approved direction:

1. Marshals have meaningful active tools: Minor Commands and some Major Operations, not only passive bonuses.
2. Operators have slightly weaker army stat growth to compensate for stronger Command/Control and Operation flexibility.
3. Some Operations may scale from Attack, Defense, or Logistics instead of Control when they are Marshal-flavored.
4. Marshal Doctrine should be able to rival Operations in impact over a full battle through sustained value.
5. Hybrid Champions should be viable, but weaker than specialists at extreme Marshal/Operator roles.

Balance intent:

- Operators should feel like the “magic hero” analogue because they produce dramatic battle interventions.
- Marshals should feel like the “might hero” analogue because their army performs better before, during, and after every engagement.
- A Marshal should not become boring passive math; they need active decisions through Minor Commands, Doctrine triggers, logistics calls, and some Major Operations.
- An Operator should not become a universal answer machine; Command pool, prepared slots, cadence limits, resistance, and counterplay constrain them.

Marshal-flavored Operation scaling examples:

- **Hold the Line** may scale with Defense.
- **Coordinated Assault** may scale with Attack.
- **Emergency Resupply** or **Supply Corridor** may scale with Logistics.
- **Forced March** may scale with Logistics or Attack depending on use.
- **Rally** may scale with Defense, Logistics, or Champion-specific Doctrine rather than Control.

Design notes:

- Control remains the default Operation scaling stat, but not the only possible one.
- Logistics-heavy Champions should be valid, not merely support builds.
- Hybrid Champions should trade peak power for flexibility: e.g. decent army stats plus a smaller prepared Operation kit.
- Marshal sustained value should be visible in UI and post-battle reports, otherwise players will undervalue it compared to flashy Operator effects.

### Example Champion Builds

Approved direction:

1. Initial Champion build examples work as a starting point, but ranged-focused archetypes must exist.
2. Bio and Echo special Operator examples are deferred until faction design.
3. Marshal examples should include aggressive and defensive/logistics builds.
4. Operator examples should include non-Signal builds, but Signal remains the most important Operator channel.

These are proof examples, not final named Champions.

#### Frontline Marshal

Fantasy:

- A hard-command battlefield leader who wins by making ordinary stacks hit harder, hold longer, and trade better.

Stat lean:

- High Attack.
- High Defense.
- Medium Logistics.
- Low/medium Command.
- Low Control.

Doctrine examples:

- **Combined Arms Discipline** — adjacent allied stacks or mixed-role formations gain small offensive/defensive reliability bonuses.
- **Retaliation Drill** — melee-capable stacks gain stronger Retaliation or better ZoC reliability.

Minor Command examples:

- **Hold Formation** — one stack gains improved Defend/ZoC until next activation.
- **Push the Line** — one stack gains limited movement or initiative correction.
- **Focus Fire Order** — mark one enemy for improved allied direct attacks this round.

Major Operation examples:

- **Coordinated Assault** — one enemy becomes vulnerable to sequential attacks.
- **Rally Under Fire** — restore Cohesion and remove one low-Cohesion penalty from nearby stacks.
- **Emergency Resupply** — limited, less efficient than a Logistics specialist.

#### Ranged / Fire-Control Marshal

Fantasy:

- A Marshal who turns ranged stacks into a disciplined kill network: lanes, overwatch-like threat, marked targets, ammunition discipline, and synchronized volleys.

Stat lean:

- High Attack.
- Medium/high Logistics.
- Medium Defense.
- Medium Command.
- Low/medium Control.

Doctrine examples:

- **Fire Discipline** — ranged stacks suffer less accuracy falloff or waste less Capacity when firing under pressure.
- **Kill Lanes** — ranged stacks gain bonuses against enemies crossing marked lanes, chokepoints, or exposed tiles.
- **Target Priority Doctrine** — marked or exposed enemies take better follow-up damage from allied ranged stacks.

Minor Command examples:

- **Focus Fire Order** — selected enemy becomes priority target for allied ranged attacks.
- **Reload Priority** — one ranged/heavy stack restores Capacity or reduces reload/recharge cost.
- **Shift Firing Line** — limited reposition for a ranged stack without fully sacrificing tempo.

Major Operation examples:

- **Coordinated Volley** — multiple ranged stacks gain a one-round bonus against a marked/exposed target.
- **Suppressive Fire Plan** — area or lane receives suppression pressure without being pure Fire Support artillery.
- **Emergency Resupply** — restore Capacity to key ranged/heavy stack(s).

Design note:

- This archetype is still a Marshal, not an Operator: the power comes from making units execute ranged doctrine better, not from external spell-like interventions.

#### Logistics Marshal

Fantasy:

- An army that should be exhausted, cut off, and empty somehow keeps fighting.

Stat lean:

- High Logistics.
- Medium Defense.
- Medium Attack.
- Medium Command.
- Low Control.

Doctrine examples:

- **Supply Discipline** — better battle Supply State; reduced penalty when Strained/Cut Off.
- **Recovery Network** — reduced post-battle losses, faster readiness recovery.

Minor Command examples:

- **Reload Priority** — one stack reloads/recharges more efficiently.
- **Field Rotation** — move a damaged stack backward or swap positions under constraints.
- **Stabilize Line** — restore small Cohesion plus defensive state.

Major Operation examples:

- **Supply Corridor**.
- **Extraction Window**.
- **Field Repair**.
- **Emergency Resupply**.

#### Signal Operator

Fantasy:

- The battle is won through targeting feeds, spoofed sensors, jammed weapons, and enemy command confusion.

Stat lean:

- High Control.
- High Command.
- Medium Logistics.
- Low Attack.
- Low Defense.

Doctrine examples:

- **Sensor Supremacy** — marked enemies are more vulnerable; allied indirect/ranged units benefit from targeting support.
- **Hardened Channels** — better resistance to hostile Signal Operations.

Minor Command examples:

- **Sensor Lock**.
- **Counter-Intrusion**.
- **Decoy Signature**.

Major Operation examples:

- **Blackout Pulse**.
- **Spoof Targeting**.
- **Feed Poisoning**.
- **Drone Strike**.
- **Jamming Screen**.

Design note:

- Signal should remain the most important Operator channel, but not the only viable way to build an Operator.

#### Covert Operator

Fantasy:

- The enemy never gets a clean fight: smoke, sabotage, false flags, ambushes, and manipulated public accounting.

Stat lean:

- High Command.
- Medium/high Control.
- Medium Logistics.
- Low/medium Attack.
- Low Defense.

Doctrine examples:

- **Prepared Cells** — better opening position, hidden assets, or ambush access when scouting/prep succeeds.
- **Plausible Deniability** — strategic/public consequences of certain battles are reduced or redirected.

Minor Command examples:

- **Decoy Signature**.
- **Smoke Break**.
- **Countermand** or **Ambush Signal**.

Major Operation examples:

- **Ambush Cell**.
- **Sabotage Kit**.
- **False Flag**.
- **Extraction Window**.
- **Pre-Battle Fire Plan**.

Design notes:

- Covert Operator proves that Operator does not mean hacker only.
- This archetype should rely more on preparation and battle context than raw Control scaling.

### Champion Build Grammar

Approved direction:

1. Use a consistent Champion build grammar for design docs, not necessarily as player-facing structure.
2. Every Champion should have a strategic-map specialty.
3. Every Champion should have soft preferred army composition rather than hard restrictions.
4. Champion abilities may allow specialization in particular creature/unit types, similar in spirit to HoMM4 creature specialization.
5. Every Champion should have an explicit weakness/counterplay note.

Design-doc build grammar:

| Field                          | Purpose                                                                                                     |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| **Archetype pole**             | Marshal, Operator, or Hybrid.                                                                               |
| **Stat lean**                  | Top stats, secondary stats, and weak stats.                                                                 |
| **Primary channels**           | Doctrine, Signal, Logistics, Fire Support, Covert, Bio, Echo, or special/factional channels.                |
| **Army preference**            | Soft preference: melee, ranged, fast, armored, swarm, elite, expendable, mixed, etc.                        |
| **Unit specialization**        | Optional explicit synergy with a creature/unit line, role, tier, faction roster segment, or upgrade family. |
| **Signature Doctrine**         | Passive/conditional army-shaping identity.                                                                  |
| **Core Minor Commands**        | Repeated active tools that keep the Champion tactically present.                                            |
| **Signature Major Operations** | High-impact prepared interventions.                                                                         |
| **Strategic-map specialty**    | Map movement, supply, scouting, site control, recruitment, recovery, political accounting, etc.             |
| **Weakness / counterplay**     | What opponents can exploit; what this Champion is bad at.                                                   |

Design notes:

- The grammar is for internal consistency and future faction/Champion authoring, not a rigid player-facing template.
- Preferred army composition should create incentives, not invalid rosters.
- Unit specializations can give HoMM-like personality: e.g. stronger recon drones, better ranged militia, improved biotech brutes, cheaper Echo support units, better armored squads.
- Avoid making every Champion a narrow creature specialist; specialization should be one possible build texture.
- Weakness/counterplay notes are required so Champions do not become purely additive power bundles.

### Champion / Unit Specialization Rules

Approved direction:

1. Champion unit specialization can be both role-based and specific-unit-line based.
   - Role-based specializations are common: ranged, melee, drone, infantry, armor, swarm, support, etc.
   - Specific unit-line specializations are rarer and more characterful.
2. Specialization affects upgraded variants in the same unit family by default.
3. Specialization bonuses should mix a small numeric baseline with one flavorful rule-changing effect.
4. Some Champions can use specialization to make unusual or off-faction rosters viable.
5. Numeric specialization bonuses may scale with Champion level; rule-changing effects are usually fixed.

Design notes:

- Specialization should create army-building texture without hard-locking the player into a single roster.
- Specific unit-line specialization is useful for HoMM-like personality: a Champion known for one creature/unit family can make that line feel iconic.
- Role-based specialization is safer for balance and easier to reuse across factions.
- Off-faction specialization should be intentional and lore-supported, not a universal optimization exploit.
- If an upgraded variant radically changes role, the specialization may need an explicit exception.

Example specialization shapes:

- **Ranged Specialist** — ranged stacks gain small accuracy/damage reliability; once per round, one ranged stack may use a Minor Command to reposition before firing.
- **Recon Drone Specialist** — recon drone family gains initiative/scouting value; upgraded variants also improve Sensor Lock or reveal radius.
- **Armored Infantry Specialist** — armored infantry family gains small Defense scaling; once per battle, a specialized stack can ignore a suppression penalty.
- **Street Militia Organizer** — low-tier militia/expendable units gain Cohesion resilience; off-faction irregulars suffer reduced mixing penalty.
- **Biotech Handler** — one Bio unit family gains regeneration/recovery scaling; rule effect may interact with Growth Surge or Tissue Reclamation.

### Champion Recruitment and Availability

Approved direction:

1. Champion availability uses a hybrid pool: faction Champions plus neutral/mercenary Champions.
2. Every faction should have both Marshal and Operator options, but faction proportions/skews differ.
3. Some neutral Champions may be recruitable only from map sites/events.
4. Champion availability strongly reinforces faction philosophy.
5. Recruitment uses a hybrid model: curated roster with rotating availability.

Design notes:

- Faction Champion pools should express the faction's worldview, command culture, economy, legitimacy, and preferred army shapes.
- Every faction needs access to both Marshal and Operator play, but not in equal proportions.
  - A militarized faction may have many Marshals and fewer Operators.
  - A Signal/corporate/intelligence faction may have many Operators and fewer pure Marshals.
  - A logistics/industrial faction may blur Marshal/Operator through supply and infrastructure play.
- Neutral/mercenary Champions can enable unusual rosters, off-faction synergies, or special map-site stories.
- Map-site/event Champions should be mostly neutral/special cases, not the default way to access core faction identity.
- Rotating availability preserves HoMM tavern-like texture, while curated rosters prevent random incoherence.

Recruitment model sketch:

- **Faction roster** — known pool of Champions associated with a faction/town.
- **Recruitment rotation** — a limited subset available at a given time/location.
- **Neutral/mercenary roster** — broader pool that may appear through taverns, contracts, event sites, or campaign state.
- **Site/event Champion** — special neutral or narrative Champion unlocked by visiting, controlling, or resolving a map site.

### Champion Defeat, Retreat, and Persistence

Approved direction:

1. Use HoMM-like loss of Champion control rather than routine literal permanent death.
2. If a Champion is defeated without successful retreat/extraction, they are removed from the player's roster and enter a lost/random/capture-style pool.
3. Permanent Champion death is rare and reserved for special conditions, scenarios, hardcore rules, executions, or faction/narrative mechanics.
4. Champion retreat/extraction depends on Logistics, Supply State, Extraction tools, and battle conditions.
5. Champion injury/cooldown occurs mainly if retreat/extraction fails.
6. Capture, ransom, interrogation, or equivalent high-stakes recovery systems may exist as rare events.
7. Echo/Bio-specific defeat interactions are deferred to faction design.

Outcome model:

| Outcome                           | Trigger                                                                    | Consequence                                                                                                                                                                   |
| --------------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Extracted / Retreated**         | Player retreats, surrenders, or uses valid extraction before total defeat. | Champion returns to a valid recruitment/base point. Army/supplies/tempo may be lost, but Champion control is preserved.                                                       |
| **Defeated / Lost**               | Army loses and Champion does not successfully extract.                     | Champion leaves player's roster and enters a lost/missing/random/capture-style pool. They may later reappear through recruitment, events, ransom, or even enemy availability. |
| **Captured / Burned / Disavowed** | Special defeat condition, enemy ability, site rule, or campaign event.     | Champion becomes a recovery objective, bargaining chip, intelligence risk, or temporarily unavailable asset.                                                                  |
| **Permanently Dead / Gone**       | Rare special condition.                                                    | Champion is permanently removed. Use sparingly to avoid save-scumming and narrative breakage.                                                                                 |

Design notes:

- This preserves HoMM/Olden Era texture: losing a battle can cost access to a developed Champion, not merely wound them for free.
- Routine true permadeath is avoided because Champions may carry narrative identity, progression, faction philosophy, and unique Operations.
- Loss of control is still serious: the player may lose tempo, artifacts/assets, army, map position, and access to that build.
- High Logistics and prepared Extraction tools should make retreat/recovery more reliable.
- Being Cut Off, surrounded, jammed, deep in hostile territory, or under special enemy control should make extraction harder.
- The system should support rare stories where a lost Champion later appears as neutral, mercenary, coerced enemy, ransom target, or altered Echo/Bio case.

### Champion Assets

Approved direction:

1. Use **Assets** as the artifact-equivalent term.
2. Champions have fixed equipment-style slots, plus general command-layer asset slots.
3. Assets include both personal and command-layer assets.
4. Assets can be lost or contested on Champion defeat, like HoMM artifacts.
5. Assets may unlock Operations and Doctrines, not only stat bonuses.

Asset slot model:

- **Personal slots** — cyberware, implants, weapons, armor modules, sensory rigs, neural interfaces, bodyguards, signature gear, or other Champion-adjacent equipment.
- **Command-layer slots** — drones, relay access, logistics packages, fire-support contracts, blackmail files, legal permissions, field labs, Echo archives, tactical AIs, transport assets, or faction credentials.

Design notes:

- Fixed slots preserve the readable artifact/equipment game from HoMM while fitting cyberpunk asset fantasy.
- Personal slots can feel closer to Shadowrun-style cyberware/equipment constraints.
- Command-layer asset slots represent off-board power: what the Champion can call, access, threaten, deploy, or authorize.
- Asset loss on defeat makes Champion defeat strategically serious and gives opponents meaningful spoils.
- Not every asset should be lootable in the same way: some may be physical, some contractual, some faction-bound, some compromised, and some burned/disavowed.

Example asset effects:

- **Targeting Relay** — improves Signal Operations or unlocks Sensor Lock variant.
- **Fire-Support Contract** — unlocks a limited Fire Support Operation.
- **Field Clinic Package** — improves post-battle recovery or unlocks Field Repair for eligible units.
- **Black Ledger** — strengthens Covert/False Flag strategic Operations.
- **Echo Archive Key** — enables a rare Echo Operation or improves Continuity effects.
- **Combat Exoskeleton** — personal asset that improves Marshal survivability/retreat odds or a Defense-scaling Minor Command.

### Asset Slot Structure and Intel Upgrades

Approved direction:

1. Personal Asset slots are body/location based and also include generic personal slots.
2. Command-layer Asset slots are generic in UI, but Assets may have typed requirements, tags, or exclusivity rules.
3. Marshals and Operators use the same slot structure, but different Assets are more useful to different archetypes.
4. Assets have rarity/tiers and can be upgraded.
5. Asset upgrades use **Intel** as a strategic resource.
6. Some Assets are faction-bound or non-transferable, mostly strategic/command-layer Assets.

Reference note — Olden Era Alchemical Dust:

- Public references describe Alchemical Dust in HoMM: Olden Era as a limited progression resource used to upgrade artifacts and spells, with some building/unit uses.
- Reported sources include dismantling/destroying artifacts, map piles, labs/trading, sites/creature banks, faction laws/skills, and some passive generation.
- The relevant design lesson is: a scarce strategic resource can turn duplicate/unwanted loot into upgrade progress and make artifact/spell progression a map-economy decision.

Neon adaptation — Intel:

- **Intel** is Neon Champions' analogue to Alchemical Dust for the asset/operation layer.
- Intel is a strategic resource used for scouting, Asset upgrades, Operation preparation, covert/signal actions, and selected strategic unlocks.
- Intel is not the same as Signal. Signal is an Operation channel; Intel is a strategic resource.

Intel sources may include:

- Scouting and recon actions.
- Captured servers, archives, dossiers, blackmail files, targeting feeds, or field evidence.
- Dismantling/burning duplicate or unwanted Assets.
- Map sites: relay towers, data centers, clinics, archives, informant networks, abandoned labs, battlefield recorders.
- Covert missions, interrogation, post-battle exploitation, or successful False Flag/Feed Poisoning effects.
- Faction buildings or faction-specific laws/policies.

Intel uses may include:

- Upgrading Assets by tier or mode.
- Improving Operation variants or prepared Operation packages.
- Enhancing scouting/pre-battle information.
- Unlocking or improving strategic Operations.
- Paying costs for covert, Signal, legal, or information-war effects.
- Converting obsolete Assets into progress rather than dead inventory.

Slot model sketch:

- **Personal body/location slots** — Head/Neural, Torso, Arms, Legs, Implant/Cyberware, etc.
- **Generic personal slots** — sidearm, bodyguard, sensory rig, field kit, personal AI, or other Champion-adjacent gear.
- **Generic command-layer slots** — command Assets with requirements/tags rather than hard slot categories.

Command Asset requirement/tag examples:

- Requires Signal training.
- Requires Logistics stat threshold.
- Requires faction authorization.
- Requires map-site access.
- Counts as Fire Support.
- Counts as Heavy Support; cannot equip another Heavy Support Asset.
- Faction-bound; cannot be transferred or looted normally.

Design notes:

- Avoid over-segmenting command slots into Signal/Logistics/Fire Support/Covert slot UI unless playtesting proves generic slots are too unclear.
- Intel should be scarce enough that upgrading every Asset is impossible.
- Asset upgrades should create strategic decisions: upgrade a signature Asset, prepare more Operations, or invest in scouting/covert leverage.
- Losing upgraded Assets on defeat should hurt, but not always erase faction-bound strategic infrastructure.

### Asset Upgrade Design

Approved direction:

1. Asset upgrades use a hybrid model: simple linear tiers plus occasional branching choices.
2. Upgrading Assets may unlock new Operations.
3. Duplicate Assets can be dismantled for Intel, except unique/story Assets by default.
4. Faction-bound strategic Assets use normal Intel plus faction building/site requirements.
5. Intel is a global player resource for MVP.

Design notes:

- MVP should avoid overcomplicating Intel locality. A global Intel pool is easier to understand and balance.
- Local or faction-specific Intel can be added later if map control and information logistics need more depth.
- Linear tiers keep upgrade UX readable: Mk I → Mk II → Mk III.
- Branches should be occasional and meaningful, not attached to every Asset.
- Branching is best for signature Assets, high-rarity Assets, faction Assets, and Operation-unlocking Assets.
- Dismantling duplicates prevents inventory clutter and creates an Olden Era-like conversion loop from unwanted loot into strategic progression.
- Unique/story Assets should not normally be dismantled unless the story explicitly supports burning, selling, leaking, or disavowing them.

Example upgrade shapes:

- **Targeting Relay Mk I → Mk II → Mk III**
  - Improves Sensor Lock reliability/range.
  - High tier may unlock Jamming Screen or improve Counter-Intrusion.
- **Fire-Support Contract**
  - Tier improves number of uses or radius.
  - Branch A: precision strike.
  - Branch B: suppression barrage.
- **Black Ledger**
  - Tier improves Covert strategic leverage.
  - Branch A: False Flag unlock/improvement.
  - Branch B: ransom/interrogation/reputation leverage.
- **Field Clinic Package**
  - Tier improves recovery and post-battle casualty conversion.
  - High tier may unlock Field Repair or emergency stabilization.

### Champion Secondary Skills

Approved direction:

1. Champions have secondary skills in addition to primary stats, Operations, Doctrines, and Assets.
2. Secondary skills are broad skills with ranks and rank-linked perks.
3. Secondary skills include Operation channel skills.
4. Secondary skills also include classic HoMM-like skills adapted to Neon.
5. Skill slots are limited, forcing build identity.

Skill model:

- A secondary skill represents a broad competency.
- Each skill has ranks, e.g. Basic / Advanced / Expert, or equivalent tiering.
- Rank increases may grant passive scaling plus one or more perk choices.
- Champions cannot learn everything; limited skill slots create identity and replayability.

Operation channel skill examples:

- **Signal Training** — improves Sensor Lock, Spoof Targeting, Jamming, Counter-Intrusion, and network contest reliability.
- **Logistics Operations** — improves Emergency Resupply, Supply Corridor, Extraction Window, capacity recovery, and strategic supply manipulation.
- **Fire Support Coordination** — improves barrages, drone strikes, suppression fire, delayed missiles, and pre-battle fire plans.
- **Covert Operations** — improves Ambush Cell, Sabotage Kit, False Flag, Smoke Break, blackmail/leverage actions, and prepared-cell reliability.
- **Doctrine Mastery** — improves Rally, Hold the Line, Coordinated Assault, Battle Rhythm, formation effects, and Marshal sustained value.

Classic HoMM-like Neon skill examples:

- **Scouting** — better map vision, enemy army estimation, site intelligence, and pre-battle Operation preparation.
- **Recruitment** — improved access to units, mercenaries, specialists, neutral stacks, or faction roster refreshes.
- **Tactics** — better deployment, opening formation, first-round positioning, and battle-start options.
- **Leadership / Cohesion** — improves morale-equivalent reliability, Cohesion recovery, panic/suppression resistance, and mixed-roster stability.
- **Pathfinding / Mobility** — improves strategic movement, terrain penalties, convoy handling, and potentially retreat routes.
- **Intelligence** — improves Intel gain, Intel efficiency, asset dismantling returns, scouting interpretation, and information-war actions.
- **Economics / Influence** — improves contracts, upkeep, recruitment cost, faction relations, ransom, and political-accounting effects.

Design notes:

- Avoid duplicating primary stats too directly. Skills should modify rules, unlock options, or specialize channels rather than simply add +Attack/+Control.
- Operation channel skills should make channels deeper without making every Operator identical.
- Classic adapted skills help preserve HoMM readability.
- Limited skill slots are important because Assets, Operations, and unit specialization already add many build axes.

### Secondary Skill List Direction

Approved direction:

1. MVP may support a broader secondary skill list, around 16 skills, rather than an ultra-lean 8-12 list.
2. **Logistics Operations** and **Pathfinding / Mobility** remain separate.
   - Logistics Operations governs supply, extraction, reload/recovery, and logistics-flavored Operations.
   - Pathfinding / Mobility governs strategic movement, terrain, convoy handling, and route access.
3. **Intelligence** remains separate from Signal Training.
   - Intel is a strategic resource/economy and interpretation layer.
   - Signal is an Operation channel for tactical/network contest, jamming, spoofing, targeting, and counter-intrusion.
4. **Economics** and **Influence** are split into separate secondary skills.
5. Bio/Echo secondary skills are special/factional and appear only when relevant factions or Champion lines exist.

Economics scope:

- Credits/income efficiency.
- Upkeep and maintenance pressure.
- Recruitment, construction, or Asset upgrade discounts where appropriate.
- Market/trade/exchange rates.
- Contract affordability.
- Strategic infrastructure and faction economy hooks.

Influence scope:

- Mercenary and neutral recruitment access.
- Diplomacy-like effects.
- Ransom, capture, and negotiation leverage.
- Reputation, legitimacy, and public-accounting manipulation.
- Contract quality and political permissions.
- Hearts-and-minds, legal cover, deniability, and faction relations.

Design notes:

- Splitting Economics and Influence creates room for both hard-resource optimization and social/political leverage.
- Economics must avoid becoming a mandatory boring income tax skill; it needs situational hooks and opportunity costs.
- Influence should be more than “cheaper units”: it is the skill for legitimacy, contracts, public narrative, neutral access, and prisoner/ransom systems.
- Around 16 skills is an upper-bound target for MVP vocabulary, not permission to create filler skills.
- Bio/Echo skills should not be generic until the relevant faction identities are designed.

### Candidate Secondary Skill List

Approved direction:

1. The initial 16-skill list works as design vocabulary, with names expected to change later.
2. **Ranged Warfare** and **Shock Warfare** exist separately.
3. **Armor / Fortification** is renamed toward **Defensive Engineering**.
4. Drone Command and Urban Warfare need further decision before being core skills.

Initial 16-skill vocabulary:

Operation/channel skills:

1. **Signal Training**.
2. **Logistics Operations**.
3. **Fire Support Coordination**.
4. **Covert Operations**.
5. **Doctrine Mastery**.

Strategic/classic skills:

6. **Scouting**.
7. **Recruitment**.
8. **Tactics**.
9. **Leadership / Cohesion**.
10. **Pathfinding / Mobility**.
11. **Intelligence**.
12. **Economics**.
13. **Influence**.

Combat/army skills:

14. **Ranged Warfare**.
15. **Shock Warfare**.
16. **Defensive Engineering**.

Optional / later / factional candidates:

- **Bio Systems**.
- **Echo Continuity**.
- **Drone Command**.
- **Urban Warfare**.
- **Naval / Air Mobility**.
- **Legal Warfare**.
- **Media Operations**.

Design notes:

- Skill names are provisional. The list is a mechanical vocabulary, not final UI naming.
- Ranged Warfare and Shock Warfare should remain distinct because ranged capacity/ammo/lanes and assault/melee/breach tempo create different army identities.
- Defensive Engineering covers armor, fortification, hardpoints, fieldworks, defensive preparation, and protection systems better than a narrow Armor/Fortification label.
- Drone Command is not a core MVP secondary skill; model drones through units, Assets, Operations, unit specialization, and optional/factional skills later.
- Urban Warfare is folded into Tactics for MVP; it can reappear as Tactics perks, Covert/Pathfinding/Defensive Engineering perks, Assets, sites, faction skills, or Champion specializations.

### Skill Ranks and Perks

Approved direction:

1. Secondary skills use 3 ranks: **Basic / Advanced / Expert**.
2. Each skill rank grants a fixed baseline effect so skill value remains predictable.
3. Some skills also offer subperks/subskills; others remain direct rank upgrades.
4. When a skill has subperks, they are chosen at **Advanced** and **Expert**, not at Basic.
5. Level-up offers new skills and rank-ups together, HoMM-like.
6. Every Champion has the same maximum number of secondary skill slots.
7. The working cap is **8 secondary skills per Champion**.
8. Because Champions can learn up to 8 skills, the total skill list should be broad enough to preserve build exclusion.

Design notes:

- Basic / Advanced / Expert is locked because it is readable, preserves HoMM familiarity, and is already established by reference-game analysis.
- Fixed baselines prevent subperk choice from making skill value opaque.
- Selective subperks add build texture without forcing all 24 skills to become full trees.
- Subperks are best reserved for skills where branching creates real identity, e.g. Edge, Signal Training, Covert Operations, Media Operations, Tactics, Leadership / Cohesion, or faction-flavored special skills.
- Skills with narrower utility can remain clean direct upgrades.
- New-skill and rank-up choices should appear together so level-up decisions feel close to HoMM.
- An 8-skill cap works well only if the total available skill pool is large enough that Champions cannot cover everything important.
- If the available pool remains near 16, an 8-skill cap may allow too much coverage; expand the candidate list or enforce archetype/faction offer weighting.

### Expanded Secondary Skill Pool

Approved direction:

1. Target total secondary skill pool size is roughly 24-26 skills.
2. Add **Medical / Recovery**.
3. Add **Asset Management**.
4. Add **Siege / Breachcraft**.
5. Add **Psychological Warfare**.
6. Add **Counterintelligence**.

Expanded core candidate list:

1. **Signal Training**.
2. **Logistics Operations**.
3. **Fire Support Coordination**.
4. **Covert Operations**.
5. **Doctrine Mastery**.
6. **Scouting**.
7. **Recruitment**.
8. **Tactics**.
9. **Leadership / Cohesion**.
10. **Pathfinding / Mobility**.
11. **Intelligence**.
12. **Economics**.
13. **Influence**.
14. **Ranged Warfare**.
15. **Shock Warfare**.
16. **Defensive Engineering**.
17. **Medical / Recovery**.
18. **Asset Management**.
19. **Siege / Breachcraft**.
20. **Psychological Warfare**.
21. **Counterintelligence**.

Candidate skills still available to reach 24-26 if needed:

22. **Training / Drilling** — improves unit XP, readiness, specialization depth, and roster reliability.
23. **Engineering / Infrastructure** — map-site repair, infrastructure control, fieldworks, roads, relays, production hooks.
24. **Legal Warfare** — permissions, sanctions, warrants, legitimacy, corporate personhood leverage.
25. **Media Operations** — public narrative, reputation, propaganda, attention, hearts-and-minds effects.
26. **Black Market** — illicit assets, smuggling, forbidden units, deniable contracts, contraband Intel conversion.
27. **Air / Drone Mobility** — optional/factional mobility and remote-platform support if needed later.

New skill scopes:

- **Medical / Recovery** — casualty conversion, wounded recovery, field stabilization, biological repair, trauma systems, post-battle readiness.
- **Asset Management** — Asset slot efficiency, Intel upgrade discounts, dismantling returns, maintenance, transfer/recovery odds, signature Asset depth.
- **Siege / Breachcraft** — attacking towns, bunkers, arcologies, gates, hardpoints, shielded sites, and fortified map objectives.
- **Psychological Warfare** — Cohesion attacks, fear/confusion, propaganda shocks, surrender pressure, morale-equivalent manipulation, intimidation.
- **Counterintelligence** — resistance against Covert/Signal/Intel attacks, detection of sabotage, protection from False Flag/Feed Poisoning, safer operations.

Design notes:

- 24-26 skills plus an 8-skill Champion cap should create meaningful build exclusion.
- Added skills must earn their place with real mechanics; do not add filler just to hit a number.
- Some optional candidates may become factional instead of universal.
- Counterintelligence should not invalidate Covert/Signal; it should create preparation/counterplay.

### HoMM Skill Reference Lessons

Research summary:

- HoMM3 secondary skills include combat skills such as Offense, Armorer, Archery, Tactics, Artillery, Ballistics, and First Aid; magic skills such as Wisdom, Sorcery, Intelligence, Mysticism, Air/Earth/Fire/Water Magic, and Resistance; and adventure/economy skills such as Logistics, Pathfinding, Scouting, Navigation, Estates, Diplomacy, Scholar, Learning, Eagle Eye, Luck, Leadership, and Necromancy.
- HoMM4 uses primary skill families with subskills, e.g. Tactics contains Offense/Defense/Leadership, Combat contains Melee/Archery/Magic Resistance, Nobility contains Estates/Mining/Diplomacy, and Scouting contains Pathfinding/Seamanship/Stealth.
- HoMM5/Olden Era keep Basic/Advanced/Expert readability, 8 skill cap, faction skills, sub-skills/perks, and synergies between skills.

Coverage notes:

- Offense/Archery are covered by Ranged Warfare, Shock Warfare, and Fire Support.
- Armorer/Defense are covered by Defensive Engineering.
- Tactics and Leadership are already represented.
- Logistics/Pathfinding are intentionally split into Logistics Operations and Pathfinding / Mobility.
- Estates/Economy and Diplomacy are represented by Economics and Influence.
- Scouting, Intelligence, Ballistics/Siege, and First Aid are represented.
- Magic schools are represented by Operation channel skills.
- Necromancy-like design is represented by Bio/Echo factional skills later.
- Resistance/Interference is partially represented by Counterintelligence, Defensive Engineering, and Leadership/Cohesion.

Additional ideas identified, not locked:

- **Edge** — Luck-equivalent skill. Represents engineered luck, nerve, opportunism, favorable breaks, backup plans, and high-risk success windows.
- **Contingency** — related but more planned/redundancy-focused than Edge; could become a perk, Asset tag, or separate skill later.
- **Operational Security / Hardening** — broader Resistance analogue against hostile Operations, jamming, spoofing, disruption, and Command attacks.
- **Support Systems / Battlecraft** — War Machines analogue for turrets, med-drones, relays, mines, decoys, and other deployed support platforms.
- **Insight / Operational Analysis** — Scholar/Wisdom/Eagle Eye analogue for learning Operations, interpreting sites, previewing enemy capabilities, and deriving knowledge from encounters.
- **Stealth / Infiltration** — HoMM4 Stealth analogue; currently folded into Covert Operations for MVP.
- **Navigation / Seamanship analogue** — only relevant if sea, air, orbital, undercity, or other special movement layers become prominent.

Current preference:

- Add **Edge** as the Luck-type skill candidate.
- Keep Contingency and the other identified ideas as design options, not locked core systems yet.

### Current Core Secondary Skill Pool

Approved direction:

1. Lock the following 24-skill pool as the current working core.
2. **Edge** is a universal core skill.
3. **Counterintelligence** remains core.
4. **Media Operations** remains core.
5. **Engineering / Infrastructure** remains separate from **Defensive Engineering**.

Current working core skills:

1. **Signal Training**.
2. **Logistics Operations**.
3. **Fire Support Coordination**.
4. **Covert Operations**.
5. **Doctrine Mastery**.
6. **Scouting**.
7. **Recruitment**.
8. **Tactics**.
9. **Leadership / Cohesion**.
10. **Pathfinding / Mobility**.
11. **Intelligence**.
12. **Economics**.
13. **Influence**.
14. **Ranged Warfare**.
15. **Shock Warfare**.
16. **Defensive Engineering**.
17. **Medical / Recovery**.
18. **Asset Management**.
19. **Siege / Breachcraft**.
20. **Psychological Warfare**.
21. **Counterintelligence**.
22. **Engineering / Infrastructure**.
23. **Media Operations**.
24. **Edge**.

Deferred / factional / idea-space skills:

- **Training / Drilling**.
- **Legal Warfare**.
- **Black Market**.
- **Air / Drone Mobility**.
- **Drone Command**.
- **Bio Systems**.
- **Echo Continuity**.
- **Contingency**.
- **Operational Security / Hardening**.
- **Support Systems / Battlecraft**.
- **Insight / Operational Analysis**.
- **Stealth / Infiltration**.
- **Navigation / Seamanship analogue**.

Design notes:

- Edge being universal preserves the HoMM Luck role while translating it into cyberpunk terms: nerve, favors, opportunism, backup plans, lucky breaks, and engineered uncertainty.
- Counterintelligence remains core because hostile Covert/Signal/Intel play needs readable counterplay.
- Media Operations remains core because control of narrative, reputation, and attention is central to Neon Champions.
- Engineering / Infrastructure is map-site and infrastructure control; Defensive Engineering is battlefield protection, fortification, armor, and hardpoint defense.

### Skill Offer Rules

Approved direction:

1. Champions receive **3 skill choices** on level-up.
2. Level-up offers use structured slots: **one existing-skill upgrade**, **one new skill**, and **one wildcard**.
3. Champion archetype and faction both weight skill offers.
4. Map sites/buildings can teach skills outside normal level-up.
5. Core skills are generally not hard-banned by Champion class/archetype; they are weighted by rarity. Hard restrictions are reserved for faction/special skills or explicitly exceptional skills.

Baseline level-up offer model:

```text
On level-up, offer up to three choices:
1. Upgrade Slot — improve one already-known skill that is not at maximum rank.
2. New Skill Slot — learn one skill not currently known, selected from the weighted eligible pool.
3. Wildcard Slot — can be an upgrade, a new skill, a rare off-archetype skill, faction-flavored offer, or special event/context offer.
```

Reference-game rationale:

- **HoMM3** uses two choices with a strong hidden structure: usually one existing-skill upgrade and one new class-weighted skill. It also supports outside-level skill learning through adventure-map sites such as Witch Huts, Universities, Scholars, and events.
- **Olden Era** publicly confirms heroes can improve an existing skill or choose a new one, keeps the 8-skill cap, uses faction iconic/starting skills, and adds subskill/subclass agency. Public information does not yet clearly confirm its exact offer-weighting algorithm.
- **Songs of Conquest** leans harder into faction/class-constrained Wielder development, with random level-up offers shaped by class/faction pools rather than a fully universal pool.
- **Age of Wonders 4** uses deterministic skill trees instead of random offers; this gives high planning clarity but loses some HoMM-style discovery and adventure-map spice.

Design notes:

- The 3-slot structure is the recommended Neon Champions compromise: more agency than HoMM3's two choices, less deterministic than a pure skill tree.
- The Upgrade/New/Wildcard pattern preserves the HoMM3 upgrade-vs-new rhythm while giving room for Neon-specific faction, site, sponsor, cybernetic, Echo, or narrative surprises.
- Weighting by both archetype and faction should create recognizable Champion identities without making every Champion build deterministic.
- Off-archetype core skills should be rare, not forbidden, unless a specific design reason exists. This keeps surprising builds possible.
- Map-taught skills are strategically valuable and very HoMM-compatible, but should be controlled: use them as memorable site rewards, faction infrastructure, black-market clinics, academies, trainers, datavaults, Echo shrines, or corporate certification programs rather than as common filler rewards.

Open tuning questions / prior-decision check:

- **Skill cap:** earlier design notes already use an **8-skill Champion cap** as the working assumption. Do not re-open unless deliberately overriding it.
- **Rank ladder:** **Basic / Advanced / Expert** is now locked as the Neon Champions secondary-skill rank ladder.
- **Subperks:** some skills have subperk/subskill choices at Advanced and Expert; others remain direct rank upgrades.
- **Wildcard slot:** can rarely offer skills outside normal faction/archetype weighting.
- **Faction/special skills:** are not offered by ordinary wildcard rolls; they require explicit events, sites, story context, or other authored triggers.
- **Map-taught skills:** use a site-specific whitelist rather than a broad random/global pool.
- **8-skill cap:** map sites do not bypass the cap directly. If a Champion is full, the site may create a replacement choice instead.
- **Map-site upgrades:** only special academy/university-type sites can upgrade existing skills; ordinary teaching sites mostly teach new skills from their whitelist.

### Champion Starting Skills

Approved direction:

1. Champions usually start with **2 secondary skills**.
2. One starting skill expresses faction identity.
3. One starting skill expresses Champion archetype, role, or personal identity.
4. Faction/iconic starting skills are generally fixed, but the fixed skill can depend on whether the Champion is a **Marshal** or **Operator**.
5. Rare signature Champions may break the normal faction/archetype starting-skill pattern if their concept justifies it.

Baseline model:

```text
Starting Skill 1 — Faction / Role Iconic
- Usually fixed by faction + Champion role family.
- A faction may have one Marshal iconic skill and one Operator iconic skill.

Starting Skill 2 — Archetype / Personal
- Chosen from the Champion's archetype, specialization, biography, or signature playstyle.
```

Design notes:

- This preserves faction philosophy without making all Champions from the same faction feel identical.
- Marshal/Operator split matters because a faction's military doctrine and operational doctrine may express the same ideology through different systems.
- Example pattern: a faction might push Marshals toward Leadership / Cohesion, Ranged Warfare, Shock Warfare, or Defensive Engineering, while Operators from the same faction lean toward Signal Training, Covert Operations, Media Operations, Intelligence, or Logistics Operations.
- The second starting skill is where named Champions can become specific: a propaganda officer, siege architect, smuggler-prince, trauma surgeon, Echo cultist, or fire-control savant should not all collapse into the same faction template.
- Exceptions should be rare and intentional, not random noise.

## AP Abilities Group

> Current working label: **AP abilities group**.

This group contains Champion/faction/rare elite abilities that temporarily alter the simple 2 AP combat economy. These should be premium command-layer or signature identity moments, not ordinary unit spam.

Approved direction:

1. MVP +AP sources may come from **Champions, faction mechanics, and rare elite unit abilities**.
2. +AP effects should be **rare but build-defining**, with several possible sources constrained by cooldowns, charges, Command/resource costs, or opportunity costs.
3. Normal tactical cases use a hard cap of **3 total AP on a stack in one turn**.
4. +AP effects usually cost cooldowns/charges plus Command/resource/opportunity cost. Risk tradeoffs such as self-damage, exposure, Jammed/Hacked vulnerability, heat, or morale stress are reserved for faction flavor and special abilities.
5. AP refund effects, such as kill-refunds, may exist only as Champion/faction signature effects and should be capped at **once per stack per turn**.

Design law:

```text
AP is stable by default. Breaking AP rules is a Champion, faction, or rare elite identity moment. A normal stack should not exceed 3 AP in one turn.
```

### Candidate Abilities

| Ability                               | Source                                   | Draft Effect                                                                                           | Design Notes                                                       |
| ------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| Command Burst                         | Champion                                 | Target allied stack gains +1 AP this turn.                                                             | Clean, readable, very strong. Needs cooldown/charge limit.         |
| Tactical Uplink                       | Champion / network faction               | Networked allied stacks in radius gain +1 AP; affected stacks become more vulnerable to EMP/hacking.   | Strong cyberpunk tradeoff: tempo for network exposure.             |
| Overclock                             | Champion / cybernetic or biotech faction | Target gains +1 AP and possibly damage; suffers heat, stress, self-damage, or vulnerability afterward. | Good for body-subscription/cybernetic themes.                      |
| Emergency Protocol                    | Champion / doctrine trait                | A stack that kills an enemy refunds 1 AP once per turn.                                                | Snowball-prone; use carefully.                                     |
| Drone Relay                           | Champion / drone faction                 | Champion spends command resource or AP to let a drone stack act immediately or gain +1 AP.             | Makes command infrastructure tactically meaningful.                |
| Echo Possession / Continuity Override | Champion / Echo faction                  | Temporarily grants AP to a wounded, disabled, or collapsing stack so it can act before destruction.    | Strong Neon Champions identity; links combat to death/Echo themes. |

### Balance Constraints

- Extra AP should usually come from the Champion, faction identity, or rare elite unit identity, not ordinary stack abilities.
- +1 AP to a stack is a major effect because it can enable move + attack + defend, triple attack if ammo allows, or attack + reload + attack.
- AP grants need visible UI/FX so players understand why a stack acted more than expected.
- AP manipulation must be constrained by cooldown, charges, command resource, risk, positioning, or faction weakness.
- Avoid permanent AP inflation in MVP.
- Normal tactical cases cap a stack at 3 total AP in one turn.
- AP refunds are especially snowball-prone; keep them signature and cap them at once per stack per turn.
