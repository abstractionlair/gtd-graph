# Ontology-Driven GTD Knowledge Graph

A lightweight, agent-maintained template for a personal GTD (Getting Things Done) system.

## What it is

This repository is a knowledge graph expressed as plain Markdown files. Every entity — a project, a person, an action, a decision, a note — is an instance of a defined type in `.schema/`. The schema is the contract; the agent is the runtime. There is no application code, no database, and no server.

An LLM agent (for example, Claude Code) reads the schemas, creates and updates files, and maintains bidirectional links between entities. Changes persist through the same review workflow you already use for code: each session's edits become a git branch, then a pull request.

## Why it works

- **Schema as contract**: before adding a new entity, the agent reads `.schema/<Type>.md` so every file follows the same shape.
- **Stable IDs**: files use `type-YYYYMMDD-NNN-description` names, so links stay valid even when titles change.
- **Bidirectional links**: relationships are stored on both sides, so the graph stays consistent and grep-friendly.
- **Plain files**: everything is Markdown + YAML frontmatter. You can inspect, edit, or archive with standard tools.
- **GTD-native**: actions are atomic, physical next steps; projects explicitly mark their current next actions.

## How it works

1. The agent starts each session on a fresh branch from `main`.
2. It reads the relevant schemas, then reads the relevant `People/`, `Projects/`, `Actions/`, and other files.
3. It makes edits, creates new files, and updates both sides of every relationship.
4. At the end of the session, the changes become a PR for review.
5. You merge the PR to persist the changes to `main`.

This is a personal productivity system, not a software project. File creation is part of the workflow: the agent should create `Action` files when you mention new tasks, `Project` directories when you start new initiatives, `Decision` records when you reason through choices, and `Notes` when you capture thinking.

## Directory layout

```
.schema/       Type definitions
People/        Person instances
Projects/      Multi-action outcomes
Actions/       Atomic next actions
Decisions/     Decision records
Notes/         Informal notes
Meetings/      Meeting prep and notes
```

## How to point Claude Code at it

1. Clone or copy this repository into a workspace Claude Code can access.
2. Open the workspace in Claude Code and include the prompt in `CLAUDE.md` as the project instructions.
3. In the first session, ask the agent to review the system state and start capturing your current work.
4. Let each session's edits become a PR; review and merge to persist.

The synthetic examples in `People/`, `Projects/`, `Actions/`, `Notes/`, and `Decisions/` show the expected file format, ID convention, and bidirectional-linking pattern.

## License

MIT — see `LICENSE`.
