---
title: Tactical Combat Deep Reference
type: research-note
status: draft
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-05-30
related: [design/gdd/tactical-combat, design/gdd/faction-unit-rosters, design/gdd/systems-index]
approval: pending
---

# Tactical Combat Deep Reference

> This file preserves the long tactical-combat working notes that previously lived in `design/gdd/tactical-combat.md`.
> It is reference material, not the first-read implementation contract.
> Use `design/gdd/tactical-combat.md` for the active readable GDD, then consult this note only when a section needs historical rationale or packet detail.

## How to Use This Reference

- Do not implement directly from this file unless the active GDD links to a specific section and confirms it is still current.
- Prefer the concise GDD for rules, scope, dependencies, and acceptance criteria.
- Treat contradictions in favor of the active GDD unless the user reopens the decision.
- When extracting detail from this reference, move the distilled rule back into the active GDD or a smaller named GDD.

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

### Deployment Phase, Scouting, and Tactics

Approved direction:

1. Default deployment is **battle-type/map-defined with limited rearrangement**.
2. In ordinary prepared battles, the player may **reorder stacks and choose from a few formation slots**, similar in spirit to HoMM's Tactics skill texture.
3. The **Tactics** secondary skill improves deployment advantage by rank/perk, with emphasis on larger/deeper deployment zones.
4. Ambush and surprise battles may lock army order, scatter/compress positions, give the attacker advantage, or apply other battle-type-specific deployment disruption.
5. Enemy deployment is visible before player deployment only with sufficient scouting/intel; without enough information, the fallback is a partial preview of rough enemy count/types while exact positions remain hidden.

Design contract:

- Deployment should not become a full roster-selection step. The active army is already chosen before battle.
- Ordinary prepared battles should provide quick formation agency, not slow tile-by-tile setup every fight.
- The map/battle type owns the deployment pattern first: field battle, ambush, siege, raid, defense, extraction, and story scenario can all use different deployment constraints.
- Army slot order remains meaningful because it influences default placement and formation options.
- Tactics should feel HoMM-readable: better initial positioning, more arrangement control, and stronger counter-deployment when supported by scouting/intel.
- Scouting and Intel systems should determine how much the player knows before deployment locks.

Example Tactics progression shape:

- **Basic Tactics**: improved reorder/formation options in ordinary prepared battles.
- **Advanced Tactics**: larger or deeper deployment zone where battle type permits.
- **Expert Tactics**: better enemy deployment preview, counter-deployment options, or stronger opening formation control when scouting/intel supports it.

Battle-type examples:

- **Prepared field battle**: limited formation slots and reorder before start.
- **Ambush suffered**: army order may be locked, positions compressed, scattered, flanked, or partially surrounded.
- **Ambush executed**: attacker may receive forward/side deployment options or delayed reveal.
- **Siege/defense**: defender may use fixed defensive zones, hardpoints, gates, or reserve/garrison exception rules.
- **Raid/extraction**: deployment may be tied to entry/exit edges and objective route.

UI/readability requirements:

- Deployment screen must clearly show which information is confirmed vs estimated.
- If exact enemy positions are hidden, the UI should label previews as estimated contacts, likely stacks, heat signatures, intercepted logistics, or similar fiction.
- Formation slots should be few and fast to choose from; avoid turning ordinary battles into lengthy setup puzzles.

### Active Army Management Timing and Constraints

Approved direction:

1. The player can freely rearrange active army stacks **anywhere on the strategy map outside battle** as the baseline. A later hostile-territory/ambush-risk modifier may be added if needed.
2. The player can swap units between active army and storage/garrison immediately before a known battle only if the army is **physically co-located** with that storage, garrison, convoy, town, base, or equivalent source.
3. Splitting/merging stacks in hostile territory is allowed, but may consume strategic movement/time or create ambush vulnerability.
4. The active army locks when the player **commits to an attack, mission, or site interaction**.
5. Scouting/intel can reveal enough to let the player adjust the active army before committing, but the default information should be partial rather than exact perfect counter-build data.

Design contract:

- Army rearrangement should be convenient by default; do not force town-only micromanagement unless playtests show free rearrangement trivializes preparation.
- Physical co-location matters for swapping with storage/garrisons. There is no default global reserve bench or instant global unit access.
- The active army can be tuned before a fight if the player has scouted, approached, or prepared properly.
- Once the player commits to a battle-triggering action, army composition is locked unless the battle type explicitly allows changes.
- Hostile-territory rearrangement is a future risk hook: if needed, it can cost time, consume movement, trigger exposure, or increase ambush chance.

Scouting/intel contract:

- Scouting should reward preparation by giving actionable pre-commitment information.
- Most scouting should reveal rough enemy composition, faction, tier range, role mix, defensive posture, terrain, or objective type rather than exact stack counts and positions.
- Higher Scouting/Intelligence, strong local intel, infiltration, or special Operations may reveal more precise counter-build information.
- The UI should distinguish estimated information from confirmed information.

### AI Valuation for Split and Duplicate Stacks

Approved direction:

1. AI target priority uses stack size, but modifies it by tactical role, objective threat, and immediate board impact.
2. AI recognition of retaliation-bait tactics depends on AI difficulty, faction, personality, and tactical sophistication. Basic AI may avoid obvious waste; stronger AI may actively punish bait stacks.
3. AI use of split stacks is faction/personality-specific.
4. Tiny stacks on objectives are treated as high-priority threats regardless of damage output when they affect objective progress/control.
5. Duplicate-stack targeting depends on AI role and tactical context, with wiping smaller duplicates for morale/action advantage as a common pattern.

Design contract:

- AI must not evaluate 1-stacks only by damage output. Blocking, ZOC, retaliation bait, objective interaction, scouting, and finishing blows all matter.
- AI should recognize that a tiny stack can be strategically decisive if it is contesting, capturing, uploading, extracting, or blocking a critical route.
- Retaliation-bait handling should scale by enemy competence:
  - low-discipline enemies may waste retaliation;
  - trained/tactical enemies avoid obvious bait when they have better targets;
  - elite, drone, cybernetic, Signal, or doctrine-heavy factions may punish bait stacks deliberately.
- AI use of split stacks should express faction identity. Disposable drone clouds, decoy-heavy factions, militia swarms, and covert cells may split more; disciplined corporate/heavy factions may prefer concentrated stacks.
- Duplicate stacks should not be treated as errors. AI can choose to wipe small duplicates for action/morale advantage, hit the largest concentration for attrition, or ignore both to pursue objectives.

AI evaluation examples:

- **Objective AI**: prioritizes a 1-stack on an upload/control/extraction objective over a larger stack that is not affecting the mission.
- **Morale-pressure AI**: prefers killing weak duplicate stacks to trigger morale/Cohesion pressure and reduce player activation count.
- **Artillery/area AI**: prefers large concentrations or clustered duplicate stacks.
- **Elite tactical AI**: avoids spending premium retaliation or high-value cooldowns into obvious 1-stack bait unless doing so protects a critical objective.
- **Swarm/decoy AI**: uses its own split stacks to block, screen, bait, and contest.

Implementation note:

- Future AI scoring should include separate terms for stack size/value, objective threat, blocking/ZOC threat, killability, morale impact, retaliation-bait risk, and faction/personality modifiers.

### Reinforcements, Garrisons, and Non-MVP Battle Exceptions

Approved direction:

1. MVP has **no ordinary mid-battle reinforcements**. Authored scenario exceptions may exist, but should be rare and explicit.
2. Garrison participation is **battle-type/site-specific**.
3. Nearby allied Champions/armies do not normally reinforce battles. Reinforcement-like support may exist only through specific Operations/Assets, and should be very rare because broad proximity reinforcement cuts against the HoMM-style active-army model.
4. Enemy reinforcements may arrive as timed scenario waves or as alarm/objective-triggered forces.
5. Reinforcement arrival communication depends on scouting/intel and scenario rules.

Design contract:

- “No normal reserve bench” remains the baseline. Reinforcements are exceptions, not the default combat model.
- The 7-slot active army is the normal player-controlled force in battle.
- Allied proximity reinforcement is not an ordinary strategic-map rule for MVP. Do not import Age-of-Wonders-style nearby army joining unless the broader strategic design explicitly changes direction.
- If allied reinforcement exists, it should be framed as a specific Operation, Asset, story event, faction mechanic, convoy support, drone drop, extraction team, or scripted scenario rule.
- Enemy reinforcement rules are more acceptable than allied reserve control because they create mission pressure, alarms, and escalation without giving the player a constant reserve bench.
- Reinforcements must be telegraphed enough to feel fair unless the scenario explicitly sells surprise as the point.

Garrison handling examples:

- **Small outpost**: garrison contributes map defenses, turrets, barriers, or objective control rather than extra stacks.
- **Town/base defense**: defender may choose the active 7-stack army from present Champion forces plus local garrison before battle.
- **Siege/arcology/bunker**: site-specific rules may add hardpoints, defenders, alarm waves, locked doors, breach points, or staged reinforcement zones.
- **Convoy defense**: garrison equivalent may be escort vehicles, civilian assets, cargo units, or extraction objectives rather than ordinary combat stacks.

Communication examples:

- High scouting/intel: exact or near-exact arrival direction, ETA, and likely composition.
- Moderate scouting/intel: rough direction and ETA range.
- Low scouting/intel: warning signs, alarms, radio chatter, heat signatures, or delayed reveal.
- Scenario surprise: hidden until triggered, but should have fiction and encounter design supporting the surprise.

### Battle Frequency and Tactical Complexity Budget

Approved direction:

1. Ordinary tactical battles should be **moderately frequent**: fewer and more meaningful than pure HoMM map-clearing, but not rare XCOM-style set-piece missions.
2. Ordinary MVP battles target **5-10 minutes**, with quicker 3-5 minute fights also desirable. Battles over 10 minutes should be exceedingly rare, if they exist at all.
3. Ordinary battle round count has **no hard target**. A 4-6 round shape is a useful default expectation, but longer or shorter battles depend on objective type, matchup, map, and battle stakes.
4. Ordinary pre-battle setup should be quick: reorder/formation/scouting summary, not full loadout puzzle every fight.
5. MVP tactical complexity should preserve the core identity: core combat, morale, objectives, and limited statuses/Operations. The current drafted systems can remain in the design, but advanced status/channel/edge-case depth should be implemented only as needed.

Design contract:

- Combat must feel **punchy, quick, and readable**, not overwhelming.
- Strategy-map pacing should not be stalled by long tactical battles as a norm.
- A normal fight should usually resolve before the player feels they have entered a separate mission game.
- The system can support richer battle types, but ordinary battles should not require exhaustive planning, long deployment, or many reinforcement waves.
- Tactical depth should come from clear high-impact choices: AP, positioning, objectives, morale/rout pressure, stack composition, and a small number of readable Champion/faction interventions.

Pacing targets:

- **Quick skirmish**: 3-5 minutes; simple objective or straight fight.
- **Ordinary battle**: 5-10 minutes; default target for MVP feel.
- **Long battle**: over 10 minutes; rare, reserved for siege/story/high-stakes scenarios if used.
- **Round count**: no hard rule; use 4-6 rounds as a rough ordinary-battle expectation, but let objective design and battle type own the final pacing.

MVP complexity stance:

- Include enough morale/objective/Operation texture to test the actual Neon Champions identity.
- Defer full-depth implementation of every drafted status, channel, reinforcement exception, and specialist objective until the MVP proves the core loop.
- If battles feel slow, reduce per-battle complexity and setup friction before cutting the HoMM-like active army model.

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

| Ability | Source | Draft Effect | Design Notes |
|---|---|---|---|
| Command Burst | Champion | Target allied stack gains +1 AP this turn. | Clean, readable, very strong. Needs cooldown/charge limit. |
| Tactical Uplink | Champion / network faction | Networked allied stacks in radius gain +1 AP; affected stacks become more vulnerable to EMP/hacking. | Strong cyberpunk tradeoff: tempo for network exposure. |
| Overclock | Champion / cybernetic or biotech faction | Target gains +1 AP and possibly damage; suffers heat, stress, self-damage, or vulnerability afterward. | Good for body-subscription/cybernetic themes. |
| Emergency Protocol | Champion / doctrine trait | A stack that kills an enemy refunds 1 AP once per turn. | Snowball-prone; use carefully. |
| Drone Relay | Champion / drone faction | Champion spends command resource or AP to let a drone stack act immediately or gain +1 AP. | Makes command infrastructure tactically meaningful. |
| Echo Possession / Continuity Override | Champion / Echo faction | Temporarily grants AP to a wounded, disabled, or collapsing stack so it can act before destruction. | Strong Neon Champions identity; links combat to death/Echo themes. |

### Balance Constraints

- Extra AP should usually come from the Champion, faction identity, or rare elite unit identity, not ordinary stack abilities.
- +1 AP to a stack is a major effect because it can enable move + attack + defend, triple attack if ammo allows, or attack + reload + attack.
- AP grants need visible UI/FX so players understand why a stack acted more than expected.
- AP manipulation must be constrained by cooldown, charges, command resource, risk, positioning, or faction weakness.
- Avoid permanent AP inflation in MVP.
- Normal tactical cases cap a stack at 3 total AP in one turn.
- AP refunds are especially snowball-prone; keep them signature and cap them at once per stack per turn.

## Tactical Combat MVP Cut / Implementation Readiness

This section defines the first playable tactical slice. The goal is to test whether the core HoMM-like stack combat, AP economy, morale pressure, objectives, deployment, and army-slot constraints work together before expanding into the full tactical vision.

Approved direction:

1. MVP tactical battles include **field battles plus control-zone and extraction/pickup objectives**.
2. MVP status scope includes **all drafted tactical statuses**, implemented in lean, data-driven forms rather than bespoke one-off scripts.
3. Champion/Operation MVP scope uses a **C-to-D path**: the first playable version must include one +AP ability, one Rally/morale ability, and one Signal/Intel ability, while the architecture should support expansion into the full Operation channel system.
4. MVP deployment includes **reorder/formation slots plus scouting preview**.
5. MVP army management includes **7 active slots, duplicate stacks, and stack splitting**.

MVP battle-type contract:

- **Straight field battle** remains the baseline combat test.
- **Control-zone objectives** add positional pressure without requiring full siege/raid systems.
- **Extraction/pickup objectives** test movement, stack splitting, sacrifice, and tiny-stack exploit rules.
- Ambush, siege, raid, multi-stage battles, and highly authored scenario battle types are deferred until the baseline proves stable.

MVP status contract:

- All drafted statuses may appear in MVP, but each status must have:
  - a clear owner/source;
  - visible UI state;
  - deterministic resolution order;
  - bounded duration or clear removal condition;
  - data-driven tuning values.
- Suppressed, Marked/Sensor Lock, and Routed are the minimum readability anchors.
- Jammed, Hacked, morale, network, damage-over-time, disable, and other drafted statuses must not become separate minigames in MVP unless explicitly promoted by a later packet.

Champion / Operation implementation contract:

- First playable tactical Champion/Operation content must include:
  - one **+AP / tempo** ability;
  - one **Rally / morale recovery** ability;
  - one **Signal / Intel** ability.
- These abilities should be authored as early representatives of the broader Operation channel model, not as hardcoded exceptions.
- Full Operation channel breadth is a supported direction, but it should scale after the minimum AP/morale/Signal triad is playable and understandable.

Deployment MVP contract:

- Players can reorder stacks into formation slots before battle.
- Scouting preview can reveal enemy formation/objective information according to scouting/intel rules.
- Full Tactics-skill progression, advanced deployment zones, hidden deployment, decoys, and initiative manipulation remain later-scope unless needed for the MVP slice.

Army-management MVP contract:

- The active army has **7 active slots**.
- Duplicate stacks of the same unit type are allowed if they consume separate active slots.
- Stack splitting is allowed and should be tested early because it interacts with objectives, Zone of Control, retaliation, scouting, and exploit prevention.
- Reserve benches, full garrison logistics, hostile-territory constraints, and storage UX are deferred from the first playable tactical slice.

Implementation readiness gates:

- A battle can be completed with field, control-zone, and extraction/pickup objectives.
- A player can deploy up to 7 active stacks, including duplicate/split stacks.
- Scouting preview affects deployment decisions.
- All MVP statuses have visible icons/tooltips and deterministic turn resolution.
- The AP/morale/Signal ability triad is implemented through a reusable ability/effect framework.
- Tiny-stack objective, ZOC, retaliation, and AP edge cases have automated tests or explicit QA scenarios.

## Tactical Implementation Contracts

This section turns MVP tactical scope into implementation-safe data contracts. The intent is to let the first tactical slice validate design risk while avoiding hardcoded one-offs that would block later Operation, status, and objective expansion.

Approved direction:

1. Abilities are authored as **data-driven ability records using reusable effect primitives and event hooks**.
2. Status effects resolve by **priority tier, then source order inside each tier**.
3. Objectives use **generic objective components plus scenario-specific overrides**.
4. Tactical test content follows a **C-to-D path**: MVP validation requires three core battles plus exploit/regression scenarios, then expands toward a full campaign slice.
5. Operation-channel architecture follows a **C-to-D path**: MVP includes shared ability schema plus channel fields/counterplay hooks, then expands toward the full Operation channel system.

Ability authoring contract:

- Each ability should be represented by a data record, not a bespoke class per ability.
- Ability records should compose reusable primitives such as:
  - grant AP;
  - spend Command/resource;
  - apply status;
  - remove status;
  - modify morale;
  - reveal/mark/sensor-lock;
  - move/push/pull;
  - deal damage;
  - trigger reaction/event hook;
  - check channel/counterplay condition.
- Custom code is allowed for new primitives or hooks, not for every individual ability.
- Ability records must expose tuning values for cost, cooldown, charges, target rules, range, duration, tags/channels, and UI text.

Status resolution contract:

- Statuses resolve in deterministic priority tiers.
- Within the same priority tier, statuses resolve by source/application order.
- Each status must define:
  - priority tier;
  - duration or removal condition;
  - stacking/refresh rule;
  - owner/source;
  - visible UI state;
  - save/load representation;
  - whether it can be cleansed, resisted, suppressed, or countered.
- Resolution order must be testable with explicit regression scenarios for AP grants, morale/rout, Jammed/Hacked/Signal interactions, and death/removal edge cases.

Objective implementation contract:

- Core objective behavior should use reusable components for capture zones, contesting, extraction, pickup, escort/carry, timers, and victory/failure checks.
- Scenario-specific overrides are allowed when a mission needs authored behavior, but overrides must declare which generic rule they replace or extend.
- Objective components must define eligibility rules for tiny/split stacks, summons/decoys/drones/Echo projections, routed units, disabled units, and hidden/scouted units.
- Objective state must be serializable and visible enough for player planning.

MVP tactical validation content:

- Required first validation set:
  - one straight field battle;
  - one control-zone battle;
  - one extraction/pickup battle;
  - exploit/regression scenarios for stack splitting, tiny stacks, Zone of Control, retaliation, AP grants/refunds, objective eligibility, status resolution, and morale/rout.
- After this validation set is stable, expand toward a **full campaign slice** that demonstrates battle selection, army management, deployment, Champion/Operation use, post-battle consequences, and progression context.

Operation-channel architecture contract:

- MVP abilities should use the shared ability schema.
- The schema should include channel fields and counterplay hooks even if most channels are inactive in the first tactical slice.
- Channel/counterplay fields should support later Signal, Covert, Media, Logistics, Fire Support, Medical/Recovery, Psychological Warfare, and faction-specific Operations without rewriting the ability model.
- Full channel breadth is a target state, not a blocker for the first three tactical validation battles.

Implementation readiness gates:

- Designers can author the MVP AP, Rally/morale, and Signal/Intel abilities from data records.
- Status interactions produce deterministic logs suitable for tests/debugging.
- Objective logic can run field, control-zone, and extraction/pickup battles without custom battle-mode classes for each case.
- Regression scenarios cover the known exploit surfaces before the tactical MVP is considered stable.
- The ability schema can represent inactive/future Operation channel metadata without changing save format or ability identity.

## Ability / Effect Schema Primitives

This section defines the minimum reusable ability/effect schema needed for tactical MVP and later Operation-channel expansion. The design should keep ordinary ability authoring data-driven while leaving a path toward deeper rules-engine behavior for rare or full-vision effects.

Approved direction:

1. Base ability structure follows a **C-to-D path**: ability record + trigger conditions + ordered effect blocks + costs/cooldowns now, with a path toward fuller card/stack-like rules behavior later if needed.
2. Effect blocks resolve in **listed order**, but each effect can declare a **timing phase**.
3. Primitive effect set follows a **C-to-D path**: MVP includes the extended primitive set needed for AP, morale, statuses, resources, summoned/created entities, objectives, and reactions, with room to grow toward a larger full-vision library.
4. Targeting follows a **C-to-D path**: MVP uses structured target-query records, with later support for scripted/custom predicates for rare abilities.
5. Future Operation channels follow a **C-to-D path**: ability data includes channel tags, counterplay tags, visibility/noise fields, and later expands toward the full Operation channel subsystem.

Base ability record contract:

- Ability identity:
  - stable id;
  - display name;
  - source type: unit, Champion, faction, objective, asset, scenario, or system;
  - tags/channels;
  - tooltip/UX text;
  - animation/VFX/SFX hooks.
- Conditions:
  - trigger condition: active use, passive, on turn start, on turn end, on kill, on damaged, on routed, on objective event, on status event, etc.;
  - target query;
  - source eligibility;
  - battle/objective/scenario restrictions;
  - channel/counterplay conditions.
- Costs and limits:
  - AP cost;
  - Command/resource cost;
  - cooldown;
  - charges;
  - per-turn/per-battle caps;
  - once-per-stack/per-source restrictions where needed.
- Effects:
  - ordered effect blocks;
  - optional timing phase per block;
  - rollback/fizzle behavior if a block fails;
  - logging/debug metadata.

Effect resolution contract:

- Effects resolve in listed order by default.
- Each effect block may declare a timing phase, such as pre-cost, cost, targeting, pre-effect, main effect, post-effect, reaction, cleanup, or objective check.
- Timing phases are deterministic and inspectable in combat logs.
- Interrupts/reactions should be represented through declared hooks and reaction phases, not arbitrary hidden execution.
- Full event-queue/interrupt-stack behavior is deferred unless later complexity proves it necessary.

MVP primitive effect set:

- Required primitive categories:
  - damage / healing / recovery;
  - grant/spend/refund AP;
  - modify morale / trigger Rally / affect rout state;
  - apply/remove/refresh status;
  - reveal, mark, sensor-lock, hide, or alter visibility;
  - move, push, pull, reposition, or restrict movement;
  - spend/refund Command or other tactical resources;
  - summon/create temporary entity, drone, decoy, Echo projection, mine, turret, relay, or similar explicitly authored entity;
  - objective interaction: pickup, drop, carry, contest, capture, extract, score progress, reset progress;
  - trigger reaction/event hook.
- The full-vision primitive library can expand later, but new primitives should be justified by multiple abilities or a signature faction/system need.

Targeting contract:

- MVP targeting uses structured target-query records rather than hardcoded per-ability targeting.
- Query fields should support:
  - side: self, ally, enemy, neutral, any;
  - target type: stack, Champion, tile, objective, created entity, drone, decoy, Echo projection, terrain feature;
  - range and distance metric;
  - line of sight / line of effect requirements;
  - status filters;
  - AP/morale/rout filters;
  - size/stack-count filters where needed for tiny-stack and split-stack rules;
  - objective eligibility filters;
  - visibility/scouting filters;
  - channel/counterplay filters.
- Later scripted predicates may be added for rare abilities, but the default authoring path should remain query composition, not arbitrary scripts.

Operation metadata contract:

- Ability records should include future-facing Operation metadata even when most Operation channels are inactive in MVP:
  - operation/channel tags;
  - counterplay tags;
  - visibility/noise profile;
  - traceability/detectability;
  - jamming/hacking/interference hooks;
  - UI disclosure level;
  - faction or Champion doctrine tags.
- These fields should not force full Operation-channel simulation in the first playable slice.
- They should prevent schema churn when the design expands from the AP/morale/Signal triad into broader Operations.

Implementation readiness gates:

- The MVP +AP, Rally/morale, and Signal/Intel abilities can be authored as data records using this schema.
- At least one objective interaction uses ability/effect primitives rather than custom battle code.
- Combat logs can show trigger, targeting, cost, effect order, status application, reaction, and cleanup.
- Save/load preserves stable ability ids, status ids, cooldowns, charges, channel metadata, and created-entity ownership.
- Regression tests cover effect ordering, fizzle behavior, AP caps/refunds, target filters, status priority, and objective eligibility.

## Status Schema and Resolution

This section defines the minimum status-effect contract for deterministic tactical play while preserving Neon Champions' emphasis on Signal, deception, hidden information, morale, hacking, and counterplay.

Approved direction:

1. Base status structure uses **status id + duration/removal + priority tier + stacking rule + owner/source + visible UI**.
2. Stacking uses **per-status stacking modes**: refresh, replace-if-stronger, stack count, unique-per-source, or similar bounded modes.
3. Status visibility uses a **full fog-of-war / information model**, because hidden state, deception, scouting, and Signal/Intel are core to the game.
4. Cleanse/resist/counterplay uses **typed counterplay tags**: cleanse, resist, immunity, suppression, jamming, hacking, morale recovery, etc.
5. MVP status resolution requires at least the full tactical phase set: battle start, turn start, pre-action, on-hit/on-damage, post-action, objective check, morale/rout check, death/removal, and turn end.

Base status record contract:

- Identity:
  - stable status id;
  - display name;
  - status family/category;
  - tooltip/UX text;
  - icon/VFX/SFX hooks.
- State:
  - duration or removal condition;
  - priority tier;
  - resolution phase hooks;
  - stacking mode;
  - owner/source;
  - target entity;
  - intensity/count/value fields if applicable.
- Rules:
  - effect primitives or modifiers applied by the status;
  - refresh/replace/expire behavior;
  - cleanse/resist/immunity/counterplay tags;
  - save/load representation;
  - combat log visibility.
- Presentation:
  - visibility level by observer;
  - UI disclosure rules;
  - revealed/identified/decoded state;
  - preview text for known effects and uncertainty text for unknown effects.

Stacking contract:

- Each status declares one bounded stacking mode rather than freeform stacking code.
- Required stacking modes:
  - **refresh** — reapplication extends or resets duration;
  - **replace-if-stronger** — stronger application replaces weaker application;
  - **stack count** — applications increment a capped count/intensity;
  - **unique-per-source** — separate instances can coexist only if their source differs;
  - **non-stacking** — reapplication has no effect or only updates source metadata.
- Each status must declare maximum stack count/intensity where relevant.
- Stacking behavior must be visible or explainable enough that players can predict important outcomes.

Information / visibility contract:

- Status visibility is part of the tactical information model, not just UI polish.
- A status may have different disclosure levels for owner, opponent, neutral observer, scouted observer, and revealed/decoded observer.
- Required visibility states:
  - public and fully identified;
  - visible but values/remaining duration hidden;
  - owner-only;
  - hidden until triggered;
  - suspected/anomaly state;
  - scouted/revealed/decoded;
  - false/decoy status if later deception systems require it.
- Signal, Intel, scouting, jamming, hacking, stealth, and Media/Psychological effects may alter what status information is visible.
- Hidden statuses still need deterministic server/simulation state and replay/debug visibility for QA.
- The player-facing model must avoid unfairness: hidden status effects should be either inferable, scoutable, or deliberately framed as deception/uncertainty.

Counterplay contract:

- Statuses declare typed counterplay tags instead of bespoke hardcoded counter rules.
- Required counterplay tags include:
  - cleanse;
  - resist;
  - immunity;
  - suppression;
  - jamming;
  - hacking;
  - morale recovery;
  - reveal/decode;
  - dispel/remove;
  - armor/biotech/network/firewall/faction-specific resistance tags as needed.
- Abilities, faction traits, Champion skills, and Operations can reference these tags for broad counterplay.
- Counterplay should distinguish prevention, mitigation, removal, concealment, and information revelation.

Resolution phase contract:

- MVP status hooks must support at least:
  - battle start;
  - turn start;
  - pre-action;
  - on-hit / on-damage;
  - post-action;
  - objective check;
  - morale/rout check;
  - death/removal;
  - turn end.
- Within a phase, statuses resolve by priority tier, then source/application order.
- Status resolution should produce deterministic combat log entries, including hidden debug logs for QA/replay when player-facing information is concealed.
- Arbitrary hook/event-queue behavior is deferred until the bounded phase model fails a real design need.

Implementation readiness gates:

- Suppressed, Marked/Sensor Lock, Routed, Jammed, Hacked, morale modifiers, and objective-affecting statuses can all be represented by the status schema.
- Status stacking behavior is testable per status mode.
- Hidden/partial status information can be represented separately from true simulation state.
- Cleanse/resist/counterplay abilities can target status tags instead of specific status ids only.
- Automated or explicit QA scenarios cover phase order, hidden visibility, reveal/decode, cleanse/removal, stacking, rout/death interactions, and save/load.

## Tactical Information Model

This section defines how hidden, partial, suspected, false, and revealed tactical information works. The goal is to support Signal/Intel, scouting, deception, hidden statuses, traps, mines, created entities, and later Operation-channel play without making tactical outcomes feel arbitrary.

Approved direction:

1. MVP information states use the **full layered model**: true state, observed state, suspected state, false/decoy state, and revealed/decoded state.
2. Tactical object coverage follows a **C-to-D path**: MVP applies the information model to statuses, hidden units, objectives, traps/mines, and created entities, then expands toward all tactical objects including abilities, intent, cooldowns, resources, channels, and objective rules.
3. Suspected/anomaly information uses **type family, confidence, and last-known location/turn**.
4. False/decoy information can mimic known object categories but must have discoverability and counterplay rules.
5. Debug/replay follows a **C-to-D path** now, with full timeline inspector as the eventual target: MVP needs player-visible, opponent-visible, and all-truth debug modes; later tooling should inspect visibility-state changes per observer over time.

Information-state contract:

- **True state** — authoritative simulation state used by rules, tests, save/load, and all-truth debug tools.
- **Observed state** — what a given observer currently knows and can act on.
- **Suspected state** — incomplete information that marks an anomaly, likely object, or last-known fact without confirming exact details.
- **False/decoy state** — deliberately misleading information created by abilities, decoys, spoofing, stealth, Media/Psychological effects, or scenario rules.
- **Revealed/decoded state** — information promoted from hidden/suspected/false/partial into confirmed knowledge by scouting, Signal, Intel, detection, hacking, or scripted reveal.

Object coverage contract:

- MVP information-model objects include:
  - hidden or partially identified statuses;
  - hidden units/stacks;
  - objectives and objective state where uncertainty is intended;
  - traps, mines, relays, sensors, turrets, drones, Echo projections, decoys, and other created entities;
  - pickup/extraction objects if scenario rules hide, mask, or misidentify them.
- Full-vision expansion may include:
  - ability intent;
  - cooldowns and charges;
  - tactical resources;
  - Operation channels;
  - counterplay hooks;
  - objective rules;
  - hidden faction/Champion traits;
  - AI plans or predicted actions where appropriate.
- The design default is not "hide everything." Hidden information must create meaningful decisions, not random punishment.

Suspected/anomaly contract:

- Suspected information should carry:
  - type family, such as unit, status, trap, mine, objective, signal source, relay, decoy, or unknown anomaly;
  - confidence level;
  - last-known location or affected entity;
  - last-known turn/phase;
  - source of suspicion, such as scouting, sensor ping, attack trace, movement noise, objective interaction, or counterintel warning.
- Suspected markers should be readable enough to support planning but incomplete enough to preserve uncertainty.
- Confidence should be discrete/bounded for MVP, not a deep probabilistic belief simulation.

False/decoy contract:

- Decoys and false information may mimic known categories such as units, statuses, objectives, mines, relays, signals, or created entities.
- Each false/decoy object must declare:
  - what category it mimics;
  - what observers can see;
  - what interactions reveal, decode, or disprove it;
  - whether it can block movement, contest objectives, draw attacks, trigger reactions, or only mislead UI/targeting;
  - what happens when revealed or destroyed.
- Decoy gameplay must remain counterplayable through scouting, Signal/Intel, proximity, attacks, reveal effects, or faction-specific counters.
- False information should be used as a signature tactical layer, not as constant UI noise.

Debug / replay contract:

- MVP replay/debug modes must include:
  - player-visible view;
  - opponent-visible view;
  - all-truth debug view.
- Later tooling should expand into a timeline inspector that shows visibility-state changes per observer, including when information became suspected, observed, false, revealed, decoded, expired, or invalidated.
- Hidden-state bugs are high risk; every hidden/false/revealed transition should be loggable with true-state and observer-state records.
- QA needs all-truth visibility even when normal replays preserve player-facing uncertainty.

Implementation readiness gates:

- A hidden status, suspected trap/mine, hidden unit, decoy entity, and revealed objective state can all be represented without bespoke per-case UI state.
- Scouting/Signal/Intel effects can promote information from hidden/suspected/false/partial to revealed/decoded.
- False/decoy objects have explicit reveal and counterplay rules.
- Combat logs/replay can display player-visible, opponent-visible, and all-truth views.
- The model avoids unfair hidden outcomes by ensuring major hidden threats are inferable, scoutable, revealable, or deliberately framed as deception.

## Objective System Schema

This section defines objective components so field battles, control zones, extraction/pickup missions, exploit tests, and later campaign-slice objectives do not become isolated custom scripts.

Approved direction:

1. Base objective structure follows a **C-to-D path**: objective id + component list + state machine + victory/failure conditions + UI/logging now, with a path toward fuller mission scripting if campaign-slice needs justify it.
2. Reusable objective components follow a **C-to-D path**: MVP includes capture zones, extraction points, pickup/carry, timers, contesting, score/progress, ownership, and eligibility filters; later expands toward escort, sabotage, defense waves, multi-stage missions, and branching outcomes.
3. Objective eligibility uses **eligibility query records** with stack size, unit type, status, routed/disabled state, created-entity type, visibility, and faction/objective tags.
4. Scenario-specific overrides are allowed only as **declared overrides/extensions of generic components**.
5. Objective information visibility follows a **C-to-D path**: objective existence, state, and rules have separate visibility levels now, with later support for false objectives, hidden objectives, spoofed progress, and masked rules.

Base objective record contract:

- Identity:
  - stable objective id;
  - display name;
  - objective family: field battle, capture/control, extraction, pickup/carry, survival, elimination, scenario, etc.;
  - scenario/map owner;
  - UI/logging text.
- Components:
  - reusable objective components;
  - eligibility queries;
  - progress/scoring rules;
  - visibility rules;
  - reward/consequence hooks.
- State machine:
  - inactive;
  - active;
  - contested;
  - progressing;
  - completed;
  - failed;
  - expired;
  - revealed/decoded if hidden information applies.
- Outcomes:
  - victory conditions;
  - failure conditions;
  - partial-success conditions if later scenario design needs them;
  - post-battle consequence hooks.

MVP reusable component set:

- **Capture/control zone** — tracks eligible units contesting or controlling an area.
- **Extraction point** — checks whether eligible entities exit, survive, or deliver carried objects.
- **Pickup/carry object** — supports pickup, drop, transfer if allowed, carrier death/drop behavior, and extraction delivery.
- **Timer** — turn/round/phase counters for deadlines, escalation, scoring, or expiry.
- **Contesting** — determines how opposing eligible entities pause, reverse, or block progress.
- **Score/progress** — supports accumulated progress, threshold completion, per-turn scoring, and reset/decay rules.
- **Ownership/control** — tracks faction/side/controller and transfer rules.
- **Eligibility filter** — queries which stacks/entities can interact, contest, carry, score, or extract.

Full-vision component expansion may include escort, sabotage, defense waves, multi-stage objectives, branching outcomes, deception objectives, scripted campaign consequences, and special scenario setpieces.

Eligibility contract:

- Objective eligibility is data-driven through query records, not hardcoded per objective.
- Query fields should support:
  - stack size / tiny-stack thresholds;
  - unit type and unit tags;
  - Champion, stack, drone, decoy, Echo projection, summoned/created entity, relay, mine, turret, or objective object;
  - routed, disabled, suppressed, jammed, hidden, revealed, or other status filters;
  - visibility/scouting state;
  - faction/side/controller;
  - objective-specific tags such as can-carry, can-contest, can-score, can-extract, can-trigger, can-block.
- Eligibility rules must explicitly handle split stacks and created entities because they are high-risk exploit surfaces.

Scenario override contract:

- Scenario-specific behavior is allowed only as a declared override or extension of a generic component.
- Each override must declare:
  - the generic component it modifies;
  - which rule is replaced or extended;
  - why generic behavior is insufficient;
  - visibility/logging behavior;
  - test or QA scenario coverage.
- Overrides should be rare for MVP validation battles and more common only in authored campaign-slice missions.
- Custom scripts must not silently bypass eligibility, visibility, objective-state, or logging contracts.

Objective visibility contract:

- Objective information has separable visibility layers:
  - existence: whether the player knows an objective exists;
  - location: where the objective is;
  - state/progress: current control, progress, timer, carrier, or contested state;
  - rules: how the objective scores, fails, or can be interacted with;
  - reward/consequence: what happens after completion or failure.
- MVP should support hidden or partial objective information when tied to scouting, Signal/Intel, deception, or scenario design.
- Full-vision expansion may support false objectives, hidden objectives, spoofed progress, masked rules, and decoy pickups, but each must have discoverability and counterplay.

Implementation readiness gates:

- Field battle, control-zone, and extraction/pickup objectives can be built from the objective schema.
- Tiny-stack, split-stack, routed, disabled, hidden, decoy, drone, and Echo-projection eligibility are all explicit and testable.
- Objective progress and contesting are deterministic and loggable.
- Objective visibility integrates with the tactical information model.
- Scenario overrides cannot bypass generic component contracts without declaring and testing the exception.

## Tactical Data / Save / Replay Contracts

This section defines what tactical state must be serializable, replayable, and testable so hidden information, statuses, objectives, ability effects, and AP/morale/Signal interactions remain debuggable.

Approved direction:

1. Tactical MVP save granularity is **battle start, turn boundaries, and after each stack activation**.
2. MVP replay model stores **initial state + player commands + RNG seeds + periodic checkpoints**.
3. Hidden-information save state follows a **C-to-D path**: true state + observer-visible states + suspected/false/revealed metadata now, with full visibility timeline per observer later.
4. Combat log detail follows a **C-to-D path**: structured logs now, expanding toward full causal event graphs as tooling matures.
5. Schema/versioning follows a **C-to-D path**: stable ids + schema version fields + migration hooks now, with a fuller formal migration framework later if save/replay longevity demands it.

Save granularity contract:

- Tactical saves/checkpoints must support:
  - battle start;
  - turn boundaries;
  - after each stack activation.
- Stack activation checkpoints should capture all state needed to resume without replaying the entire battle.
- Atomic event/effect reconstruction is not required for MVP save granularity, but the data model should not block later event-sourced debugging.
- Save/checkpoint state must include AP state, status state, objective state, visibility state, ability cooldowns/charges, RNG state or seed cursor, created entities, and battle phase/turn/activation index.

Replay model contract:

- MVP replay stores:
  - initial battle state;
  - player commands / AI commands;
  - RNG seeds or deterministic RNG stream state;
  - periodic checkpoints.
- Replay must be deterministic enough to reproduce tactical outcomes during QA.
- Checkpoints reduce replay fragility and make mid-battle debugging practical.
- Full event-sourced replay of every atomic effect is deferred, but structured logs should preserve enough causal data to diagnose common issues.

Hidden-information persistence contract:

- Saves and replays must preserve:
  - true simulation state;
  - observer-visible state for each side/observer;
  - suspected/anomaly metadata;
  - false/decoy metadata;
  - revealed/decoded metadata;
  - stale/last-known information where relevant.
- Later tooling should expand to a full visibility timeline per observer, tracking when information became hidden, suspected, observed, false, revealed, decoded, expired, or invalidated.
- Hidden information must survive save/load without leaking to the wrong observer or losing QA all-truth visibility.

Structured combat log contract:

- MVP structured logs should include:
  - turn/phase/activation index;
  - trigger/event type;
  - source id;
  - target id/query result;
  - costs paid;
  - effect blocks resolved;
  - AP changes;
  - status applications/removals/refreshes;
  - morale/rout changes;
  - objective state/progress changes;
  - visibility state changes;
  - RNG rolls/seed references where relevant;
  - fizzle/failure reasons.
- Player-facing logs may hide or summarize hidden information, but debug/all-truth logs must preserve the real causal data.
- Later tooling may promote this into a full event graph with causal links between commands, triggers, effects, reactions, statuses, objective changes, and visibility transitions.

Schema and versioning contract:

- Data records, saves, and replays must use stable ids for units, abilities, statuses, objectives, effects, created entities, and scenario objects.
- Tactical data must include schema version fields.
- Migration hooks should exist for saves, replays, and data records when ids/fields change.
- MVP does not require a heavy formal migration framework, but schema changes must not silently corrupt tactical saves/replays.
- Versioning is especially important for data-driven abilities, status definitions, objective components, and hidden-information metadata.

Implementation readiness gates:

- A battle can be saved and resumed at battle start, turn boundary, and after stack activation.
- A replay can reproduce a tactical battle from initial state, commands, RNG seed/state, and checkpoints.
- Hidden/suspected/false/revealed information persists correctly per observer.
- Structured logs expose enough detail to debug AP grants/refunds, status resolution, objective eligibility/progress, morale/rout, and visibility changes.
- Schema versions and stable ids exist for tactical data records before broad content authoring begins.

## Tactical MVP Content Matrix

This section defines the minimum tactical content needed to validate the MVP systems. The goal is to prove field battles, objectives, AP/morale/Signal abilities, status resolution, hidden information, stack splitting, and exploit surfaces with actual playable scenarios rather than abstract schemas alone.

Approved direction:

1. MVP validation battles follow a **C-to-D path**: start with three core battles plus dedicated exploit/regression scenarios, then expand into a linked campaign slice.
2. Playable faction coverage follows a **B-to-C-to-D path**: start with two small asymmetric factions, expand to three, then eventually the full initial faction set.
3. MVP faction unit coverage uses the **full roster** for the selected MVP factions.
4. Champion/Operation abilities follow a **C-to-D path**: start with six abilities, two each for AP/tempo, Rally/morale, and Signal/Intel, then expand toward 9+ abilities across multiple channels.
5. Status coverage follows a **C-to-D path**: start with 8-10 validation statuses covering the main tactical categories, then expand toward all drafted statuses.

Validation battle contract:

- First validation set:
  - one straight field battle;
  - one control-zone battle;
  - one extraction/pickup battle;
  - dedicated exploit/regression scenarios for stack splitting, tiny stacks, Zone of Control, retaliation, AP grants/refunds, objective eligibility, hidden information, and status resolution.
- After the first validation set is stable, expand into a campaign slice with linked battles, army persistence, Champion/Operation use, post-battle consequences, progression context, and objective variety.

Faction rollout contract:

- MVP begins with **two asymmetric factions** so combat can test different tactical identities without needing the full faction set immediately.
- The next validation expansion adds a **third faction** to test whether the systems generalize beyond a binary matchup.
- Full initial faction coverage comes after the tactical loop, schemas, and content pipeline prove stable.
- Even at two-faction MVP scope, faction choice should express real Neon Champions asymmetry, not palette-swapped mirror units.

Unit roster contract:

- For the selected MVP factions, use the **full intended roster** rather than a partial 3/5/7-unit sample.
- This is a deliberate scope increase: it tests army composition, 7-slot pressure, duplicate stacks, stack splitting, unit-role overlap, counters, objective roles, and roster identity early.
- If implementation load becomes too high, content can be staged internally, but the design target remains full roster coverage for MVP validation factions.
- Roster implementation should prioritize data-driven unit definitions so full roster coverage does not create one-off tactical code.

Champion / Operation ability content contract:

- Initial MVP ability set:
  - two AP/tempo abilities;
  - two Rally/morale abilities;
  - two Signal/Intel abilities.
- The six-ability set should test variation, not duplicates:
  - one clean/simple representative per category;
  - one more conditional, counterplay-heavy, or faction-flavored representative per category.
- Expansion path:
  - add 9+ abilities across multiple Operation channels once the six-ability set proves the schema;
  - later connect abilities to broader Champion progression, faction doctrine, assets, and full Operation-channel systems.

Status content contract:

- Initial validation set should include **8-10 statuses** covering:
  - Suppressed / action pressure;
  - Marked or Sensor Lock / targeting and information;
  - Routed / morale collapse;
  - Jammed / Signal disruption;
  - Hacked / hostile system control or interference;
  - morale modifier or panic/stress state;
  - visibility/hidden/revealed state;
  - AP/action restriction or exhaustion state;
  - objective-affecting state such as carrying, contesting, extracted, disabled, or anchored;
  - one faction- or Operation-flavored status if needed to prove extensibility.
- Expansion path moves toward all drafted statuses after the first validation set proves status resolution, visibility, counterplay, and save/replay stability.

Implementation readiness gates:

- The three validation battles and exploit/regression scenarios are playable and replayable.
- Two asymmetric factions are playable with full rosters and meaningful tactical identity.
- Full-roster unit data exercises stack splitting, duplicate stacks, objective roles, counters, and 7-slot composition pressure.
- Six Champion/Operation abilities prove AP, morale, and Signal/Intel ability families through the shared ability schema.
- 8-10 statuses prove resolution order, stacking, counterplay, hidden information, objective interaction, and save/replay behavior.

## MVP Faction Pair Selection Criteria

This section defines what the first two MVP tactical factions should prove before exact faction names and rosters are locked. The goal is to choose a matchup that validates Neon Champions' tactical identity rather than merely testing generic damage exchange.

Approved direction:

1. The first two MVP factions should primarily test a **high-tech Signal/Intel faction versus a physical/industrial faction**.
2. The first matchup should use **strong asymmetry, while both factions still cover essential tactical roles**.
3. The faction pair should test **basic damage/range balance, objective play/stack splitting, and hidden information/Signal/counterplay**, with hidden information / Signal / counterplay weighted most heavily.
4. MVP factions should have **canonical faction identities and representative rosters**.
5. The second expansion faction should stress a **different major system not covered by the first pair**.

First-pair test contract:

- The high-tech Signal/Intel faction should stress:
  - scouting and information advantage;
  - hidden/revealed/decoded tactical state;
  - Jammed/Hacked/Sensor Lock interactions;
  - ability channels and counterplay hooks;
  - precision, tempo, or networked coordination.
- The physical/industrial faction should stress:
  - durable battlefield presence;
  - straightforward damage/range baselines;
  - control-zone and extraction/pickup pressure;
  - stack-splitting and 7-slot composition tradeoffs;
  - readable counters to Signal/Intel pressure through armor, logistics, discipline, mass, hardening, or industrial redundancy.

Asymmetry contract:

- The factions should not be palette swaps.
- Both factions still need enough baseline tools to play the MVP modes:
  - ranged pressure;
  - close/control presence;
  - objective interaction;
  - some answer to scouting/hidden info;
  - at least one meaningful Champion/Operation interaction.
- Asymmetry should be strong enough to expose system stress, but not so extreme that early balance cannot distinguish bad faction design from bad core rules.

Design-risk priority:

- The matchup must test all three risk categories:
  1. basic damage/range balance;
  2. objective play and stack splitting;
  3. hidden information / Signal / counterplay.
- Hidden information / Signal / counterplay is the highest priority because recent tactical contracts make information state, visibility, replay/debug, and status concealment core rather than optional polish.
- Basic damage/range and objective/stack-splitting still need explicit scenarios so the MVP does not overfit to Signal play while ignoring fundamentals.

Canonical identity contract:

- MVP factions should use canonical Neon Champions faction identities, not generic placeholder teams.
- Rosters may be representative rather than final-polished, but their unit roles should express real faction philosophy.
- The goal is to validate whether the tactical system carries the world's ideological/factional texture.
- Final names, art direction, VO, campaign integration, and full lore presentation can continue to mature after the tactical contract is proven.

Expansion-faction contract:

- The third faction should not merely counter one of the first two.
- It should stress a different major system not fully covered by Signal-vs-industrial play, such as:
  - morale/media/psychological warfare;
  - biotech/body-subscription pressure;
  - drone/swarm/network saturation;
  - Echo/continuity/death-state mechanics;
  - extreme mobility or logistics;
  - faction-specific objective manipulation.
- Selection should be based on system coverage and faction identity proof, not implementation convenience alone.

Implementation readiness gates:

- The first two factions can play field, control-zone, and extraction/pickup battles with strong but understandable asymmetry.
- The matchup includes explicit scenarios for damage/range balance, stack splitting/objective play, and hidden information/Signal/counterplay.
- Each faction has a representative roster expressing canonical identity.
- The third faction candidate is chosen by what untested major system it stresses.

## First MVP Faction Pair Candidates

This section selects the first actual MVP faction-pair archetype for representative tactical roster development. The purpose is to give the MVP combat slice a concrete matchup that tests Signal/Intel, hidden information, hardening, objectives, stack splitting, and physical board control while remaining readable.

Approved direction:

1. Signal/Intel-side faction archetype: **corporate surveillance/security network**.
2. Physical/industrial-side faction archetype: **heavy corporate extraction/logistics bloc**.
3. First matchup feel: **“Sensors vs steel”** — precision visibility and disruption against armor, redundancy, and mass.
4. Weirdness level: **grounded and readable**, with weirdness mostly expressed through abilities, statuses, hidden information, and faction-flavored tech.
5. Naming specificity: use **working canonical names**, with **provisional roster themes** sufficient for roster design.

Signal/Intel faction contract:

- Core fantasy: a corporate surveillance/security apparatus that turns information into battlefield tempo.
- Tactical identity:
  - sees more than the opponent;
  - marks, reveals, sensor-locks, jams, hacks, and coordinates precision action;
  - uses contracts, compliance logic, predictive security, and networked tactical teams;
  - wins by making the opponent’s position, intent, and vulnerabilities legible.
- MVP roles to cover:
  - sensor/scout unit;
  - precision ranged unit;
  - disruption/support unit;
  - light objective runner;
  - hardpoint or elite security unit;
  - at least one drone/relay/created-entity interaction if roster identity needs it.
- Weaknesses / counterplay:
  - less raw durability and mass than the industrial faction;
  - vulnerable to hardening, redundancy, line-of-sight denial, jamming/counterintel, and objective pressure that forces physical commitment;
  - should not win by invisible gotchas alone.

Physical/industrial faction contract:

- Core fantasy: a heavy extraction/logistics bloc that solves tactical problems through armor, tools, redundancy, mass, and resource control.
- Tactical identity:
  - holds ground and survives disruption;
  - uses armored crews, security contractors, industrial drones-as-tools, repair/logistics assets, heavy weapons, and hardened systems;
  - pressures objectives through physical presence and resilience;
  - turns extraction infrastructure into battlefield advantage.
- MVP roles to cover:
  - durable frontline/security crew;
  - heavy ranged or breaching unit;
  - logistics/repair/support unit;
  - objective carrier/hauler/extractor;
  - hardened anti-Signal/counter-disruption unit;
  - elite industrial platform or contractor force.
- Weaknesses / counterplay:
  - less precise information control;
  - slower or more telegraphed tempo;
  - vulnerable to being marked, isolated, misdirected, delayed, or forced to split heavy assets across objectives.

Matchup contract — “Sensors vs steel”:

- The Signal/Intel side should feel like it is shaping the fight through knowledge, target designation, disruption, and tempo.
- The industrial side should feel like it can endure, occupy, contest, repair, and force the Signal side to prove that information can beat mass.
- The matchup should explicitly test:
  - hidden/revealed/decoded information;
  - Marked/Sensor Lock, Jammed, Hacked, Suppressed, Routed, and objective-affecting statuses;
  - control-zone scoring;
  - extraction/pickup carrying;
  - stack splitting and duplicate stacks;
  - AP/tempo abilities versus armor/redundancy;
  - Signal counterplay and hardening.

Tone / weirdness contract:

- The first pair should be grounded enough to teach the combat system.
- Speculative weirdness should appear through tactical effects, not through maximum-concept faction premise.
- Acceptable early weirdness:
  - predictive surveillance;
  - compliance contracts as tactical authority;
  - automated sensor networks;
  - hacked logistics systems;
  - industrial body risk and hardened crews;
  - drones/relays/created entities;
  - partial hidden information and decoys.
- Defer maximum-weirdness faction identity such as Echo/continuity identity confusion or full body-horror biotech until later factions unless a specific unit/ability needs a small preview.

Naming / theme contract:

- Use working canonical names so documents and rosters can be specific.
- Names remain provisional until faction worldbuilding and roster design settle.
- Roster themes should be concrete enough to start unit-role packets, but not treated as final art/lore lock.
- The pair should read as two globally plausible corporate/industrial actors rather than local-only organizations.

Implementation readiness gates:

- Two working canonical faction names can be attached to this pair.
- Each faction has a provisional full-roster theme list ready for unit-role decomposition.
- The first three validation battles can be framed around “Sensors vs steel.”
- The pair can test Signal/Intel versus hardening/redundancy without relying on final campaign lore.

## Working Names for First MVP Faction Pair

This section selects working canonical names for the first MVP tactical faction pair. The names are lore-derived from existing Neon Champions worldbuilding rather than newly invented placeholders.

Approved direction:

1. Signal/Intel-side MVP faction: **Barents Research Group**.
2. Signal/Intel battlefield / roster-facing formation: **Polar Certification Combine**.
3. Physical/industrial-side MVP faction: **Janus-Kestrel Continuity Group**.
4. Physical/industrial battlefield / roster-facing formation: **Mining-Logistics Consortium**.
5. Name lock level: **working canonical names** with provisional roster themes. Names can still change after roster/worldbuilding review, but they are strong enough to anchor faction packets.

Faction-pair label:

```text
Barents Research Group / Polar Certification Combine
vs
Janus-Kestrel Continuity Group / Mining-Logistics Consortium
```

Barents fit:

- Barents is the stronger Signal/Intel MVP candidate because its existing lore already centers on polar data, route certification, sensor truth, risk scoring, and scientific neutrality as power.
- It should play as the faction that makes the battlefield legible: scouting, marking, revealing, route control, certification, exclusion zones, sensor drones, and debuffs through superior information.
- Its public face is research, rescue, route safety, and polar certification.
- Its darker face is that what Barents measures becomes claimable, insurable, legal, safe, unsafe, rescued, abandoned, or excluded.

Janus-Kestrel fit:

- Janus-Kestrel is the stronger industrial/logistics MVP candidate because its existing lore already centers on ports, customs, bonded corridors, cargo identity, cable landings, relay priority, drone corridors, extraction finance, and concession contracts.
- It should play as the faction that makes force and logistics physically arrive: armored crews, cargo swarms, concession guards, mining frames, customs enforcement, port drones, hardened routes, and objective pressure.
- Its public face is continuity, circulation, movement, clearance, and emergency logistics.
- Its darker face is that if Janus-Kestrel does not carry, clear, route, certify, or recognize something, it does not arrive.

Matchup meaning:

- The first MVP faction pair becomes **certification versus concession** as much as **sensors versus steel**.
- Barents asks: *what is safe, legal, visible, measurable, and certified?*
- Janus-Kestrel asks: *what is cleared, routed, extracted, delivered, bonded, and enforced?*
- This gives the MVP matchup a grounded corporate conflict over Arctic/Greenland logistics, extraction, data, route truth, and physical control.

Naming notes:

- Use **Barents Research Group** for the parent/global faction name.
- Use **Polar Certification Combine** when a more battlefield-facing or campaign-map formation label is useful.
- Use **Janus-Kestrel Continuity Group** for the parent/global faction name.
- Use **Mining-Logistics Consortium** when a more battlefield-facing or Greenland/extraction-specific formation label is useful.
- Avoid shortening Janus-Kestrel to only Janus or only Kestrel; the dual name preserves both threshold/legal control and fast relay/drone movement.

Implementation readiness gates:

- The next roster packet can derive Barents unit roles from certification, sensors, route truth, and polar exclusion.
- The next roster packet can derive Janus-Kestrel unit roles from concessions, cargo identity, extraction, bonded logistics, and hardened movement.
- The first three validation battles can frame their objectives around disputed route certification, server/sensor capture, concession-zone control, and extraction/pickup logistics.

## Barents Roster Role Skeleton

This section defines the Barents Research Group / Polar Certification Combine roster role skeleton before final unit names, stats, or ability values are locked. The goal is to keep Barents grounded in existing lore: polar data, route certification, sensor truth, risk scoring, scientific neutrality, and exclusion authority.

Approved direction:

1. Primary tactical identity: **hybrid sensor-control and certification-control faction**.
2. Durability profile: **low frontline durability, but strong defensive tools and exclusion zones**.
3. Roster shape: **mixed human specialist teams, drones, route-control tech, and one elite exclusion/security unit**.
4. Signature mechanic: **Certified Route + Risk Score, with Sensor Lock as common tactical status**.
5. Objective interaction: **can certify/decertify objective zones, altering scoring, eligibility, and progress**.

Tactical identity:

- Barents should not play as a generic scout faction.
- It wins by deciding what the battlefield means: what is visible, measurable, safe, unsafe, insured, excluded, claimable, or legally routable.
- Its information advantage should become movement pressure, objective leverage, debuffs, and selective firepower.
- Barents should feel calm, procedural, and data-backed even when acting coercively.

Durability profile:

- Barents should not out-brawl Janus-Kestrel in a direct steel-on-steel fight.
- Frontline bodies are relatively vulnerable compared to heavy industrial factions.
- Survivability comes from preparation: certified lanes, exclusion zones, sensor coverage, route denial, defensive drones, and positional debuffs.
- If Barents loses the information layer, it becomes materially exposed.

Roster-shape requirements:

The full MVP/vertical-slice roster should include roles resembling:

1. **Field survey / route team** — basic scout-support stack; identifies zones, hazards, and objective metadata.
2. **Sensor / radar operators** — reveal, mark, remove suspected/hidden state, apply Sensor Lock.
3. **Research drone swarm** — mobile recon/harass stack; extends sensor net and contests weak objectives.
4. **Rescue-security contractors** — midline human stack; credible combat presence without becoming heavy infantry.
5. **Cable / infrastructure specialists** — scenario and objective interaction; disable relays, restore routes, manipulate pickup/extraction systems.
6. **Risk / certification board unit** — command-support stack; applies Risk Score, certifies routes, decertifies enemy-controlled zones.
7. **Polar exclusion/security elite** — expensive control unit; area denial, anti-stealth, anti-drone, protects certified corridors.

Signature mechanic contract:

- **Certified Route** marks tiles/zones/objectives as certified, contested, decertified, or excluded.
- Certified ally zones may grant movement reliability, objective progress, accuracy, morale stability, or reduced hazard penalties.
- Decertified or excluded enemy zones may impose movement penalties, objective ineligibility, accuracy penalties, morale pressure, or increased Risk Score.
- **Risk Score** accumulates on enemy stacks, zones, or actions when they move through excluded routes, attack protected assets, ignore warnings, operate while Sensor Locked, or contest certified objectives.
- Risk Score should create predictable escalating consequences rather than random punishment.
- **Sensor Lock** remains the common tactical status: it makes targets easier to hit, reveal, track, debuff, or classify for later Barents effects.

Objective interaction:

- Barents can certify or decertify objective zones rather than simply occupying them.
- Certification can alter scoring speed, eligibility, visibility, extraction safety, pickup legality, or contesting rules.
- A Barents-controlled objective may become easier for Barents to score but more politically/legally costly for opponents to attack.
- Barents should reveal hidden objective rules better than most factions, but should not freely spoof objectives in MVP.
- Full false objective / spoofed progress play remains a later deception-system extension, not the baseline Barents MVP identity.

Counterplay expectations:

- Janus-Kestrel should be able to contest Barents through hard routing, redundant logistics, armored objective pressure, and contract enforcement.
- Signal/Intel counterplay should exist: jamming, destroying sensor assets, forcing line-of-sight breaks, corrupting route data, overloading Risk Score systems, or using decoy cargo/entities.
- Barents should be powerful when prepared but vulnerable when forced into chaotic close fights or when its sensor grid collapses.

Implementation readiness gates:

- The next packet can define concrete Barents unit lines and upgrade names from this skeleton.
- Ability design should prioritize Sensor Lock, Certified Route, Risk Score, reveal/mark, route denial, and objective certification.
- Validation battles should include at least one objective where Barents can certify a route or decertify a Janus-Kestrel concession zone.

## Barents Unit-Line Skeleton

This section turns the Barents Research Group / Polar Certification Combine role skeleton into seven provisional HoMM-style unit lines. These names are approved as **provisional**: strong enough for roster/ability packets, but not final lore or UI lock.

Approved provisional unit lines:

| Tier | Basic Unit | Upgraded Unit | Primary Role | Core Function |
|---:|---|---|---|---|
| 1 | Field Surveyors | Certified Route Team | Scout/support | Identify routes, hazards, and objective metadata. |
| 2 | Ice Radar Operators | Cryo-Mapping Cell | Reveal/mark | Reveal hidden/suspected targets, apply Sensor Lock, improve targeting. |
| 3 | Research Drones | Boreal Sensor Net | Drone recon/harass | Extend sensor coverage, contest weak objectives, enable marks. |
| 4 | Rescue Contractors | Denied-Zone Responders | Midline combat/security | Credible combat stack with rescue/security dual use. |
| 5 | Cable Divers | Under-Ice Saboteurs | Infrastructure/objective specialist | Disable or restore relays, cable nodes, pickup/extraction systems, and map infrastructure. |
| 6 | Risk Actuaries | Certification Board | Command/support | Apply Risk Score, certify/decertify routes and objectives, manipulate eligibility/progress. |
| 7 | Polar Exclusion Team | Black-Ice Wardens | Elite control | Area denial, anti-stealth, anti-drone, corridor protection, exclusion enforcement. |

Roster principles:

- The roster should feel like a research/certification corporation that has become a tactical authority, not like a conventional army.
- Each unit line should imply a source institution: survey offices, radar stations, drone networks, rescue contracts, cable infrastructure, risk boards, and exclusion teams.
- The heroic read is safety, rescue, navigation, and scientific competence.
- The horrific read is abandonment, exclusion, proprietary truth, legal violence, and data-backed dispossession.
- Unit upgrades should feel like stronger mandate, better equipment, cleaner legal authority, improved sensor integration, or more coercive certification power — not fantasy evolution.

Line notes:

1. **Field Surveyors → Certified Route Team**
   - Baseline utility stack.
   - Should interact with route/objective metadata early, making Barents readable from tier 1.
   - Likely abilities: Scout Route, Identify Hazard, Preliminary Certification.

2. **Ice Radar Operators → Cryo-Mapping Cell**
   - Primary reveal/mark line.
   - Should be one of the main ways Barents removes suspected/hidden state and applies Sensor Lock.
   - Likely abilities: Ice Radar Sweep, Sensor Lock, Map Drift.

3. **Research Drones → Boreal Sensor Net**
   - Mobile recon/harassment and sensor-extension line.
   - Should be useful without high damage; their value is coverage, tagging, and objective nuisance.
   - Likely abilities: Extend Sensor Net, Drone Harass, Relay Mark.

4. **Rescue Contractors → Denied-Zone Responders**
   - Combat-capable human stack with a plausible public-good mask.
   - Should bridge rescue, private security, and emergency route enforcement.
   - Likely abilities: Extract Casualties, Secure Zone, Emergency Response.

5. **Cable Divers → Under-Ice Saboteurs**
   - Distinctive infrastructure and scenario-objective line.
   - Strongest on maps with cables, relays, ports, ice-water edges, server bunkers, or extraction infrastructure.
   - Likely abilities: Cut Relay, Restore Cable, Flooded Approach, Under-Ice Breach.

6. **Risk Actuaries → Certification Board**
   - The most Neon Champions support line: institutional modeling as tactical pressure.
   - Should apply predictable escalating penalties rather than random punishment.
   - Likely abilities: Assign Risk Score, Certify Route, Decertify Objective, Liability Finding.

7. **Polar Exclusion Team → Black-Ice Wardens**
   - Elite control stack and hard expression of Barents authority.
   - “Black-Ice” should read as both Arctic hazard and cyberpunk ICE.
   - Likely abilities: Exclusion Zone, Anti-Stealth Sweep, Drone Denial, Corridor Lockdown.

Implementation readiness gates:

- Next Barents packet should define unit stat profiles and combat roles: melee/ranged/support/control, speed, durability, damage posture, AP costs, and objective utility.
- Ability packets should avoid overloading every unit with all Barents mechanics; distribute Sensor Lock, Certified Route, and Risk Score cleanly across the roster.
- Names remain provisional until roster feel, faction fantasy, and opponent matchup are tested against Janus-Kestrel.

## Barents Unit Stat-Role Profiles

This section defines provisional tactical stat-role profiles for each Barents Research Group / Polar Certification Combine unit line before detailed values, final abilities, or balance numbers are locked. These are **provisional role contracts**: enough to guide ability design and matchup testing, not final tuning.

Approved provisional profiles:

| Tier | Unit Line | Profile | Tactical Contract |
|---:|---|---|---|
| 1 | Field Surveyors → Certified Route Team | Weak combat, strong certification/objective interaction | Teaches route/objective certification from tier 1. |
| 2 | Ice Radar Operators → Cryo-Mapping Cell | Ranged support with reveal/mark and light damage | Useful in normal fights while carrying reveal/Sensor Lock duties. |
| 3 | Research Drones → Boreal Sensor Net | Fast fragile ranged harass + sensor extender | Extends Barents sensor coverage and creates low-damage pressure. |
| 4 | Rescue Contractors → Denied-Zone Responders | Medium infantry with sustain/extraction utility | Gives Barents a credible midline without becoming heavy industrial infantry. |
| 5 | Cable Divers → Under-Ice Saboteurs | Mobile sabotage/objective unit with modest combat | Infrastructure flavor remains central, but the line is broadly playable. |
| 6 | Risk Actuaries → Certification Board | Fragile backline command unit with strong Risk/Certification effects | Powerful battlefield bureaucracy that opponents can punish if exposed. |
| 7 | Polar Exclusion Team → Black-Ice Wardens | Elite area-denial bruiser with control tools | Closes Barents' durability gap while remaining control-first, not a plain tank. |

Profile principles:

- Barents should be strongest when it prepares, measures, marks, certifies, and controls routes before direct engagement.
- Barents should be weakest when forced into chaotic close fights without sensor coverage or certified zones.
- Damage should generally be secondary to information advantage, route control, objective leverage, and escalating Risk Score.
- The roster needs enough ordinary combat presence to function in frequent HoMM-like battles, but should not out-muscle Janus-Kestrel.

Line-by-line role contracts:

1. **Field Surveyors → Certified Route Team**
   - Combat: low damage, low-to-medium durability.
   - Mobility: decent; should reach objectives and route nodes early.
   - Utility: high; interacts with objective metadata, hazards, routes, and preliminary certification.
   - Design risk: if too weak, tier 1 feels like dead weight; if too strong, Barents gets too much early board control.

2. **Ice Radar Operators → Cryo-Mapping Cell**
   - Combat: light ranged damage.
   - Durability: fragile-to-medium; should need protection.
   - Utility: reveal, mark, remove suspected state, apply Sensor Lock.
   - Design risk: reveal tools must be valuable even when the opponent has little hidden information.

3. **Research Drones → Boreal Sensor Net**
   - Combat: light ranged harassment.
   - Durability: fragile; vulnerable to anti-drone, jamming, and focused fire.
   - Mobility: high; likely flying or terrain-agnostic depending on map rules.
   - Utility: extend sensor net, tag targets, contest weak objectives, enable line-of-sight/range setups.
   - Design risk: avoid making cheap drones the best objective blockers or stack-splitting exploit units.

4. **Rescue Contractors → Denied-Zone Responders**
   - Combat: medium infantry baseline.
   - Durability: medium; the roster's first reliable contact unit.
   - Utility: sustain, extraction, zone securing, emergency response.
   - Design risk: should not become generic rifle infantry; rescue/security dual-use must remain visible.

5. **Cable Divers → Under-Ice Saboteurs**
   - Combat: modest; enough to survive specialist plays.
   - Mobility: medium-to-high on infrastructure/coastal/ice-water maps; normal elsewhere.
   - Utility: sabotage and repair of relays, cables, server nodes, extraction systems, pickups, and objective infrastructure.
   - Design risk: scenario specialization must not make them useless on ordinary field/control-zone battles.

6. **Risk Actuaries → Certification Board**
   - Combat: very low direct damage.
   - Durability: fragile; should be protected by positioning and certified zones.
   - Utility: high-impact Risk Score and certification commands.
   - Role: caster/commander-equivalent, but expressed through institutional authority rather than magic.
   - Design risk: effects must be deterministic, readable, and counterplayable; avoid opaque punishment.

7. **Polar Exclusion Team → Black-Ice Wardens**
   - Combat: strong but control-weighted.
   - Durability: high for Barents, but not the game's heaviest tank baseline.
   - Utility: area denial, anti-stealth, anti-drone, corridor lockdown, protects certified routes.
   - Role: elite bruiser-control stack; the hard edge of Barents authority.
   - Design risk: should feel like enforcement of exclusion/certification, not generic elite soldiers.

Implementation readiness gates:

- Next Barents packet should define per-line ability slots: passive, active, upgrade delta, and signature interaction.
- Unit stat tuning should keep Barents' average durability below Janus-Kestrel while giving Barents superior information and route leverage.
- Objective validation should include at least one battle where Field Surveyors, Cable Divers, and Risk Actuaries each matter in different ways.

## Barents Unit Ability-Slot Contracts

This section defines provisional ability-slot contracts for each Barents Research Group / Polar Certification Combine unit line. The goal is to preserve strong faction identity without turning every unit into a spellcaster or making every Barents stack carry every faction mechanic.

Approved provisional contracts:

1. Baseline ability complexity: **1 passive + 1 active for most lines; upgraded form improves or adds one interaction**.
2. Certified Route access: **Field Surveyors get basic certification; Risk Actuaries get strong certification**.
3. Sensor Lock access: **Ice Radar is primary; Research Drones are secondary**.
4. Risk Score access: **Risk Actuaries apply it; multiple units may exploit it carefully**.
5. Objective manipulation: **Field Surveyors + Cable Divers + Risk Actuaries** are the main objective-interaction units.

Complexity rule:

- Most Barents unit lines should have one passive identity hook and one active tactical button.
- Upgrades should either strengthen an existing interaction, add a conditional rider, or improve the interaction with Certified Route / Sensor Lock / Risk Score.
- Avoid giving every unit a reveal, a mark, a certification tool, and a Risk Score interaction. The roster should have distributed jobs.
- Elite or support lines may be more complex, but only if their tactical role requires it.

Mechanic ownership:

| Mechanic | Primary Owner | Secondary / Exploiters | Notes |
|---|---|---|---|
| Certified Route | Field Surveyors, Risk Actuaries | Black-Ice Wardens as zone protectors | Field Surveyors teach the mechanic; Risk Actuaries make it powerful. |
| Sensor Lock | Ice Radar Operators | Research Drones | Keep access common enough for play, but not universal. |
| Risk Score | Risk Actuaries | Ice Radar, Research Drones, Black-Ice Wardens, possibly Cable Divers as exploiters | Application should be controlled; exploitation can feel faction-wide. |
| Objective manipulation | Field Surveyors, Cable Divers, Risk Actuaries | Rescue Contractors for extraction/sustain support | Three specialist lines give depth without making all units scenario tools. |

Provisional per-line ability structure:

1. **Field Surveyors → Certified Route Team**
   - Passive: better objective/hazard metadata visibility or safer movement through certified routes.
   - Active: basic route/objective certification.
   - Upgrade delta: certification affects objective progress or eligibility more strongly.
   - Signature interaction: early access to Certified Route.

2. **Ice Radar Operators → Cryo-Mapping Cell**
   - Passive: bonus accuracy/reveal reliability against suspected, hidden, or Sensor Locked targets.
   - Active: scan/reveal and apply Sensor Lock.
   - Upgrade delta: broader scan, stronger mark, or removes more hidden-state metadata.
   - Signature interaction: primary Sensor Lock applier.

3. **Research Drones → Boreal Sensor Net**
   - Passive: extends local sensor coverage or improves Barents targeting in nearby tiles/zones.
   - Active: mobile mark/harass that can apply or refresh Sensor Lock under constraints.
   - Upgrade delta: stronger relay coverage, safer disengage, or better objective contest rules.
   - Signature interaction: secondary Sensor Lock and sensor-net extension.

4. **Rescue Contractors → Denied-Zone Responders**
   - Passive: improved survival/extraction behavior near certified or contested zones.
   - Active: stabilize, extract, or secure a zone/stack.
   - Upgrade delta: stronger denied-zone response, sustain, or emergency movement.
   - Signature interaction: keeps Barents from collapsing in contact while preserving public-good mask.

5. **Cable Divers → Under-Ice Saboteurs**
   - Passive: bonuses near infrastructure, relays, cables, ports, ice-water edges, or server objectives.
   - Active: sabotage/restore infrastructure or manipulate pickup/extraction systems.
   - Upgrade delta: adds stealthier approach, stronger disable, or Risk Score exploitation against exposed infrastructure.
   - Signature interaction: objective/infrastructure specialist.

6. **Risk Actuaries → Certification Board**
   - Passive: improves or discounts Risk/Certification effects in certified zones.
   - Active: apply Risk Score, certify/decertify route/objective, or issue liability finding.
   - Upgrade delta: stronger area effect, additional Risk Score threshold, or objective-eligibility manipulation.
   - Signature interaction: primary Risk Score and strong Certified Route owner.

7. **Polar Exclusion Team → Black-Ice Wardens**
   - Passive: stronger while defending certified/excluded zones or attacking high-Risk targets.
   - Active: create exclusion zone, lock corridor, deny drones/stealth, or punish Risk Score threshold.
   - Upgrade delta: better area denial, anti-stealth/anti-drone, or stronger high-Risk exploitation.
   - Signature interaction: hard enforcement of Barents' certification authority.

Design constraints:

- Certified Route should be readable as map/objective control, not a hidden math buff.
- Sensor Lock should be useful even when the enemy is not using stealth, by improving targeting or enabling follow-up effects.
- Risk Score should be deterministic, escalating, and clearly telegraphed.
- Objective manipulation should be explicit in UI: players must know why a zone scores, stalls, becomes ineligible, or becomes dangerous.
- Upgrade deltas should be tactical and thematic, not just flat stat increases.

Implementation readiness gates:

- Next packet can define the actual first-pass ability names/effects per Barents unit line.
- Ability implementation should map each active/passive to the generic ability/effect schema already defined in the tactical implementation contracts.
- Validation scenarios should test whether Barents has enough combat presence when objective/information tools are less relevant.

## Barents First-Pass Unit Abilities

This section defines preliminary first-pass ability names and effects for Barents Research Group / Polar Certification Combine unit lines. These are **preliminary/provisional**: they should be used to test faction feel and implementation shape, not treated as final balance or final UI copy.

Approved preliminary ability sets:

| Tier | Unit Line | Passive | Active | Core Effect |
|---:|---|---|---|---|
| 1 | Field Surveyors → Certified Route Team | Route Literacy | Preliminary Certification | Basic route/objective certification and safer movement/metadata use. |
| 2 | Ice Radar Operators → Cryo-Mapping Cell | Cold Read | Ice Radar Sweep | Reveal/clarify hidden or suspected targets; apply Sensor Lock rider. |
| 3 | Research Drones → Boreal Sensor Net | Relay Coverage | Tagging Pass | Extend sensor coverage and apply/refresh constrained Sensor Lock. |
| 4 | Rescue Contractors → Denied-Zone Responders | Rescue Mandate | Emergency Extraction | Stabilize or reposition endangered stacks/objective carriers. |
| 5 | Cable Divers → Under-Ice Saboteurs | Wetline Specialist | Restore/Cut Cable | Restore or sabotage relays, cable nodes, extraction systems, and objective infrastructure. |
| 6 | Risk Actuaries → Certification Board | Risk Ledger | Certify/Decertify | Manipulate Certified Route state and Risk Score / objective eligibility. |
| 7 | Polar Exclusion Team → Black-Ice Wardens | Wardens' Mandate | Exclusion Zone | Create/control exclusion space; upgrade riders can add anti-stealth/anti-drone. |

Line details:

1. **Field Surveyors → Certified Route Team**
   - Passive: **Route Literacy**.
   - Effect: better use of route/objective metadata; reduced penalties or improved reliability on certified routes.
   - Active: **Preliminary Certification**.
   - Effect: mark a small route, tile group, or objective zone as preliminarily certified for limited ally movement/objective benefit.
   - Upgrade direction: Certified Route Team improves the certification's objective-progress, eligibility, or hazard-mitigation effect.

2. **Ice Radar Operators → Cryo-Mapping Cell**
   - Passive: **Cold Read**.
   - Effect: improved accuracy/reveal reliability against suspected, hidden, obscured, or Sensor Locked targets.
   - Active: **Ice Radar Sweep**.
   - Effect: scan an area, clarify suspected/hidden state, reveal decoys or anomalies where applicable, and apply Sensor Lock to valid targets.
   - Upgrade direction: Cryo-Mapping Cell increases scan area, reveal strength, or the quality/duration of Sensor Lock.

3. **Research Drones → Boreal Sensor Net**
   - Passive: **Relay Coverage**.
   - Effect: extends local Barents sensor coverage and may improve targeting/reveal reliability in nearby zones.
   - Active: **Tagging Pass**.
   - Effect: mobile low-damage harassment that tags a target, applies or refreshes constrained Sensor Lock, and helps maintain line-of-sight logic.
   - Upgrade direction: Boreal Sensor Net improves relay radius, safer disengage, or objective-contest support.

4. **Rescue Contractors → Denied-Zone Responders**
   - Passive: **Rescue Mandate**.
   - Effect: improved sustain, extraction, or morale stability near certified/contested zones or endangered allied stacks.
   - Active: **Emergency Extraction**.
   - Effect: stabilize, pull, reposition, or protect an endangered allied stack/objective carrier under defined range and AP limits.
   - Upgrade direction: Denied-Zone Responders improve extraction safety, add zone-securing effect, or gain a defensive rider after extraction.

5. **Cable Divers → Under-Ice Saboteurs**
   - Passive: **Wetline Specialist**.
   - Effect: bonuses near infrastructure, relays, cable nodes, ports, ice-water edges, server rooms, or extraction/pickup systems.
   - Active: **Restore/Cut Cable**.
   - Effect: choose restoration or sabotage mode on eligible infrastructure: restore allied relay/objective function, or disable enemy route/sensor/objective infrastructure.
   - Upgrade direction: Under-Ice Saboteurs gain stronger disable, stealthier approach, or Risk Score exploitation against exposed infrastructure.

6. **Risk Actuaries → Certification Board**
   - Passive: **Risk Ledger**.
   - Effect: tracks or improves Risk Score / certification effects; may reduce cost or improve effect in certified zones.
   - Active: **Certify/Decertify**.
   - Effect: change a route/objective zone's certification state, apply or escalate Risk Score under clear conditions, and manipulate objective eligibility/progress where allowed.
   - Upgrade direction: Certification Board increases area, adds threshold effects, or gains stronger objective-state manipulation.

7. **Polar Exclusion Team → Black-Ice Wardens**
   - Passive: **Wardens' Mandate**.
   - Effect: stronger while defending certified/excluded zones or engaging high-Risk / Sensor Locked targets.
   - Active: **Exclusion Zone**.
   - Effect: create or enforce an exclusion area that restricts movement, punishes entry, blocks stealth/drone intrusion with upgrade riders, or protects a certified corridor.
   - Upgrade direction: Black-Ice Wardens improve area denial, anti-stealth/anti-drone control, or high-Risk target punishment.

Design constraints:

- These abilities should map cleanly to the reusable ability/effect schema: statuses, reveal/mark, movement modification, objective interaction, resource/cost, and zone-state changes.
- Sensor Lock should be a rider on Ice Radar Sweep and Tagging Pass, not a universal Barents button.
- Certified Route should remain readable on the board and in objective UI.
- Risk Ledger and Certify/Decertify must be deterministic and explainable; no hidden random punishment.
- Emergency Extraction must have tight limits to avoid trivializing positioning, rout, or objective carrier risk.
- Restore/Cut Cable should degrade gracefully on maps without literal cable infrastructure by targeting relays, extraction machinery, server nodes, or other scenario infrastructure.

Implementation readiness gates:

- Next Barents packet should define ability costs/cooldowns/AP use and MVP effect primitives per ability.
- Validation should include at least one map with infrastructure targets so Cable Divers can prove their identity.
- Barents must be tested in at least one low-infrastructure field battle to verify the roster still functions outside ideal maps.

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
