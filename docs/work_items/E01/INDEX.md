# E01: Canonical Documentation Foundation

- **Status**: refined backlog foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `backlog-refinement`
- **Last updated**: 2026-05-03
- **MVP**: MVP1 - Canonical concept-to-implementation pipeline
- **Primary trace**: PRD-001, PRD-002, PRD-008; FR-001, FR-002, FR-003, FR-004, FR-019

## Epic purpose

Establish the canonical documentation foundation that lets Synapse move one
initiative from concept inputs into implementation-ready requirements, planning,
and work items without losing provenance or uncertainty. E01 is the first MVP1
epic because workflow definitions, validation, backlog generation, and handoff
all depend on stable canonical paths, source-attribution rules, open-question
tracking, and acceptance-quality criteria.

## Scope

### In scope for E01

- Canonical documentation registry for requirements, architecture, planning,
  standards, work items, and refinement artifacts.
- Requirement and artifact metadata expectations for source/evidence,
  assumptions, open questions, validation needs, and readiness.
- Immutable handling of `raw/` and `research/` source inputs during canonical
  drafting.
- Open-question and validation-need tracking for backlog and downstream
  architecture/product decisions.
- Acceptance-quality criteria for canonical artifacts before downstream stories
  are promoted.

### Out of scope for E01

- Workflow/task-packet schema details owned by E02.
- Deterministic validator implementation or signal formats owned by E03.
- Full backlog generation and readiness-gate application owned by E04.
- Runtime, UI, storage, cloud, LLM-provider, compliance, pricing, or GTM
  commitments.

## Story map

| Story | Title | Readiness status | Requirement trace | Dependencies | Summary |
| --- | --- | --- | --- | --- | --- |
| US-E01-001 | Define the canonical documentation registry | Refined | PRD-001; FR-001 | None | Identify canonical doc families and paths agents should treat as implementation truth. |
| US-E01-002 | Standardize source attribution and uncertainty labels | Refined | PRD-002; FR-002, FR-004 | US-E01-001 | Require source/evidence, status, assumptions, open questions, and validation needs on canonical requirements and backlog artifacts. |
| US-E01-003 | Protect raw and research inputs during canonical drafting | Refined | PRD-001, PRD-002; FR-003 | US-E01-001 | Make source immutability visible in work-item expectations and acceptance criteria. |
| US-E01-004 | Maintain the open-question and validation-need register | Refined | PRD-002; FR-004 | US-E01-002 | Keep unresolved decisions visible with impact, blocking status, and affected epics/stories. |
| US-E01-005 | Define canonical artifact acceptance-quality criteria | Refined | PRD-001, PRD-008; FR-001, FR-019 | US-E01-001, US-E01-002 | State quality gates for canonical docs before downstream MVP1 work starts. |

## Story details

### US-E01-001: Define the canonical documentation registry

**User story**: As a human operator, I need the canonical documentation registry
to identify the implementation-truth locations for Synapse artifacts, so that
agents and humans cite stable docs instead of raw seed files or ad hoc notes.

**Readiness status**: Refined

**Requirement trace**: PRD-001; FR-001

**Dependencies**: None

**Acceptance-quality criteria**

- Given an agent starts Synapse concept-to-implementation work, when it looks for
  product, functional, planning, architecture, standards, work-item, or
  refinement context, then the canonical `docs/` path family is identifiable.
- Given a backlog item cites requirements or planning context, when it is
  reviewed, then it points to canonical docs rather than treating `raw/` or
  `research/` files as implementation truth.
- Given a new canonical artifact family is introduced, when it is added to the
  registry, then its owning workflow, purpose, and downstream consumers are
  clear.

**Open questions / assumptions**

- Assumption: the long-term canonical root remains `docs/` until architecture
  records a replacement decision.
- Open question: should future initiatives support external repositories or
  cross-workspace canonical registries?

### US-E01-002: Standardize source attribution and uncertainty labels

**User story**: As a product stakeholder, I need each canonical artifact to show
source/evidence and uncertainty status, so that assumptions are not mistaken for
committed product scope.

**Readiness status**: Refined

**Requirement trace**: PRD-002; FR-002, FR-004

**Dependencies**: US-E01-001

**Acceptance-quality criteria**

- Given a requirement, epic, story, decision, or planning assertion is created,
  when it is saved in canonical docs, then it includes requirement/source trace
  or explicitly marks the item as an assumption, open question, or validation
  need.
- Given unsupported details are requested, when no source support exists, then
  the detail is recorded as an open question or validation need rather than
  promoted to committed scope.
- Given a downstream story references a canonical requirement, when it is
  reviewed, then PRD/FR IDs and confidence/readiness status are visible.

**Open questions / assumptions**

- Assumption: Source-backed, assumption, open-question, and validation-need
  labels are sufficient for MVP1.
- Open question: should Synapse add machine-readable metadata blocks or keep
  traceability in Markdown tables for MVP1?

### US-E01-003: Protect raw and research inputs during canonical drafting

**User story**: As a repository maintainer, I need raw and research inputs to
remain immutable during canonical drafting, so that provenance remains intact and
derived artifacts can be audited.

**Readiness status**: Refined

**Requirement trace**: PRD-001, PRD-002; FR-003

**Dependencies**: US-E01-001

**Acceptance-quality criteria**

- Given a Synapse backlog-refinement or concept-extraction agent writes outputs,
  when work completes, then only approved canonical deliverables were modified.
- Given a seed source is cited, when an artifact references it, then the source
  path is cited without changing the seed file.
- Given a source mutation is detected, when recovery starts, then the mutation is
  treated as unauthorized and downstream canonical work is checked for valid
  provenance.

**Open questions / assumptions**

- Assumption: `raw/` and `research/` remain read-only source areas for MVP1.
- Open question: should immutable-source protection be enforced by convention,
  validation script, repository permissions, or all three?

### US-E01-004: Maintain the open-question and validation-need register

**User story**: As a delivery planner, I need blocking questions and validation
needs visible beside the affected work, so that implementation does not begin on
unsupported scope.

**Readiness status**: Refined

**Requirement trace**: PRD-002; FR-004

**Dependencies**: US-E01-002

**Acceptance-quality criteria**

- Given an open question blocks product, architecture, quality, or sequencing
  decisions, when it is recorded, then the affected epics/stories and impact are
  listed.
- Given validation evidence later resolves a question, when canonical docs are
  updated, then the relevant requirement or backlog item can be promoted,
  revised, deferred, or dropped with source attribution.
- Given a story is reviewed for readiness, when it has blocking open questions,
  then readiness remains Draft or Refined rather than Ready candidate.

**Open questions / assumptions**

- Assumption: E01 can maintain open questions in Markdown tables until a runtime
  issue tracker or decision system is selected.
- Open question: who owns final resolution of product-mode, first-domain,
  compliance, and MVP1 delivery-depth questions?

### US-E01-005: Define canonical artifact acceptance-quality criteria

**User story**: As a delivery lead, I need acceptance-quality criteria for
canonical artifacts, so that downstream workflow, validation, backlog, and
handoff work starts from reviewed contracts.

**Readiness status**: Refined

**Requirement trace**: PRD-001, PRD-008; FR-001, FR-019

**Dependencies**: US-E01-001, US-E01-002

**Acceptance-quality criteria**

- Given a canonical artifact is submitted for downstream use, when it is
  reviewed, then purpose, scope, source trace, assumptions/open questions,
  dependencies, acceptance criteria, and readiness status are present.
- Given a story is promoted toward implementation, when readiness is assessed,
  then product, requirements traceability, architecture/technical, quality,
  dependencies, risk, and implementation gates are recorded.
- Given an artifact lacks source trace or unresolved assumptions are hidden,
  when quality review occurs, then the artifact is not accepted as
  implementation-ready.

**Open questions / assumptions**

- Assumption: E01 defines quality criteria; E03 may later add deterministic
  validation for checking them.
- Open question: which acceptance-quality checks should become automated in
  MVP1 versus remain human review criteria?

## Epic-level dependencies

| Dependency | Type | Status | Notes |
| --- | --- | --- | --- |
| Canonical PRD and FR IDs | Upstream requirement | Available | `PRODUCT_REQUIREMENTS.md` and `FUNCTIONAL_REQUIREMENTS.md` provide stable IDs for E01 traceability. |
| MVP1 delivery mode decision | Product/architecture decision | Accepted | CLI-assisted orchestration using the existing framework; runtime-backed product behavior deferred. |
| First domain or internal initiative | Product decision | Open | If unresolved, use this repository's concept-to-implementation workflow as the internal MVP1 reference initiative. |
| Metadata format | Product/technical decision | Open | Markdown tables are acceptable for refinement; machine-readable front matter remains a possible future enhancement. |

## Epic-level assumptions and open questions

| ID | Type | Item | Impact |
| --- | --- | --- | --- |
| A-E01-001 | Assumption | `docs/` is the canonical implementation-truth root for MVP1. | Enables E01-E05 to proceed without inventing external registry mechanics. |
| D-E01-001 | Decision | MVP1 delivery is CLI-assisted orchestration using the existing framework. | Unblocks E02 and constrains E05 handoff scope. |
| D-E01-002 | Decision | The orchestration framework is the first internal foundation domain/initiative. | Gives the internal foundation concrete templates and backlog examples; product MVPs are tracked separately. |
| D-E01-003 | Decision | MVP1 canonical metadata is Markdown-first, using structured headings and tables. | Unblocks task packets and validators; machine-readable schemas are deferred. |
| D-E01-004 | Decision | Initial deterministic validators target files, sections, trace IDs, ID formats, source immutability, and completion signals. | Gives E03 a concrete validator scope. |
| OQ-E01-002 | Open question | Which sponsor or role approves open-question resolution and story promotion? | Affects readiness governance for E04/E05; default role-based approvers are proposed in technical gates. |
| OQ-E01-003 | Open question | What repository or workspace boundaries must future initiatives support? | Affects long-term canonical registry design. |

## Downstream handoff

E01 is ready for downstream technical refinement when:

- The canonical registry and Markdown-first metadata expectations are accepted by product,
  architecture, and quality reviewers.
- E01 stories retain PRD/FR traceability and visible assumptions/open questions.
- Raw and research immutability remains explicit in story criteria.
- E02, E03, E04, and E05 can cite E01 as the source for canonical paths,
  provenance expectations, and artifact readiness criteria.

