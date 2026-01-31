# GitHub Community Health Files Specification

**Version**: 1.3.0
**Purpose**: Default templates for SuperBenefit DAO repositories that integrate with the project-mgmt plugin
**Location**: `superbenefit/.github` repository (must be public)
**Last verified**: January 2026 against official GitHub Docs
**Aligned with**: project-mgmt plugin v0.1.0

---

## Overview

These files provide org-wide defaults for all SuperBenefit repositories. Individual repos can override by adding their own files.

### How Defaults Work

GitHub looks for community health files in this order:
1. Repository's `.github` folder
2. Repository's root directory
3. Repository's `docs` folder
4. Organization's `.github` repository (this spec)

**Important**: If a repository has ANY files in its `.github/ISSUE_TEMPLATE` folder, the entire default `ISSUE_TEMPLATE` folder is ignored.

### Files in This Spec

| File | Location | Purpose |
|------|----------|---------|
| `CONTRIBUTING.md` | Root | Contribution guidelines for humans and AI |
| Issue templates | `.github/ISSUE_TEMPLATE/` | Issue forms (.yml) |
| `config.yml` | `.github/ISSUE_TEMPLATE/` | Template chooser configuration |
| `pull_request_template.md` | Root or `.github/` | PR template |

### Label Requirements

⚠️ **Critical**: Labels specified in issue templates must be created in:
1. The `.github` repository itself
2. Every repository where the template will be used

Labels are NOT automatically created.

---

## Directory Structure

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

**Note on ordering**: Template filenames are sorted alphanumerically. Use `01-`, `02-` prefixes (not `1-`, `2-`) to ensure correct ordering when you have 10+ templates.

---

## CONTRIBUTING.md

```markdown
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
```

---

## ISSUE_TEMPLATE/config.yml

```yaml
blank_issues_enabled: false
contact_links:
  - name: 💬 Community Discussion
    url: https://github.com/orgs/superbenefit/discussions
    about: Ask questions and discuss ideas with the community
  - name: 📚 Documentation
    url: https://docs.superbenefit.org
    about: Check our docs for guides and reference
```

---

## ISSUE_TEMPLATE/01-bug.yml

```yaml
name: 🐛 Bug Report
description: Report a bug or unexpected behavior
title: "[Bug]: "
labels: ["bug", "triage"]
body:
  - type: markdown
    attributes:
      value: |
        Thanks for reporting! Please fill out the sections below.

  - type: checkboxes
    id: existing-check
    attributes:
      label: Existing Issue Check
      options:
        - label: I searched existing issues and this is not a duplicate
          required: true

  - type: textarea
    id: description
    attributes:
      label: Bug Description
      description: What happened? What did you expect to happen?
      placeholder: |
        When I did X, Y happened.
        I expected Z to happen instead.
    validations:
      required: true

  - type: textarea
    id: reproduction
    attributes:
      label: Steps to Reproduce
      description: How can we reproduce this bug?
      placeholder: |
        1. Go to '...'
        2. Click on '...'
        3. See error
    validations:
      required: true

  - type: textarea
    id: environment
    attributes:
      label: Environment
      description: Relevant version info, OS, browser, etc.
      placeholder: |
        - OS: macOS 14.0
        - Node: 20.10.0
        - Browser: Chrome 120
      render: markdown
    validations:
      required: false

  - type: textarea
    id: logs
    attributes:
      label: Error Logs
      description: Paste any relevant error messages or logs
      render: shell
    validations:
      required: false

  - type: dropdown
    id: severity
    attributes:
      label: Severity
      description: How severe is this bug?
      options:
        - Low - Minor inconvenience
        - Medium - Affects workflow but has workaround
        - High - Blocks important functionality
        - Critical - System unusable / data loss
    validations:
      required: true

  - type: checkboxes
    id: reproduce-check
    attributes:
      label: Reproducibility
      options:
        - label: I can reproduce this bug consistently
          required: false
```

---

## ISSUE_TEMPLATE/02-feature.yml

```yaml
name: ✨ Feature Request
description: Propose a new feature or enhancement
title: "[Feature]: "
labels: ["enhancement", "triage"]
body:
  - type: markdown
    attributes:
      value: |
        Thanks for your feature idea! Help us understand the problem and your proposed solution.

  - type: checkboxes
    id: existing-check
    attributes:
      label: Existing Issue Check
      options:
        - label: I searched existing issues and this is not a duplicate
          required: true

  - type: textarea
    id: problem
    attributes:
      label: Problem Statement
      description: What problem does this solve? Who experiences this pain point?
      placeholder: |
        As a [type of user], I want [goal] so that [benefit].
        
        Currently, I have to [workaround], which is [why it's painful].
    validations:
      required: true

  - type: textarea
    id: solution
    attributes:
      label: Proposed Solution
      description: How do you envision this working?
      placeholder: |
        Describe the feature and how it would work from a user's perspective.
    validations:
      required: true

  - type: textarea
    id: alternatives
    attributes:
      label: Alternatives Considered
      description: What other approaches did you consider?
      placeholder: |
        - Alternative A: [description] - rejected because [reason]
        - Alternative B: [description] - possible but [tradeoff]
    validations:
      required: false

  - type: dropdown
    id: complexity
    attributes:
      label: Estimated Complexity
      description: How complex do you think this is?
      options:
        - Small - A few hours of work
        - Medium - A few days of work
        - Large - A week or more
        - Unknown - Needs investigation
    validations:
      required: true

  - type: textarea
    id: context
    attributes:
      label: Additional Context
      description: Any other context, mockups, or references?
    validations:
      required: false

  - type: checkboxes
    id: help-check
    attributes:
      label: Contribution
      options:
        - label: I'm willing to help implement this feature
          required: false
```

---

## ISSUE_TEMPLATE/03-task.yml

```yaml
name: 📋 Task
description: Create an implementation task (for maintainers/contributors)
title: "[Task]: "
labels: ["task"]
body:
  - type: markdown
    attributes:
      value: |
        Use this template for well-defined implementation work.
        For exploratory work, use Feature Request first.

  - type: textarea
    id: description
    attributes:
      label: Task Description
      description: What needs to be done?
      placeholder: |
        Implement X to enable Y.
        
        This involves:
        - Change A
        - Change B
        - Update tests
    validations:
      required: true

  - type: textarea
    id: acceptance
    attributes:
      label: Acceptance Criteria
      description: How do we know this is done?
      placeholder: |
        - [ ] Criterion 1
        - [ ] Criterion 2
        - [ ] Tests pass
        - [ ] Documentation updated
    validations:
      required: true

  - type: textarea
    id: related
    attributes:
      label: Related Issues/Specs
      description: Link any related issues, specs, or documentation
      placeholder: |
        - Spec: #123
        - Depends on: #456
        - Blocks: #789
    validations:
      required: false

  - type: dropdown
    id: complexity
    attributes:
      label: Complexity
      options:
        - S - Less than 2 hours
        - M - Half day to full day
        - L - Multiple days
        - XL - Week or more (consider breaking down)
    validations:
      required: true

  - type: dropdown
    id: ai-suitable
    attributes:
      label: AI Suitability
      description: Is this task suitable for AI agent implementation?
      options:
        - "Yes - Well-scoped, clear criteria"
        - "Partial - Needs human review/guidance"
        - "No - Requires human judgment/context"
    validations:
      required: false

  - type: checkboxes
    id: ready-check
    attributes:
      label: Ready for Work
      options:
        - label: Acceptance criteria are clear and testable
          required: true
        - label: Dependencies are identified
          required: false
        - label: Spec exists (if needed for this scope)
          required: false
```

---

## pull_request_template.md

```markdown
## Summary

<!-- Brief description of what this PR does -->

## Related Issue

Closes #<!-- issue number -->

## Changes

<!-- What changed? List the main changes -->

- 
- 
- 

## Spec Compliance

<!-- If this PR implements a spec, verify compliance -->

- [ ] No spec required (simple change)
- [ ] Spec exists at `.project/{issue#}/spec.md`
- [ ] Spec status is `approved` (or explain why implementing draft/review spec)
- [ ] Implementation matches spec requirements
- [ ] Any deviations are documented below

<!-- If there are deviations from spec, explain: -->

## Testing

<!-- How was this tested? -->

- [ ] Unit tests added/updated
- [ ] Manual testing performed
- [ ] No tests needed (docs/config only)

## Checklist

- [ ] Code follows project conventions
- [ ] Self-review completed
- [ ] Documentation updated (if needed)
- [ ] No unrelated changes included
- [ ] plan.md steps are checked off

## Screenshots

<!-- If applicable, add screenshots -->

## Notes for Reviewers

<!-- Any context that helps reviewers? -->

---

<!-- AI contributors: Feel free to note your model/tool below -->
<!-- Generated by: Claude Code / GitHub Copilot / etc. -->
```

---

## Integration with project-mgmt Plugin

These templates complement the project-mgmt Claude Code plugin (v0.1.0).

### Alignment Summary

| GitHub Spec Element | Plugin Element | Notes |
|---------------------|----------------|-------|
| `.project/{issue#}/` directory | Same | Standard location for all project files |
| plan.md, spec.md, findings.md, progress.md | Same | Four core tracking files |
| 6 workflow phases | `references/*.md` files | start, specify, plan, implement, pr, sync |
| Plan phase field | `plan-template.md` | Tracks current workflow phase |
| Spec status: `draft \| review \| approved` | `spec-template.md` | Tracks spec approval |
| Issue → Spec flow | start → specify phases | Issues feed into spec creation |
| PR template | pr phase | Creates PR with spec compliance |
| PR spec compliance | plan.md checkboxes | Review checks steps completed |

### How They Work Together

1. **Issue Templates** → Capture structured input for the plugin's start phase
2. **CONTRIBUTING.md** → Explains the 6-phase workflow to contributors
3. **PR Template** → Used by pr phase, validates spec compliance and plan.md completion
4. **Task Template AI Suitability** → Helps triage which issues to assign to AI agents

### Workflow Example

```
1. User creates issue using 02-feature.yml template
   → Labels: enhancement, triage

2. Maintainer triages and marks ready for work
   → Labels: enhancement, ready

3. Contributor picks up issue, starts spec-driven workflow:
   
   START phase:
   → Creates .project/123/plan.md (from issue)
   → Phase: specify
   
   SPECIFY phase:
   → Creates .project/123/spec.md (requirements)
   → Phase: plan
   
   PLAN phase:
   → Updates .project/123/plan.md (implementation steps)
   → Phase: implement
   
   IMPLEMENT phase:
   → Works through steps, logs to progress.md
   → Records findings to findings.md
   → Phase: pr (when complete)

4. PR phase:
   → Creates/updates branch
   → Commits changes
   → Creates PR using pull_request_template.md
   → Links issue with "Closes #123"
   → Confirms spec compliance
   → Phase: review

5. Reviewer checks PR against spec in .project/123/
   
   SYNC phase:
   → Updates GitHub issue with progress summary
```

---

## Setup Checklist

Before deploying, ensure:

- [ ] `.github` repository is **public** (required for org-wide defaults)
- [ ] Labels exist in `.github` repo: `bug`, `triage`, `enhancement`, `task`
- [ ] Labels are created in target repositories that will use these templates
- [ ] Discussion links point to correct GitHub Discussions URL

---

## Maintenance

- Review templates quarterly
- Update based on contributor feedback
- Keep in sync with project-mgmt plugin changes
- Test templates after GitHub UI changes
- Re-verify against GitHub Docs annually (structure may change)

---

## References

- [Creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
- [About issue and pull request templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates)
- [Syntax for issue forms](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms)
- [Syntax for GitHub's form schema](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-githubs-form-schema)
- [Creating a pull request template](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)
- [Configuring issue templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)