---
title: Control Manifest
type: adr
status: draft
phase: technical-setup
owner: shared
created: 2026-05-22
updated: 2026-05-22
source_lore: []
related: [docs/architecture/architecture]
approval: pending
---

# Control Manifest

Rules agents must obey once implementation begins.

## Implementation authority

- Do not implement from chat memory.
- Implement only READY stories.
- If a story conflicts with an approved GDD or ADR, stop and report the conflict.
- If design ambiguity changes gameplay, stop and ask for a design decision.

## Data and tuning

- No hardcoded tunable gameplay values unless explicitly approved for prototype code.
- Use registries/config for entities, formulas, and tuning knobs once architecture defines them.

## Verification

- Every implementation story needs evidence.
- Logic stories require automated tests unless explicitly N/A.
- Visual/feel stories require screenshot/video/playtest evidence or defined review protocol.

## Scope

- Do not add extra mechanics because they seem useful.
- Do not promote full-vision features into MVP without a gate decision.
