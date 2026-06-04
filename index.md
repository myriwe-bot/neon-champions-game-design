# Neon Champions Game Design Index

> Last updated: 2026-06-04
> Current phase: Phase 1 — Concept
> Review mode: Lean default, Full for major gates

## Start Here

- [[README]] — repository purpose and separation from worldbuilding.
- [[SCHEMA]] — document statuses, traceability, and metadata rules.
- [[production/gates/review-mode]] — selected review mode and gate policy.
- [[design/game-design-principles]] — design principles and workflow lenses.
- [[design/workflow]] — phase workflow adapted from Claude Code Game Studios.

## Concept and GDDs

- [[design/gdd/README]] — GDD reading guide for humans and LLM agents.
- [[design/gdd/game-concept]] — current draft concept: HoMM3-inspired cyberpunk strategy/RPG beginning with Greenland during Blue Monday, later remembered as the start of Blue Week.
- [[design/gdd/game-pillars]] — current draft pillars and anti-pillars, including Intel, infrastructure power, dirty information, and wilderness without escapism.
- [[design/gdd/systems-index]] — system map scaffold.
- [[design/gdd/strategic-map]] — strategic-map MVP scope: two-faction local hotseat, duel/race scenario pacing, site control, resources, recruitment/reinforcement, and tactical battle handoff.
- [[design/gdd/intel-resource]] — draft system GDD for Intel as Neon Champions' Alchemical Dust analogue.
- [[design/gdd/faction-unit-rosters]] — draft unit roster concepts and faction tactical identities for the Greenland campaign.
- [[design/gdd/tactical-combat]] — concise active tactical combat GDD for first-read design and AI implementation planning.
- [[design/gdd/tactical-combat/section-map]] — preservation map for the tactical-combat split; confirms every original top-level section is still present in smaller articles.

### Tactical Combat Detailed Articles

- [[design/gdd/tactical-combat/overview-and-scope]]
- [[design/gdd/tactical-combat/army-deployment-and-stacks]]
- [[design/gdd/tactical-combat/ap-actions-and-reactions]]
- [[design/gdd/tactical-combat/targeting-damage-and-defense]]
- [[design/gdd/tactical-combat/statuses-terrain-and-objectives]]
- [[design/gdd/tactical-combat/morale-rout-and-cohesion]]
- [[design/gdd/tactical-combat/post-battle-resolution]]
- [[design/gdd/tactical-combat/ammo-capacity-and-logistics]]
- [[design/gdd/tactical-combat/champion-operations-and-progression]]
- [[design/gdd/tactical-combat/implementation-contracts]]
- [[design/gdd/tactical-combat/mvp-content-and-faction-rosters]]
- [[design/gdd/tactical-combat/deferred-and-open-questions]]

## Research / Deep Reference

- [[design/research/commander-spellbook-reference]] — commander/spellbook/operations reference research.
- [[design/research/tactical-combat-deep-reference]] — preserved long-form tactical-combat packet history and rationale; reference only, not first-read implementation contract.

## World Import Layer

- [[design/world/lore-import-policy]] — rules for importing world wiki content.
- [[design/world/approved-world-slice]] — approved game-facing lore summary scaffold.
- [[design/world/faction-game-briefs]] — faction design-brief scaffold.

## Production Planning

- [[production/epics/epic-template]] — epic template.
- [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop]] — approved parent epic for the first strategic MVP core loop stories.
- [[production/stories/story-template]] — story template.
- [[production/stories/story-strat-001-scenario-map-graph-state]] — READY first strategic MVP implementation story for scenario/map graph state.
- [[production/stories/story-strat-002-hotseat-turn-ownership]] — READY next story for deterministic local-hotseat turn ownership.
- [[production/stories/story-strat-003-champion-route-movement]] — READY next story for single-route Champion movement.
- [[production/stories/story-strat-vis-001-minimal-strategic-map-presentation]] — READY minimal strategic map presentation story.
- [[production/stories/story-strat-input-001-select-champion-and-route-move]] — READY select-and-route-move input story.
- [[production/stories/story-strat-ui-001-minimal-hotseat-hud]] — READY minimal hotseat HUD story.
- [[production/stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke]] — READY local hotseat strategic loop smoke story.
- [[production/stories/story-tac-001-battle-setup-result-dto-contracts]] — DONE/merged tactical boundary DTO story with clarified strategic-map §14 authority.
- [[production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger]] — READY guarded-site interaction and BattleSetup launch story.
- [[production/sprints/strategic-mvp-closeout-story-train-002]] — approved closeout train from guarded-site interaction through visible capture smoke.
- [[production/sprints/strategic-mvp-story-train-001]] — Codex-safe sequential implementation train for the next strategic MVP stories.
- [[production/sprints/strategic-mvp-codex-execution-system]] — approved Codex execution system and story-specific prompt wrappers for the strategic MVP train.
- [[production/sprints/strategic-mvp-codex-run-prompts]] — exact PowerShell commands and Codex prompts for running the next strategic MVP implementation stories.
- [[production/gates/gate-template]] — phase/artifact/story gate template.
- [[production/spikes/spike-001-unity-project-ci-foundation]] — approved first Unity technical foundation spike.
- [[production/checklists/codex-pr-review-checklist]] — future implementation PR review checklist for Codex/agents.

## Architecture

- [[docs/architecture/control-manifest]] — agent implementation rules scaffold.
- [[docs/architecture/architecture]] — architecture scaffold.
- [[docs/architecture/unity-technical-scheme]] — Unity technical boundaries and defaults.
- [[docs/architecture/technical-decision-priorities]] — technical decision gate priorities.
- [[docs/architecture/data-authoring-options]] — data authoring options and phased-hybrid decision.
- [[docs/architecture/testing-strategy]] — strict layered testing ADR.
- [[docs/architecture/ci-build-automation]] — strict CI/build automation ADR.
- [[docs/architecture/merge-to-main-gate]] — approved workflow for rigorous PR merge gates before implementation branches land on main.
- [[docs/architecture/codex-agent-instructions]] — researched Codex/AGENTS.md instruction strategy.
- [[docs/architecture/unity-repo-agents-template]] — approved starting template for future Unity repo AGENTS.md files.
- [[docs/architecture/multi-agent-operating-model]] — role/gate/worktree model for using many agents safely.

## Logs

- [[log]] — chronological repository log.
