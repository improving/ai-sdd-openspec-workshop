# AI Spec-Driven Development Workshop

A hands-on workshop demonstrating **Spec-Driven Development (SDD)** using [OpenSpec](https://github.com/Fission-AI/OpenSpec) and an AI-enabled IDE (Devin Desktop, formerly Windsurf). Participants build a Bug Tracker app feature-by-feature using a propose → review → apply → verify → archive cycle.

---

## What You'll Build

A minimal **Bug Tracker** web application with:

- **Create Bug** — form with title, description, and optional severity
- **List Bugs** — sortable table showing all bugs newest-first
- **Triage Bug** — set severity and transition status from `New` → `Triaged`

### Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React + TypeScript + Vite + Tailwind CSS |
| Backend | Node.js + Express + TypeScript |
| Storage | In-memory (no database) |
| Tests | Vitest + React Testing Library + Supertest |

---

## Prerequisites

1. **[Node.js](https://nodejs.org/) v18+** installed
2. **[Devin Desktop](https://devin.ai/)** (formerly Windsurf) — or another AI-enabled IDE
3. **Clone the Workshop repository**:
   ```powershell
   git clone https://github.com/improving/ai-sdd-openspec-workshop
   ```
4. **Install the OpenSpec CLI** globally:
   ```powershell
   npm install -g @fission-ai/openspec@latest
   ```
5. Open `initial-prompt.md` — the product requirements for the Bug Tracker app.

---

## Workshop Lab

---

## Part 1 — As a Class: Setup OpenSpec and create Bug Feature

Follow along with the instructor for this section.

### Step 1 — Initialize OpenSpec

In a PowerShell terminal at the repo root, run:

```powershell
openspec init
```

This scaffolds the `openspec/` directory structure and skills used by all subsequent commands.

> **Note:** OpenSpec's `.devin/workflows/` commands have been deprecated in favor of skill-based slash commands. The legacy `/opsx-*` workflow commands (e.g. `/opsx-propose`, `/opsx-apply`, `/opsx-archive`) no longer work in the Devin chat panel. Use the skill-based commands documented below instead: `/openspec-propose`, `/openspec-apply-change`, `/openspec-archive-change`, etc.

### Step 1.5 - Configure config.yaml

Open the `openspec/config.yaml` file and replace its contents with the following:

```yaml
# openspec/config.yaml
schema: spec-driven

context: |
  Domain: Bug Tracker web application — a demo POC for a workshop teaching Spec-Driven Development (SDD) using OpenSpec.

  Tech stack:
  - Frontend: React + TypeScript (Vite) + Tailwind CSS
  - Backend: Node.js + Express + TypeScript
  - Storage: in-memory only (no database)
  - Tests: Vitest + Supertest for API tests
  - Dev runtime: frontend and backend run together via a single `npm run dev` command

  TDD discipline (non-negotiable):
  - Follow Red–Green–Refactor strictly.
  - For every behavior in the specs, write failing tests FIRST, then implement.

  Project conventions:
  - UI: one create form and one list view, minimal Tailwind styling, no extra dependencies.
  - Tests: backend endpoint tests with Supertest and frontend component tests with React Testing Library; run with `npm run test`.
  - We value backwards compatibility for all public APIs.

  Task conventions:
  - Group tasks under `## N. Group Name` headings.
  - Every task must be a checkbox in the form `- [ ] N.M Task description`.
  - Each task must be small, focused, reference the relevant spec scenario, and sequence: tests → implementation → refactor.
  - Check off tasks as you complete them one-by-one or a section at a time.

rules:
  proposal:
    - Include rollback plan
    - Identify affected teams
    - If you are running on model SWE 1.7, do not add `npm run dev` to the task list
  specs:
    - Use Given/When/Then format
    - Reference existing patterns before inventing new ones

operations:
  apply:
    guidance:
      - Run focused tests before the full suite
      - Do not run `npm run dev` during the apply phase
      - Prefer small, focused diffs; keep each implementation change under ~30 lines when possible

```

### Why these model-specific guidance rules matter

These guidance rules are specifically tuned for the SWE 1.7 model, which is significantly cheaper than other models. The goal is to add precision and guardrails so the cheaper model stays reliable in this lab:

- **No `npm run dev` in proposals and no `npm run dev` during apply** — prevents the Devin Desktop window from hanging.
- **Small, focused diffs (~30 lines max per change)** — keeps each apply step minimal, reducing the amount of code and reasoning the model must handle at once.
- **Concrete tasks, no multi-file refactors** — avoids the broad, sweeping rewrites that consume large context windows and can trigger rework.
- **Verify before archiving** — ensures a single clean completion step rather than repeated back-and-forth corrections.

### Step 2 — Propose the "Create Bug" Feature

**Open a new Devin Cascade Session** to start with a fresh context window.

In the Devin chat panel, type the following slash command:

```
/openspec-propose @initial-prompt.md plan and implement only the `create-bug` feature, and include all greenfield scaffolding required to run and verify it end-to-end. Greenfield scaffolding includes the React/Vite/Tailwind frontend, Express/TypeScript backend, in-memory storage, API tests, frontend tests, Vite development proxy and package/tooling configuration, plus the root `LAB-README.md`. Do not ask for clarification about this scope, and do not include `list-bugs` or `triage-bug` behavior in this change.
```

Devin will generate the following artifacts inside `openspec/changes/create-bug/`:

| File | Purpose |
|---|---|
| `proposal.md` | High-level change summary and goals |
| `design.md` | Technical design decisions |
| `spec.md` | Given/When/Then acceptance criteria |
| `tasks.md` | Ordered, TDD-sequenced task list |

### Step 3 — Review the Artifacts

Open and read each generated file. Discuss with the class:

- Does the spec match the requirements in `initial-prompt.md`?
- Are the acceptance criteria clear and testable?
- Does the task list follow Red–Green–Refactor order?

Request any changes from Devin before moving on.

### Step 4 — Apply the Change

**Open a new Devin Cascade Session** to start with a fresh context window.

Once satisfied with the artifacts, run in Cascade:

```
/openspec-apply-change create-bug
```

Devin will implement the feature — writing failing tests first, then making them pass, following the task list in `tasks.md`.

### Step 5 — Verify and Demo

1. Install dependencies and start the dev servers:
   ```powershell
   npm install
   npm run dev
   ```
2. Open the app in your browser and demo the Create Bug feature.
3. Run the test suite to confirm all tests pass:
   ```powershell
   npm test
   ```
4. Discuss with the class: What did Devin do well? What would you change?

### Step 6 — Archive the Change

**Open a new Devin Cascade Session** to start with a fresh context window.

When the feature is complete and verified, archive it in Cascade:

```
/openspec-archive-change create-bug
```

This moves the artifacts to `openspec/changes/archive/` to keep the workspace clean.

---

## Part 2 — In Groups: List Bugs & Triage Bug Features

Split into small groups (2–3 people). Each group will complete the remaining features independently, following the same propose → review → apply → demo → archive cycle.

### Feature A — List Bugs

**Step 1 — Propose**

**Open a new Devin Cascade Session** to start with a fresh context window.

```
/openspec-propose @initial-prompt.md list-bugs feature only
```

**Step 2 — Review** the generated artifacts in `openspec/changes/list-bugs/`. Verify the spec covers:
- Bugs displayed sorted newest-first.
- Title truncated to 50 chars with `…`.
- Severity shown as "Untriaged" when not set.

**Step 3 — Apply**

**Open a new Devin Cascade Session** to start with a fresh context window.

```
/openspec-apply-change list-bugs
```

**Step 4 — Verify and Demo**

```powershell
npm test
npm run dev
```

Open the browser and confirm the bug list renders correctly.

**Step 5 — Archive**

**Open a new Devin Cascade Session** to start with a fresh context window.

```
/openspec-archive-change list-bugs
```

---

### Feature B — Triage Bug

**Step 1 — Propose**

**Open a new Devin Cascade Session** to start with a fresh context window.

```
/openspec-propose @initial-prompt.md triage-bug feature only
```

**Step 2 — Review** the generated artifacts in `openspec/changes/triage-bug/`. Verify the spec covers:
- Triage sets Severity (P1/P2/P3) and transitions Status from `New` → `Triaged`.
- Once `Triaged`, Severity cannot be changed (error returned).

**Step 3 — Apply**

**Open a new Devin Cascade Session** to start with a fresh context window.

```
/openspec-apply-change triage-bug
```

**Step 4 — Verify and Demo**

```powershell
npm test
npm run dev
```

Open the browser and demonstrate the triage workflow end-to-end.

**Step 5 — Archive**

**Open a new Devin Desktop Session** to start with a fresh context window.

```
/openspec-archive-change triage-bug
```

---

## Key Concepts to Reflect On

After completing the lab, discuss these questions with your group or the class:

- Vibe Coding is powerful but important context is lost in chat conversations.
- How did the OpenSpec workflow feel different from traditional coding? From Vibe Coding?
- How did having a **spec before implementation** change the way code was written?
- Where do you see OpenSpec fitting into your real-world workflow?

---

## OpenSpec Slash Commands

OpenSpec commands are now distributed as **Devin skills** (located in `.devin/skills/`). The legacy `.devin/workflows/` commands (`/opsx-*`) have been deprecated and no longer work in the Devin chat panel. Use the skill-based slash commands below instead.

### Core Commands
| Command | Purpose |
|---|---|
| `/openspec-explore` | Think through ideas before committing to a change |
| `/openspec-propose` | Create a change and generate planning artifacts in one step |
| `/openspec-apply-change` | Implement tasks from the change |
| `/openspec-archive-change` | Archive a completed change |

### Expanded Workflow Commands
| Command | Purpose |
|---|---|
| `/openspec-verify-change` | Validate implementation matches artifacts |
| `/openspec-sync-specs` | Merge delta specs into main specs |

---

## Best Practice: Fresh Devin Desktop Sessions for Each Agent Command

It is recommended to **open a new Devin Desktop Session before running each agent command** (`/openspec-propose`, `/openspec-apply-change`, `/openspec-archive-change`, etc.). Here's why:

- **Context Window Management**: Each Devin Desktop session starts with a clean context window, preventing token accumulation from previous conversations that could limit the AI's ability to reason about the current task.
- **Reduced Hallucination**: A fresh context reduces the risk of the AI referencing or conflating details from prior features or changes.
- **Clearer Focus**: Each session is dedicated to a single feature or change, making it easier to track what the AI is working on and verify correctness.
- **Better Artifact Quality**: With a focused context, the generated specs, designs, and task lists are more precise and less likely to contain cross-feature contamination.

This practice is especially important in a workshop setting where multiple features are being developed in sequence.

---

## Tests-First vs. Tests-Second in Agentic SDD

A common objection to TDD in agentic development: *"The agent writes both the tests and the code, so why not let it write the code first and the tests second? It uses fewer tokens."*

**Tests-Second (the pushback)**
- Slightly lower token cost on the happy path.
- Tests are written with the implementation in view — they describe what the code *does*, not what the spec *demanded*.
- The agent has no objective oracle during implementation, so drift from the spec is harder to detect.
- One round of rework wipes out any token savings.

**Tests-First (recommended)**
- The first artifact produced is a machine-checkable encoding of the spec — intent drift is caught in seconds.
- Gives the agent a tight feedback loop: write → run → observe → fix, terminating cleanly when tests go green.
- Slightly higher best-case token cost, dramatically lower worst-case cost.
- Optimizes for **enforceable intent**, not generation efficiency.

**Key Takeaway**

> *Tests-second optimizes for tokens. Tests-first optimizes for intent. Pick which one you want to be wrong about in production. The agent will happily write tests that pass — only tests written before the code can prove the code did what the spec asked.*
