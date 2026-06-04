---
title: Tactical Combat — Targeting, Damage, and Defense
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

# Tactical Combat — Targeting, Damage, and Defense

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Line of Sight and Cover
- Range Bands and Minimum Range
- Damage Types, Weapon Tags, and Defense Tags

---

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
