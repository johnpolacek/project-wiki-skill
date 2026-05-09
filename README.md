# Project Wiki

A skill for AI coding agents creating and maintaining a docs-first project memory layer for agentic development.

Bootstrapping is one mode. The skill also supports feature planning, plan updates, codebase-to-wiki sync, decision capture, project-context logging, roadmap maintenance, and additive wiki audits/upgrades.

Inspired by [Karpathy's LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). This skill adapts the persistent, LLM-maintained markdown wiki pattern for software projects: source context, project plans, roadmap state, agent guidance, and codebase-to-wiki sync.

## Install

Install in your project:

```bash
npx skills add johnpolacek/project-wiki-skill
```

## Requirements

- A software project with either an existing repository or enough source context to create project wiki files.
- Git is recommended. For brand-new projects, the skill initializes Git unless the user opts out.
- No generator or CLI runtime is required; this is a markdown contract and template set for AI coding agents.
- The skill is agent-agnostic. It is intended to work in Codex, Claude Code, and other agents that support markdown skills.

## Workflow

```text
User Prompt / Repo Evidence
        |
        v
wiki/Sources.md
        |
        v
Source Briefs + Roadmap
        |
        v
wiki/plans/
        |
        v
Implementation
        |
        v
sync_changes -> wiki/log.md + updated plans/source docs
```

## What It Helps With

- Bootstraps a new project into a maintained `wiki/` structure.
- Imports an existing repository without overwriting user-authored files.
- Creates a required source index at `wiki/Sources.md`.
- Generates PRD, technical, marketing, or design briefs only when project evidence justifies them.
- Creates or updates feature and implementation plans under `wiki/plans/`.
- Syncs recent codebase changes back into the wiki when work happened before planning or made project knowledge stale.
- Records durable planning, validation, decision, and project-context history in `wiki/log.md` without duplicating Git history.
- Adds managed agent guidance with bounded update markers, following the repository's existing agent-file convention when present.
- Initializes Git for new projects unless the user opts out.
- Leaves starter app scaffolding outside the core skill; explicit scaffold requests should be handled as separate implementation work.

## When To Use

Use this skill when the user explicitly wants to create, import, maintain, audit, or sync a docs-first project wiki for a software project. Also use it when the project already has this wiki structure and the user asks to update project memory, plans, source briefs, or durable agent context.

Do not use it for ordinary coding tasks unless the project already uses this wiki structure or the user asks to update project wiki context.

Example prompts:

```text
Use $project-wiki to bootstrap a wiki for this existing app.
Use $project-wiki to plan this feature before implementation.
Use $project-wiki to sync recent code changes back into the wiki.
Use $project-wiki to audit this project's wiki and agent guidance files.
```

## What The Agent Does

The agent inspects the repo and source material first, identifies whether the target is the repo root or a specific package/app root, preserves user-authored docs, writes bounded managed sections where appropriate, and creates or updates the minimal wiki artifacts needed for the requested mode. It avoids placeholder leakage, skips unsupported source briefs, records only durable project context in `wiki/log.md`, and reports skipped or blocked work explicitly.

## Core Outputs

A completed docs-first bootstrap creates or preserves:

- `AGENTS.md`
- `CLAUDE.md` when the repository already uses Claude Code guidance or the user explicitly requests it
- `wiki/AGENTS.md`
- `wiki/index.md`
- `wiki/log.md`
- `wiki/Sources.md`
- `wiki/plans/README.md`
- `wiki/roadmap.md`
- `.agents/skills/project-wiki-maintainer/SKILL.md` when repo-local skills are already in use or explicitly requested

Source briefs under `wiki/sources/` are conditional. The skill creates them only when the available source material supports a separate durable artifact.

## Use In A Project

Skill installation and project wiki initialization are separate steps. Installing this skill makes the workflow available to the agent; it does not automatically modify every repository.

### Initialize A Project

From a new or existing project, run:

```text
Use $project-wiki to initialize this project.
```

For an existing repo, you can be more explicit:

```text
Use $project-wiki to bootstrap this existing app into a docs-first project wiki.
```

The agent should inspect the project first, identify the target root, preserve existing files and Git history, then create or update the wiki baseline, source index, roadmap, planning area, and bounded agent guidance. It should create source briefs only when project evidence justifies them, skip repo-local skill creation unless `.agents/skills/` is already in use or explicitly requested, and report created, preserved, skipped, blocked, and `present_but_not_upgraded` artifacts.

During initialization, the agent should record a repo automation policy in `wiki/AGENTS.md`. The default is conservative: ask before commits, pushes, dependency installs, or long commands. A common low-friction setting is to auto-commit docs-only wiki changes while continuing to ask before code commits and pushes.

For an existing live project, the agent should treat the project as post-MVP unless source evidence says otherwise. It should create `wiki/plans/README.md` and `wiki/roadmap.md`, but skip `wiki/plans/mvp/` by default. Focused `features/`, `maintenance/`, or `releases/` plans should be created only when a concrete workstream exists.

For a brand-new project, invoke the skill with source context such as a prompt, PRD, notes, or initial repo files. The agent creates the wiki baseline, source index, roadmap, planning area, bounded agent guidance, and Git initialization unless opted out.

### Enable Auto-Commits

By default, the skill asks before committing. To make project-wiki documentation changes commit automatically in one repo, ask during initialization or audit:

```text
Use $project-wiki to set this repo's automation policy to auto-commit docs-only wiki changes.
```

The agent should record this in `wiki/AGENTS.md`:

```markdown
## Automation Policy

- Commit docs-only wiki changes: auto
- Commit code changes: ask
- Push changes: ask
- Install dependencies: ask
- Run long commands: ask
- Create plans before code: meaningful-only
```

With that policy, the agent may commit completed docs-only project-wiki changes automatically. It should stage only intended wiki/docs/agent-guidance files, leave unrelated dirty files untouched, and avoid pushing unless explicitly requested or the repo policy allows auto-push.

### Start A Plan

Before meaningful product, architecture, schema, API, dependency, build, auth, integration, deployment, or durable UI direction changes in a project that uses this wiki structure, ask:

```text
Use $project-wiki to plan this feature before implementation.
```

You can name the feature directly:

```text
Use $project-wiki to create a plan for billing export.
```

The agent should inspect the repo, wiki, source briefs, roadmap, and existing plans before writing. It should aim for maximum useful clarification and usually ask a focused batch of 3-7 high-leverage questions about scope, non-goals, architecture, schema, UX, dependencies, validation, rollout, risks, sequencing, or the next execution unit. It should proceed directly to a plan only when the user asks to skip questions, the change is a small fast-path fix, or repo/wiki/source evidence already answers the important planning questions.

Small local reversible fixes do not need plans. Typo fixes, narrow tests for existing behavior, private helper refactors, and local TypeScript fixes should use the fast path unless they reveal durable project knowledge.

### Work With Plans In The CLI

To inspect the current plan state without opening every file, ask:

```text
Use $project-wiki to show me the current plan state for this project.
```

To continue the next unit:

```text
Use $project-wiki to continue the current plan.
```

Continue/resume prompts are orientation prompts by default. The agent should inspect the current branch or worktree, Git state, `wiki/plans/README.md`, and relevant plan files, then summarize the current plan, current unit, blockers, and next choices. It should not create a plan or edit code unless you explicitly ask it to plan or implement after orientation.

If no active plan exists, the agent should say so, ask clarification questions, and wait for your direction before creating a plan or changing code.

For CLI-friendly planning:

```text
Use $project-wiki to plan this feature for CLI-friendly execution.
```

The agent should treat `wiki/plans/README.md` as the plan dashboard. It should keep the first screen of the dashboard and every active plan useful in a terminal: status, planning shape, current unit, blockers, next action, validation, and exact files to read next. Completed plans should move under `wiki/plans/zzz_completed/` and be removed from active current-plan slots while leaving compact archive links in the dashboard. For handoffs, the agent should summarize the current plan state and provide paths or commands such as:

```bash
sed -n '1,80p' wiki/plans/README.md
sed -n '1,120p' wiki/plans/features/blog-authoring.md
```

It should avoid dumping long markdown into the chat unless you ask for the full file.

### Complete Or Update A Plan

After implementing planned work, ask:

```text
Use $project-wiki to update the plan for the work we just completed.
```

The agent should inspect current changes, validation results, and the relevant plan. It should update the plan only when the implementation completed, invalidated, narrowed, expanded, or redirected planned work. It should update `wiki/log.md` only for durable project-context changes, not routine commits, lint fixes, test runs, or obvious Git history.

Every execution unit should include a `Verification` section with automated, manual, or explicitly deferred checks. A unit should not be marked complete unless verification is recorded or deferred with a reason.

When the top-level plan, all stages, all units, completion gates, and required verification records support completion, the agent should move the whole completed plan tree into `wiki/plans/zzz_completed/`. For example, a finished feature plan moves from `wiki/plans/features/billing-export.md` to `wiki/plans/zzz_completed/features/billing-export.md`, while a finished MVP moves as the whole `wiki/plans/mvp/` tree to `wiki/plans/zzz_completed/mvp/`.

If implementation changed source truth, roadmap direction, architecture, UI direction, or known constraints, the agent should also update `wiki/Sources.md`, source briefs, `wiki/roadmap.md`, or `wiki/index.md` as needed.

### Sync Unplanned Changes

If code changed before a plan existed, ask:

```text
Use $project-wiki to sync recent code changes back into the wiki.
```

The agent should inspect Git status, diffs, recent commits when relevant, current plans, roadmap, source briefs, and `wiki/log.md`. It should avoid inventing retrospective intent. If the repo shows what changed but not why, it should record the observed change and the unknown decision rather than turning it into a confident plan narrative.

### Audit Or Upgrade

To check an existing project wiki, ask:

```text
Use $project-wiki to audit this project's wiki and agent guidance files.
```

The agent should validate required wiki files, managed blocks, source indexes, planning structure, source brief status metadata, log policy, monorepo target-root safety, and repo-local skill behavior. It should add missing artifacts only when safe, preserve user-authored docs, and report warnings or blockers with next actions.

## Sample Workflows

Bootstrap a new project from a rough idea:

```text
Use $project-wiki to initialize this project from this idea: a small internal dashboard for reviewing invoice exceptions.
Use $project-wiki to create a plan for the first review queue workflow.
Use $project-wiki to update the plan after implementation.
```

Import an existing app, then plan a feature:

```text
Use $project-wiki to import this existing Next.js app into a docs-first project wiki.
Use $project-wiki to create a plan for billing export.
Use $project-wiki to sync recent code changes back into the wiki.
```

Recover after unplanned work:

```text
Use $project-wiki to sync recent code changes back into the wiki.
Use $project-wiki to update the roadmap and closest feature plan based on what changed.
```

In all workflows, the agent should keep routine implementation history in Git and reserve `wiki/log.md` for durable project context that would help a future agent make better decisions.

## Works Best With

- Clear source material such as a PRD, README, technical notes, existing code, or user-provided product direction.
- Projects where agents will return across multiple sessions and need durable memory beyond Git history.
- Teams that want planning docs and codebase knowledge to stay synchronized during agentic development.

## Repository Layout

- `LICENSE` - MIT license
- `SKILL.md` - installable skill entrypoint
- `references/canonical-bootstrap-contract.md` - full bootstrap contract
- `references/generated-baseline-artifacts.md` - required artifact templates and managed-block markers
- `references/example-minimal-bootstrap.md` - filled minimal bootstrap example
- `references/example-moderate-import.md` - moderate existing-repo import example
- `references/planning-contract.md` - feature planning, plan updates, codebase sync, and project-context log guidance
- `references/upgrade-contract.md` - additive upgrade behavior
- `references/validation-checklist.md` - validation scenarios

## License

MIT
