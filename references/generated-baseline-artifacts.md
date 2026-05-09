# Generated Baseline Artifacts

Use this reference when creating the required baseline files for a bootstrapped project. Keep generated files compact and project-specific. Replace bracketed placeholders with real project context, or name the unknown when context is missing.

## Managed Block Markers

When updating existing root or wiki agent guidance such as `AGENTS.md`, `CLAUDE.md`, or `wiki/AGENTS.md`, preserve user-authored content and add or replace only this bounded block:

```markdown
<!-- PROJECT-WIKI-BOOTSTRAPPER:START v1 -->
[managed project wiki guidance]
<!-- PROJECT-WIKI-BOOTSTRAPPER:END -->
```

Do not create multiple managed blocks in the same file. If markers already exist, replace only the content between them.

## `AGENTS.md`

```markdown
# AGENTS.md instructions for [project-root]

<!-- PROJECT-WIKI-BOOTSTRAPPER:START v1 -->
## [Project Name] Agent Guide

### Project Wiki

- Read `wiki/index.md` before answering project-specific questions or making structural changes.
- Keep durable project knowledge, plans, decisions, and project-context history under `wiki/`.
- Use `wiki/Sources.md` as the source index.
- Create or update `wiki/plans/` before meaningful code, config, schema, dependency, architecture, test, build, or app behavior changes.
- Do not create plans for small, local, reversible fixes that do not change product behavior, architecture, schema, dependencies, build configuration, public APIs, security posture, or durable project direction.
- Sync recent codebase changes back into `wiki/log.md`, relevant plans, roadmap, and source docs when work happened before planning or made the wiki stale.
- Update `wiki/index.md` when adding or materially changing durable wiki pages.
- Update `wiki/log.md` after bootstrapping, planning, validation, or material project changes that affect durable project context.

### Working Rules

- Inspect existing files and Git state before writing.
- Preserve user-authored files and existing Git history.
- Do not create root-level `docs/` or `tasks/` for durable planning.
- Name unknowns and contradictions instead of inventing certainty.

### Automation Policy

- Commit docs-only wiki changes: ask
- Commit code changes: ask
- Push changes: ask
- Install dependencies: ask
- Run long commands: ask
- Create plans before code: meaningful-only
<!-- PROJECT-WIKI-BOOTSTRAPPER:END -->
```

## `CLAUDE.md`

Create `CLAUDE.md` only when the repository already uses Claude Code guidance or the user explicitly requests Claude-specific local guidance. If both `AGENTS.md` and `CLAUDE.md` exist, keep the `CLAUDE.md` block compact and point to the shared project-wiki guidance instead of duplicating the full contract.

```markdown
# CLAUDE.md instructions for [project-root]

<!-- PROJECT-WIKI-BOOTSTRAPPER:START v1 -->
## [Project Name] Project Wiki

- Read `AGENTS.md`, `wiki/AGENTS.md`, and `wiki/index.md` before project-specific structural work.
- Keep durable project knowledge, plans, decisions, and project-context history under `wiki/`.
- Use `wiki/Sources.md` as the source index and `wiki/plans/` for maintained implementation plans.
- Sync durable project-context changes back into the wiki when implementation makes plans, source briefs, roadmap state, or the source index stale.
- Preserve user-authored instructions outside this managed block.
<!-- PROJECT-WIKI-BOOTSTRAPPER:END -->
```

## `wiki/AGENTS.md`

```markdown
# [Project Name] Wiki Agent Guide

<!-- PROJECT-WIKI-BOOTSTRAPPER:START v1 -->
This `wiki/` directory is the maintained knowledge and planning layer for `[Project Name]`.

## Source Of Truth

- `index.md` is the wiki front door.
- `log.md` is the project-context changelog. Git owns routine implementation history.
- `Sources.md` catalogs source material, repository evidence, and unknowns.
- `plans/README.md` defines the planning contract.
- `roadmap.md` tracks the next useful project direction.

## Rules

- Read `index.md` before structural wiki changes.
- Keep durable project knowledge, planning, decisions, and validation notes under `wiki/`.
- Preserve exact source material under `wiki/sources/` only when provenance matters.
- Update `index.md` when adding or materially changing durable pages.
- Update `log.md` after bootstrapping, planning, validation, or material project changes that affect durable project context.
- Use plain markdown and relative links.

## Boundaries

Do not create root-level `docs/` or `tasks/` for maintained project knowledge.

## Automation Policy

Default to asking before committing, pushing, installing dependencies, or running long commands unless the user chooses a more automated repo policy.

- Commit docs-only wiki changes: ask
- Commit code changes: ask
- Push changes: ask
- Install dependencies: ask
- Run long commands: ask
- Create plans before code: meaningful-only
<!-- PROJECT-WIKI-BOOTSTRAPPER:END -->
```

## `wiki/index.md`

```markdown
# [Project Name] Wiki

This is the maintained project knowledge layer for `[Project Name]`.

## Overview

[One short paragraph describing what the project is. If unknown, say what is known and what is missing.]

## Current Focus

[Current project focus, next decision, or bootstrap handoff state.]

## Core Pages

- `AGENTS.md` - local wiki maintenance contract
- `log.md` - project-context changelog
- `Sources.md` - source and evidence index
- `plans/README.md` - planning contract
- `roadmap.md` - staged project direction

## Source Briefs

[List generated source briefs when present. If none were generated, state that no separate source briefs were justified by current evidence.]
```

## `wiki/log.md`

```markdown
# [Project Name] Log

Append durable project-context changes here. Git owns routine implementation history. Prefer headings like `## [YYYY-MM-DD] type | title`, replacing `[YYYY-MM-DD]` with the actual date at the time of bootstrap.

Log bootstrap/import events, planning direction changes, codebase sync summaries after unplanned work, validation results that affect plans or roadmap, source-context changes, and important decisions discovered during implementation. Do not log routine commits, every code edit, every test run, formatting, minor refactors, or details already obvious from Git. If this file becomes hard to scan, summarize older entries into `wiki/log-archive.md` or a dated archive such as `wiki/log/YYYY.md`.

## [YYYY-MM-DD] bootstrap | initialize project wiki

- Created the docs-first project wiki, source index, local agent guidance, and planning contract.
- Mode: `[bootstrap_new|import_existing]`.
- Git result: [initialized new repository | preserved existing repository | skipped by request | failed: reason].
- Source briefs: [none generated | generated `wiki/sources/prd.md` | generated `wiki/sources/design-brief.md` | generated ...].
```

## `wiki/Sources.md`

```markdown
# Sources

This page catalogs source material, repository evidence, and unresolved unknowns for `[Project Name]`.

## Source Material

- [Prompt/source note/repository evidence]: [short description]

## Repository Evidence

- [Observed file, manifest, stack, or Git state]

## Generated Source Briefs

- None generated yet. Current evidence does not justify separate source briefs.

## Unknowns

- [Unknown or contradiction that matters for future planning]
```

## `wiki/sources/design-brief.md`

Create this source brief only when project evidence justifies durable UI design memory. Do not create it for CLI tools, backend services, libraries, infra projects, or thin prompts without a meaningful interface signal.

All generated source briefs should include this status pattern near the top, replacing placeholders with current evidence or `Unknown`:

```markdown
## Status

- Last reviewed: [YYYY-MM-DD]
- Evidence basis: [prompt | repo | source doc | implementation]
- Confidence: [high | medium | low]
- Known gaps: [Unknown | concise list]
```

```markdown
# Design Brief

## Status

- Last reviewed: [YYYY-MM-DD]
- Evidence basis: [prompt | repo | source doc | implementation]
- Confidence: [high | medium | low]
- Known gaps: [Unknown | concise list]

## Product Surface

[The UI, frontend, website, dashboard, visual workflow, design system, or interaction-heavy surface this brief covers.]

## Interface Principles

[Durable guidance for density, hierarchy, tone, navigation, workflow ergonomics, and what future UI work should preserve.]

## Visual System

[Colors, typography, spacing, component conventions, iconography, imagery, brand constraints, or unknowns.]

## Interaction Patterns

[Forms, tables, filters, navigation, empty states, loading states, errors, confirmations, keyboard behavior, and similar patterns.]

## Responsive And Accessibility Expectations

[Viewport priorities, contrast, focus states, reduced motion, assistive technology expectations, and known constraints.]

## Validation

[Manual design review, browser QA, screenshot checks, viewport checks, accessibility checks, or automated tests expected for UI work.]

## Unknowns

[Missing brand, target devices, design system decisions, reference screenshots, asset needs, or unresolved tradeoffs.]
```

## `wiki/plans/README.md`

```markdown
# Plans

This directory holds durable implementation plans for `[Project Name]`.

## Planning Rule

Create or update a markdown plan before meaningful code, config, schema, dependency, architecture, test, build, or app behavior changes.

Fast-path exception: for small, local, reversible fixes that do not change product behavior, architecture, schema, dependencies, build configuration, public APIs, security posture, or durable project direction, do not create a plan. Make the change, validate it, and avoid wiki/log updates unless the fix reveals durable project knowledge.

## Structure

- Use `features/` for focused feature plans that do not need a full numbered roadmap.
- Use `mvp/` only for greenfield, pre-launch, or explicitly MVP work that needs numbered roadmap implementation sessions.
- Use `zzz_completed/` for completed plans after all stages, units, completion gates, and verification records support completion.
- For imported or existing live projects, default to `roadmap.md` plus focused `features/`, `maintenance/`, or `releases/` plans only when concrete workstreams justify them.
- Keep bugfix or cleanup planning in the closest relevant existing plan.
- Record completed work, decisions discovered during implementation, and verification in `../log.md` only when they affect durable project context.

## Current Planning State

[No numbered implementation plan exists yet | Current plan: `mvp/README.md` | Next planning target: ...]

## Completed Plans

[No completed plans archived yet | Completed plans: `zzz_completed/features/example.md`]
```

## `wiki/roadmap.md`

```markdown
# Roadmap

## Current Goal

[The first durable project outcome.]

## Next Decision

[The next decision needed before implementation or deeper planning.]

## Next Steps

1. [Concrete next step]
2. [Concrete next step]
3. [Concrete next step]

## Deferred

- [Known deferred work, non-goal, or future option]
```

## `.agents/skills/project-wiki-maintainer/SKILL.md`

Use the local skill support decision tree in [`canonical-bootstrap-contract.md`](canonical-bootstrap-contract.md) before creating repo-local skills. Create `.agents/skills/project-wiki-maintainer/SKILL.md` only when repo-local skills are already in use or explicitly requested. For ordinary `bootstrap_new`, skip `.agents/skills/` creation when repo-local skills are not already in use or explicitly requested, and report the skip reason.

The `project-wiki-maintainer` skill should be short and project-local. It must instruct agents to maintain that project's `wiki/`, not this reusable skill repo.

Required traits:

- Frontmatter with `name: project-wiki-maintainer`.
- A description customized with the target project name that triggers on maintaining that project's wiki, plans, logs, source docs, local agent rules, and codebase-to-wiki sync.
- Workflow to read `wiki/AGENTS.md` and `wiki/index.md` first.
- Rules to update `wiki/index.md` and `wiki/log.md`.
- Rule to reconcile recent codebase changes into plans, roadmap, source docs, and the log when work happened before planning or made the wiki stale.
- Boundary against root-level `docs/` and `tasks/` for durable planning.

Do not generate additional repo-local skill stubs from this baseline. If the user explicitly asks for frontend, copywriting, browser, test, deployment, or other local skills, treat that as separate skill-authoring or skill-installation work and preserve any existing user-edited skill files.

```markdown
---
name: project-wiki-maintainer
description: Maintain [Project Name]'s wiki, plans, log, source index, source briefs, and local agent rules. Use when updating durable project knowledge, planning features, updating implementation plans, syncing recent codebase changes back into the wiki, recording validation or decisions, maintaining roadmap/log state, or answering from [Project Name]'s project wiki.
---

# Project Wiki Maintainer

Use this skill to maintain `[Project Name]`'s `wiki/` knowledge layer. Replace `[Project Name]` during bootstrap so the local skill is specific to the bootstrapped project.

## Workflow

1. Read `wiki/AGENTS.md` and `wiki/index.md` first.
2. Preserve source context in `wiki/Sources.md`; create `wiki/sources/` briefs only when project evidence justifies them, including `design-brief.md` for durable UI design memory.
3. Create or update durable plans under `wiki/plans/` before meaningful code, config, schema, dependency, architecture, test, build, or app behavior changes, except for small, local, reversible fixes that do not change durable project direction.
4. Move fully complete plans into `wiki/plans/zzz_completed/` after all stages, units, completion gates, and verification records support completion; remove them from active current-plan slots while preserving compact archive links.
5. Sync recent codebase changes back into `wiki/log.md`, relevant plans, roadmap, and source docs when work happened before planning or made the wiki stale.
6. Update `wiki/index.md` when adding or materially changing durable pages.
7. Append `wiki/log.md` after planning, validation, or material project changes that affect durable project context.

## Boundaries

- Do not create root-level `docs/` or `tasks/` for durable planning.
- Do not overwrite user-authored wiki or skill files.
- Name unknowns and contradictions instead of inventing certainty.
```
