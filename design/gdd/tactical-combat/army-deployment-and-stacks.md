---
title: Tactical Combat — Army, Deployment, and Stacks
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-05-30
source_lore: []
related: [design/gdd/tactical-combat, design/research/tactical-combat-deep-reference]
approval: pending
---

# Tactical Combat — Army, Deployment, and Stacks

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Army Composition and Battle Participation

---

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
