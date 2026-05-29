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
