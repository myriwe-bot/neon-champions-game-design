# Neon Champions Game Design Log

> Append-only project log.

## [2026-06-24] approve | Promote STORY-QA-009 for implementation

- Promoted `STORY-QA-009 EPIC-008 Playtest and Closeout Review` to READY / approved after human approval.
- Recorded approved scope: closeout-first review; allow only tiny QA/evidence/test polish if needed, no new gameplay; Codex may recommend `CLOSE EPIC`, `ONE NARROW FOLLOW-UP`, or `REJECT CLOSEOUT`; next-epic options are decision options only.
- Converted `production/sprints/codex-story-qa-009.prompt.txt` from guarded candidate to runnable implementation handoff.
- Updated EPIC-008, the EPIC-008 plan, and run-prompt index.

## [2026-06-19] merge | STORY-ARMY-004 and prepare QA-009 candidate

- Marked `STORY-ARMY-004 Composition Consequence Scenario` DONE / merged after Unity PR #67 and post-merge Unity Foundation CI passed.
- Added `STORY-QA-009 EPIC-008 Playtest and Closeout Review` as a READY-candidate / approval-pending closeout packet.
- Added guarded `production/sprints/codex-story-qa-009.prompt.txt`; it self-blocks until human approval promotes QA-009 to READY.
- Updated EPIC-008, the EPIC-008 plan, run-prompt index, and production index.
- Updated Unity README current-task pointer via PR #68, merged as `4568e08bc36843e01b25acc9e3bde462c84de512`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27837997087

## [2026-06-19] approve | Promote STORY-ARMY-004 for implementation

- Promoted `STORY-ARMY-004 Composition Consequence Scenario` to READY / approved after human approval.
- Recorded approved defaults: narrow Home Rule `settlement_watch` proof first; visible setup/label/loss-summary difference instead of guaranteed win/loss tuning; adapt existing guarded-site path if small, otherwise create one story-scoped composition-demo guarded site; defer mirrored QXZ proof to QA/closeout unless trivial.
- Converted `production/sprints/codex-story-army-004.prompt.txt` from guarded candidate to runnable implementation handoff.
- Updated EPIC-008, the EPIC-008 plan, run-prompt index, and production index.
- Updated Unity README current-task pointer via PR #66, merged as `85c3ff35bb91ed4ee9043fcd8d9465eb4588a715`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27833694023

## [2026-06-19] merge | STORY-ARMY-003 and prepare ARMY-004 candidate

- Marked `STORY-ARMY-003 Fixed Recruitment Offers and Army Summary` DONE / merged after Unity PR #64 and post-merge Unity Foundation CI passed.
- Added `STORY-ARMY-004 Composition Consequence Scenario` as a READY-candidate / approval-pending packet.
- Added guarded `production/sprints/codex-story-army-004.prompt.txt`; it self-blocks until human approval promotes ARMY-004 to READY.
- Updated EPIC-008, the EPIC-008 plan, run-prompt index, and production index.
- Updated Unity README current-task pointer via PR #65, merged as `bf0b72e0f441a2fe13430e6b01ddb1c98d5ef0fc`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27831766110

## [2026-06-19] approve | Promote STORY-ARMY-003 for implementation

- Promoted `STORY-ARMY-003 Fixed Recruitment Offers and Army Summary` to READY / approved after human approval.
- Recorded approved defaults: Home Rule hub offers `settlement_watch`, QXZ hub offers `meridian_security`, neutral site attempts `survey_drones` only if small, claims are one-time consumed, and stack counts use MVP defaults unless evidence documents a readability exception.
- Updated the Codex prompt and run-prompt index for runnable implementation handoff.
- Updated the Unity repo current-task pointer via Unity PR #63; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27824663511

## [2026-06-19] merge | STORY-ARMY-002 and prepare ARMY-003 candidate

- Marked `STORY-ARMY-002 Tactical Role Behaviors and Sensor Lock` DONE / merged after Unity PR #61 and post-merge Unity Foundation CI passed.
- Added `STORY-ARMY-003 Fixed Recruitment Offers and Army Summary` as a READY-candidate / approval-pending packet.
- Added guarded `production/sprints/codex-story-army-003.prompt.txt`; it self-blocks until human approval promotes ARMY-003 to READY.
- Updated EPIC-008, the EPIC-008 plan, run-prompt index, and production index.
- Cleared the Unity repo current-task pointer via Unity PR #62; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27822509900

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

## [2026-06-01] approve | Merge-to-main gate workflow

- Recorded human approval for `docs/architecture/merge-to-main-gate.md`.
- Marked the merge-to-main gate as an approved, binding workflow for Unity implementation branches landing on `main`.
- Updated `index.md` to show the workflow as approved.

## [2026-06-02] plan | Strategic MVP story train 001

- Created `production/stories/story-strat-002-hotseat-turn-ownership.md` as a READY-candidate domain story for deterministic local-hotseat turn ownership.
- Created `production/stories/story-strat-003-champion-route-movement.md` as a READY-candidate domain story for single-route Champion movement over authored graph routes.
- Created `production/stories/story-tac-001-battle-setup-result-dto-contracts.md` as a READY-candidate contract story for strategy-to-tactics DTOs.
- Created `production/sprints/strategic-mvp-story-train-001.md` to sequence Codex implementation one approved story/branch/PR at a time.
- Updated `production/epics/epic-strat-mvp-001-strategic-mvp-core-loop.md` and `index.md` with the new story train.
- Approval remains pending; the new stories are not READY for implementation until human approval is recorded.

## [2026-06-02] approve | Strategic MVP Codex story train READY

- Added estimates and marked READY/approved: STORY-STRAT-002, STORY-STRAT-003, STORY-STRAT-VIS-001, STORY-STRAT-INPUT-001, STORY-STRAT-UI-001, and STORY-LOOP-001.
- Clarified STORY-TAC-001 authority: strategic-map §14 is binding; draft tactical-combat docs are compatibility-only and must not expand/block the DTO minimum unless they contradict §14.
- Approved `production/sprints/strategic-mvp-story-train-001.md` and created `production/sprints/strategic-mvp-codex-execution-system.md` with Codex queue, preflight, prompt wrappers, PR evidence template, and merge/continue rule.
- Updated `index.md` with the newly READY story links and Codex execution system.

## [2026-06-02] add | Strategic MVP Codex run prompts

- Created `production/sprints/strategic-mvp-codex-run-prompts.md` with exact Windows PowerShell commands for Codex.
- Added preferred single-story prompt for STORY-STRAT-002 and optional two-story logic batch prompt for STORY-STRAT-002 plus STORY-STRAT-003.
- Updated `index.md` with the run-prompt document.

## [2026-06-02] revise | Copy-safe Codex prompt files

- Added `production/sprints/codex-story-strat-002.prompt.txt` and `production/sprints/codex-strat-002-003-batch.prompt.txt` so PowerShell can pass prompts via `Get-Content -Raw` without here-string continuation prompts.
- Updated `production/sprints/strategic-mvp-codex-run-prompts.md` with copy-safe prompt-file commands.

## [2026-06-04] approve | Strategic MVP closeout train and STORY-STRAT-004

- Recorded human approval for `production/sprints/strategic-mvp-closeout-story-train-002.md`.
- Promoted `production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger.md` from READY-candidate to READY with approved defaults for pending battle record, major-interaction spend, and neutral guard CombatAI controller metadata.
- Added `production/sprints/codex-story-strat-004.prompt.txt` as the copy-safe Codex prompt for the first closeout implementation story.
- Updated Codex run prompts, epic traceability, and index discoverability.


## [2026-06-04] approve | STORY-TAC-002 implementation packet

- Recorded human approval for `production/stories/story-tac-002-minimal-hex-board-and-stack-placement.md`.
- Promoted STORY-TAC-002 from READY-candidate to READY with approved assumptions: tiny fixed hex board, exactly one attacker stack, exactly one neutral guard stack, and domain/test focus unless safe placeholder visual proof is needed.
- Added `production/sprints/codex-story-tac-002.prompt.txt` as the copy-safe Codex implementation prompt.
- Updated closeout train, epic traceability, run prompts, and index discoverability.


## [2026-06-04] fix | STORY-TAC-002 source-authority blocker

- Resolved Codex source-authority stop condition for STORY-TAC-002.
- Promoted `design/gdd/tactical-combat.md` and `design/gdd/tactical-combat/overview-and-scope.md` from stale draft/pending front matter to approved source status for MVP tactical-combat implementation planning.
- Added a STORY-TAC-002 source-authority reconciliation note clarifying that approval authorizes only the story-scoped sections and does not expand implementation scope into broader tactical systems.
- Updated the TAC-002 Codex prompt to tell implementers to pull the design repo if stale local front matter is still visible.

## [2026-06-04] approve | STORY-TAC-VIS-001 implementation packet

- Recorded human approval for `production/stories/story-tac-vis-001-minimal-tactical-board-presentation-and-handoff-switch.md`.
- Promoted STORY-TAC-VIS-001 from READY-candidate to READY with approved assumptions: crude placeholder tactical board, visible guarded-site handoff/switch, attacker/neutral guard stack markers, tactical-mode status labels, no battle result or strategic mutation.
- Confirmed linked GDD/ADR/control sources are approved for the narrow visual handoff scope.
- Updated closeout train, epic traceability, run prompts, prompt guard, and index discoverability.

## [2026-06-04] approve | STORY-TAC-004 implementation packet

- Recorded human approval for `production/stories/story-tac-004-minimal-battle-end-and-result-return.md`.
- Promoted STORY-TAC-004 from READY-candidate to READY with approved assumptions: attacker-win/defender-win only, retreat/draw/cancel/rout deferred, and no strategic result application inside tactical result creation.
- Confirmed linked GDD/ADR/control sources are approved for the narrow battle-end/BattleResult-return scope.
- Added `production/sprints/codex-story-tac-004.prompt.txt` as the copy-safe Codex implementation prompt.
- Updated closeout train, epic traceability, run prompts, and index discoverability.


## [2026-06-04] approve | STORY-TAC-005 tactical player controls

- Marked `STORY-LOOP-002` DONE / merged after Unity PR #19 and post-merge main CI passed.
- Recorded human review note that the current tactical view is not yet usable enough because it lacks basic movement/pass-style controls.
- Marked `EPIC-STRAT-MVP-001` implemented for the first guarded-site capture loop and moved tactical usability follow-up into `EPIC-VSLICE-MVP-002`.
- Approved `EPIC-VSLICE-MVP-002` for the next production packet and created READY story `STORY-TAC-005 Basic Tactical Player Controls`.
- Created checked-in Codex prompt `production/sprints/codex-story-tac-005.prompt.txt` and updated run-prompt instructions.

## [2026-06-05] close | STORY-TAC-005 merged and MAP-001 drafted

- Marked `STORY-TAC-005 Basic Tactical Player Controls` DONE / merged after Unity PR #20 squash-merged as `4bd753cfbb861a49f96daf90378a674d27be5d4f`.
- Recorded final PR-head CI and post-merge main verification evidence; post-merge push run was replaced by workflow-dispatch verification run `27016431640`, which passed Compile, EditMode, Placeholder Validator, and PlayMode.
- Updated `EPIC-VSLICE-MVP-002`, closeout train, index, and run-prompt instructions so no stale TAC-005 implementation prompt is presented as current.
- Drafted `production/stories/story-map-001-larger-two-base-strategic-map-slice.md` as the next candidate; it remains draft/pending with ambiguity questions and is not READY until human approval.

## 2026-06-05 — STORY-MAP-001 ambiguity resolved

- Updated `production/stories/story-map-001-larger-two-base-strategic-map-slice.md` to READY-candidate after user decisions: central objective gets a minimal non-victory interaction, base/hub is a real minimal site type, and PlayMode smoke must prove two possible guarded neutral choices.
- Updated epic, story train, run prompts, and index traceability. `STORY-MAP-001` remains approval-pending and must not be implemented until explicitly promoted to READY.


## [2026-06-08] approve | STORY-MAP-001 implementation packet

- Recorded explicit human implementation approval for `production/stories/story-map-001-larger-two-base-strategic-map-slice.md`.
- Promoted STORY-MAP-001 from READY-candidate to READY with approved scope: larger deterministic two-base map, real minimal base/hub site type, minimal non-victory central objective interaction, and two guarded neutral choices in PlayMode smoke.
- Added `production/sprints/codex-story-map-001.prompt.txt` as the copy-safe Codex implementation prompt.
- Updated `EPIC-VSLICE-MVP-002`, closeout train, run prompts, and index discoverability.


## [2026-06-08] close | STORY-MAP-001 merged and STRAT-006 drafted

- Marked `STORY-MAP-001 Larger Two-Base Strategic Map Slice` DONE / merged after Unity PR #21 squash-merged as `6e3e5efdda81d46b4b2080ba0a9c06c2f356d2f6`.
- Recorded merge-gate fix commit `49ad163a52cb7921df7e15cab0770b7a3d5bf44e`: stale evidence CI text removed and central-objective interaction validation tightened to the authored runtime objective ID.
- Recorded final PR-head CI and post-merge main CI run `27127890489`, which passed Compile, EditMode, Placeholder Validator, and PlayMode.
- Drafted `production/stories/story-strat-006-simple-recruitment-site-fixed-offer.md` as the next candidate; it remains READY-candidate / approval pending with ambiguity questions before implementation.
- Updated `EPIC-VSLICE-MVP-002`, run prompts, and index traceability.


## [2026-06-08] approve | STORY-STRAT-006 implementation packet

- Recorded human approval for `production/stories/story-strat-006-simple-recruitment-site-fixed-offer.md`.
- Promoted STORY-STRAT-006 from READY-candidate to READY with approved scope: one unguarded dwelling/recruitment site, two player-choice fixed offers, normal costing Credits only, upgraded costing Credits + Materials, and both adding new placeholder stacks.
- Added `production/sprints/codex-story-strat-006.prompt.txt` as the copy-safe Codex implementation prompt with workspace-write and danger-full-access command variants.
- Updated `EPIC-VSLICE-MVP-002`, run prompts, and index discoverability.

## [2026-06-09] done | STORY-STRAT-006 merge and LOOP-003 prep

- Marked `STORY-STRAT-006 Simple Recruitment Site and Fixed Offers` DONE / merged after Unity PR #22 squash-merged as `a699055d67087821a5e6fdcb0f2e84c7d5891b28`.
- Recorded post-merge Unity `main` CI success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests.
- Drafted `production/stories/story-loop-003-larger-map-recruitment-and-neutral-capture-vertical-slice.md` as the next READY-candidate / approval pending connected-smoke packet.
- Added guarded prompt file `production/sprints/codex-story-loop-003.prompt.txt`; it explicitly stops unless STORY-LOOP-003 is promoted to READY/approved.
- Updated `EPIC-VSLICE-MVP-002`, run prompts, and index traceability.

## [2026-06-09] approve | STORY-LOOP-003 implementation packet

- Recorded human approval for `production/stories/story-loop-003-larger-map-recruitment-and-neutral-capture-vertical-slice.md`.
- Promoted STORY-LOOP-003 from READY-candidate to READY with approved scope: connected larger-map smoke from recruitment preview/apply through guarded-site tactical handoff, tactical resolution, BattleResult return, and strategic capture feedback.
- Recorded approved scope valve: Codex may fix one small usability/readability blocker only if necessary for judging the connected loop; otherwise no usability fix should be added.
- Updated `production/sprints/codex-story-loop-003.prompt.txt` as the active checked-in Codex implementation prompt.
- Updated `EPIC-VSLICE-MVP-002`, run prompts, and index discoverability.

## [2026-06-09] blocked | STORY-LOOP-003 tactical setup prerequisite

- Recorded Codex's correct STORY-LOOP-003 stop condition: recruited two-stack attacker army hits `tactical-board-unsupported-stack-count` because current STORY-TAC-002 tactical board setup supports exactly one attacker stack.
- Marked `STORY-LOOP-003` BLOCKED until multi-stack attacker tactical setup lands; explicitly preserved the rule not to hide, merge, bench, or ignore the recruited stack.
- Created and approved `production/stories/story-tac-006-multi-stack-attacker-tactical-setup.md` as the narrow prerequisite implementation packet.
- Updated `EPIC-VSLICE-MVP-002`, run prompts, and index traceability.

## [2026-06-09] done | STORY-TAC-006 merge and LOOP-003 retry prep

- Marked `STORY-TAC-006 Multi-Stack Attacker Tactical Setup` DONE / merged after Unity PR #23 squash-merged as `ca41ca3d4d0f3ccfac3fc31b154cb19eeffbe8ee`.
- Recorded post-merge Unity `main` CI success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests.
- Promoted `STORY-LOOP-003 Larger Map Recruitment and Neutral Capture Vertical Slice` back to READY after TAC-006 verified recruited two-stack attacker tactical setup.
- Repointed `production/sprints/strategic-mvp-codex-run-prompts.md` to the existing LOOP-003 prompt file.
- Updated `EPIC-VSLICE-MVP-002`, index, and story verdicts.

## [2026-06-09] done | STORY-LOOP-003 merge and QA-003 prep

- Marked `STORY-LOOP-003 Larger Map Recruitment and Neutral Capture Vertical Slice` DONE / merged after Unity PR #24 squash-merged as `2c0f64039f828d2b973ec4d1d10e8f25694f9361`.
- Recorded post-merge Unity `main` CI success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests.
- Drafted `STORY-QA-003 Loop Slice Visual Readability and Clickable Layout Pass` from human feedback that current BMP/layout evidence is hard to read and controls/views need clearer clickable scalable layout.
- Added guarded prompt file `production/sprints/codex-story-qa-003.prompt.txt`; it stops unless QA-003 is promoted to READY/approved.
- Updated `EPIC-VSLICE-MVP-002`, run prompts, index, and story verdicts.

## [2026-06-09] approve | STORY-QA-003 implementation packet

- Recorded human approval for `STORY-QA-003 Loop Slice Visual Readability and Clickable Layout Pass` and promoted it from READY-candidate / pending to READY / approved.
- Updated Ambiguity Check to PASS with the approved visual/readability/clickability scope.
- Activated `production/sprints/codex-story-qa-003.prompt.txt` by removing stale DO NOT RUN / approval-pending language while keeping the preflight check for READY/approved/PASS.
- Repointed `production/sprints/strategic-mvp-codex-run-prompts.md` to QA-003 as the current approved prompt.
- Updated `EPIC-VSLICE-MVP-002` and index traceability.

## [2026-06-10] draft | STORY-QA-004 playability map scale and UI clarity pass

- Recorded human closeout feedback after QA-003 and hotfix PR #26: the map is still tiny/unreadable, text labels overlap, buttons are obstructed by text, there is no zoom/focus, clicked objects are unclear, and button meanings are unclear.
- Drafted `production/stories/story-qa-004-playability-map-scale-zoom-and-ui-clarity-pass.md` as READY-candidate / approval pending.
- Updated `EPIC-VSLICE-MVP-002` verdict to CONCERNS / closeout blocked until QA-004 is approved/implemented/verified or the user explicitly accepts the current usability risk.
- Updated `production/sprints/strategic-mvp-codex-run-prompts.md` and `index.md` so no Unity implementation prompt is active for QA-004 before human approval.

## [2026-06-10] approve | STORY-QA-004 implementation packet

- Recorded human approval for `STORY-QA-004 Playability Map Scale, Zoom, and UI Clarity Pass` and promoted it from READY-candidate / pending to READY / approved.
- Updated Ambiguity Check to PASS with the approved scope: map scale/readability, zoom/focus, non-overlapping labels, unobstructed buttons, selected/clicked feedback, and tactical move/attack clarity.
- Added `production/sprints/codex-story-qa-004.prompt.txt` as the checked-in copy-safe Codex implementation prompt with workspace-write and danger-full-access command variants.
- Repointed `production/sprints/strategic-mvp-codex-run-prompts.md` to QA-004 as the current approved prompt.
- Updated `EPIC-VSLICE-MVP-002` and index traceability.

## [2026-06-10] blocked | STORY-QA-004 PR #27 readability remediation

- Recorded merge-gate verdict for Unity PR #27 as BLOCKED despite green CI because human review still reports blocker-level usability: BMP evidence is not useful, labels overlap, buttons are obstructed by text, guarded-site and Champion markers overlap, and the map remains hard to test.
- Added `production/sprints/codex-story-qa-004-remediation.prompt.txt` to direct remediation on the existing PR branch.
- Remediation direction: replace fragile world-space/debug action UI with a real uGUI Canvas using built-in layout groups, move controls/status/action lists out of map TextMesh clutter, fix guarded-site/Champion marker slots, make Focus actually center the selection, and produce PNG evidence that includes the actual tester UI.
- Updated `production/sprints/strategic-mvp-codex-run-prompts.md` to point at the remediation prompt and explicitly prohibit merging PR #27 before human visual review passes.

## [2026-06-10] done | STORY-QA-004 merge and epic closeout review

- Marked `STORY-QA-004 Playability Map Scale, Zoom, and UI Clarity Pass` DONE / merged after Unity PR #27 squash-merged as `d7661bf0e1fe7edca0704ac928994489e93ad337`.
- Recorded human visual acceptance before merge and post-merge Unity `main` CI success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests in run https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27278547989.
- Updated `EPIC-VSLICE-MVP-002`, run prompts, and index traceability; no next Unity implementation story is READY until the human chooses closeout or another follow-up direction.

## [2026-06-10] approve-candidate | EPIC-003 objective and tactical stakes packet

- Formally closed `EPIC-VSLICE-MVP-002` as DONE after user chose closeout option A and accepted the current visual state.
- Drafted `EPIC-VSLICE-MVP-003 Scenario Objective, Champion Combat, and Casualty Stakes` as an approved-candidate next epic.
- Recorded user direction: central guarded objective capture, allow Champion-vs-Champion combat as a later path, defender tiers named `weak / standard / strong`, and simple per-stack HP/strength persistence.
- Drafted `STORY-OBJ-001 Scenario Objective State and Victory Feedback` as READY-candidate only; later OBJ/TAC/LOOP stories remain Draft placeholders until promoted by explicit approval.
- Updated run prompts to state no Unity implementation story is currently READY.

## [2026-06-10] approve | STORY-OBJ-001 implementation prep

- Promoted `EPIC-VSLICE-MVP-003 Scenario Objective, Champion Combat, and Casualty Stakes` to approved.
- Promoted `STORY-OBJ-001 Scenario Objective State and Victory Feedback` to READY / approved after explicit human approval.
- Added checked-in Codex prompt `production/sprints/codex-story-obj-001.prompt.txt` and repointed `production/sprints/strategic-mvp-codex-run-prompts.md` to it.
- Adjacent EPIC-003 stories remain Draft and out of implementation scope: defender tiers, HP/strength persistence, Champion-vs-Champion encounter path, and connected objective/casualty smoke.

## [2026-06-11] merge-and-prepare | STORY-OBJ-001 closeout and OBJ-002 candidate

- Verified and merged Unity PR #28 for `STORY-OBJ-001 Scenario Objective State and Victory Feedback` after fixing merge-gate blockers.
- Recorded merge commit `69be356e2f0a4dbbb2d9cd1789b9c101dc1ab034` and post-merge main CI success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests.
- Marked `STORY-OBJ-001` DONE / merged and updated `EPIC-VSLICE-MVP-003` child status.
- Expanded `STORY-OBJ-002 Guarded Site Defender Strength Tiers` into a DRAFT / READY-candidate packet with approval pending; it is not implementation-authorizing yet.
- Added guarded prompt `production/sprints/codex-story-obj-002.prompt.txt` and repointed run prompts to stop until human approval promotes OBJ-002 to READY / approved.

## [2026-06-11] approval | STORY-OBJ-002 promoted to READY

- Human approved `STORY-OBJ-002 Guarded Site Defender Strength Tiers` as the next implementation story.
- Recorded approved scope: placeholder `weak` / `standard` / `strong` defender mappings, no final balance claims, central objective tier `standard` for now.
- Promoted story frontmatter to `status: ready` / `approval: approved`, Ambiguity Check PASS, and activated `production/sprints/codex-story-obj-002.prompt.txt` as the current approved prompt.

## [2026-06-11] merge-and-prepare | STORY-OBJ-002 closeout and TAC-007 candidate

- Verified and merged Unity PR #29 for `STORY-OBJ-002 Guarded Site Defender Strength Tiers` after fixing merge-gate blockers around tier/setup consistency.
- Recorded merge commit `7b6807b5fe3b0b231102d293d12abd54e98acafd` and post-merge main CI success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests.
- Marked `STORY-OBJ-002` DONE / merged and updated `EPIC-VSLICE-MVP-003` child status.
- Expanded `STORY-TAC-007 Simple Stack HP/Strength Persistence` into a DRAFT / READY-candidate packet with approval pending; it is not implementation-authorizing yet.
- Added guarded prompt `production/sprints/codex-story-tac-007.prompt.txt` and repointed run prompts to stop until human approval promotes TAC-007 to READY / approved.

## [2026-06-11] approval | STORY-TAC-007 promoted to READY

- Recorded human approval for `STORY-TAC-007 Simple Stack HP/Strength Persistence`.
- Captured zero-count stack decision: remove zero-count stacks from the active strategic army, document and test the rule.
- Added explicit minimal visual-layer requirement for stack strength and battle-result feedback so the player can see stack-count changes and understand the battle result caused them.
- Promoted TAC-007 to READY / approved and activated `production/sprints/codex-story-tac-007.prompt.txt` as the current implementation prompt.

## [2026-06-11] unblock | STORY-TAC-007 roster-source exception

- Codex correctly stopped because `design/gdd/faction-unit-rosters.md` is `status: draft` / `approval: pending` while TAC-007 linked it as a required source.
- Recorded a narrow human-approved exception: TAC-007 may read the draft roster GDD only as a non-authoritative placeholder fixture reference for existing unit/stack IDs.
- Clarified that final roster names, balance, recovery, lore, faction identity, and content remain unauthorized; implementation must stop if it needs those decisions.
- Updated the TAC-007 prompt and run prompts so Codex can proceed without weakening source-control rules.

## [2026-06-11] approval | STORY-LOOP-004 promoted to READY

- Recorded human approval for `STORY-LOOP-004 Objective, Champion Combat, and Casualty Stakes Smoke`.
- Promoted LOOP-004 to READY / approved with Ambiguity Check PASS.
- Approved scope is pure connected smoke/evidence only; if a real gameplay or UI blocker prevents the smoke, implementation must stop and report instead of broadening scope.
- Recorded that EPIC-VSLICE-MVP-003 must not close automatically from CI alone; LOOP-004 evidence informs the next human closeout/playtest decision.
- Activated `production/sprints/codex-story-loop-004.prompt.txt` as the current copy-safe Codex prompt.


## [2026-06-12] approve | EPIC-004 Intel on-ramp and STORY-INTEL-001 implementation prep

- Closed `EPIC-VSLICE-MVP-003` as DONE after LOOP-004 evidence, post-merge Unity CI, and human closeout acceptance.
- Created `production/epics/epic-vslice-mvp-004-intel-resource-on-ramp.md` as the next approved capability container.
- Created and promoted `production/stories/story-intel-001-faction-intel-and-data-cache-pickup.md` to READY / approved as the only current Unity implementation authority.
- Created `production/sprints/codex-story-intel-001.prompt.txt` and updated current run-prompt docs for Codex-safe implementation.
- Kept broader Intel systems deliberately out of scope: spending, fog/hidden information, dirty information, tactical Intel rewards, recurring economy, and final content.

## [2026-06-12] approve | STORY-INTEL-002 implementation prep

- Marked `STORY-INTEL-001 Faction Intel and Data Cache Pickup` DONE / merged after Unity PR #33 squash-merged as `c28e64a25f6283c18463e404ff0368047fbb7ad2`.
- Recorded PR-gate Unity Actions success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests; later verified post-merge main CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27411089173.
- Promoted `STORY-INTEL-002 First Intel Spending Sink — Field Upgrade` to READY / approved as the next implementation packet.
- Human-approved scope: one placeholder selected-Champion field upgrade costing 5 Intel, using current global faction Intel and existing attached-army state for a small visible effect; no upgrade tree, asset inventory, operations/hacks/doctrine, fog/hidden information, dirty information, tactical Intel rewards, recurring economy, final content, or broad UI redesign.
- Added `production/sprints/codex-story-intel-002.prompt.txt` and repointed current Codex run prompts to STORY-INTEL-002.

## [2026-06-12] merge | STORY-INTEL-002 closeout and next candidate prep

- Reviewed Unity PR #34 for `STORY-INTEL-002 First Intel Spending Sink — Field Upgrade` against the approved story contract.
- Fixed a review blocker where rejected invalid field-upgrade Apply calls could create a missing Champion upgrade-marker list before validation completed; added regression coverage for invalid no-partial-mutation and missing-selected spend rejection.
- Verified PR exact-head Unity Actions success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27418263410.
- Squash-merged PR #34 to Unity `main` as `cc0b3070de38da8891f5f0f02de4a354e90aed06` and verified post-merge `main` Unity Actions success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27419055491.
- Marked `STORY-INTEL-002` DONE / merged.
- Prepared `STORY-INTEL-003 Guarded Data Site Intel Reward` as DRAFT / READY-candidate only, with approval pending and Ambiguity Check FAIL until human review.
- Added guarded non-runnable prompt `production/sprints/codex-story-intel-003.prompt.txt`; no Unity implementation is currently authorized.

## [2026-06-12] approve | STORY-INTEL-003 implementation prep

- Recorded human approval for `STORY-INTEL-003 Guarded Data Site Intel Reward`.
- Promoted STORY-INTEL-003 to READY / approved with Ambiguity Check PASS.
- Approved scope: one guarded Intel reward path; reuse an existing guarded site if technically clean, otherwise add one placeholder guarded data site; award exactly 5 Intel to the active/claiming faction only after successful guarded-site capture / battle-result return.
- Kept recurring economy, Intel subtypes, hidden/dirty information, tactical optional objectives beyond the single approved path, operations/hacks/doctrine, upgrade trees, asset inventory, final content/art/UI redesign, save/load, and strategic AI spending out of scope.
- Activated `production/sprints/codex-story-intel-003.prompt.txt` and repointed current Codex run prompts to STORY-INTEL-003.
## [2026-06-12] merge | STORY-INTEL-003 closeout and next candidate prep

- Reviewed Unity PR #35 for `STORY-INTEL-003 Guarded Data Site Intel Reward` against the approved story contract.
- Verified PR exact-head Unity Actions success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27422389899.
- Marked PR #35 ready for review, recorded merge-gate PASS, and squash-merged to Unity `main` as `e8640ba8120fc7f6c31d6014fd40d4133fe6f95b`.
- Verified post-merge `main` Unity Actions success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27423740025.
- Marked `STORY-INTEL-003` DONE / merged.
- Prepared `STORY-INTEL-004 Intel On-Ramp Closeout Smoke` as DRAFT / READY-candidate only, with approval pending and Ambiguity Check FAIL until human review.
- Added guarded non-runnable prompt `production/sprints/codex-story-intel-004.prompt.txt`; no Unity implementation is currently authorized.
## [2026-06-12] decision | Field Upgrade placeholder

- Human clarified that `field_upgrade_alpha` / “Field Upgrade” is acceptable for now as a placeholder only.
- It is not a canon final Champion upgrade system and may be renamed, re-fictionalized, or replaced when Champion assets/upgrades are designed properly.
## [2026-06-12] approve | STORY-INTEL-004 implementation prep

- Recorded human approval for `STORY-INTEL-004 Intel On-Ramp Closeout Smoke`.
- Promoted STORY-INTEL-004 to READY / approved with Ambiguity Check PASS.
- Approved scope: one connected smoke/evidence path for cache -> placeholder `field_upgrade_alpha` / “Field Upgrade” spend -> guarded Intel reward, with no new Intel mechanics.
- Recorded that “Field Upgrade” remains approved for now as placeholder only and may be renamed/replaced later.
- Activated `production/sprints/codex-story-intel-004.prompt.txt` and repointed current Codex run prompts to STORY-INTEL-004.
## [2026-06-12] merge | STORY-INTEL-004 closeout and next candidate prep

- Reviewed Unity PR #36 for `STORY-INTEL-004 Intel On-Ramp Closeout Smoke` against the approved story contract.
- Verified PR exact-head Unity Actions success for Compile / Standalone Check, EditMode Tests, Placeholder Validator, and PlayMode Smoke Tests at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27426393447.
- Marked PR #36 ready for review, recorded merge-gate PASS, and squash-merged to Unity `main` as `e596b2a6aa0b309f4d11038ace380b777d42d45c`.
- First post-merge `main` run stalled; cancelled and re-ran the same run, which completed successfully at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27434768941.
- Marked `STORY-INTEL-004` DONE / merged.
- Prepared `STORY-UX-001 Strategic Map Readability and Action Clarity Pass` as DRAFT / READY-candidate only, with approval pending and Ambiguity Check FAIL until human review.
- Added guarded non-runnable prompt `production/sprints/codex-story-ux-001.prompt.txt`; no Unity implementation is currently authorized.
## [2026-06-12] approve | STORY-UX-001 implementation prep

- Recorded human approval for `STORY-UX-001 Strategic Map Readability and Action Clarity Pass`.
- Promoted STORY-UX-001 to READY / approved with Ambiguity Check PASS.
- Approved scope: small strategic-map readability/action clarity improvements before further gameplay/system expansion, with before/after PNG evidence and no new gameplay mechanics.
- Activated `production/sprints/codex-story-ux-001.prompt.txt` and repointed current Codex run prompts to STORY-UX-001.

- 2026-06-12: STORY-UX-001 merged via Unity PR #37 (`a43ed135bb07f495a7cff791aeca562d5afe936b`) after right-panel overflow blocker was fixed and exact-head/post-merge CI passed. Prepared STORY-QA-005 as READY-candidate to clean up PlayMode evidence artifact hygiene.

## [2026-06-13] approve | STORY-QA-005 implementation prep

- Recorded human approval for `STORY-QA-005 PlayMode Evidence Artifact Hygiene`.
- Promoted STORY-QA-005 from DRAFT / READY-candidate to READY / approved with Ambiguity Check PASS.
- Approved scope: PlayMode evidence artifact hygiene only; no gameplay/UI changes, no committed evidence deletion, preserve local evidence override, reduce stale CI evidence paths and artifact quota pressure.
- Activated `production/sprints/codex-story-qa-005.prompt.txt` and repointed current Codex run prompts to STORY-QA-005.

## [2026-06-13] merge | STORY-QA-005 closeout

- Reviewed Unity PR #38 for `STORY-QA-005 PlayMode Evidence Artifact Hygiene` against the approved story contract.
- Verified exact-head Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27461099199.
- Recorded merge-gate PASS, marked PR #38 ready for review, and squash-merged to Unity `main` as `507fb8c7b2e42dc54ed1902096230d369225efc7`.
- Verified post-merge `main` Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27461556833.
- Marked `STORY-QA-005` DONE / merged and cleared the current Codex prompt pointer; no next Unity implementation story is currently READY.
- Cleared the Unity repo current-task pointer in follow-up PR #39, squash-merged as `4943a74554a1777156af960bdccb90d52a2b16b3`; post-merge `main` Unity Foundation CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27461937339.

## [2026-06-13] plan | EPIC-005 Champion Command direction

- Formally closed `EPIC-VSLICE-MVP-004 Intel Resource On-Ramp` as DONE after human closeout acceptance.
- Drafted `EPIC-VSLICE-MVP-005 Champion Command and Operations On-Ramp` as the next approved-candidate capability container.
- Recorded human direction to pursue Champion Command / Operations and to try supporting both archetype poles: Marshals and Operators.
- Drafted `STORY-CMD-001 Champion Command Archetype State and Tactical HUD` as READY-candidate / approval pending. It establishes finite Command state and tactical HUD visibility for both Marshal-like and Operator-like profiles, without active command spending.
- Added guarded non-runnable prompt `production/sprints/codex-story-cmd-001.prompt.txt`; no Unity implementation is currently authorized.

## [2026-06-13] design | Marshal / Operator Command clarification and STORY-CMD-001 READY

- Consulted Champion Operations design notes and active tactical-combat Champion Operations GDD.
- Clarified that capital-C `Command` is the HoMM Knowledge analogue, not generic military authority. Operators lean into Command/Control; Marshals lean into Attack/Defense/Logistics, Doctrine, Cohesion reliability, and Minor Command capacity.
- Approved `EPIC-VSLICE-MVP-005 Champion Command and Operations On-Ramp` as the next production capability container.
- Promoted `STORY-CMD-001 Champion Command Archetype State and Tactical HUD` to READY / approved.
- Recorded barebones profile contract: `marshal_alpha` has Command 2, Major Operation Slots 0, Minor Command Capacity 2, Control Scalar 0, Doctrine Scalar 1; `operator_alpha` has Command 3, Major Operation Slots 1, Minor Command Capacity 0, Control Scalar 1, Doctrine Scalar 0.
- Updated `production/sprints/codex-story-cmd-001.prompt.txt` as the current approved Unity implementation prompt.

## [2026-06-13] done | STORY-CMD-001 merged

- Implemented and merged Unity PR #40 for `STORY-CMD-001 Champion Command Archetype State and Tactical HUD`.
- Clarified design question in implementation: capital-C `Command` is the Knowledge analogue, so Operators lean into Command/Control; Marshals lean into Attack/Defense/Logistics, Doctrine, Cohesion reliability, and Minor Command capacity.
- Barebones implementation added `marshal_alpha` and `operator_alpha` command profile state, tactical board propagation, tactical presentation snapshot fields, and HUD visibility.
- No active command spending/effects were added.
- PR CI passed on final head and post-merge main CI passed.
- Cleared current Codex prompt pointer; no Unity implementation story is currently READY.

## [2026-06-13] approve | STORY-CMD-002 implementation prep

- Recorded human request to prepare `STORY-CMD-002 First Marshal and Operator Command Pair` for Codex implementation after `STORY-CMD-001` merged.
- Created and promoted `production/stories/story-cmd-002-first-marshal-and-operator-command-pair.md` to READY / approved with Ambiguity Check PASS.
- Approved narrow prototype command pair: Marshal `rally_order` / `Rally Order` costs 1 Command and restores 1 current stack count up to cap; Operator `drone_strike` / `Drone Strike` costs 2 Command and deals 1 direct damage to one opposing non-defeated stack, with at most one Major Operation per battle for this MVP story.
- Kept broader Operations UI, command trees, Command regeneration, round/cooldown/reaction systems, Intel integration, final content/art/VFX/audio, and progression out of scope.
- Added checked-in Codex prompt `production/sprints/codex-story-cmd-002.prompt.txt` and repointed current run prompts to STORY-CMD-002.

## [2026-06-13] merge-and-prepare | STORY-CMD-002 closeout and CMD-003 READY

- Reviewed Unity PR #41 for `STORY-CMD-002 First Marshal and Operator Command Pair` against the approved story contract.
- Fixed merge-gate issues before merge: added null-safe Drone Strike fallback / tactical presentation handling for missing placed-stack collections, plus regression coverage for Rally insufficient Command, Drone Strike after battle completion, visible second-Drone-Strike denial feedback, and missing placed-stack fallback denial.
- Verified PR exact-head Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27467133863.
- Marked PR #41 ready for review, recorded merge-gate PASS, and squash-merged to Unity `main` as `73a15d98d24a93857405bcdff09c3f20ddac498c`.
- Verified post-merge `main` Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27467415661.
- Marked `STORY-CMD-002` DONE / merged.
- Promoted `STORY-CMD-003 Command On-Ramp Closeout Smoke` to READY / approved as the next implementation packet, recording the human request to merge CMD-002 and prepare the next implementation story as delegated approval for this immediate closeout smoke.

## [2026-06-13] merge-and-closeout | STORY-CMD-003 merged; EPIC-005 awaits human review

- Reviewed Unity PR #42 for `STORY-CMD-003 Command On-Ramp Closeout Smoke` against the approved story contract.
- Confirmed implementation is connected smoke/evidence only: PlayMode smoke plus `production/evidence/STORY-CMD-003/` README/PNGs; no runtime mechanics or out-of-scope systems added.
- Verified PR exact-head Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27468129149.
- Marked PR #42 ready for review, recorded merge-gate PASS, and squash-merged to Unity `main` as `edebd1eb8023e736351649916c7dca8a2117b155`.
- Verified post-merge `main` Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27468769463.
- Marked `STORY-CMD-003` DONE / merged.
- Updated EPIC-005 to awaiting human closeout/playtest review instead of DONE; no next implementation story is approved yet.
- Cleared the current Codex implementation prompt until a new READY / approved story is selected.

## [2026-06-13] story-prep | STORY-CMD-004 approved and prepared

- Human approved continuing EPIC-005 with one final tactical command usability and targeting pass after `STORY-CMD-003` merged.
- Created `STORY-CMD-004 Tactical Command Usability and Targeting Pass` as READY / approved.
- Scope is intentionally narrow: improve player-facing usability, target/denial feedback, and PlayMode evidence for existing `Rally Order` and `Drone Strike` only.
- Updated EPIC-005 from awaiting closeout to active for this final usability pass.
- Added copy-safe Codex prompt `production/sprints/codex-story-cmd-004.prompt.txt` and repointed the run-prompt index.

## [2026-06-13] merge-and-closeout | STORY-CMD-004 merged; EPIC-005 awaits human review

- Reviewed Unity PR #43 for `STORY-CMD-004 Tactical Command Usability and Targeting Pass` against the approved story contract.
- Confirmed implementation improves existing `Rally Order` and `Drone Strike` usability/targeting only: availability/denial text, explicit Drone Strike target feedback, no-target denial, HUD summary refresh, tests, and evidence.
- Fixed stale/pending CI evidence text in `production/evidence/STORY-CMD-004/README.md`, pushed an evidence commit, and re-verified exact-head CI.
- Verified PR exact-head Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27470536214.
- Recorded merge-gate PASS and squash-merged PR #43 to Unity `main` as `0fd5ac072f8dc285f00b06e551ee7142f56e464a`.
- Verified post-merge `main` Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27470891186.
- Marked `STORY-CMD-004` DONE / merged.
- Updated EPIC-005 to awaiting human closeout/playtest review; no next implementation story is approved yet.
- Cleared the current Codex implementation prompt until a new READY / approved story is selected.

## [2026-06-13] playtest-closeout | EPIC-005 closeout rejected; QA repair train approved

- Recorded human playtest feedback for the whole current prototype / EPIC-005 closeout review.
- Verdict: REJECT CLOSEOUT. The implementation is technically connected, but the loop is not player-readable enough to judge.
- Main blockers: unclear active turn/actor, unclear selected Champion location on some nodes, unclear guarded/site/objective state, unclear tactical current stack/friendly/enemy/attack target, weak action/result feedback, and visible-but-unexplained Champion commands.
- Human approved the proposed repair stories.
- Created approved repair train `production/sprints/epic-005-playability-repair-train.md`.
- Promoted `STORY-QA-006 Strategic and Tactical State/Action Feedback Readability Pass` to READY / approved as the next Codex implementation packet.
- Added `STORY-QA-007 Champion Encounter Initiation Clarity` and `STORY-CMD-005 Champion Command Explanation Pass` as gated READY-candidates after QA-006.
- Added `STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction` as DRAFT because objective capture pacing is design-heavy and not current implementation.
- Created current Codex prompt `production/sprints/codex-story-qa-006.prompt.txt` and repointed run prompts.

## [2026-06-13] merge-and-advance | STORY-QA-006 merged; STORY-QA-007 prepared

- Reviewed Unity PR #44 for `STORY-QA-006 Strategic and Tactical State/Action Feedback Readability Pass`.
- Independent review found one blocker: evidence README lacked the required CI URL. Fixed the README, pushed an evidence commit, and re-verified exact-head CI.
- Verified PR exact-head Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27476023860.
- Squash-merged PR #44 to Unity `main` as `a0c2b052746e0cba2838242cc2732853c9e8f9a8`.
- Verified post-merge `main` Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27476388754.
- Marked `STORY-QA-006` DONE / merged.
- Promoted `STORY-QA-007 Champion Encounter Initiation Clarity` to READY / approved as the next implementation packet.
- Created current Codex prompt `production/sprints/codex-story-qa-007.prompt.txt` and repointed run prompts.
- Kept `STORY-CMD-005` READY-candidate and `STORY-STRAT-OBJECTIVE-001` DRAFT.

## [2026-06-14] merge-and-advance | STORY-QA-007 merged; STORY-CMD-005 prepared

- Reviewed Unity PR #45 for `STORY-QA-007 Champion Encounter Initiation Clarity`.
- Independent review found stale/non-specific CI evidence; fixed `production/evidence/STORY-QA-007/README.md`, pushed an evidence clarification commit, and recorded final exact-head CI in the PR gate comment.
- Verified PR exact-head Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27500086022.
- Squash-merged PR #45 to Unity `main` as `52d36e22751555bb012b43798db39649d8a90ff6`.
- Verified post-merge `main` Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27500477543.
- Marked `STORY-QA-007` DONE / merged.
- Promoted `STORY-CMD-005 Champion Command Explanation Pass` to READY / approved as the next implementation packet, recording the user request to merge QA-007 and prepare the next implementation packet as delegated approval for this immediate repair-train follow-up.
- Created current Codex prompt `production/sprints/codex-story-cmd-005.prompt.txt` and repointed run prompts.
- Updated the Unity repo current-task pointer on `main` to `STORY-CMD-005` as commit `fe480605a901fcab6a4407e19746891f52bfbc93`; Unity Foundation CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27500803658.

## [2026-06-14] merge-and-gate-next | STORY-CMD-005 merged; objective direction guarded

- Reviewed Unity PR #46 for `STORY-CMD-005 Champion Command Explanation Pass`.
- Independent review found stale/non-specific CI evidence; fixed `production/evidence/STORY-CMD-005/README.md`, pushed an evidence clarification commit, and recorded final exact-head CI in the PR gate comment.
- Verified PR exact-head Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27502389529.
- Squash-merged PR #46 to Unity `main` as `b89b02d568c67b70dcead1cfcae90ee9f937d3cd`.
- Verified post-merge `main` Unity Foundation CI success at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27502711745.
- Marked `STORY-CMD-005` DONE / merged.
- Expanded `STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction` only to READY-candidate / approval pending with Ambiguity Check FAIL; objective-rule design remains unapproved.
- Created guarded non-runnable prompt `production/sprints/codex-story-strat-objective-001.prompt.txt` and updated run prompts to say no Unity implementation packet is currently approved.
- Cleared the Unity repo current-task pointer on `main` as commit `60c30cf316023c79e4afd71ac58c90f01676fe09`; Unity Foundation CI passed at https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27502974784.
## 2026-06-14 — Approved STORY-STRAT-OBJECTIVE-001 implementation packet

- Recorded human approval for `STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction`.
- Approved rule shape: Option 1, a narrow two-turn central-objective hold countdown.
- Promoted the story to READY / approved with Ambiguity Check PASS.
- Replaced the guarded prompt with runnable Codex prompt `production/sprints/codex-story-strat-objective-001.prompt.txt`.
- Updated EPIC-005, the playability repair train, run prompts, and index so this story is the current implementation packet.


## 2026-06-15 — STORY-STRAT-OBJECTIVE-001 merged; EPIC-005 closeout review ready

- Verified and merged Unity PR #47 for `STORY-STRAT-OBJECTIVE-001 Multi-Turn Objective Contest Direction`.
- Merge commit: `2eab67d8a10824a122493271feae94d53119c440`.
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27530718158
- Marked `STORY-STRAT-OBJECTIVE-001` DONE / merged and updated EPIC-005 repair-train status.
- Cleared current Codex run prompts: no next Unity implementation packet is approved until human closeout review or a new READY story direction.
- Unity current-task pointer cleared on main as `272fe543bc496ff729cfb428599e4e553e685979`; Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27531270885

## [2026-06-15] add | Prototype readability and HoMM-like map references

- Added `design/research/homm-like-tactical-battle-ui-reference.md` with tactical readability references for HoMM3, Olden Era, and Songs of Conquest: stack counts, event-feed language, movement/attack affordances, Defend, and retaliation.
- Added `design/research/homm-like-strategic-map-topology-reference.md` with strategic/adventure-map topology references: H3 square-tile adventure map, Olden Era/Songs modern HoMM-like map expectations, King's Bounty as anti-reference, and a recommended region/site transition path.
- Added `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` recommending a readability-first implementation order: tactical stack labels/event feed, minimal melee retaliation, movement/attack affordances, unit definitions, AP/Defend, neutral AI, strategic readability, bases, then region/site map evolution.
- Updated `index.md` links.

## [2026-06-15] approve | EPIC-006 and EPIC-007 split; STORY-TAC-READ-002 READY

- Recorded human approval for the two-epic split: `EPIC-VSLICE-MVP-006 Tactical Battle Readability and Defender Agency` first, then `EPIC-VSLICE-MVP-007 Strategic Map Readability, Bases, and Spatial Presentation`.
- Marked `EPIC-VSLICE-MVP-005 Champion Command and Operations On-Ramp` complete / human closeout accepted for next-direction handoff.
- Created approved `production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency.md` with child-story sequence: stack labels/event feed, retaliation, movement/attack affordances, unit definitions, AP/Defend, neutral guard AI.
- Created approved `production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation.md`, sequenced after the tactical readability baseline.
- Created READY / approved `production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed.md` as the only current Unity implementation authority.
- Added checked-in Codex prompt `production/sprints/codex-story-tac-read-002.prompt.txt` and updated `index.md`.

## [2026-06-15] merge | STORY-TAC-READ-002 tactical readability baseline

- Reviewed and merged Unity PR #48 for `STORY-TAC-READ-002 Tactical Stack Labels and Combat Event Feed`.
- Squash merge commit: `2c22667532ccc64e0fe746030fd33707c2edd682`.
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27543258160
- Marked `STORY-TAC-READ-002` DONE and updated EPIC-006 child-story status.

## [2026-06-15] approve | STORY-TAC-RET-001 minimal melee retaliation

- Created `production/stories/story-tac-ret-001-minimal-melee-retaliation.md` as the next READY / approved EPIC-006 implementation packet.
- Created `production/sprints/codex-story-tac-ret-001.prompt.txt` for Codex execution.
- Scope is intentionally narrow: adjacent surviving defender retaliation, once-per-minimal-cycle availability, readable event-feed output, tests/evidence/CI; excludes AP, Defend bonus, ZoC, Overwatch, CombatAI, unit roster/stat expansion, and final art/content.

## [2026-06-15] merge | STORY-TAC-RET-001 minimal melee retaliation

- Reviewed and merged Unity PR #49 for `STORY-TAC-RET-001 Minimal Melee Retaliation`.
- Squash merge commit: `cfc24e04c53da0a6917b0117452c72a230ef9a84`.
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27552604744
- Marked `STORY-TAC-RET-001` DONE and updated EPIC-006 child-story status.

## [2026-06-15] approve | STORY-TAC-AFFORD-001 movement and attack affordance pass

- Created `production/stories/story-tac-afford-001-movement-and-attack-affordance-pass.md` as the next READY / approved EPIC-006 implementation packet.
- Created `production/sprints/codex-story-tac-afford-001.prompt.txt` for Codex execution.
- Scope is intentionally narrow: visible movement range, attack range, current coordinate, legal move/attack affordances, blocked/non-attackable context, and denial feedback; excludes AP, Defend bonus, ZoC, Overwatch, CombatAI, unit roster/stat expansion, strategic-map changes, and final art/content.

## [2026-06-15] verify | STORY-TAC-AFFORD-001 handoff publish and Unity pointer

- Design/control publish CI passed for `STORY-TAC-AFFORD-001` packet: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27553269879
- Unity README current-task pointer commit `9cdb31adcd7829b073889af84c56e85ff8e264fc` passed Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27553270134

## [2026-06-15] merge | STORY-TAC-AFFORD-001 movement and attack affordance pass

- Reviewed and merged Unity PR #50 for `STORY-TAC-AFFORD-001 Movement and Attack Affordance Pass`.
- Squash merge commit: `11e5703d79f0dde6be8f5ceec9c7834c3e8e4b9e`.
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27562547868
- Marked `STORY-TAC-AFFORD-001` DONE and updated EPIC-006 child-story status.

## [2026-06-15] draft | STORY-TAC-UNIT-001 minimal unit definition stats

- Created `production/stories/story-tac-unit-001-minimal-unit-definition-stats.md` as the next proposed EPIC-006 packet.
- Created guarded prompt `production/sprints/codex-story-tac-unit-001.prompt.txt`.
- Status is READY-candidate / approval pending because the parent epic only listed this item as a draft target; Codex prompt self-blocks until human approval promotes the story to READY.
- Proposed scope: minimal code-side unit definition catalog, definition-derived movement/attack/damage/retaliation capability/display labels, tests/evidence; excludes full roster, final content/art, balance pass, AP, Defend bonus, ZoC, Overwatch, CombatAI, abilities/statuses, and strategic-map/base changes.

## [2026-06-15] verify | STORY-TAC-UNIT-001 candidate publish and Unity pointer clear

- Design/control publish CI passed for `STORY-TAC-UNIT-001` candidate packet: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27563075187
- Unity README pointer-clear commit `7b75805be994228c048c13daf8d24be2e0878886` passed Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27563076371

## [2026-06-15] approval | STORY-TAC-UNIT-001 ready for implementation

- Human approval recorded from chat: "Approved, prepare."
- Promoted `production/stories/story-tac-unit-001-minimal-unit-definition-stats.md` from READY-candidate to READY / approved.
- Recorded approved assumptions: code-side placeholder catalog only; one or two tiny prototype stat differences allowed to prove data path; non-retaliating units may skip melee retaliation with event-feed explanation.
- Recorded narrow source-authority exception for cited draft/pending tactical article passages; broader roster, AP, ability/status, objective, CombatAI, and strategic-map work remains unapproved.
- Updated EPIC-006, index, and Codex prompt `production/sprints/codex-story-tac-unit-001.prompt.txt` for implementation handoff.

## [2026-06-16] merge | STORY-TAC-UNIT-001 minimal unit definition stats

- Reviewed and merged Unity PR #51 for `STORY-TAC-UNIT-001 Minimal Unit Definition Stats`.
- Squash merge commit: `b95368b66ed53be957bbdb545c7dbb4da627e2fd`.
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27619495357
- Marked `STORY-TAC-UNIT-001` DONE and updated EPIC-006 child-story status.
- Added a closeout safeguard to the active Codex prompt and reusable handoff pattern: future Codex implementation prompts must explicitly commit, push, open/update the PR, or report a concrete push blocker with `git status --short --branch`.

## [2026-06-16] draft | STORY-TAC-AP-001 minimal tactical AP and Defend state

- Created `production/stories/story-tac-ap-001-minimal-tactical-ap-and-defend-state.md` as the next proposed EPIC-006 packet.
- Created guarded prompt `production/sprints/codex-story-tac-ap-001.prompt.txt`.
- Status is READY-candidate / approval pending because the parent epic listed AP/Defend as a draft target, not an approved READY story.
- Proposed scope: baseline 2 AP activation state, Move/Basic Attack cost 1 AP, insufficient-AP denial/no mutation, visible Defend state, tactical snapshot/HUD/event-feed visibility, and focused tests/evidence.
- Open approval question before READY: Defend visible state only versus tiny prototype damage-reduction effect. Recommended default is visible state only.

## [2026-06-16] verify | STORY-TAC-AP-001 candidate publish and Unity pointer clear

- Design/control publish CI passed for `STORY-TAC-AP-001` candidate packet: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27620455931
- Unity README pointer-clear PR #52 merged as `1aeb8f193e1371884c0a44a9c027b53623bbc4d9`; Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27620829960
## [2026-06-17] approval | STORY-TAC-AP-001 promoted to READY

- Human approval recorded for `STORY-TAC-AP-001 Minimal Tactical AP and Defend State`.
- Approved Defend direction: visible `Defending` state plus a tiny prototype damage-reduction effect.
- Promoted story to READY / approved, passed ambiguity check, and recorded the narrow source-authority exception for draft AP/Defend planning sources.
- Replaced guarded `production/sprints/codex-story-tac-ap-001.prompt.txt` with the runnable implementation prompt.
- Updated EPIC-006, index, and Codex run prompts to point at `STORY-TAC-AP-001` as the current approved Unity implementation packet.


## [2026-06-17] merge | STORY-TAC-AP-001 minimal tactical AP and Defend state

- Reviewed and merged Unity PR #53 for `STORY-TAC-AP-001 Minimal Tactical AP and Defend State`.
- Merge-gate fixes made before merge: Basic Attack from full AP now spends 1 AP without ending activation, Drone Strike respects the temporary Defend reduction, and strategic/PlayMode smoke flows were updated for 2-AP activations.
- Squash merge commit: `d2c55ad4820d64f6980a7cbf432f632bd4c17ce3`.
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27689580984
- Marked `STORY-TAC-AP-001` DONE and updated EPIC-006 child-story status.

## [2026-06-17] draft | STORY-TAC-AI-001 neutral guard one-step CombatAI

- Created `production/stories/story-tac-ai-001-neutral-guard-one-step-combat-ai.md` as the next proposed EPIC-006 packet.
- Created guarded prompt `production/sprints/codex-story-tac-ai-001.prompt.txt`.
- Status is READY-candidate / approval pending. The prompt self-blocks until human approval promotes the story to READY.
- Proposed scope: deterministic one-step CombatAI for neutral guarded-site defender stacks only: Attack if legal, else move one legal step toward nearest living enemy, else Defend, else Pass.
- Explicitly excludes strategic AI, advanced tactical AI/planning, randomness, initiative/Wait, ZoC/Overwatch, new combat mechanics, final UI/audio/VFX/content, and broad controller architecture rewrites.

## [2026-06-17] verify | STORY-TAC-AI-001 candidate publish and Unity pointer clear

- Design/control publish CI passed for `STORY-TAC-AI-001` candidate packet: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27693399088
- Unity README pointer commit `607bf03c091d13dd43ecdf01b4d6636f8aa8539c` passed Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27693503026
- Unity README now states no READY / approved implementation task is active and points to the guarded `STORY-TAC-AI-001` candidate packet only.


## [2026-06-17] approval | STORY-TAC-AI-001 promoted to READY

- Human approval recorded for `STORY-TAC-AI-001 Neutral Guard One-Step CombatAI`.
- Approved direction: deterministic one-step neutral guard CombatAI for guarded-site defender stacks only: Attack if legal, else move one legal step toward nearest living enemy, else Defend, else Pass.
- Promoted story to READY / approved, passed ambiguity check, and recorded the narrow source-authority exception for draft tactical AI/AP implementation sources.
- Replaced the guarded prompt `production/sprints/codex-story-tac-ai-001.prompt.txt` with the runnable implementation prompt.
- Updated EPIC-006, index, and Codex run prompts to point at `STORY-TAC-AI-001` as the current approved Unity implementation packet.


## [2026-06-17] verify | STORY-TAC-AI-001 approval publish and Unity pointer

- Design/control publish CI passed for `STORY-TAC-AI-001` approval packet: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27694739627
- Unity README approved-task pointer commit `0e54ac1d99616ab3b1f3d9e4800238b35f871e1f` passed Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27694848108
- Unity README now names `STORY-TAC-AI-001 Neutral Guard One-Step CombatAI` as the current READY / approved implementation task.


## [2026-06-17] merge | STORY-TAC-AI-001 neutral guard one-step CombatAI

- Reviewed and merged Unity PR #54 for `STORY-TAC-AI-001 Neutral Guard One-Step CombatAI`.
- Squash merge commit: `0a7e67383932101459529a015e4d82d1d06b53b1`.
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27700425414
- Marked `STORY-TAC-AI-001` DONE and updated EPIC-006 child-story status.

## [2026-06-17] draft | STORY-STRAT-READ-002 strategic map readability pass

- Created `production/stories/story-strat-read-002-strategic-map-readability-pass.md` as the next proposed EPIC-007 packet.
- Created guarded prompt `production/sprints/codex-story-strat-read-002.prompt.txt`.
- Status is READY-candidate / approval pending. The prompt self-blocks until human approval promotes the story to READY.
- Proposed scope: strategic map readability improvements for reachable routes/sites, path-cost preview, site category/state labels, interaction preview, and post-battle return summary using existing graph-backed state.
- Explicitly excludes tile/hex topology, new base/recruitment systems, strategic AI, fog/logistics/weather, full economy, new tactical rules, and final map art/content.


## [2026-06-17] verify | STORY-STRAT-READ-002 candidate publish and Unity pointer clear

- Design/control publish CI passed for `STORY-STRAT-READ-002` candidate packet: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27701173908
- Unity README pointer commit `914d6e938b85316403de8c5b9fbeb524d38e165b` passed Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27701275473
- Unity README now states no READY / approved implementation task is active and points to the guarded `STORY-STRAT-READ-002` candidate packet only.

## [2026-06-18] approval | STORY-STRAT-READ-002 promoted to READY

- Human approval recorded from chat: `STORY-STRAT-READ-002 approved`.
- Promoted `production/stories/story-strat-read-002-strategic-map-readability-pass.md` from READY-candidate to READY / approved.
- Approved assumptions: existing strategic mechanics only; placeholder labels/icons/markers may be used if clear and covered by evidence; exact text is implementation-owned within acceptance criteria.
- Recorded narrow source-authority exception for the cited draft planning/reference notes as bounded context only; broader topology, base/recruitment, economy, fog/logistics, strategic AI, and final-content work remain out of scope.
- Replaced the guarded `production/sprints/codex-story-strat-read-002.prompt.txt` with the runnable implementation prompt.
- Updated EPIC-007, index, and Codex run prompts to point at `STORY-STRAT-READ-002` as the current approved Unity implementation packet.

## [2026-06-18] merge | STORY-STRAT-READ-002 strategic map readability pass

- Reviewed and merged Unity PR #55 for `STORY-STRAT-READ-002 Strategic Map Readability Pass`.
- Merge-gate fixes before merge: added recruit/reinforce preview coverage, restored legacy visible action strings, and compacted strategic readability UI text.
- Squash merge commit: `e6e26835595db1cad51a3fbcdf3220d1391874cd`.
- Exact-head PR Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27744712697
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27745368044
- Marked `STORY-STRAT-READ-002` DONE and updated EPIC-007 child-story status.

## [2026-06-18] draft | STORY-STRAT-BASE-001 starting hub reinforcement preview

- Created `production/stories/story-strat-base-001-starting-hub-reinforcement-preview.md` as the next proposed EPIC-007 packet.
- Created guarded prompt `production/sprints/codex-story-strat-base-001.prompt.txt`.
- Status is READY-candidate / approval pending. The prompt self-blocks until human approval promotes the story to READY.
- Proposed scope: one fixed prototype starting-hub/base-like reinforcement preview/action for the active Champion using existing strategic resource/army state.
- Explicitly excludes full base/town-building systems, garrisons, reserves/caravans, stock economy, new unit roster/balance, topology migration, new tactical rules, and final map/base art/content.

## [2026-06-18] verify | STORY-STRAT-BASE-001 candidate publish and Unity pointer clear

- Design/control publish CI passed for `STORY-STRAT-BASE-001` candidate packet: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27745979278
- Unity README pointer commit `18520eac55d55f4193137a46b9857921ca1c6358` passed Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27745985653
- Unity README now states no READY / approved implementation task is active and points to the guarded `STORY-STRAT-BASE-001` candidate packet only.

## [2026-06-18] approval | STORY-STRAT-BASE-001 starting hub reinforcement preview

- Human approved `STORY-STRAT-BASE-001 Starting Hub Reinforcement Preview`.
- Promoted story from READY-candidate / approval pending to READY / approved.
- Approved assumptions: one fixed prototype starting-hub/base-like reinforcement affordance only; reuse existing recruitment/resource/army infrastructure where practical; labels/effect values may remain prototype-scoped.
- Updated EPIC-007, run-prompt index, guarded prompt, and Unity task pointer for implementation handoff.
- Workflow note from human: future approvals and verify-review-fix-merge-next-packet loops should be faster and less ruminative; next epic should consider larger stories or safe batched chunk review to reduce cycle time.

## [2026-06-18] merge | STORY-STRAT-BASE-001 starting hub reinforcement preview

- Reviewed and merged Unity PR #56 for `STORY-STRAT-BASE-001 Starting Hub Reinforcement Preview`.
- Merge-gate fixes before merge: trimmed trailing whitespace in new Unity `.meta` files and refreshed story evidence README CI status.
- Squash merge commit: `c49c52d86043bb2fdd0095223e3bcb890ea5dec6`.
- Exact-head PR Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27750164280
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27751021572
- Marked `STORY-STRAT-BASE-001` DONE and updated EPIC-007 child-story status.

## [2026-06-18] draft | STORY-STRAT-MAP-REGION-001 region/site presentation prototype

- Created `production/stories/story-strat-map-region-001-region-site-presentation-prototype.md` as the next proposed EPIC-007 packet.
- Created guarded prompt `production/sprints/codex-story-strat-map-region-001.prompt.txt`.
- Status is READY-candidate / approval pending. The prompt self-blocks until human approval promotes the story to READY.
- Proposed scope: one graph-backed region/site/corridor presentation prototype that improves HoMM-like spatial readability without changing strategic topology or adding tile/hex movement.
- Explicitly excludes tile/hex movement, pathfinding, fog/logistics/weather/supply, strategic AI, procedural/map editor work, new economy/base/tactical systems, final art/content, and graph replacement.

## [2026-06-18] verify | STORY-STRAT-MAP-REGION-001 candidate publish and Unity pointer clear

- Design/control publish CI passed for `STORY-STRAT-MAP-REGION-001` candidate packet: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27751683596
- Unity README pointer commit `82125506f6b45eb328872d0f8ff48f8b75661580` passed Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27751688521
- Unity README now states no READY / approved implementation task is active and points to the guarded `STORY-STRAT-MAP-REGION-001` candidate packet only.

## [2026-06-18] approval | STORY-STRAT-MAP-REGION-001 region/site presentation prototype

- Human approved `STORY-STRAT-MAP-REGION-001 Region/Site Presentation Prototype`.
- Promoted story from READY-candidate / approval pending to READY / approved.
- Approved assumptions: graph remains the authoritative strategic rules substrate; lightweight deterministic presentation fields/markers/labels/tints/coordinates are allowed; story improves spatial readability without introducing new mechanics.
- Updated EPIC-007, run-prompt index, guarded prompt, and Unity task pointer for implementation handoff.

## [2026-06-18] merge | STORY-STRAT-MAP-REGION-001 region/site presentation prototype

- Reviewed and merged Unity PR #57 for `STORY-STRAT-MAP-REGION-001 Region/Site Presentation Prototype`.
- Merge-gate fixes before merge: refreshed stale story evidence README CI status and marked draft PR ready for review.
- Squash merge commit: `ffe1dd68c61faa897f0ae4021b61aa12d77df924`.
- Exact-head PR Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27758159262
- Post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27759022977
- Marked `STORY-STRAT-MAP-REGION-001` DONE and updated EPIC-007 child-story status.

## [2026-06-18] draft | STORY-QA-008 strategic map region playtest and closeout review

- Created guarded closeout candidate `production/stories/story-qa-008-strategic-map-region-playtest-and-closeout-review.md`.
- Created guarded prompt `production/sprints/codex-story-qa-008.prompt.txt`.
- Status is READY-candidate / approval pending. The prompt self-blocks until human approval promotes the story to READY.
- Proposed scope: one narrow EPIC-007 closeout/review pass that verifies the merged strategic map readability/base/region-site surface at 1280x720 and fixes only concrete readability/clickability regressions found during review.
- Explicitly excludes new mechanics, tile/hex/freeform movement, pathfinding, fog/logistics/weather/supply, strategic AI, procedural/map editor work, base/economy/tactical system expansion, final art/content, and next-epic implementation.

## [2026-06-18] verify | STORY-QA-008 candidate publish and Unity pointer clear

- Design/control publish CI passed for `STORY-QA-008` guarded candidate packet: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27759595723
- Unity README pointer-clear commit `b8da4b50951fd9e471060f0f0f860deef0d5cf39` passed Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27759608451
- Unity README now states no READY / approved implementation task is active and points to guarded `STORY-QA-008` candidate only.

## [2026-06-18] approval | STORY-QA-008 strategic map region playtest and closeout review

- Human approved `STORY-QA-008 Strategic Map Region Playtest and Closeout Review`.
- Promoted story from READY-candidate / approval pending to READY / approved.
- Approved assumptions: run this closeout/review before starting another mechanics/design epic; Codex may fix concrete readability/clickability regressions directly tied to EPIC-007 commitments; broader next-epic direction remains human-owned after closeout verdict.
- Updated EPIC-007, run-prompt index, prompt, and Unity task pointer for implementation handoff.

## [2026-06-18] verify | STORY-QA-008 approval publish and Unity pointer

- Design/control publish CI passed for `STORY-QA-008` READY promotion: https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/27761239723
- Unity README pointer commit `753d1837593c45de8cea02beb92213de1a34d43d` passed Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27761243650
- Unity README now names `STORY-QA-008` as the current READY / approved implementation task.

## [2026-06-18] plan | EPIC-008 faction armies, recruitment, and tactical role identity

- Human selected next direction after EPIC-007 closeout: faction armies + recruitment + tactical role identity.
- Recorded accepted defaults: Home Rule Coalition vs QXZ Meridian; Home Rule is soft-canon/provisional; 3 unit lines per faction; QXZ owns the first Sensor Lock / Marked lane; fixed offers at starting hubs plus one neutral recruitment site; 4 medium-batched implementation slices plus QA closeout.
- Created `production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md` as approved/planned epic.
- Created `production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan.md`.
- Created `production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed.md` as READY-candidate / approval pending, not yet implementation-authorized.
- Created guarded candidate prompt `production/sprints/codex-story-army-001.prompt.txt`.

## [2026-06-18] approval | STORY-ARMY-001 MVP faction unit definitions and roster seed

- Human approved `STORY-ARMY-001 MVP Faction Unit Definitions and Roster Seed`.
- Promoted story from READY-candidate / approval pending to READY / approved.
- Recorded human-approved answers for Home Rule Coalition as provisional soft-canon name, Sled Logistics Team as support/mobility placeholder, QXZ Strato Sensor Swarm as future Sensor Lock lane, and neutral Survey Drones/Site Guards selection rule.
- Updated EPIC-008, planning note, run-prompt index, checked-in Codex prompt, and implementation handoff state.

## [2026-06-18] merge | STORY-ARMY-001 and prepare STORY-ARMY-002 candidate

- Verified, gate-fixed, and merged Unity PR #60 for `STORY-ARMY-001 MVP Faction Unit Definitions and Roster Seed`.
- Merge-gate blocker fixed before merge: unit definition IDs now match the approved story literals (`settlement_watch`, `sled_logistics_team`, `hunter_scouts`, `meridian_security`, `strato_sensor_swarm`, `climate_bulwark`, `survey_drones`, `site_guards`).
- Unity PR #60 final gate-fix head: `ba2d3103d410decdeca85af6d9c0ff83af1238e0`.
- Unity merge commit: `3c3158ce1e06bf63c19f1d1f5b7e0024a32e29e1`.
- Exact-head Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27775537496.
- Post-merge Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27776429736.
- Created `production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock.md` as READY-candidate / approval pending.
- Created guarded prompt `production/sprints/codex-story-army-002.prompt.txt`; it self-blocks until ARMY-002 is explicitly approved.

## [2026-06-18] approval | STORY-ARMY-002

- Promoted `STORY-ARMY-002 Tactical Role Behaviors and Sensor Lock` to READY / approved after human approval.
- Approved Sensor Lock effect: Strato Sensor Swarm applies a separate 1 AP support action; the next successful attack against the marked target deals +1 stack-count damage and consumes the mark.
- Home Rule counterplay remains deferred.
- Sled Logistics Team remains visible support/mobility role only; no special mobility ability in ARMY-002.
- Activated prompt `production/sprints/codex-story-army-002.prompt.txt`.
