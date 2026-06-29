---
title: STORY-UX-002 Tactical Playability Scale, Resource HUD, and Stack Clarity
type: story
status: done
phase: production
owner: shared
created: 2026-06-29
updated: 2026-06-29
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/stories/story-qa-013-epic-010-playtest-and-closeout-review,
    production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-UX-002 Tactical Playability Scale, Resource HUD, and Stack Clarity

## Status

DONE / merged. Unity PR #105 merged on 2026-06-29 as `6e22e844fba6c8744424d1963f3a6a35ccfb9b2f`. Exact-head PR CI passed on `72aa0bba0f2e994517b968ff691a301920c8d498`: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28370117987. Post-merge `main` CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28372400692. Human approval recorded 2026-06-29: "<Approved".

## Story type

Unity UX / playability readability repair.

## Parent / context

This is a cross-epic tactical/strategic readability repair packet, not a terrain mechanics story. EPIC-010 is closed; this story preserves remaining human playtest pain that is broader than terrain/context closeout.

## Human playtest source authority

Preserve these complaints exactly as acceptance drivers:

- "Resource use is unclear, resources are not displayed anywhere."
- "Unit stacks also unclear."
- "Tactical area still small."

Context from the same playtest, already partially addressed by `STORY-QA-013`, must not regress:

- "central objective situation seems broken - champion is directed away from the point. Holding is not possible."
- "\"Engage CHampion\" option is incorrectly displayed there. Cannot attack guard or take control over objective."
- "Also, champion-on-champion combat is not working."

## Player/design value

As a player, I need the tactical battle surface and resource/stack information to be large, persistent, and readable enough that I understand what I own, what resources/actions I have, what unit stacks mean, and what I can do next without interpreting debug IDs.

## In scope

- Increase the usable tactical battle area at 1280x720 by reducing avoidable panel waste, dead space, or over-small board scaling in the current prototype UI.
- Keep the strategic/tactical HUD resource state visible and legible wherever resource-consuming or resource-relevant actions are presented.
- Display current resource names/amounts in player-facing language; if a resource is prototype-only, label it as prototype but do not hide it.
- Improve unit-stack labels and selected-stack details so the player can see at least:
  - side/owner: friendly, enemy, neutral/guard;
  - unit role/type/name;
  - current count / starting or max count where available;
  - current actionable state: active, waiting/acted, defeated, legal target, non-target;
  - relevant command/AP/resource state where currently implemented.
- Preserve or improve `STORY-QA-013` fixes for objective/site affordance and Champion encounter affordance; no misleading `Engage Champion` action may appear for an objective/guard site.
- Add/repair tests or presentation snapshot coverage for resource HUD visibility, stack label/detail clarity, tactical area scale/readability, and non-regression of objective/Champion affordances where feasible.
- Capture evidence under Unity `production/evidence/STORY-UX-002/`.

## Out of scope

- No new resources, income rules, costs, economy, recruitment model, facilities, or balance changes.
- No new combat mechanics, damage rules, AI, objective capture rules, stack stats, roster content, or Champion powers.
- No final UI art system, icons, animation, VFX, audio, localization, accessibility framework, or full responsive UI rewrite.
- No strategic map topology changes, new sites/routes, or new scenario win/loss rules.
- No expansion of `STORY-QA-013` beyond preserving its already-merged behavior.

## Acceptance criteria

- [ ] At 1280x720, the tactical board/area is visibly larger or materially less cramped than the current post-`STORY-QA-013` main branch while preserving required HUD/action text.
- [ ] Resource state is visible in the strategic HUD and tactical/interaction context where actions can consume, award, or depend on resources.
- [ ] Resource labels include current amounts and player-facing resource names; no resource-relevant action is presented without visible resource context.
- [ ] Tactical stack labels distinguish friendly/enemy/guard identity and show role/name plus current count clearly enough to compare stacks without selecting each one.
- [ ] Selecting or inspecting a stack shows readable stack details, including count/status/actionability and any currently implemented command/AP/resource context.
- [ ] Legal move and legal attack/target state remains clear after layout/scale changes.
- [ ] Objective/guard site interaction does not display `Engage Champion`; Champion-vs-Champion engage affordance remains limited to actual same-node enemy Champions.
- [ ] Existing objective capture and Champion battle regression coverage from `STORY-QA-013` continues to pass.
- [ ] Evidence under Unity `production/evidence/STORY-UX-002/` includes before/after or final-state screenshots/text notes for tactical area scale, resource HUD, stack labels/details, and objective/Champion affordance non-regression.
- [ ] Exact-head Unity Foundation CI passes before merge if implemented.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- EditMode tests for any application/domain/presentation snapshot logic changes.
- PlayMode smoke tests or generated screenshot evidence for the 1280x720 tactical surface.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge, and post-merge main CI after merge.

## Ambiguity Check

Status: PASS.

Human-approved assumptions:

- This story is the next implementation packet after `STORY-QA-013`.
- It should repair readability/scale/HUD/stack clarity only, not add new mechanics.
- Resource display means showing existing current prototype resource state, not inventing an economy.

## Branch / PR requirements

- Branch name: `story/STORY-UX-002-tactical-scale-resource-stack-clarity`.
- PR title: `STORY-UX-002 tactical scale resource HUD and stack clarity`.
- Required linked story ID: `STORY-UX-002`.
- Required evidence path: `production/evidence/STORY-UX-002/` in Unity.
- Required omissions section: explicitly list unresolved readability/playtest issues or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent/context.
- [x] User/player/system value is clear.
- [x] Exact human playtest complaints are preserved.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Ambiguity Check status is PASS for READY-candidate.
- [x] Human approval has been recorded.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required evidence exists.
- [x] Required tests/CI pass, or human-approved exceptions are documented.
- [x] PR/code review is complete if a Unity PR is opened.
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged in Unity PR #105: https://github.com/myriwe-bot/neon-champions-unity/pull/105. Merge commit: `6e22e844fba6c8744424d1963f3a6a35ccfb9b2f`. Exact-head PR CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28370117987. Post-merge main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28372400692. The immediate approved UX/readability repair packet is complete; no next Unity implementation story is approved yet. Next step is a human decision on the next implementation direction, prepared in `production/planning/next-implementation-direction-brief-2026-06-29.md` with a guarded, non-runnable prompt at `production/sprints/codex-next-implementation-direction-brief-2026-06-29.prompt.txt`.
