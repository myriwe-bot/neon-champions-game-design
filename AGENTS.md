# AGENTS.md — Neon Champions Game Design Repo

This repository is the production-facing game design and agent-control source of truth for Neon Champions. It is not the Unity implementation repository.

## Repository Role

This repo defines:

- what is being built;
- what is approved;
- how agents may safely implement it later;
- what evidence is required.

Do not add Unity runtime code here unless an approved spike/story explicitly authorizes it.

## Required Reading Order

Before modifying durable docs, read in this order:

1. `README.md`
2. `SCHEMA.md`
3. `design/workflow.md`
4. relevant GDD/design docs
5. `docs/architecture/control-manifest.md`
6. relevant ADRs under `docs/architecture/`
7. relevant production epic/story/spike/checklist
8. existing target file(s)

If these sources conflict, stop and report. Do not resolve conflicts by guessing.

## Agent Authority

Agents may:

- draft design docs, ADRs, stories, epics, checklists, and spike definitions;
- review consistency and traceability;
- propose options with trade-offs;
- prepare implementation handoff prompts.

Agents may not:

- mark a doc approved unless the user explicitly approved it;
- implement from chat memory;
- implement from worldbuilding directly;
- implement from epics;
- invent mechanics, balance, UX, names, lore, assets, content, architecture, or production scope;
- treat Git/GitHub history as design authority.

Approved written docs authorize work. Git/GitHub proves what happened.

## Document Hygiene

- Use lowercase kebab-case filenames.
- Use YAML frontmatter from `SCHEMA.md`.
- Every durable artifact must be linked from `index.md`.
- Every meaningful repository change must be appended to `log.md`.
- Preserve source-of-truth separation:
  - worldbuilding belongs in the world vault;
  - production-facing design belongs here;
  - implementation evidence belongs with the future Unity repo/PR unless mirrored by an approved policy.

## Stop Conditions

Stop and report if:

- approval status is unclear;
- source docs conflict;
- a request would require inventing design/architecture/content;
- a requested implementation lacks a READY story or approved spike;
- a file appears generated or outside the requested scope;
- the change would silently weaken gates, testing, CI, or agent controls.

## Verification Before Final Response

For doc edits, run:

```bash
git diff --check
```

Then summarize:

- files changed;
- approvals recorded;
- remaining open decisions;
- verification result.
