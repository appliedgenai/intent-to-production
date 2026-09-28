# From Intent to Production

### AI-DLC for the codebase you already have

**Mohit Mittal · September 2026 · A six-minute architecture story**

The request sounds small: **“Help advisors catch missing onboarding documents before they submit an application.”**

Give that sentence to a coding agent and it can add required-field validation, tests and a pull request. The tests pass. The implementation is plausible. It can still be wrong: an advisor must be able to save an incomplete draft, existing integrations may use the same endpoint, and “missing” depends on the application type and the current document rules.

The difficult work is deciding which behavior should change, which must survive, and what evidence will distinguish the two.

That is where I would start an **AI-driven development lifecycle (AI-DLC)**. AI investigates, proposes, implements and checks. People resolve business ambiguity and remain accountable for the result. The architecture makes those decisions available to every subsequent step.

My reference points are production LLM/RAG work at Chegg and building governed agent infrastructure and MCP servers in healthcare. The onboarding change below is a worked design, not a claim about an LPL deployment.

## 1. Make the agent expose the missing decisions

Before writing the feature, ask the agent to inspect the relevant code and propose questions. Does validation run on save or submission? Which application types are eligible? Who owns the document rules? What consumes the existing response? What happens if the rule service is unavailable?

Product, an operations specialist and an engineer resolve these together. The result is a short intent contract with examples:

| Situation | Agreed behavior |
|---|---|
| Save an incomplete draft | Save succeeds; missing items remain visible. |
| Submit an eligible application with a required document missing | Submission is blocked with a specific reason. |
| Rules cannot be determined | Preserve the draft and route an owned exception; do not report it as ready. |
| Existing integration uses the service | Preserve its agreed interface, or deliver an explicitly versioned change. |

The operations specialist supplies the awkward cases. The engineer challenges feasibility. The agent turns the agreed examples into proposed tasks and checks. This is a working session with decisions, followed by small implementation cycles.

**The first useful output is a better-defined change.**

## 2. Establish what the existing system actually does

A wiki says the rule is checked at submission. The endpoint may also be used for saving drafts. Reading either source alone is insufficient.

I would have the agent produce a change-impact map: callers, relevant code paths, rule sources, persisted states and tests. Every statement is marked as an observed behavior, an approved requirement or an unresolved assumption. An extracted rule is a hypothesis until its owner confirms whether to preserve it.

Then assemble a bounded context pack: the approved intent, relevant source revisions, API contracts, domain examples and open questions. Keep “the API's unknown consumers” visible as a gap. A larger context window does not establish that a dependency has been found.

This distinction matters: **a characterization test records today's behavior; an acceptance test defines the behavior we want.** They can disagree. A domain decision must resolve the disagreement before an agent changes production behavior.

[![A plausible validation change becomes a dependable release when the team resolves intent, checks existing behavior, and tests the missing case](diagrams/change-journey.png)](diagrams/change-journey.png)

## 3. Build the ecosystem around those decisions

The six layers below make this process repeatable. Each has an output another layer can inspect.

| Layer | Buy or reuse | What the enterprise must own |
|---|---|---|
| **Intent** | Planning and specification tools | The draft-versus-submit decision, acceptance examples and accountable owner. |
| **Knowledge** | Repositories, catalog and search | Authoritative document rules, service ownership and source precedence. |
| **Context** | Retrieval and code-navigation capabilities | A task-specific evidence pack, access filters, source revisions and explicit gaps. |
| **Execution** | Coding agents and isolated runners | Task boundaries, approved adapters and a reviewable change. |
| **Control** | CI, security scanning and evaluation tooling | Independent domain cases, compatibility checks and release conditions. |
| **Evidence** | Git, telemetry and artifact storage | Links from intent to release, operational outcomes and reviewed regression cases. |

For this feature, I would buy the coding harness and use the existing repository and CI. I would begin the context pack as versioned files. A custom assembler becomes worthwhile when multiple teams repeatedly struggle to assemble the same governed evidence. Its value must justify ownership, support and migration cost.

The shared platform supplies identity, model access, tool permissions, isolation and telemetry. Domain teams own the rules and examples. A complete ecosystem is one in which those responsibilities connect; it can start with very few new services. The [architecture guide](ECOSYSTEM.md) makes the interfaces and build/buy decisions explicit.

## 4. Make the change earn its release

Suppose the agent implements validation in a shared save function. Its tests use only complete applications, so they pass.

An independently maintained case tries to save an incomplete draft. It fails immediately. That one case is more valuable than a large generated suite built around the same mistaken assumption as the implementation.

I would split delivery into reviewable changes: establish existing interface behavior; add document assessment without changing submission; introduce the submission gate; then enable it for a controlled cohort. Each change has a reason, a test and a recovery decision. Parallel generation is useful only while reviewers can absorb the output.

If a document rule changes during implementation, record which context packs, cases and pending changes are affected. Previous evaluation evidence needs review against the new rule. Updating the prompt alone leaves the delivery system reasoning from inconsistent versions.

In production, instrument the consequential decision: application category, rule version, missing-document reason, outcome and exception owner, with controlled references to sensitive evidence. Link it to the release. This lets the team distinguish a bad rule, stale context, an implementation defect and a failing dependency. Model latency alone cannot do that.

## 5. Prove that the work improved

Consider an **illustrative** change requiring 20 implementation hours, 10 review/rework hours and 40 waiting hours. AI reduces implementation to eight hours, while the other components stay constant. Coding effort falls 60%; elapsed time falls from 70 to 58 hours—about 17%—under this simplified, sequential model.

That is a useful saving. It is also a reason to inspect the review queue before buying more generation capacity.

Measure delivery time, review waiting and total cost per accepted change alongside failures and rework. Then measure the actual workflow: avoidable missing-document returns per eligible submission, human handling minutes, draft-save success and unresolved exceptions. Faster releases and better onboarding are separate claims, with separate evidence. The [field guide](FIELD-GUIDE.md) defines the denominators and anti-patterns.

## What I would build first

One team. One existing workflow. A versioned intent, a source-and-consumer map, a bounded coding agent, independent cases and a release record linked to operational outcomes.

Then ask a second team to adopt it. Keep the interfaces that transfer; correct the assumptions that do not. That is the point where a useful delivery practice begins to become a platform.

The advisor sees a precise explanation of what is missing and can still save their work. Operations receives fewer avoidable returns. Engineering can explain what changed and why it is safe to expand. **That is the result the lifecycle exists to produce.**

---

[Ecosystem and build/buy decisions](ECOSYSTEM.md) · [Patterns, metrics and operating decisions](FIELD-GUIDE.md) · [Worked intent and evidence pack](WORKED-EXAMPLE.md) · [Sources](SOURCES.md)

The six-layer architecture is my proposal. [AWS's AI-DLC methodology](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) provides the broader inception–construction–operations framing. The example's contracts, timings and rollout choices are illustrative. [CC BY 4.0](LICENSE.md).
