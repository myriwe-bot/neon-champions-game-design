---
title: STORY-QA-013 EPIC-010 Playtest and Closeout Review
type: story
status: ready
phase: production
owner: shared
created: 2026-06-29
updated: 2026-06-29
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability,
    production/stories/story-terrain-001-strategic-terrain-tags-and-tactical-layout-family-contract,
    production/stories/story-terrain-002-tactical-layout-definitions-and-deployment-zones,
    production/stories/story-terrain-003-tactical-blockers-and-simple-defensive-terrain,
    production/stories/story-terrain-004-range-threat-and-terrain-readability-pass,
    production/stories/story-terrain-005-strategic-context-to-tactical-battlefield-smoke,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-QA-013 EPIC-010 Playtest and Closeout Review

## Status

READY / approved for Unity implementation. Human approval recorded 2026-06-29: "Approved". This approves the listed QA/playability closeout scope, narrow-fix allowance, exclusions, branch/PR requirements, and verification requirements as written.

## Story type

QA / Playability Review + Narrow Fix Pass.

## Parent epic

- [EPIC-VSLICE-MVP-010 Terrain, Tactical Battlefields, and Map-Space Readability](../epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md)

## User/player/system value

As project director, I need the now-merged EPIC-010 terrain/context implementation reviewed as one playable surface before EPIC-010 is closed or a new mechanics train starts.

## Source requirements

- Parent epic: `production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md`.
- Merged story evidence in Unity:
  - `production/evidence/STORY-TERRAIN-001/`
  - `production/evidence/STORY-TERRAIN-002/`
  - `production/evidence/STORY-TERRAIN-003/`
  - `production/evidence/STORY-TERRAIN-004/`
  - `production/evidence/STORY-TERRAIN-005/`
- GDD/control:
  - `design/gdd/strategic-map.md` §§1-10.
  - `design/gdd/tactical-combat.md` §§3-6 and §6.2A.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

If approved, this story may:

- Review/run current Unity `main` at 1280x720 against the EPIC-010 terrain/context surface.
- Inspect the complete terrain chain together:
  - strategic terrain/context identity;
  - tactical layout-family selection from strategic context;
  - tactical deployment zones;
  - blocked terrain and simple defensive/readability-only terrain;
  - range/threat/terrain readability;
  - strategic site/context handoff into tactical presentation for at least two contexts.
- Fix only concrete player-facing readability/clickability/evidence regressions directly tied to EPIC-010 commitments, such as unreadable terrain/deployment/range labels, misleading context handoff summaries, missing evidence for required terrain states, or stale CI/evidence wording.
- Add or update PlayMode smoke tests and PNG/text evidence under `production/evidence/STORY-QA-013/` if a fix is made or if the closeout review needs new evidence.
- Produce a concise closeout verdict recommending one of:
  - `CLOSE EPIC-010`;
  - `ONE NARROW FOLLOW-UP`;
  - `REJECT CLOSEOUT / NEEDS HUMAN PLAYTEST`.

## Out of scope

Not authorized by this story:

- No new strategic terrain movement costs, movement-type rules, supply/logistics, weather, fog, stealth/reveal, scouting uncertainty, strategic AI terrain valuation, topology rewrite, procedural maps, or map editor UI.
- No new tactical combat mechanics: damage, AP, Defend, retaliation, Sensor Lock, CombatAI changes, objectives, elevation, line-of-sight rewrite, cover system, hazards, overwatch, destructible terrain, facing, accuracy, or balance expansion.
- No new strategic nodes, routes, sites, factions, resources, facilities, recruitment offers, win/loss rules, or battle-result rules.
- No broad UI redesign, final art/icons/VFX/audio/localization, or next-epic implementation story promotion without separate human approval.

## Allowed placeholders

- Existing prototype labels, colors, debug markers, and screenshot style may remain if they are readable enough for closeout judgment.
- Evidence-only labels/captures are allowed if generated from real runtime/presentation state and not treated as new design authority.

## Acceptance criteria

- [ ] The merged EPIC-010 terrain/context surface can be reviewed on current Unity `main` at 1280x720.
- [ ] The review explicitly addresses strategic context tags, tactical layout family, deployment zones, blocked terrain, defensive terrain, legal moves, legal attack targets, out-of-range/non-attackable enemies, and strategic-to-tactical handoff readability.
- [ ] Any concrete in-scope closeout blocker discovered is fixed narrowly and covered by PlayMode/regression evidence.
- [ ] Evidence under `production/evidence/STORY-QA-013/` documents the final inspected surface if a Unity PR is opened or if new closeout evidence is needed.
- [ ] Unity Foundation CI passes at exact PR head before merge if Unity changes are made.
- [ ] Closeout verdict is recorded: `CLOSE EPIC-010`, `ONE NARROW FOLLOW-UP`, or `REJECT CLOSEOUT / NEEDS HUMAN PLAYTEST`.

## Verification requirements

- Placeholder validator remains green.
- EditMode tests pass if any application/domain/projection changes are made.
- PlayMode tests pass if any Unity code/UI/evidence changes are made.
- Standalone Windows64 build passes if a Unity PR is opened.
- Exact-head Unity Foundation CI passes before merge if implemented as a Unity branch.
- If no code changes are made, closeout documentation must still record what was inspected and why no fix was needed.

## Ambiguity Check

Status: PASS.

Human-approved answers:

- Approved 2026-06-29 via user instruction: "Approved".
- Run this QA/playtest closeout packet as the next Unity step.
- Allow only narrow readability/clickability/evidence fixes directly tied to EPIC-010 commitments.
- Record a closeout verdict; do not close EPIC-010 or start a next-epic implementation story without separate human direction.

Assumptions:

- This is a closeout/playability review, not a new terrain mechanics packet.
- Narrow fixes are allowed only for concrete EPIC-010 readability/clickability/evidence blockers found during review.

## Branch / PR requirements

- Branch name: `story/STORY-QA-013-epic-010-playtest-closeout-review`.
- PR title: `STORY-QA-013 EPIC-010 playtest and closeout review`.
- Required linked story ID: `STORY-QA-013`.
- Required evidence summary: inspected flows, tests run, evidence path, CI URL, closeout verdict.
- Required omissions section: explicitly list unresolved readability/playtest issues or state `No known omissions`.

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
- [x] Ambiguity Check status is PASS.
- [x] Human approval has been recorded.

## DONE gate

- [ ] Review/implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required evidence exists if needed.
- [ ] Required tests/CI pass, or human-approved exceptions are documented.
- [ ] Closeout verdict is recorded.
- [ ] PR/code review is complete if a Unity PR is opened.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY / approved for Unity implementation. Runnable Codex prompt prepared at `production/sprints/codex-story-qa-013.prompt.txt`.
