# Email Type Schema

## Description
A draft or sent email communication. Uses sidecar metadata pattern to keep email content clean and ready to send.

## File Location
```
Emails/eml-YYYYMMDD-NNN-recipient-subject.md           # Email content (no frontmatter)
Emails/eml-YYYYMMDD-NNN-recipient-subject.md.meta.md  # Metadata with frontmatter
```

## Content File (.md)
The email content file contains pure markdown - no YAML frontmatter. Ready to copy-paste or send.

**Format:**
```
To: [Recipient name(s)]
From: [Your name]
Subject: [Email subject]

---

[Email body in markdown]
```

## Metadata File (.meta.md)

### Required Fields

```yaml
id: eml-YYYYMMDD-NNN           # Unique identifier
type: Email                     # Type discriminator
created: YYYY-MM-DD            # Creation date
to: [PersonID, ...]            # Recipients (with readable IDs)
subject: String                # Email subject
source_file: String            # Filename of email content
```

### Optional Fields

```yaml
cc: [PersonID, ...]            # CC recipients
from_action: ActionID          # Action that produced this
related_projects: [ProjectID, ...] # Related projects
status: Draft|Sent             # Email status
sent_date: YYYY-MM-DD         # When sent (if status=Sent)
tags: [String, ...]           # Freeform tags
```

### Metadata Body Content

Optional markdown notes about the email:
- Context for why it was sent
- Follow-up needed
- Response received
- Outcome

## Relationships

- **People**: Many-to-many (to, cc)
- **Actions**: Many-to-one (produced by action)
- **Projects**: Many-to-many (relates to)

## Workflow

**Creating an email:**
1. Create content file: `eml-YYYYMMDD-NNN-description.md` (pure markdown)
2. Create metadata file: `eml-YYYYMMDD-NNN-description.md.meta.md` (with frontmatter)
3. Update action's `outputs: [...]` to reference this email
4. Update related projects/people if needed (bidirectional)

**Sending an email:**
1. Copy content from `.md` file (no frontmatter to strip!)
2. Paste into email client or export as needed
3. Update metadata: `status: Draft` → `status: Sent`, add `sent_date`

## Why Sidecar Pattern?

Keeping frontmatter separate means:
- Email content is clean and ready to use
- No need to strip YAML before sending
- Can convert to other formats (PDF, HTML) easily
- Still participates fully in linking system via metadata

## Lifecycle

1. **Draft**: Created but not sent yet
2. **Sent**: Actually sent to recipients

After sending, may archive to Emails/Archive/YYYY-MM/
Metadata travels with the content file.
