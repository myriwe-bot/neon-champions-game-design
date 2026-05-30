---
title: GDD Reading Guide
type: agent-instructions
status: draft
phase: systems-design
owner: shared
created: 2026-05-30
updated: 2026-05-30
related: [design/gdd/game-concept, design/gdd/game-pillars, design/gdd/systems-index, design/gdd/tactical-combat]
approval: pending
---

# GDD Reading Guide

> Use this page as the first stop for humans and LLM agents working inside `design/gdd/`.

## Purpose

The GDD folder should help design and implementation, not bury decisions in long transcripts. Each active GDD should be readable in one pass, cite dependencies, and separate approved direction from reference notes.

## Reading Order

1. [[design/gdd/game-concept]] — what game this is.
2. [[design/gdd/game-pillars]] — decision filters and anti-pillars.
3. [[design/gdd/systems-index]] — system map and dependency order.
4. System GDDs needed for the current task.
5. Research notes only when the active GDD links to them.

## Rules for LLM Agents

- Do not implement from chat memory.
- Do not treat old long-form reference notes as stronger than active GDDs.
- Cite exact GDD sections in stories and implementation prompts.
- If a section is unclear, propose a small design packet instead of inventing a rule.
- Prefer small, testable MVP contracts over Full Vision mechanics.
- Keep taxonomy shallow unless it clearly improves player-facing clarity.

## Active GDD Expectations

Each active system GDD should include:

- summary and player fantasy;
- MVP in/out scope;
- core loop or user flow;
- numbered rules or concise tables;
- dependencies and data ownership;
- tuning knobs;
- UI/readability requirements;
- acceptance criteria;
- open questions;
- links to deeper reference material.

## Current GDD Map

| GDD | Use For | Notes |
|---|---|---|
| [[design/gdd/game-concept]] | North-star concept. | Draft. |
| [[design/gdd/game-pillars]] | Design filters. | Draft. |
| [[design/gdd/systems-index]] | Dependency and priority map. | Draft. |
| [[design/gdd/intel-resource]] | Intel as resource/upgrade material. | Draft. |
| [[design/gdd/faction-unit-rosters]] | Faction tactical identities and roster concepts. | Draft. |
| [[design/gdd/tactical-combat]] | Active tactical combat overview and implementation-facing first-read contract. | Concise source-of-truth entry point; detailed preserved design-session material is split under `design/gdd/tactical-combat/`. |
| [[design/gdd/tactical-combat/section-map]] | Preservation map for tactical-combat split articles. | Confirms every original top-level section is still present and mapped. |
