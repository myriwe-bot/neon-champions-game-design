---
title: Tactical Combat — Morale, Rout, and Cohesion
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

# Tactical Combat — Morale, Rout, and Cohesion

> This article preserves and reorganizes design-session content from [[design/research/tactical-combat-deep-reference]]. It is part of the tactical combat GDD split for readability. Do not treat missing context as permission to invent rules; check the active overview at [[design/gdd/tactical-combat]].

## Article Contents

- Retreat, Surrender, and Tactical Loss Boundary
- Morale, Routing, and Stack Collapse
- Global Morale Model
- Morale Scale, Thresholds, and Rout Checks
- Morale Recovery and Rally Actions
- Morale Event Sources and Strategic Links
- Morale UI, Prediction, and Player Readability
- Morale Complexity Boundary and MVP Cut
- End of Morale Block — Integration Check
- Morale / Cohesion

---

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
