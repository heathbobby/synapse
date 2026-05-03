# E01 Deliverables: Canonical Documentation Foundation

- **Status**: refined backlog foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `backlog-refinement`
- **Last updated**: 2026-05-03
- **MVP**: MVP1 - Canonical concept-to-implementation pipeline
- **Epic trace**: PRD-001, PRD-002, PRD-008; FR-001, FR-002, FR-003, FR-004, FR-019

## Purpose

This file defines the concrete E01 outputs required before downstream MVP1 work
can treat canonical documentation as a stable contract. E01 does not implement
workflow execution, validators, runtime services, or UI behavior; it defines the
documentation foundation those later epics depend on.

## Deliverable summary

| Deliverable | Related stories | Readiness status | Requirement trace | Dependencies | Acceptance-quality focus |
| --- | --- | --- | --- | --- | --- |
| D-E01-001 Canonical documentation registry | US-E01-001 | Refined | PRD-001; FR-001 | None | Canonical path families, purpose, owners/consumers, and source-of-truth expectations are explicit. |
| D-E01-002 Attribution and uncertainty standard | US-E01-002 | Refined | PRD-002; FR-002, FR-004 | D-E01-001 | Source/evidence, assumptions, open questions, validation needs, and readiness labels are consistently defined. |
| D-E01-003 Immutable source handling rule | US-E01-003 | Refined | PRD-001, PRD-002; FR-003 | D-E01-001 | `raw/` and `research/` remain read-only inputs; canonical outputs cite them without mutation. |
| D-E01-004 Open-question and validation register | US-E01-004 | Refined | PRD-002; FR-004 | D-E01-002 | Blocking questions show impact, affected work, and resolution path. |
| D-E01-005 Canonical artifact quality gate | US-E01-005 | Refined | PRD-001, PRD-008; FR-001, FR-019 | D-E01-001, D-E01-002 | Product, traceability, architecture/technical, quality, dependency, risk, and implementation criteria are inspectable. |

## Deliverable details

### D-E01-001: Canonical documentation registry

**Outcome**: A human and agent can identify the canonical documentation families
that hold implementation truth for Synapse MVP1.

**Expected content**

- Canonical paths for requirements, architecture, planning, standards, work
  items, and refinement artifacts.
- Purpose for each path family and how downstream agents should use it.
- Rule that raw and research files are source inputs, not implementation truth,
  until promoted into canonical docs with provenance.
- Known gaps where future registry behavior may need external repository or
  cross-workspace support.

**Acceptance-quality criteria**

- The registry is understandable without reading raw source packets.
- Every listed path family has a clear downstream use.
- New backlog items can cite canonical documents using stable paths.
- Unsupported future registry mechanics remain open questions.

### D-E01-002: Attribution and uncertainty standard

**Outcome**: Canonical artifacts use a shared language for source support and
uncertainty so downstream work does not overcommit.

**Expected content**

- Labels for source-backed items, assumptions, open questions, and validation
  needs.
- Requirement trace expectations for PRD IDs, FR IDs, and affected backlog IDs.
- Readiness status expectations for Draft, Refined, Ready candidate, and
  Deferred backlog items.
- Guidance that unsupported specificity must be recorded as an assumption, open
  question, or validation need.

**Acceptance-quality criteria**

- A reviewer can distinguish committed source-backed scope from hypotheses.
- Each E01 story links to PRD/FR IDs.
- Open questions and validation needs are visible beside affected work.
- The standard can be applied in Markdown without requiring a runtime tool.

### D-E01-003: Immutable source handling rule

**Outcome**: Source provenance remains intact while canonical docs evolve.

**Expected content**

- Explicit rule that `raw/` and `research/` are not edited during canonical
  drafting or backlog refinement.
- Citation expectation for source paths when canonical artifacts rely on seed
  material.
- Recovery expectation if source mutation is detected.
- Handoff note for E03 to consider deterministic checks for forbidden source
  mutations.

**Acceptance-quality criteria**

- The rule is visible in E01 story criteria and downstream readiness gates.
- Canonical work can cite source files without modifying them.
- Recovery behavior distinguishes unauthorized source edits from valid derived
  canonical work.

### D-E01-004: Open-question and validation register

**Outcome**: Blocking uncertainty is tracked with affected work and impact.

**Initial register**

| ID | Type | Question or assumption | Affected work | Blocking status |
| --- | --- | --- | --- | --- |
| A-E01-001 | Assumption | `docs/` is the MVP1 canonical implementation-truth root. | E01-E05 | Non-blocking for E01; revisit if architecture changes registry boundaries. |
| D-E01-001 | Decision | MVP1 is CLI-assisted using `orchestration-framework/cli.py`, generated task cards, memos, and canonical docs. | E02-E05 | Accepted; runtime-backed Synapse product behavior is deferred. |
| D-E01-002 | Decision | The orchestration framework is the first internal MVP1 domain/initiative. | E02, E04 | Accepted; use existing workflows, task cards, memos, and framework conventions as the template domain. |
| D-E01-003 | Decision | MVP1 metadata remains Markdown-first with structured tables/headings. | E02, E03, E04 | Accepted; machine-readable front matter/schema extraction is deferred until validators require it. |
| D-E01-004 | Decision | Initial deterministic validators target required files, required sections, PRD/FR trace markers, E##/US-E## ID format, prohibited source mutations, and completion-signal format. | E03, E04, E05 | Accepted; review-only criteria remain labeled. |
| OQ-E01-002 | Open question | Which sponsor or role approves story promotion and open-question closure? | E04, E05 | Default role-based approvers are proposed, but sponsor override remains possible. |
| OQ-E01-003 | Open question | What repository or workspace boundaries must future initiatives support? | E01, E06, E08 | Blocks long-term registry design, not MVP1 internal pipeline refinement. |

**Acceptance-quality criteria**

- Each open question has affected work and blocking status.
- Non-blocking assumptions are safe enough for E01 refinement and explicitly
  reversible.
- Resolution of a question can promote, revise, defer, or drop affected work
  with source attribution.

### D-E01-005: Canonical artifact quality gate

**Outcome**: Canonical artifacts have a shared review checklist before they are
used as downstream implementation contracts.

**Quality gate**

| Gate | Required evidence |
| --- | --- |
| Product | Persona or operator, user value, MVP fit, scope boundaries, assumptions, open questions, and exclusions are explicit. |
| Requirements traceability | PRD and FR IDs are linked where applicable; unsupported details are labeled. |
| Architecture/technical | Technical boundaries, data/integration implications, write targets, and sequencing constraints are reviewed or marked non-blocking. |
| Quality | Acceptance criteria, validation approach, deterministic-check candidates, and failure/recovery expectations are documented. |
| Dependencies | Upstream docs, decisions, stories, and unsafe parallelism are listed. |
| Risk | Source provenance, security/privacy, reliability, token-budget, and scope-creep risks are considered where relevant. |
| Implementation | Work is small enough to execute and has inspectable done criteria. |

**Acceptance-quality criteria**

- A downstream epic can cite this gate when assessing story readiness.
- Missing PRD/FR traceability or hidden assumptions prevent promotion to Ready
  candidate.
- The gate identifies which checks are currently human-reviewed and which are
  candidates for E03 deterministic validation.

## Cross-epic dependencies and handoff

| Downstream epic | What it receives from E01 | Handoff condition |
| --- | --- | --- |
| E02 Workflow Definition and Task-Packet Model | Canonical paths, metadata expectations, source/uncertainty labels, and quality gate. | E02 can draft task packets without redefining canonical documentation rules. |
| E03 Deterministic Validation and Completion Signals | Candidate checks for source immutability, required sections, traceability, and quality gate completeness. | E03 can decide which E01 criteria become automated versus human-reviewed. |
| E04 Backlog Generation and Readiness Gates | Story naming convention, PRD/FR traceability expectations, readiness statuses, and dependency/open-question format. | E04 can expand backlog items without inventing new readiness semantics. |
| E05 Orchestration Execution Handoff | Accepted foundation assumptions, unresolved blockers, and MVP1 readiness constraints. | E05 can package launch sequencing around known foundation decisions. |

## Risks

| Risk | Impact | Mitigation |
| --- | --- | --- |
| Metadata format churn | E02/E03 may need rework if Markdown tables later become machine-readable schemas. | Keep MVP1 Markdown-first and sequence schema/front matter extraction as a later validator-driven spike. |
| Product-mode overreach | E05 could drift into runtime-backed product behavior despite CLI-assisted MVP1 scope. | Anchor E05 to CLI-assisted orchestration and explicitly defer runtime-backed behavior. |
| Source mutation | Provenance and auditability degrade if seed files are edited. | Preserve immutable-source rule and hand off automation candidate to E03. |
| Overcommitting future MVP scope | Persona, monitoring, approval, and legacy bridge details could leak into MVP1. | Mark E06-E13 as deferred and keep E01 scope limited to the canonical pipeline foundation. |

## Done criteria for E01 refinement

E01 is ready for parent review when:

- `docs/work_items/INDEX.md` uses `E##` and `US-E##-###` naming and centers
  MVP1 on the canonical concept-to-implementation pipeline.
- `docs/work_items/E01/INDEX.md` contains refined US-E01 stories with PRD/FR
  traceability, readiness status, dependencies, assumptions/open questions, and
  acceptance-quality criteria.
- This deliverables file lists concrete E01 outputs, handoffs, quality gates,
  risks, and blocking questions.
- No `raw/` or `research/` files are modified.
