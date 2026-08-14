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
- Provide an end-to-end create-bug workflow with greenfield application scaffolding when this is the initial feature.
- The workflow shall collect a required Title (nonblank, maximum 100 characters), optional Description, and optional Severity (`P1`, `P2`, or `P3`).
- A valid submission shall create and persist a bug with the submitted fields, status `New`, and an automatically generated `CreatedAt` timestamp.
- Invalid title input shall show a user-visible validation error and shall not create a bug.
- The frontend shall submit through the configured Vite `/api/*` proxy and shall handle non-2xx, network, and non-JSON responses without uncaught or JSON parsing errors.
- After successful creation, the user shall receive visible confirmation and the bug list shall reflect the created bug.
- The create page shall match the supplied visual reference in hierarchy, responsive layout, typography, spacing, controls, colors, and empty-state presentation; the reference is an acceptance criterion, not inspiration.
- The initial page shall contain one create form and one bug list with the visible headings `Bug Tracker`, `Create Bug`, and `Bugs`; an empty list shall display exactly `No bugs yet.`.
- The page shall remain usable on narrow screens and shall not add navigation, extra routes, or unrelated UI elements.
- Verify the workflow with frontend tests, backend API tests, visual comparison at approximately 1024×710px, and a running-browser submission through the Vite proxy.

### list-bugs
- Display all bugs sorted newest-first.
- Each row shows:
  - Title, truncated to 50 characters with `…` when longer
  - Severity or `Untriaged` when not set
  - Status
  - CreatedAt

### triage-bug
- Provide `POST /api/bugs/:id/triage`, accepting a severity of `P1`, `P2`, or `P3` and returning the updated bug.
- A valid request shall assign the severity and transition a `New` bug to `Triaged`.
- Missing bug IDs, missing or unsupported severities, and requests against an already-triaged bug shall return clear client errors without mutating the bug.
- The bug list shall expose triage directly: each `New` bug shall provide inline severity selection and a Triage action that is unavailable until a supported severity is selected.
- The frontend shall submit the selected severity and correct bug ID through the configured Vite proxy.
- After success, the list shall show the server-authoritative severity and `Triaged` status; already-triaged bugs shall display their values without resubmission controls.
- Triage failures, including network and non-JSON responses, shall be visible to the user while preserving the bug's displayed state.
- Verify the feature with Supertest API tests, React Testing Library component tests, and running-browser confirmation of the complete list-to-triage workflow.

## Constraints and Non-Goals
- No authentication, roles, persistence, edit, or delete operations.
- Minimal UI: one create form and one list view.
- Only the `create-bug` feature should include greenfield scaffolding (frontend, backend, tests, and a root `LAB-README.md`). Subsequent features must build on the existing scaffolding.

## Scope Guidance for the AI
- The user will request one feature at a time (e.g., `create-bug feature only, include greenfield scaffolding`).
- Generate the OpenSpec proposal/spec/design/tasks artifacts for only the requested feature.
- Do not re-scaffold or rewrite `LAB-README.md` unless the user explicitly asks for greenfield scaffolding.
- When implementing the create form, include automated coverage for the development API path/proxy and for a failed or non-JSON response; the submit action must never produce an uncaught `Unexpected end of JSON input` error.
- For every feature that adds or changes an API capability, inspect all existing frontend surfaces that consume the affected resource and include the required user interaction, component tests, and running-browser verification in the same feature scope unless the user explicitly declares the feature backend-only.
- A feature is not complete when its backend tests pass alone: all specified user-facing behavior, API behavior, frontend behavior, and corresponding automated tests must be represented in the OpenSpec requirements and tasks.
