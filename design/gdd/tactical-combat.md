---
title: Tactical Combat
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-28
updated: 2026-05-28
source_lore: []
related: [design/gdd/game-concept, design/gdd/game-pillars, design/gdd/systems-index, design/gdd/faction-unit-rosters]
approval: pending
---

# Tactical Combat

> Status: Draft. Do not use for implementation yet.

## Summary

Neon Champions tactical combat is intended to combine HoMM-style army/faction identity with cyberpunk XCOM-lite tactical choices. The MVP combat board is flat: no elevation or multi-level terrain. Tactical depth should come from brutally simple AP, movement, ranged/melee roles, ammo/charge pressure, Champion command abilities, and faction-specific rule bending.

> Quick reference — Layer: Core · Priority: MVP · Key deps: Champions, Factions, Faction Unit Rosters, Strategic Map, Resources

## Current Design Direction

- Avoid full XCOM complexity for MVP.
- Target feel: Shadowrun Returns / Dragonfall / Hong Kong tactical simplicity, with HoMM-like strategic battle frequency and army identity.
- AP is stable by default; breaking AP rules is a Champion/faction identity moment.
- Elevation/high ground is explicitly deferred.
- Combat should remain fast enough for repeated strategy-map encounters.

## MVP Scope Constraints

### In Scope

- Flat grid battlefield.
- Simple action point economy.
- Different movement values by unit/stack.
- Melee and ranged attacks.
- Ammo, magazine, charge, or heat limits for ranged/special units where useful.
- Champion abilities that can manipulate AP for allied stacks.
- Defensive fallback action.

### Out of Scope for MVP

- Height/elevation.
- Multi-floor tactical maps.
- Complex vertical pathfinding.
- Full XCOM-style simulation stack.
- Universal overwatch for every ranged unit.
- Deep hacking minigame inside every battle.

## Activation, Initiative, AP, Wait, and Defend

### Approved Direction

1. Combat uses an initiative-ordered stack activation model.
2. Each stack acts once per round.
3. Initiative determines activation order within the round; higher-Initiative stacks act earlier.
4. Initiative can be bumped, delayed, or manipulated by abilities/status effects, but does not normally grant extra activations.
5. Each stack has 2 AP by default at the start of its activation.
6. AP does not carry over between turns or rounds.
7. Baseline AP does not vary by unit class, tier, or upgrade level; upgraded/elite units should usually gain better stats, initiative, movement, abilities, traits, ammo/charge, or conditional tempo effects rather than permanent 3 AP.
8. Most actions cost 1 AP.
9. Heavy/signature actions cost 2 AP.
10. Extra AP is rare, temporary, highly visible, and usually comes from a Champion/faction mechanic.
11. Fast units should usually gain more tiles per Move action, not more baseline AP.
12. More units in a stack increase damage/survivability, not number of actions.

### Wait

Wait is HoMM-like delay, not AP banking.

```text
Wait: delay this stack's activation until later in the same round. The stack retains its current AP for that later activation window. AP still does not carry into future rounds.
```

Design notes:

- Wait is used to let enemies commit first, set up combos, or avoid wasting actions before targets enter range.
- Wait should not allow a stack to act twice in the same round.
- Wait should not preserve AP into the next round.
- Initiative-bump abilities may interact with Wait, but must not create infinite activation loops.

### Defend

Defend is HoMM-like: it ends the stack's activation and grants a defensive bonus.

```text
Defend: end this stack's activation and gain a defensive bonus until its next activation.
```

Design notes:

- Defend is chosen when the stack cannot make a useful attack, wants to hold position, or expects incoming damage.
- Defend does not cost 1 AP in the final model; it consumes/end the remaining activation.
- Defend competes with Wait: Wait preserves tactical timing; Defend sacrifices timing for protection.

## Base Actions

| Action | AP Cost | Notes |
|---|---:|---|
| Move | 1 | Move up to the stack's Move value. |
| Basic Attack | 1 | Standard melee or ranged attack. |
| Heavy / Signature Attack | 2 | Stronger attack, burst, charge, artillery strike, etc. |
| Reload / Recharge | 1 | Refills magazine, charge, heat capacity, or equivalent. |
| Defend | End activation | HoMM-like defensive action; consumes remaining activation and grants defensive bonus. |
| Overwatch | 1 | Not universal; only available to units/stacks with the relevant trait. |
| Simple Ability | 1 | Tactical utility, light faction ability, minor Champion-granted action. |
| Major Ability | 2 | High-impact tactical ability. |
| Interact / Objective | 1 | Capture, extract, activate, sabotage, loot, or mission-specific action. |

## Defend / Brace Direction

Use one clean player-facing action: **Defend**. Defend ends the stack's activation and grants a defensive bonus until its next activation.

Internally, the defensive behavior can be flavored per unit/faction:

- Heavy/melee units: Brace.
- Ranged units: Take Cover.
- Shield units: Guard.
- Drone units: Stabilize Platform.
- Biotech units: Harden Tissue.
- Echo units: Phase Anchor.

Baseline MVP effect candidate:

```text
Defend: End activation to gain a defensive bonus until this stack's next activation.
```

Candidate implementations to test:

- +25% damage reduction until next activation.
- +1 Armor and immunity/resistance to forced movement until next activation.
- Reduced suppression/disruption chance until next activation.

Open decision: choose one baseline Defend rule after prototype testing.

## Counterattacks, Zone of Control, and Overwatch

### Counterattack / Retaliation

Approved direction:

1. Most melee-capable stacks have a default retaliation/counterattack.
2. Retaliation triggers when the stack is attacked in melee.
3. Retaliation happens after the attacker deals damage, HoMM-style.
4. Retaliation does not cost AP.
5. Retaliation consumes a separate once-per-round retaliation resource.
6. By default, a stack can retaliate once per round.
7. First Strike may exist as a special trait/ability that retaliates or strikes before the attacker deals damage.

Design notes:

- This gives melee engagement HoMM-style bite without complicating the AP economy.
- Retaliation should be blocked if the stack is stunned, disabled, or otherwise unable to attack.
- Special traits may modify this rule later, such as No Retaliation, Unlimited Retaliation, First Strike, Shock Retaliation, or Suppressing Retaliation.

### Zone of Control

Approved direction:

1. Most melee-capable stacks project Zone of Control into adjacent tiles by default.
2. Enemy stacks inside a hostile Zone of Control are considered engaged.
3. Leaving an enemy Zone of Control triggers a retaliation/opportunity attack.
4. Retaliation and opportunity attacks use the same named once-per-round resource: **Retaliation**.
5. If a stack has already spent its Retaliation for the round, it cannot make an opportunity attack until Retaliation refreshes.
6. All units are vulnerable to Zone of Control by default.
7. Special traits/abilities may ignore, reduce, or alter Zone of Control later.

Design notes:

- This keeps the rule HoMM-compatible: opportunity attacks are not a new resource, they are another way to spend Retaliation.
- Future features may add penalties or bonuses for entering, standing in, or attacking from Zone of Control, but MVP behavior is leaving-ZoC triggers Retaliation.
- Candidate future traits: Disengage, Phase Step, Smoke Break, Unstoppable, Skirmisher, Guardian, Extended Reach.

### Overwatch

Approved direction:

1. Overwatch exists in MVP, but only for stacks with a specific Overwatch trait/action.
2. Overwatch is not a universal ranged-unit action.
3. Overwatch costs 1 AP.
4. By default, Overwatch grants one reaction shot before the stack's next activation.
5. Overwatch triggers when an enemy moves through the overwatching stack's line of sight / watched range.
6. Overwatch uses ammo/charge if the weapon normally uses ammo/charge.
7. Overwatch can be blocked or disrupted by status/effects such as Suppressed, Jammed, Hacked, smoke, stealth, or line-of-sight blocking.

Design notes:

- Overwatch adds cyberpunk/XCOM flavor without turning every ranged stack into a reaction-fire turret.
- Specialist units may later modify Overwatch with wider arcs, longer watched range, multiple shots, Signal-assisted targeting, or suppression fire.
- Counterplay must remain visible: players should understand why Overwatch did or did not fire.

## Damage Types, Weapon Tags, and Defense Tags

### Damage Types

Approved direction:

Neon Champions uses exactly five primary damage types:

1. **Kinetic** — physical harm: bullets, blades, fists, rail slugs, shrapnel, impact.
2. **Energy** — lasers, plasma, heat, microwave, directed-energy weapons.
3. **Shock** — EMP, electrical attacks, anti-shield, anti-drone, anti-cybernetic disruption.
4. **Chemical** — toxins, acid, corrosives, viral payloads, engineered agents.
5. **Signal** — hacking, spoofing, memetic attack, Echo disruption, command/network intrusion.

Combination rule:

- Attacks may combine damage types, but this should be uncommon and mostly reserved for special or advanced attacks.
- Basic/common attacks should usually have one primary damage type.

Piercing direction:

- Do not use Piercing as a damage type in the current model.
- Do not add a Piercing tag for now.
- If armor-bypass behavior is needed later, define it as a specific ability/weapon rule rather than a core damage category.

Signal scope:

- Signal primarily affects high-tech, networked, cybernetic, drone, command-linked, and Echo-related units.
- Signal has limited effect on analogue/low-tech/organic units unless a specific ability says otherwise.
- This supports the intended high-tech vs analogue tradeoff: powerful connected units can lose capabilities to spoofing/disruption, while simpler mass units are less vulnerable to Signal.

### Attack Description Model

Approved direction:

Do not create a formal weapon/attack tag system in the current design. Tags are likely to add muddled complexity unless they are clearly needed later for implementation.

Use three clearer concepts instead:

1. **Attack Delivery** — how the attack reaches the target.
2. **Damage Type** — what kind of harm/disruption it causes.
3. **Explicit Rules** — special behavior written directly on the unit/attack/ability.

Attack Delivery categories:

- **Melee** — adjacent or close-contact attack; interacts with Retaliation and Zone of Control.
- **Direct Ranged** — ranged attack requiring normal targeting/line of sight.
- **Indirect** — attack that can target without direct line of sight, subject to restrictions.
- **Area** — attack affects multiple tiles/stacks; can combine with Melee, Direct Ranged, or Indirect.

Example format:

```text
Smart Rifle
Delivery: Direct Ranged
Damage: Kinetic
Rule: Deals bonus damage to Marked targets.
Ammo: 1
```

```text
EMP Grenade
Delivery: Indirect Area
Damage: Shock
Rule: Applies Jammed to drones/cybernetic units.
Ammo/Charge: limited use
```

Design notes:

- HoMM-like special behavior should appear as explicit unit traits or attack rules, not broad abstract tags.
- If implementation later needs internal tags for AI, UI, or validation, those can be added as data-only implementation details without becoming player-facing design categories.

### Defense / Resistance Model

Approved direction:

1. Defense is not symmetrical to the five damage types.
2. Units use core durability values plus explicit resistance/vulnerability traits.
3. Core durability values are **HP**, **Armor**, and optional **Shield**.
4. Armor is mostly Kinetic-focused.
5. Shield is a separate durability layer for selected units only, not universal bonus HP.
6. High-tech/networked status is double-edged: it enables bonuses and advanced abilities, but increases vulnerability to Signal/Shock disruption.

Core durability values:

- **HP** — body/platform integrity; when depleted, the stack loses units or is destroyed.
- **Armor** — primarily reduces Kinetic damage; may interact with specific explicit rules.
- **Shield** — optional separate protection layer, often strong against direct damage but vulnerable to Shock/Signal-style disruption depending on unit rules.

Defense traits should be explicit unit traits, not a mirrored resistance table. Candidate traits:

- **Armored** — reduces incoming Kinetic damage.
- **Shielded** — has Shield as a separate protection layer.
- **Sealed** — resistant to Chemical effects.
- **Hardened Systems** — resistant to Shock disruption.
- **Analog** — resistant or immune to most Signal effects, but may lose access to high-tech/network bonuses.
- **Networked** — eligible for command/network bonuses, but vulnerable to Signal disruption.
- **Drone** — generally vulnerable to Shock/Signal and resistant or immune to Chemical, depending on unit design.
- **Organic** — generally more vulnerable to Chemical and less affected by Signal, depending on unit design.
- **Echo-Stable** — resists Signal/Echo disruption.

Design notes:

- This supports the desired "Ewoks vs Stormtroopers" tradeoff: expensive high-tech stacks are stronger while their systems work, but can lose capabilities when spoofed, jammed, EMP'd, or cut off; simple mass units are less flashy but harder to disable through Signal/Shock tricks.
- Do not expose five resistance columns by default. Show exceptions and important vulnerabilities clearly on the unit card.

### Stack Health and Damage Scaling

Approved direction:

1. Regular combat units are represented as multi-unit stacks.
2. Champions are not battlefield units; they are a commander layer affecting combat through abilities, doctrine, operations, morale/cohesion, logistics, and initiative/AP manipulation.
3. Each stack has a Unit Count and per-unit HP.
4. Stack total HP is derived from Unit Count × per-unit HP, plus any explicit modifiers.
5. Damage kills units as HP thresholds are crossed.
6. Partial damage carries over inside the stack.
7. Stack damage output scales down as units die, HoMM-style.
8. Factions and units may bend stack degradation rules through explicit traits/abilities.

Example:

```text
A stack has 5 units with 10 HP each.
It takes 15 damage.
1 unit dies, and 5 damage carries onto the next unit.
The stack now has 4 living units plus 5 carried damage on the front unit.
Its damage output scales from 5 units to 4 units unless a special rule says otherwise.
```

Design notes:

- This preserves HoMM-like army-stack identity and avoids drifting into XCOM/tactics-RPG individual-unit combat.
- Elite units should usually be represented as small high-quality stacks, not single entities. Example: a heavy drone platform unit might field as a stack of 2–4 platforms with high HP and strong abilities.
- Rare bosses, map objects, or special scenario entities may be considered later, but they are not part of normal recruitable army design.
- Candidate faction exceptions: Echo-backed stacks may preserve output briefly after casualties; drone swarms may degrade in steps; biotech masses may regenerate lost bodies; command-dependent high-tech stacks may degrade sharply if Signal-disrupted.

## Ammo, Capacity, Cooldowns, and Logistics

### Tactical Capacity Model

Approved direction:

1. Basic melee attacks are the only universally unlimited attack type.
2. Most ranged and special attacks use some limiter: capacity, cooldown, limited uses, logistics, or explicit scenario rules.
3. Standard ranged units track tactical Capacity/Magazine.
4. Use one unified **Capacity** system for ammo, charge, heat, battery, reservoir, payload, or bandwidth. The fiction varies by unit/weapon, but the core rule stays mostly the same.
5. Special abilities may use cooldowns, charges, or both, depending on ability type.

Capacity examples:

- Rifle: magazine.
- Railgun: capacitor.
- Laser: heat sink / charge cycle.
- Drone weapon: battery.
- Bio sprayer: reservoir.
- Signal attack: bandwidth / processing window.
- Missile pod: payload count.

### Reload / Recharge

Approved direction:

Reload/recharge has a 1 AP cost, but the UI should avoid unnecessary reload-button tedium.

Rules:

1. If a stack has Capacity, it can fire normally.
2. If a stack is empty and has supply/recharge access, its next ranged attack can automatically combine Reload + Fire.
3. Fire with Capacity: 1 AP.
4. Manual Reload/Recharge: 1 AP.
5. Reload + Fire while empty: 2 AP, if supply/recharge is available and the stack has enough AP.
6. If empty with only 1 AP remaining, the stack can reload/recharge but cannot fire in the same activation.
7. If logistics/supply is unavailable, reload/recharge may be limited or impossible depending on scenario and unit rules.

UI intent:

- Show **Fire: 1 AP** when loaded.
- Show **Reload + Fire: 2 AP** when empty but supplied.
- Show **Reload: 1 AP** when manually preparing.
- Show **No Supply** or equivalent when reload/recharge is blocked.

Design notes:

- This preserves tactical ammo pressure without turning reload into a repetitive button tax.
- HoMM-style frequent battles argue against mandatory manual reload clicks for ordinary ranged stacks.
- XCOM/Shadowrun-style reload costs are useful, but should be streamlined for stack-based combat.
- Strategic logistics will decide how plentiful reload/recharge access is in a given battle.

### Strategic Logistics and Supply State

Approved direction:

1. Tactical reload/recharge depends on a battle's strategic **Supply State**.
2. A HoMM Ammo Cart equivalent should exist as a logistics asset that improves reload/recharge access.
3. Fighting in friendly/controlled territory improves Supply State.
4. Infrastructure can further improve or stabilize Supply State.
5. Logistics is a faction identity axis: different factions can have different supply strengths, weaknesses, and methods.
6. Low-tech/analogue mass units are generally less supply-dependent than high-tech units.

Candidate Supply States:

- **Supplied** — normal reload/recharge access; most units can restore Capacity during battle.
- **Strained** — limited reload/recharge; reloads may be capped, slower, or restricted to some units.
- **Cut Off** — stacks start with initial Capacity only; no normal reload/recharge unless the unit has self-supply or a battlefield logistics asset.
- **Prepared / Over-Supplied** — better than normal; may grant extra starting Capacity, improved reload/recharge, or special logistics actions.

HoMM Ammo Cart equivalent:

- Working category: **Logistics Asset**.
- Candidate names by fiction/faction: Field Logistics Node, Supply Drone, Smart Munitions Crate, Salvage Cache, Battery Relay, Nutrient Vat, Spore Reservoir, Bandwidth Relay, Uplink Mast.
- Function: improves reload/recharge access, extends Capacity sustainability, or offsets poor Supply State.

Strategic-map implications:

- Fighting inside friendly/controlled territory should usually improve Supply State.
- Fighting beyond operational reach should reduce Supply State.
- Some factions may project supply better; others may scavenge, self-regenerate, or rely on network coverage instead of physical supply.
- Supply State should interact with area control on the strategic map.

Design notes:

- This connects tactical ranged/special-unit power to operational planning.
- Expensive high-tech armies should be powerful when supplied and networked, but brittle when cut off or disrupted.
- Low-tech/analogue mass armies should have fewer advanced options but better resilience under bad supply conditions.

### Indirect and Area Attacks

Approved direction:

1. Indirect attacks require spotting/targeting support unless the attack has a special rule.
2. Spotting/targeting support is usually electronic: drone vision, sensor lock, network mark, satellite/sky-feed cue, hacked camera, relay beacon, or similar.
3. Indirect attacks are mostly deterministic in MVP; avoid random scatter.
4. Powerful indirect attacks should be delayed and/or telegraphed.
5. Indirect/area attacks are primarily moderate damage plus status/position pressure, not high-randomness deletion tools.
6. Area attacks may flush units out of cover or punish clumping.
7. MVP counterplay should include moving out, spreading out, using cover/shields, and jamming/disabling the attacker or spotter.

Design notes:

- Indirect fire should not be a random missile that deletes stacks without counterplay.
- Heavy indirect attacks should create readable battlefield pressure: move, disperse, disable the spotter, jam targeting, or accept the hit.
- Electronic spotting creates a cyberpunk tradeoff: high-tech targeting enables powerful indirect fire, but can be disrupted through Shock/Signal tools.
- Area attacks can be used to break static cover play by applying pressure rather than simply dealing maximum damage.

Candidate restrictions for indirect attacks:

- Requires an allied spotter with line of sight.
- Requires a Marked / Sensor Locked target.
- Requires active network/logistics support.
- Has minimum range.
- Uses high Capacity or limited charges.
- Can be Jammed, Spoofed, or interrupted by disabling the spotter.
- Heavy versions telegraph impact before resolving.

## Morale / Cohesion

### Core Cohesion Model

Approved direction:

1. Use **Cohesion** as Neon Champions' morale-equivalent stat.
2. Cohesion covers morale, command integrity, squad coordination, signal discipline, ideological alignment, and faction/army synchronization.
3. Low Cohesion can cause negative events or penalties.
4. High Cohesion should grant stable bonuses rather than swingy positive tempo spikes.
5. Faction mixing reduces Cohesion by default unless Champion/faction traits, diplomacy, doctrine, or other systems mitigate it.
6. Everyone uses the same Cohesion system by default; exceptions should be explicit traits, not hidden category rules.

Low Cohesion candidate effects:

- Initiative penalty.
- AP penalty in severe cases.
- Reduced damage or accuracy.
- Weaker response to Champion commands.
- Higher vulnerability to Signal disruption or suppression.
- Chance of delayed/skipped action if the system later supports controlled randomness.

High Cohesion candidate effects:

- Stable initiative bonus.
- Better resistance to Suppressed/Hacked/Jammed effects.
- Improved Champion command reliability.
- Better Defend/Retaliation consistency.
- Reduced penalties from casualties or mixed forces.

Design notes:

- Cohesion should not create frequent random bonus turns; that would add too much swinginess.
- Different unit types can justify Cohesion fiction differently: drone Cohesion is command-link/swarm coordination; corporate Cohesion is doctrine/comms discipline; street Cohesion is trust and momentum; Echo Cohesion is identity continuity; biotech Cohesion is pack/body-control integrity.
- Candidate future traits may modify Cohesion behavior: Autonomous, Fanatical, Fragile Command Link, Echo-Stable, Coalition Doctrine, Analog Discipline.
- Keep the default rule universal for readability; add exceptions only when a unit/faction needs them.

### Cohesion Sources and Faction Mixing

Approved direction:

1. Army composition uses a hybrid model: basic faction mixing can reduce Cohesion, and specific compatibility/incompatibility rules may further modify it.
2. Mixed armies should also provide positive benefits: tactical flexibility, access to more damage types, abilities, logistics styles, and strategic options.
3. Champion identity can mitigate or worsen mixed-force Cohesion. Some Champions are coalition-builders; others demand faction purity, command discipline, or ideological alignment.
4. Battlefield events can affect Cohesion during combat.
5. Temporary combat Cohesion mostly resets/recalculates after battle, but strategic morale/cohesion problems may persist when caused by major events, campaign state, faction conflict, or specific systems.

Candidate composition factors:

- Number of factions represented in the army.
- Whether units share ideology, employer, command protocol, or operational culture.
- Whether a Champion has coalition/purity/discipline traits.
- Presence of incompatible units or hated rivals.
- Presence of mediating units, officers, handlers, translators, command relays, or doctrine assets.

Candidate positive reasons to mix factions:

- Broader damage type coverage.
- Better answers to specific defensive traits.
- Access to different movement profiles.
- Logistics flexibility.
- More tactical roles and utility abilities.
- Strategic diplomacy or recruitment opportunities.

Candidate battlefield Cohesion events:

- Friendly stack destroyed.
- Enemy stack destroyed.
- Champion command succeeds or fails.
- Stack is Suppressed, Hacked, Jammed, or hit by Signal attack.
- High-value/elite stack suffers casualties.
- Army is cut off from supply or network support.
- Unit acts adjacent to incompatible or inspiring ally.

Design notes:

- Mixing should be a real tradeoff, not an automatic mistake.
- Pure armies should be more coherent and easier to command.
- Mixed armies should be tactically broader but require Champion support, doctrine, logistics, or player planning to avoid Cohesion penalties.
- Avoid tracking persistent Cohesion damage for every small combat event; reserve persistence for major campaign-relevant problems.

## AP Abilities Group

> Current working label: **AP abilities group**.

This group contains Champion/faction abilities that temporarily alter the simple 2 AP combat economy. These should be premium command-layer moments, not ordinary unit spam.

Design law:

```text
AP is stable by default. Breaking AP rules is a Champion/faction identity moment.
```

### Candidate Abilities

| Ability | Source | Draft Effect | Design Notes |
|---|---|---|---|
| Command Burst | Champion | Target allied stack gains +1 AP this turn. | Clean, readable, very strong. Needs cooldown/charge limit. |
| Tactical Uplink | Champion / network faction | Networked allied stacks in radius gain +1 AP; affected stacks become more vulnerable to EMP/hacking. | Strong cyberpunk tradeoff: tempo for network exposure. |
| Overclock | Champion / cybernetic or biotech faction | Target gains +1 AP and possibly damage; suffers heat, stress, self-damage, or vulnerability afterward. | Good for body-subscription/cybernetic themes. |
| Emergency Protocol | Champion / doctrine trait | A stack that kills an enemy refunds 1 AP once per turn. | Snowball-prone; use carefully. |
| Drone Relay | Champion / drone faction | Champion spends command resource or AP to let a drone stack act immediately or gain +1 AP. | Makes command infrastructure tactically meaningful. |
| Echo Possession / Continuity Override | Champion / Echo faction | Temporarily grants AP to a wounded, disabled, or collapsing stack so it can act before destruction. | Strong Neon Champions identity; links combat to death/Echo themes. |

### Balance Constraints

- Extra AP should usually come from the Champion or faction identity, not ordinary stack abilities.
- +1 AP to a stack is a major effect because it can enable move + attack + defend, triple attack if ammo allows, or attack + reload + attack.
- AP grants need visible UI/FX so players understand why a stack acted more than expected.
- AP manipulation must be constrained by cooldown, charges, command resource, risk, positioning, or faction weakness.
- Avoid permanent AP inflation in MVP.

## Stack Action Principle

If combat uses HoMM-style stacks, each stack acts as one tactical entity.

Example:

- A stack of 8 Corporate Riflemen has 2 AP total.
- The stack may Move + Shoot, Shoot + Shoot, Reload + Shoot, or Overwatch + Defend.
- The stack's size modifies output/survivability, not action count.
- If a Champion grants +1 AP, the same stack can perform a third action this turn.

This prevents action-count explosion while preserving the power fantasy of larger forces.

## Deferred: Elevation / High Ground

Elevation is not part of MVP.

If revisited later, use a simple abstract rule before considering true vertical maps:

- High-ground tiles may grant +1 range, +damage, or improved hit/graze outcome for ranged attacks.
- Flying/jump units may ignore height penalties.
- Avoid multi-floor interiors and complex vertical pathfinding until proven necessary by playtests.

## Open Questions

| Question | Owner | Deadline | Resolution |
|---|---|---|---|
| Is tactical combat stack-based, individual-unit-based, or a hybrid? | shared | TBD | Pending. |
| What is the baseline Defend effect? | shared | TBD | Pending prototype. |
| Does Move consume AP, or is there separate free movement plus AP? | shared | TBD | Current draft assumes Move costs 1 AP. |
| Which AP abilities belong to Champions versus faction/unit traits? | shared | TBD | Current draft favors Champions/faction identity. |
| How often should normal battles occur on the strategy map? | shared | TBD | Impacts combat complexity budget. |
