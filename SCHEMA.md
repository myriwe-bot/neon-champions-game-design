# Neon Champions Game Design Schema

## Domain

Production-facing game design and AI-assisted development control for Neon Champions.

## Repository role

This repo answers: what are we building, why, what is approved, how do agents safely implement it, and what evidence proves it works?

It does not replace the lore/worldbuilding wiki.

## File naming

- Use lowercase kebab-case filenames.
- Markdown for docs.
- YAML for registries and structured data.
- One major system per GDD.

## Document statuses

Use these production statuses:

- `draft`: written but not reviewed.
- `in-review`: under gate/review.
- `approved`: accepted as current source of truth.
- `accepted-with-risk`: usable, but risks are explicitly recorded.
- `implemented`: implemented and verified against evidence.
- `deprecated`: superseded; do not use for new work.

Do not use worldbuilding canon levels for GDDs. Canon belongs in the world wiki; approval belongs here.

## Frontmatter template

```yaml
---
title: Document Title
type: concept | pillars | system-gdd | ux-spec | art-spec | lore-import | design-bridge-import | adr | gate | epic | story | playtest | qa | milestone | registry
status: draft | in-review | approved | accepted-with-risk | implemented | deprecated
phase: concept | systems-design | technical-setup | pre-production | production | polish | release
owner: human | agent | shared
created: YYYY-MM-DD
updated: YYYY-MM-DD
source_lore: []
related: []
approval: pending | approved | accepted-with-risk | rejected
---
```

## Traceability chain

Production work should trace like this:

Worldbuilding source -> design bridge / lore import -> GDD -> ADR/control rule -> epic -> story -> implementation -> test/playtest evidence.

## Index/log requirements

- Every durable design artifact must be listed in `index.md`.
- Every meaningful repository change must be logged in `log.md`.
- Every phase advancement needs a gate file under `production/gates/`.
