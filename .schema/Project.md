# Project Type Schema

## Description
A multi-action outcome (GTD definition: anything requiring more than one action).

## File Location
`Projects/prj-YYYYMMDD-NNN-short-name/index.md`

## Required Fields (Frontmatter)

```yaml
id: prj-YYYYMMDD-NNN           # Unique identifier
type: Project                   # Type discriminator
created: YYYY-MM-DD            # Creation date
title: String                  # Project title
status: Active|Someday|Done    # Project status
```

## Optional Fields

```yaml
owner: PersonID                # Project owner (you or someone else)
stakeholders: [PersonID, ...]  # People involved (bidirectional)
next_actions: [ActionID, ...]  # Explicitly marked next actions
actions: [ActionID, ...]       # All related actions (bidirectional)
dependencies: [ProjectID, ...] # Projects this depends on
dependents: [ProjectID, ...]   # Projects depending on this
target_date: YYYY-MM-DD       # Target completion
context: String               # Where/when this applies
tags: [String, ...]           # Freeform tags
```

## Body Content

Free-form markdown with suggested sections:
- Overview
- Goals
- Current Status
- Key Milestones
- Notes

## Relationships

- **People**: Many-to-many (owner, stakeholders)
- **Actions**: One-to-many (project generates actions)
- **Projects**: Many-to-many (dependencies form DAG)

## Lifecycle

- **Active**: Currently being worked on, has next_actions
- **Someday**: Not ready to start, no current next_actions
- **Done**: Completed, archived to Projects/Archive/

## Next Actions Property

The `next_actions` field explicitly marks which of the project's many actions are "next" in the GTD sense. During reviews:
- If empty and status=Active, identify next action
- If all next_actions are Done/Blocked, identify new ones
