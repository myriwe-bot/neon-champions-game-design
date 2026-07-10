---
title: Accelerated Prototype and Early Access Plan — 2026-07-10
type: decision-brief
status: in-review
phase: production
owner: shared
created: 2026-07-10
updated: 2026-07-10
related:
  - design/gdd/game-concept
  - design/gdd/game-pillars
  - design/gdd/strategic-map
  - design/gdd/tactical-combat
  - docs/architecture/determinism-and-rng-adr
  - docs/architecture/data-scenario-save-format-adr
  - production/playtests/playtest-journal
approval: pending
---

# Accelerated Prototype and Early Access Plan — 2026-07-10

## Status and authority

The owner approved the delivery ambition and constraints below on 2026-07-10. The detailed sequencing remains **in review** until the owner approves this plan or revises it.

This plan does not authorize implementation by itself. Implementation still requires approved capability epics and READY stories.

## Human-approved delivery direction

1. Produce a fully playable prototype in approximately **8 weeks**, not 12–16 weeks.
2. The prototype must already have a normal player-facing interface, coherent visual treatment, initial graphics, sound, and game-feel feedback. It cannot remain a debug UI with raw IDs.
3. Reach a near-shipping **Early Access candidate in 24 weeks** with graphics, sound, polish, editor/tooling, and the broad product feature set described in the July 6 Claude plan and subsequent audit discussion.
4. The six-month target is not a narrow demo. It is the first substantial commercial product milestone.
5. Use four playable factions by the six-month target: Home Rule Coalition, QXZ Meridian, Barents, and Janus-Kestrel, subject to later faction-design approval.
6. Include a usable map/scenario editor in the six-month product.
7. Do not forecast capacity from raw story counts. Plan by playable capabilities and parallel production lanes.

## Human-approved design corrections

### First campaign geography

- Do not publicly identify the first campaign as Greenland because of current geopolitical concerns.
- Do not lock a replacement name or exact polity yet.
- Working direction: an unnamed fictional Arctic region, internally inspired by Greenland after significant ice-shelf retreat.
- `Meridian Shelf` is rejected.
- Existing Greenland research remains useful internal grounding, not player-facing location authority.

### Determinism and randomness

- Current deterministic behavior is a temporary implementation baseline, not a human-approved final product identity.
- Reach a stable, playtestable combat baseline before introducing randomness.
- Revisit tactical resolution after that baseline; likely direction is visible damage ranges and controlled seeded randomness.
- Any implemented randomness still requires deterministic seed ownership, replay/save/debug support, preview rules, and tests.

### Blue Monday

- Working private-truth direction remains: an activist attack or limited shutdown attempt contributes to the initial sky break; a larger infrastructure/failsafe cascade causes the disaster.
- Exact culpability, tutorial framing, and whether the tutorial depicts the attack remain open.
- Do not spend the next implementation train resolving this narrative detail.

### Champion Operations idea

- Keep the existing Command / Operations / Doctrine model as current authority.
- Record army-generated Bandwidth / Protocol capacity as an exploratory option.
- Do not replace the existing model until a focused design comparison and combat prototype justify it.

### Ukrainian defense megacorp

- Rename `Tryzub Systems` to **Vezha Systems**.
- Dnipro Systems and Sich Dynamics remain subsidiaries/acquired predecessor firms.
- Do not merge Vezha Systems with Janus-Kestrel.

## Production model required by the ambition

The target is not credible as one serial story lane. Run four coordinated lanes with one human creative director:

| Lane | Primary output | Near-term owner model |
| --- | --- | --- |
| Core game | strategic/tactical rules, AI, economy, information, persistence, networking | Codex/Hermes implementation agents with strict tests |
| UX and presentation | UI architecture, strategic/tactical screens, game feel, accessibility | dedicated agent lane plus human visual review |
| Content and audiovisual | maps, scenarios, factions, units, narrative, 2D/3D assets, VFX, sound, music | agent-assisted authoring plus licensed/generated/contracted assets |
| Tools and product | editor, validators, mod packaging, builds, distribution, telemetry/crash reporting | dedicated tools/infrastructure lane |

Required operating changes:

- Use medium-batched capability stories rather than dozens of tiny scaffolding stories.
- Keep one integration owner/gate; parallel lanes merge only through green CI and playable integration smoke.
- Capture screenshots/video for every presentation story.
- Run a human playtest at least weekly from week 2 onward.
- Add outside testers by week 6, not only at final hardening.
- Choose the asset sourcing strategy in week 1. Code throughput cannot substitute for art direction, sound, and content production.

## Eight-week fully playable prototype

### Weeks 1–2 — production reset and playable shell

Goal: replace the debug-instrumented presentation with a coherent game shell while protecting the existing tested loop.

Deliver:

- map-first strategic interface with no raw IDs in normal play;
- tactical interface with initiative, selected stack, legal actions, forecasts, and concise event feedback;
- normal menus, scenario start, settings shell, pause/restart, and win/loss flow;
- first cohesive visual kit: palette, typography, map tokens, faction color/shape language, unit silhouettes, terrain tiles, effects baseline;
- first audio kit: UI confirmations/denials, attack impact, movement, battle transition, ambient loop, one music bed;
- data loading failure becomes explicit; hardcoded scenario fallback is removed or isolated behind a developer-only switch;
- reusable static definitions separated from scenario placement where necessary for multiple maps;
- UI Toolkit and plain-.NET extraction handled as bounded spikes, not unconditional migrations;
- revised prototype map brief for 16–24 meaningful nodes with loops, chokepoints, prizes, bases, and a victory network;
- fresh human baseline playtest entered in the journal.

Gate A — **legible shell**: a player starts, acts, enters combat, returns, and understands win/loss without seeing implementation IDs or needing developer explanation.

### Weeks 3–4 — strategic game and opponent

Deliver:

- 16–24-node authored Arctic test map;
- Credits, Materials, and Intel economy with visible recurring income and competing sinks;
- one-build-per-base cadence and meaningful facility choices;
- guarded rewards, caches, contractor/recruitment sites, and a temptation every few moves;
- networked victory objective rather than one easy central capture;
- strategic AI that values sites, recruits, contests objectives, attacks when favorable, and protects its own route;
- operations-cycle forecast and cadence at minimum viable depth;
- first maintenance site and source-tagged output discrepancy;
- engagement brief before tactical battle;
- save/resume prototype for the full test scenario;
- visual/audio pass on all new interactions.

Gate B — **strategic choice**: testers can describe competing routes, economy tradeoffs, opponent pressure, and why the objective cannot be solved by a trivial rush.

### Weeks 5–6 — tactical depth and faction identity

Deliver:

- HRC and QXZ prototype rosters at five basic tiers, with upgrades allowed to remain selective for the 8-week build;
- initiative, AP, Wait, Defend, retaliation, morale/cohesion, terrain, hazards, and mission objectives working together;
- one signature active per implemented unit line plus faction passives;
- current Command / Operations / Doctrine model made readable and useful;
- 2–3 polished Operations per current core channel only where needed for the prototype roster;
- tactical boards selected from strategic context;
- tactical AI able to use objectives, terrain, unit roles, and signature actions;
- battle speed and autoresolve/fast-resolution direction evaluated;
- controlled audiovisual identity for both factions.

Gate C — **combat worth repeating**: battles create distinct army-composition and terrain decisions without relying on hidden rules.

### Weeks 7–8 — distinctive vertical prototype

Deliver:

- unknown / detected / identified or Lead / Stale / Verified information states reconciled into one readable model;
- ghost/decoy contact at prototype depth;
- Feed as event log and player-facing world frame;
- attribution/Heat prototype with at least one threshold consequence;
- one Champion public consequence and at least two defeat outcomes;
- maintenance/audit/repair loop connected to the economy;
- victory web connected to multiple tactical mission types;
- editor foundation able to load, validate, modify, and save the prototype map/scenario data, even if usability remains developer-facing;
- tutorial/onboarding flow over the real game shell; the Blue Monday attack may later become its narrative framing;
- first outsider playtests and repair pass;
- packaged Windows prototype build.

Prototype Gate — **fully playable at 8 weeks**:

- complete 60–120 minute match/scenario;
- normal interface and cohesive initial graphics/audio;
- two differentiated factions;
- functional strategic and tactical AI;
- save/resume;
- no critical readability blockers;
- testers can explain both the core loop and at least two Neon Champions differentiators;
- editor foundation proves that another map can be authored without bespoke runtime code.

If this gate fails, repair the prototype immediately, but continue asset/content production in parallel rather than pausing the entire roadmap.

## Weeks 9–16 — Early Access breadth

### Weeks 9–12 — systems completion and first campaign slice

Deliver:

- explicit seeded RNG service and ADR revision if playtests approve damage ranges;
- visible tactical damage ranges with reproducible seeds and exact replay/save continuation;
- complete HRC and QXZ five-tier rosters with upgrades;
- full Heat/attribution/Lantern intervention ladder at first-product depth;
- fuller Feed, sentiment/legitimacy, and manipulation operations;
- Champion Wounded, Captured, Echoed, and Martyred outcomes where narratively approved;
- squad/detachment names and lightweight persistent traits;
- doctrine drafts;
- convoy and interdiction missions;
- seasonal/forecast route changes;
- Audience/broadcast tradeoff;
- production-ready save/load and replay-debug logs;
- two linked campaign scenarios including tutorial/onboarding;
- editor MVP with node/edge/site/objective/event editing, undo/redo, validation, preview, and save;
- first external schema/mod documentation.

Gate D — **vertical slice**: HRC/QXZ campaign slice is presentation-complete enough for public preview and the editor can create a valid alternate scenario.

### Weeks 13–16 — four-faction product

Deliver:

- Barents and Janus-Kestrel complete five-tier rosters with upgrades;
- faction economies/tracks and information identities;
- Bandwidth-from-army experiment resolved: integrate, restrict to a faction/doctrine, or reject based on evidence;
- broader Protocol/Operation content without replacing approved vocabulary accidentally;
- faction-aware strategic and tactical AI;
- balance/autoplay harness and reports;
- third campaign scenario and skirmish generator;
- editor usability pass and scenario templates;
- mod/datapack discovery, packaging, compatibility/version checks, and error reporting;
- async multiplayer vertical slice using command logs, version checks, persistence, resign/time controls, and desync detection;
- faction audiovisual differentiation and upgraded unit presentation.

Gate E — **content-complete alpha**: four factions, three-scenario campaign, skirmish, editor, mods, and async match flow all work end-to-end, with placeholders explicitly inventoried.

## Weeks 17–24 — near-shipping Early Access candidate

### Weeks 17–20 — production quality

Deliver:

- replace remaining critical placeholder art, icons, text, animation, VFX, audio, and music;
- final strategic/tactical information hierarchy and accessibility pass;
- scenario pacing, difficulty presets, and AI personality tuning;
- campaign narrative/event pass and Echo tutorial decision;
- editor documentation and starter templates;
- async multiplayer UX, recovery, notifications, and compatibility hardening;
- performance budgets and profiling;
- crash reporting and diagnostic export;
- localization-ready string tables and at least one pseudo-localization pass;
- Steam/demo packaging direction and store assets started;
- weekly external playtests with tracked funnels and completion rates.

Gate F — **beta**: all advertised Early Access features exist, no critical placeholder blocks comprehension, and the full campaign path can be completed repeatedly.

### Weeks 21–24 — ship candidate

Deliver:

- bug burn-down and regression hardening;
- balance pass informed by human and batch simulation evidence;
- save migration and backward-compatibility policy;
- input remapping, text scaling, contrast, motion, and audio controls;
- install/update/uninstall and clean-machine verification;
- editor/mod security and destructive-action safeguards;
- multiplayer desync/recovery tests;
- final legal/provenance inventory for assets, licenses, generated content, music, fonts, and middleware;
- release checklist, known issues, support plan, telemetry/privacy stance, rollback/patch plan;
- release-candidate build and external acceptance playtest.

Six-Month Gate — **Early Access candidate**:

- near-shipping commercial presentation;
- four playable factions and approximately forty basic/upgraded unit variants;
- strategic and tactical layers with AI;
- campaign, skirmish, save/load, editor, mod packaging, and async multiplayer beta;
- dirty information, maintenance, Heat/attribution, Feed/legitimacy, Champion consequences, convoys, seasonal map behavior, doctrines, squad identity, and Audience/broadcast systems at coherent first-product depth;
- graphics, audio, UX, accessibility, performance, packaging, and support readiness sufficient for an Early Access launch decision.

## Scope discipline inside the ambitious target

Including a feature does not require maximum depth.

Use three levels:

- **Product-complete:** the advertised player loop works end-to-end and is supportable.
- **First-product depth:** a narrow but coherent rule/content set, designed to expand after Early Access.
- **Experimental/beta:** explicitly labeled but usable, especially async multiplayer and mod support.

Do not respond to schedule pressure by adding hollow UI buttons, schemas with no users, or systems only agents can operate. Every included feature must have a playable path, validation, UI, and evidence.

## Critical dependencies and failure modes

1. **Asset throughput:** choose licensed/generated/contracted art and audio sources immediately. Without this, near-shipping presentation is not credible.
2. **Parallel integration:** four lanes require branch discipline and a daily integration build. Serial story execution will miss the target.
3. **Human decisions:** unresolved faction, geography, Operations, and narrative details must not block systems with placeholder-safe data contracts.
4. **UI architecture:** extending the 3,960-line bootstrap directly will slow every lane. Decompose or replace touched presentation surfaces early.
5. **Test architecture:** split the 5,989-line PlayMode suite as new product surfaces arrive.
6. **Editor scope:** editor must author the actual runtime format; no second hidden format.
7. **Networking scope:** async multiplayer remains beta unless persistence, versioning, desync detection, and recovery pass real tests.
8. **Quality truth:** automated evidence cannot substitute for weekly human playtests.

## Immediate next capability train

Recommend one medium-batched, implementation-facing epic:

**EPIC-016 Accelerated Playable Product Foundation**

Children to prepare after plan approval:

1. `STORY-UI-SHELL-001 Map-First Strategic UI and Normal Player Shell`
2. `STORY-PRESENTATION-001 Initial Visual/Audio Kit and Evidence Pipeline`
3. `STORY-MAP-FUN-001 Dense Arctic Prototype Map, Economy, and Objective Web`
4. `STORY-AI-PLAY-001 Strategic AI Value, Recruitment, Contest, and Attack`
5. `STORY-TACTICS-FUN-001 Tactical Initiative, Roles, Terrain, and Signature Actions Integration`
6. `STORY-PROTOTYPE-016 Eight-Week Playable Prototype Integration and Human Gate`

Promote only the first approved child to READY at a time, but allow independent art/audio research and asset sourcing to run concurrently.

## Verdict

**CONCERNS / AMBITIOUS BUT ACTIONABLE WITH CONDITIONS.**

The target is intentionally aggressive. It is viable as a production plan only if work becomes genuinely parallel, asset sourcing begins immediately, medium-batched stories replace excessive ceremony, and human playtests govern integration. Under a serial one-agent/one-story pipeline with no dedicated asset lane, it is not a credible forecast.
