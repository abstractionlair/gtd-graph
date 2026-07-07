# Choose React for the Atlas frontend

## Context

Project Atlas needs a small admin interface for the service catalog. The team wants
to minimize maintenance overhead and keep the skill set aligned with the rest of
the organization.

## Decision

Use React for the Project Atlas frontend.

## Rationale

- React is already used elsewhere in the organization.
- The admin UI is small enough that a lightweight React setup is sufficient.
- Hiring and onboarding are easier with a familiar stack.

## Alternatives Considered

- Vue.js: also a strong candidate, but less internal expertise.
- Svelte: appealing for bundle size, but fewer maintainers available.

## Consequences

- The requirements document should include React-specific assumptions.
- Future frontend contributors can onboard quickly.
- Bundle size may be slightly larger than with Svelte, but acceptable for an admin tool.

## Implementation

- Document the React choice in the Atlas requirements doc.
- Set up the frontend skeleton once the API contract is finalized.
