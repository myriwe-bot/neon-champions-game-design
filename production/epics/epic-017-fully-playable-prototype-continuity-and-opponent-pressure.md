---
title: EPIC-017 Fully Playable Prototype Continuity and Opponent Pressure
type: epic
status: active
phase: production
owner: shared
created: 2026-07-16
updated: 2026-07-17
approval: approved
related: [production/planning/full-project-review-and-completion-plan-2026-07-12, production/epics/epic-016-accelerated-playable-product-foundation, docs/architecture/data-scenario-save-format-adr, design/gdd/product-constitution]
---

# EPIC-017 Fully Playable Prototype Continuity and Opponent Pressure

## Outcome

Extend the merged presentable proof into the first durable prototype foundation: a player can leave and resume a real strategic match safely, then face an opponent that makes legible scenario-directed choices rather than relying on authored route order alone.

## Gate

A clean Windows build can save a stable strategic state, return to title, resume the same scenario state without divergence, and continue against deterministic opponent pressure. Corrupt or incompatible saves fail safely and explain the problem without damaging the last valid save.

## Why this comes next

EPIC-016 proved the connected player-facing route and is implementation-complete, while its authentic human QA closeout remains explicitly deferred. The approved eight-week prototype contract still requires save/resume and functional strategic AI. Save/resume is first because it forces an explicit, testable runtime-state boundary before AI and scenario complexity grow.

This epic may proceed as a parallel implementation train without claiming that deferred `STORY-PROOF-QA-001` has passed or that EPIC-016 is DONE.

## Capability sequence

1. `STORY-SAVE-001` — DONE / merged through Unity PR #161, with rollback continuity hotfix PR #162.
2. `STORY-AI-PLAY-001` — DONE / merged through Unity PR #166 as `a1ae8bcbf2b9705c2b20c3e4f4fce8423b3747d1`; post-merge `main` CI 29581484295 passed.
3. `STORY-PROTOTYPE-CONTINUITY-QA-001` — READY / approved on 2026-07-17; human-owned build, full-relaunch resume-continuity, opponent-pressure, and evidence closeout gate.

The third child is the sole current READY packet. Codex may run only after the Unity pointer activation and its exact-head/post-merge CI gates pass.

## Boundaries

- Preserve current deterministic behavior as the temporary implementation baseline.
- No tactical mid-battle save, multiple profiles, cloud sync, migration framework, replay system, campaign persistence, editor UI, or multiplayer.
- No sophisticated AI, hidden-information cheating, random choice, diplomacy, or broad tactical-AI rewrite in the first story.
- EPIC-016 human QA remains deferred and separately approval-gated.

## Approval

Human-approved on 2026-07-16 with `STORY-SAVE-001` and the prototype save ADR as proposed. On 2026-07-17, the human separately approved `STORY-AI-PLAY-001` and its deterministic policy exactly as written, then approved `STORY-PROTOTYPE-CONTINUITY-QA-001` with a mandatory full build close/relaunch and bounded `PASS WITH FOLLOW-UPS` verdict.
