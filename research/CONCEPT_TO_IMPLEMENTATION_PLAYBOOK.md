# Concept → Implementation Playbook

**Replicating the Schedul-R Orchestration Process on a New SaaS Initiative
Using the `cursor_orchestrator` Framework**

- **Source project**: Schedul-R (`c:\Users\Heath\dev\Scheduling`)
- **Target framework**: [`heathbobby/cursor_orchestrator`](https://github.com/heathbobby/cursor_orchestrator)
- **Audience**: A Master Orchestrator AI agent (and the human operator behind it) bootstrapping a brand-new SaaS offering from a small set of seed documents
- **Goal**: Reproduce the same "concept → backlog-refined → implementation-ready" pipeline that took 21 unstructured `.docx` seed files and produced 109 audited user stories, 4 MVPs of complete technical documentation, and a 73-page execution handoff — autonomously and reproducibly

---

## 0. How to Use This Document

This playbook is **prescriptive** — it is meant to be read and applied verbatim, with substitutions only where explicitly marked `{like_this}`. It is also **layered**: read the executive summary, then read each layer top-to-bottom. The "Adaptation Playbook" (§12) is the operational checklist; everything before it is the *why* you need to make it work.

When using it inside Cursor on the target repo:

1. Drop this file into the new repo (e.g. `documentation/handoffs/CONCEPT_TO_IMPLEMENTATION_PLAYBOOK.md`).
2. Bootstrap `cursor_orchestrator` per §11.
3. Open Cursor and attach this file plus the four files in §4.5 to a new chat.
4. Issue: **"You are the Master Orchestrator. Read the playbook and execute it for this project."**

---

## 1. Executive Summary: What Schedul-R Actually Did

### 1.1 What went in (the "seed")

Twenty-one Microsoft Word documents in `raw/` representing the unstructured concept of a scheduling SaaS product — repeated, conflicting versions of:

- Business Plan, Pitch Deck, Go-To-Market Strategy
- Product Requirements Document (PRD) v1, v2
- Functional Requirements v2
- Feature Requirements
- Technical Architecture Design v1, v2
- Technical Specifications v1.0 → v2.10 (~24 versions)
- Implementation Plan v2.0 → v2.8 (9 versions)
- Project Development Plan v1, v2

These were *never edited again*. They are immutable inputs (enforced by `.cursorignore`).

### 1.2 What came out (the "deliverable")

A canonical, internally consistent, implementation-ready documentation tree:

| Layer | Artifact | Volume |
|---|---|---|
| Canonical specs | `documentation/requirements/`, `architecture/`, `standards/`, `planning/` | ~30 docs |
| Backlog | `documentation/work_items/E01..E21/` with epic indexes, deliverables, and 109 user stories | 109 stories, 4 MVPs |
| Per-MVP technical docs | `documentation/MVP{1..4}/{Domain}/` — Overview, Infrastructure, BusinessEntities, DataModel, Integrations, TestingStrategy, AcceptanceCriteria, OperationalRunbook + per-feature `Features/{Feature}/Overview.md` and `Workflows/*.md` | ~600 files, ~6 MB markdown |
| Implementation handoff | `documentation/implementation/` — Roadmap, Team Assignments, Operational Readiness, Integration Testing Plan, Risk Mitigation | 5 docs, 73 pages |
| Reusable framework | `documentation/orchestration-framework/` — extracted, generic version of the orchestration system itself | Now the `cursor_orchestrator` repo |

### 1.3 What did the work

A **Master Orchestrator AI agent**, governed by ~10 cursor rules and ~50 process documents, executing **6 standard iterations per MVP** through a tightly-defined **template → generate → launch → monitor → validate → feedback** loop. The agent itself never wrote documentation — it orchestrated specialized sub-agents (Architect, Tech Lead, Data Architect, API Architect, Integration Architect, Product Owner, QA Lead, Test Engineer, Tech Writer, SRE) running concurrently via `cursor-agent` CLI.

### 1.4 Why it worked (the four invariants you must preserve)

1. **The orchestrator never produces deliverables.** It only delegates. Every time a human or agent broke this rule, quality collapsed and the system stopped scaling.
2. **Every iteration has the same skeleton.** `CONTEXT.md`, `COMPLETION_CRITERIA.md`, `README.md`, generated agent prompts, an `outputs/` directory. This skeleton is what made automated tooling possible.
3. **Tools, not loops.** Anything that looked like `sleep N && check` was wrong. Wait, validation, signaling, and feedback collection are *deterministic Bash/Python*, not agent inference.
4. **Feedback closes the loop or it doesn't exist.** Every iteration produces a `feedback.json`. Patterns trigger updates to *templates*, not just retries. Iteration N+1 is measurably better than N.

---

## 2. The Mental Model: Four Layers of the Project

Replicate this layout on your target project (names can differ, structure cannot):

```
{project-root}/
├── raw/                       # Layer 0: SEEDS (immutable, ignored by Cursor)
│   └── *.docx, *.pdf, *.md    # Whatever the founder/PM wrote informally
│
├── documentation/             # Layer 1: CANONICAL TRUTH (single source of truth)
│   ├── extracts/              # Auto-extracted text from raw/ (Markdown of every docx)
│   ├── requirements/          # PRODUCT_REQUIREMENTS.md, FUNCTIONAL_REQUIREMENTS.md
│   ├── architecture/          # ARCHITECTURE.md, TECHNICAL_SPECIFICATIONS.md, DECISIONS.md
│   ├── planning/              # DELIVERY_BACKLOG.md, EXECUTION_ORCHESTRATION.md, CONCURRENCY_ANALYSIS.md
│   ├── standards/             # ENGINEERING_STANDARDS.md, AI_AGENT_STANDARDS.md, *_STANDARDS.md
│   ├── observability/         # OBSERVABILITY_STANDARDS.md, TELEMETRY_CONFORMANCE.md
│   ├── runbooks/              # Operational runbook templates
│   ├── tools/                 # Doc tooling (extract_docs.py, raw_inventory.py, etc.)
│   ├── work_items/            # Layer 2 (see below)
│   ├── MVP1/ MVP2/ MVP3/ MVP4/  # Layer 3 (see below)
│   ├── implementation/        # Final handoff docs (Layer 4)
│   └── refinement/            # Layer 5 (the orchestration machine itself)
│
├── work_items/  (or documentation/work_items/)   # Layer 2: BACKLOG
│   ├── INDEX.md               # Epic index
│   ├── E01/ ... E21/          # One folder per epic
│   │   ├── INDEX.md
│   │   ├── DELIVERABLES.md    # What "epic done" means
│   │   ├── US-E01-010.md      # User stories with full refinement record
│   │   └── tasks/             # T-US-E01-010-01 task breakdowns
│
├── documentation/MVP{N}/      # Layer 3: PROGRESSIVE TECHNICAL SPECS
│   └── {Domain}/              # Each domain (e.g. Platform, Scheduling, StaffUI)
│       ├── Overview.md
│       ├── Infrastructure.md
│       ├── BusinessEntities.md
│       ├── DataModel.md
│       ├── Integrations.md
│       ├── TestingStrategy.md
│       ├── AcceptanceCriteria.md
│       ├── OperationalRunbook.md
│       └── Features/{Feature}/
│           ├── Overview.md
│           └── Workflows/{Workflow}.md
│
└── documentation/refinement/  # Layer 5: THE ORCHESTRATION MACHINE
    ├── MASTER_ORCHESTRATOR_INIT.md      # Boot prompt for the orchestrator
    ├── ORCHESTRATION_PLAYBOOK.md        # Detailed workflow
    ├── SCALABLE_ORCHESTRATION_PHILOSOPHY.md
    ├── APPLYING_LEARNINGS_PLAYBOOK.md   # Pattern → action matrix
    ├── COMPLETION_SIGNALS_SYSTEM.md
    ├── PARALLEL_ITERATION_PATTERN.md
    ├── agent-roles/                     # Role definitions (boot prompts)
    ├── templates/
    │   ├── prompts/{role}-agent.md.j2   # Jinja2 prompt templates
    │   └── roles/{role}-role-definition.md
    ├── prompt-library/{version}/        # Versioned, scored historical prompts
    ├── feedback/{iteration}-feedback.json
    ├── iterations/{iteration-name}/     # One folder per iteration
    ├── generate_prompts.py              # Template → prompt
    ├── orchestrate.sh                   # Launch only
    ├── orchestrate_full.sh              # Launch → monitor → validate → report
    ├── orchestrate_session.sh           # Resumable single-agent sessions
    ├── monitor_enhanced.sh              # Intelligent waiting (--wait)
    ├── validate_iteration.sh            # Deterministic validation
    └── collect_feedback.sh              # Feedback JSON generation
```

**Why these four layers matter to the orchestrator:**

- **Seeds** are the founder's intent. The orchestrator may *read* them but never *cite* them as requirements; it cites canonical docs.
- **Canonical truth** is the contract. Everyone (humans, agents, CI/CD) treats it as the source of truth.
- **Backlog** is what you implement. Every story traces to canonical requirements.
- **Progressive technical specs** are the bridge: an engineer reading `MVP1/Scheduling/Integrations.md` knows exactly what API to build.

---

## 3. The Six-Iteration Standard for Each MVP

This is the single most important pattern in the project. Every MVP — `MVP1` through `MVP4` — follows the *exact same six iterations*, and the orchestrator's job is to execute them in order without inventing variations.

| # | Iteration name suffix | Deliverables (per domain) | Typical agents | Typical duration |
|---|---|---|---|---|
| 1 | `-iteration-01-domain-infrastructure` | `Infrastructure.md` | Architect | 10–15 min |
| 2 | `-iteration-02-entities-models` | `BusinessEntities.md` + `DataModel.md` | Tech Lead + Data Architect | 6–8 min |
| 3 | `-iteration-03-integrations` | `Integrations.md` (REST APIs + Events) | API Architect + Integration Architect | 6 min |
| 4 | `-iteration-04-feature-specifications` | `Features/{Feature}/Overview.md` + `Features/{Feature}/Workflows/*.md` | Product Owner + Tech Writer | 45–60 min |
| 5 | `-iteration-05-quality-testing` | `TestingStrategy.md` + `AcceptanceCriteria.md` | QA Lead + Test Engineer | 15–20 min |
| 6 | `-iteration-06-release-operations` | `OperationalRunbook.md`, `ReleaseNotes.md`, `DeploymentGuide.md`, etc. | SRE + Tech Writer | 15–20 min |

### Why this exact order

- Iteration 1 produces the *infrastructure shape* — every later iteration references compute/storage/messaging assumptions.
- Iteration 2 cannot run before 1 (entities need to know what database they live in).
- Iteration 3 cannot run before 2 (APIs need entities to expose).
- Iteration 4 (features/workflows) needs entities + APIs to reference.
- Iteration 5 (testing) needs features to write tests against.
- Iteration 6 (operations) needs everything to write runbooks against.

### Adapting to your project

If your domain has different artifacts, **change the deliverable names but keep the six-iteration sequence**. Example for an analytics SaaS:

1. Domain Infrastructure (data warehouse, ETL platform)
2. Entities + Models (fact/dim schema, semantic layer)
3. Integrations (ingestion connectors, embedding API)
4. Feature Specs (dashboards, query builders)
5. Quality (data quality strategy, acceptance metrics)
6. Release & Operations (deployment, observability runbooks)

---

## 4. The Master Orchestrator Agent

### 4.1 What the orchestrator IS

A persistent role embodied by an AI agent in the Cursor IDE. It thinks like **a project manager + a system architect** combined and behaves as a *dispatcher*, never as a *worker*.

### 4.2 What the orchestrator does NOT do (absolute prohibitions)

These are reproduced from `documentation/refinement/MASTER_ORCHESTRATOR_INIT.md` because they are the difference between a working system and a broken one:

- ❌ **NEVER write deliverable files itself.** No `Infrastructure.md`, no `DataModel.md`, no work item — ever. The agents do that.
- ❌ **NEVER hand-write agent prompts.** Use `generate_prompts.py`. Always.
- ❌ **NEVER use manual sleep/poll loops.** Use `monitor_enhanced.sh --wait`.
- ❌ **NEVER manually `ls`/`find` to check if files exist.** Use `validate_iteration.sh`.
- ❌ **NEVER write completion reports manually.** Use `collect_feedback.sh`.
- ❌ **NEVER "take a pragmatic shortcut" by doing it yourself "just this once".** That is exactly what destroyed prior attempts.
- ❌ **NEVER wait idle while sub-agents run.** That 10–20 minutes is for *planning iteration N+1*.

When the orchestrator catches itself doing any of the above, the rule is: **STOP IMMEDIATELY. You are doing it wrong.**

### 4.3 What the orchestrator MUST do

1. **Assess current state** by reading the canonical docs and the latest iteration completion reports — do not ask the user "where are we?"
2. **Identify the next priority** by walking the priority hierarchy: finish current MVP → start next MVP → enhance complete MVPs.
3. **Plan the next iteration** by creating its directory and writing `CONTEXT.md`, `COMPLETION_CRITERIA.md`, `README.md`.
4. **Generate prompts** with `generate_prompts.py --force` (always `--force` — it skips HIGH-RISK confirmations that would block automation).
5. **Launch with `orchestrate_full.sh`**, which itself runs launch → monitor → validate → report.
6. **Plan iteration N+1 in parallel** (mandatory, not optional — see §8).
7. **Collect feedback** with `collect_feedback.sh` and **apply learnings** by updating templates (see §9).
8. **Commit changes** with conventional commits, never to `main` directly.

### 4.4 The orchestrator's "first action" protocol

When initialized, the orchestrator MUST first answer three questions to the user, in writing, before doing anything:

1. *What MVPs/phases exist and their completion status?* (read iteration completion reports, not user input)
2. *What is the next highest-priority work item?* (specific iteration name)
3. *What is the exact plan to execute it?* (specific shell commands)

Only after the user (or auto-approval rule) confirms does the orchestrator proceed.

### 4.5 Files the orchestrator needs attached to its initial chat

When you start the Master Orchestrator chat in the new project, attach exactly these four files:

1. `@documentation/refinement/MASTER_ORCHESTRATOR_INIT.md` — the boot prompt
2. `@documentation/refinement/agent-roles/MASTER_ORCHESTRATOR.md` — the role definition
3. `@documentation/refinement/ORCHESTRATION_PLAYBOOK.md` — the detailed workflow
4. `@documentation/refinement/SCALABLE_ORCHESTRATION_PHILOSOPHY.md` — the "agents only where agentic decisions are needed" doctrine

Then send: **"Begin orchestration."**

That single message is enough. The agent figures out everything else.

---

## 5. The Specialized Agent Role Library

The orchestrator delegates to specialized sub-agents. Each role has a *perspective*, *core values*, a *thinking framework*, an *initialization prompt*, and a *Jinja2 prompt template*. Reproduce these on the new project — adjusting expertise areas to match your domain — but keep the structure.

### 5.1 The eleven roles Schedul-R used

Documented in `documentation/refinement/AGENT_ROLE_DEFINITIONS.md` and `documentation/refinement/templates/prompts/`:

| Role | Perspective | Primary deliverables | Optimal files / Complexity budget |
|---|---|---|---|
| `architect` | System architect + boundary designer | `Infrastructure.md` per domain | 5 files, complexity ≤ 14 |
| `tech-lead` | Senior engineer + standards enforcer | `BusinessEntities.md`, workflows | 15 files, ≤ 18 |
| `data-architect` | DB expert + data modeler | `DataModel.md` per domain | 6 files, ≤ 15 |
| `api-architect` | REST/OpenAPI specialist | `Integrations.md` (HTTP) | 4 files, ≤ 14 |
| `integration-architect` | Event schema + integration patterns | `Integrations.md` (events/CloudEvents) | 4 files, ≤ 14 |
| `product-owner` | Product manager + user advocate | `Features/{F}/Overview.md`, requirements traceability | 12 files, ≤ 16 |
| `qa-lead` | Testing strategy + quality gates | `TestingStrategy.md` per domain | 8 files, ≤ 15 |
| `test-engineer` | Acceptance criteria + test matrices | `AcceptanceCriteria.md` per domain | 6 files, ≤ 15 |
| `tech-writer` | User docs + release notes | `Features/{F}/Workflows/*.md`, release docs | 5–8 files, ≤ 12 |
| `sre` | Operations + reliability | `OperationalRunbook.md`, runbooks | 3 files, ≤ 12 (HIGHEST single-file complexity) |
| `dependency-analyst`, `concurrency-analyst` | Sequencing + parallelization | Update `EXECUTION_ORCHESTRATION.md`, `CONCURRENCY_ANALYSIS.md` | Used during refinement-only phases |

These map cleanly onto the `cursor_orchestrator` AGENT_ROLE_LIBRARY (which is a generic superset).

### 5.2 Anatomy of a role (copy this pattern for any new role)

Every role definition has six sections:

1. **Role Perspective** — How this agent thinks (e.g. "thinks like a senior engineer + standards enforcer")
2. **Core Values** — The 5 values it must prioritize (e.g. correctness, maintainability, observability)
3. **Thinking Framework** — The five questions it asks of every work item (e.g. "Can we build this? Does this meet standards?")
4. **Responsibilities** — Mapped to refinement phases or iteration types
5. **Initialization Prompt** — The literal text to paste/render into the agent's first message
6. **Canonical Documents** — The exact `@`-references the agent must load

The matching `templates/prompts/{role}-agent.md.j2` file then *renders* this for a specific iteration with file lists, complexity scores, token budgets, and "EXECUTE NOW" framing.

### 5.3 The token-budget complexity model (copy verbatim)

`generate_prompts.py` ships with this complexity table. **Tune the numbers for your domain, but keep the model**:

```python
FILE_COMPLEXITY = {
  "Overview.md": 1, "Infrastructure.md": 3, "BusinessEntities.md": 2,
  "DataModel.md": 3, "Integrations.md": 4, "Workflow.md": 2,
  "TestingStrategy.md": 3, "AcceptanceCriteria.md": 3,
  "OperationalRunbook.md": 5,           # the most expensive single artifact
  "MonitoringAndAlerting.md": 4, "DisasterRecovery.md": 3,
  # ... one entry per artifact type your project produces
}

ROLE_CONFIGS = {
  "sre":            {"optimal_files": 3,  "max_files": 5,  "complexity_budget": 12},
  "tech-lead":      {"optimal_files": 15, "max_files": 25, "complexity_budget": 18},
  # ... one entry per role
}
```

Risk is computed automatically: `LOW` ≤ optimal, `MEDIUM` ≤ max, otherwise `HIGH`. The orchestrator must always pass `--force` to suppress the interactive prompt and proceed even on `HIGH`, but `HIGH` allocations almost always become partial completions, which the feedback loop catches and corrects.

---

## 6. Anatomy of an Iteration (the unit of work)

Every iteration directory looks like this:

```
documentation/refinement/iterations/{mvp{N}-iteration-{NN}-{name}}/
├── CONTEXT.md                       # 15,000–20,000 words of shared context
├── COMPLETION_CRITERIA.md           # File-by-file checkboxes with size minimums
├── README.md                        # How to execute this iteration
├── {role1}-agent-prompt.md          # Generated, 6,000–8,000 words
├── {role2}-agent-prompt.md          # Generated, 6,000–8,000 words
├── orchestrate_iteration_{N}.sh     # (Legacy iterations) bespoke launcher
├── outputs/                         # Logs, agent_pids.txt, validation reports
└── ITERATION_{N}_COMPLETION_REPORT.md  # Generated post-validation
```

### 6.1 `CONTEXT.md` (the single most important file in the system)

Purpose: give every agent in this iteration the *same* background so they produce internally-consistent output without communicating.

Required structure:

1. **Iteration overview** — Goal, scope, deliverables, agents, expected duration
2. **MVP scope reminder** — Explicit "IN scope" vs "OUT of scope (future MVPs)" lists with epic IDs
3. **Architecture context** — System diagrams (Mermaid), component boundaries, tech stack
4. **Standards & references** — Naming, format templates, quality thresholds (with concrete examples)
5. **Domain-specific context** — One block per target domain (key entities, integration focus, special considerations)
6. **Cross-domain coordination** — Contracts between domains; what one agent's output must respect for another
7. **Quality standards** — Per artifact type, what makes "good"
8. **Agent roles & responsibilities** — Who is doing what in this iteration
9. **Success criteria** — Definition of done

**Hard rule**: 15,000+ words is normal and good. Comprehensive context is *cheaper* than fixing scope confusion in feedback loops.

### 6.2 `COMPLETION_CRITERIA.md` (the validation contract)

Mostly checklists, with grep-friendly patterns. The validator parses lines like:

```
- [ ] `documentation/MVP3/Platform/Integrations.md` (exists, >40KB)
```

This makes validation **deterministic Bash** (no agent inference). The size minimum is the most important field — it catches stub files where an agent declared TASK_COMPLETE but produced 200 bytes.

### 6.3 The role prompt (`{role}-agent-prompt.md`)

Generated, never hand-written. Each prompt:

1. Opens with **EXECUTE NOW** framing — "You are EXECUTING this task autonomously. DO NOT ask for permission or clarification."
2. Lists the exact files to create with complexity scores
3. Reminds the agent of role expertise + canonical role definition reference
4. Sets a **token budget management strategy** based on file count (sequential, signal-every-N)
5. Embeds the **artifact structure template** with concrete examples (this is critical — agents replicate examples)
6. Lists **success criteria** (size, sections, examples)
7. Defines **completion signals**: `✅ TASK_COMPLETE` or `⚠️ TOKEN_BUDGET_LOW`
8. Ends with a literal **"BEGIN NOW with file 1: `{first file}`"**

### 6.4 The `outputs/` folder

- `agent_pids.txt` — newline-delimited `PID:role` for monitoring
- `{role}.log` — agent stdout/stderr; may be empty (agents write directly to target files)
- `validation_report.txt` — generated by `validate_iteration.sh`
- The orchestrator never inspects logs by hand; it greps for `TASK_COMPLETE` / `TOKEN_BUDGET_LOW`

---

## 7. The Deterministic Toolchain

This is what made the system *scalable* and not just *clever*. Memorize these tools and never bypass them.

### 7.1 `generate_prompts.py` — Template → Prompt

```bash
python3 documentation/refinement/generate_prompts.py \
  --iteration "mvp3-iteration-02-entities-models" \
  --agent "tech-lead" \
  --files "Platform/BusinessEntities.md,Scheduling/BusinessEntities.md,..." \
  --task "Define business entities for all MVP3 domains" \
  --mvp 3 \
  --force \
  --output "documentation/refinement/iterations/mvp3-iteration-02-entities-models/tech-lead-agent-prompt.md"
```

Estimates tokens, scores complexity, validates against role budget, and renders the Jinja2 template. With `--force`, proceeds through HIGH-risk warnings (so the orchestrator is never blocked on input).

**Time savings: 30 minutes manual → 2 minutes (93%).**

### 7.2 `orchestrate_full.sh` — Full lifecycle

```bash
./documentation/refinement/orchestrate_full.sh \
  iterations/mvp3-iteration-02-entities-models
```

Internally runs:

1. `orchestrate.sh` (launch agents in background, capture PIDs)
2. `monitor_enhanced.sh --wait` (intelligent waiting on PIDs + file stability + signals)
3. `validate_iteration.sh` (deterministic file/size checks)
4. Generates pointer to validation + completion reports

### 7.3 `monitor_enhanced.sh --wait` — Intelligent waiting

Three completion-detection mechanisms in priority order:

1. **PID exit** (most reliable) — reads `outputs/agent_pids.txt`, polls each PID
2. **Completion signals** (preferred when no PID file) — greps logs for `✅ TASK_COMPLETE` / `⚠️ TOKEN_BUDGET_LOW`
3. **File stability** (fallback) — same file count + same total size for 3 consecutive 10-second checks

Default timeout: 1200s (20 min). Configurable: `--wait=600`. Returns exit code 0 (success/partial) or 1 (timeout).

**This replaced the catastrophe** documented in `SCALABLE_ORCHESTRATION_PHILOSOPHY.md`: the user spent a full session typing `sleep 30 && ls -lh ...` over and over, defeating the entire purpose of building tools.

### 7.4 `validate_iteration.sh` — Deterministic validation

Parses `COMPLETION_CRITERIA.md`, extracts `path/to/file.md > NKB` pairs, checks each:

- Exists?
- ≥ minimum size?

Writes `validation_report.txt`. Exit 0 if 100% pass, 0 if ≥90% (treat as success), 1 otherwise.

### 7.5 `collect_feedback.sh` — Feedback loop

Generates `documentation/refinement/feedback/{iteration-name}-feedback.json`:

```json
{
  "iteration": "mvp4-iteration-04-feature-specifications",
  "agents": [
    { "role": "tech-writer", "files_target": 79, "files_completed": 17,
      "completion_rate": 21, "issues": [{ "type": "partial_completion", ... }] }
  ],
  "overall_completion_rate": 30,
  "lessons": [ /* manual */ ],
  "prompt_adjustments_recommended": [ /* manual */ ]
}
```

This file is the **input** to step 8 of every iteration (apply learnings).

### 7.6 `orchestrate_session.sh` — Resumable single-agent sessions

Used for "recovery iterations" (e.g., `mvp4-iteration-03b-integrations-recovery`). Reuses the agent's chat session via `agent --resume {sessionId}`, drastically reducing tokens because CONTEXT.md doesn't have to be re-sent. Use when:

- A single agent needs to finish files left over by a token-budget-exhausted run
- The same agent will refine its own previous output

---

## 8. Concurrency: Both Within and Across Iterations

### 8.1 Within-iteration concurrency

A single iteration launches 2–N agents *in parallel*, each writing to disjoint output files. Schedul-R proved 2 agents reliably; 3+ should work but was untested. Within-iteration parallelism is safe when:

- ✅ Multiple **independent domains** (Platform, Scheduling, Availability, ...)
- ✅ **Separable concerns** (entities vs. schemas, REST APIs vs. events)
- ✅ **Repeatable structure** (same template across N targets)
- ✅ **High volume** (≥100KB output)

It is unsafe when:

- ❌ Sequential dependencies (Agent B needs Agent A's output)
- ❌ Mid-execution coordination needed (agents can't talk to each other in this model)
- ❌ Output < 10KB (faster sequential, less overhead)

### 8.2 Across-iteration concurrency (the parallel-preparation pattern)

This is the productivity multiplier nobody discovers on their own. The rule:

> **Never wait idle while agents execute. The 10–20 minutes of agent runtime is when you build iteration N+1.**

While iteration N agents run:

1. `mkdir` for iteration N+1
2. Draft N+1's `README.md`
3. Outline N+1's `CONTEXT.md` (using N's CONTEXT as a base)
4. Review previous feedback and bake learnings into N+1
5. Pre-generate N+1 prompts if structure is clear

Then when N completes → validate → commit → **immediately** launch N+1 (no setup delay).

**Measured impact**: 6 iterations in ~120 minutes vs. ~180 minutes serial — a 33% throughput gain.

When NOT to parallelize:

- First iteration of a brand-new MVP (you may discover unexpected domain structure that invalidates N+1 planning)
- N+1 truly depends on N's specific findings (unusual; check first)

Documented in `documentation/refinement/PARALLEL_ITERATION_PATTERN.md`.

---

## 9. The Continuous Improvement Loop

The reason MVP4 ran more smoothly than MVP1 was not luck — it was that every iteration ended with a *prescribed* feedback application step. The pipeline:

```
Run iteration N
       │
       ▼
Agent emits completion signal (✅ TASK_COMPLETE or ⚠️ TOKEN_BUDGET_LOW)
       │
       ▼
collect_feedback.sh → feedback/{iteration}-feedback.json
       │
       ▼
Master Orchestrator reviews JSON → applies pattern→action matrix (next subsection)
       │
       ▼
Updates one of: template, role definition, generate_prompts.py thresholds, MASTER_ORCHESTRATOR_INIT.md
       │
       ▼
Updates LESSONS_LEARNED.md
       │
       ▼
Commits change with conventional commit
       │
       ▼
Iteration N+1 starts with the lesson already baked in
```

### 9.1 The pattern → action matrix (memorize this)

| Pattern detected | Symptom in feedback.json | Action |
|---|---|---|
| **Token budget hit** | `completion_rate < 0.8`, gap between `files_target` / `files_created` | (a) Split files across more agents next time, OR (b) lower `complexity_budget` for that role in `generate_prompts.py`, OR (c) add explicit warning to that role's `.j2` template |
| **Scope confusion** | Files created outside intended MVP, wrong epic referenced | Enhance `CONTEXT.md`'s "MVP scope boundaries" table with explicit ✅/❌ matrix per feature |
| **Tool avoidance** | Manual file creation, ignored CLI tool, hand-rolled prompt | Make tool commands more explicit in template (literal copy-paste examples, anti-pattern callouts) |
| **Quality issues** | Missing sections, inconsistent format, files near minimum size | Add concrete format examples to template; raise minimum size in `COMPLETION_CRITERIA.md` |
| **Silent completion** | No `TASK_COMPLETE` or `TOKEN_BUDGET_LOW` in logs | Add completion protocol to template; remind via boot prompt |

### 9.2 Three update modes

- **Template update** (most powerful) — `vim documentation/refinement/templates/prompts/{role}-agent.md.j2` → propagates to all future iterations
- **One-time prompt adjustment** — pass different `--files` or `--notes` next time
- **Process update** — modify `MASTER_ORCHESTRATOR_INIT.md`, `ORCHESTRATION_PLAYBOOK.md`, or a role definition

The rule is: **if the same mistake appears twice, it MUST be promoted to a template change**. Otherwise the system has not learned.

### 9.3 The "close the loop" non-negotiable

`APPLYING_LEARNINGS_PLAYBOOK.md` is explicit: collecting feedback without applying it is *worse than not collecting it* because it creates the illusion of improvement. The orchestrator's iteration is not complete until:

- ✅ `feedback.json` exists
- ✅ The orchestrator has *named* the patterns and *committed* the template/role/process changes

---

## 10. Cursor Configuration That Makes It Work

### 10.1 `.cursorignore` — protect the seeds

```
raw/                    # NEVER let Cursor edit raw inputs
*.log
.env
node_modules/
dist/ build/
```

### 10.2 `.cursor/rules/*.mdc` — always-attached rules

Every chat in the repo automatically picks up these `.mdc` files. Replicate this set on the new project:

| File | Purpose |
|---|---|
| `project-context.mdc` | Names the project, lists key documentation locations |
| `automated-orchestration.mdc` | The full multi-agent orchestration playbook (3,800 lines in Schedul-R) |
| `backlog-refinement-workflow.mdc` | Describes the Master Orchestrator boot sequence |
| `file-organization.mdc` | Naming conventions: `E##`, `US-E##-###`, `T-US-E##-###-##`; never modify `raw/` |
| `git-workflow.mdc` | Conventional commits, feature branches, never to `main` |
| `standards-compliance.mdc` | Where engineering / event / API standards live |
| `context-loading.mdc` | Quality gates: a story is "Ready for Implementation" only when all gates pass |

### 10.3 The boot ritual

In Cursor:

1. Open the project root.
2. New chat.
3. Attach the four files from §4.5.
4. Send **"Begin orchestration."**

That's it. The rules auto-attach; the orchestrator reads itself in.

---

## 11. Mapping to `cursor_orchestrator` (the Generic Framework)

The Schedul-R team extracted everything above into a portable Python framework: `heathbobby/cursor_orchestrator`. It generalizes the same patterns. **Use it. Do not re-implement them by hand on the new project.**

### 11.1 What the generic framework gives you out-of-the-box

| Schedul-R artifact | Generic framework equivalent |
|---|---|
| `documentation/refinement/generate_prompts.py` | `orchestration-framework/tools/generate_prompts.py` |
| `documentation/refinement/orchestrate_full.sh` | `orchestration-framework/tools/orchestrate_full.sh` |
| `documentation/refinement/monitor_enhanced.sh` | `orchestration-framework/tools/monitor_enhanced.sh` |
| `documentation/refinement/validate_iteration.sh` | `orchestration-framework/tools/validate_iteration.sh` |
| `documentation/refinement/collect_feedback.sh` | `orchestration-framework/tools/collect_feedback.sh` |
| Per-iteration directories under `documentation/refinement/iterations/` | `.orchestration/runtime/iterations/{iteration}/` |
| `MASTER_ORCHESTRATOR_INIT.md` + `agent-roles/*.md` | `AGENT_ROLE_LIBRARY.md` + `templates/_base.md.j2` |
| `templates/prompts/*.j2` | `templates/{role}.md.j2` |
| Cursor rules (always-attached) | `.cursor/rules/` (enabled by `cursor.enabled: true` in `config.yaml`) |
| 6-iteration MVP cadence | YAML workflows under `.orchestration/config/workflows/` (e.g. `user-story-refinement.yaml`) |
| Slash-command shorthand (`/orchestrator::start_workflow(...)`) | First-class — see `templates/COMMAND_SHORTHAND.md` |
| Worktrees for concurrent agents | First-class via `worktrees:` block in `config.yaml` |

### 11.2 The generic framework's CLI surface

Where Schedul-R used Bash scripts, the generic framework adds a Python CLI that an agent can drive end-to-end:

```bash
# Bootstrap once
python orchestration-framework/bootstrap.py --init --project-name "MyProject"

# Then everything is one command
python cli.py execute "/orchestrator::start_workflow(user-story-refinement, phase-1, iteration-1)"
python cli.py execute "/orchestrator::launch_agents(iteration-1, parallel, 3)"
python cli.py execute "/integrator::apply_ready"
python cli.py execute "/integrator::validate_iteration(iteration-1)"
```

This is what enables the orchestrator agent to drive itself from the terminal.

### 11.3 What you must still bring yourself

The framework is *generic* — it does not know your domain. You still must author:

- A **workflow YAML** (your version of the 6-iteration cadence) under `.orchestration/config/workflows/{your-workflow}.yaml`
- **Domain-specific role configurations** (your equivalents of Architect, Tech Lead, etc., with adjusted token budgets and complexity tables)
- **Domain-specific prompt templates** under `templates/{role}.md.j2` (your equivalents of the embedded artifact structure templates)
- A **canonical documentation skeleton** (your `documentation/architecture/`, `requirements/`, `standards/` files — at least skeletons before the orchestrator starts)
- A **work_items skeleton** with at least the epic structure

Everything else — generate, launch, monitor, validate, feedback, integrator merge — is provided.

---

## 12. The Adaptation Playbook for Your New Project

Follow these steps in order. Do not skip. Do not invent variations on the first pass.

### Step 0 — Land the seeds

1. Create the new repo.
2. Drop all founder/PM seed documents (`.docx`, `.pdf`, raw `.md` notes) into `raw/`.
3. Add `.cursorignore` containing `raw/` so Cursor never edits them.
4. Commit the seeds untouched as your "v0 input archive."

### Step 1 — Bootstrap `cursor_orchestrator`

```bash
git clone https://github.com/heathbobby/cursor_orchestrator
cp -r cursor_orchestrator/orchestration-framework {your-project}/
cd {your-project}
python orchestration-framework/bootstrap.py --init \
  --project-name "{YourProjectName}" \
  --trunk-branch main
```

This creates `.orchestration/`, `.cursor/rules/`, `CONTRIBUTING.md`, and updates `.gitignore`.

### Step 2 — Extract seeds to canonical Markdown

Write/borrow a `documentation/tools/extract_docs.py` that converts every `raw/*.docx` to `documentation/extracts/*.docx.md`. (Schedul-R has one and a `raw-inventory.json`/`raw-index.md` generator that tracks versions.) This is what gives the agents readable input without ever modifying the originals.

### Step 3 — Skeleton the canonical truth

Create empty (or minimally-populated) versions of:

```
documentation/
├── requirements/PRODUCT_REQUIREMENTS.md
├── requirements/FUNCTIONAL_REQUIREMENTS.md
├── architecture/ARCHITECTURE.md
├── architecture/TECHNICAL_SPECIFICATIONS.md
├── architecture/DECISIONS.md           # ADR log
├── planning/DELIVERY_BACKLOG.md
├── planning/EXECUTION_ORCHESTRATION.md
├── planning/CONCURRENCY_ANALYSIS.md
├── standards/ENGINEERING_STANDARDS.md
├── standards/AI_AGENT_STANDARDS.md
└── standards/EVENT_CONTRACT_STANDARDS.md
```

These are the *targets* the orchestrator will fill (or refine via a "concept-extraction" iteration that reads `documentation/extracts/` and produces the first drafts). Even empty-skeleton versions tell the agents these documents exist.

### Step 4 — Define your domains and epics

Decide:

- Which **business domains** does your SaaS have? (e.g. for an analytics platform: `Platform`, `Ingestion`, `Storage`, `Query`, `Visualization`, `UserPortal`)
- Which **epics (E01..E0N)** roll up under each MVP?

Create `documentation/work_items/INDEX.md` listing epics by MVP and one folder per epic with at minimum `INDEX.md` and `DELIVERABLES.md`.

### Step 5 — Author the agent roles

Open `orchestration-framework/AGENT_ROLE_LIBRARY.md` and pick the roles you actually need. The "default 11" from §5.1 covers most SaaS projects. For each:

- Customize the role's *expertise areas* to match your tech stack (e.g. swap "Kubernetes" for "Snowflake" if you're a data product)
- Set its *complexity_budget* and *optimal_files* in `tools/generate_prompts.py` (or its equivalent config)
- Author a `templates/{role}.md.j2` Jinja template embedding **a complete artifact example** (this is the single highest-leverage thing you do — agents replicate examples, so a great example produces great output)

### Step 6 — Author your workflow YAML

Create `.orchestration/config/workflows/{your-domain}-mvp-cadence.yaml`. Model it after the user-story-refinement workflow in `cursor_orchestrator/WORKFLOW_CATALOG.md`, but encode **your six iterations**:

```yaml
workflow:
  name: mvp-progressive-documentation
  description: 6-iteration cadence per MVP
  phases:
    - phase: 1-infrastructure
      iterations: [{ name: domain-infrastructure, agents: [{ role: architect, ... }] }]
    - phase: 2-entities-models
      dependencies: [1-infrastructure]
      iterations: [{ name: entities-models, agents: [
        { role: tech_lead,      ... },
        { role: data_architect, ... }
      ]}]
    - phase: 3-integrations
      dependencies: [2-entities-models]
      iterations: [{ name: integrations, agents: [
        { role: api_architect,         ... },
        { role: integration_architect, ... }
      ]}]
    - phase: 4-features
      dependencies: [3-integrations]
      iterations: [{ name: feature-specifications, agents: [
        { role: product_owner, ... },
        { role: tech_writer,   ... }
      ]}]
    - phase: 5-quality
      dependencies: [4-features]
      iterations: [{ name: quality-testing, agents: [
        { role: qa_lead,        ... },
        { role: test_engineer,  ... }
      ]}]
    - phase: 6-operations
      dependencies: [5-quality]
      iterations: [{ name: release-operations, agents: [
        { role: sre,         ... },
        { role: tech_writer, ... }
      ]}]
```

### Step 7 — Customize the cursor rules

Copy Schedul-R's seven `.mdc` files into `.cursor/rules/` and edit:

- `project-context.mdc` — replace "Schedul-R" with your project name; update doc paths if you changed them
- `automated-orchestration.mdc` — keep verbatim (the patterns are domain-agnostic)
- `git-workflow.mdc`, `file-organization.mdc`, `standards-compliance.mdc`, `context-loading.mdc`, `backlog-refinement-workflow.mdc` — adapt naming conventions

### Step 8 — Author `MASTER_ORCHESTRATOR_INIT.md` for your project

Take Schedul-R's `documentation/refinement/MASTER_ORCHESTRATOR_INIT.md` verbatim and edit only:

- Project name
- Path to your workflow YAML
- The standard 6-iteration sequence (substitute your deliverable names)
- Directory paths if you've reorganized

**Do not change the absolute prohibitions section.** Those rules are why it works.

### Step 9 — Run a "concept-extraction" pre-iteration

Before MVP1 Iteration 1, run a custom one-off iteration that:

- **Agent**: `product_analyst` + `architect`
- **Input**: `documentation/extracts/*.md` (the converted seeds)
- **Output**: First-draft fills of `documentation/requirements/PRODUCT_REQUIREMENTS.md`, `FUNCTIONAL_REQUIREMENTS.md`, `architecture/ARCHITECTURE.md`, `planning/DELIVERY_BACKLOG.md`, and `work_items/E*/US-*.md` skeletons

This is what reconciles your noisy `.docx` versions into a single canonical truth. Schedul-R did this implicitly through manual curation; you should make it explicit.

### Step 10 — Run MVP1 Iteration 1

Now you are in steady state. Issue the boot ritual:

```
[Open Cursor in repo root]
[New chat]
[Attach the four files from §4.5]

Begin orchestration.
```

The agent will:

1. Assess state (newly bootstrapped — nothing complete)
2. Identify next priority (MVP1 Iteration 1: Domain Infrastructure)
3. Plan the iteration (create directory, CONTEXT.md, COMPLETION_CRITERIA.md, README.md)
4. Generate the architect prompt
5. Run `orchestrate_full.sh`
6. **Immediately** start planning MVP1 Iteration 2 in parallel
7. Validate and collect feedback when Iteration 1 completes
8. Apply learnings
9. Launch Iteration 2

Iterate until MVP1 is done, then proceed to MVP2.

### Step 11 — Synthesize the implementation handoff (after all MVPs complete)

Mirror Schedul-R's `documentation/implementation/`:

- `IMPLEMENTATION_ROADMAP.md` — phase-by-phase execution plan
- `TEAM_ASSIGNMENTS.md` — workstreams aligned to your domains
- `OPERATIONAL_READINESS.md` — pre-development checklist
- `INTEGRATION_TESTING_PLAN.md` — integration + E2E strategy
- `RISK_MITIGATION_PLAN.md` — risk register

Run as a final iteration with `tech_writer` + `architect` + `sre` agents synthesizing across the completed MVP docs.

---

## 13. What You (the Human) Need to Provide

Not everything can be inferred from seeds. The orchestrator will ask for these — provide them in writing up-front to save round-trips:

| Input | Why |
|---|---|
| **Project name** | All naming conventions key off it |
| **The 4 (or more) MVP scopes** | The orchestrator must know what's in each MVP to maintain scope discipline |
| **Business domains** | Drives directory structure and the "for each domain" loops in iterations |
| **Epic list (E01..E0N)** | Maps work items to deliverables |
| **Tech stack constraints** | Cloud (AWS/GCP/Azure), database (Postgres/MySQL/...), runtime (Node/Python/Go/...), messaging (Kafka/SNS/...) — embedded into the architect's templates |
| **Performance / SLO targets** | The QA Lead and SRE roles need concrete numbers for AcceptanceCriteria.md and OperationalRunbook.md |
| **Compliance constraints** | HIPAA, SOC 2, GDPR, etc. — informs Standards docs and the Security agent (if used) |
| **Token budget / model preferences** | Affects `complexity_budget` calibration and which `--model` flag the launch script uses |
| **Trunk branch and worktree location** | Fed into `bootstrap.py` |

---

## 14. Operating Cadence (Daily / Weekly Loop)

Once steady-state, this is the human's rhythm:

- **Per iteration (every ~15–30 min during active orchestration)**
  - Approve the orchestrator's "next priority" plan
  - Spot-check 2–3 generated files for quality (don't read every file)
  - Review feedback.json and confirm template/process updates
- **Per MVP completion (every ~2 hours of orchestration)**
  - Read the `MVP{N}_AUDIT_REPORT.md` the orchestrator produces
  - Decide: proceed to MVP{N+1}, or back-fill gaps via recovery iterations
- **Continuous**
  - Watch for "tool avoidance" patterns (orchestrator hand-writing things) — call it out, force a template update
  - Watch for repeated mistakes — they signal feedback isn't being applied

---

## 15. Quality Gates: Definition of "Done" at Each Layer

A **work item** is "Ready for Implementation" when:

- ✅ Definition phase complete (story format, persona, FRs/PRDs linked, acceptance criteria, MVP assigned)
- ✅ Product refinement complete (value scored, priority calculated, dependencies identified, success metrics defined)
- ✅ Technical refinement complete (architecture aligned, dependencies mapped, contracts defined, observability specified)
- ✅ All gates approved (Product Owner / Tech Lead / Architect)

An **iteration** is complete when:

- ✅ All target files exist and meet size minimums (validated by `validate_iteration.sh`)
- ✅ Agent emitted `✅ TASK_COMPLETE` (not `⚠️ TOKEN_BUDGET_LOW`)
- ✅ MVP scope maintained (no future-MVP features marked "implemented")
- ✅ Cross-domain consistency validated (terminology, references)
- ✅ `feedback.json` collected and learnings applied

An **MVP** is complete when:

- ✅ All 6 iterations completed and validated
- ✅ Audit report generated (one per MVP, e.g. `MVP1_AUDIT_REPORT.md`)
- ✅ All work items in scope are "Ready for Implementation"

The **project** is implementation-ready when:

- ✅ All planned MVPs documented end-to-end
- ✅ Implementation handoff docs synthesized (Roadmap, Team Assignments, Operational Readiness, Integration Testing, Risk Mitigation)
- ✅ Operational readiness checklist drafted (you don't need to *complete* it, but you need it to exist for engineering)

---

## 16. Risks and Mitigations (the ones Schedul-R actually hit)

| Risk | Symptom | Mitigation |
|---|---|---|
| **Orchestrator becomes a writer** | Long tool-free responses; markdown deliverables in chat | Boot prompt opens with explicit "STOP if you're typing documentation" reminder; cursor rule reinforces; human calls it out instantly |
| **Token-budget partial completions** | Iteration shows 30–60% completion rate | (a) Lower role's `complexity_budget`, (b) split into recovery sub-iteration with `orchestrate_session.sh`, (c) update template's "if you have more than N files, signal early" logic |
| **Scope creep into future MVPs** | Files reference features that belong to a later MVP | Make MVP scope table in CONTEXT.md absolute (✅/❌ matrix), add scope-validation block at top of every prompt template |
| **Quality drift across domains** | Same artifact looks different per domain | Embed a complete worked example in CONTEXT.md *and* in the role template — agents replicate examples more than instructions |
| **Tool avoidance** | Orchestrator runs `sleep 30 && ls`, hand-writes prompts, edits MVP files directly | Cursor rule lists prohibited commands literally; boot prompt enumerates the prohibited patterns with examples |
| **Empty / silent logs** | `outputs/{role}.log` is 0 bytes after agent exits | Normal behavior — agents write to target files, not logs. Trust file-stability + signal detection in `monitor_enhanced.sh`, not log size |
| **Sandbox / permission errors** | `orchestrate_full.sh` blocks asking for permissions | Approve once with `--all` or in agent settings; do not work around by going manual |
| **Agent says "I'd recommend you do X manually"** | Suggests human do the actual work | Reply with: "No. Use the agents. If the tool is broken, fix the tool." Then commit the fix back to the orchestration framework |

---

## 17. Anti-Patterns Hall of Fame (do not do these)

These are the actual failures Schedul-R logged. Treat each as a tripwire:

1. **"I'll just create the file myself, it's faster."** → Files lose template improvements, quality becomes inconsistent, system stops scaling.
2. **`sleep 60 && find documentation/MVP3 -name "*.md" -newermt "1 minute ago"`** → Defeats automation. Use `monitor_enhanced.sh --wait`.
3. **Hand-writing an agent prompt because "the template is missing something"** → The fix is to update the template.
4. **Skipping `collect_feedback.sh` because the iteration "looks fine"** → You will repeat the same mistake on the next MVP.
5. **Collecting feedback but not updating templates** → Same as not collecting it; possibly worse because of false confidence.
6. **Adding new agent roles ad-hoc per iteration** → Roles must be defined in the role library with token budgets and templates first.
7. **Letting the orchestrator wait for the agent to finish before planning the next iteration** → Costs ~30% throughput across an MVP.
8. **Combining iteration types into "mega iterations"** (e.g. "let's do entities + APIs + features in one shot") → Always exhausts budget; always produces partial completion.

---

## 18. Appendix A — File Templates (Copy-Ready)

### A.1 Minimal `CONTEXT.md` skeleton

```markdown
# {Iteration N}: {Description} — Shared Context

**Iteration**: {N} of {Total}
**Focus**: {What this iteration produces}
**Date**: YYYY-MM-DD
**Concurrent Agents**: {Agent1} + {Agent2}

## Iteration Overview
**Objective**: {Clear, one-sentence statement}
**Deliverables**:
1. `path/to/file1.md` — {Description}
2. `path/to/file2.md` — {Description}
**Target Completion**: ~X-Y minutes (concurrent execution)

## MVP{N} Scope Reminder
**IN scope** (✅ document these as "implemented"):
- E##: {Epic} — {Description}
**OUT of scope** (❌ defer; mark "Future" if referenced):
- MVP{N+1}: E## ({Feature})

## Architecture Context
[Mermaid system diagram]
[Component diagrams, data flows]

## Standards & References
- {Standard name}: {Description, link to canonical doc}
- Concrete example: ```{format}\n{example}\n```

## Domain-Specific Context
### {Domain1} (E##)
**Focus**: {Key entities, integration points, special considerations}

## Cross-Domain Coordination
1. **{Domain A} → {Domain B}**: {Contract, what must be stable, who coordinates}

## Quality Standards
{Per artifact type, what makes "good"}

## Agent Roles & Responsibilities
### {Agent1}
**Focus**: {What this agent documents}
**Deliverables**: {List}
**Domains**: {Which domains}

## Success Criteria
1. ✅ All {N} files exist
2. ✅ All artifacts documented per quality standards
3. ✅ MVP{N} scope maintained
4. ✅ Cross-domain consistency validated

**End of Shared Context — Agents: review before starting.**
```

### A.2 Minimal `COMPLETION_CRITERIA.md` skeleton

```markdown
# Iteration {N}: Completion Criteria

## Deliverables Checklist
### {Domain1}
- [ ] `documentation/MVP{N}/{Domain1}/{File}.md` (exists, >NKB)
- [ ] `documentation/MVP{N}/{Domain1}/{File2}.md` (exists, >NKB)

## Quality Standards
### {Artifact Type}
- [ ] {Required section} present
- [ ] {Required example} included

## MVP{N} Scope Compliance
- [ ] No {feature} documented as "implemented" (deferred to MVP{N+1})

## Cross-Domain Consistency
- [ ] All domains use {standard}

## Sign-Off
Iteration {N} is COMPLETE when:
1. ✅ All N files exist with substantial content
2. ✅ All deliverables checklists checked
3. ✅ Quality standards validated
4. ✅ MVP{N} scope compliance validated
```

### A.3 Minimal Jinja2 prompt template skeleton

```jinja2
# {{ role_name }} Agent — {{ iteration_name }}

**Role**: {{ role_name }}
**Task**: {{ task_description }}
**Iteration**: {{ iteration_name }}
**Files Target**: {{ file_count }}

## EXECUTE NOW
You are EXECUTING this task autonomously. DO NOT ask for permission.

**BEGIN IMMEDIATELY** — Complete these {{ file_count }} files sequentially:
{% for file in files %}
{{ loop.index }}. `{{ file.path }}` (Complexity: {{ file.complexity }})
{% endfor %}

Use the write tool. Target {{ min_size_kb }}-{{ max_size_kb }}KB per file.

## Your Role ({{ role_name }} v{{ role_version }})
**Core Responsibility**: {{ role_summary }}
**Expertise Areas**: {{ expertise_list }}
**Output Standards**: see `@{{ role_definition_path }}`

## Token Budget Management
{% if estimated_tokens > 80000 %}
⚠️ **HIGH TOKEN LOAD** — Work sequentially, signal every 2 files
{% elif file_count > 5 %}
⚠️ **MODERATE LOAD** — Process sequentially, signal completion
{% else %}
✅ **MANAGEABLE** — Process all, signal `✅ TASK_COMPLETE`
{% endif %}

## Artifact Structure (REQUIRED)
[Embed concrete worked example here — this is the single highest-leverage section]

## Success Criteria
- All {{ file_count }} files completed
- Each file ≥ {{ min_size_kb }}KB
- {{ specific success criteria }}

## Completion Signals
**When complete**:
```
✅ TASK_COMPLETE: {{ file_count }}/{{ file_count }} {{ artifact_type }} generated
```
**If unable to complete**:
```
⚠️ TOKEN_BUDGET_LOW: Completed X/{{ file_count }} files
Completed: [list]
Remaining: [list]
Recommendation: Create follow-up iteration for remaining files
```

**BEGIN NOW** with file 1: `{{ files[0].path }}`
```

### A.4 The four files to attach when starting the orchestrator

(Reproduced for the new project — replace `documentation/refinement/` with whatever path your project uses.)

```
@documentation/refinement/MASTER_ORCHESTRATOR_INIT.md
@documentation/refinement/agent-roles/MASTER_ORCHESTRATOR.md
@documentation/refinement/ORCHESTRATION_PLAYBOOK.md
@documentation/refinement/SCALABLE_ORCHESTRATION_PHILOSOPHY.md
```

Then send: **"Begin orchestration."**

---

## 19. Appendix B — The First-Day Run-Sheet

Print this. Follow it. Don't deviate.

### Hour 0–1: Setup
- [ ] Clone target repo
- [ ] Drop seeds into `raw/`, add `.cursorignore`
- [ ] `git clone heathbobby/cursor_orchestrator`
- [ ] `cp -r cursor_orchestrator/orchestration-framework {target}/`
- [ ] `python orchestration-framework/bootstrap.py --init --project-name "{name}"`
- [ ] Commit: `chore: bootstrap orchestration framework`

### Hour 1–3: Customize
- [ ] Copy Schedul-R's `.cursor/rules/*.mdc` files into target's `.cursor/rules/`, edit project name
- [ ] Author `documentation/refinement/MASTER_ORCHESTRATOR_INIT.md` (copy + edit Schedul-R's)
- [ ] Author `documentation/refinement/agent-roles/MASTER_ORCHESTRATOR.md`
- [ ] Author `documentation/refinement/ORCHESTRATION_PLAYBOOK.md`
- [ ] Author `documentation/refinement/SCALABLE_ORCHESTRATION_PHILOSOPHY.md`
- [ ] Author `documentation/refinement/APPLYING_LEARNINGS_PLAYBOOK.md`
- [ ] Author `.orchestration/config/workflows/mvp-progressive-documentation.yaml`
- [ ] Skeleton `documentation/{requirements,architecture,standards,planning}/`
- [ ] Skeleton `documentation/work_items/INDEX.md` and `E01/E02/...` folders

### Hour 3–4: Concept extraction
- [ ] Write `documentation/tools/extract_docs.py` (or borrow Schedul-R's)
- [ ] Run extraction → `documentation/extracts/*.md`
- [ ] Manually run a one-off "concept-extraction" iteration to draft canonical requirements + architecture

### Hour 4+: Steady state
- [ ] Open Cursor, new chat
- [ ] Attach the four boot files
- [ ] Send: **"Begin orchestration."**
- [ ] Approve the orchestrator's first-action assessment
- [ ] Walk away for 15 minutes; come back for the validation review

---

## 20. Final Note: The One Insight

The thing that makes this whole system work — that is responsible for the success of Schedul-R and that you must preserve in the new project — is:

> **The orchestrator's job is to make sure the system improves with every iteration, not to make sure each iteration succeeds.**

A perfect iteration that doesn't update a template or role definition is *less valuable* than an imperfect iteration whose feedback gets baked into the next one. That is why the absolute prohibitions exist (they prevent shortcuts that hide what's broken), why feedback is mandatory (it makes what's broken visible), and why the templates evolve (they encode every lesson learned).

If the new project's orchestrator follows that one principle, every other detail in this playbook is recoverable. If it doesn't, none of them are.

---

**End of Playbook.**

**Next document to read** (in the new project): `cursor_orchestrator/GENERIC_ORCHESTRATION_FRAMEWORK.md` for the framework's own conceptual reference.

**Source attribution**: Distilled from the Schedul-R project (`c:\Users\Heath\dev\Scheduling`), specifically:
- `documentation/refinement/MASTER_ORCHESTRATOR_INIT.md`
- `documentation/refinement/ORCHESTRATION_PLAYBOOK.md`
- `documentation/refinement/SCALABLE_ORCHESTRATION_PHILOSOPHY.md`
- `documentation/refinement/CONTINUOUS_IMPROVEMENT_FRAMEWORK.md`
- `documentation/refinement/APPLYING_LEARNINGS_PLAYBOOK.md`
- `documentation/refinement/COMPLETION_SIGNALS_SYSTEM.md`
- `documentation/refinement/PARALLEL_ITERATION_PATTERN.md`
- `documentation/refinement/PROGRESSIVE_DOCUMENTATION_PLAN.md`
- `documentation/refinement/AGENT_ROLE_DEFINITIONS.md`
- `documentation/refinement/agent-roles/*.md`
- `documentation/refinement/templates/prompts/*.j2`
- `documentation/refinement/{generate_prompts.py, orchestrate_full.sh, monitor_enhanced.sh, validate_iteration.sh, collect_feedback.sh, orchestrate_session.sh}`
- `documentation/orchestration-framework/{GENERIC_ORCHESTRATION_FRAMEWORK.md, WORKFLOW_CATALOG.md, AGENT_ROLE_LIBRARY.md, bootstrap.py, cli.py}`
- `.cursor/rules/{automated-orchestration, backlog-refinement-workflow, project-context, file-organization, git-workflow, standards-compliance, context-loading}.mdc`
- `cursor_orchestrator` GitHub repo: `README.md`, `WORKFLOW_CATALOG.md`, `AGENT_ROLE_LIBRARY.md`, `config.yaml.example`, `templates/COMMAND_SHORTHAND.md`
