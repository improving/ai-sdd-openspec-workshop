Create a small “Bug Tracker” web application as a demo POC for a workshop teaching SDD using OpenSpec.

Tech stack:
- Frontend: React + TypeScript (Vite) + Tailwind CSS
  - Clean frontend look and feel
  - Modern, professional design
- Backend: Node.js + Express + TypeScript
- Storage: in-memory only (no database)
- Tests: Vitest (and Supertest for API tests if needed)
- Runtime: The app should be scaffolded to run frontend and backend together with a single command (npm run dev)

TDD is REQUIRED (non-negotiable):
- Follow Red–Green–Refactor.
- For every behavior in the specs, write tests FIRST (failing), then implement.
- The task list must explicitly sequence: tests → implementation → refactor.

Include a comprehensive README.md in the root of the project.

Features (minimal but complete):
1) Create Bug
- Fields: Title (required, max 100 chars), Description (optional), Severity (P1/P2/P3 optional at creation), Status (defaults to “New”), CreatedAt.
- Validation: if Title missing or >100 chars, show error and do not create.

1) List Bugs
- Show all bugs sorted newest-first.
- Each row shows Title (truncate with “…” after 50 chars), Severity (or “Untriaged”), Status, CreatedAt.

1) Triage Bug (state rule)
- Triage sets Severity (P1/P2/P3) and transitions Status from “New” → “Triaged”.
- Once “Triaged”, Severity cannot be changed again (reject with clear error).

Constraints / non-goals:
- No auth/roles, no persistence, no edit/delete, minimal UI (one create form + list view).
- Provide Given/When/Then acceptance criteria with at least 2 edge cases per feature.
- Include a small ordered task list suitable for a short lab, with tests-first steps for each feature.
