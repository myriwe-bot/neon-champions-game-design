# Neon Champions Game Design Log

> Append-only project log.

## [2026-05-22] create | Initialize game design repository

- Created private production-facing design repo scaffold under `/root/wiki/neon-champions-game-design`.
- Established separation between worldbuilding wiki and game design source of truth.
- Added concept, systems, world-import, gate, epic, story, architecture, and workflow templates.


## [2026-05-22] revise | Greenland / Blue Week concept draft

- Rewrote `design/gdd/game-concept.md` around the leading direction: a HoMM3-inspired cyberpunk strategy/RPG with the initial campaign in Greenland during Blue Week.
- Rewrote `design/gdd/game-pillars.md` with falsifiable pillars and anti-pillars: dirty information, infrastructure power, Champions as legitimacy, factions as evolutionary philosophies, wilderness without escapism, and Intel as secrets turned into power.
- Updated `index.md` concept links.
- Approval remains pending; these are strong draft foundations, not final production requirements.


## [2026-05-22] revise | Intel resource and tactical combat decisions

- Created `design/gdd/intel-resource.md` as a draft GDD translating Olden Era Alchemical Dust into Neon Champions Intel.
- Updated `design/gdd/game-concept.md` with current decisions: Blue Week is both summit and sky-break event; DPD / the Blue / the Blues is the UNP Net-security body; full tactical battles are in MVP scope.
- Updated `design/gdd/systems-index.md` with Intel Resource and Tactical Combat as MVP systems.
- Updated `index.md`.


## [2026-05-22] add | Faction unit rosters

- Created `design/gdd/faction-unit-rosters.md` with draft tactical identities and unit lines for Greenland campaign factions.
- Updated `design/gdd/systems-index.md` and `index.md`.


## [2026-05-25] revise | Workflow source-of-truth and audit model

- Expanded `design/workflow.md` with the approved four-layer source-of-truth model: worldbuilding, game design, technical, and production truth.
- Added support/evidence categories for prototypes, asset/content pipeline rules, references/legal/cultural constraints, chat/memory/agent output, and Git/GitHub audit trail.
- Made omissions explicit as a PR requirement: implementation changes must state known omissions, stubs, mocks, assumptions, deferred work, or `No known omissions`.
- Added conflict rules: approved docs authorize work, Git/GitHub proves what happened, and divergence is a defect until reviewed.


## [2026-05-25] revise | Ambiguity check and implementation authorization gate

- Added an explicit Implementation Authorization Gate to `design/workflow.md`.
- Defined the ambiguity check as a required pre-implementation review: agents may not implement stories that require guessing design, technical, UX/content, scope, or canon/lore decisions.
- Added required story-field template for ambiguity status, open questions, assumptions, out-of-scope items, allowed stubs/mocks, and human-approved exceptions.


## [2026-05-25] revise | Story readiness standard

- Added Story Readiness Standard and Story DONE Standard to `design/workflow.md`.
- Rewrote `production/stories/story-template.md` to require exact source references, bounded scope, out-of-scope declarations, ambiguity check, verification requirements, branch/PR traceability, omissions disclosure, READY gate, and DONE gate.


## [2026-05-25] revise | Epic standard

- Added Epic Standard, Epic Readiness Gate, Epic DONE Standard, and Epic Anti-Patterns to `design/workflow.md`.
- Rewrote `production/epics/epic-template.md` to make epics capability containers rather than implementation tickets.
- Documented the hard rule that agents and Codex may not implement epics directly; only READY child stories authorize implementation.


## [2026-05-27] revise | Control manifest standard

- Added Control Manifest Standard to `design/workflow.md`.
- Rewrote `docs/architecture/control-manifest.md` as the stricter Codex / agent implementation rulebook.
- Manifest now defines implementation authority, source reading order, Unity blockers, architecture boundaries, data/tuning rules, verification requirements, scope control, documentation duties, Git/GitHub rules, and stop conditions.
- Production Unity implementation remains blocked until READY stories reference approved GDDs and approved technical rules.


## [2026-05-27] add | Unity technical scheme skeleton

- Created `docs/architecture/unity-technical-scheme.md` as the approved skeleton for Unity implementation boundaries.
- Established direction: testable C# domain logic, Unity as presentation/orchestration, data-driven definitions, explicit assembly boundaries, thin scenes, prefab constraints, and strict prototype-vs-production separation.
- Recorded open technical decisions: exact Unity LTS version, render pipeline, 2D/2.5D/3D presentation model, final data-authoring balance, save/load, input system, and CI/build setup.
- Updated `docs/architecture/architecture.md`, `docs/architecture/control-manifest.md`, and `design/workflow.md` to reference the Unity scheme.


## [2026-05-27] revise | Technical decision priorities and data authoring options

- Created `docs/architecture/technical-decision-priorities.md`.
- Recorded approved defaults: Unity 6.4 target `6000.4.8f1` if available, 2.5D presentation, URP, Unity Input System, default folder/assembly scheme, early-but-not-first-prototype save/load, serializable runtime state, and localization from the start.
- Created `docs/architecture/data-authoring-options.md` with four options: Unity-first ScriptableObjects, external data first, external canonical data with Unity authoring adapters, and phased hybrid.
- Approved Option D: phased hybrid, because it preserves prototype speed while protecting future map editors, scenario tools, balancers, datapacks, and modloaders.
- Expanded testing direction to require at least domain automated tests, data/schema validation, Unity integration/smoke evidence, and manual visual/UX evidence where needed.
- Explained CI/build setup as a later GitHub automated check layer, required before production PR-based implementation but not before local prototypes.


## [2026-05-27] approve | Strict testing strategy

- Created `docs/architecture/testing-strategy.md` as an approved technical-setup ADR.
- Approved strict layered testing: domain/EditMode tests, data/content/localization validators, Unity PlayMode/smoke coverage, UX/visual/feel evidence, and per-story evidence packages.
- Approved the stricter Unity integration stance: automated PlayMode coverage is the target wherever feasible; manual Unity evidence is supplemental or a documented temporary exception.
- Required TDD for production gameplay logic and bug fixes unless a human-approved exception is documented.
- Updated `docs/architecture/architecture.md`, `docs/architecture/unity-technical-scheme.md`, `docs/architecture/control-manifest.md`, `production/stories/story-template.md`, and `production/epics/epic-template.md` to reference the approved testing strategy.


## [2026-05-27] approve | Strict CI / build automation

- Created `docs/architecture/ci-build-automation.md` as an approved technical-setup ADR.
- Approved GitHub Actions as the default CI provider.
- Approved strict timing: CI is required immediately after Unity project creation, including spike PRs.
- Production PRs require merge-blocking automated checks unless a human-approved exception is documented.
- Updated architecture, technical priorities, Unity scheme, control manifest, story template, epic template, and testing strategy references.


## [2026-05-27] approve | SPIKE-001 Unity project and CI foundation

- Created `production/spikes/spike-001-unity-project-ci-foundation.md` as the approved first Unity spike.
- Defined the spike as technical foundation work only: Unity version confirmation, URP project setup, folder/assembly scaffold, smoke tests, validator stub/path, and CI scaffold.
- Explicitly excluded gameplay implementation, save/load, final data schemas, localization package choice, grid/camera/tile decisions, and production gameplay code.
- Updated `docs/architecture/technical-decision-priorities.md` to reference the approved spike and its conditions.


## [2026-05-27] approve | Codex and multi-agent operating instructions

- Researched current Codex AGENTS.md behavior, Codex sandbox/non-interactive/worktree guidance, Git worktrees, GitHub Copilot coding-agent guidance, and Claude Code multi-agent practices.
- Created root `AGENTS.md` for the game design repo to prevent agents from confusing design/control work with Unity implementation.
- Created `docs/architecture/codex-agent-instructions.md` as the approved Codex/AGENTS.md strategy.
- Created `docs/architecture/unity-repo-agents-template.md` as the approved starting template for future Unity repo root/scoped AGENTS.md files.
- Created `docs/architecture/multi-agent-operating-model.md` to define human/design/architecture/coordinator/implementation/QA/review agent roles, gates, worktree isolation, and evidence rules.
- Created `production/checklists/codex-pr-review-checklist.md` for future implementation PR review.
- Updated `SCHEMA.md`, `index.md`, architecture docs, story/epic templates, and SPIKE-001 to include agent instruction scopes and AGENTS.md requirements.

## [2026-05-28] approve | SPIKE-001 source authority cleanup

- Approved `docs/architecture/control-manifest.md` as the technical-setup implementation control manifest.
- Approved `docs/architecture/unity-technical-scheme.md` for SPIKE-001 foundation scaffold and technical setup boundaries.
- Kept unresolved production architecture decisions explicit as later blockers: concrete data schemas/tooling, save/load format/versioning, localization implementation layer, and exact CI runner/license/cache/artifact policy.
- Clarified that approval does not authorize production gameplay; Unity implementation still requires an approved spike or READY story with evidence.

## [2026-05-29] revise | Tactical combat GDD and MVP faction pair

- Expanded `design/gdd/tactical-combat.md` with the latest F.67-F.92 tactical packet work: AP limits, tactical MVP scope, implementation contracts, ability/effect schema, status schema, information model, objective schema, save/replay contracts, MVP content matrix, and Barents unit roster packets.
- Selected the first working canonical MVP faction pair as Barents Research Group / Polar Certification Combine versus Janus-Kestrel Continuity Group / Mining-Logistics Consortium.
- Added `design/gdd/tactical-combat.md` to the public index so the GDD is visible from the game-design site.

## [2026-05-30] revise | Tactical combat readability pass

- Reworked `design/gdd/tactical-combat.md` from a long packet transcript into a concise first-read GDD for humans and LLM agents.
- Preserved the previous long-form tactical packet history in `design/research/tactical-combat-deep-reference.md` as reference material, not the primary implementation contract.
- Added `design/gdd/README.md` as a GDD reading guide with explicit LLM rules, reading order, and active GDD expectations.
- Updated `design/gdd/systems-index.md` and `index.md` to point readers to the concise tactical GDD and deep reference split.

## [2026-05-30] revise | Tactical combat split-article preservation pass

- Split the preserved tactical-combat design-session material into smaller readable articles under `design/gdd/tactical-combat/`.
- Added `design/gdd/tactical-combat/section-map.md` to verify that every original top-level tactical-combat section is mapped to a split article.
- Kept `design/research/tactical-combat-deep-reference.md` as the raw backup while making the split articles the readable detailed layer.
- Updated `design/gdd/tactical-combat.md`, `design/gdd/README.md`, and `index.md` so humans and LLM agents can find both the concise overview and the preserved detailed material.

## [2026-05-30] fix | Design wiki interlink and legacy cleanup

- Added tactical-combat split articles directly to `index.md` so durable detailed GDD artifacts are visible from the main wiki index.
- Corrected active concept/pillar wording from Blue Week-as-initial-event toward the current Blue Monday initial event with Blue Week as later/retrospective framing.
- Fixed malformed open-question table rows in `design/gdd/game-concept.md`.
- Updated `design/gdd/systems-index.md` status/deferred wording so it no longer implies stale concept-approval blocking.
- Updated `SCHEMA.md` to recognize `research-note`, matching existing research artifacts.

## [2026-05-30] fix | Faction roster metadata and Blue Monday naming

- Normalized `design/gdd/faction-unit-rosters.md` frontmatter to the repository schema.
- Updated active faction-roster naming from Open Sky / Blue Week Cells to Open Sky / Blue Monday Cells while preserving Blue Week as later public framing.
- Updated Intel resource source-lore tags to include Blue Monday alongside Blue Week.

## [2026-05-30] add | Strategic map hotseat MVP direction

- Created `design/gdd/strategic-map.md` as the strategic-map MVP GDD entry point.
- Recorded the approved MVP direction as C3-H: two-faction local hotseat strategy, avoiding strategic AI while keeping a real opposing Champion/faction on the map.
- Recorded the first scenario shape as B1 duel map with B2 race-map pacing: two starting hubs, neutral sites, guarded resource sites, recruitment/reinforcement points, and a central contested objective.
- Updated `design/gdd/systems-index.md`, `design/gdd/README.md`, and `index.md` so the strategic map is discoverable before future implementation-story work.

## [2026-05-30] approve | Strategic map topology packet

- Recorded Packet C in `design/gdd/strategic-map.md`: use a C/D hybrid topology for MVP.
- Approved an authored node-route graph as the gameplay rules model, presented over a visual Greenland map.
- Required stable node/route/map IDs, presentation coordinates separate from domain graph rules, and an abstract enough model to allow richer tile/grid/region topology later.
- Deferred strategic tile movement, freeform pathfinding, procedural map generation, route construction/destruction, and final map editor format.

## [2026-05-30] approve | Strategic site model packet

- Recorded Packet D in `design/gdd/strategic-map.md`: use a hybrid site model with HoMM-like mechanical categories and Neon-flavored infrastructure themes.
- Defined MVP mechanical categories: Start Hub, Resource Site, Recruitment Site, Upgrade/Intel Site, Neutral Guard Site, Central Objective, and One-Shot Visit Site.
- Defined MVP theme types including mining/extraction, fishery/cold-chain, sensor/White Sky node, clinic/bodytech, recruitment contractor/local ally, Treaty-Net infrastructure, cache/salvage/black site, and starting hub.
- Recorded reusable site state and ownership/control draft rules while deferring full town trees, deep infrastructure simulation, diplomacy/consent mechanics, complex provenance ownership, and full fog/feed misinformation.

## [2026-05-30] approve | Strategic resource model packet

- Recorded Packet E in `design/gdd/strategic-map.md`: use a phased hybrid resource model for MVP.
- Approved active MVP stockpiles: Credits, Materials, and Intel.
- Kept Compute, Medical Capacity, Energy, Legitimacy, Favors, and White Sky Access as future-facing flavor/tags rather than separate MVP stockpiles.
- Defined one-time and recurring reward support, with first implementation allowed to start from one-time rewards if turn-income timing is not yet implemented.
- Defined recruitment/reinforcement as predefined offers with fixed costs/stock, while deferring full town trees, dynamic pricing, supply chains, upkeep, and deep Intel operation systems.

## [2026-05-30] approve | Strategic Champion movement packet

- Recorded Packet F in `design/gdd/strategic-map.md`: use a phased hybrid Champion/army movement model.
- Approved HoMM-lite MVP rules: one Champion per faction, node-route movement points, one attached army, one major strategic interaction per turn, and explicit movement/site-interaction commands.
- Required the data model to support later richer logistics such as route types, weather, supply, fatigue, faction movement modifiers, and movement-type differences without implementing them now.
- Defined minimum Champion, army, movement command, site interaction command, and battle-result army-delta concepts for future implementation stories.
- Deferred multiple Champions, freeform/tile movement, caravans/reserves, garrison management, Champion progression/equipment, supply/fatigue/weather, complex defeat handling, and strategic AI movement planning.

## [2026-05-30] approve | Strategic turn and victory packet

- Recorded Packet G in `design/gdd/strategic-map.md`: use a phased hybrid turn/scenario/victory structure.
- Approved objective-duel MVP rules: fixed two-faction local hotseat turn order, deterministic start/end turn phases, start-of-turn refresh/income, and manual end turn baseline.
- Approved MVP victory conditions: defeat the enemy only-Champion faction, or hold the central objective for a scenario-defined number of own start-of-turn checks; working default is 2 consecutive own turns.
- Required scenario state to track active faction, turn/round counters, objective hold state, victory state, and defeat state while remaining ready for later score/race modes.
- Deferred online/simultaneous turns, strategic AI, diplomacy, more than two factions, active score/turn-limit victory, multiple objectives, campaign persistence, complex Champion recovery, hidden victory conditions, and crisis-clock systems.

## [2026-05-30] approve | Strategic DTO boundary packet

- Recorded Packet H in `design/gdd/strategic-map.md`: use explicit strategy-to-tactical boundary DTOs for MVP.
- Approved `BattleSetup` as the strategy-owned setup snapshot carrying battle/source/site/node/faction/controller/army/objective/reward-context references.
- Approved `BattleResult` as the tactical-owned outcome payload carrying winner/outcome, survivors/losses, defeated flags, optional retreat/cancel state, summary, result flags, and diagnostics.
- Locked the boundary rule: tactical combat resolves battles, but strategy applies site ownership, rewards, resources, objective progress, Champion defeat, turn, and victory consequences.
- Added minimum strategic-loop test cases for guarded sites, site contests, reward gating, Champion defeat victory, and no pre-result mutation.

## [2026-05-30] draft | STORY-STRAT-001 scenario map graph state

- Created `production/stories/story-strat-001-scenario-map-graph-state.md` as the first READY-candidate strategic MVP implementation story.
- Scope covers pure strategic scenario/map graph definitions, runtime initialization state, MVP validation rules, test-local sample data allowance, and EditMode/data validation evidence.
- Story remains Draft pending human approval and parent epic handling before it can be marked READY.

## [2026-05-30] publish | Add STORY-STRAT-001 to site index

- Added `production/stories/story-strat-001-scenario-map-graph-state.md` to `index.md` so the generated game-design website exposes the new READY-candidate story directly from Production Planning.

## [2026-06-01] approve | STORY-STRAT-001 and parent strategic MVP epic

- Created `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md` as the approved parent epic for the first strategic MVP core loop.
- Recorded human approval for `production/stories/story-strat-001-scenario-map-graph-state.md` and marked it READY.
- Cleared the parent-epic READY blocker; remaining implementation discovery is limited to Unity repo source/test paths, branch/PR setup, and assembly layout.
- Updated `index.md` so the epic and READY story are visible from Production Planning.

## [2026-06-01] draft | Merge-to-main gate workflow

- Created `docs/architecture/merge-to-main-gate.md` as an in-review workflow for rigorous PR merge gates before implementation branches land on `main`.
- Defined gate checks for branch hygiene, source authority, scope compliance, architecture/Unity asset safety, TDD evidence, local verification, CI/branch protection, independent review, documentation sync, and final merge decision.
- Added a standard gate verdict template and exception policy requiring human approval for merge-blocking exceptions.
- Updated `index.md` so the workflow is visible from Architecture.
