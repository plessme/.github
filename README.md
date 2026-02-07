# Plessme Organization Configuration

This repository contains organization-wide configuration for the plessme distributed system.

## Contents

### Issue Templates

This repository provides standardized issue templates for **service repositories**:

- **Story** (`ISSUE_TEMPLATE/story.yml`): User-facing functionality in a single service
- **Task** (`ISSUE_TEMPLATE/task.yml`): Technical tasks or subtasks

**Note:** Feature and Enabler templates are defined in the `plessme/plessme` tracking repository only, as these issue types should only be created there.

### Pull Request Template

Standard pull request template (`PULL_REQUEST_TEMPLATE.md`) for consistent PR documentation.

### Workflow Documentation

See `profile/WORKFLOW.md` for detailed workflow documentation on using these templates.

## How It Works

Any repository in the `plessme` organization **without** its own `.github/ISSUE_TEMPLATE/` directory will automatically inherit these templates (Story and Task).

**Template Distribution:**

- **Organization `.github` (this repo)**: Story and Task templates
  - Inherited by all service repositories
  - Prevents creating Features/Enablers in the wrong place

- **`plessme/plessme` tracking repository**: Feature and Enabler templates
  - Local override ensures only Features/Enablers can be created there
  - Enforces the hierarchy at the template level

This design prevents mistakes by making it **impossible** to create the wrong issue type in the wrong repository.

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
- **Parent references**: For linking Stories to Features/Enablers, Tasks to Stories
- **Claude Code context**: Special instructions for AI-assisted implementation
- **Consistent labels**: `type: story`, `type: task`, `status: planned`

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
