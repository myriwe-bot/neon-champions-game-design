---
title: Tactical Combat — MVP Content and Faction Rosters
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

# Tactical Combat — MVP Content and Faction Rosters

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Tactical MVP Content Matrix
- MVP Faction Pair Selection Criteria
- First MVP Faction Pair Candidates
- Working Names for First MVP Faction Pair
- Barents Roster Role Skeleton
- Barents Unit-Line Skeleton
- Barents Unit Stat-Role Profiles
- Barents Unit Ability-Slot Contracts
- Barents First-Pass Unit Abilities

---

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
- Barents asks: _what is safe, legal, visible, measurable, and certified?_
- Janus-Kestrel asks: _what is cleared, routed, extracted, delivered, bonded, and enforced?_
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

| Tier | Basic Unit           | Upgraded Unit          | Primary Role                        | Core Function                                                                               |
| ---: | -------------------- | ---------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------- |
|    1 | Field Surveyors      | Certified Route Team   | Scout/support                       | Identify routes, hazards, and objective metadata.                                           |
|    2 | Ice Radar Operators  | Cryo-Mapping Cell      | Reveal/mark                         | Reveal hidden/suspected targets, apply Sensor Lock, improve targeting.                      |
|    3 | Research Drones      | Boreal Sensor Net      | Drone recon/harass                  | Extend sensor coverage, contest weak objectives, enable marks.                              |
|    4 | Rescue Contractors   | Denied-Zone Responders | Midline combat/security             | Credible combat stack with rescue/security dual use.                                        |
|    5 | Cable Divers         | Under-Ice Saboteurs    | Infrastructure/objective specialist | Disable or restore relays, cable nodes, pickup/extraction systems, and map infrastructure.  |
|    6 | Risk Actuaries       | Certification Board    | Command/support                     | Apply Risk Score, certify/decertify routes and objectives, manipulate eligibility/progress. |
|    7 | Polar Exclusion Team | Black-Ice Wardens      | Elite control                       | Area denial, anti-stealth, anti-drone, corridor protection, exclusion enforcement.          |

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

| Tier | Unit Line                                   | Profile                                                              | Tactical Contract                                                               |
| ---: | ------------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
|    1 | Field Surveyors → Certified Route Team      | Weak combat, strong certification/objective interaction              | Teaches route/objective certification from tier 1.                              |
|    2 | Ice Radar Operators → Cryo-Mapping Cell     | Ranged support with reveal/mark and light damage                     | Useful in normal fights while carrying reveal/Sensor Lock duties.               |
|    3 | Research Drones → Boreal Sensor Net         | Fast fragile ranged harass + sensor extender                         | Extends Barents sensor coverage and creates low-damage pressure.                |
|    4 | Rescue Contractors → Denied-Zone Responders | Medium infantry with sustain/extraction utility                      | Gives Barents a credible midline without becoming heavy industrial infantry.    |
|    5 | Cable Divers → Under-Ice Saboteurs          | Mobile sabotage/objective unit with modest combat                    | Infrastructure flavor remains central, but the line is broadly playable.        |
|    6 | Risk Actuaries → Certification Board        | Fragile backline command unit with strong Risk/Certification effects | Powerful battlefield bureaucracy that opponents can punish if exposed.          |
|    7 | Polar Exclusion Team → Black-Ice Wardens    | Elite area-denial bruiser with control tools                         | Closes Barents' durability gap while remaining control-first, not a plain tank. |

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

| Mechanic               | Primary Owner                                 | Secondary / Exploiters                                                             | Notes                                                                      |
| ---------------------- | --------------------------------------------- | ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Certified Route        | Field Surveyors, Risk Actuaries               | Black-Ice Wardens as zone protectors                                               | Field Surveyors teach the mechanic; Risk Actuaries make it powerful.       |
| Sensor Lock            | Ice Radar Operators                           | Research Drones                                                                    | Keep access common enough for play, but not universal.                     |
| Risk Score             | Risk Actuaries                                | Ice Radar, Research Drones, Black-Ice Wardens, possibly Cable Divers as exploiters | Application should be controlled; exploitation can feel faction-wide.      |
| Objective manipulation | Field Surveyors, Cable Divers, Risk Actuaries | Rescue Contractors for extraction/sustain support                                  | Three specialist lines give depth without making all units scenario tools. |

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

| Tier | Unit Line                                   | Passive            | Active                    | Core Effect                                                                                |
| ---: | ------------------------------------------- | ------------------ | ------------------------- | ------------------------------------------------------------------------------------------ |
|    1 | Field Surveyors → Certified Route Team      | Route Literacy     | Preliminary Certification | Basic route/objective certification and safer movement/metadata use.                       |
|    2 | Ice Radar Operators → Cryo-Mapping Cell     | Cold Read          | Ice Radar Sweep           | Reveal/clarify hidden or suspected targets; apply Sensor Lock rider.                       |
|    3 | Research Drones → Boreal Sensor Net         | Relay Coverage     | Tagging Pass              | Extend sensor coverage and apply/refresh constrained Sensor Lock.                          |
|    4 | Rescue Contractors → Denied-Zone Responders | Rescue Mandate     | Emergency Extraction      | Stabilize or reposition endangered stacks/objective carriers.                              |
|    5 | Cable Divers → Under-Ice Saboteurs          | Wetline Specialist | Restore/Cut Cable         | Restore or sabotage relays, cable nodes, extraction systems, and objective infrastructure. |
|    6 | Risk Actuaries → Certification Board        | Risk Ledger        | Certify/Decertify         | Manipulate Certified Route state and Risk Score / objective eligibility.                   |
|    7 | Polar Exclusion Team → Black-Ice Wardens    | Wardens' Mandate   | Exclusion Zone            | Create/control exclusion space; upgrade riders can add anti-stealth/anti-drone.            |

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
