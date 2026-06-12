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
