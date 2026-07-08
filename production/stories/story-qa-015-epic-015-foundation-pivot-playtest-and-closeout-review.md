---
title: STORY-QA-015 EPIC-015 Foundation Pivot Playtest and Closeout Review
type: story
status: ready
phase: production
owner: shared
created: 2026-07-08
updated: 2026-07-08
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    production/stories/story-data-001-static-scenario-data-contract-and-scenario-extraction-prep,
    production/stories/story-playtest-001-playtest-journal-and-gate-hook,
    production/stories/story-gate-001-hollow-gate-and-source-truth-reconciliation,
    production/stories/story-determinism-001-determinism-and-rng-decision-record,
    production/stories/story-ai-001-dumb-strategic-ai-playtest-opponent,
    production/planning/post-audit-foundation-pivot-2026-07-03,
    docs/architecture/data-scenario-save-format-adr,
    docs/architecture/determinism-and-rng-adr,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    design/gdd/strategic-map,
  ]
approval: approved
---

# STORY-QA-015 EPIC-015 Foundation Pivot Playtest and Closeout Review

## Status

READY / approved. Prepared 2026-07-08 after `STORY-AI-001` merged through Unity PR #141 and post-merge `main` CI passed. This is a narrow Unity QA/playtest closeout packet for EPIC-015, not a new feature train.

## Story type

QA / Playability Review + Closeout Gate.

## Parent epic

- `production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation.md`.

## User/player/system value

As project director, I need the post-audit foundation pivot reviewed as one playable/control surface after data extraction, playtest journal/gate hooks, hollow-gate reconciliation, determinism policy, and dumb strategic AI have landed, so we can decide whether EPIC-015 closes or needs one narrow repair before the next capability train.

## Source requirements

- Parent epic: `production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation.md`.
- Pivot brief: `production/planning/post-audit-foundation-pivot-2026-07-03.md`.
- Merged child stories and evidence:
  - `STORY-DATA-001` / Unity PR #138.
  - `STORY-PLAYTEST-001` / game-design PR #1.
  - `STORY-GATE-001` / game-design PR #2.
  - `STORY-DETERMINISM-001` / game-design PR #3.
  - `STORY-AI-001` / Unity PR #141.
- `docs/architecture/data-scenario-save-format-adr.md`.
- `docs/architecture/determinism-and-rng-adr.md`.
- `production/playtests/playtest-journal.md`.
- `production/reconciliation/hollow-gates-and-source-truth-2026-07-05.md`.
- `design/gdd/strategic-map.md`.
- `docs/architecture/control-manifest.md`, `testing-strategy.md`, and `ci-build-automation.md`.

## In scope

If approved/run, this story may:

- Run/review current Unity `main` at 1280x720 against the complete EPIC-015 surface.
- Inspect the current scenario data path and confirm the checked-in smoke scenario still loads from reviewable data without gameplay drift.
- Inspect the human -> dumb strategic AI -> human turn cycle and confirm AI control/action status is player-visible.
- Inspect that deterministic-by-default policy is not contradicted by new runtime random/entropy use.
- Confirm playtest journal and hollow-gate/source-truth outputs are discoverable from design/control docs.
- Fix only concrete closeout blockers directly tied to EPIC-015 commitments, such as broken AI turn smoke, stale pointer/evidence wording, missing visibility text, or a regression in scenario data loading.
- Add or update focused Unity evidence under `production/evidence/STORY-QA-015/` if a Unity PR is opened.
- Produce a closeout verdict recommending exactly one of: `CLOSE EPIC-015`, `ONE NARROW FOLLOW-UP`, or `REJECT CLOSEOUT / NEEDS HUMAN PLAYTEST`.

## Out of scope

Not authorized by this story:

- No sophisticated strategic AI, utility scoring, planning, personality, diplomacy, fog/dirty-information reasoning, deception, or hidden-info rolls.
- No new campaign mode, scenario generator, save/load UI, replay system, map/scenario editor, or meta-progression.
- No new map topology, factions, sites, objectives, resources, facilities, recruitment offers, balance changes, final content/lore names, art/audio/VFX/icons/localization/accessibility framework.
- No tactical CombatAI changes or new tactical mechanics.
- No new Intel/dirty-information mechanics beyond checking that existing pivot outputs remain honest and discoverable.
- No next-epic implementation story promotion without separate human direction.

## Acceptance criteria

- [ ] The merged EPIC-015 surface is reviewed on current Unity `main` at 1280x720.
- [ ] The review explicitly addresses scenario data loading, dumb StrategicAI turn cycle, deterministic/no-randomness policy, playtest journal hook, and hollow-gate/source-truth reconciliation discoverability.
- [ ] Any concrete in-scope closeout blockers are fixed narrowly, or the story records why no fix was needed.
- [ ] Evidence under Unity `production/evidence/STORY-QA-015/` documents the inspected surface if a Unity PR is opened.
- [ ] Exact-head Unity Foundation CI passes before merge if any Unity PR is opened.
- [ ] Closeout verdict is recorded: `CLOSE EPIC-015`, `ONE NARROW FOLLOW-UP`, or `REJECT CLOSEOUT / NEEDS HUMAN PLAYTEST`.

## Verification requirements

- `git diff --check`.
- Placeholder validator remains green.
- Focused EditMode tests pass if any domain/application/scenario data changes are made.
- PlayMode smoke tests pass if any Unity code/UI/evidence changes are made.
- Runtime entropy scan still finds no unapproved `UnityEngine.Random`, `System.Random`, `Random.Range`, `Guid.NewGuid`, `DateTime.Now`, or `DateTime.UtcNow` under `Assets/NeonChampions/Runtime`.
- Standalone Windows64 build passes if a Unity PR is opened and the workflow runs it.
- Exact-head Unity Foundation CI before merge and post-merge main CI after merge if implemented as a Unity branch.
- If no code changes are needed, closeout documentation must still record what was inspected and why no fix was needed.

## Ambiguity Check

Status: PASS. Implementation authority granted for a narrow EPIC-015 playtest/closeout review only.

Human-approved answers / assumptions:

- User asked 2026-07-08 to verify/review/fix/merge `STORY-AI-001`, then prepare the next implementation packet.
- The safe next packet is EPIC-015 closeout review, because all approved EPIC-015 child outputs have now landed.
- Scope is review and narrow repair only; do not start a new capability train or broaden AI/data/save/editor work.

## Branch / PR requirements

- Branch name: `story/STORY-QA-015-epic-015-foundation-pivot-closeout-review`.
- PR title: `STORY-QA-015 EPIC-015 foundation pivot closeout review`.
- Required linked story ID: `STORY-QA-015`.
- Required evidence path: `production/evidence/STORY-QA-015/` in Unity if a Unity PR is opened.
- Required verdict section: close epic, one narrow follow-up, or reject closeout / needs human playtest.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Source requirements are linked.
- [x] In-scope work is bounded.
- [x] Out-of-scope work is explicit.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval for next-packet preparation has been recorded.

## Verdict

READY / approved. Run only the narrow EPIC-015 closeout review and direct blocker-fix scope. Do not promote or implement the next capability train from this packet.
