# Action Type Schema

## Description
A single, physical next action (GTD definition). The atomic unit of work.

## File Location
`Actions/act-YYYYMMDD-NNN-short-description.md`

## Required Fields (Frontmatter)

```yaml
id: act-YYYYMMDD-NNN           # Unique identifier
type: Action                    # Type discriminator
created: YYYY-MM-DD            # Creation date
title: String                  # Action description (verb phrase)
status: Ready|InProgress|Blocked|Done
```

## Optional Fields

```yaml
projects: [ProjectID, ...]     # Related projects (many-to-many, bidirectional)
people: [PersonID, ...]        # Related people (bidirectional)
context: @office|@email|@phone|@home|@anywhere  # GTD context
estimated_time: Number         # Minutes
depends_on: [ActionID, ...]    # Other actions this depends on
waiting_on: [PersonID, ...]    # People we're waiting on (if Blocked)
waiting_on_note: String        # What we're waiting for
outputs: [OutputID, ...]       # Artifacts produced by this action
completed: YYYY-MM-DD          # Completion date (when status=Done)
tags: [String, ...]           # Freeform tags
```

## Body Content

Free-form markdown:
- Context and background
- Sub-task checklist (if needed)
- Notes
- Links to related items

## Relationships

- **Projects**: Many-to-many (an action can serve multiple projects)
- **People**: Many-to-many (assigned to, waiting on)
- **Actions**: Many-to-many (dependencies form DAG)
- **Outputs**: One-to-many (produces artifacts)

## Status Lifecycle

1. **Ready**: Can be worked on now, no blockers
2. **InProgress**: Currently being worked on
3. **Blocked**: Waiting on something/someone (see waiting_on fields)
4. **Done**: Completed

## Archiving

When status=Done, action eventually moves to Actions/Archive/YYYY-MM/
Links continue to work via ID resolution.

## Granularity

Actions should be atomic physical steps. If you find yourself with multiple distinct physical actions, create separate action files. Use checklists in the body only for sub-steps of a single coherent action.

## Queries

Common queries:
- Ready actions by context: `grep -l "status: Ready" Actions/*.md | xargs grep -l "context: @email"`
- Short actions available: `grep -l "estimated_time: [0-2][0-9]" Actions/*.md`
- Actions waiting on someone: `grep -l "waiting_on.*per-XXXXXX-NNN" Actions/*.md`
