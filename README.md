# From Intent to Production

### A Six-Layer Architecture for AI-Driven Software Delivery

A leader’s guide to connecting intent, knowledge, AI-assisted work and verified releases.

**A six-minute guided overview · Mohit Mittal · September 2026**

An enterprise can give teams AI coding tools and still struggle to turn a business request into a reliable production change. If requirements, domain rules, code and release decisions are disconnected, faster implementation can move work into clarification, review and recovery.

**The AI-driven development lifecycle (AI-DLC) needs a delivery architecture around the agent.** This paper organizes it into six responsibilities: **Intent, Knowledge, Context, Execution, Control, and Memory & Evidence.** Together they connect what the business wants, what the team and agent need to know, what they produce and the evidence for releasing it.

For a leader, the decision is where to reuse existing capabilities, buy missing ones or build justified integrations—and who will operate them. The aim is shorter delivery time and less total effort while preserving quality, measured across the whole change.

**An AI-native software factory is that repeatable delivery system with a reviewed learning loop.** Findings from delivery and production become approved updates to specifications, knowledge, context and checks. Each new change can use those improvements; better results must still be demonstrated.

<a id="1--start-with-a-change-that-looks-right-and-still-fails"></a>

## 1 · Connect six responsibilities around every change

[![Six responsibilities connect agreed intent and enterprise knowledge to task context, AI-assisted work, verification and release; reviewed outcomes improve future work](diagrams/connected-delivery.png)](diagrams/connected-delivery.png)

*Logical responsibilities, not six sequential phases or six mandatory products. Control and evidence apply throughout. Select a diagram for full resolution.*

<a id="2--give-each-layer-a-concrete-job"></a>

**L6 · Intent — agree the outcome and expected behavior.** Product, domain experts and engineering maintain a specification with acceptance examples. Jira or another tracker records priority and commitment; the specification defines the behavior to deliver.

**L5 · Knowledge — maintain authoritative sources and relationships.** Domain owners steward rules, code, interfaces and ownership records. Search and catalog links may suffice. Add a knowledge graph when recurring dependency questions justify maintaining its relationships and provenance.

**L4 · Context — select what this task may use.** Design, implementation and verification need different inputs. Select relevant, permitted source revisions; expose conflicts and gaps. Required missing information pauses affected work. A knowledge store alone does not perform this selection.

**L3 · Execution — perform bounded development work.** Agents can draft requirements, explore designs, implement changes or assist review. Their harness—the software managing model calls, tools and run state—needs scoped access, isolation and stopping rules. Engineers own the resulting change.

**L2 · Control — constrain actions and verify results.** Apply access controls throughout. Evaluate candidates against domain-owned cases, ordinary software tests and security checks. Required evidence and authorization govern release; an agent's completed task does not.

**L1 · Memory & Evidence — retain decisions and review outcomes.** Link sources, specifications, runs, checks and releases. Record concise rationale, owners and outcomes. Service and domain owners review this experience before promoting reusable guidance into knowledge, context or tests.

<a id="3--connect-jira-specifications-and-context-without-creating-duplicate-truth"></a>

## 2 · Make a build-versus-buy decision at every layer

[![Build-versus-buy map pairs candidate tools with gaps that may justify custom components; enterprise accountability remains in either choice](diagrams/six-layer-reference.png)](diagrams/six-layer-reference.png)

Reuse or buy capabilities that meet the need; build missing components when the gap justifies their lifecycle cost. Buying implementation leaves the enterprise accountable for business meaning, access, acceptance and release decisions.

For a team already using Jira, Git and CI, start by linking its work item, maintained specification, agent attempt and release evidence. Buy an execution capability that fits the environment. Fund a custom adapter only where supported interfaces fail the required contract. Include source stewardship, review, integration support and recovery in both options' costs.

[Kiro specs](https://kiro.dev/docs/specs/) and [GitHub Spec Kit](https://github.github.com/spec-kit/reference/agentic-sdd.html) are specification options. [Birgitta Böckeler's analysis](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) examines their differing approaches. The six-layer integration here is an independent proposal. [Tools and decision tests by layer](ECOSYSTEM.md)

<a id="4--keep-a-passing-result-attached-to-what-it-actually-checked"></a>

## 3 · Test the connections with one change

Consider a fictional onboarding request: **reduce applications returned for missing documents while preserving the ability to save unfinished drafts.**

Intent records both behaviors. Knowledge supplies the applicable document rule and code; context selects them for implementation. The agent proposes a change. An independent control catches a document check incorrectly placed in shared save/submit code. Engineering confines it to submission and verifies both behaviors. Evidence links the corrected candidate to the specification and rule version.

In this hypothetical sequence, the agreed checks pass; then a revised rule becomes effective before release and requires another document. The domain owner confirms applicability; engineering uses the links to investigate affected code and checks. Keep earlier results as history, rerun affected checks and justify evidence reused. Hold release until required evidence and authorization cover the exact build, configuration and applicable rule.

This exercises the architecture's connections. A graph may help locate known dependencies; it cannot prove the map is complete. [Detailed records and failure cases](WORKED-EXAMPLE.md)

<a id="5--fund-the-interfaces-and-the-people-who-keep-them-useful"></a>

## 4 · Operate the factory and improve it

When review or production exposes a failure, identify whether its cause lies in the specification, source selection, implementation or checks. An owner reviews, versions and evaluates the correction before reuse, retaining a rollback path. Compare recurrence and rework across similar changes. Raw traces do not become trusted knowledge automatically.

Product owns benefit; domain experts own rules; engineers own correctness; platform teams own shared connections; service owners own release and recovery. Review capacity limits useful agent concurrency.

Start with one change type using existing platforms. Test missing context, changed rules and recovery. Compare delivery time, total human effort, failure rates and cost per accepted change across all attempts. Separately measure the business outcome. Expand when a second team can reuse the interfaces with its own rules and demonstrate value without shifting effort into review or operations.

[Full architecture paper](PAPER.md) · [Patterns, tradeoffs and metric definitions](FIELD-GUIDE.md) · [Sources](SOURCES.md)

---

## About the author

**Mohit Mittal · Chief Architect · 22+ years**

**The future of AI depends on disciplined engineering.**

Mohit's experience includes production LLM/RAG at Chegg and target-state architecture for an AI-native healthcare platform. His work spans agentic AI, AI-assisted development frameworks, evaluation, guardrails and observability.

*Independent architecture proposal. Examples are synthetic; tool combinations require evaluation.*

[Agent authority at runtime](https://github.com/appliedgenai/earned-autonomy) · [CC BY 4.0](LICENSE.md)
