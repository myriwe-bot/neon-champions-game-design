---
title: Game Concept
type: concept
status: draft
phase: concept
owner: shared
created: 2026-05-22
updated: 2026-07-25
source_lore:
  [greenland, blue-monday, blue-week, digital-net, white-sky, champions]
related:
  [
    design/gdd/game-pillars,
    design/gdd/core-fun-prototype,
    design/gdd/systems-index,
    design/world/approved-world-slice,
  ]
approval: pending
---

# Game Concept: Neon Champions

## Creative Brief

Neon Champions is a single-player-first turn-based strategy/RPG inspired by Heroes of Might and Magic III and Olden Era, translated into a no-magic cyberpunk world where Champions lead factions through infrastructure wars, polluted information, body technology, and public legitimacy struggles.

The first campaign takes place in an as-yet-unnamed fictional Arctic region during Blue Monday, later remembered as the start of Blue Week: a sparse strategic theater of outposts, mines, fishery hubs, sensor stations, White Sky infrastructure, Treaty Net nodes, and corporate development spectacle. Internally, geography and material conditions are grounded in research on Greenland after major ice-shelf retreat, but the player-facing location is not explicitly Greenland and no final replacement name or polity is approved. The player should feel like they are commanding a mythic public operator in a world where every road, feed, body, mine, and sky system is owned, contested, or failing.

## Elevator Pitch

Lead Champions through an Arctic Blue Monday crisis: investigate contested infrastructure, read rival intent, commit scarce movement and forces, fight for control, establish a credible public account, and turn recovered Intel into apex Assets and units under the White Sky.

## Core Fantasy

You are not a wizard-king. You are the visible face and strategic hand of a faction fighting over survival infrastructure, secrets, bodies, networks, and public truth.

Your Champion turns local alliances, cybernetic Assets, squads, captured infrastructure, and credible evidence into power while the world watches through polluted feeds. Intel is a separate scarce progression resource used for apex technology.

## Unique Hook

Like Heroes of Might and Magic III, but with Champions instead of fantasy heroes, outposts instead of castles, Intel as the Alchemical Dust-style apex-upgrade resource, evidence and public belief as contested terrain, full tactical battles instead of autoresolved abstractions, and climate/corporate infrastructure instead of enchanted kingdoms.

## Target Audience

- Primary: strategy/RPG players who enjoy HoMM-style map exploration, faction identity, hero progression, readable resource snowballing, and campaign scenarios.
- Secondary: cyberpunk fans who want political economy, megacorps, body tech, information warfare, and climate infrastructure beyond generic neon megacities.
- Not for: players seeking real-time action, pure tactical combat, direct spellcasting fantasy, cozy settlement building, or morally simple faction war.

## MDA Analysis

- Mechanics: turn-based strategic map, Champions, squads, hubs/outposts, guarded sites, resources, Intel-funded apex upgrades, a separate evidence/proof layer, crisis clocks, faction buildings, Asset equipment, full tactical battles.
- Dynamics: tempo races, scouting uncertainty, infrastructure control, legitimacy tradeoffs, upgrade specialization, public narrative warfare, risky shortcuts through dark/pirate nets, fragile logistics.
- Aesthetics: mastery, pressure, discovery, faction pride, moral unease, “one more turn,” lonely Arctic scale, cyberpunk intrigue, mythic public crisis.

## Core Loops

### 30-Second Loop

Read the crisis and rival intent, choose a response, commit movement or forces, contest a site, and receive an attributable physical, operational, and public consequence.

### 5-Minute Loop

Claim an opportunity, investigate its risks and stakeholders, commit to one approach, contest it, and prove an account that changes local access or authority. Intel rewards feed slower Asset and apex-unit progression rather than paying for investigation or proof actions.

### Session Loop

Complete one campaign objective or scenario beat: secure a hub, expose a lie, capture a White Sky/Digital-Net node, survive a Blue Monday event, defeat a rival Champion, or shift local legitimacy before the crisis clock advances.

### Long-Term Progression

Develop Champions, asset sets, faction hubs, recruitment networks, Intel upgrade paths, relationship/legitimacy states, and campaign consequences across multiple Arctic-region scenarios and later megacity/corporate-grid campaigns.

## Player Motivation Fit

- Autonomy: choose routes, captures, upgrades, proof actions, faction bargains, and whether to expose, exploit, or suppress information.
- Competence: learn map tempo, resource conversion, scouting reliability, faction strengths, and crisis-clock management.
- Relatedness: Champions are public figures; local communities, factions, rivals, Echoes, and feeds react to their actions.

## Scope Tiers

### Eight-Week Playable Prototype

One complete Arctic-region scenario with normal player-facing UI, initial graphics/audio, and:

- 2 playable factions;
- 2 Champions;
- 3 hubs/outposts;
- 8-12 map sites;
- movement constraints;
- full tactical battle prototype for guarded sites;
- 3 active prototype resources: Credits, Materials, Intel;
- basic asset equipment and Intel upgrade;
- simple Digital-Net/proof overlay;
- one Blue Monday / Blue Week crisis clock.

### Six-Month Early Access Candidate

A near-shipping Blue Monday / Blue Week product milestone with:

- 4 playable factions;
- 4-6 Champions;
- hub building trees;
- recruitment sites;
- complete strategic/tactical loop and AI;
- asset sets;
- local legitimacy mechanics;
- physical and Digital-Net layers;
- authored events and multiple victory paths;
- campaign, skirmish, save/load, editor, mod packaging, and async multiplayer beta;
- graphics, sound, accessibility, performance, packaging, and polish sufficient for an Early Access launch decision.

### Post-Early Access Expansion

Complete and expand the first Arctic campaign arc beyond the Early Access candidate with additional scenarios, factions, content depth, and narrative consequences.

### Full Vision

Multiple campaigns including Arctic wilderness/infrastructure, a megacity/corporate-grid setting, and player/community map editor support with templates and scenario scripting.

## Visual Identity Anchor

White daylight cyberpunk: pale engineered sky, hard Arctic terrain, neon against snow and rust, modular outposts, radar domes, fish plants, drones, body clinics, corporate green branding, and luxury blue-sky simulations.

## Risks

| Risk                                      | Type             | Severity | Mitigation                                                                                  |
| ----------------------------------------- | ---------------- | -------: | ------------------------------------------------------------------------------------------- |
| Core fun hypothesis untested              | Design           |     High | Build MVP prototype before production.                                                      |
| Arctic region becomes exotic scenery      | Narrative/design |     High | Make local consent, sovereignty, and infrastructure dependency mechanically visible.        |
| Too many resources                        | Systems          |     High | Keep the prototype economy to Credits, Materials, and Intel.                                |
| Intel becomes generic mana or proof currency | Systems/theme | High | Restrict Intel sinks to Asset upgrades and apex-unit/production unlocks; use Evidence/Proof state for information warfare. |
| No-magic cyberpunk loses HoMM readability | UX/design        |     High | Preserve towns, guarded sites, resources, routes, dwellings, hero assets, and turn clarity. |
| UNP Net authority cleans up the setting   | Worldbuilding    |   Medium | Keep it treaty-bound, partial, contested, and dependent on corporate/state cooperation.     |
| Animal-control fantasy becomes silly      | Tone             |   Medium | Ground in telemetry, biosecurity, wildlife management, and hacked sensor networks.          |

## Open Questions

| Question                                                                                                       | Owner  | Deadline                    | Resolution                                                                                     |
| -------------------------------------------------------------------------------------------------------------- | ------ | --------------------------- | ---------------------------------------------------------------------------------------------- |
| Should the first campaign use real Greenland/Kalaallit Nunaat or a fictionalized Arctic autonomy?              | Human  | Before concept approval     | Resolved 2026-07-10: fictional Arctic region, internally Greenland-inspired; exact name/polity remains open.   |
| Is Blue Monday primarily the initial sky-break event, with Blue Week as the later/retrospective crisis period? | Human  | Before concept approval     | Current direction: Blue Monday is the initial event; Blue Week is later/retrospective framing. |
| What is the first player faction?                                                                              | Human  | Before systems design       | Pending                                                                                        |
| What should the UNP Net security body be called?                                                               | Human  | Before world slice approval | Digital Peacekeeping Directorate; commonly the Blue / the Blues.                               |
| Is Intel global, Champion-local, or hybrid?                                                                    | Shared | Before resource GDD         | Resolved for prototype: global faction resource.                                               |
| Does combat use full tactical battles in MVP or guarded-site autoresolution first?                             | Human  | Before MVP plan             | Full tactical battles.                                                                         |
