# MVP2 Knowledge Source Inventory

- **Status**: draft MVP2 source-grounding foundation
- **Owning workflow**: `synapse-concept-to-implementation`
- **Iteration**: `mvp2-iteration-01-source-grounding`
- **Domain**: Knowledge grounding for repeatable SME agents
- **Last updated**: 2026-05-03

## Purpose

This inventory defines the initial MVP2 source classes, priorities, ownership,
freshness, confidence, provenance, and consumption boundaries for Synapse
knowledge grounding. It extends the MVP1 repository-first operating model into a
technology-neutral source-grounding contract for future role agents, persona
templates, domain configuration, and learning promotion.

This document does not select or imply a knowledge store, retrieval mechanism,
embedding model, connector, crawler, synchronization job, tenancy model,
access-control model, retention policy, compliance control, provider runtime, or
source-system integration technology.

## Source basis

| Source | How this inventory uses it |
| --- | --- |
| `docs/refinement/iteration-inputs/mvp2-iteration-01-source-grounding.md` | Iteration goal, role references, source-priority expectations, and future-scope exclusions. |
| `docs/requirements/PRODUCT_REQUIREMENTS.md` | PRD-001, PRD-002, PRD-007, and PRD-009 for canonical truth, provenance, learning loops, and domain-agnostic configuration. |
| `docs/requirements/FUNCTIONAL_REQUIREMENTS.md` | FR-001, FR-002, FR-003, FR-004, FR-010, FR-016, FR-017, FR-021, and FR-022 for canonical registries, source attribution, immutable source handling, grounding, feedback, and implementation-agnostic boundaries. |
| `docs/architecture/ARCHITECTURE.md` | Canonical truth principle, knowledge and grounding layer, SME knowledge models, knowledge loop, and open decisions. |
| `docs/architecture/TECHNICAL_SPECIFICATIONS.md` | KnowledgeAsset conceptual contract, evidence class, confidence, freshness, applicability, and open storage/retrieval decisions. |
| `docs/architecture/DECISIONS.md` | ADR-0002, ADR-0006, ADR-0009, ADR-0010, ADR-0011 through ADR-0014, and OAD-0005 for accepted source/knowledge direction and open implementation decisions. |
| `docs/MVP1/Platform/Overview.md` | MVP1 scope: canonical `docs/` truth, CLI-assisted orchestration, runtime memos as operational evidence, and deferred knowledge retrieval store. |
| `docs/MVP1/Platform/Infrastructure.md` | Canonical path families, runtime artifact posture, validation scope, and source immutability guardrails. |
| `docs/MVP1/Platform/DataModel.md` | Logical records for deliverables, task packets, memos, validation, decisions, readiness gates, runtime references, and data-quality rules. |
| `docs/MVP1/Platform/Integrations.md` | Integration participants, handoff contracts, telemetry/log reference treatment, and recovery flow. |
| `docs/MVP1/Platform/TestingStrategy.md` | Quality gates, source immutability checks, future-scope guard, and review-only evidence sufficiency. |
| `docs/MVP1/Platform/AcceptanceCriteria.md` | Acceptance criteria for source immutability, traceability, handoff, runtime finding promotion, and technology-neutral integration. |
| `docs/MVP1/Platform/OperationalRunbook.md` | Operational source handling, runtime artifact management, incidents, escalation, and source-immutability recovery. |
| `docs/MVP1/Platform/ReleaseNotes.md` | Released MVP1 artifact set, readiness state, known limitations, and next actions. |
| `docs/implementation/IMPLEMENTATION_ROADMAP.md` | E06 placement after E01/E02, MVP1 handoff limitations, runtime/log treatment, and open decision register. |
| `docs/work_items/INDEX.md` | E06 source inventory and grounding model scope, dependencies, and deferred status. |
| `docs/work_items/DEPENDENCY_MAP.md` | E06 dependencies, G3 knowledge/persona gate, blocker B-DM-007, and safe/unsafe MVP2 sequencing. |
| `docs/standards/AI_AGENT_STANDARDS.md` | Required task-packet inputs, evidence classes, output quality, handoff, and promotion governance. |
| `docs/standards/EVENT_CONTRACT_STANDARDS.md` | Conceptual knowledge, persona, validation, telemetry, and promotion event families without implementation commitment. |

## Inventory principles

1. **Approved knowledge starts with promoted sources**: Canonical `docs/`
   artifacts and reviewed `.orchestration/config/` files are the initial approved
   source families for MVP2. Raw, research, runtime, and external materials are
   inputs or operational evidence until reviewed and promoted.
2. **Source class is not storage class**: Source categories describe trust,
   ownership, freshness, and consumption contracts. They do not imply a database,
   index, connector, serialization format, or retrieval technology.
3. **Provenance travels with claims**: Any material claim used by a role agent or
   persona must retain source path or source record, evidence class, confidence,
   owner, last-reviewed marker when known, and open decisions.
4. **Freshness is review responsibility**: MVP2 defines review cadence and stale
   markers conceptually. It does not automate crawling, expiry, retention, or
   synchronization.
5. **Operational sources require promotion**: Runtime memos, logs, command
   output, validation output, and task cards can inform knowledge only after
   material facts are summarized into canonical docs, standards, work items,
   decision logs, or approved extracts.
6. **Future source systems stay future**: External documentation systems,
   ticketing, code repositories, communication tools, incident systems, customer
   corpora, and legacy systems remain future/open until source ownership,
   access, compliance, and adapter boundaries are accepted.

## Source class model

| Class ID | Source class | Examples | MVP2 status | Primary owner role | Default consumer posture |
| --- | --- | --- | --- | --- | --- |
| SC-01 | Canonical requirements and product scope | `docs/requirements/PRODUCT_REQUIREMENTS.md`, `docs/requirements/FUNCTIONAL_REQUIREMENTS.md` | Approved source | Product owner / requirements owner | May ground product, persona, workflow, and backlog claims when cited with PRD/FR IDs. |
| SC-02 | Canonical architecture and decisions | `docs/architecture/ARCHITECTURE.md`, `docs/architecture/TECHNICAL_SPECIFICATIONS.md`, `docs/architecture/DECISIONS.md` | Approved source | Architect / data architect / tech lead | May ground architecture, data, integration, and open-decision claims; open decisions block implementation specifics. |
| SC-03 | MVP1 platform contract docs | `docs/MVP1/Platform/*.md`, including feature, quality, acceptance, operations, and release docs | Approved source for MVP1 operating model | Domain architect / integrator | May ground MVP2 inheritance from MVP1, including task packets, runtime artifact treatment, validation, and handoff rules. |
| SC-04 | Work items, dependency maps, and roadmap | `docs/work_items/INDEX.md`, `docs/work_items/DEPENDENCY_MAP.md`, `docs/implementation/IMPLEMENTATION_ROADMAP.md` | Approved source for sequencing | Backlog owner / dependency analyst / implementation planner | May ground priorities, dependencies, blockers, gate status, and owner expectations. |
| SC-05 | Standards and reusable governance | `docs/standards/AI_AGENT_STANDARDS.md`, `docs/standards/EVENT_CONTRACT_STANDARDS.md`, future knowledge-grounding standards | Approved source | Standards curator / integrator | May ground role-agent behavior, evidence classes, completion signals, handoffs, and reusable-promotion gates. |
| SC-06 | Orchestration configuration | `.orchestration/config/workflows/*.yaml`, `.orchestration/config/agent-personas.yaml` | Approved configuration source when reviewed | Orchestrator / configuration owner | May ground workflow phase/iteration/role bindings and persona role contracts; config drift requires reconciliation with canonical docs. |
| SC-07 | Reviewed iteration input packets | `docs/refinement/iteration-inputs/*.md` | Approved boundary source for the named iteration | Orchestrator / integrator | May bound role-agent work, deliverables, prohibited edits, and completion criteria for the related iteration. |
| SC-08 | Runtime memos, task cards, logs, and command output | `.orchestration/runtime/agent-sync/`, `.orchestration/runtime/iterations/`, branch/SHA notes, validation command summaries | Operational source only | Orchestrator / integrator / producing agent | Must not be treated as durable knowledge until material facts are promoted through review. |
| SC-09 | Raw and research seed material | `raw/`, `research/` | Seed source only; immutable | Source owner / integrator | Read-only input for reviewed promotion; not direct implementation truth and not editable by MVP2 tasks. |
| SC-10 | Future external source systems | External docs, tickets, code repositories, chat, incidents, customer/legacy corpora, operational tools | Future/open | To be assigned by domain/source-system decision | Discovery candidates only until source owner, access, provenance, compliance, and promotion rules are accepted. |
| SC-11 | Human/SME review evidence | Reviewer decisions, SME annotations, approval rationales, source-review notes | Approved only when recorded in canonical artifact or approved review record | Reviewer / SME / gate owner | May adjust confidence, applicability, and promotion state; must include reviewer role, evidence reviewed, rationale, and limits. |

## MVP2 source priority

| Priority | Source classes | Rationale | Promotion requirement |
| --- | --- | --- | --- |
| P0 - Binding canonical contract | SC-01, SC-02, SC-03, SC-04, SC-05 | These are the strongest existing sources for MVP2 because they are canonical `docs/` outputs with accepted scope, requirements, architecture, standards, and sequencing. | Already approved within documented status limits; cite path/ID and preserve open decisions. |
| P1 - Approved workflow configuration and packets | SC-06, SC-07 | These define role, phase, iteration, deliverable, and task boundaries needed for persona/template work. | Review against canonical docs before treating as reusable guidance; record owner and drift if config and docs disagree. |
| P2 - Operational evidence needing summary | SC-08 | Runtime memos and logs reveal execution facts, blockers, validation issues, and repeated learnings. | Summarize material facts into canonical docs, standards, work items, decision logs, or approved extracts before reuse. |
| P3 - Immutable seed evidence | SC-09 | Raw/research files are original context but not current implementation truth. | Promote claims through reviewed canonical docs; do not edit sources or cite them as runtime truth unless a task explicitly asks for source archaeology. |
| P4 - Future domain/external evidence | SC-10, SC-11 when not yet canonicalized | External systems and SME review will be necessary for broader Synapse use cases but currently lack accepted boundaries. | Define source owner, authority, access boundary, provenance, confidence, freshness, and compliance posture before promotion. |

## Approved vs operational source rules

| Source posture | Meaning | Can directly ground role-agent outputs? | Required handling |
| --- | --- | --- | --- |
| Approved source | Reviewed canonical doc, standard, decision, work item, roadmap, or configuration accepted for its stated scope. | Yes, within scope and status limits. | Cite path, section or ID when practical; preserve status, assumptions, open decisions, and last-updated metadata. |
| Approved extract | A reviewed summary of seed, runtime, SME, or external evidence promoted into a canonical artifact. | Yes, within the extract's stated applicability. | Cite the extract and original source reference when available; include reviewer and confidence. |
| Operational source | Runtime memo, generated task card, log, command output, validation output, branch/SHA reference, or transient handoff. | No, not as durable truth. | Use only for traceability or recovery until summarized into approved source or extract. |
| Seed source | Raw or research material that preserves original context. | No for implementation truth; yes for bounded source review. | Read-only; promote findings through canonical docs and mark source-backed, inferred, assumed, or open. |
| Future candidate source | External or legacy system source not yet governed by accepted boundaries. | No. | Treat as discovery input; record open decisions for owner, access, compliance, freshness, and promotion. |

## Freshness and review policy

Freshness describes how recently a source was reviewed for the claim being made;
it does not imply automated synchronization.

| Freshness label | Meaning | Default review expectation | Stale handling |
| --- | --- | --- | --- |
| `current` | Source was reviewed in the current iteration or explicitly remains valid for the target claim. | Cite source path/ID and reviewer or last-updated marker when available. | None. |
| `recent` | Source is from a prior accepted iteration and no later conflicting source is known. | Confirm no downstream decisions supersede it before reuse. | Mark confidence no higher than medium unless reviewer confirms. |
| `stale-risk` | Source predates newer decisions, scope changes, or likely domain changes. | Reviewer or owner must confirm applicability before grounding future behavior. | Record as review-needed or open if unconfirmed. |
| `superseded` | A later accepted artifact or decision replaces the source. | Do not use for grounding except historical trace. | Cite newer source and preserve supersession note if relevant. |
| `unknown` | Review date, owner, or applicability is missing. | Treat as operational or discovery context only. | Assign owner or convert to open question. |

## Confidence labels

| Confidence | Meaning | Typical source basis | Required caveat |
| --- | --- | --- | --- |
| High | Directly supported by an approved source with no known conflicting decision and clear applicability. | P0 approved canonical docs or accepted ADRs. | Cite source and scope. |
| Medium | Supported by approved sources but includes interpretation, dependency, or pending review. | P0/P1 sources with assumptions, deferred decisions, or inferred application. | Mark inference or review need. |
| Low | Plausible but based on stale, operational, seed, or incomplete source context. | P2/P3/P4 sources not yet promoted. | Treat as assumption, validation need, or open question. |
| Blocked | Claim requires unresolved product, architecture, governance, compliance, source, owner, or implementation decision. | Open OAD/OQ, missing owner, missing source, or future-source dependency. | Do not use as committed scope; route to decision/spike. |

## Provenance fields

MVP2 knowledge records, approved extracts, persona guidance, and role-agent task
packets should be able to carry the following logical provenance fields. These
are documentation/data-contract fields, not a physical schema commitment.

| Field | Requirement |
| --- | --- |
| `source_class` | One of the source classes in this inventory. |
| `source_id_or_path` | Canonical path, configuration path, runtime reference, source packet, decision ID, work-item ID, or future external reference. |
| `source_status` | Approved source, approved extract, operational source, seed source, or future candidate source. |
| `evidence_class` | `source-backed`, `inferred`, `assumed`, or `open`, aligned with AI agent standards. |
| `confidence` | High, medium, low, or blocked with rationale. |
| `freshness` | Current, recent, stale-risk, superseded, or unknown. |
| `owner_role` | Role accountable for source correctness or promotion. |
| `reviewer_role` | Role that accepted review-only evidence, when applicable. |
| `applicability` | Workflows, domains, personas, work items, or decisions where the source applies. |
| `limitations` | Known uncertainty, open decisions, stale markers, source gaps, or future-scope exclusions. |
| `promotion_state` | Candidate, proposed, review-needed, approved, operational-only, superseded, or rejected. |

## Source ownership matrix

| Source area | Accountable owner role | Supporting roles | Review or escalation path |
| --- | --- | --- | --- |
| Product and functional requirements | Product owner / requirements owner | Integrator, product reviewer | Product or requirements traceability gate. |
| Architecture, data, and decisions | Architect / data architect | Tech lead, integration architect, security/privacy reviewer | Architecture/technical gate or ADR/OAD update. |
| MVP platform and operations docs | Domain architect / integrator | SRE, QA lead, tech writer | Implementation-readiness or release-operations review. |
| Work items, dependency maps, and roadmap | Backlog owner / dependency analyst / implementation planner | Product owner, integrator, tech lead | Dependency/concurrency and implementation gates. |
| Standards and reusable templates | Standards curator / configuration owner | Orchestrator, QA lead, integrator | Reusable behavior change review. |
| Orchestration configuration and personas | Orchestrator / configuration owner | Standards curator, role owners | Config/doc drift review before promotion. |
| Runtime memos and logs | Producing agent / orchestrator | Integrator, validator owner | Operational handoff; promote material findings through canonical docs. |
| Raw/research seeds | Source owner / integrator | Product owner, architect | Source promotion review; prohibited edit recovery if mutated. |
| External/future sources | Future domain/source owner | Security/privacy, integration architect, data architect | Needs-spike until owner, access, compliance, and promotion rules are accepted. |

## Consumption contract summary

Role agents and personas consuming this inventory must:

- prefer P0 approved canonical docs for source-backed claims;
- use P1 config and input packets to bound workflow, role, and deliverable scope;
- treat P2 runtime evidence as operational until promoted;
- treat P3 raw/research sources as immutable seed context, not implementation
  truth;
- treat P4 external/future sources as discovery or open decision context until
  governed;
- preserve evidence class, confidence, freshness, provenance, and limitations in
  outputs;
- record open questions instead of choosing storage, retrieval, embeddings,
  connectors, tenancy, compliance, providers, access control, or retention;
- route reusable learnings to canonical docs, standards, workflow templates,
  persona guidance, validators, or backlog gates after review.

## MVP2 inventory readiness gates

| Gate | Ready condition | Blocks readiness when |
| --- | --- | --- |
| Source priority gate | P0-P4 source classes are identified and tied to owners. | Source class, owner, or approved/operational posture is unclear. |
| Provenance gate | Claims carry source path/ID, evidence class, confidence, freshness, owner, and limitations. | Claims cannot be traced or conflate approved and operational evidence. |
| Promotion gate | Operational, seed, and future sources have a reviewed path to approved knowledge. | Runtime logs, raw notes, or external sources are treated as durable truth without promotion. |
| Future-scope gate | Runtime knowledge store, retrieval, embeddings, connectors, tenancy, compliance, provider, access-control, and retention remain open/future. | A source rule implies a technology or governance implementation choice. |
| Persona handoff gate | Source inventory can be consumed by role agents/personas without hidden source expansion. | Task packets or persona guidance omit source posture, confidence, freshness, or limitations. |

## Open decisions

| ID | Decision needed | Current MVP2 handling |
| --- | --- | --- |
| OQ-SI-001 | Which non-MVP1 source types must be promoted first after canonical docs and orchestration config? | Treat external docs, tickets, code, chat, incidents, customer corpora, and legacy systems as P4 candidates until prioritized by product/domain decision. |
| OQ-SI-002 | Who are the named source owners and reviewer roles for each source family? | Use role-based owners in this inventory until named people or teams are accepted. |
| OQ-SI-003 | What concrete freshness cadence, expiration policy, retention policy, deletion rule, and stale-source escalation apply? | Use conceptual freshness labels only; keep retention/deletion/compliance implementation open. |
| OQ-SI-004 | What source-access, tenancy, compliance, privacy, and sensitive-data constraints apply to future external sources? | Treat as governance blockers before external source ingestion or connector implementation. |
| OQ-SI-005 | What runtime evidence should be retained, summarized, or discarded after orchestration runs? | Summarize material findings into approved sources; leave retention and storage decisions open. |
| OQ-SI-006 | What knowledge storage, retrieval, search, embeddings, indexing, connector, sync, or provider technology should implement this model? | Future/open; this inventory defines source contracts only. |

## Assumptions

- MVP1 canonical docs, accepted decisions, work items, standards, and
  orchestration configuration are stable enough to seed MVP2 source classes.
- MVP2 source grounding can proceed as documentation and contract work before a
  runtime-backed knowledge system exists.
- Runtime artifacts are useful evidence but are not durable truth unless
  summarized into canonical docs, standards, work items, decisions, or approved
  extracts.
- Human reviewers and SMEs remain accountable for confidence, freshness,
  promotion, and reusable behavior changes.
