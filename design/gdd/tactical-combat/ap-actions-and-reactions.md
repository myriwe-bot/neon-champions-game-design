---
title: Tactical Combat — AP, Actions, and Reactions
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

# Tactical Combat — AP, Actions, and Reactions

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Activation, Initiative, AP, Wait, and Defend
- Base Actions
- Defend / Brace Direction
- Counterattacks, Zone of Control, and Overwatch

---

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

| Action                   |        AP Cost | Notes                                                                                 |
| ------------------------ | -------------: | ------------------------------------------------------------------------------------- |
| Move                     |              1 | Move up to the stack's Move value.                                                    |
| Disengage                |              1 | Leave hostile Zone of Control without triggering Retaliation.                         |
| Basic Attack             |              1 | Standard melee or ranged attack.                                                      |
| Heavy / Signature Attack |              2 | Stronger attack, burst, charge, artillery strike, etc.                                |
| Reload / Recharge        |              1 | Refills magazine, charge, heat capacity, or equivalent.                               |
| Defend                   | End activation | HoMM-like defensive action; consumes remaining activation and grants defensive bonus. |
| Overwatch                |              1 | Not universal; only available to units/stacks with the relevant trait.                |
| Simple Ability           |              1 | Tactical utility, light faction ability, minor Champion-granted action.               |
| Major Ability            |              2 | High-impact tactical ability.                                                         |
| Interact / Objective     |              1 | Capture, extract, activate, sabotage, loot, or mission-specific action.               |

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
