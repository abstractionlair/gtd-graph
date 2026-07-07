# Person Type Schema

## Description
Represents an individual you interact with professionally or personally.

## File Location
`People/per-YYYYMMDD-NNN-name.md`

## Required Fields (Frontmatter)

```yaml
id: per-YYYYMMDD-NNN           # Unique identifier
type: Person                    # Type discriminator
created: YYYY-MM-DD            # Creation date
name: String                   # Full name
```

## Optional Fields

```yaml
role: String                   # Job title/role
team: String                   # Team/department
reports_to: PersonID           # Manager (if you manage them)
email: String                  # Email address
projects: [ProjectID, ...]     # Related projects (bidirectional)
actions: [ActionID, ...]       # Related actions (bidirectional)
meetings: MeetingSeriesID      # Regular meeting series
tags: [String, ...]           # Freeform tags
```

## Body Content

Free-form markdown with sections like:
- Role & Background
- Communication Style
- Current Focus
- Recent Context
- Notes

## Relationships

- **Projects**: Many-to-many (stakeholder, owner, participant)
- **Actions**: Many-to-many (assigned to, waiting on)
- **Meetings**: One-to-many meeting series

## Lifecycle

- Created when person becomes relevant
- Updated as context changes
- Archived when no longer active (move to People/Archive/)
