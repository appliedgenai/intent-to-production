# From Intent to Production

### A Six-Layer Architecture for AI-Driven Software Delivery

Connecting business intent, enterprise knowledge and coding agents to verified releases.

**A six-minute architecture brief · Mohit Mittal · September 2026**

A coding agent can produce working code while missing a business rule or breaking behavior users rely on.

Here, **AI-SDLC** means applying AI across the software development lifecycle. AI helps engineers design, build and verify software; the delivered feature need not use an AI model.

**Buy or reuse coding capabilities. Own the business decisions, context and verification that connect them to production.** Three principles guide this proposal:

- **Make intent testable.** Agree what must change, what must keep working and how success will be checked.
- **Supply current, task-specific knowledge.** Connect specifications and coding agents to the relevant business rules and code, with clear owners and access controls.
- **Release the change the evidence supports.** A completed agent task or passing test suite alone cannot establish readiness.

[Full architecture paper](PAPER.md) · [Worked change](WORKED-EXAMPLE.md) · [Tool choices and build/buy guide](ECOSYSTEM.md)

## 1 · Start with a change that looks right and still fails

An advisor saves a client's incomplete onboarding application as a draft, then submits it when ready. The requested improvement is: **“Catch missing documents before submission.”**

In fictional change **ONB-017**, a coding agent puts the document check in code shared by save and submit. Its tests cover only complete applications. They pass, but incomplete drafts can no longer save.

Operations makes draft preservation an explicit acceptance example; engineering finds the shared code path. The team moves the check to submission and tests both behaviors. **Code and generated tests can share the same mistaken assumption.** Domain examples must establish expected behavior.

## 2 · Give each layer a concrete job

The six layers are this paper's proposed division of responsibilities. They are not six sequential phases or six products to install. Controls and evidence apply throughout.

[![Six-layer delivery architecture maps reusable tools to enterprise-owned interfaces, with control and evidence across all layers](diagrams/six-layer-reference.png)](diagrams/six-layer-reference.png)

*Each layer carries part of the agreed behavior through to release. Select an image for full resolution.*

| Layer | Buy or reuse candidates | Enterprise responsibility in ONB-017 |
|---|---|---|
| **L6 · Intent** | Jira, Azure Boards, Linear or GitHub Projects; Kiro specs or Spec Kit | Agree the outcome and examples: drafts save; incomplete applications cannot submit. |
| **L5 · Knowledge** | Repositories, documents, service catalog, search; Neo4j where justified | Maintain document rules, code ownership and known dependencies. |
| **L4 · Context** | Native search; retrieval tools when needed | Select the relevant rule version, save/submit code and examples for this task; expose missing information. |
| **L3 · Execution** | Approved coding agent and isolated runners | Produce a bounded code change with appropriate permissions and a recovery path. |
| **L2 · Control** | Existing automated tests, security checks and release tools | Verify both new and preserved behavior; enforce access and release conditions. |
| **L1 · Memory & evidence** | Git, artifact stores and telemetry | Link inputs, code, checks and deployment records; review outcomes for future changes. |

**Owning a responsibility does not require building its software from scratch.** Start with existing tools; these candidates are not a tested product bundle.

## 3 · Connect Jira, specifications and context without creating duplicate truth

In this design, **the tracker records priority, owner and delivery status; the maintained specification defines intended behavior; the agent's task list records an attempt to implement it.** These are different records, even when one product hosts several.

Link the work item to the specification, code change, test results and verified deployment. Finishing an agent task cannot mark the feature released; repairing tracker status must not repeat deployment.

[Kiro specs](https://kiro.dev/docs/specs/) and [GitHub Spec Kit](https://github.github.com/spec-kit/reference/agentic-sdd.html) are candidate specification workflows. Choose one approach and maintain agreed behavior alongside code. [Birgitta Böckeler's analysis](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) distinguishes one-time specification work from specifications maintained through later changes.

**Knowledge is the maintained source material; context is the selection supplied for this task.** For ONB-017, that selection includes the applicable document rule, relevant code and save/submit examples, with source revisions, access checks and known gaps.

A knowledge graph can connect rules to services, owners and tests to answer: **“What else could this rule change affect?”** Use it when maintained relationships justify the cost; search and catalog links may suffice. Known paths do not prove every dependency has been found. [Context design](PAPER.md#l4--context-engineering)

## 4 · Keep a passing result attached to what it actually checked

Now imagine the corrected candidate passes the expanded tests under document rule **POL-17 v4**. Before release, the domain owner confirms that **v5 is effective for the planned rollout and adds a required document for those application types**. An application considered complete under v4 may now be incomplete.

[![Illustrative release review keeps the earlier passing result but holds release because the target cohort now requires a changed rule](diagrams/release-evidence.png)](diagrams/release-evidence.png)

*The release owner holds candidate REL-42. The earlier pass remains valid history; it does not establish behavior under the new requirement. This is a hypothetical result, not an executed test.*

Review affected specifications, selected context, code or configuration and tests. Investigate dependency gaps, rerun affected checks and retain other results only where their applicability is justified.

Release authorization must bind to the **exact build and configuration, applicable rules and application types, and required evidence**. Repository and deployment controls enforce that boundary. The example remains held until the missing evidence and authorization are supplied.

## 5 · Fund the interfaces and the people who keep them useful

Product owns the benefit; domain experts own rules and examples; engineers own design and correctness; the platform team owns shared integrations; service owners own release and recovery. Agent concurrency must fit the team's review capacity.

Begin with one change type, connecting the tracker and specification to permitted context, coding work, checks and release records. Compare delivery time, human effort, failures and cost across all attempts, including abandoned work. Separately measure missing-document returns, draft-save success and operations handling time.

After deployment, link observed outcomes to the released version. Turn recurring failures into reviewed rules, tests or guidance—not unfiltered agent memory.

**Expand when a second team can reuse these connections with its own rules and acceptance examples—and demonstrate better delivery without shifting work into review and operations.**

---

## About the author

**Mohit Mittal · Chief Architect**

**The future of AI depends on disciplined engineering.**

Mohit brings 22+ years in enterprise architecture and distributed systems, including production LLM/RAG work at Chegg and governed agent infrastructure and MCP servers in healthcare.

His focus spans RAG, agentic systems and the AI-driven development lifecycle (AI-DLC), with continuous evaluation, enforceable guardrails and agent observability. This paper applies that approach to software delivery for advisor and operations capabilities in regulated financial services.

*Independent architecture proposal. Examples are synthetic; tool combinations are candidates to evaluate.*

[Full paper](PAPER.md) · [Build/buy decisions and operating metrics](FIELD-GUIDE.md) · [Agent authority at runtime](https://github.com/appliedgenai/earned-autonomy) · [CC BY 4.0](LICENSE.md)

