# Contributing to SuperBenefit

Thank you for your interest in contributing! This guide covers workflows for both human and AI contributors.

## Quick Start

1. Check existing issues or create one describing your proposed change
2. Fork the repo and create a branch from `main`
3. Make your changes following our conventions
4. Submit a PR linking the relevant issue

## Spec-Driven Development

We use spec-driven development for complex changes. The workflow has 6 phases:

1. **Start**: Initialize project directory and plan.md from the issue
2. **Specify**: Define requirements in spec.md (what & why)
3. **Plan**: Create implementation steps in plan.md (how)
4. **Implement**: Execute steps, track in progress.md
5. **PR**: Create pull request with spec compliance
6. **Sync**: Update GitHub issue with progress

### When to use spec-driven development

- Changes touching multiple files
- New features or significant refactors
- Research or exploration tasks
- Work that takes more than ~30 minutes

### Project files

When using our project-mgmt tooling, you'll work with these files in `.project/{issue#}/`:

| File | Purpose | Created in Phase |
|------|---------|------------------|
| `plan.md` | Implementation steps + current phase | Start |
| `spec.md` | Requirements (what & why, no tech stack) | Specify |
| `findings.md` | Research discoveries and decisions | Any |
| `progress.md` | Session log of actions taken | Any |

### Plan.md phase tracking

The `plan.md` file tracks which phase you're in:

```
**Phase**: specify | plan | implement | pr | review
```

### Spec.md status tracking

The `spec.md` file tracks approval status:

```
**Status**: draft | review | approved
```

## For Human Contributors

### Commit messages

Use imperative mood: "Add feature" not "Added feature"

```
type(scope): subject

body (optional)

Closes #123
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

### Code style

- Follow existing patterns in the codebase
- Run linters before committing
- Add tests for new functionality

### Pull requests

- Create PR when implementation is complete (or ready for review)
- Link the related issue with `Closes #123`
- Fill out the PR template completely
- Keep PRs focused on a single concern
- Respond to review feedback promptly

## For AI Contributors

AI agents (Claude Code, GitHub Copilot, etc.) are welcome contributors! Follow these guidelines:

### Before starting work

1. Read the issue description and any linked specs
2. Check `.project/` for existing context on the issue
3. Review `CLAUDE.md` or equivalent project-specific guidance
4. If `.project/{issue#}/` exists, read plan.md to understand current phase

### During implementation

1. Follow the 6-phase workflow: start → specify → plan → implement → pr → sync
2. Create plan.md first (start phase), then spec.md (specify phase)
3. Update plan.md phase field as you progress
4. Log discoveries to findings.md after research
5. Log actions and errors to progress.md
6. Check off completed steps in plan.md

### Creating PRs

1. When implementation steps are complete, move to PR phase
2. Create branch if not already on one
3. Commit changes with descriptive messages
4. Create PR using the template
5. Link the issue and confirm spec compliance

### Submitting changes

1. Ensure all tests pass
2. Fill out the PR template (AI-generated summaries are fine)
3. Reference the spec if one exists
4. Flag any deviations from the original spec
5. Run sync phase to update GitHub issue

### AI-specific conventions

- Prefix AI-generated commits with `[ai]` if helpful for tracking
- Include tool/model info in PR description (optional but appreciated)
- Don't modify files outside the issue scope without discussion

## Issue Guidelines

### Bug reports

Include:
- Steps to reproduce
- Expected vs actual behavior
- Environment details
- Error messages/logs

### Feature requests

Include:
- Problem statement (what's the pain point?)
- Proposed solution
- Alternatives considered
- Who benefits

### Tasks

Include:
- Clear acceptance criteria
- Links to related specs/issues
- Estimated complexity (S/M/L)

## Getting Help

- Open a [Discussion](../../discussions) for questions
- Tag `@maintainers` for urgent issues
- Check existing issues before creating new ones

## Recognition

All contributors (human and AI) are recognized in release notes. AI contributions are attributed to the human who initiated the work.
