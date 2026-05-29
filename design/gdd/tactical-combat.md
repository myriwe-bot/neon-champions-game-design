---
title: Tactical Combat
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-28
updated: 2026-05-29
source_lore: []
related: [design/gdd/game-concept, design/gdd/game-pillars, design/gdd/systems-index, design/gdd/faction-unit-rosters]
approval: pending
---

# Tactical Combat

> Status: Draft. Do not use for implementation yet.

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

### In Scope

- Flat grid battlefield.
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

## Army Composition and Battle Participation

Approved direction:

1. Baseline participation model: **all stacks in the active army deploy; the active army itself has limited stack slots**.
2. MVP has **no normal tactical reserve bench**.
3. Active army size uses a **fixed default slot count, modified only by Champion, Command, doctrine, or scenario rules**.
4. The player chooses or arranges participating stacks through **active-army management before battle**; all active stacks deploy.

Design contract:

- “Army” in tactical rules means the Champion's **active army**, not every unit the player owns, stores, garrisons, transports, sponsors, or can theoretically requisition.
- Active army slots are a strategic constraint. The player decides what belongs in those slots before combat through army management.
- Once battle begins, every surviving stack in those active slots normally appears in the tactical battle.
- Deployment rules may still affect **position, order, formation, surprise, or disrupted entry**, but they do not normally create a fresh roster-selection puzzle.
- Storage, garrisons, convoys, bases, scenario reinforcements, faction support, and reserve forces are separate strategic concepts; they are not an MVP tactical bench.
- Battle-type exceptions can exist later: ambushes may disrupt formation, sieges may add garrison rules, raids may use extraction edges, and authored scenarios may introduce reinforcements.

Reference research summary:

- **HoMM III**: a hero army has a small capped set of troop-stack slots, and those carried stacks fight. There is no normal model where a hero carries a large bench and chooses a subset immediately before each battle. Stack order and Tactics affect deployment/placement.
  - Sources: https://heroes.thelazy.net/index.php/Troop_stack, https://heroes.thelazy.net/index.php/Tactics, https://heroes.thelazy.net/index.php/Retaliation, https://heroes.thelazy.net/index.php/Speed, https://heroes.thelazy.net/index.php/Morale, https://steamcommunity.com/sharedfiles/filedetails/?id=503993419
- **Heroes of Might and Magic: Olden Era**: public Steam material and community discussion point toward the classic limited-army-slot model, with placement/order for 4-7 stack armies and discussion around army-slot count. Exact slot details should remain marked as current public/EA evidence until official rules are stable.
  - Sources: https://store.steampowered.com/app/3105440/Heroes_of_Might_and_Magic_Olden_Era/, https://steamcommunity.com/sharedfiles/filedetails/?id=3728932126
- **Songs of Conquest**: follows the HoMM-like pattern of limited active troop slots for a Wielder rather than a broad combat reserve bench.
  - Sources: https://www.songsofconquest.com/, https://store.steampowered.com/app/867210/Songs_of_Conquest/
- **King's Bounty**: uses a small active troop lineup, commonly framed through Leadership/control capacity; it supports the idea that command capacity limits what can be brought to battle.
  - Source: https://store.steampowered.com/app/25900/Kings_Bounty_The_Legend/
- **Age of Wonders 4 / Planetfall**: useful contrast. Armies have fixed unit caps, and nearby armies can reinforce, but this is strategic-map proximity reinforcement, not a carried bench. Borrow only if Neon Champions later wants multi-force positioning to matter more than classic HoMM texture.
  - Sources: https://aow4.paradoxwikis.com/Unit, https://aow4.paradoxwikis.com/Combat, https://aowplanetfall.paradoxwikis.com/Unit

Rationale:

- The strongest HoMM-like answer to “why not deploy all stacks?” is: **you do deploy all active stacks, but active slots are capped**.
- This makes composition a strategic commitment instead of an arbitrary pre-battle exclusion.
- It avoids tedious loadout selection before every ordinary fight.
- It keeps MVP tactical UI and AI simpler.
- It preserves future design space for special reinforcements, ambush disruption, siege garrisons, faction assets, or story scenarios without making reserves baseline.

### Active Army Slot Count and Stack-Splitting Rules

Approved direction:

1. The default active army size is **7 stack slots**, as a HoMM-readable working baseline. This may change later if prototype pacing, UI, or battle readability proves 7 too busy.
2. Marshal and Operator Champions use the **same baseline active army slot count** for MVP.
3. Every stack uses **1 active army slot** by default; heavy or elite stacks do not consume extra slots.
4. General stack splitting is allowed, HoMM-like, unless later roster or balance rules constrain it.
5. Duplicate stacks of the same unit type may occupy separate active army slots if the player intentionally chooses that composition.

Design contract:

- Slot count is a baseline combat/army-management rule, not a Champion-role differentiator for MVP.
- Marshal/Operator identity should come from Command, Operations, Doctrine, Assets, skills, and faction/archetype weighting rather than different army UI capacity.
- Heavy and elite units should be constrained first by cost, recruitment access, growth, upkeep, rarity, logistics, tactical profile, or counters rather than by multi-slot weight.
- If a player splits one unit type into multiple stacks, each split stack consumes a real active army slot.
- Duplicate/split stacks trade concentrated power for board coverage, activation count, blocking, objective interaction, and tactical flexibility.

Balance risks to watch:

- Free stack splitting can create one-stack abuse, retaliation baiting, objective cheese, disposable blockers, and action-count inflation.
- If these problems dominate playtests, prefer targeted constraints before removing the rule entirely: minimum split size, no objective interaction by tiny detachments, reduced morale for understrength detachments, limited split count per unit type, or faction/skill-gated detachments.
- Because stack splitting is now allowed, recruitment, morale, objective, and AI rules must later account for intentionally small stacks.

### Stack Splitting Safeguards and One-Stack Rules

Approved direction:

1. A stack of **1 unit** can be created through normal army management. This is allowed for HoMM fidelity, but must be explicitly flagged for playtest.
2. Objective interaction by tiny/split stacks is **objective-specific**.
3. Tiny split stacks block movement and exert Zone of Control normally as the working baseline, but this must be playtested.
4. Retaliation-baiting with tiny stacks is accepted as intended HoMM-like tactical texture.
5. Understrength/tiny stacks suffer extra morale/Cohesion fragility only when **isolated, outnumbered, or otherwise contextually vulnerable**, not as a flat penalty.

Design contract:

- Tiny stacks are legal tactical entities, not invalid UI artifacts.
- A tiny stack spends a real active army slot, so its opportunity cost is the main balancing lever.
- Tiny stacks may be used for scouting, blocking, retaliation baiting, objective pressure, sacrificial tempo, and lane coverage unless a specific rule says otherwise.
- Objective rules own their own eligibility requirements. Examples: a control zone may count any stack; a terminal may require a Hacker/Signal-capable stack; extraction or sabotage may require minimum strength, unit type, AP, or status requirements.
- Tiny stacks are not automatically cowardly or useless. Fragility should emerge from board context: isolation, being surrounded, hostile ZOC, suppression, poor Cohesion state, or being badly outmatched.

Playtest flags:

- Watch whether 1-stacks make optimal play tedious or mandatory.
- Watch whether normal ZOC from tiny stacks creates too much traffic jamming.
- Watch whether retaliation-baiting is fun tactical texture or repetitive exploit.
- Watch whether objective-specific eligibility is readable enough in UI.
- If needed, later constraints should be narrow and explainable rather than removing stack splitting wholesale.

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
Defend: end this stack's activation. Until its next activation, this stack gains +1 Armor, resists forced movement, and gains defensive stability against disruption through relevant Leadership / Cohesion or Doctrine effects.
```

Design notes:

- Defend is chosen when the stack cannot make a useful attack, wants to hold position, or expects incoming damage.
- Defend does not cost 1 AP in the final model; it consumes/ends the remaining activation.
- Defend competes with Wait: Wait preserves tactical timing; Defend sacrifices timing for protection.
- Defend is broadly useful against incoming harm, but Signal/Chemical attacks and other special damage types may bypass or interact differently by explicit unit/attack rule.
- Defend does not universally reduce Cohesion damage by itself; Cohesion protection comes through Leadership / Cohesion, Doctrine, traits, or specific defensive effects.
- A Defending stack can retaliate / make opportunity attacks normally.
- Defend lasts until the stack's next activation unless removed by displacement, stun, disruption, or a specific anti-defense ability.

## Base Actions

| Action | AP Cost | Notes |
|---|---:|---|
| Move | 1 | Move up to the stack's Move value. |
| Disengage | 1 | Leave hostile Zone of Control without triggering Retaliation. |
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

Approved baseline rule:

```text
Defend: End activation. Until this stack's next activation, gain +1 Armor and resistance to forced movement.
```

Approved interactions:

- Defend protects broadly, but Signal/Chemical and other special attacks may bypass or interact differently by explicit unit/attack rule.
- Defend does not automatically reduce Cohesion damage. Cohesion protection is provided by Leadership / Cohesion, Doctrine, unit traits, or specific defensive effects.
- Defending stacks can retaliate and make opportunity attacks normally.
- Defend can be stripped before the next activation by displacement, stun, disruption, or specific anti-defense abilities.

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
8. A universal **Disengage** action exists: spend 1 AP to leave Zone of Control without triggering Retaliation.
9. Forced movement does not trigger Zone-of-Control Retaliation.
10. Ranged stacks can shoot while engaged, but suffer a major damage penalty by default.

Engaged ranged attack rule:

```text
If a stack makes a ranged attack while engaged in hostile Zone of Control, that attack deals 50% damage unless a trait, weapon rule, or ability says otherwise.
```

Design notes:

- This keeps the rule HoMM-compatible: opportunity attacks are not a new resource, they are another way to spend Retaliation.
- Disengage gives every stack a clean escape valve, but spending 1 AP means the stack sacrifices tempo to avoid Retaliation.
- Forced movement bypassing ZoC Retaliation keeps push/pull/displacement effects tactically distinct from voluntary movement.
- The 50% engaged-ranged penalty makes melee contact matter without fully disabling ranged stacks.
- No unit ignores Zone of Control by hidden category. Exceptions require explicit traits/abilities.
- Candidate future traits: Phase Step, Smoke Break, Unstoppable, Skirmisher, Guardian, Extended Reach, Close-Quarters Fire, Point-Blank Specialist.

### Overwatch

Approved direction:

1. Overwatch exists in MVP, but only for stacks with a specific Overwatch trait/action.
2. Overwatch is not a universal ranged-unit action.
3. Overwatch costs 1 AP.
4. By default, Overwatch grants one reaction shot before the stack's next activation.
5. Overwatch triggers on voluntary enemy movement through the overwatching stack's line of sight / watched range.
6. Forced movement does not trigger Overwatch.
7. Disengage can trigger Overwatch if the moving stack enters or crosses watched line of sight / range.
8. Overwatch uses ammo/charge if the weapon normally uses ammo/charge.
9. Overwatch cannot trigger while the overwatching stack is engaged in hostile Zone of Control, unless a specific trait/ability says otherwise.
10. Overwatch cannot hit invisible/stealthed units unless they are revealed or detected.
11. MVP Overwatch targeting is automatic: the first valid voluntary enemy movement in line of sight / watched range triggers the shot.
12. Overwatch can be blocked or disrupted by status/effects such as Suppressed, Jammed, Hacked, smoke, stealth, or line-of-sight blocking.

Design notes:

- Overwatch adds cyberpunk/XCOM flavor without turning every ranged stack into a reaction-fire turret.
- Forced movement bypassing Overwatch preserves displacement as clean counterplay.
- Disengage avoids melee Retaliation, not all battlefield reaction fire.
- Melee engagement suppresses standard Overwatch, making close contact a strong counter to ranged control.
- Stealth/detection remains meaningful: unseen units do not get shot by baseline Overwatch.
- Automatic targeting is the MVP default because declared cones/arcs add too much tactics-game overhead for frequent HoMM-like battles.
- Specialist units may later modify Overwatch with wider arcs, longer watched range, multiple shots, Signal-assisted targeting, suppression fire, point-defense behavior, or Overwatch-while-engaged exceptions.
- Counterplay must remain visible: players should understand why Overwatch did or did not fire.

## Line of Sight and Cover

Approved direction:

1. Ranged attacks require line of sight by default.
2. Exceptions such as Indirect attacks, Signal attacks, special sensors, or map effects must say so explicitly.
3. MVP uses one universal **Cover** state rather than separate light/heavy cover.
4. Cover reduces incoming ranged damage by 25%.
5. Cover protects against **Kinetic** and **Energy** damage by default.
6. Cover does not protect against **Signal**, **Chemical**, or most **Shock** effects unless a specific object, trait, or attack rule says otherwise.
7. Melee attacks ignore Cover.

Cover rule:

```text
Cover: A covered stack takes 25% less damage from Kinetic or Energy ranged attacks. Melee attacks ignore Cover.
```

Design notes:

- Line of sight is required because ranged attacks, Overwatch, stealth, smoke, and battlefield blocking all depend on visible targeting.
- A single Cover state gives positional texture without turning combat into XCOM-style cover management.
- The 25% damage reduction keeps Cover useful but weaker than Defend; Cover is positional, Defend is an activation sacrifice.
- Cover mostly represents hard surfaces, barricades, vehicles, corners, terrain breaks, and urban clutter.
- Cover should be visually obvious and should not require tile-by-tile ambiguity.
- Special objects can define exceptions later, such as Faraday cover against Signal, sealed cover against Chemical, or insulated cover against Shock.

## Range Bands and Minimum Range

Approved direction:

1. Each ranged attack has an explicit maximum range in tiles.
2. Ranged attacks use damage falloff at long range, similar in spirit to Heroes III ranged penalties.
3. Baseline ranged attacks can fire normally within their effective range.
4. Shots beyond effective range but within maximum range deal reduced damage.
5. Heavy, sniper, artillery, missile, launcher, or other specialist weapons may have a minimum range by explicit rule.
6. Indirect attacks do not require direct line of sight, but require scouting, spotting, sensor lock, mark, or another valid targeting source.
7. Melee attacks are adjacent-only by default.
8. Some units or weapons may have Reach 2 by explicit trait/rule.

Range rule:

```text
Ranged Attack: Has Max Range X and, if needed, Effective Range Y. Attacks beyond Effective Range but within Max Range deal reduced damage. The default long-range penalty is 50% damage unless the attack says otherwise.
```

Indirect targeting rule:

```text
Indirect Attack: Does not require direct line of sight, but requires a valid spotter, Marked target, sensor lock, revealed target, or equivalent targeting source.
```

Design notes:

- Tile-based max range is clearer than abstract short/medium/long bands for a grid tactics layer.
- Damage falloff gives a HoMM-like ranged texture without adding hit-chance math.
- Minimum range is not universal; it is a weapon identity rule for heavy/indirect/specialist attacks.
- Indirect fire should create artillery/drone/mortar identity, but it must remain counterable through scouting denial, jamming, stealth, smoke, sensor disruption, or killing/pressuring spotters.
- Reach beyond adjacency is an exception, not a melee baseline.

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

- **Melee** — adjacent by default; explicit Reach rules can extend this. Interacts with Retaliation and Zone of Control.
- **Direct Ranged** — ranged attack requiring normal targeting/line of sight, max range, and any applicable long-range falloff.
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
4. Armor is flat damage reduction against Kinetic damage by default.
5. Armor applies at half value against Energy damage by default.
6. Armor does not protect against Chemical, Signal, or most Shock effects unless an explicit rule says otherwise.
7. Shield is a separate durability layer for selected units only, not universal bonus HP.
8. Shields are depleted before HP.
9. Shields do not regenerate during battle by default; regeneration requires an explicit trait, ability, operation, or map effect.
10. High-tech/networked status is double-edged: it enables bonuses and advanced abilities, but increases vulnerability to Signal/Shock disruption.

Core durability values:

- **HP** — body/platform integrity; when depleted, the stack loses units or is destroyed.
- **Armor** — flat reduction against Kinetic damage; applies at half value against Energy unless a specific rule says otherwise.
- **Shield** — optional separate protection layer, often strong against direct damage but vulnerable to Shock/Signal-style disruption depending on unit rules.

Damage reduction order:

```text
1. Start with rolled/unit-specific stack damage.
2. Apply situational percentage modifiers: range falloff, engaged-ranged penalty, Cover, Defend, and similar effects.
3. Apply Armor reduction: full Armor vs Kinetic, half Armor vs Energy, none vs other damage types unless specified.
4. Apply remaining damage to Shield first, then HP.
5. If the damaging attack successfully applies, final damage is at least 1 unless immunity or an explicit rule negates it.
```

Design notes:

- Flat Armor makes +1 Armor from Defend concrete and readable.
- Half Armor vs Energy gives Armor some broad value without making Energy feel like Kinetic with different flavor text.
- Shields are an optional high-tech durability layer, not a universal second HP bar.
- Shield regeneration is reserved for explicit unit/faction identity, Champion effects, or special map systems.

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

### Armor, Shield, and Defense Counterplay

Approved direction:

1. **Shock** damage is especially good against Shields by default: Shock deals bonus damage to Shield HP.
2. **Signal** does not directly damage Shield HP by default.
3. Signal can disable Shield regeneration, Shield traits, or Shield-linked systems through explicit effects.
4. **Chemical** bypasses Armor by default; Armor does not reduce Chemical damage unless an explicit rule says otherwise.
5. Armor-piercing weapons can exist as explicit attack rules only, not as a formal Piercing damage type or universal tag.
6. The default armor-piercing pattern is **ignore half Armor**.
7. Stronger specialist weapons may explicitly ignore all Armor or use another written rule.

Counterplay rules:

```text
Shock vs Shield: Shock attacks deal bonus damage to Shield HP by default. Exact bonus value is tunable per attack/faction, with +50% Shield damage as the working baseline.

Signal vs Shield: Signal does not damage Shield HP by default, but explicit Signal effects may disable Shield regeneration, Shield traits, Shield projection, or other Shield-linked systems.

Armor Piercing: If an attack says Armor Piercing and gives no more specific rule, it ignores half of the target's Armor.
```

Design notes:

- Shock owns the anti-shield/EMP space without making Shields irrelevant.
- Signal manipulates or disables systems rather than becoming generic shield damage.
- Chemical bypassing Armor keeps toxins, acid, gas, and engineered agents distinct from weapon impact.
- Armor-piercing remains explicit rule text so the design does not reintroduce Piercing as a sixth damage type or broad tag.

### Attack Accuracy, Randomness, and Damage Variance

Approved direction:

1. Basic attacks do not use hit/miss accuracy by default; normal attacks hit if the target is valid.
2. Randomness comes primarily from damage variance, explicit effects, Edge/Luck-like mechanics, and special unit rules.
3. Use HoMM-style unit-specific damage ranges rather than one global variance percentage.
4. Universal critical hits do not exist.
5. Lucky/critical-style outcomes can be created by **Edge**, traits, abilities, or explicit attack rules.
6. After reductions, a damaging attack deals at least 1 damage if it successfully applies, unless immunity, invalid targeting, or an explicit rule reduces it to 0.

Damage variance rule:

```text
Unit Attack Damage: Each unit has a min-max damage range. Stack damage is based on surviving unit count and the attack's rolled/unit-specific damage value, then modified by range, cover, armor, Defend, resistances, and explicit rules.
```

Minimum damage rule:

```text
If a damaging attack successfully applies after targeting and defenses, final damage is at least 1 unless an immunity or explicit rule negates it.
```

Design notes:

- No baseline hit/miss keeps combat fast, readable, and closer to HoMM than XCOM.
- Unit-specific min/max damage preserves uncertainty and faction/unit texture without accuracy frustration.
- Edge should own the Luck/critical space rather than every attack having universal crit chance.
- Special attacks may still define miss, scatter, partial success, resist checks, evasion, or failure rules explicitly when that is central to their identity.

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

## Status Effect Taxonomy

Approved direction:

1. Statuses are grouped into four broad families: **Physical**, **System**, **Chemical**, and **Cohesion**.
2. Do not use a universal hard-control **Stunned** status as a baseline rule.
3. Hard-control effects should be more specific and rarer: Jammed, Suppressed, Pinned, Disoriented, Hacked, Immobilized, etc.
4. **Suppressed** is a core status: it blocks Overwatch and weakens ranged attacks.
5. **Jammed** and **Hacked** are separate statuses.
6. **Jammed** means temporary system interference: weapons, shields, sensors, drones, cybernetics, or other tech systems malfunction or lose specific functions.
7. **Hacked** means hostile control or deeper compromise: enemy influence, forced behavior, false commands, compromised targeting, or persistent system intrusion.
8. Status durations use simple timing categories: until next activation, 1 round, or battle-long.

Status family model:

```text
Physical: suppression, pinning, immobilization, knockback, bleeding, burning, disorientation from impact.
System: jammed, hacked, sensor disruption, shield disruption, drone/cybernetic malfunction, Signal compromise.
Chemical: poison, acid, viral payloads, gas, corrosion, biotech contamination.
Cohesion: panic, command confusion, morale shock, identity fracture, propaganda pressure, formation instability.
```

Core status examples:

```text
Suppressed: Cannot trigger Overwatch. Ranged attacks deal 50% damage while Suppressed. No baseline movement or melee penalty. Lasts until the suppressed stack's next activation unless an effect says otherwise.

Jammed: One named system/action chosen by the jamming effect temporarily fails or operates at reduced effectiveness. It only blocks Overwatch if the jammed system is the weapon, sensor, or control system used for Overwatch. Lasts until the jammed stack's next activation unless an effect says otherwise.

Hacked: The stack suffers hostile control or deeper compromise. A baseline Hack usually disables one named trait/action and adds a hostile rider effect. Hacked is mostly limited to networked, cybernetic, drone, Echo, or otherwise compromisable units unless an effect says otherwise.
```

Duration rule:

```text
Status durations should use: until next activation, 1 round, or battle-long. Use exact counters only for explicit special cases.
```

Design notes:

- The family taxonomy is for consistency, not a resistance-table system.
- Avoid generic full-turn Stun because it is too blunt for stack combat and undermines counterplay.
- Suppression gives fire-support and ranged-control units a clean role without relying on hit/miss accuracy.
- Jammed vs Hacked preserves cyberpunk nuance: interference is not the same as hostile control.

## Suppression

Approved direction:

1. **Suppressed** is a core Physical status.
2. Suppressed stacks cannot trigger Overwatch.
3. Suppressed stacks deal 50% damage with ranged attacks.
4. Suppressed has no baseline movement penalty.
5. Suppressed has no baseline melee penalty.
6. Baseline Suppressed lasts until the suppressed stack's next activation.
7. Defend does not remove Suppressed by default.
8. Doctrine, Leadership / Cohesion, traits, abilities, or specific cleanse effects may reduce, remove, or prevent Suppressed.

Suppression rule:

```text
Suppressed: Until this stack's next activation, it cannot trigger Overwatch and its ranged attacks deal 50% damage. Suppressed does not reduce movement or melee attacks by default.
```

Design notes:

- Suppression is anti-ranged/control, not a generic weakness state.
- Matching the 50% engaged-ranged penalty keeps the mental model simple: if your ranged unit is under immediate pressure, its shooting is halved.
- Defend is not a universal cleanse; command-layer systems and disciplined-unit traits are the proper counterplay space.

## Jammed

Approved direction:

1. **Jammed** is a System status.
2. Jammed usually affects one named system/action chosen by the jamming effect.
3. Jammed blocks Overwatch only if the jammed system is the weapon, sensor, control link, or targeting system used for Overwatch.
4. Jammed does not affect basic attacks unless the jammed system is that attack/weapon.
5. Baseline Jammed lasts until the target's next activation.
6. Analogue/low-tech units cannot be Jammed unless they have a named system vulnerable to jamming.

Jammed rule:

```text
Jammed: Until this stack's next activation, one named system/action chosen by the jamming effect fails or operates at reduced effectiveness. Jammed only affects attacks, Overwatch, movement, Shields, sensors, or traits if the named jammed system controls that function.
```

Examples:

```text
Sensor Jam: Target loses sensor lock and cannot use Overwatch that depends on sensors until its next activation.

Weapon Jam: Target cannot use the named smart weapon or uses it at reduced effect until its next activation.

Shield Jam: Target cannot use the named Shield trait/regeneration/projection effect until its next activation.
```

Design notes:

- Jammed is precision interference, not a generic shutdown.
- This preserves the high-tech vs analogue tradeoff: advanced systems create power and vulnerability; simpler units are less jammable.
- Suppressed remains the general anti-Overwatch/ranged-pressure status; Jammed only blocks Overwatch when it hits the relevant system.

## Hacked

Approved direction:

1. **Hacked** is a System status representing hostile control, false command input, or deeper compromise.
2. A baseline Hack usually disables one named trait/action and adds a hostile rider effect.
3. Hacked is mostly limited to networked, cybernetic, drone, Echo, command-linked, or otherwise compromisable units by default.
4. Hacked is rarer, higher-tier, or more conditional than Jammed.
5. A common pattern is that Hacked requires prior setup such as Jammed, Marked, Sensor Lock, exposed network state, or a successful Operation.
6. Hacked has no single baseline duration; each Hack defines its timing explicitly.
7. Hacked counters depend on the hack family. Technical hacks may be answered by Signal Training, Counterintelligence, or system hardening; command/social/Echo compromises may be answered by Doctrine, Leadership / Cohesion, identity stability, or fallback protocols.

Hacked rule pattern:

```text
Hacked: Disable one named trait/action and apply one hostile rider effect. The effect must define its valid targets, setup requirement, duration, and counterplay.
```

Example patterns:

```text
Targeting Hack: Requires Sensor Lock. Target cannot use Smart Targeting and its next ranged attack prioritizes a decoy/marked false target if valid.

Drone Override: Requires Jammed or exposed command link. Target drone stack loses one named special action and may be forced to Move 1 tile or waste its next special-action window.

Echo Identity Spoof: Requires Signal access or prior Mark. Target Echo-linked stack loses one continuity trait and suffers Cohesion pressure until the effect expires.
```

Design notes:

- Hacked should feel scarier than Jammed, but not usually become full unit control or skipped activation.
- The default shape is “disable + hostile rider,” not “you lose your turn.”
- Setup requirements keep hacking tactical and counterable instead of spammy.
- Different hack families should advertise different counters; do not collapse all answers into one generic cleanse.

## Marked and Sensor Lock

Approved direction:

1. **Marked** and **Sensor Lock** are separate setup statuses.
2. **Marked** is general tactical designation: spotters, scouts, visible paint, target calls, tracer logic, informants, battlefield designation, or analogue marking.
3. **Sensor Lock** is technical targeting lock: sensors, drones, targeting suites, Signal systems, smart weapons, networked optics, or electronic acquisition.
4. Marked enables indirect targeting and some abilities; it does not grant a damage bonus by default.
5. Sensor Lock enables indirect targeting and technical abilities; it can support hacks.
6. Both Marked and Sensor Lock reveal stealthed/invisible units while active.
7. Baseline Marked and Sensor Lock last 1 round unless the source effect says otherwise.

Rules:

```text
Marked: For 1 round, the target is tactically designated. Marked can enable indirect targeting and abilities that require a marked target. Marked grants no damage bonus by default. While active, Marked reveals stealthed/invisible targets.

Sensor Lock: For 1 round, the target is technically acquired. Sensor Lock can enable indirect targeting, smart weapons, technical abilities, and Hack setup. Sensor Lock grants no damage bonus by default. While active, Sensor Lock reveals stealthed/invisible targets.
```

Design notes:

- Keeping Marked and Sensor Lock separate lets analogue scouts/spotters and high-tech sensor units both matter.
- Neither status is a generic vulnerability multiplier by default; they are setup/permission states.
- Revealing stealth while active gives both statuses strong tactical value, but duration keeps them temporary.
- Sensor Lock should be more vulnerable to Jammed, Signal counterplay, smoke, decoys, and sensor disruption.
- Marked should be more vulnerable to line-of-sight denial, killing/pressuring spotters, smoke/visibility breaks, and command confusion.

## Stealth and Reveal

Approved direction:

1. **Stealthed** units cannot be targeted by direct ranged attacks or Overwatch unless revealed/detected.
2. Stealthed units can be hit by Area attacks if the area includes their tile.
3. Any attack by a Stealthed unit breaks Stealth by default.
4. Entering melee adjacency reveals Stealthed units.
5. **Reveal** lasts 1 round by default.
6. Marked and Sensor Lock reveal Stealthed/invisible units while active.

Rules:

```text
Stealthed: Cannot be targeted by direct ranged attacks or Overwatch unless Revealed/detected. Can still be affected by Area attacks that include its tile.

Reveal: For 1 round, the target loses Stealth targeting protection and can be targeted normally, subject to line of sight, range, Cover, and other rules.
```

Reveal sources:

- Marked.
- Sensor Lock.
- Adjacent enemy contact.
- The Stealthed unit making any attack.
- Explicit detection, scanning, flare, drone, Signal, scout, or anti-stealth effects.

Design notes:

- Stealth is strong positioning/approach protection, not absolute immunity.
- Area attacks provide intuitive counterplay against suspected Stealth positions.
- Attacking breaks Stealth to avoid permanent invisible damage dealers.
- Adjacency reveal makes melee pressure and scouting movement useful against Stealth.
- Reveal lasting 1 round matches Marked/Sensor Lock and gives enough time for follow-up.

## Smoke and Vision Blocking

Approved direction:

1. **Smoke** blocks line of sight through its tiles by default.
2. Units inside Smoke cannot be targeted by direct ranged attacks unless the attacker has a valid detection/sensor source that bypasses or sees through Smoke.
3. Valid detection/sensor sources can come from the attacking unit, another allied unit, Champion ability, Operation, map system, sensor network, or explicit effect.
4. Area attacks can target Smoke-covered tiles.
5. Smoke does not remove existing Marked or Sensor Lock; it blocks future line-of-sight-based application unless the applying effect can bypass Smoke.
6. Baseline Smoke lasts 1 round.

Smoke rule:

```text
Smoke: For 1 round, blocks line of sight through affected tiles. Direct ranged attacks cannot target units inside Smoke unless the attacker has a valid detection/sensor source that bypasses Smoke. Area attacks may still target Smoke-covered tiles.
```

Design notes:

- Smoke is vision denial, not generic damage protection.
- Smoke counters direct ranged attacks, Overwatch, clean line-of-sight targeting, and new LoS-based Marked/Sensor Lock applications.
- Existing Marked or Sensor Lock persists for its normal duration; Smoke does not cleanse it by default.
- Sensor bypass should be explicit and can be provided by units, allied spotters, Champion abilities, Operations, map infrastructure, or faction systems.
- Area attacks remain the intuitive counter to obscured positions.

## Terrain Hazards

Approved direction:

1. Terrain hazards are a core tactical system: common enough to matter, but kept simple.
2. Hazards apply when a stack enters the hazardous tile/area and again at the start of that stack's activation if it remains there.
3. Hazards affect all stacks equally by default unless an explicit resistance, immunity, trait, or rule says otherwise.
4. Hazards do not block movement by default; they punish movement/positioning but do not make tiles impassable.
5. Ability-created hazards usually last **1 round** as the baseline, but specific abilities may define a different duration when needed.

Hazard rule:

```text
Hazard: A hazardous tile/area applies its effect when a stack enters it and at the start of that stack's activation while it remains inside. Hazards do not block movement by default. Ability-created hazards last 1 round unless the ability says otherwise.
```

Example hazard types:

- Fire / burning zone: Energy damage or burning Physical status.
- Gas / toxin cloud: Chemical damage or Chemical status.
- Acid spill: Chemical damage, Armor/cover degradation, or explicit corrosion effect.
- Electrified zone: Shock damage, Shield damage, Jammed risk, or anti-drone/cybernetic disruption.
- Signal interference zone: System/Cohesion disruption, Sensor Lock denial, Jammed/Hacked setup, or network penalty.
- Rubble / debris: movement friction or Physical hazard if an effect explicitly says so.

Design notes:

- Hazards should make positioning matter without turning the map into a puzzle of impassable tiles.
- “Affects all by default, exceptions explicit” keeps the rules readable and prevents hidden category complexity.
- Enter + start-of-activation timing makes hazards matter immediately and prevents easy abuse by stepping through danger for free.
- 1 round is the default duration for ability-created hazards, matching Smoke/Reveal/Marked timing, but persistent map hazards and special abilities can override it.

## Forced Movement

Approved direction:

1. Forced movement can push/pull/move stacks into hazards; hazards apply on entry.
2. Occupied tiles block forced movement by default.
3. If forced movement hits an obstacle or occupied tile, the moved stack stops early and takes collision damage.
4. Defend reduces incoming forced movement by 1 tile.
5. Forced movement can move stacks off objective/control tiles.
6. Forced movement does not trigger Zone-of-Control Retaliation or Overwatch by default.

Forced movement rule:

```text
Forced Movement: Move the target the specified number of tiles. Occupied tiles and obstacles block forced movement. If blocked early by an obstacle or occupied tile, the target stops and takes collision damage. If moved into a hazard, the hazard applies on entry. Forced movement does not trigger ZoC Retaliation or Overwatch.
```

Defend interaction:

```text
Defend vs Forced Movement: While Defending, reduce incoming forced movement distance by 1 tile.
```

Collision baseline:

```text
Collision Damage: If forced movement is blocked by an obstacle or occupied tile, the moved stack takes minor Kinetic damage. Exact damage is ability/tuning dependent; use a small fixed value or low unit-scaled value as the baseline pattern.
```

Design notes:

- Forced movement is a tactical combo tool: push into hazards, break positions, expose targets, clear objectives.
- Occupied tiles blocking movement avoids collision-chain complexity.
- Collision damage gives blocked pushes some value without requiring automatic secondary displacement.
- Defend resisting 1 tile is deterministic and readable.
- Objective displacement is allowed so battlefield positioning matters for control play.

## Tactical Objectives and Interactions

Approved direction:

1. Objective control/resolution depends on objective type.
2. Most objectives require spending AP; **Interact / Objective** usually costs 1 AP.
3. Whether engaged stacks can interact depends on objective type.
4. Suppressed, Jammed, Hacked, and other statuses can affect objective interaction when relevant to the objective type.
5. Objective progress can be instant or persistent depending on objective type.

Objective interaction rule:

```text
Interact / Objective: Usually costs 1 AP while the stack is in the required position or valid interaction range. The objective defines whether interaction is allowed while engaged, whether statuses interfere, and whether progress resolves instantly or persists over time.
```

Objective type patterns:

```text
Control Zone: Usually checks occupation/control state and may allow engaged stacks to contest or hold.

Terminal / Hack Point: Usually requires 1 AP Interact and may be blocked or modified by Jammed, Hacked, Sensor Lock, Signal interference, or enemy adjacency.

Sabotage / Plant / Extract: Usually requires 1 AP Interact and may use instant completion, multi-step progress, or scenario-specific timing.

Hold Point / Upload / Ritualized Operation: May use persistent progress across rounds and can be interrupted by displacement, Hacked, Suppressed, objective contesting, or scenario rules.
```

Design notes:

- Objectives should compete with attacking, moving, reloading, and defending; 1 AP Interact makes that tradeoff visible.
- Do not force all objectives into one model. Capture zones, terminals, extraction points, sabotage targets, and uploads need different pacing.
- Engaged interaction should be objective-specific: holding ground while engaged is fine; delicate hacking or extraction under melee pressure may not be.
- Status interaction should be fictional and readable, not universal. Suppressed might affect exposed upload work; Jammed might block technical interaction; Hacked might compromise a terminal or objective action.
- Forced movement can remove stacks from objective/control tiles, making displacement valuable in objective play.

## Retreat, Surrender, and Tactical Loss Boundary

Approved direction:

1. Voluntary retreat availability depends on battle type.
2. Retreat is primarily a command-layer escape/concession, not a default way to save the committed army.
3. In most ordinary battle types, choosing retreat means losing the committed army/stacks for sure.
4. Stack preservation on leaving combat depends on battle type, but mostly retreat does **not** preserve surviving stacks.
5. Scenario extraction is a separate pattern: only stacks that satisfy the extraction rule, such as reaching an extraction edge/tile, may escape.
6. Surrender exists separately from retreat.
7. Surrender should preserve more than retreat, but costs resources, reputation, leverage, terms, prisoners, debt, access, or other strategic concessions.
8. If all allied stacks are destroyed, routed, or otherwise removed, the battle is lost.
9. Champion death or capture from tactical loss occurs only by explicit scenario/battle rule, not by default.
10. Champion assets, operations, or supporting resources are at risk only if they were deployed or committed to that battle.

Baseline rule text:

```text
Retreat: battle-type-dependent voluntary exit. In most ordinary battles, retreat concedes the battlefield and forfeits the committed army/stacks. Retreat protects the command-layer Champion from routine tactical death/capture unless the battle explicitly says otherwise.

Surrender: battle-type-dependent negotiated loss. Surrender may preserve more forces or assets than retreat, but imposes strategic costs such as payment, reputation damage, prisoners, debt, loss of position, access concessions, or scenario-specific terms.

Extraction: scenario-specific escape. Stacks escape only if they meet the scenario's extraction condition, usually reaching or controlling an extraction tile/edge/objective.
```

Battle-type patterns:

```text
Field Battle / Skirmish: Retreat may be available, but normally forfeits the committed army. Surrender may preserve some forces at a strategic cost.

Ambush / Trap: Retreat may be restricted, delayed, or especially punishing. Extraction or survival objectives may replace generic retreat.

Raid / Sabotage / Extraction Mission: Leaving the battlefield should usually be objective-driven. Surviving stacks are preserved only if the scenario extraction rules are satisfied.

Siege / Base Assault: Retreat and surrender terms should depend on attacker/defender role, encirclement, control zones, and strategic stakes.

Story / Set-Piece Battle: Champion capture, death, asset loss, or special escape rules occur only if explicitly authored.
```

Design notes:

- This keeps HoMM-like retreat/surrender texture without making retreat a low-cost army-saving button.
- Retreat should usually protect the Champion's continuity/control layer, not preserve the deployed army.
- Surrender is the softer-loss valve: it can save more than retreat, but should create visible strategic debt or loss of leverage.
- Extraction missions should reward positional play rather than letting the player press a universal Retreat command to save everyone.
- Champion consequences should be battle-authored. Routine tactical defeat should not casually kill or capture Champions because Champions are not baseline board units.
- Asset risk should follow commitment. If a drone wing, safehouse uplink, Operator channel, transport, or special support asset was committed to the fight, it can be lost, damaged, exposed, or captured according to scenario rules.

## Morale, Routing, and Stack Collapse

Approved direction:

1. Individual stacks can rout during tactical combat.
2. Rout is a normal morale state, not only a rare scenario exception.
3. A routed stack normally remains on the battlefield but cannot attack or perform objective interactions.
4. Baseline routed behavior: the stack may only Move or Defend unless the causing effect defines a different behavior.
5. Specific rout-causing effects may override the baseline behavior when fiction requires it, such as panic flight, signal seizure, surrender cascade, berserk withdrawal, or forced retreat.
6. Whether rout counts as destroyed/removed for battle-loss checks depends on recoverability.
7. If a routed stack can recover, it does not automatically count as destroyed for battle-loss checks.
8. If a routed stack is permanently out of player control, removed, captured, or forced off-field, it counts as removed for battle-loss checks.
9. Combat uses an army-wide global morale model.

Baseline rule text:

```text
Routed: a stack morale-collapse state. A routed stack remains present but loses offensive and objective agency. By default it may only Move or Defend. It cannot Attack, Interact / Objective, Reload + Fire, use active special abilities, or voluntarily trigger complex tactical actions unless a rule explicitly allows it.

Recoverable Rout: the stack is temporarily routed and may return to normal control through morale recovery, Champion command, faction effects, rally actions, time, or scenario rules. Recoverable routed stacks do not automatically count as destroyed for battle-loss checks.

Removed Rout: the stack is effectively gone from the fight through flight, capture, surrender, signal seizure, cohesion collapse, or forced off-field removal. Removed routed stacks count as removed for battle-loss checks.
```

Design notes:

- Making rout a normal morale state gives battles a middle failure state between full combat readiness and stack death.
- The baseline should be simple: routed stacks lose agency, but are not automatically deleted.
- Effect-specific rout behavior keeps room for faction identity: propaganda panic, Hacked command loops, cult discipline breaks, drone swarm desync, biotech shock, or corporate surrender protocols can all read differently.
- The global morale model should be visible and readable, not a hidden dicey subsystem.
- Morale must not become a second HP bar for every stack unless later packets justify that complexity.

## Global Morale Model

Approved direction:

1. Combat uses one army-wide Morale value per side.
2. Global Morale is side-level, not a separate morale bar for every stack.
3. Morale mostly changes through readable battle events.
4. Pre-battle army quality, Champion state, faction traits, doctrine, preparation, and strategic context can set or modify starting Morale.
5. Event-based morale swings include stack loss, stack rout, objective loss/gain, Champion command, terror/propaganda effects, flanking or encirclement moments, decisive kills, and scenario-specific shocks.
6. Low global Morale creates a combination of consequences, but mostly increases stack rout risk.
7. Low Morale may also create limited penalties, command friction, or vulnerability to enemy pressure, but should not become an overwhelming snowball by default.
8. High Morale primarily enables Champion/faction/command abilities rather than granting broad passive stat bonuses.

Baseline rule text:

```text
Global Morale: each side has one visible army-wide Morale value for the battle. Morale reflects battlefield confidence, command cohesion, perceived legitimacy, fear, panic, and willingness to keep fighting.

Starting Morale: set before battle from army quality, Champion/Marshal/Operator context, faction traits, doctrine, strategic preparation, scenario state, and relevant assets.

Morale Change: Morale changes mainly through significant readable events, not constant hidden drift. Stack destruction, rout, objective shifts, command actions, terror/propaganda, and scenario shocks can raise or lower Morale.

Low Morale: increases the risk that stacks rout or fail to recover from rout. It may also apply light command friction or expose the army to specific pressure effects, but rout risk is the primary consequence.

High Morale: does not normally grant broad passive combat stats. Instead it can unlock, empower, discount, or stabilize specific Champion, faction, doctrine, or command abilities.
```

Design notes:

- One side-level value keeps morale readable and avoids a hidden morale simulation for every stack.
- Starting Morale lets strategic-layer quality matter without requiring per-stack morale accounting.
- Event-based morale makes the system legible: players should know why morale changed.
- High morale should be active/identity-driven rather than generic win-more damage or defense.
- Low morale should create pressure and rout risk, but avoid irreversible death spirals unless a faction/scenario is explicitly built around morale collapse.

## Morale Scale, Thresholds, and Rout Checks

Approved direction:

1. Morale uses a hidden numeric value with player-facing visible bands.
2. The hidden numeric value exists for tuning, balancing, event deltas, thresholds, and AI evaluation.
3. The player-facing UI should show morale as readable bands rather than over-precise numbers.
4. Rout checks happen from a combination of major morale events and heavy stack losses.
5. Rout should feel caused by battlefield events, not like a random per-round tax.
6. Rout is weighted/probabilistic based on Morale band and event severity.
7. Stack type affects rout resistance through broad traits rather than a full morale stat on every unit.
8. Broad rout-resistance traits may include disciplined, fearless, fragile, drone, fanatic, mercenary, civilian, expendable, unstable, or similar faction/unit descriptors.

Baseline rule text:

```text
Morale Value: each side has a hidden numeric Morale value for tuning and rules resolution.

Visible Morale Band: the UI presents Morale as broad readable bands, such as Broken, Shaken, Steady, Confident, and Inspired, rather than exposing exact numbers by default.

Rout Check: when a major morale event occurs or a stack suffers heavy losses, affected stacks may make a rout check. The check is weighted by current Morale band, event severity, relevant stack traits, Champion/faction modifiers, and scenario rules.

Stack Rout Traits: units do not need a universal morale stat. Instead, broad traits modify rout behavior where fiction and roster identity justify it.
```

Example morale bands:

```text
Inspired: high morale; enables or strengthens specific Champion/faction/command abilities.
Confident: above baseline; troops are stable and less vulnerable to rout pressure.
Steady: normal morale; no special collapse pressure.
Shaken: low morale; rout checks become more dangerous and recovery is harder.
Broken: collapse state; rout risk is severe and some commands/effects may fail or become unavailable.
```

Example rout-trigger events:

```text
- A stack is destroyed.
- A stack suffers heavy losses in a single attack or activation.
- A key objective is lost, captured, hacked, sabotaged, or extracted.
- A Champion/faction terror, propaganda, command, or shock effect resolves.
- A routed stack fails to recover or is removed from the field.
- A scenario-specific morale shock occurs.
```

Design notes:

- Hidden numeric plus visible bands gives implementation flexibility without making players count morale points.
- Major-event and heavy-loss checks keep rout connected to drama the player can understand.
- Weighted chance preserves uncertainty; event severity and banding prevent it from feeling arbitrary.
- Broad stack traits give unit identity without adding a mandatory morale-resistance stat to every roster entry.
- Traits should be sparse and meaningful. Do not tag every unit unless the trait changes a real rule.

## Morale Recovery and Rally Actions

Approved direction:

1. Routed stack recovery depends on the source of the rout.
2. Panic, hack seizure, surrender cascade, drone desync, biotech shock, propaganda collapse, and other rout sources may define different recovery rules.
3. Combat has a basic Champion/command-layer Rally action.
4. There is no baseline adjacent-stack Rally action.
5. Rally cost depends on the Rally source.
6. Basic Champion Rally can cost a Champion command resource/action, while faction, unit, doctrine, asset, or scenario Rally tools may use their own costs.
7. Rally effects depend on the Rally source.
8. Rally may improve global Morale, clear/reduce Routed on one or more stacks, stabilize recovery checks, remove command friction, or combine those effects where appropriate.

Baseline rule text:

```text
Rout Recovery: a routed stack's recovery method is defined by the source of the rout. Some rout states can recover naturally, some require Champion command, some require faction/unit abilities, and some are removed-rout states that cannot recover during the battle.

Champion Rally: a command-layer action used to restore control, stabilize morale, or reassert command over routed or wavering forces. Champion Rally is the baseline universal Rally form.

Rally Source: each Rally effect defines its own cost and scope. Costs may include Champion command resource, once-per-battle use, cooldown, doctrine charge, asset exposure, scenario resource, or faction-specific requirement.

Rally Effect: a Rally may raise global Morale, clear or downgrade Routed, improve recovery odds, stabilize a stack against further rout checks, restore command access, or combine several modest effects.
```

Design notes:

- Recovery should preserve fiction. A panicked militia stack, a hacked drone swarm, and a corporate unit entering surrender protocol should not all snap back for the same reason.
- Keeping baseline Rally at the Champion/command layer avoids adjacency micromanagement and reinforces that morale is a command problem.
- Unit/faction-specific rally abilities can still exist, but they are exceptions and identity tools, not the default recovery UI.
- Rally should be strong enough to create comeback decisions but not erase rout as a meaningful failure state.
- Removed-rout states should be clearly labeled so the player knows when recovery is impossible.

## Morale Event Sources and Strategic Links

Approved direction:

1. Stack destruction affects global Morale, scaled by stack value and battlefield role.
2. Losing cheap, expendable, or low-commitment stacks should not hit Morale as hard as losing elite, symbolic, expensive, rare, or command-critical stacks.
3. Objective gain and loss affects global Morale by default.
4. Objective morale impact should reflect objective importance, current scenario stakes, and whether the objective is framed as symbolic, tactical, logistical, informational, or existential.
5. Pre-battle strategic conditions affect starting Morale.
6. Starting Morale can be shaped by supply, fatigue, territory, intel, reputation, recent victories/losses, preparation, army quality, Champion state, faction traits, doctrine, and scenario context.
7. Factions can have distinct morale baselines and morale-response hooks.
8. Morale behavior is a faction-identity surface: drones, cultists, mercenaries, citizens, biotech swarms, corporate professionals, insurgents, and Echo-mediated forces may gain, lose, resist, or exploit Morale differently.

Baseline rule text:

```text
Stack Loss Morale: when a stack is destroyed or removed, global Morale changes based on the stack's value, role, rarity, symbolic weight, and faction/scenario traits. Expendable stacks may have reduced or altered morale impact; elite or command-critical stacks may create major shocks.

Objective Morale: gaining, holding, losing, hacking, sabotaging, extracting, or failing objectives can raise or lower global Morale. The objective definition sets the morale weight and any faction/scenario exceptions.

Starting Morale: before combat begins, each side's starting Morale is modified by strategic conditions such as supply, fatigue, territory control, intel advantage, reputation, recent victories or losses, preparation, Champion state, faction traits, doctrine, and scenario context.

Faction Morale Hooks: factions may define morale baselines, event modifiers, recovery patterns, rout traits, high-morale uses, low-morale vulnerabilities, or unusual interpretations of morale.
```

Example faction morale hooks:

```text
Drone / autonomous forces: may resist fear-based morale shocks but be vulnerable to command desync, hacking, bandwidth collapse, or control-node loss.

Cult / ideology-bound forces: may resist ordinary casualties but suffer severe shocks from symbolic failure, leader contradiction, exposed fraud, or doctrine-breaking events.

Mercenary / corporate forces: may respond strongly to contract viability, payment confidence, reputation, extraction options, and perceived legal/PR exposure.

Citizen / militia forces: may be sensitive to casualties and terror, but gain morale from defending home territory, visible legitimacy, or successful protection of civilians.

Biotech / swarm forces: may treat individual losses as low-impact but react strongly to brood-node death, chemical disruption, command pheromone collapse, or containment breach.
```

Design notes:

- Scaling stack-loss morale by value prevents cheap fodder from becoming morale-liability spam.
- Objective morale ties psychological momentum to scenario play and makes non-kill actions matter.
- Strategic starting Morale gives map-layer decisions tactical consequences without adding per-turn overhead.
- Faction morale hooks should be sparse and legible. The goal is identity, not a bespoke morale minigame for every faction.
- Morale rules should expose why morale changed: “Elite stack destroyed,” “Upload secured,” “Fighting in home territory,” “Supply exhausted,” etc.

## Morale UI, Prediction, and Player Readability

Approved direction:

1. Morale is always visible in the tactical UI as a band plus trend indicator.
2. The UI should always show recent causes for Morale changes.
3. Rout risk should be previewed before major foreseeable morale-risk actions, events, or objective decisions.
4. Exact hidden numeric Morale may be exposed through optional advanced tooltip/accessibility UI.
5. Normal UI should remain band-based and readable; exact numbers are not the default presentation.

Baseline rule text:

```text
Morale Display: each side's Morale is always visible in tactical combat as a readable band plus trend indicator, such as rising, stable, pressured, or collapsing.

Morale Cause Feed: when Morale changes, the UI shows the recent cause or causes, such as Elite stack destroyed, Objective secured, Supply exhausted, Fighting in home territory, Champion Rally, or Broadcast panic effect.

Rout Risk Preview: when a major foreseeable action or objective outcome may trigger meaningful rout risk, the UI previews an approximate risk band rather than an exact hidden roll by default.

Advanced Morale Detail: optional advanced tooltips or accessibility settings may expose exact hidden numeric Morale, recent modifiers, and approximate rout probabilities for players who want more transparency.
```

Example UI language:

```text
Morale: Shaken, falling
Recent causes: Elite stack destroyed; Upload objective contested
Risk preview: Destroying this stack may trigger Moderate rout risk among nearby low-discipline units.
Advanced tooltip: Morale 34/100; Shaken band; -12 recent event delta; +5 home territory modifier.
```

Design notes:

- Morale cannot be both mechanically important and invisible. Always-visible bands protect fairness.
- Showing causes is mandatory for event-based morale; otherwise morale will feel arbitrary.
- Rout risk preview should focus on major foreseeable events, not every tiny action, to avoid UI noise and over-mechanization.
- Optional exact values support clarity, accessibility, testing, and strategy-minded players without forcing spreadsheet UI on everyone.
- The trend indicator helps players understand direction even when the band has not changed yet.

## Morale Complexity Boundary and MVP Cut

Approved direction:

1. MVP morale scope is core tactical morale only: visible bands, major morale events, rout, and Champion Rally.
2. MVP should include enough morale to support rout gameplay and command-layer recovery without carrying the full strategic/faction morale system.
3. Post-MVP morale scope includes faction-specific morale hooks, strategic starting modifiers, advanced numeric/accessibility detail, and deep per-objective morale tuning.
4. MVP rout should be mostly deterministic rather than random.
5. Rout resolution should use morale band, event severity, and relevant traits/modifiers to produce clear outcomes or threshold-based outcomes.
6. Morale-linked surrender/retreat negotiation is not part of MVP.
7. Retreat and surrender remain separate battle-type rules for MVP, not morale-driven systems.

Baseline rule text:

```text
MVP Morale Scope: tactical combat ships with visible morale bands, major event-driven morale changes, stack rout, and Champion Rally. The system should prove whether morale/rout adds useful battlefield pressure before adding strategic and faction-specific depth.

Post-MVP Morale Scope: faction-specific morale hooks, strategic starting modifiers, advanced numeric/accessibility detail, and detailed per-objective morale tuning are valuable but do not block first playable tactical combat.

MVP Rout Resolution: rout is mostly deterministic. Morale band, event severity, stack rout traits, Champion modifiers, and scenario rules determine whether a stack routs or stays controlled. Avoid hidden random morale rolls as the baseline MVP behavior.

MVP Retreat/Surrender Boundary: morale does not drive retreat or surrender terms in MVP. Retreat and surrender follow battle-type and scenario rules.
```

Deterministic vs probabilistic note:

```text
Deterministic rout means the same state produces the same result: for example, Shaken morale + severe loss + Fragile trait always routs, while Steady morale + minor loss does not.

Probabilistic rout means the same state produces a chance: for example, Shaken morale + severe loss + Fragile trait gives a 65% rout chance.

Approved direction: prefer the deterministic version for baseline/MVP. If later playtests show morale feels too solved or too rigid, limited uncertainty can be added as a post-MVP tuning layer.
```

Design notes:

- This cut keeps morale from overtaking basic combat implementation.
- Visible bands, event changes, rout, and Champion Rally are enough to test whether morale creates good decisions.
- Strategic/faction morale depth should return after the base combat loop is playable and understandable.
- Deterministic rout is easier to test, explain, balance, and debug than hidden random checks.
- If randomness is ever added later, the UI must still preview risk clearly and explain causes.

## End of Morale Block — Integration Check

Approved direction:

1. Basic morale/rout/Rally is part of MVP tactical combat.
2. Morale/rout should be referenced in the combat summary/current direction, not hidden only in the morale section.
3. Morale is kept separate from retreat/surrender/loss integration for now.
4. The next design area after morale should be victory/loss rewards and post-battle resolution.

Integration notes:

- MVP tactical combat includes basic morale/rout/Rally as an implementation-relevant system slice.
- The Summary and MVP Scope sections now explicitly mention basic morale/rout/Rally.
- Retreat and surrender remain battle-type/scenario systems, not morale-driven systems for MVP.
- Routed/removed stacks can still matter for battle-loss checks according to the rout rules, but no extra retreat/surrender morale coupling is being added here.
- Post-battle resolution is the natural next packet because retreat, surrender, rout, tactical loss, and asset commitment now need consequence handling.

## Post-Battle Resolution: Outcome Categories

Approved direction:

1. Post-battle resolution uses fixed primary outcome categories with optional scenario subtitles.
2. Fixed primary outcomes provide systemic clarity and consistent player expectations.
3. Scenario subtitles provide narrative and objective-specific precision without inventing incompatible outcome taxonomies for every battle.
4. Victory has no universal grade; victory is victory by default.
5. Defeat grades are scenario-specific only.
6. Post-battle resolution uses systemic rules first, with scenario overrides where needed.

Baseline primary outcomes:

```text
Victory: the player wins the battle under the battle's core rules.

Defeat: the player loses the battle under the battle's core rules.

Retreat: the player voluntarily exits through the battle-type retreat rules.

Surrender: the player accepts a negotiated/concessionary loss through surrender rules.

Extraction Success: the player completes an extraction-type objective.

Extraction Failure: the player fails an extraction-type objective.
```

Scenario subtitle rule:

```text
A scenario may attach a subtitle or result note to the fixed primary outcome to explain what actually happened. The primary outcome drives systemic resolution; the subtitle clarifies objective, narrative, and reward/loss context.
```

Example outcome display:

```text
Victory — Data Secured
Victory — Upload Completed, Asset Exposed
Defeat — Target Escaped
Defeat — Siege Line Broken
Retreat — Army Forfeited, Champion Escaped
Surrender — Forces Preserved, Reputation Damaged
Extraction Success — VIP Extracted, Drone Wing Lost
Extraction Failure — Asset Killed
```

Design notes:

- Fixed primary outcomes prevent vague or incompatible scenario resolution logic.
- Scenario subtitles keep non-standard missions from feeling mislabeled.
- Victory should not require universal Decisive/Standard/Pyrrhic grading; scenarios can express nuance in subtitles and rewards.
- Defeat grades are not universal. If a scenario needs Rout, Catastrophic Defeat, Asset Captured, or Target Escaped, it should express that as a scenario subtitle or override.
- Systemic rules handle default rewards/losses first; scenarios may override or add specific consequences.

## Post-Battle Losses and Preservation

Approved direction:

1. After ordinary Victory, surviving allied stacks return to the army, and losses inside stacks are permanent by default.
2. Victory preserves surviving stack entities but does not automatically restore killed units.
3. After ordinary Defeat, all committed allied stacks are lost by default.
4. Surrender preserves some surviving stacks based on surrender terms.
5. Surrender should be meaningfully softer than ordinary defeat or retreat, but still costly and negotiable.
6. Post-battle unit losses can be recoverable only through faction, building, asset, repair, medbay, insurance, body-subscription, drone recovery, biotech regrowth, or similar strategic systems.
7. There is no universal free automatic recovery percentage for killed units.

Baseline rule text:

```text
Victory Preservation: after ordinary Victory, all surviving allied stacks return to the army. Units killed inside those stacks are gone unless recovered by a specific strategic recovery system.

Defeat Loss: after ordinary Defeat, all committed allied stacks are lost by default. Scenario rules may override this only when the battle explicitly defines survivor escape, extraction, capture, recovery, or special preservation.

Surrender Preservation: after Surrender, some surviving stacks may be preserved according to negotiated terms, faction rules, scenario context, enemy policy, and strategic concessions. Surrender is softer than ordinary Defeat but not free.

Unit Recovery Systems: killed units are not automatically restored. Recovery requires specific infrastructure, faction mechanics, assets, buildings, insurance, repair capacity, medbay support, biotech regrowth, drone salvage, or scenario rules.
```

Design notes:

- Victory uses HoMM-like attrition: what survives comes home; what died is gone unless a separate recovery system applies.
- Default Defeat is harsh and clear: committed stacks are lost. Retreat, surrender, and extraction are the designed alternatives for changing that outcome.
- Surrender must preserve enough to be tempting, but its cost should be visible: resources, reputation, prisoners, leverage, access, legal exposure, contracts, or strategic debt.
- Recovery/repair systems fit the cyberpunk setting, but should be strategic investments and faction identity tools rather than automatic forgiveness.
- This preserves battle stakes while leaving room for medbay, repair bay, insurance, body subscription, drone salvage, and biotech faction mechanics later.

## Post-Battle Rewards and Spoils

Approved direction:

1. Victory rewards/spoils are granted by battle, site, or scenario reward tables.
2. Victory does not use one universal flat reward for every battle.
3. Defeated enemy stacks can produce salvage, intel, samples, hardware, data, or other spoils, but collection depends on post-battle recovery/salvage capacity.
4. Captures/prisoners are rare special outcomes, not routine spoils from defeated stacks.
5. Spoils are not magically collected just because an enemy stack was defeated.
6. Casualties reduce rewards only for specific objective types.
7. There is no universal casualty penalty applied to all rewards.
8. Surrender or retreat can preserve objective rewards already secured before leaving.
9. Surrender/retreat do not grant generic victory spoils by default.

Baseline rule text:

```text
Victory Rewards: after Victory, rewards are determined by the battle, site, or scenario reward table. Different battle types and strategic-map locations define different resources, intel, access, reputation, recruits, salvage, assets, or narrative outcomes.

Spoils and Salvage: defeated enemy stacks may create recoverable spoils, but collection requires relevant post-battle capacity such as salvage teams, drones, secure transport, data extraction, biotech containment, legal cover, or scenario access.

Casualty-Sensitive Rewards: casualties reduce reward quality or quantity only when the objective defines that relationship, such as rescue missions, extraction contracts, clean raids, public-defense operations, stealth jobs, or preservation-based objectives.

Secured Objective Rewards: if the player retreats or surrenders after already securing a discrete objective reward, that secured reward may be retained unless the battle or surrender terms explicitly remove it. Retreat/surrender do not grant generic spoils by default.
```

Design notes:

- Reward tables keep strategy-map rewards readable while letting locations and scenarios differ.
- Salvage/intel should feel logistical and cyberpunk: drones, cyberware, vehicles, data cores, biotech samples, and other recoverable materials require the means to recover and process them.
- Casualty penalties should be objective-authored, not a blanket punishment for hard-won battles.
- Retreat/surrender can still recognize partial objective success, but should not become a safe way to farm battlefield spoils.
- Recovery capacity creates design space for factions, buildings, assets, Champion operations, and strategic preparation.

## Rare Capture, Resurrection, and Post-Battle Control

Approved direction:

1. Routine post-battle capture/prisoner systems are not the baseline.
2. Enemy units should rarely be captured after battle.
3. Capture may exist through specific faction mechanics, scenario objectives, unit traits, Champion skills, assets, or authored events.
4. Resurrection, recovery, reanimation, reprinting, drone re-keying, Echo restoration, biotech regrowth, or similar post-battle return mechanics may exist for some factions or skills.
5. Capture/resurrection should be exceptional and identity-driven, not a standard reward pipeline.
6. Capturing enemy assets or special units requires explicit rules and appropriate capacity/containment when used.
7. General prisoner economy and routine capture-to-recruitment are not MVP baseline systems.

Baseline rule text:

```text
Rare Capture: enemy units are not routinely captured after battle. Capture only occurs when a scenario, faction mechanic, unit trait, Champion skill, support asset, or explicit objective allows it.

Factional Recovery / Resurrection: some factions or skills may recover, resurrect, reprint, repair, re-key, regrow, or restore units after battle. These are faction identity mechanics, not universal post-battle rules.

Special Capture Capacity: when a capture or containment mechanic exists, it defines its own requirements such as transport, holding space, drone control, data isolation, biotech containment, legal cover, or scenario custody.

No Routine Prisoner Economy: ordinary victories do not create a generic pool of prisoners for recruitment, ransom, or conversion. Those outcomes require explicit mechanics.
```

MVP boundary:

```text
MVP does not need a general capture/prisoner economy. MVP may include rare authored capture objectives or faction-specific recovery/resurrection mechanics if they are central to a faction or scenario.
```

Design notes:

- This avoids capture becoming a win-more army-growth loop.
- Recruitment from defeated enemies should be rare, authored, or faction-specific rather than a standard post-battle reward.
- Cyberpunk recovery fantasy still has room: drone salvage, backup bodies, Echo continuity, biotech regrowth, contractual body replacement, or resurrection-like faction mechanics can exist where appropriate.
- The key distinction: salvage/intel/data can be common post-battle rewards; captured living units should be rare.
- Champion capture remains separate and only happens by explicit scenario rule.

## Rare Recovery, Resurrection, and Faction Return Mechanics

Approved direction:

1. Post-battle unit return mechanics can exist as faction identity tools.
2. Some factions may recover, resurrect, repair, reprint, re-key, regrow, restore, insure, or otherwise return units after battle.
3. Return mechanics may restore the same unit/stack or create a replacement depending on the faction mechanic.
4. The usual output should be a replacement unit rather than true restoration of the exact same unit.
5. True restoration can exist, but should be rarer and more identity-specific.
6. Recovery/resurrection is limited by a combination of resource cost, infrastructure/capacity, time/cooldown, and faction/scenario constraints.
7. Whether recovery/resurrection is MVP should be decided during faction roster design, not added globally.

Baseline rule text:

```text
Faction Return Mechanic: a faction, Champion skill, asset, building, doctrine, or scenario may define a way for some lost units to return after battle. This is not a universal post-battle rule.

Replacement Output: most return mechanics create a replacement unit/stack rather than restoring the exact original. The replacement may represent repaired drones, contract replacement bodies, backup-grown biotech, reprinted shells, fresh recruits from an insurance pool, or other faction-specific continuity.

True Restoration: some rare mechanics may restore the same unit/stack identity, such as Echo continuity, preserved control cores, elite body recovery, or named/special unit restoration. These should be exceptional.

Return Limits: every return mechanic defines its cost and bottleneck, such as resources, repair bays, med/clone capacity, drone control, biotech vats, data backups, legal insurance, cooldowns, strategic time, or scenario restrictions.
```

MVP boundary:

```text
Do not add global recovery/resurrection to MVP by default. Include a simple version only if an MVP faction, scenario, or Champion identity requires it.

Faction roster design decides whether a faction needs a return mechanic and what form it takes.
```

Design notes:

- This preserves attrition while allowing cyberpunk identity mechanics.
- Replacement is the safer baseline because it avoids erasing losses completely while still supporting continuity fantasy.
- True restoration should feel special and may matter more for elite/special units than ordinary stacks.
- Strong return mechanics need strong bottlenecks or they will flatten post-battle consequences.
- Examples: drone repair pool, corporate body-insurance replacement, biotech regrowth, Echo-backed continuity shell, re-keyed autonomous unit, medbay survival protocol, faction-specific resurrection analogue.

## Post-Battle Resolution Summary UI

Approved direction:

1. The post-battle result screen should always show outcome, stack losses, rewards, objectives, assets at risk, and recovery/return effects.
2. The result screen should show why losses, rewards, missed rewards, recovery, salvage, forfeiture, and asset consequences happened.
3. Major unavailable or failed rewards should be shown with the reason they were missed.
4. Minor missed micro-salvage does not need to clutter the result screen.
5. The result screen should preview only available strategic follow-up actions.

Baseline result-screen sections:

```text
Outcome: fixed primary outcome plus optional scenario subtitle.

Objectives: secured, failed, partial, contested, or scenario-specific objective results.

Army Losses: surviving stacks, lost units inside surviving stacks, destroyed/lost committed stacks, routed/removed stacks where relevant.

Rewards and Spoils: resources, access, intel, reputation, recruits, salvage, assets, or other rewards gained.

Missed Major Rewards: important rewards or spoils not gained, with reasons such as no salvage capacity, objective failed, retreat forfeiture, surrender terms, enemy escape, asset destroyed, or time expired.

Assets at Risk / Asset Consequences: committed Champion assets, support assets, drone wings, transports, safehouses, channels, or special systems lost, damaged, exposed, preserved, or recovered.

Recovery / Return Effects: factional recovery, repair, replacement, resurrection, insurance, drone salvage, biotech regrowth, Echo restoration, or other return mechanics that apply.

Available Follow-Up Actions: only actions the player can actually take next, such as repair, recover, replace, debrief, process salvage, assign medbay, trigger insurance, continue, or resolve scenario-specific aftermath.
```

Reason-line examples:

```text
Army Forfeited: Retreat from field battle forfeits committed stacks.
Salvage Missed: No drone recovery team assigned.
Objective Reward Secured: Data core extracted before retreat.
Asset Exposed: Operator channel was committed and traced.
Replacement Available: Corporate body-insurance pool can replace 3 lost units next strategic turn.
Recovery Blocked: Biotech containment capacity full.
```

Design notes:

- Result UI must make consequence channels legible: outcomes, objectives, stack losses, assets, rewards, missed major rewards, and recovery effects.
- Always explain why important consequences happened. This prevents retreat, salvage, surrender, and recovery systems from feeling arbitrary.
- Show major missed rewards as teaching moments, but avoid spam for tiny salvage fragments.
- Follow-up actions should be actionable, not encyclopedic. If the player cannot do it now, hide it or put it in a detail tooltip.

## Post-Battle Block MVP Cut

Approved direction:

1. MVP post-battle resolution includes outcome, stack losses, basic rewards, secured objective rewards, missed major rewards, asset consequences, and result screen presentation.
2. Rare capture is post-MVP by default unless specifically required by a scenario, faction, skill, or asset.
3. Complex salvage capacity and complex asset consequence chains are post-MVP by default.
4. Faction return/recovery/resurrection mechanics are not globally post-MVP or MVP by default; inclusion is decided during faction roster design.
5. MVP salvage capacity should be numeric rather than only binary.
6. MVP includes asset-at-risk reporting if assets exist in MVP.

Baseline MVP contract:

```text
MVP Post-Battle Resolution: resolve and display the primary outcome, optional scenario subtitle, stack losses, basic reward table results, secured objective rewards, missed major rewards, asset consequences, and available follow-up actions.

MVP Salvage Capacity: MVP may use a simple numeric salvage capacity to limit how much salvage/spoils can be recovered. This should be lightweight and readable, not a full logistics simulation.

MVP Asset Reporting: if assets can be committed in MVP, the result screen must report whether committed assets were preserved, damaged, lost, exposed, recovered, or otherwise affected.
```

Post-MVP defaults:

```text
Rare Capture: post-MVP by default, except for authored scenario/faction/skill/asset needs.

Complex Salvage Logistics: post-MVP by default. MVP numeric salvage capacity should not require deep transport, legal, personnel, quarantine, and processing chains unless a scenario needs them.

Complex Asset Consequence Chains: post-MVP by default. MVP should report direct asset consequences, but deeper follow-on chains can wait.

Faction Return Mechanics: decided during faction roster design. Add to MVP only if an MVP faction's identity depends on it.
```

Design notes:

- This keeps post-battle resolution useful in MVP without implementing the entire aftermath economy.
- Asset consequences are MVP-relevant if assets are MVP-relevant; do not hide them if they exist.
- Numeric salvage capacity gives more tuning control than a binary support flag, but should stay simple.
- Rare capture remains explicitly outside the normal MVP reward loop to avoid snowballing.
- Recovery/resurrection remains faction-driven, not a global tactical-combat requirement.

## End of Post-Battle Block — Integration Check

Approved direction:

1. Post-battle resolution is listed in MVP scope as a compact post-battle resolution/result screen bullet.
2. General capture/prisoner economy is explicitly out of scope for MVP.
3. Rare authored or faction-specific capture can still exist when required by a scenario, faction, skill, or asset.
4. Faction return/recovery/resurrection mechanics are roster-design dependent, not globally included or excluded.
5. The next design area after post-battle resolution is army composition and deployment rules.

Integration notes:

- MVP Scope now includes post-battle resolution/result screen: outcomes, stack losses, basic rewards, secured objectives, missed major rewards, and asset consequences where assets exist.
- Out of Scope for MVP now includes general capture/prisoner economy.
- Out of Scope for MVP now also clarifies that global recovery/resurrection/return mechanics are not default; faction-specific return mechanics are decided during roster design.
- This closes the post-battle block and sets up the pre-battle counterpart: what army is brought, how stacks are selected, and how deployment works.

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

| Operation | Scope | Type | Concept |
|---|---|---|---|
| Sensor Lock | Tactical | Minor Command / Major Operation variant | Mark an enemy stack; allied ranged/indirect attacks gain accuracy or targeting access against it. |
| Spoof Targeting | Tactical | Major Operation | Enemy stack's next ranged or indirect attack suffers accuracy penalty, target restriction, or may be redirected to invalid/decoy target. |
| Blackout Pulse | Tactical | Major Operation | Temporarily disables Overwatch, targeting assists, and some networked bonuses in an area. |
| Counter-Intrusion | Tactical/Strategic | Minor Command / Reaction | Cancel or reduce an enemy Signal Operation; strategic version protects army/site from hostile feed manipulation. |
| Feed Poisoning | Strategic | Major Operation | Corrupt local information state before battle: enemy starts with worse Cohesion, false scouting, or reduced starting Command. |

#### Logistics Operations

| Operation | Scope | Type | Concept |
|---|---|---|---|
| Emergency Resupply | Tactical | Major Operation | Restore Capacity to one or more allied stacks, especially ranged/heavy units. |
| Field Repair | Tactical | Major Operation | Restore HP to mechanical/cybernetic/armored stacks or repair Shield/Armor state. |
| Rapid Redeploy | Tactical | Major Operation | Move an allied stack without spending its AP, or reposition a limited distance under restrictions. |
| Supply Corridor | Strategic/Tactical | Major Operation | Improve battle Supply State or negate Cut Off/Strained penalties for a limited time. |
| Extraction Window | Tactical/Strategic | Major Operation | Enable safe retreat, partial casualty recovery, evacuation of objective unit, or reduced post-battle losses. |

#### Fire Support Operations

| Operation | Scope | Type | Concept |
|---|---|---|---|
| Drone Strike | Tactical | Major Operation | Direct or semi-indirect strike against a marked/visible target; moderate damage, high precision. |
| Suppression Barrage | Tactical | Major Operation | Area pressure that applies Suppressed, damages lightly, and punishes clumping. |
| Delayed Missile Call | Tactical | Major Operation | Telegraph a high-impact strike resolving later; enemies can move, jam, shield, or disable spotters. |
| Area Denial Pattern | Tactical | Major Operation | Create temporary danger tiles that discourage movement or protect a flank. |
| Pre-Battle Fire Plan | Strategic/Tactical | Major Operation | Strategic preparation that starts combat with damaged cover, exposed enemies, or a first-round targeting advantage. |

#### Doctrine Operations

| Operation | Scope | Type | Concept |
|---|---|---|---|
| Rally | Tactical | Minor Command / Major Operation variant | Restore Cohesion or remove a low-Cohesion penalty from selected allied stacks. |
| Forced March | Tactical/Strategic | Minor Command / Major Operation | Tactical version grants movement/reposition; strategic version improves campaign movement or battle entry position. |
| Hold the Line | Tactical | Minor Command / Major Operation variant | Boost Defend, Retaliation readiness, ZoC reliability, or Shield/Armor for a defensive turn. |
| Coordinated Assault | Tactical | Major Operation | One target becomes vulnerable to follow-up attacks from multiple allied stacks this round. |
| Battle Rhythm | Tactical | Major Operation | Adjust initiative timing, recover Wait positioning, or let a stack act earlier under constraints. |

#### Covert Operations

| Operation | Scope | Type | Concept |
|---|---|---|---|
| Smoke Break | Tactical | Major Operation | Create smoke/obscurement that blocks line of sight, weakens Overwatch, and enables disengage. |
| Ambush Cell | Tactical/Strategic | Major Operation | Reveal hidden allied asset/stack, or start battle with a flanking/hidden position if prepared strategically. |
| Sabotage Kit | Tactical/Strategic | Major Operation | Disable a battlefield object, enemy supply source, turret, door, or heavy weapon for a limited time. |
| False Flag | Strategic | Major Operation | Manipulate feed/legitimacy before or after battle; may alter enemy response, reinforcements, or public accounting. |
| Decoy Signature | Tactical | Minor Command / Major Operation variant | Create false target/heat/signal/visual signature that soaks targeting or enables repositioning. |

#### Bio Operations — special/factional

| Operation | Scope | Type | Concept |
|---|---|---|---|
| Growth Surge | Tactical | Major Operation | Temporarily bolster a Bio stack's HP, Armor-like tissue, movement, or damage; may have post-effect decay. |
| Spore Bloom | Tactical | Major Operation | Area contamination that pressures cover, applies Chemical risk, or punishes enemies who remain clustered. |
| Tissue Reclamation | Tactical/Post-Battle | Major Operation | Recover losses from nearby organic casualties or convert battlefield biomass into healing/reinforcement. |
| Forced Adaptation | Tactical/Strategic | Major Operation | Grant temporary resistance or trait response after taking a damage type; strategic version prepares adaptation before battle. |
| Brood Signal | Tactical | Major Operation | Coordinate organic/swarm units: extra movement, Cohesion stabilization, or synchronized attack. |

#### Echo Operations — special/factional

| Operation | Scope | Type | Concept |
|---|---|---|---|
| Afterimage Action | Tactical | Major Operation | A recently damaged or destroyed stack leaves an Echo trace that performs a limited final action. |
| Continuity Anchor | Tactical/Strategic | Major Operation | Reduce casualty permanence, stabilize Cohesion after losses, or preserve command identity through disruption. |
| Ghost Command | Tactical | Minor Command / Major Operation variant | Issue an order through an Echo trace, allowing a stack to ignore some Signal/Cohesion disruption or act from memory-pattern discipline. |
| Identity Fracture | Tactical | Major Operation | Disrupt enemy Echo/networked/command-linked units; may reduce Cohesion, initiative, or Retaliation reliability. |
| Memorial Protocol | Strategic/Tactical | Major Operation | Convert fallen-unit memory into morale/Cohesion, recruitment legitimacy, or a battle-start Doctrine bonus. |

## Champion Progression Stats

### Primary Champion Stats

Approved direction:

Neon Champions uses **5 primary Champion stats** for now.

The stat model preserves the functional readability of HoMM's classic stat split while using setting-appropriate terms.

| Neon Champion Stat | HoMM Analogue | Primary Role |
|---|---|---|
| **Attack** | Attack | Improves army offensive performance. |
| **Defense** | Defense | Improves army durability and defensive performance. |
| **Control** | Spell Power | Improves Operation strength, duration, radius, reliability, or penetration across all channels. |
| **Command** | Knowledge | Increases starting Command pool and/or prepared operation capacity. |
| **Logistics** | Logistics / campaign skill elevated to primary | Improves supply, movement, capacity recovery, battle preparation, strategic reach, and post-battle recovery. |

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

| Field | Purpose |
|---|---|
| **Archetype pole** | Marshal, Operator, or Hybrid. |
| **Stat lean** | Top stats, secondary stats, and weak stats. |
| **Primary channels** | Doctrine, Signal, Logistics, Fire Support, Covert, Bio, Echo, or special/factional channels. |
| **Army preference** | Soft preference: melee, ranged, fast, armored, swarm, elite, expendable, mixed, etc. |
| **Unit specialization** | Optional explicit synergy with a creature/unit line, role, tier, faction roster segment, or upgrade family. |
| **Signature Doctrine** | Passive/conditional army-shaping identity. |
| **Core Minor Commands** | Repeated active tools that keep the Champion tactically present. |
| **Signature Major Operations** | High-impact prepared interventions. |
| **Strategic-map specialty** | Map movement, supply, scouting, site control, recruitment, recovery, political accounting, etc. |
| **Weakness / counterplay** | What opponents can exploit; what this Champion is bad at. |

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

| Outcome | Trigger | Consequence |
|---|---|---|
| **Extracted / Retreated** | Player retreats, surrenders, or uses valid extraction before total defeat. | Champion returns to a valid recruitment/base point. Army/supplies/tempo may be lost, but Champion control is preserved. |
| **Defeated / Lost** | Army loses and Champion does not successfully extract. | Champion leaves player's roster and enters a lost/missing/random/capture-style pool. They may later reappear through recruitment, events, ransom, or even enemy availability. |
| **Captured / Burned / Disavowed** | Special defeat condition, enemy ability, site rule, or campaign event. | Champion becomes a recovery objective, bargaining chip, intelligence risk, or temporarily unavailable asset. |
| **Permanently Dead / Gone** | Rare special condition. | Champion is permanently removed. Use sparingly to avoid save-scumming and narrative breakage. |

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

Neon Champions uses HoMM-style stacks as the baseline tactical entities. Each stack acts as one tactical entity.

Example:

- A stack of 8 Corporate Riflemen has 2 AP total.
- The stack may Move + Shoot, Shoot + Shoot, Reload + Shoot, or Overwatch + Defend.
- The stack's size modifies output/survivability, not action count.
- If a Champion grants +1 AP, the same stack can perform a third action this turn.
- Tactical stack-splitting is allowed through army management, but every split consumes one of the 7 active army slots.
- Specific abilities/assets may also create decoys, drone detachments, swarm fragments, Echo projections, or similar exceptions by explicit rule.

This preserves the power fantasy of larger forces while making each additional tactical entity spend real active-army capacity.

## Deferred: Elevation / High Ground

Elevation is not part of MVP.

If revisited later, use a simple abstract rule before considering true vertical maps:

- High-ground tiles may grant +1 range, +damage, or improved hit/graze outcome for ranged attacks.
- Flying/jump units may ignore height penalties.
- Avoid multi-floor interiors and complex vertical pathfinding until proven necessary by playtests.

## Open Questions

| Question | Owner | Deadline | Resolution |
|---|---|---|---|
| Does Move consume AP, or is there separate free movement plus AP? | shared | TBD | Current draft assumes Move costs 1 AP. |
| Which AP abilities belong to Champions versus faction/unit traits? | shared | TBD | Current draft favors Champions/faction identity. |
| How often should normal battles occur on the strategy map? | shared | TBD | Impacts combat complexity budget. |
