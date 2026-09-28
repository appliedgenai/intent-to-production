# From Intent to Production

### Six layers that keep business intent, enterprise knowledge and release evidence connected

**A six-minute architecture brief · Mohit Mittal · September 2026**

**Buy or reuse the coding agent. Own the context, domain decisions and verification that make its changes fit your business.** The investment is a reusable delivery system: six logical layers connecting the work item to an accepted production change, with explicit owners and evidence at each boundary.

[Full architecture paper](PAPER.md) · [Worked change](WORKED-EXAMPLE.md) · [Sources](SOURCES.md)

## 1 · Start with a change that looks right and still fails

“Catch missing documents before an advisor submits an application.” In synthetic change **ONB-017**, an agent adds a validation guard to a helper shared by save and submit. Its generated tests use complete applications. All pass; incomplete drafts can no longer save.

The missing decision was **what must change and what must survive**. Operations supplies the incomplete-draft example; engineering identifies the shared path. The approved behavior is now precise: preserve draft saving; check completeness at submission.

This example tests the architecture. The product feature itself needs no runtime LLM.

## 2 · Give each layer a concrete job

[![Six-layer delivery architecture maps reusable tools to enterprise-owned interfaces, with control and evidence across all layers](diagrams/six-layer-reference.png)](diagrams/six-layer-reference.png)

The layers are responsibilities, not six sequential phases or six new services. Products can span layers. For ONB-017:

| Layer | Buy or reuse | What the enterprise owns |
|---|---|---|
| **L6 · Intent** | Jira, Boards, Linear or Projects; Kiro specs **or** Spec Kit | Outcome, save/submit examples, decisions and links between work item, spec and PR. |
| **L5 · Knowledge** | Git/docs, catalog, search; Neo4j where useful | Authoritative rule, supported consumers, owners and maintained relationships. |
| **L4 · Context** | Native search; retrieval frameworks when needed | Task-specific evidence, current revisions, access checks and visible gaps. |
| **L3 · Execution** | Approved coding agent and isolated runners | Domain adapters, bounded changes, environment permissions and recovery. |
| **L2 · Control** | Existing CI, tests, security and release tools | Preservation cases, consumer contracts, architecture checks and release criteria. |
| **L1 · Memory & evidence** | Git/artifact stores and telemetry | Which inputs were checked, which bundle shipped, observed outcomes and reviewed learning. |

Start with the tracker, repository, agent and CI already in use. Build missing interfaces only after demonstrating the gap. Owning an interface does not mean writing every component.

## 3 · Connect Jira, specifications and context without creating duplicate truth

In this design, **Jira owns the commitment; the versioned specification defines intended behavior; the run records an execution attempt.** Completed agent tasks cannot declare a release. Verified delivery events update the tracker; synchronization failures have a repair queue.

[Kiro's specs](https://kiro.dev/docs/specs/) and [GitHub Spec Kit](https://github.github.com/spec-kit/reference/agentic-sdd.html) are alternative ways to structure specification work. Choose a primary approach, with a clear rule for maintaining it alongside code. This follows the distinction between spec-first and maintained, spec-anchored development in [Birgitta Böckeler's analysis on Martin Fowler's site](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html).

**Knowledge persists; context is selected for a decision.** A graph can relate a rule to requirements, services, consumers, owners and tests. Search supplies the rule text; traversal supplies known dependency paths. Neither proves the inventory complete. Native code search may find the shared helper; a graph earns its cost when maintained relationships support repeated cross-system impact questions.

The context pack records selected source revisions, permissions and unresolved gaps. A discovery task can proceed with known unknowns; a release cannot rely on missing required evidence. [Knowledge-to-context design](PAPER.md#l4--context-engineering)

## 4 · Keep a passing result attached to what it actually checked

After correcting the save/submit boundary, imagine the candidate passes the agreed cases under rule **POL-17 v4**. Before release, the domain owner makes **v5** applicable to the target cohort, changing its document requirement.

[![Illustrative release review keeps the earlier passing result but holds release because the target cohort now requires a changed rule](diagrams/release-evidence.png)](diagrams/release-evidence.png)

The old result remains valid history. It does not establish readiness under v5. Follow the recorded relationships to affected specifications, context, behavior and tests; investigate mapping gaps; rerun affected checks and refresh the release decision. Preserve unaffected evidence when its applicability is justified.

**This is the practical value of the architecture:** a rule change produces owned engineering work rather than an unexplained green dashboard. Instructions and hooks accelerate feedback; repository, environment and destination controls enforce the release boundary.

## 5 · Fund the interfaces and the people who keep them useful

Product owns the benefit; domain experts own meanings and difficult examples; engineers own design and merged correctness; the platform team owns shared access, execution and evidence interfaces; service owners own release and recovery. Limit parallel agent work to available review capacity.

Start with one change class. Measure delivery time **and** human effort, review queues, change failures and total cost across all attempts. Measure the business result separately: missing-document returns, draft-save success, handling minutes and exceptions.

Promote repeated failures into reviewed specifications, sources, tests or skills. Raw traces do not become trusted knowledge automatically. A model upgrade does not, by itself, invalidate unchanged deterministic application tests.

**The expansion decision:** can a second team use the same interfaces with its own domain rules and acceptance cases, while improving delivery without shifting cost into review and operations? That is stronger evidence of a platform than more generated code.

---

**Author:** Mohit Mittal, Chief Architect, with 22+ years in enterprise architecture and distributed systems, including production LLM/RAG work at Chegg and governed agent infrastructure and MCP servers in healthcare. ONB-017 and its release review are synthetic designs, not employer incidents or measured results.

[Full paper](PAPER.md) · [Build/buy decisions and operating metrics](FIELD-GUIDE.md) · [Agent authority at runtime](https://github.com/appliedgenai/earned-autonomy) · [CC BY 4.0](LICENSE.md)

