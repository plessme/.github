# Plessme Development Workflow

## Issue Hierarchy

The plessme distributed system uses a two-level issue hierarchy for project management:

```text
Feature/Enabler (plessme/plessme repo)
├── Story (service repo A)
│   ├── Task (service repo A)
│   └── Task (service repo A)
└── Story (service repo B)
    └── Task (service repo B)
```

### Issue Types

**Parent Level (tracked in `plessme/plessme`):**

- **Feature**: Cross-cutting features spanning multiple repositories
- **Enabler**: Technical enablers (infrastructure, tooling, architecture)

**Child Level (tracked in service repositories):**

- **Story**: User-facing functionality in a single service
- **Task**: Technical task, subtask of a story

## Creating Issues

### 1. Create Feature/Enabler (Parent)

Features and Enablers are created in the central tracking repository:

```bash
# Navigate to plessme/plessme repository
cd plessme

# Create Feature or Enabler using Claude Code
/plessme-issue
# Select type: Feature or Enabler
# Follow prompts to provide details
```

**Output:** Issue created in `plessme/plessme` with tracking section for child issues

**Required Information:**

- Title and description
- Business value (Feature) or technical goal (Enabler)
- Acceptance criteria
- Estimated effort (Small/Medium/Large/XLarge)
- Technical stack
- Affected repositories
- Claude Code context (optional)

### 2. Create Story (Child of Feature/Enabler)

Stories implement part of a Feature or Enabler in a specific service:

```bash
# Navigate to service repository
cd backend-service  # or any service repo

# Create Story using Claude Code
/plessme-issue
# Select type: Story
# Provide parent reference: plessme/plessme#42
# Follow prompts to provide details
```

**Output:** Issue created in service repo with link to parent Feature/Enabler

**Required Information:**

- Title and description
- Parent Feature/Enabler reference (format: `plessme/plessme#42`)
- Acceptance criteria
- Estimated effort
- Technical stack
- Technical approach (optional)
- Claude Code context (optional)

### 3. Create Task (Child of Story)

Tasks are technical subtasks of a Story:

```bash
# In service repository
/plessme-issue
# Select type: Task
# Provide parent reference: backend-service#123
# Follow prompts to provide details
```

**Output:** Issue created in service repo with link to parent Story

**Required Information:**

- Title and description
- Parent Story reference (format: `owner/repo#123`)
- Technical details
- Estimated effort
- Acceptance criteria
- Testing strategy (optional)
- Claude Code context (optional)

## Issue Labels

### Type Labels

- `type: feature` - Cross-cutting features spanning multiple repos
- `type: enabler` - Technical enablers (infrastructure, tooling, architecture)
- `type: story` - User-facing functionality in a single service
- `type: task` - Technical task, subtask of a story

### Status Labels

- `status: planned` - Not started (default)
- `status: in-progress` - Currently being worked on
- `status: completed` - Done

## Parent-Child Linking

### Automatic Linking

When creating Stories or Tasks, the `/plessme-issue` skill automatically:

1. Creates a `## Parent` section in the child issue body
2. Links to the parent issue using the format `Relates to org/repo#number`
3. Allows Claude Code agents to fetch parent context during implementation

### Manual Linking

You can also manually link issues:

- In child issue body: Add `Relates to plessme/plessme#42` in the `## Parent` section
- In parent issue comments: Add task list items like `- [ ] plessme/backend-service#123`

## Using GitHub CLI

The GitHub CLI (`gh`) provides powerful tools for issue management:

```bash
# View issue details
gh issue view 123 --repo plessme/plessme

# List issues by label
gh issue list --label "type: feature" --repo plessme/plessme

# Search for issues
gh issue list --search "authentication" --repo plessme/plessme

# Add comment to issue
gh issue comment 123 --body "Implementation started"

# Close issue
gh issue close 123
```

## GitHub Projects

Consider using GitHub Projects (beta) for visual boards:

- Create organization-level project
- Add issues from multiple repositories
- Use custom fields for additional metadata
- Automate status updates with workflows

## Implementation Workflow

Implementation is handled separately via custom command using specialized agents. See separate documentation for the feature development workflow.

## Best Practices

1. **Start with Features/Enablers**: Always create the parent issue first
2. **Break down work**: Split Features into Stories, Stories into Tasks
3. **Link properly**: Always reference parent issues when creating children
4. **Update progress**: Use status labels and comments to track progress
5. **Use Claude context**: Provide clear instructions in the Claude Code Context field
6. **Close hierarchically**: Close Tasks → Stories → Features as work completes

## Example Workflow

```bash
# 1. Create Feature
cd ~/Work/plessme/plessme
/plessme-issue
# → Creates plessme/plessme#42 (Feature: User Authentication)

# 2. Create Story in backend service
cd ~/Work/plessme/backend-service
/plessme-issue
# → Creates backend-service#123 (Story: API authentication endpoints)
# → Links to plessme/plessme#42

# 3. Create Tasks
/plessme-issue
# → Creates backend-service#124 (Task: JWT middleware)
# → Links to backend-service#123

/plessme-issue
# → Creates backend-service#125 (Task: Token validation)
# → Links to backend-service#123

# 4. Implement using agents (separate workflow)
# Agents fetch context from parent issues during implementation
```

## Questions?

For help with the workflow or tools:

- Check issue templates in this repository
- Review the `/plessme-issue` skill documentation
- Consult the main project README
