---
title: Full Project Review and Completion Plan — 2026-07-12
type: decision-brief
status: in-review
phase: production
owner: shared
created: 2026-07-12
updated: 2026-07-12
related:
  - production/planning/accelerated-prototype-and-early-access-plan-2026-07-10
  - production/playtests/playtest-journal
  - design/gdd/game-concept
  - design/gdd/game-pillars
  - design/gdd/systems-index
  - design/gdd/strategic-map
  - design/gdd/tactical-combat
  - docs/architecture/data-scenario-save-format-adr
  - docs/architecture/determinism-and-rng-adr
approval: pending
---

# Full Project Review and Completion Plan — 2026-07-12

## Executive verdict

**Strategic direction: APPROVE WITH MAJOR REVISION.**

**Current roadmap as executable schedule: BLOCKED.**

**Current build as a technical prototype: CONCERNS, but promising.**

**Current build as a commercial game: NOT READY.**

Neon Champions has three unusually strong foundations:

1. a distinctive core fantasy — command a mythic cyberpunk Champion through an Arctic infrastructure crisis beneath an engineered White Sky;
2. a tested strategic/tactical code foundation with strong deterministic domain tests and CI;
3. a world thesis that can differentiate it from generic HoMM-likes: infrastructure is power, information has provenance, and Champions are public identities rather than simple heroes.

The primary danger is not lack of ideas. It is **production inversion**: governance, tests, stories, and designed system breadth have advanced faster than player-facing quality, human fun evidence, content tooling, audiovisual production, and product definition.

The existing 8-week prototype and 24-week Early Access ambition should remain as a target, but the clock should not be treated as credibly started until a short Production Definition Gate is passed. The six-month target is only credible with genuine parallel specialist lanes, immediate asset sourcing, ruthless prototype focus, weekly human playtests, and an explicit willingness to label editor/modding/async multiplayer as beta or move them behind the launch decision if they threaten the core game.

## Evidence basis

Reviewed current synchronized `main` across:

- game design: `95a8c25341dccc90778fe5fc78e2831fe82193d7`;
- Unity: `6c0e9addff25c519053edc3f3be8ab52b932bc0c`;
- world vault: `c0cfa3233c9b4077a4690f827b1f02935a843718`.

All three working trees were clean and matched `origin/main` during review.

Unity evidence includes:

- 75 C# files and approximately 41,927 lines;
- 23,004 runtime lines and 18,852 test lines reported by repository audit;
- 35 test files, 422 test methods, and strong EditMode/PlayMode coverage;
- one enabled game scene;
- no gameplay prefabs, no production gameplay art, and no audio assets;
- one JSON scenario and a retained hardcoded fallback;
- current presentation concentrated in `StrategicMapBootstrap.cs` at about 3,960 lines;
- PlayMode smoke concentrated in one file at about 5,989 lines;
- approximately 1 GB of checked-in evidence history, including hundreds of PNGs, without Git LFS.

The latest checked-in human-turn screenshot remains a debug/instrumentation surface: raw IDs, large diagnostic panels, weak map hierarchy, disabled-looking action rows, placeholder geometry, dense text, and no commercial visual identity. It proves state visibility and automation, not a normal strategy-game interface.

Fresh Unity tests were not rerun in the Linux audit environment because the project CI is Windows/self-hosted Unity. Checked-in CI and evidence were inspected, not misrepresented as fresh execution.

## What is genuinely strong

### 1. The game has a saleable fantasy

The strongest public-facing promise is:

> Lead an iconic cyberpunk Champion across a frozen frontier, build an army, seize the machines keeping the world alive, and fight over what people believe happened.

This is stronger than leading with Treaty Net, admissibility, continuity liability, provenance, or institutional acronyms. Those ideas are valuable depth; they should be discovered through play after the basic fantasy is understood.

### 2. The world has real thematic differentiation

White Sky, infrastructure dependency, body continuity, Echo identity, corporate personhood, polluted feeds, maintenance politics, and factions as evolutionary philosophies form a coherent thesis. This is not generic neon cyberpunk.

### 3. The implementation foundation is unusually testable

Plain C# domain/application boundaries, deterministic behavior, strong test coverage, CI, stable IDs, and evidence requirements are valuable. They should make balancing, replay/debugging, AI simulation, and future networking easier if the architecture is simplified rather than allowed to accrete.

### 4. The project records human complaints rather than erasing them

The preserved complaints in `production/playtests/playtest-journal.md` are excellent source material. They identify real failures: unreadability, unclear turns, tiny tactical space, unclear armies and stacks, confusing attacks, unexplained abilities, broken-feeling objectives, and poor map control.

### 5. The intended differentiators can reinforce the strategy loop

Dirty information, maintenance, legitimacy, Champion consequences, and infrastructure control can create meaningful strategic tradeoffs rather than becoming separate narrative minigames — if integrated through one or two concrete player verbs each.

## Fundamental problems

### 1. The project is not yet governed by an approved north star

`design/gdd/game-concept.md`, `design/gdd/game-pillars.md`, and `design/gdd/systems-index.md` remain draft/pending. The approved-world slice is still only a short draft scaffold. Faction game briefs remain an empty template.

This creates an inversion: dozens of implementation stories are DONE while the high-level product contract remains pending. Narrow story exceptions helped development move, but continuing this pattern will produce local correctness and global incoherence.

**Recommendation:** approve a concise Product Constitution before the next implementation epic. It should lock the player fantasy, primary audience, pillars, anti-pillars, prototype factions, first-player faction, core loop, prototype victory structure, and product scope tiers. It need not settle all lore.

### 2. Human fun evidence is almost absent

The playtest journal is a template plus historical complaint seeds, not a cadence of dated playthroughs. Automated screenshots and agent closeouts prove execution and state, not enjoyment, comprehension, pacing, desire to replay, or emotional identity.

**Recommendation:** no major system expansion until a fresh owner playthrough is recorded. From then on, run one internal human playtest every week and an outside test at least every two weeks after the shell is legible.

### 3. The current UI architecture is a delivery bottleneck

A roughly 3,960-line `StrategicMapBootstrap.cs` and 2,352-line input session indicate that presentation, orchestration, and interaction concerns are over-concentrated. The screenshot confirms the player experience is still shaped like a debug harness.

A cosmetic skin over this surface will fail. The player shell needs decomposition around screens, presenters/view-models, reusable controls, map interaction, and a debug overlay that can be turned off.

**Recommendation:** make the first implementation capability a bounded shell replacement/decomposition, not broad gameplay expansion. Preserve the tested domain layer and replace only the touched presentation path.

### 4. The plan confuses feature breadth with product value

The 24-week ledger includes four factions, roughly forty unit variants, campaign, skirmish, editor, mods, asynchronous multiplayer, dirty information, Feed, Heat, legitimacy, Champion outcomes, doctrines, convoys, seasons, Audience, save migration, accessibility, release hardening, art, audio, and more.

This is not impossible in principle, but it is not credible for a serial AI-agent workflow plus one human director. Integration, content tuning, visual judgment, UX repair, and testing scale nonlinearly.

**Recommendation:** preserve the feature ledger but assign each feature one of four statuses:

- launch-critical;
- Early Access first-product depth;
- explicit beta;
- post-launch unless ahead of schedule.

Async multiplayer should be behind a launch-risk firewall. The editor should first be an internal scenario-production tool; public usability is a separate product feature. Mod packaging should follow a stable runtime schema, not precede it.

### 5. Content production has no demonstrated throughput

The roadmap calls for maps, scenarios, four factions, units, upgrades, events, tutorials, narrative, art, VFX, audio, and music, but the Unity repository has no production gameplay art/audio and no demonstrated repeatable scenario pipeline beyond one JSON file.

**Recommendation:** conduct an asset and content production spike before committing to the six-month presentation claim. Build one representative final-ish strategic node, one Champion portrait/token, one tactical unit family, one terrain set, one attack VFX/SFX sequence, and one music/ambience sample. Measure real integration time and establish a style bible, naming/license ledger, and import rules.

### 6. The first campaign is a setting premise, not yet a campaign

The fictional Arctic region, Blue Monday, HRC, and QXZ provide a strong premise. Missing are the playable protagonist, emotional stakes, scenario arc, antagonist relationship, mission escalation, major reversals, recurring characters, ending decision, and how campaign consequences persist.

**Recommendation:** write a one-page campaign spine before creating multiple scenarios. Keep it player-facing and dramatic, not encyclopedic.

### 7. Faction philosophy has not become faction gameplay

The faction-pillar language is strong, but `design/world/faction-game-briefs.md` is empty and broad rosters remain draft. Four factions by six months will become cosmetic variants unless each has a concise gameplay contract.

**Recommendation:** for each faction define:

- player fantasy in one sentence;
- strategic advantage and strategic liability;
- tactical rhythm;
- information relationship;
- infrastructure relationship;
- Champion archetype;
- signature resource conversion;
- one heroic and one horrific expression;
- explicit anti-overlap with every other faction.

Only HRC and QXZ need full prototype depth. Barents and Janus-Kestrel should not enter production until that template proves useful.

### 8. Neon Champions mechanics risk becoming administrative overlays

Feed, Heat, attribution, legitimacy, maintenance, source tags, stale Intel, and Champion outcomes are interesting, but too many meters and status vocabularies can bury the core fantasy under bureaucracy.

**Recommendation:** every differentiator must pass a verb-and-consequence test:

- What does the player actively do?
- What opportunity does it create this turn?
- What visible cost or risk follows?
- How does the opponent respond?
- Can it be explained without lore jargon?

If a system cannot answer these, keep it as event/content framing rather than a standalone meter.

### 9. Tactical combat is over-scoped for the first strong prototype

The 8-week plan combines five-tier rosters, initiative, AP, Wait, Defend, retaliation, morale/cohesion, terrain, hazards, objectives, signature actions, Operations, tactical AI, and audiovisual faction identity. This is enough for a full tactics game and leaves little time for tuning.

**Recommendation:** prototype combat should prove three things:

1. army composition changes decisions;
2. terrain/objective changes decisions;
3. HRC and QXZ feel different.

Use three strongly differentiated unit lines per faction plus one Champion/Operation layer first. Add tiers/upgrades only when the base match is readable and worth repeating.

### 10. Strategic map success criteria need stronger pressure and replay value

The project has already found trivial-rush and unclear-objective problems. A larger map alone will not fix this.

**Recommendation:** prototype scenario design should include:

- at least three viable opening routes;
- one early irreversible or costly commitment;
- visible opponent pressure by turn 2–3;
- a victory web requiring two or three linked conditions;
- one optional high-risk prize;
- one information-driven route reversal;
- one comeback valve that does not erase advantage;
- expected session length and turn-count budgets.

### 11. Save/load, localization, accessibility, release, and commercial work are mostly promises

There is no production save/load, localization implementation, normal settings shell, telemetry/crash pipeline, store plan, pricing/positioning artifact, community plan, support process, or robust clean-machine release pipeline demonstrated.

**Recommendation:** add a Product/Release lane now, but keep it thin until the prototype is enjoyable. Its first outputs should be save architecture, string-table enforcement, input remapping stance, settings persistence, build versioning, crash-log export, license/provenance ledger, and a Steam positioning brief.

### 12. Repository evidence is becoming technical debt

Approximately 1 GB of checked-in historical evidence and hundreds of PNGs without LFS will slow clones, CI, and agent work. One 5,989-line PlayMode file is also a maintenance bottleneck.

**Recommendation:** move future bulk evidence to CI artifacts or Git LFS with an indexed lightweight summary in Git. Split PlayMode suites by player journey/screen. Do not rewrite history casually; create and approve a migration policy first.

## Opportunities

### 1. Make public truth a tactical-strategic weapon

Instead of adding a generic morality system, let proof affect concrete map rules: access, recruitment price, local assistance, legal attack permission, extraction routes, surrender, or post-battle consequences.

### 2. Turn maintenance into tempo, not chores

Maintenance should produce strategic dilemmas: keep a failing route alive, exploit it before collapse, expose the owner, divert resources, or allow a crisis that harms both sides differently. Avoid routine repair clicking.

### 3. Use Champions as the campaign’s emotional persistence layer

Armies and maps may reset, but Champion body state, public reputation, legal status, Echo continuity, rivals, and signature equipment can carry memory across scenarios.

### 4. Treat the White Sky as a visual and mechanical clock

Sky color, light, forecast overlays, atmospheric effects, and infrastructure behavior can make the crisis legible without text walls. This is a strong art-direction anchor and a natural source of scenario escalation.

### 5. Design the editor first as the studio’s content multiplier

An internal authoring tool that reliably creates and validates scenarios can save the schedule. A polished public editor is valuable but should be a second layer over the same format.

### 6. Build marketing proof alongside the vertical slice

A striking map view, Champion close-up, tactical clash, White Sky transition, and one dirty-information reveal can become the first trailer/GIF language. This also forces the product fantasy to remain visually comprehensible.

## Revised production model

### Production Definition Gate — before Week 1

Timebox: maximum 5–7 working days. This is not a new month of design.

Required decisions and outputs:

1. Approve the Product Constitution: concept, pillars, anti-pillars, target player, prototype factions, first-player faction, core loop, and scope tiers.
2. Record a fresh owner playthrough of current `main`, including exact complaints and a KEEP/REVISE/REJECT verdict.
3. Select asset strategy and budget: licensed, generated, contracted, original, or hybrid.
4. Approve the prototype product contract below.
5. Produce one representative audiovisual integration spike.
6. Approve technical shell decomposition boundaries.
7. Create a single integrated milestone dashboard by capability, not story count.

Do not resolve every world mystery or write all faction lore during this gate.

## Recommended eight-week prototype contract

### Non-negotiable player experience

- One polished 60–90 minute scenario, replayable in approximately 30–60 minutes after learning.
- HRC versus QXZ.
- One primary player Champion and one rival Champion; optional second Champion only if it improves strategic choice.
- Normal map-first UI, settings/pause/restart, win/loss, save/resume, tutorial prompts, and no raw IDs.
- Strategic and tactical AI sufficient for the scenario.
- Cohesive initial art/audio treatment.
- At least two unmistakable Neon Champions differentiators.
- A second scenario can be created through the internal data/tool path without runtime code changes.

### Recommended strategic depth

- 16–20 meaningful nodes, not 24 by default.
- Three resources: Credits, Materials, Intel.
- Three opening routes and linked victory conditions.
- One base per side plus neutral infrastructure.
- Three facility choices total, not a broad building tree.
- Three recruitment/contractor decisions per faction.
- One maintenance dilemma.
- One dirty-information/proof loop.
- One Champion consequence at scenario end.

### Recommended tactical depth

- Three core unit lines per faction, with one upgrade or variant each only if useful.
- One Champion command identity per side.
- AP, move, attack, Defend, and one timing option such as Wait.
- Retaliation only if readable and strategically meaningful.
- Two terrain families and two mission objectives.
- One signature active per unit line only where it changes decisions.
- Morale/cohesion only if it produces understandable visible choices; otherwise move it after the prototype.
- No obligation to implement five complete tiers before combat is fun.

### Explicit prototype exclusions

- public-ready editor UX;
- mods;
- multiplayer;
- four-faction balance;
- full campaign persistence;
- complete Heat/legitimacy ladders;
- complete Champion death-state matrix;
- broad doctrine system;
- convoys and seasons unless integral to the single scenario;
- polished autoresolve.

These remain six-month/post-prototype product candidates, not permanent cuts.

## Eight-week execution sequence

### Week 1 — product shell and vertical look target

- Decompose the current bootstrap enough to support normal screens and hide diagnostics.
- Build title/scenario start, strategic HUD, selected-object panel, action bar, pause/settings, and win/loss shell.
- Integrate the representative art/audio kit.
- Establish debug overlay toggle.
- Run owner playtest and repair immediately.

**Gate:** a new player can start, select, move, understand a site, end a turn, and identify the objective without raw IDs or developer explanation.

### Week 2 — strategic interaction quality

- Implement map pan/zoom/focus, selection hierarchy, routes, reachability, site states, resources, recruitment, and clear denial/result feedback.
- Lock the 16–20-node scenario topology.
- Remove or isolate hardcoded fallback.
- Split static definitions from scenario placement where required.

**Gate:** tester can explain three route choices, their army, resources, and what will happen next turn.

### Week 3 — strategic pressure and save/resume

- Upgrade AI to value sites, recruit, contest, attack, and protect routes.
- Implement linked victory web and opponent pressure.
- Add save/resume with version and scenario identity.
- Add engagement brief before combat.

**Gate:** no trivial objective rush; save/reload continues the same match correctly.

### Week 4 — tactical readability and core decisions

- Replace tactical debug presentation with readable initiative, stack identity, movement, legal targets, forecast, action results, and battle conclusion.
- Implement only the chosen core action set and terrain families.
- Split the monolithic PlayMode file by journey.

**Gate:** tester can explain whose turn it is, which side is theirs, what each stack does, why an action is legal, and what the result was.

### Week 5 — HRC/QXZ identity

- Implement three core unit lines and one Champion command identity per faction.
- Add faction-specific strategic advantage/liability.
- Integrate audiovisual faction language.
- Tune tactical AI for roles and objectives.

**Gate:** blind-description test — players can identify which faction they played from incentives and behavior, not color/name alone.

### Week 6 — Neon Champions differentiator integration

- Integrate one dirty-information/proof loop.
- Integrate one maintenance/infrastructure dilemma.
- Frame outcomes through Feed without adding multiple redundant meters.
- Add one scenario-end Champion consequence.
- Begin outside tests.

**Gate:** testers can name two things this game does that HoMM or a generic tactics game does not.

### Week 7 — onboarding, content, and internal editor path

- Tutorialize the real scenario through contextual prompts and safe early decisions.
- Validate all player-facing strings and remove raw IDs.
- Prove second-scenario authoring through the same data format.
- Add settings, remapping baseline, text scaling, contrast checks, and audio controls.

**Gate:** outside tester completes the opening and first battle without live guidance.

### Week 8 — integration and prototype release

- Bug burn-down, balance, pacing, performance, clean-machine build, save/load regression, and evidence.
- Run at least five outside playthroughs if feasible.
- Produce a short gameplay capture.
- Make a formal prototype gate decision: continue, repair, or redesign.

**Gate:** complete, understandable, coherent, replayable prototype with no critical comprehension blocker.

## Six-month roadmap after prototype

Do not pre-authorize every feature. Re-plan at the Week 8 evidence gate.

### Months 3–4 — vertical slice and content-production proof

Priority:

1. two- or three-scenario HRC/QXZ campaign arc;
2. production save/load and migration policy;
3. internal editor MVP used by the team for every new scenario;
4. stable static definitions, localization keys, and validation;
5. deeper HRC/QXZ rosters only where playtests demand it;
6. Heat/attribution/legitimacy at one coherent first-product depth;
7. Champion persistence and consequence framework;
8. skirmish setup and balance simulation;
9. presentation quality sufficient for public footage and store-page testing.

Gate: strangers can play the campaign slice, understand the fantasy, finish it, and express interest in another scenario.

### Month 5 — breadth decision, not automatic breadth

Add Barents and Janus-Kestrel only if:

- HRC/QXZ content production throughput is measured;
- faction contracts are approved;
- tools can author content without code bottlenecks;
- AI can use faction rules;
- presentation lane can differentiate them;
- adding them does not threaten campaign completion.

Otherwise ship the first Early Access build with two deep factions and announce the next two transparently. Four shallow factions are worse than two memorable factions.

Editor public UX, mod packaging, and async multiplayer each require independent go/no-go gates. Recommended order:

1. internal editor;
2. public editor usability;
3. stable mod/datapack schema;
4. async multiplayer only after save/replay/versioning are proven.

### Month 6 — release candidate hardening

- content lock;
- critical placeholder replacement;
- onboarding and accessibility completion;
- performance profiling;
- clean-machine installation/update/uninstall;
- crash diagnostics and support bundle;
- legal/provenance/license audit;
- Steam page, screenshots, trailer, pricing/positioning, known issues, support and patch plans;
- external acceptance playtest;
- launch/no-launch decision based on evidence, not date alone.

## Team and lane requirements

Minimum credible lane ownership:

1. **Creative/product director:** final design, scope, playtests, integration verdicts.
2. **Core engineering:** domain, AI, save/load, data, tactical/strategic systems.
3. **UX/presentation:** screen architecture, map interaction, usability, accessibility.
4. **Art/content/audio:** visual target, assets, animation/VFX, maps, narrative, SFX/music.
5. **Tools/release:** editor, validation, builds, versioning, crash/support, store preparation.

One person may own multiple lanes, and agents can accelerate each lane, but a lane without an accountable human reviewer is not staffed. AI cannot supply taste, player observation, or final asset coherence by itself.

## Production rules

1. One integrated playable `main` at all times.
2. Daily or per-merge playable smoke; weekly human build.
3. No feature enters the prototype without a player verb and observable consequence.
4. No system is called complete without UI, feedback, AI interaction, save behavior, and playtest evidence as applicable.
5. Debug tooling is preserved behind toggles, never mixed into normal UI.
6. Medium-batched capability stories replace ceremony-heavy micro-stories, but every batch retains explicit acceptance criteria and evidence.
7. At most one major unknown per capability story; use bounded spikes for UI Toolkit, asset pipelines, networking, and editor architecture.
8. Human playtest findings outrank automated screenshot approval for fun and clarity.
9. Do not merge new world canon into gameplay by implementation inertia.
10. Every Friday: capability review, risk review, scope review, and next-week go/no-go.

## Owner decisions — recorded 2026-07-12

1. **Prototype factions:** HRC and QXZ are the clear opposing factions. Both are playable; neither is inherently the protagonist or villain. Campaign viewpoint may vary by scenario or side.
2. **Prototype units:** reducing to three strong lines per faction is acceptable only if the lines create enough composition and tactical variety. This remains a prototype-depth question, not approval to make factions thin.
3. **Base/town building:** the prototype must open meaningful Heroes-style base construction and resource choices. The narrow three-facility recommendation is not accepted as a permanent model; the exact prototype breadth still needs a focused base-building packet.
4. **Asset direction:** final ambition is contractors and/or original work. Before funding, use a deliberate zero-cost prototype stack and establish a coherent art target rather than waiting for final assets.
5. **Immediate budget:** essentially zero through the one-month prototype. Budget bands after that must be proposed against evidence and fundraising needs.
6. **Human capacity:** owner plus one collaborating company CFO/game designer, who is primarily responsible for a separate strategy game but can collaborate on systems design and review. Do not plan as if a five-person specialist team exists.
7. **Commercial gate:** produce something marketable and investor-facing earlier than six months. Six months is a launch-capable candidate followed by a launch/no-launch decision, not an unconditional release date.
8. **Faction/town breadth:** owner values varied mechanics and different town/base types. The two-deep-versus-four-shallow decision remains unresolved; design should preserve four differentiated faction/town contracts without forcing premature full production.
9. **Editor:** reliable internal scenario tool first; player-facing usability follows. Custom scenarios must be playable, and a scenario editor remains a product goal.
10. **Campaign:** a three-scenario first arc is acceptable, alongside custom-scenario play.
11. **Reference targets:** Heroes of Might and Magic III and Olden Era; XCOM: Enemy Unknown/Within; Harebrained Schemes' Shadowrun Returns series. Additional references should be researched by specific design problem rather than copied wholesale.
12. **Platform/input:** Windows mouse and keyboard is sufficient for the first product.
13. **Testing:** more humans can be brought into the loop, although exact tester counts are not committed.

### Remaining blocking questions

Resolved 2026-07-12:

1. **Async multiplayer:** may probably move after the first Early Access launch if it threatens single-player, editor, or campaign quality. Treat this as a product-risk valve rather than launch-critical scope.
2. **One-month marketing proof:** capture all four — strategic exploration, base construction, tactical combat, and a Feed/narrative moment.
3. **Campaign viewpoints:** scenarios may use different faction viewpoints. Both HRC and QXZ remain playable, but every scenario need not offer a side-selection variant. Specific campaign content can be authored later.
4. **Base-building cadence:** one construction decision per base per strategic day/cycle. Routine construction does not require Champion presence; presence may later enable bonuses or special projects.

Additional reference direction: Civilization V is a primary inspiration for UI feel — calm, map-first, authoritative, tactile, readable, and strategically dense without looking like a debug dashboard.

## Recommended immediate authorization

Approve a short **Production Definition and Player Shell Reset**, not the entire 24-week ledger as automatic implementation authority.

Its first outputs should be:

1. approved Product Constitution;
2. fresh human baseline playtest;
3. asset/audiovisual integration spike and sourcing decision;
4. campaign spine and HRC/QXZ faction contracts;
5. UI shell architecture spike with decomposition boundaries;
6. one READY implementation story for the normal player shell;
7. a revised capability dashboard using the gates in this document.

## Final recommendation

Continue the project. The concept is worth making and the technical base is stronger than the current visual build suggests.

Do not continue by adding more systems to the existing debug-shaped surface. The next phase must turn the project from a tested mechanics laboratory into a game people can understand, desire, and emotionally remember.

The quality strategy is:

- approve the north star;
- simplify the first playable contract;
- establish the visual/audio target immediately;
- rebuild the player shell without discarding the tested domain core;
- prove strategic fun and tactical clarity;
- integrate only the strongest Neon Champions differentiators;
- use human playtests as the weekly steering mechanism;
- scale content and product breadth only after measured throughput;
- treat release as an evidence gate, not a calendar promise.
