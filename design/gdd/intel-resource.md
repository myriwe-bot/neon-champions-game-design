---
title: Intel Resource System
type: system-gdd
status: draft
phase: systems-design
owner: shared
created: 2026-05-22
updated: 2026-07-25
source_lore: [digital-net, greenland, blue-monday, blue-week]
related:
  [design/gdd/game-concept, design/gdd/game-pillars, design/gdd/systems-index]
approval: core-role-approved
---

# Intel Resource System

> Status: Draft. Direction based on _Heroes of Might and Magic: Olden Era_ Alchemical Dust, but translated diegetically into Neon Champions.

## Summary

Intel is Neon Champions' scarce apex-progression resource. Like Olden Era's Alchemical Dust, it converts rare map rewards and obsolete Assets into upgrades for artifact-equivalent Champion Assets and access to highest-tier units or the buildings that produce them. It is not a generic information-action, proof, scouting, hacking, or ability currency.

> Quick reference — Layer: Core · Priority: MVP/Vertical Slice · Key deps: Strategic Map, Resources, Champions, Assets, Hubs, Recruitment

## Design Reference: Alchemical Dust

Olden Era's Alchemical Dust is acquired by:

- trading rare resources in Alchemical Labs;
- disenchanting items in hero inventory;
- finding it in the wild;
- unlocking certain subskills;
- likely weekly map objects and guarded reward sites, based on community reports.

It is spent on:

- upgrading town dwellings;
- leveling up spells;
- empowering artifacts.

Neon Champions translation:

- Alchemical Labs -> Intel Exchanges / Analysis Cells.
- Disenchanting items -> debriefing, reverse-engineering, burning, or leaking assets.
- Wild pickups -> data caches / field dossiers / dead drops.
- Subskills -> Analyst / Fixer / Signals / HUMINT specializations.
- Dwelling upgrades -> recruitment-site / unit-line upgrades.
- Spell upgrades are not mapped to Intel by default; Operations use their own progression contracts.
- Artifact empowerment -> asset upgrades.

## Player Fantasy

Intel should feel like turning secrets into operational superiority.

The player should think:

- “I stole their research, so my gear improves.”
- “I burned an asset for what it taught me.”
- “I know how this site works now, so my units can be upgraded.”
- “I cannot fund every apex Asset and unit line, so this recovery determines my build.”

## Core Rules

1. Intel is a strategic resource stored globally by faction for the prototype.
2. Intel is rarer than Credits/Energy and should not be required for every basic action.
3. Intel has two approved sink families:
   - upgrading artifact-equivalent Champion Assets;
   - unlocking highest-tier units or the buildings that produce them.
4. Intel has four main source types:
   - map discovery and guarded data sites;
   - conversion of other rare resources through analysis structures;
   - dismantling / reverse-engineering assets;
   - Champion/faction skills or site control producing recurring Intel.
5. Intel sources must be visible enough that scarcity feels strategic, not arbitrary.
6. Intel spending should create opportunity cost between stronger Champion Assets and access to apex troops.
7. Intel should never be named or presented as magic energy. It is always captured research, technical models, schematics, credentials, reverse-engineered process knowledge, or comparable apex-development material.
8. Evidence/Proof is separate state used to investigate claims and establish public accounts. Intel does not pay for routine investigation, proof, scouting, Signal actions, or legitimacy.

## Acquisition Modes

| Mode                | Olden Era Analogue      | Neon Champions Implementation                           | Renewable?                 |
| ------------------- | ----------------------- | ------------------------------------------------------- | -------------------------- |
| Data cache          | wild dust pile          | map pickup, dead drop, black box, leaked archive        | No                         |
| Guarded data site   | guarded reward object   | server bunker, wrecked convoy, archive, dark-net mirror | Usually no                 |
| Intel Exchange      | Alchemical Lab          | trade Compute/Proof/Credits/rare resources for Intel    | Yes if inputs renewable    |
| Analysis Cell       | Alchemical Dust Storage | weekly Intel from controlled analysis site              | Yes, weekly                |
| Reverse-engineering | disenchant artifact     | dismantle asset, burn contact, debrief captured gear    | No, converts item to Intel |
| Specialist skill    | subskill generation     | Analyst/Fixer/Signals Champion produces Intel/day       | Yes                        |
| Tactical outcome    | battle reward           | capture VIP, hack tactical objective, recover prototype | Event-based                |
| Research exposure   | unique cyberpunk source | recover apex schematics or authorization from an exposed program | Event-based |

## Spending Modes

| Sink                     | Olden Era Analogue     | Neon Champions Translation                                                      | Notes                      |
| ------------------------ | ---------------------- | ------------------------------------------------------------------------------- | -------------------------- |
| Asset empowerment        | artifact empowerment   | upgrade Champion gear/assets                                                    | Core MVP use               |
| Apex production unlock   | town dwelling upgrade  | unlock or construct a highest-tier unit facility                                | Core second proof sink     |
| Highest-tier unit unlock | dwelling/unit upgrade  | authorize the apex unit line when no separate facility is used                  | Scenario/faction alternative |

## Prototype Values

Use placeholder values until playtested:

- Small cache: 5 Intel.
- Standard guarded cache: 10 Intel.
- Major data vault: 25 Intel.
- Dismantle common asset: 5 Intel.
- Dismantle rare asset: 10 Intel.
- Dismantle elite asset: 20 Intel.
- Basic asset upgrade: 10 Intel.
- Major asset upgrade: 25 Intel.
- Apex production unlock: 25 Intel.
- Highest-tier unit authorization: 25 Intel.

These are intentionally lower-granularity than Olden Era until the resource economy is proven.

## Tactical Combat Integration

Full tactical battles are in scope.

Intel can enter tactical battles through optional objectives:

- capture a server rack before destroying defenders;
- prevent enemy data wipe for +Intel;
- extract a VIP alive;
- scan prototype units during combat;
- hack a tactical node instead of using an attack action;
- win without using destructive weapons to preserve evidence.

This makes Intel more interesting than post-battle loot and reinforces the cyberpunk theme.

## Edge Cases

| Scenario                           | Expected Behavior                                                      | Rationale                               |
| ---------------------------------- | ---------------------------------------------------------------------- | --------------------------------------- |
| Player spends all Intel early      | Core map remains playable; high-end upgrades slow down                 | Avoid hard fail through experimentation |
| Player hoards Intel                | Unspent Intel has no passive value by default                          | Encourage use                           |
| Map lacks recurring Intel          | Scenario UI should show it is a scarcity map                           | Avoid hidden frustration                |
| Asset is dismantled                | Asset is permanently destroyed unless scenario marks it as recoverable | Preserve opportunity cost               |
| Captured Intel exceeds storage cap | No cap in MVP                                                          | Avoid bookkeeping until needed          |
| Intel from local community         | Should require consent/trust, not extraction-only framing              | Avoid colonial resource logic           |

## Tuning Knobs

| Parameter                    | Current Value | Safe Range | Effect of Increase      | Effect of Decrease         |
| ---------------------------- | ------------: | ---------: | ----------------------- | -------------------------- |
| Basic asset upgrade cost     |            10 |       5-20 | Slower Champion growth  | Faster experimentation     |
| Major asset upgrade cost     |            25 |      15-50 | More specialization     | More frequent power spikes |
| Analysis Cell weekly yield   |            10 |       5-25 | More renewable Intel    | More map scarcity          |
| Specialist daily yield       |             1 |        0-3 | Stronger economy builds | Less snowball              |
| Dismantle common asset yield |             5 |       0-10 | More salvage economy    | More attachment to assets  |

## Acceptance Criteria

- [ ] Intel has at least one rare map/guarded source and one Asset-dismantling source in the vertical slice.
- [ ] Intel can upgrade at least one Champion asset in the MVP.
- [ ] Intel can unlock one highest-tier unit or its production building in the vertical slice.
- [ ] Intel costs and rewards are data-driven.
- [ ] Full tactical battles can award Intel through at least one optional objective.
- [ ] UI labels Intel sources as research, schematics, credentials, or reverse-engineered process knowledge rather than abstract dust or public Proof.
- [ ] Investigation, Evidence/Proof, Signal actions, and ordinary abilities do not deduct Intel.
- [ ] A player can recover from an early bad Intel spend without campaign failure.

## Open Questions

| Question                                                       | Owner        | Deadline                       | Resolution                                                             |
| -------------------------------------------------------------- | ------------ | ------------------------------ | ---------------------------------------------------------------------- |
| Should Intel be stored globally, Champion-local, or hybrid?    | Human/shared | Before resource implementation | Resolved 2026-07-25: global faction resource for the prototype.          |
| Should Intel have subtypes, e.g. HUMINT/SIGINT/Research/Proof? | Human/shared | After MVP                      | Recommended: no for MVP.                                               |
| Can Intel be traded on markets?                                | Human/shared | Before economy GDD             | Recommended: only through controlled Intel Exchanges, not open market. |
