# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is the `superbenefit/.github` repository — the organization-wide default community health files for all SuperBenefit DAO repositories. It must remain **public** for GitHub to serve these as org-wide defaults.

The single source of truth is `spec.md` (v1.3.0), which defines all community health file templates and their integration with the project-mgmt Claude Code plugin.

## What This Repo Contains

All content is specified in `spec.md` and extracted into the following file structure:

```
superbenefit/.github/
├── CONTRIBUTING.md
├── pull_request_template.md
└── ISSUE_TEMPLATE/
    ├── config.yml
    ├── 01-bug.yml
    ├── 02-feature.yml
    └── 03-task.yml
```

## Key Concepts

### GitHub Default Fallback Chain
GitHub resolves community health files in order: repo `.github/` → repo root → repo `docs/` → org `.github/` (this repo). If a repo has ANY files in its `.github/ISSUE_TEMPLATE/` folder, the entire default ISSUE_TEMPLATE folder is ignored.

### Labels Must Be Pre-Created
Labels referenced in issue templates (`bug`, `triage`, `enhancement`, `task`) are NOT auto-created. They must exist in both this repo and every target repo.

### Template Filename Ordering
Use `01-`, `02-` prefixes (not `1-`, `2-`) to ensure correct alphanumeric sort order with 10+ templates.

### Spec-Driven Development Workflow
All templates align with the project-mgmt plugin's 6-phase workflow: **start → specify → plan → implement → pr → sync**. Project files live in `.project/{issue#}/` with four tracking files: `plan.md`, `spec.md`, `findings.md`, `progress.md`.

## Commit Convention

```
type(scope): subject
```
Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`. Use imperative mood.

## AI Contributor Guidelines

- Prefix AI-generated commits with `[ai]` if helpful for tracking
- Follow the 6-phase workflow when using project-mgmt tooling
- Check `.project/` for existing context before starting work
- Don't modify files outside issue scope without discussion
