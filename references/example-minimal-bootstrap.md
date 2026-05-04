# Example Minimal Bootstrap

Use this example for output density and tone. It shows a thin greenfield `bootstrap_new` for a hypothetical project called `Link Minder`, a tiny CLI idea with no confirmed implementation stack yet.

## Example `wiki/index.md`

```markdown
# Link Minder Wiki

This is the maintained project knowledge layer for `Link Minder`.

## Overview

`Link Minder` is a proposed small CLI that checks a list of URLs and reports broken links. Current context is thin: no implementation language, package manager, hosting target, or release workflow has been chosen.

## Current Focus

Preserve the project idea, identify missing technical decisions, and avoid scaffold handoff recommendations until the stack is chosen.

## Core Pages

- `AGENTS.md` - local wiki maintenance contract
- `log.md` - project-context changelog
- `Sources.md` - source and evidence index
- `plans/README.md` - planning contract
- `roadmap.md` - staged project direction

## Source Briefs

No separate source briefs were generated. Current evidence does not justify a PRD, technical brief, marketing brief, or design brief.
```

## Example `wiki/Sources.md`

```markdown
# Sources

This page catalogs source material, repository evidence, and unresolved unknowns for `Link Minder`.

## Source Material

- User prompt: "Make a small tool that checks links in a text file."

## Repository Evidence

- New empty project folder.
- Git initialized during bootstrap.
- No package manifest, source files, tests, or existing documentation.

## Generated Source Briefs

- None generated yet. Current evidence does not justify separate source briefs.

## Unknowns

- Implementation language and package manager.
- Input file format.
- Expected output format and exit-code behavior.
- Whether this should be a CLI only or also expose a library API.
```

## Example `wiki/roadmap.md`

```markdown
# Roadmap

## Current Goal

Turn the link-checker idea into a decision-complete implementation plan.

## Next Decision

Choose the implementation language, CLI behavior, and validation approach.

## Next Steps

1. Decide the runtime and package manager.
2. Define accepted input and output formats.
3. Create an implementation plan before adding code.

## Deferred

- Package publishing.
- Parallel link checking.
- HTML crawling beyond explicit URLs in an input file.
```

## Example Handoff Summary

```markdown
Created a `bootstrap_new` project wiki for `Link Minder`.

Created: `AGENTS.md`, `wiki/AGENTS.md`, `wiki/index.md`, `wiki/log.md`, `wiki/Sources.md`, `wiki/plans/README.md`, `wiki/roadmap.md`.
Skipped: `.agents/skills/project-wiki-maintainer/SKILL.md` because repo-local skills were not already in use or explicitly requested.
Source briefs: none generated; source context is thin.
Git: initialized new repository.
Unknowns: runtime, input format, output format, test approach.
Next action: choose the runtime and CLI behavior, then create a plan before adding code.
```
