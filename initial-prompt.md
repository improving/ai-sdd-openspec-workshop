# Bug Tracker — Product Requirements

Create a small “Bug Tracker” web application as a demo POC for a workshop teaching Spec-Driven Development (SDD) using OpenSpec.

## Tech Stack
- Frontend: React + TypeScript (Vite) + Tailwind CSS
- Backend: Node.js + Express + TypeScript
- Storage: in-memory only (no database)
- Tests: Vitest + Supertest for API tests
- Runtime: `npm run dev` must start both frontend and backend concurrently

## TDD Discipline (non-negotiable)
- Follow Red–Green–Refactor.
- For every behavior in the specs, write failing tests FIRST, then implement.
- Task lists must explicitly sequence: tests → implementation → refactor.

## Features

### create-bug
- Create a new bug with:
  - Title: required string, max 100 characters
  - Description: optional string
  - Severity: optional, one of `P1`, `P2`, `P3`
  - Status: defaults to `New`
  - CreatedAt: timestamp set automatically
- Validation: if Title is missing or exceeds 100 characters, show an error and do not create the bug.

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
