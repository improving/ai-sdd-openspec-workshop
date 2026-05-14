# AI Spec-Driven Development Workshop

A hands-on workshop demonstrating **Spec-Driven Development (SDD)** using [OpenSpec](https://github.com/Fission-AI/OpenSpec) and an AI-enabled IDE (Windsurf). Participants build a Bug Tracker app feature-by-feature using a propose → review → apply → verify → archive cycle.

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
2. **[Windsurf](https://windsurf.com/)** (or another AI-enabled IDE)
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

This scaffolds the `openspec/` directory structure and skills/workflows used by all subsequent commands.

### Step 1.5 - Configure config.yaml

Open the `openspec/config.yaml` file and update the `context` section to include the following:

```yaml
context: |
  Domain: Bug Tracker web application — a demo POC for a workshop teaching Spec-Driven Development (SDD) using OpenSpec.

  Tech stack:
  - Frontend: React + TypeScript (Vite) + Tailwind CSS — clean, modern, professional design
  - Backend: Node.js + Express + TypeScript
  - Storage: in-memory only (no database)
  - Tests: Vitest (and Supertest for API tests)
  - Dev runtime: frontend and backend run together via a single `npm run dev` command

  TDD discipline (non-negotiable):
  - Follow Red–Green–Refactor strictly.
  - For every behavior in the specs, write failing tests FIRST, then implement.
  - Task lists must sequence: tests → implementation → refactor.
```

### Step 2 — Propose the "Create Bug" Feature

**Open a new Windsurf Cascade Session** to start with a fresh context window.

In the Cascade chat panel, type the following slash command:

```
/opsx-propose @initial-prompt.md create-bug feature only, include greenfield scaffolding
```

Cascade will generate the following artifacts inside `openspec/changes/create-bug/`:

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

Request any changes from Cascade before moving on.

### Step 4 — Apply the Change

**Open a new Windsurf Cascade Session** to start with a fresh context window.

Once satisfied with the artifacts, run in Cascade:

```
/opsx-apply create-bug
```

Cascade will implement the feature — writing failing tests first, then making them pass, following the task list in `tasks.md`.

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
4. Discuss with the class: What did Cascade do well? What would you change?

### Step 6 — Archive the Change

**Open a new Windsurf Cascade Session** to start with a fresh context window.

When the feature is complete and verified, archive it in Cascade:

```
/opsx-archive create-bug
```

This moves the artifacts to `openspec/changes/archive/` to keep the workspace clean.

---

## Part 2 — In Groups: List Bugs & Triage Bug Features

Split into small groups (2–3 people). Each group will complete the remaining features independently, following the same propose → review → apply → demo → archive cycle.

### Feature A — List Bugs

**Step 1 — Propose**

**Open a new Windsurf Cascade Session** to start with a fresh context window.

```
/opsx-propose @initial-prompt.md list-bugs feature only
```

**Step 2 — Review** the generated artifacts in `openspec/changes/list-bugs/`. Verify the spec covers:
- Bugs displayed sorted newest-first.
- Title truncated to 50 chars with `…`.
- Severity shown as "Untriaged" when not set.

**Step 3 — Apply**

**Open a new Windsurf Cascade Session** to start with a fresh context window.

```
/opsx-apply list-bugs
```

**Step 4 — Verify and Demo**

```powershell
npm test
npm run dev
```

Open the browser and confirm the bug list renders correctly.

**Step 5 — Archive**

**Open a new Windsurf Cascade Session** to start with a fresh context window.

```
/opsx-archive list-bugs
```

---

### Feature B — Triage Bug

**Step 1 — Propose**

**Open a new Windsurf Cascade Session** to start with a fresh context window.

```
/opsx-propose @initial-prompt.md triage-bug feature only
```

**Step 2 — Review** the generated artifacts in `openspec/changes/triage-bug/`. Verify the spec covers:
- Triage sets Severity (P1/P2/P3) and transitions Status from `New` → `Triaged`.
- Once `Triaged`, Severity cannot be changed (error returned).

**Step 3 — Apply**

**Open a new Windsurf Cascade Session** to start with a fresh context window.

```
/opsx-apply triage-bug
```

**Step 4 — Verify and Demo**

```powershell
npm test
npm run dev
```

Open the browser and demonstrate the triage workflow end-to-end.

**Step 5 — Archive**

**Open a new Windsurf Cascade Session** to start with a fresh context window.

```
/opsx-archive triage-bug
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

### Core Commands
| Command | Purpose |
|---|---|
| `/opsx:explore` | Think through ideas before committing to a change |
| `/opsx:propose` | Create a change and generate planning artifacts in one step |
| `/opsx:apply` | Implement tasks from the change |
| `/opsx:archive` | Archive a completed change |

### Expanded Workflow Commands (custom workflow selection)
| Command | Purpose |
|---|---|
| `/opsx:new` | Start a new change scaffold |
| `/opsx:continue` | Create the next artifact based on dependencies |
| `/opsx:ff` | Fast-forward: create all planning artifacts at once |
| `/opsx:verify` | Validate implementation matches artifacts |
| `/opsx:sync` | Merge delta specs into main specs |
| `/opsx:bulk-archive` | Archive multiple changes at once |
| `/opsx:onboard` | Guided tutorial through the complete workflow |

---

## Best Practice: Fresh Cascade Sessions for Each Agent Command

It is recommended to **open a new Windsurf Cascade Session before running each agent command** (`/opsx-propose`, `/opsx-apply`, `/opsx-archive`, etc.). Here's why:

- **Context Window Management**: Each Cascade session starts with a clean context window, preventing token accumulation from previous conversations that could limit the AI's ability to reason about the current task.
- **Reduced Hallucination**: A fresh context reduces the risk of the AI referencing or conflating details from prior features or changes.
- **Clearer Focus**: Each session is dedicated to a single feature or change, making it easier to track what the AI is working on and verify correctness.
- **Better Artifact Quality**: With a focused context, the generated specs, designs, and task lists are more precise and less likely to contain cross-feature contamination.

This practice is especially important in a workshop setting where multiple features are being developed in sequence.
