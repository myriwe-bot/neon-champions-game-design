---
title: Game Design Workflow
type: concept
status: draft
phase: concept
owner: shared
created: 2026-05-22
updated: 2026-05-22
source_lore: []
related: [design/game-design-principles, production/gates/review-mode]
approval: pending
---

# Game Design Workflow

This project follows a Claude Code Game Studios-style flow adapted for strict human-led design and agent-safe implementation.

## Core rule

Humans own creative direction. Agents facilitate, draft, review, decompose, implement from approved specs, and verify with evidence.

## Phases

1. Concept
   - Define fantasy, audience, pillars, loops, MVP, vertical slice, risks.
   - Output: `design/gdd/game-concept.md`, `design/gdd/game-pillars.md`.
   - Gate: Concept -> Systems Design.

2. Systems Design
   - Map explicit and implicit systems.
   - Sort by dependency layer and priority tier.
   - Write implementation-grade system GDDs.
   - Gate: Systems Design -> Technical Setup.

3. Technical Setup
   - Pin Unity version and architecture rules.
   - Write ADRs, control manifest, test strategy.
   - Gate: Technical Setup -> Pre-Production.

4. Pre-Production
   - Build throwaway prototypes and vertical-slice candidates.
   - Create epics/stories only after GDDs and architecture are usable.
   - Run playtests.
   - Gate: Pre-Production -> Production.

5. Production
   - Implement READY stories in sprints.
   - Require traceability and verification evidence.
   - Gate: Production -> Polish.

6. Polish
   - Balance, UX, accessibility, performance, onboarding, content audit.
   - Gate: Polish -> Release.

7. Release
   - Release checklist, patch/rollback plan, known issues, launch material.

## Review intensity

Default: Lean.
Use Full for:
- game concept approval;
- systems index approval;
- MVP GDD approval;
- pre-production readiness;
- production readiness;
- release readiness.

## Handoff rule

No implementation work unless the relevant story is READY and references approved GDDs/ADRs/control rules.
