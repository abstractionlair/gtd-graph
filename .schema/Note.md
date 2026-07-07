# Note Type Schema

## Description
Informal notes, observations, meeting notes, or quick captures. Notes can optionally use sidecar metadata when they need to participate in the linking system.

## File Location

**Simple notes (no metadata needed):**
```
Notes/note-YYYYMMDD-NNN-topic.md    # Just the note content
```

**Notes with relationships (optional metadata):**
```
Notes/note-YYYYMMDD-NNN-topic.md           # Note content
Notes/note-YYYYMMDD-NNN-topic.md.meta.md  # Metadata with frontmatter (optional)
```

## When to Use Metadata

**Use metadata (.meta.md) when:**
- Note needs to link to projects, people, or actions
- Note is output from an action (tracked in system)
- Note has structured relationships you want to query
- Note is important reference material for multiple contexts

**Skip metadata when:**
- Quick capture or brainstorming
- Standalone observation
- Temporary note that will be processed later
- Personal reflection not tied to projects

## Content File (.md)
Notes are free-form markdown. No required structure.

Common patterns:
- Meeting notes
- Research notes
- Observations and insights
- Brainstorming captures
- Quick references

## Metadata File (.meta.md) - Optional

### Required Fields (if using metadata)

```yaml
id: note-YYYYMMDD-NNN          # Unique identifier
type: Note                      # Type discriminator
created: YYYY-MM-DD            # Creation date
title: String                  # Note title/summary
source_file: String            # Filename of note content
```

### Optional Fields

```yaml
from_action: ActionID          # Action that produced this
related_projects: [ProjectID, ...] # Related projects
people: [PersonID, ...]        # People mentioned or involved
tags: [String, ...]           # Freeform tags
meeting_date: YYYY-MM-DD      # If meeting notes
```

### Metadata Body Content

Optional context about the note:
- Why it was created
- How it's being used
- Follow-up needed

## Relationships (when metadata exists)

- **People**: Many-to-many (mentioned, involved)
- **Actions**: Many-to-one (produced by action)
- **Projects**: Many-to-many (relates to)

## Workflow

**Simple note (no metadata):**
1. Create `note-YYYYMMDD-NNN-topic.md`
2. Write content
3. Done - no linking needed

**Note with metadata:**
1. Create `note-YYYYMMDD-NNN-topic.md` (content)
2. Create `note-YYYYMMDD-NNN-topic.md.meta.md` (metadata)
3. Update action's `outputs: [...]` if from action
4. Update related projects/people (bidirectional)

**Promoting a simple note:**
If a simple note later becomes important:
1. Create the `.meta.md` file
2. Add relationships
3. Update bidirectional links

## Why Optional Metadata?

Notes are often quick captures. Requiring metadata for every note would slow down capture and create maintenance burden.

Only add metadata when the note needs to be:
- Findable via relationships
- Tracked as output of work
- Referenced from multiple contexts

## Queries

```bash
# All notes (simple + with metadata)
ls Notes/*.md | grep -v "\.meta\.md$"

# Notes with metadata (have relationships)
ls Notes/*.meta.md

# Notes related to a project
grep -l "related_projects:.*prj-XXXXXX" Notes/*.meta.md
```

## Lifecycle

Notes can be:
- **Active**: Frequently referenced
- **Archived**: Move to Notes/Archive/ when no longer relevant
- **Deleted**: Simple notes can be deleted when obsolete
- **Promoted**: Add metadata when note becomes important
