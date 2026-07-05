---
title: Review Mode
type: gate
status: draft
phase: concept
owner: shared
created: 2026-05-22
updated: 2026-07-05
source_lore: []
related: [production/gates/gate-template, design/workflow]
approval: pending
---

# Review Mode

## Selected default

Lean mode.

## Meaning

Run major phase gates and key artifact reviews. Skip micro-gates unless a document is risky, foundational, or about to drive implementation.

## Escalate to Full mode for

- Game concept approval.
- Pillar stress test.
- Systems index approval.
- MVP GDD approval.
- Technical setup approval.
- Pre-production readiness.
- Production readiness.
- Release readiness.

## Story readiness

Story gates are strict. A story is not READY unless it has traceability, acceptance criteria, scope boundaries, dependency notes, and evidence requirements.

## Closeout / playtest evidence hook

Closeout, playability, readability, UX/visual/feel, and fun-verdict gates must link `production/playtests/playtest-journal.md` entries as subjective evidence, or explicitly state `Playtest evidence: N/A` with the reason. Exact human complaints must be preserved as quoted acceptance drivers instead of paraphrased into generic polish tasks.
