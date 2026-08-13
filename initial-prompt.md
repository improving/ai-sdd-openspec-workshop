# Bug Tracker — Product Requirements

Create a small “Bug Tracker” web application as a demo POC for a workshop teaching Spec-Driven Development (SDD) using OpenSpec.

## Tech Stack
- Frontend: React + TypeScript (Vite) + Tailwind CSS
- Backend: Node.js + Express + TypeScript
- Storage: in-memory only (no database)
- Tests: Vitest + Supertest for API tests
- Runtime: `npm run dev` must start both frontend and backend concurrently.
- Development API routing: the Vite dev server must proxy `/api/*` requests to the Express backend (for example, `http://localhost:3000`) so browser requests made from the frontend do not return a Vite 404.

## TDD Discipline (non-negotiable)
- Follow Red–Green–Refactor.
- For every behavior in the specs, write failing tests FIRST, then implement.
- Task lists must explicitly sequence: tests → implementation → refactor.

## Features

### Visual Reference

Use [`image.png`](./image.png) as the visual reference for the initial `create-bug` page. Match its overall layout, proportions, typography, spacing, controls, colors, and responsive behavior at approximately 1024×710px.

The written requirements in this document are authoritative where they clarify or differ from the image. Do not embed the image in the application; it is provided for implementation and visual verification only.

### create-bug
- Create a new bug with:
  - Title: required string, max 100 characters
  - Description: optional string
  - Severity: optional, one of `P1`, `P2`, `P3`
  - Status: defaults to `New`
  - CreatedAt: timestamp set automatically
- Validation: if Title is missing or exceeds 100 characters, show an error and do not create the bug.
- Submission behavior: the form must submit to the API through the configured development proxy, handle non-2xx responses without assuming the response body is valid JSON, and show a user-visible error instead of throwing an uncaught promise or JSON parse error.
- The create-bug implementation must include the initial application shell and all greenfield scaffolding required to run the feature end-to-end.
- The initial UI must reliably match the supplied Bug Tracker reference screenshot at approximately 1024×710px. Treat the screenshot as a visual acceptance reference, not merely inspiration.
- Use a single white page with one centered content column approximately 510px wide on desktop, with approximately 85–95px of top spacing and 16–20px horizontal page padding on narrow screens.
- Keep all content left-aligned within the column. Do not center the form fields or button text.
- Render the exact visible hierarchy and order below:
  1. Page heading: `Bug Tracker`
  2. Section heading: `Create Bug`
  3. Label and single-line text input: `Title`
  4. Label and multiline textarea: `Description`
  5. Label and native select: `Severity`
  6. Compact left-aligned submit button: `Create Bug`
  7. Section heading: `Bugs`
  8. Empty state: `No bugs yet.`
- Use a neutral sans-serif font, dark high-contrast headings, regular dark labels, and muted gray empty-state text.
- Use approximate typography: page heading 28–32px bold; section headings 24px bold; labels 16px.
- Inputs, textarea, and select must be full-width, white, lightly bordered, slightly rounded (approximately 4px), and comfortably padded. The textarea should be approximately 65px tall.
- The Severity select must show `Select severity` when unset and offer exactly `P1`, `P2`, and `P3`.
- The submit button must be compact rather than full-width, left-aligned, blue (similar to `#2563eb`), use white text, and have approximately 8px vertical and 18px horizontal padding.
- Use approximately 12px between each label and its control, 20–24px between fields, 18px between the final field and button, and 38–45px before the `Bugs` heading.
- The initial empty state must display exactly `No bugs yet.` in muted gray.
- Do not add navigation, sidebars, cards, hero sections, gradients, illustrations, decorative icons, dashboards, tables, badges, avatars, charts, or extra routes unless explicitly requested.
- The UI must remain usable on narrow screens: the content column must shrink fluidly, controls must not overflow, and the hierarchy must remain unchanged.
- Before considering create-bug complete, compare the rendered page against the reference screenshot at approximately 1024×710px and verify the visual acceptance criteria above.
- Before considering create-bug complete, verify from the running frontend that submitting a valid bug reaches the backend through the Vite proxy and returns a successful created bug response.

### list-bugs
- Display all bugs sorted newest-first.
- Each row shows:
  - Title, truncated to 50 characters with `…` when longer
  - Severity or `Untriaged` when not set
  - Status
  - CreatedAt

### triage-bug
- Triage sets Severity to one of `P1`, `P2`, `P3` and transitions Status from `New` to `Triaged`.
- Once a bug is `Triaged`, Severity cannot be changed again; reject such requests with a clear error.

## Constraints and Non-Goals
- No authentication, roles, persistence, edit, or delete operations.
- Minimal UI: one create form and one list view.
- Only the `create-bug` feature should include greenfield scaffolding (frontend, backend, tests, and a root `LAB-README.md`). Subsequent features must build on the existing scaffolding.

## Scope Guidance for the AI
- The user will request one feature at a time (e.g., `create-bug feature only, include greenfield scaffolding`).
- Generate the OpenSpec proposal/spec/design/tasks artifacts for only the requested feature.
- Do not re-scaffold or rewrite `LAB-README.md` unless the user explicitly asks for greenfield scaffolding.
- When implementing the create form, include automated coverage for the development API path/proxy and for a failed or non-JSON response; the submit action must never produce an uncaught `Unexpected end of JSON input` error.
