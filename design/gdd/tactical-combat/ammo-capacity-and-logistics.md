---
title: Tactical Combat — Ammo, Capacity, and Logistics
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

# Tactical Combat — Ammo, Capacity, and Logistics

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Ammo, Capacity, Cooldowns, and Logistics

---

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
