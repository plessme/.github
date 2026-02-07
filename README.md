# Plessme Organization Configuration

This repository contains organization-wide configuration for the plessme distributed system.

## Contents

### Issue Templates

This repository provides four standardized issue templates for all repositories in the organization:

- **Feature** (`ISSUE_TEMPLATE/feature.yml`): Cross-cutting features spanning multiple services
- **Enabler** (`ISSUE_TEMPLATE/enabler.yml`): Technical enablers for infrastructure, tooling, or architecture
- **Story** (`ISSUE_TEMPLATE/story.yml`): User-facing functionality in a single service
- **Task** (`ISSUE_TEMPLATE/task.yml`): Technical tasks or subtasks

### Pull Request Template

Standard pull request template (`PULL_REQUEST_TEMPLATE.md`) for consistent PR documentation.

### Workflow Documentation

See `profile/WORKFLOW.md` for detailed workflow documentation on using these templates.

## How It Works

Any repository in the `plessme` organization **without** its own `.github/ISSUE_TEMPLATE/` directory will automatically inherit these templates.

Individual repositories can:

- **Inherit all templates**: Do nothing (default behavior)
- **Override templates**: Create their own `.github/ISSUE_TEMPLATE/` directory
- **Selective override**: Copy specific templates to customize, inherit others

## Repository-Specific Overrides

### plessme/plessme (Tracking Repository)

The central tracking repository overrides templates to only show Feature and Enabler types, since Stories and Tasks are tracked in service repositories.

### Service Repositories

Service repositories inherit all four templates by default, but developers typically use Story and Task templates.

## Usage with Claude Code

These templates are optimized for use with the `/plessme-issue` Claude Code skill, which:

- Guides users through creating properly structured issues
- Automatically links child issues to parents
- Applies consistent labels and formatting
- Structures issue bodies for agent parsing

## Template Structure

All templates follow GitHub Issue Forms syntax (YAML) and include:

- **Structured fields**: Title, description, acceptance criteria, etc.
- **Estimated effort**: Small/Medium/Large/XLarge dropdown
- **Technical stack**: Free-form text for specifying technologies
- **Parent references**: For linking Stories/Tasks to their parents
- **Claude Code context**: Special instructions for AI-assisted implementation
- **Consistent labels**: `type: *` and `status: *` for filtering

## Issue Hierarchy

```text
Feature/Enabler (plessme/plessme)
├── Story (service-repo-a)
│   ├── Task (service-repo-a)
│   └── Task (service-repo-a)
└── Story (service-repo-b)
    └── Task (service-repo-b)
```

## Links

- [Workflow Documentation](profile/WORKFLOW.md)
- [plessme/plessme Tracking Repository](https://github.com/plessme/plessme)

## Contributing

To update these templates:

1. Create a branch in this repository
2. Modify templates in `.github/ISSUE_TEMPLATE/`
3. Test templates by creating test issues
4. Submit PR for review

Changes will propagate to all repositories that inherit these templates.
