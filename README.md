# Six Layers for Intent-Driven AI Delivery

### How Jira, specifications, enterprise knowledge and coding agents become one delivery system

**A six-minute architecture brief · Mohit Mittal · September 2026**

**Buy a suitable coding harness; own the enterprise context, domain interfaces and evidence that turn a requirement into a verified release.** This paper defines six layers for that investment decision, maps tools to each, and shows how they connect.

[Read the full architecture paper](PAPER.md) · [Research and sources](SOURCES.md)

## The problem a coding assistant does not solve

A feature starts in Jira. Its business rules live in documents. Its dependencies live in code and people's heads. The agent receives a fraction of that context, generates a plausible implementation, and hands it to reviewers who must reconstruct what matters.

The architecture connects **what we intended, what we knew, what we changed and how we verified it**.

## The six-layer architecture

[![Six-layer architecture showing concrete tools, owned interfaces and the learning loop](diagrams/six-layer-reference.png)](diagrams/six-layer-reference.png)

*Logical responsibilities, not sequential phases. Products can span layers. Tool names are candidate capabilities, not a mandatory shopping list. Open the diagram for full resolution.*

| Layer | Tools to evaluate or reuse | Enterprise responsibility |
|---|---|---|
| **L6 Intent** | Jira / Boards / Linear / Projects; Kiro specs **or** Spec Kit. | Outcomes, examples and work/spec/PR links. |
| **L5 Knowledge** | Git/docs, Backstage, OpenSearch / pgvector; Neo4j when justified. | Ontology, source ownership, freshness and access. |
| **L4 Context** | Native search; LlamaIndex / GraphRAG / managed retrieval where needed. | Authorized selection, provenance and gaps. |
| **L3 Execution** | Kiro / approved agent, runners; orchestration where needed. | Domain adapters, isolation, budgets and escalation. |
| **L2 Control** | CI/tests, OPA, ArchUnit, security and applicable AI evaluations. | Domain cases, policy, reviews and release criteria. |
| **L1 Memory & Evidence** | Git/artifact stores, telemetry, OpenTelemetry / Langfuse. | Correlation, retention and curated learning. |

## Three boundaries make the architecture work

**1. Jira manages the commitment; specifications define the behavior.** Keep the established tracker. Put detailed requirements, design and acceptance examples in versioned artifacts. Kiro and Spec Kit offer specification workflows; choose a primary approach for the team. Agent steps remain execution state. Link these records through IDs, and let verified workflow events update status. “Task checked” must not mean “feature released.”

**2. Knowledge is durable; context is selected.** A knowledge graph can connect policies, capabilities, services, APIs, owners and tests. Search retrieves relevant passages; graph traversal follows known relationships. A context assembler selects authorized, current evidence for a specific task. It should expose gaps and provenance. Connecting every document to an agent is not context engineering.

**3. Instructions guide; controls enforce.** Steering files and skills help the agent work. Repository protections, environment permissions, destination authorization and release gates establish boundaries. Generated tests can reproduce a generated implementation's mistaken assumptions; domain examples and independently maintained checks matter.

The specification distinction draws on [Birgitta Böckeler's SDD analysis on Martin Fowler's site](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) and [Kiro's workflow](https://kiro.dev/docs/specs/). The six layers and integration boundaries are my synthesis; the full paper explains their sources and contracts.

## What to build, and what to buy

Buy or reuse broad capabilities: tracking, coding agents, retrieval engines, runners, policy engines and telemetry. Own the business meanings and the interfaces between them: source precedence, context assembly, domain tool contracts, acceptance cases and the evidence that connects a work item to a release.

For a Jira/GitHub organization, begin with those platforms, one approved specification workflow, an approved agent and existing CI. Add a bounded knowledge domain. Introduce a graph when relationship queries justify its maintenance cost. Introduce a shared context service when several teams need the same assembly and access rules.

Product owns the outcome; domain experts supply meaning and difficult cases; engineers own design and merged correctness; the platform team owns shared interfaces; service owners own release and recovery. A tool purchase cannot assign these responsibilities.

## How to tell whether it works

Compare similar changes and include abandoned attempts. Measure intent-to-production time, review waiting time, change failures, rework and **total cost per accepted change**, including human correction and platform costs. Inspect context freshness, missing evidence and access failures. Measure the delivered business outcome separately.

The adoption test is a second team delivering through the same interfaces without copying a bespoke harness or rebuilding an evidence pipeline. Faster code generation helps; reusable delivery capability is the larger result.

---

Explore the [full paper and integration contracts](PAPER.md), [operating field guide](FIELD-GUIDE.md) or [optional worked example](WORKED-EXAMPLE.md).

**About the author:** Mohit Mittal is a Chief Architect with 22+ years in enterprise architecture and distributed systems, including production LLM/RAG work at Chegg and governed agent infrastructure and MCP servers in healthcare. This is an independent architecture proposal; tool combinations are candidates to evaluate.

[Separate paper: agent authority in regulated workflows](https://github.com/appliedgenai/earned-autonomy) · [Sources](SOURCES.md) · [CC BY 4.0](LICENSE.md)
