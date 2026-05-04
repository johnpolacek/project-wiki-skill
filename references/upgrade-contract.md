# Upgrade Contract

Use this reference when auditing or upgrading a project that was previously bootstrapped by this skill.

## Principles

- Preserve user-authored project files, wiki pages, source context, and Git history.
- Add missing standard artifacts when safe.
- Replace only managed blocks that use recognized project-wiki-bootstrapper markers.
- Do not rewrite generated-looking markdown wholesale unless it is inside a managed block.
- Report artifacts as `present_but_not_upgraded` when no safe update boundary exists.

## Managed Marker Versions

Current marker:

```markdown
<!-- PROJECT-WIKI-BOOTSTRAPPER:START v1 -->
...
<!-- PROJECT-WIKI-BOOTSTRAPPER:END -->
```

Legacy marker without an explicit version is treated as `v0`:

```markdown
<!-- PROJECT-WIKI-BOOTSTRAPPER:START -->
...
<!-- PROJECT-WIKI-BOOTSTRAPPER:END -->
```

When upgrading a `v0` block to `v1`, replace only the content inside the block and update the start marker to `v1`. Preserve all content outside the markers.

## Files With Managed Blocks

Managed block replacement is allowed for:

- `AGENTS.md`
- `CLAUDE.md` when it already exists or the user explicitly requested Claude Code local guidance
- `wiki/AGENTS.md`

For files without managed blocks, preserve by default:

- `wiki/index.md`
- `wiki/log.md`
- `wiki/Sources.md`
- `wiki/plans/README.md`
- `wiki/roadmap.md`
- source briefs under `wiki/sources/`

## Additive Upgrade Behavior

When a required artifact is missing, create it from the current baseline template.

When an artifact exists:

- append to `wiki/log.md`
- preserve `wiki/Sources.md` and add only clearly missing source-index sections when doing so does not disturb user content
- preserve `wiki/index.md`; add missing links only when the existing structure makes a safe insertion obvious
- preserve `wiki/plans/README.md`; report `present_but_not_upgraded` if it lacks the current planning rule
- preserve `wiki/roadmap.md`; report `present_but_not_upgraded` if it has a different structure

## Upgrade Handoff

End an upgrade with:

- upgraded managed blocks
- created missing artifacts
- preserved existing artifacts
- `present_but_not_upgraded` artifacts
- skipped artifacts and reasons
- unresolved unknowns or contradictions
- Git result
