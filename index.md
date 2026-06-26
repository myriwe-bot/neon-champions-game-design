# Neon Champions Game Design Index

> Last updated: 2026-06-25
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
- [[design/research/homm-like-tactical-battle-ui-reference]] — HoMM-like tactical battle UI/readability references: stack counts, event feed, movement/attack affordances, retaliation.
- [[design/research/homm-like-strategic-map-topology-reference]] — HoMM-like strategic/adventure map topology references: node, region, tile/hex, bases, guarded sites.
- [[design/research/homm-town-building-reference]] — HoMM3 and Olden Era town/building/dwelling reference for Neon Champions base facilities.

## World Import Layer

- [[design/world/lore-import-policy]] — rules for importing world wiki content.
- [[design/world/approved-world-slice]] — approved game-facing lore summary scaffold.
- [[design/world/faction-game-briefs]] — faction design-brief scaffold.

## Production Planning

- [[production/planning/prototype-readability-and-map-next-steps-2026-06-15]] — draft next-steps plan after prototype readability/reference review: tactical stack labels/event feed, retaliation, movement/attack affordances, unit data, AP/Defend, neutral AI, strategic map readability, bases, and region/site map evolution.
- [[production/epics/epic-template]] — epic template.
- [[production/epics/epic-strat-mvp-001-strategic-mvp-core-loop]] — implemented parent epic for the first strategic MVP core loop stories.
- [[production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat]] — DONE larger map/bases/recruitment/minimal tactical combat vertical slice.
- [[production/stories/story-template]] — story template.
- [[production/stories/story-strat-001-scenario-map-graph-state]] — READY first strategic MVP implementation story for scenario/map graph state.
- [[production/stories/story-strat-002-hotseat-turn-ownership]] — READY next story for deterministic local-hotseat turn ownership.
- [[production/stories/story-strat-003-champion-route-movement]] — READY next story for single-route Champion movement.
- [[production/stories/story-strat-vis-001-minimal-strategic-map-presentation]] — READY minimal strategic map presentation story.
- [[production/stories/story-strat-input-001-select-champion-and-route-move]] — READY select-and-route-move input story.
- [[production/stories/story-strat-ui-001-minimal-hotseat-hud]] — READY minimal hotseat HUD story.
- [[production/stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke]] — READY local hotseat strategic loop smoke story.
- [[production/stories/story-tac-001-battle-setup-result-dto-contracts]] — DONE/merged tactical boundary DTO story with clarified strategic-map §14 authority.
- [[production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger]] — DONE/merged guarded-site interaction and BattleSetup launch story.
- [[production/stories/story-tac-002-minimal-hex-board-and-stack-placement]] — DONE/merged minimal hex board and stack placement story.
- [[production/stories/story-tac-003-minimal-tactical-movement-and-attack-resolution]] — DONE/merged minimal tactical movement and attack resolution story.
- [[production/stories/story-tac-vis-001-minimal-tactical-board-presentation-and-handoff-switch]] — DONE/merged visible tactical board presentation and handoff switch story.
- [[production/stories/story-tac-004-minimal-battle-end-and-result-return]] — DONE/merged minimal battle end and BattleResult return story.
- [[production/stories/story-loop-002-visible-guarded-site-capture-smoke]] — DONE/merged visible guarded-site capture smoke story.
- [[production/stories/story-tac-005-basic-tactical-player-controls]] — DONE/merged basic tactical player controls story.
- [[production/stories/story-map-001-larger-two-base-strategic-map-slice]] — DONE/merged larger two-base strategic map slice.
- [[production/stories/story-strat-006-simple-recruitment-site-fixed-offer]] — DONE/merged simple recruitment site and fixed normal/upgraded offers implementation packet.
- [[production/stories/story-loop-003-larger-map-recruitment-and-neutral-capture-vertical-slice]] — DONE/merged larger-map recruitment and neutral-capture connected smoke story.
- [[production/stories/story-tac-006-multi-stack-attacker-tactical-setup]] — DONE/merged tactical setup prerequisite for recruited multi-stack attacker armies.
- [[production/stories/story-qa-003-loop-slice-visual-readability-and-clickable-layout-pass]] — DONE/merged visual/readability and clickable-layout pass for the connected loop slice.
- [[production/stories/story-qa-004-playability-map-scale-zoom-and-ui-clarity-pass]] — DONE/merged playability pass for map scale, zoom/focus, overlapping labels, unobstructed buttons, and click/action clarity.
- [[production/epics/epic-vslice-mvp-003-scenario-objective-champion-combat-and-casualty-stakes]] — DONE objective, Champion combat path, defender tiers, and simple HP/strength casualty stakes epic.
- [[production/epics/epic-vslice-mvp-004-intel-resource-on-ramp]] — DONE Intel resource on-ramp epic.
- [[production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp]] — COMPLETE / human closeout accepted after repair train.
- [[production/epics/epic-vslice-mvp-006-tactical-battle-readability-and-defender-agency]] — IMPLEMENTATION COMPLETE / awaiting human closeout tactical battle readability and defender agency epic.
- [[production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation]] — DONE / closed strategic readability, starting-hub reinforcement, region/site presentation, and closeout review epic.
- [[production/stories/story-cmd-001-champion-command-archetype-state-and-tactical-hud]] — DONE first Champion Command story.
- [[production/stories/story-cmd-002-first-marshal-and-operator-command-pair]] — DONE first active Marshal/Operator Command spending story.
- [[production/stories/story-cmd-003-command-on-ramp-closeout-smoke]] — DONE Champion Command on-ramp closeout smoke story.
- [[production/stories/story-cmd-004-tactical-command-usability-and-targeting-pass]] — DONE tactical command usability and targeting story.
- [[production/sprints/epic-005-playability-repair-train]] — DONE repair train after human playtest.
- [[production/stories/story-qa-006-strategic-tactical-state-action-feedback-readability-pass]] — DONE cross-mode state/action feedback readability story.
- [[production/stories/story-qa-007-champion-encounter-initiation-clarity]] — DONE Champion encounter clarity story.
- [[production/stories/story-cmd-005-champion-command-explanation-pass]] — DONE command explanation story.
- [[production/stories/story-strat-objective-001-multi-turn-objective-contest-direction]] — DONE merged objective contest countdown story.
- [[production/stories/story-tac-read-002-tactical-stack-labels-and-combat-event-feed]] — DONE / merged first EPIC-006 tactical stack labels and HoMM-like combat event feed story.
- [[production/stories/story-tac-ret-001-minimal-melee-retaliation]] — DONE / merged EPIC-006 story for minimal melee retaliation and defender agency.
- [[production/stories/story-tac-afford-001-movement-and-attack-affordance-pass]] — DONE / merged EPIC-006 story for tactical movement and attack affordance clarity.
- [[production/stories/story-tac-unit-001-minimal-unit-definition-stats]] — DONE / merged EPIC-006 story for minimal unit definition stats.
- [[production/stories/story-tac-ap-001-minimal-tactical-ap-and-defend-state]] — DONE / merged EPIC-006 story for minimal tactical AP and Defend state with tiny prototype Defend damage reduction.
- [[production/stories/story-tac-ai-001-neutral-guard-one-step-combat-ai]] — DONE / merged EPIC-006 story for neutral guard one-step CombatAI.
- [[production/stories/story-strat-read-002-strategic-map-readability-pass]] — DONE / merged EPIC-007 story for strategic map readability.
- [[production/stories/story-strat-base-001-starting-hub-reinforcement-preview]] — DONE / merged EPIC-007 story for starting hub reinforcement preview.
- [[production/stories/story-strat-map-region-001-region-site-presentation-prototype]] — DONE / merged EPIC-007 story for region/site presentation.
- [[production/stories/story-qa-008-strategic-map-region-playtest-and-closeout-review]] — DONE / merged EPIC-007 closeout review.
- [[production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity]] — DONE / closed faction armies, recruitment, and tactical role identity epic.
- [[production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction]] — APPROVED / PLANNED strategic map geography, bases, and simple facility construction epic.
- [[production/stories/story-map-real-001-scenario-authored-strategic-map-shell]] — DONE / merged first EPIC-009 story.
- [[production/stories/story-base-001-base-definition-and-facility-construction-core]] — READY-candidate / approval pending next EPIC-009 story.
- [[production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan]] — approved EPIC-008 slice plan and roster seed.
- [[production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed]] — DONE / merged first EPIC-008 story for MVP faction unit definitions and roster seed.
- [[production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock]] — DONE / merged EPIC-008 story for tactical role behaviors and Sensor Lock.
- [[production/stories/story-army-003-fixed-recruitment-offers-and-army-summary]] — DONE / merged EPIC-008 packet for fixed recruitment offers and army summary.
- [[production/stories/story-army-004-composition-consequence-scenario]] — DONE / merged EPIC-008 packet for composition consequence scenario.
- [[production/stories/story-qa-009-epic-008-playtest-and-closeout-review]] — DONE / merged EPIC-008 closeout review packet; later superseded by human playtest rejection.
- [[production/stories/story-army-005-army-recruitment-and-map-readability-repair]] — DONE / merged repair packet for army, recruitment, tactical stack, and map readability.
- [[production/stories/story-qa-010-epic-008-repair-playtest-and-closeout-review]] — DONE / closeout rejected after repair playtest.
- [[production/stories/story-army-006-map-camera-recruitment-and-tactical-stack-interaction-repair]] — DONE / merged repair for pan/zoom persistence, recruitment truthfulness, and tactical drone interaction.
- [[production/stories/story-qa-011-epic-008-second-repair-playtest-and-closeout-review]] — DONE / one narrow follow-up second repair playtest closeout.
- [[production/planning/strategic-map-realism-brief-2026-06-25]] — DRAFT / design-only realistic strategic map and EPIC-009 base-facility planning brief.
- [[production/stories/story-obj-001-scenario-objective-state-and-victory-feedback]] — DONE / merged first story for visible objective state and victory feedback.
- [[production/stories/story-obj-002-guarded-site-defender-strength-tiers]] — DONE / merged follow-up for weak/standard/strong defender tiers.
- [[production/stories/story-tac-007-simple-stack-strength-persistence]] — DONE / merged simple stack HP/strength persistence story.
- [[production/stories/story-tac-008-champion-vs-champion-tactical-encounter-path]] — DONE / merged Champion-vs-Champion tactical encounter path.
- [[production/stories/story-loop-004-objective-champion-combat-and-casualty-stakes-smoke]] — DONE / merged connected smoke for objective, Champion combat, and casualty stakes.
- [[production/stories/story-intel-001-faction-intel-and-data-cache-pickup]] — DONE / merged faction Intel and one data-cache pickup.
- [[production/stories/story-intel-002-first-intel-spending-sink-field-upgrade]] — DONE / merged first narrow Intel spend sink.
- [[production/stories/story-intel-003-guarded-data-site-intel-reward]] — DONE / merged guarded Intel reward path.
- [[production/stories/story-intel-004-intel-on-ramp-closeout-smoke]] — DONE / merged connected Intel closeout smoke.
- [[production/stories/story-ux-001-strategic-map-readability-action-clarity-pass]] — DONE / merged strategic-map readability/action clarity pass.
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

- [[production/stories/story-qa-005-playmode-evidence-artifact-hygiene|STORY-QA-005 PlayMode Evidence Artifact Hygiene]] — DONE / merged maintenance story after UX-001 merge.

- [[production/stories/story-army-007-strategic-map-pan-input-repair]] — DONE / merged final EPIC-008 pan input repair.
