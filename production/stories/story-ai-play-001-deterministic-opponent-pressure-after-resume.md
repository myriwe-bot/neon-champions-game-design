---
title: STORY-AI-PLAY-001 Deterministic Opponent Pressure After Resume
type: story
status: ready
phase: production
owner: shared
created: 2026-07-16
updated: 2026-07-16
approval: approved
related: [production/epics/epic-017-fully-playable-prototype-continuity-and-opponent-pressure, production/stories/story-ai-001-dumb-strategic-ai-playtest-opponent, production/stories/story-save-001-prototype-strategic-save-and-resume, docs/architecture/determinism-and-rng-adr, docs/architecture/prototype-strategic-save-resume-adr, docs/architecture/control-manifest, docs/architecture/testing-strategy]
---

# STORY-AI-PLAY-001 Deterministic Opponent Pressure After Resume

## Status

READY / approved on 2026-07-17. Human approval accepts the recommended priority order and the strict-greater aggregate-count battle proxy exactly as written. Implementation becomes runnable only after the Unity pointer activation gate passes.

## Parent epic

- `EPIC-017 Fully Playable Prototype Continuity and Opponent Pressure`.

## Player/system value

As a solo player, I need the strategic opponent to make legible choices from the exact resumed state, so saving and continuing does not reduce the match to route-order behavior or change what the opponent would do next.

## Approved baseline

- `STORY-AI-001` provides a deterministic but deliberately crude first-legal-route opponent.
- `STORY-SAVE-001` provides complete strategic-state persistence and deterministic continuation.
- Unity PR #162 preserves save-era Feed and migration state during failed-AI-turn rollback.
- The determinism ADR keeps unseeded and seeded randomness out of this story.

## Human-approved policy

Replace route-list-order choice with a small deterministic candidate-ranking policy. On one AI turn, evaluate legal actions from the active runtime state in this order:

1. preserve or contest the central objective when a legal move or interaction does so;
2. initiate an existing legal battle only when a visible-state proxy is favorable: the active army's aggregate current unit count is strictly greater than the visible opposing/guard aggregate count;
3. buy one legal affordable recruitment offer, preferring the largest aggregate unit-count gain, then lower effective Credits cost, then ordinal offer ID;
4. claim one safe unconsumed one-time reward/site interaction;
5. move along the legal route that minimizes remaining unweighted route hops to the central objective;
6. if no candidate is legal, end turn with a readable reason.

Within a tier, use explicit ordinal IDs as the final tie-break. Never rely on source list/dictionary iteration order. The AI may perform at most one movement plus one major interaction/recruitment in a turn. A battle launch pauses strategic completion and uses the existing tactical handoff; this story does not auto-resolve tactical combat.

## In scope

- Introduce a pure/read-only candidate enumeration and ranking boundary for the current strategic AI.
- Use current scenario definitions plus the restored `ScenarioRuntimeState`; do not reconstruct state from scenario defaults.
- Support central-objective pressure, safe site value, one affordable recruitment choice, and the bounded favorable-battle proxy above where current legal preview data exposes both forces.
- Preserve atomic rollback across every mutable runtime collection if execution fails.
- Keep action summaries player-readable; raw IDs may appear only in diagnostics/debug/evidence metadata.
- Prove a save/continue path produces the same ranked AI choice and next runtime state as an equivalent unsaved path.
- Add 1920x1080 evidence showing the opponent action and resulting pressure in the normal shell.

## Out of scope

- Randomness, learning, minimax, search trees, personalities, diplomacy, fog/hidden-information cheating, economic forecasting, multi-turn plans, or difficulty levels.
- New combat odds, tactical auto-resolution, or tactical `CombatAI` rewrite.
- New map topology, units, factions, scenario balance, objective rules, save schema, or persistence fields.
- More than one move and one major action per AI turn.
- Human playtest closeout; `STORY-PROTOTYPE-CONTINUITY-QA-001` remains separate.

## Acceptance criteria

- [ ] AI candidate generation is read-only and deterministic for the same scenario/runtime input.
- [ ] Choice uses the approved tier order and explicit ordinal tie-breaks, never route/source collection order.
- [ ] AI can choose a useful affordable recruitment offer and applies its real costs, stock, army, and major-action effects through existing services.
- [ ] AI moves toward or contests the central objective when higher-tier legal pressure exists.
- [ ] AI launches only battles that satisfy the approved visible aggregate-count proxy; unavailable force comparison makes that battle candidate ineligible.
- [ ] Battle launch uses the existing tactical handoff and does not incorrectly end/advance the strategic turn.
- [ ] Failed execution restores all mutable strategic state, including Feed consequences and migration diagnostics.
- [ ] Save -> Continue -> AI turn matches the equivalent unsaved AI choice and resulting runtime state.
- [ ] No entropy APIs or unordered iteration determine choices.
- [ ] Normal-shell action text is readable at 1920x1080 and does not expose raw IDs or paths.
- [ ] Focused EditMode/PlayMode tests, full suites, validators, standalone build, exact-head CI, and evidence pass.

## Verification matrix

- Candidate tier and tie-break tests with deliberately reordered scenario/runtime collections.
- Recruitment: affordable, unaffordable, exhausted, locked, and tie-break cases.
- Objective: already holding, enemy holding, neutral, and no legal route cases.
- Battle: favorable, equal, unfavorable, missing visible comparison, and pending tactical handoff cases.
- Rollback: injected post-action turn failure preserves every mutable runtime collection.
- Continuity: equivalent saved/resumed and unsaved states choose the same action and produce equivalent runtime state.
- Player shell: opponent summary and pressure visible/readable at 1920x1080; no raw IDs.
- `git diff --check`, asset/`.meta` pairing, focused/full Unity suites, validators, standalone Windows build, exact-head PR CI, and post-merge main CI.

## Dependencies

- `STORY-AI-001`: DONE / merged.
- `STORY-SAVE-001`: DONE / merged through Unity PR #161.
- AI rollback continuity hotfix: merged through Unity PR #162.
- Human approval of the policy in this packet: approved on 2026-07-17 as written.
- Unity README pointer activation: merged through PR #165 as `a2312752544fd3370addccc07f821769abe02653`; exact-head CI 29557773784 and post-merge main CI 29558124758 passed.

## Ambiguity check

Status: PASS. The policy, priority order, and strict-greater aggregate-count battle proxy were human-approved on 2026-07-17.

Human-approved answer:

- Use the recommended strict-greater aggregate-count battle proxy and priority order exactly as written.

## Branch / PR requirements

- Branch: `story/STORY-AI-PLAY-001-deterministic-opponent-pressure-after-resume`
- PR title: `STORY-AI-PLAY-001 deterministic opponent pressure after resume`
- Evidence: `production/evidence/STORY-AI-PLAY-001/`
- Non-draft PR required.

## Readiness gate

- [x] Stable ID, parent epic, player value, scope, exclusions, and verification are explicit.
- [x] Existing AI/save/determinism authority is linked.
- [x] Proposed deterministic policy is concrete and testable.
- [x] Human approved the proposed policy.
- [x] Status changed to READY / approval approved.
- [x] Unity pointer activated and exact-head/post-merge pointer CI passed.

## Verdict

READY / approved. Implement only from the activated Unity pointer on current `main`.
