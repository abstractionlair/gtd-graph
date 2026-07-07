# Decision Type Schema

## Description
A formal decision record capturing what was decided, why, and context. Uses sidecar metadata pattern to keep decision content clean and shareable.

## File Location
```
Decisions/dec-YYYYMMDD-NNN-decision-topic.md           # Decision content (no frontmatter)
Decisions/dec-YYYYMMDD-NNN-decision-topic.md.meta.md  # Metadata with frontmatter
```

## Content File (.md)
The decision content file contains pure markdown - no YAML frontmatter. Ready to share with stakeholders or reference later.

**Suggested structure:**
```
# [Decision Title]

## Context
Why this decision was needed...

## Decision
What was decided...

## Rationale
Why this choice...

## Alternatives Considered
- Option A: [description and why not chosen]
- Option B: [description and why not chosen]

## Consequences
Expected impact and implications...

## Implementation
How this will be executed...
```

## Metadata File (.meta.md)

### Required Fields

```yaml
id: dec-YYYYMMDD-NNN           # Unique identifier
type: Decision                  # Type discriminator
created: YYYY-MM-DD            # Decision date
title: String                  # Decision summary
source_file: String            # Filename of decision content
status: Proposed|Decided|Implemented
```

### Optional Fields

```yaml
decision_makers: [PersonID, ...] # Who made the decision (with readable IDs)
stakeholders: [PersonID, ...]    # Who's affected
from_action: ActionID            # Action that produced this
related_projects: [ProjectID, ...] # Related projects
implementation_actions: [ActionID, ...] # Actions to implement
alternatives_considered: [String, ...] # Other options evaluated (brief list)
tags: [String, ...]             # Freeform tags
```

### Metadata Body Content

Optional markdown notes about the decision:
- How it was received
- Challenges during implementation
- Retrospective learnings
- Updates or reversals

## Relationships

- **People**: Many-to-many (decision makers, stakeholders)
- **Projects**: Many-to-many (impacts projects)
- **Actions**: One-to-many (spawns implementation actions)

## Workflow

**Creating a decision:**
1. Create content file: `dec-YYYYMMDD-NNN-topic.md` (pure markdown with decision record)
2. Create metadata file: `dec-YYYYMMDD-NNN-topic.md.meta.md` (with frontmatter)
3. Update action's `outputs: [...]` to reference this decision
4. Update related projects/people (bidirectional)
5. Create implementation actions if needed, link in metadata

**Sharing a decision:**
1. Content file is ready to share - no frontmatter
2. Convert to PDF or email as needed
3. Metadata tracks stakeholders and implementation separately

## Why Sidecar Pattern?

Keeping frontmatter separate means:
- Decision content is clean and professional
- Easy to share with stakeholders who don't need metadata
- Can convert to other formats for distribution
- Metadata tracks relationships without cluttering the decision

## Status Lifecycle

1. **Proposed**: Under consideration, not yet decided
2. **Decided**: Decision made, not yet implemented
3. **Implemented**: Fully executed and in effect

## Usage

Decision records provide:
- Historical context for future questions ("Why did we choose X?")
- Rationale for current state
- Accountability for choices
- Reference for similar future decisions
- Onboarding material for new team members

## Archiving

Decisions are generally permanent - they're historical records. May move very old decisions to Decisions/Archive/ but keep them accessible for reference.
