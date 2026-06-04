---
title: Tactical Combat — Statuses, Terrain, and Objectives
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

# Tactical Combat — Statuses, Terrain, and Objectives

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Status Effect Taxonomy
- Suppression
- Jammed
- Hacked
- Marked and Sensor Lock
- Stealth and Reveal
- Smoke and Vision Blocking
- Terrain Hazards
- Forced Movement
- Tactical Objectives and Interactions

---

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
6. Objective eligibility uses a **universal default with objective-specific overrides**.
7. Universal default: any **non-routed, non-disabled** stack can interact with or control an objective if it meets the objective's position/range/AP requirements.
8. Control zones, simple pickups, and extraction presence allow tiny/split stacks by default.
9. Terminals, sabotage, heavy extraction, repair/medical, and specialist objectives usually require specific unit capability, type, tag, status, or minimum strength.
10. Revealed/scouted objectives display whether the selected stack is eligible before the player commits movement or AP.

Objective interaction rule:

```text
Interact / Objective: Usually costs 1 AP while the stack is in the required position or valid interaction range. The objective defines whether interaction is allowed while engaged, whether statuses interfere, and whether progress resolves instantly or persists over time.
```

Objective type patterns:

```text
Control Zone: Usually checks occupation/control state and may allow engaged stacks to contest or hold. Tiny/split stacks count by default unless the objective specifies minimum strength or special control requirements.

Simple Pickup / Extraction Presence: Usually allows any non-routed, non-disabled stack at the required tile/range to interact or count as present, unless the payload/objective requires minimum strength, cargo capacity, or specialist handling.

Terminal / Hack Point: Usually requires 1 AP Interact and a valid Signal/Hacker/technical capability. May be blocked or modified by Jammed, Hacked, Sensor Lock, Signal interference, enemy adjacency, or objective security state.

Sabotage / Plant / Extract: Usually requires 1 AP Interact and may use instant completion, multi-step progress, or scenario-specific timing. Often requires Covert, Engineer, Heavy, Signal, or other specialist capability depending on fiction.

Heavy Extraction / Repair / Medical / Specialist Objective: Usually requires explicit unit capability, minimum strength, equipment, status condition, or support Asset.

Hold Point / Upload / Ritualized Operation: May use persistent progress across rounds and can be interrupted by displacement, Hacked, Suppressed, objective contesting, or scenario rules.
```

Eligibility and UI rule:

```text
Objective Eligibility: By default, any non-routed, non-disabled stack may interact with or control a revealed objective if it satisfies the objective's position, range, and AP requirements. Objectives may override this with capability, unit type, minimum strength, status, or scenario requirements. Once an objective is revealed or scouted, the UI must show whether the selected stack is eligible before the player spends movement or AP.
```

Design notes:

- Objectives should compete with attacking, moving, reloading, and defending; 1 AP Interact makes that tradeoff visible.
- Do not force all objectives into one model. Capture zones, terminals, extraction points, sabotage targets, and uploads need different pacing.
- Engaged interaction should be objective-specific: holding ground while engaged is fine; delicate hacking or extraction under melee pressure may not be.
- Status interaction should be fictional and readable, not universal. Suppressed might affect exposed upload work; Jammed might block technical interaction; Hacked might compromise a terminal or objective action.
- Forced movement can remove stacks from objective/control tiles, making displacement valuable in objective play.
- Objective eligibility must be visible once the objective is known. The player should not spend scarce movement/AP only to discover a revealed terminal requires Signal capability or a heavy extraction requires minimum strength.
- Tiny/split stacks are valid for spatial presence objectives by default, but specialist objectives should use explicit requirements so one-unit detachments do not solve every mission type.
