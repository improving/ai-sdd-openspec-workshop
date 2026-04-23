# Lab Instructions

## Prerequisites

Before the lab begins, make sure you have the following ready:

1. **Clone the workshop repository** to your local machine.
   - https://github.com/improving/ai-sdd-openspec-workshop
2. **Open the repo** in Windsurf (or your AI-enabled IDE).
3. **Install the OpenSpec CLI** globally if you have not already:
   ```powershell
   npm install -g openspec
   ```
4. Familiarize yourself with the prompt in the repo root:
   - `initial-prompt.md` — the product requirements for a simple Bug Tracker app.

---

## Part 1 — As a Class: Setup OpenSpec and create Bug Feature

Follow along with the instructor for this section.

### Step 1 — Initialize OpenSpec

In a PowerShell terminal at the repo root, run:

```powershell
openspec init
```

This scaffolds the `openspec/` directory structure and skills/workflows used by all subsequent commands.

### Step 2 — Propose the "Create Bug" Feature

In the Cascade chat panel, type the following slash command:

```
/opsx-propose @initial-prompt.md create-bug feature only
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

```
/opsx-propose @initial-prompt.md list-bugs feature only
```

**Step 2 — Review** the generated artifacts in `openspec/changes/list-bugs/`. Verify the spec covers:
- Bugs displayed sorted newest-first.
- Title truncated to 50 chars with `…`.
- Severity shown as "Untriaged" when not set.

**Step 3 — Apply**

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

```
/opsx-archive list-bugs
```

---

### Feature B — Triage Bug

**Step 1 — Propose**

```
/opsx-propose @initial-prompt.md triage-bug feature only
```

**Step 2 — Review** the generated artifacts in `openspec/changes/triage-bug/`. Verify the spec covers:
- Triage sets Severity (P1/P2/P3) and transitions Status from `New` → `Triaged`.
- Once `Triaged`, Severity cannot be changed (error returned).

**Step 3 — Apply**

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

```
/opsx-archive triage-bug
```

---

## Key Concepts to Reflect On

After completing the lab, discuss these questions with your group or the class:

- How did having a **spec before implementation** change the way code was written?
- Would you have caught the same edge cases without the Given/When/Then format?
- Where do you see OpenSpec fitting into your real-world workflow?
- What are the **limits** of AI-driven spec-to-code generation?