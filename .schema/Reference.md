# Reference Type Schema

## Description
A reference file (document, PDF, image, spreadsheet, etc.) that provides supporting information for projects and actions. Uses sidecar metadata pattern for external formats.

## File Location
```
References/ref-YYYYMMDD-NNN-description.{ext}
References/ref-YYYYMMDD-NNN-description.{ext}.meta.md
```

The actual file and its metadata sidecar share the same base name.

## Metadata File Required Fields

```yaml
id: ref-YYYYMMDD-NNN           # Unique identifier
type: Reference                 # Type discriminator
created: YYYY-MM-DD            # When added to system
title: String                  # Human-readable title
source_file: String            # Filename of actual reference
format: String                 # File format (PDF, XLSX, PNG, etc.)
```

## Optional Fields

```yaml
original_name: String          # Original filename before ingestion
related_projects: [ProjectID, ...] # Projects this supports (bidirectional)
related_actions: [ActionID, ...] # Actions using this reference
people: [PersonID, ...]        # People associated with this
source_url: String             # Original URL if downloaded
author: String                 # Document author
date: YYYY-MM-DD              # Document date (different from created)
tags: [String, ...]           # Freeform tags
```

## Metadata Body Content

Free-form markdown describing:
- What this reference contains
- Key sections or highlights
- Why it's relevant
- How to use it
- Notes and observations

## Relationships

- **Projects**: Many-to-many (reference supports multiple projects)
- **Actions**: Many-to-many (reference used by actions)
- **People**: Many-to-many (reference relates to people)

## File Naming Convention

**On ingestion:**
1. Determine next sequence number for date
2. Create descriptive slug from title
3. Rename file: `ref-YYYYMMDD-NNN-slug.{ext}`
4. Store original filename in `original_name` field
5. Create companion `.meta.md` file

**Example:**
- Original: `Endur_Contract_Final_v3_2025.pdf`
- Renamed: `ref-20251115-001-endur-contract.pdf`
- Metadata: `ref-20251115-001-endur-contract.pdf.meta.md`
- Metadata contains: `original_name: "Endur_Contract_Final_v3_2025.pdf"`

## Supported Formats

Any format, but common ones:
- **Documents**: PDF, DOCX, TXT, MD
- **Spreadsheets**: XLSX, CSV
- **Images**: PNG, JPG, SVG
- **Presentations**: PPTX, KEY
- **Data**: JSON, YAML, XML

## Why Sidecar Metadata?

External formats (PDF, XLSX, PNG, etc.) can't contain YAML frontmatter. Sidecar `.meta.md` files:
- Provide frontmatter for any format
- Enable bidirectional linking
- Allow searching/querying all references
- Keep reference content immutable
- Support markdown notes about the reference

## Queries

```bash
# References for a project
grep -l "related_projects:.*prj-20250115-001" References/*.meta.md

# References by format
grep -l "format: PDF" References/*.meta.md

# References by tag
grep -l "tags:.*contract" References/*.meta.md
```

## Lifecycle

- References are generally permanent (rarely deleted)
- May archive old/obsolete ones to References/Archive/
- Metadata can be updated as relationships change
- Actual files are immutable (don't edit PDFs in place)
