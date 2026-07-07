# Document Type Schema

## Description
A formal document (plan, presentation, report, analysis, etc.). Uses sidecar metadata pattern to keep document content clean and ready to share.

## File Location
```
Documents/doc-YYYYMMDD-NNN-title.md           # Document content (no frontmatter)
Documents/doc-YYYYMMDD-NNN-title.md.meta.md  # Metadata with frontmatter
```

## Content File (.md)
The document content file contains pure markdown - no YAML frontmatter. Ready to share, convert to PDF, or present.

**Format:**
```
# [Document Title]

[Document content in markdown - headings, paragraphs, lists, tables, etc.]
```

## Metadata File (.meta.md)

### Required Fields

```yaml
id: doc-YYYYMMDD-NNN           # Unique identifier
type: Document                  # Type discriminator
created: YYYY-MM-DD            # Creation date
title: String                  # Document title
source_file: String            # Filename of document content
```

### Optional Fields

```yaml
from_action: ActionID          # Action that produced this
related_projects: [ProjectID, ...] # Related projects
people: [PersonID, ...]        # People involved or audience
status: Draft|Review|Final|Published  # Document status
audience: String               # Intended audience
version: String                # Version number if applicable
tags: [String, ...]           # Freeform tags
```

### Metadata Body Content

Optional markdown notes about the document:
- Purpose and context
- How it was used
- Feedback received
- Distribution list
- Follow-up actions

## Relationships

- **People**: Many-to-many (authors, reviewers, audience)
- **Actions**: Many-to-one (produced by action)
- **Projects**: Many-to-many (relates to)

## Workflow

**Creating a document:**
1. Create content file: `doc-YYYYMMDD-NNN-title.md` (pure markdown)
2. Create metadata file: `doc-YYYYMMDD-NNN-title.md.meta.md` (with frontmatter)
3. Update action's `outputs: [...]` to reference this document
4. Update related projects/people if needed (bidirectional)

**Sharing a document:**
1. Content file is ready to use - no frontmatter to strip
2. Convert to PDF, DOCX, slides, etc. as needed
3. Update metadata status: Draft → Review → Final → Published
4. Record in metadata notes: who reviewed, where shared, feedback

## Why Sidecar Pattern?

Keeping frontmatter separate means:
- Document content is presentation-ready
- Easy conversion to other formats (PDF, DOCX, slides)
- No metadata pollution in shared versions
- Still participates fully in linking system

## Document Types

Common document types (use tags or status to distinguish):
- **Plans**: Project plans, roadmaps, strategies
- **Reports**: Status reports, analysis, findings
- **Presentations**: Slide content (can convert to reveal.js, PPTX)
- **Decisions**: Can also use Decision type for formal decision records
- **Analysis**: Technical analysis, evaluations
- **Proposals**: Feature proposals, architecture proposals

## Status Lifecycle

1. **Draft**: Work in progress
2. **Review**: Under review by others
3. **Final**: Approved, ready to use
4. **Published**: Shared/distributed to audience

## Lifecycle

Documents are generally permanent. May archive old/superseded versions to Documents/Archive/.
Metadata tracks version history and usage.
