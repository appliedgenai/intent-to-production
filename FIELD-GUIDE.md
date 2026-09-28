# The operating decisions behind AI-DLC

[Executive overview](README.md) · [Full six-layer architecture](PAPER.md) · [Worked example](WORKED-EXAMPLE.md)

This guide explains operating responsibilities, build/buy decisions and measures for the six-layer architecture. ONB-017 supplies one connected example throughout the paper. These are proposed engineering practices, not reported incidents or measured results from an employer.

## People: move judgment to where it can change the result

An agent can draft a requirement, investigate consumers, propose a design and generate tests. The team must make room to answer the questions those activities uncover. Otherwise it has added a faster producer to an unchanged decision queue.

| Decision | Accountable contribution | Observable output |
|---|---|---|
| Which problem deserves solving? | Product owner | Baseline, eligible population and intended benefit. |
| Which exceptions change the meaning of “correct”? | Operations/domain expert | Labeled examples, rule ownership and exception-handling decisions. |
| What existing behavior must survive? | Engineer/service owner | Change-impact map, supported consumer contracts and preservation tests. |
| How may the agent work? | Platform and security owners | Identity, permitted tools, isolated environment and enforced boundaries. |
| What evidence is enough to release? | Service owner with applicable risk partners | Risk-proportionate test/review requirements and a recorded release decision. |
| Did the feature improve work? | Product and operations | Matured-cohort outcome review, costs and unresolved cases. |

For the worked example, bring product, an operations specialist and an engineer together to settle draft versus submission semantics. A short discussion can resolve a question that otherwise produces a wrong implementation, a rejected review and another generation cycle.

Non-coders have a concrete role: supply examples, challenge assumptions and prototype in appropriate environments. That contribution is more useful than requiring them to express everything as elaborate prompts. Engineers retain hands-on system understanding, review responsibility and mentoring; generated code still needs people who can diagnose it.

Plan review capacity explicitly. Limit concurrent agent work by the amount of change the team can evaluate. Measure waiting and active review separately. Idle agent capacity can be cheaper than a growing queue of partially understood changes.

## Process: spend attention on decisions, not document production

1. **Elaborate:** the agent proposes questions and a draft intent. People resolve material ambiguity and approve examples.
2. **Discover:** the agent maps relevant code, sources and consumers. Engineers distinguish observed behavior from desired behavior and investigate gaps.
3. **Design:** agree the change boundary, interfaces, failure states and recovery. Run a spike when an assumption would otherwise determine the architecture.
4. **Construct and challenge:** generate small changes; evaluate against preservation tests and independent domain cases; inspect the actual diff.
5. **Release and learn:** promote a known bundle, operate a controlled cohort and compare the outcome with the baseline. Curate failures into future cases after review and redaction.

These activities overlap and recur. An incident may expose a missing requirement; a design spike may change scope. Scale the process to the work: an API contract change deserves more investigation than a wording correction. AI-DLC should shorten the time from uncertainty to decision, not generate a larger document set for the same approval meeting.

## Patterns with their failure signals

The example's critical decisions have different owners. The domain owner settles whether POL-17@v5 is material and effective for the target cohort. Product approves any changed benefit/scope; engineering reviews impacted behavior and tests; the service owner decides whether REL-42 has sufficient applicable evidence to ship. Platform owners maintain the links and enforcement interfaces; they do not decide the meaning of the document rule.

| Pattern | Tempting anti-pattern | Signal that it is failing | Intervention and cost |
|---|---|---|---|
| Separate preservation tests from acceptance tests | Treat current code as the complete business specification | The new submission rule breaks draft saving, or a legacy defect is faithfully reproduced | Domain owner resolves the difference; requires access to people who understand the workflow. |
| Maintain examples independently of generated code | Ask the same agent to generate implementation, expected answers and the success report | Large passing suite, few edge cases from operations | Add domain cases and held-out checks; maintain their provenance and revisit stale labels. |
| Make missing context explicit | Fill gaps with plausible assumptions or retrieve everything | Review repeatedly discovers unknown callers and conflicting rules | Keep a source/consumer map and unresolved-gap list; accept some discovery work before generation. |
| Review evidence applicability by revision and change type | Reuse old approval for changed behavior, or invalidate every test on any edit | The release claim cannot be matched to its candidate, or harmless changes trigger excessive reruns | Preserve historical results; requalify affected claims and justify retained evidence. Maintain links without assuming complete dependency coverage. |
| Use small changes and review work-in-progress limits | Maximize the number of parallel coding agents | Review age and abandoned changes rise | Reduce inflow and split changes; raw generation utilization may fall. |
| Buy the general coding harness | Build a multi-agent framework before delivering one workflow | Platform work grows while no team has a measured outcome | Start with existing tools and one adapter; custom behavior may initially be less convenient. |
| Reuse stable domain interfaces | Clone prompts, tools and policy logic into each team's harness | Every new use case forks the platform | Consolidate the repeated contract; requires product management for the internal platform. |
| Curate failures into cases | Feed every trace back into agent memory | Sensitive or incorrect material reappears as trusted guidance | Review, redact and label before promotion; learning now has an owner and a cost. |
| Connect delivery observations to product outcomes | Count tokens, suggestions and completed agent runs as ROI | More generated output, unchanged operations backlog | Link release and workflow cohorts; business instrumentation takes additional work. |

## Make build-versus-buy a testable decision

The minimum foundation is the existing tracker, Git repository, approved agent, isolated runner and CI. Each layer requires a build-versus-buy decision: reuse or configure a suitable existing capability, buy a missing capability, or build/adapt a component for a demonstrated gap. Compare these options against the same acceptance exercise. A purchased service can implement an enterprise-owned contract; ownership does not require custom infrastructure.

| Layer | Start by adopting or configuring | Build/integrate when this gap is demonstrated | Acceptance exercise |
|---|---|---|---|
| Intent | Existing tracker plus one specification workflow | Agreed work/spec/release links cannot be maintained reliably | Change scope during a run; preserve the old baseline, record a new decision and prevent stale events from closing the work item. |
| Knowledge | Owned sources, catalog links and existing search | Repeated rule-to-service/consumer/test questions exceed those capabilities | Compare candidate impact paths with reviewed changes; expose missing relationships and measure stewardship effort before adding a graph. |
| Context | Versioned repository packs and native search | Several teams repeat the same access/selection/freshness failures | Revoke source access and simulate an outage; verify the context exposes unavailable evidence and does not leak cached content. |
| Execution | A suitable coding harness and isolated runners | Required domain actions or recovery cannot be supported through available interfaces | Demonstrate scoped credentials, context delivery, cancellation/recovery and export of required evidence in the intended deployment mode. |
| Control | Existing tests, policy checks and release system | Candidate evidence cannot be bound to the actual release | Change the artifact or applicable rule after checks; verify the unsupported release is held and valid history remains intact. |
| Memory & evidence | Git/CI artifacts, existing telemetry and incident systems | Teams cannot reconstruct decisions or reuse reviewed learning | Reconstruct one release, replay a duplicate status event without redeploying, and turn an adjudicated defect into a versioned case. |

For a buy decision, price licenses together with connector upkeep, source stewardship, evaluation maintenance, human review, on-call support and exit/migration work. For a build decision, identify the product owner and support capacity. Prototype success does not establish sustainable total cost.

The most useful integration trial changes a governing rule while work is in flight. Observe whether the selected tools preserve the old context, find known dependents, expose gaps, requalify affected work and block an unsupported release. Test substitution of a coding provider where relevant; do not assume every tool exports equivalent evidence or supports identical controls.

## Agent observability: diagnose the kind of failure

For the development agent, record the task and intent revision, context references, tool invocations, outcomes, retries, timing, usage/cost and handoffs. Link the resulting change to review and evaluation. Use approved redacted content where diagnostic value justifies it; do not capture secrets or hidden model reasoning.

| Symptom | Evidence to inspect | Likely intervention to investigate |
|---|---|---|
| Code follows an obsolete document rule | Context manifest versus authoritative source revision | Source selection/freshness or rule ownership. |
| Agent repeatedly edits the wrong layer | Task scope, code-navigation results and review corrections | Better decomposition, better discovery or narrower tool scope. |
| Correct intent, wrong save/submit behavior | Domain cases, diff and execution path | Implementation fix and regression coverage. |
| Tests pass but consumers reject responses | Consumer inventory and contract-test coverage | Compatibility investigation; generation quality may be irrelevant. |
| Delivery accelerates but operations work increases | Release cohorts, return reasons, handling effort and exception age | Product scope, workflow design or operational readiness. |

These are diagnostic hypotheses, not automatic root-cause classifications. A human owns the investigation. A dashboard should provide an entry point into evidence and a response process.

The delivered onboarding service needs ordinary application and business telemetry even if it has no model at runtime. If AI is part of a later product feature, add runtime retrieval, tool, policy and outcome traces with separate access and retention. Link delivery and operation through the released configuration.

## Metrics: distinguish effort, elapsed time and business effect

Define the unit of comparison before the pilot: the service and a cohort of similarly scoped changes, followed by eligible onboarding submissions. Record sample size, complexity/risk mix, staffing changes and simultaneous process changes. Show distributions as well as averages. Before/after observation alone does not isolate AI's effect.

| Measure | Definition / denominator | Practical interpretation |
|---|---|---|
| Intent-to-production time | Elapsed time from agreed intent to production availability, median and p90 | Includes waiting; report pre-agreement clarification time separately. |
| Review waiting time | Intervals during which a change is ready for review but not actively being reviewed | Identifies a queue; PR-open time is not a reliable substitute without state tracking. |
| Cost per accepted change | Human effort plus agent/tooling and allocated platform cost across all cohort attempts / accepted changes | Includes rejected attempts and rework; allocate unfinished work consistently. |
| Change fail rate | Deployments requiring immediate intervention / deployments | Pair speed with instability; classify failures consistently. |
| Failed deployment recovery time | Time from failed deployment to restored service | Report severity and sample count; a sparse sample cannot support a confident ranking. |
| Avoidable missing-document return rate | Eligible submissions later returned for the agreed missing-document reasons / eligible submissions with a matured outcome window | Exclude unrelated return reasons explicitly, not inconvenient cases. Keep pending outcomes visible. |
| Human minutes per eligible application | Handling, review, exception and rework effort / eligible applications in the same cohort | Reveals whether work moved from advisors to operations. |
| Draft-save success | Successful saves / valid draft-save attempts, segmented by rollout cohort | A preservation guardrail for the failure in the story. |
| Exception backlog and age | Open exceptions; median/p90 age and oldest item | Prevents blocked work from disappearing from the success dashboard. |
| Evidence coverage | Required valid and linked records / expected records under the agreed policy | Missing telemetry is unknown evidence, not success. |

The two deployment measures follow [DORA's definitions](https://dora.dev/guides/dora-metrics/). The other measures here serve this proposal; they are not DORA standards. Continue established deployment frequency, change lead time and deployment rework measures where useful. Avoid comparing individual developers by generated code or agent usage.

### Observe change and revalidation

The change-and-revalidation path needs its own operating signals. Segment by service, change class and observation window; record sample counts and pending work.

| Signal | Definition | Decision it supports |
|---|---|---|
| Time to owned impact review | Source change detected to an accountable reviewer accepting triage; median/p90, plus unassigned count and oldest age | Whether domain/platform staffing can respond before unsupported work progresses. Track known detection lag separately. |
| Candidates held for missing or inapplicable evidence | Unique candidates held for these reasons / candidates submitted for release review in the window | Where linking, source freshness or review capacity causes delay; separate missing, failed and applicability-pending states. |
| Rework from missed dependencies | Reviewed changes with confirmed dependency-omission rework / reviewed changes, plus attributable effort | Whether source/consumer discovery needs improvement; disclose review sampling and avoid assigning every defect to retrieval. |
| Reuse effort for the second team | Human onboarding, domain adaptation and support effort, plus new bespoke interfaces | Whether shared contracts reduce repeated platform work. Business benefit still needs separate evidence. |

Lower hold rates do not prove better controls; holds may have been bypassed. More reruns do not prove higher quality. Pair these signals with escaped defects, workflow outcomes and total effort.

### The arithmetic that exposes the bottleneck

These inputs are illustrative, not measurements or targets. Assume sequential time with no overlapping work:

| Component | Before | After AI assistance |
|---|---:|---:|
| Implementation | 20 hours | 8 hours |
| Review and rework | 10 hours | 10 hours |
| Waiting | 40 hours | 40 hours |
| **Elapsed time** | **70 hours** | **58 hours** |
| **Active human effort** | **30 hours** | **18 hours** |

Coding effort improves 60%; active human effort improves 40%; elapsed time improves about 17%. These are three different quantities. Real work overlaps, so use timestamps for elapsed time rather than adding effort estimates as if they were durations.

At an illustrative $100 per active human hour and $300 incremental agent/tooling cost, direct cost is $3,000 before and $2,100 after, a 30% reduction before shared platform and operating allocations. Waiting time is not charged as labor in this calculation. Its opportunity cost, if relevant, needs a separate model.

None of this establishes a benefit for advisors. That claim requires the workflow measures: returns, handling effort, draft-save success, adoption and exceptions. Set expansion thresholds with owners before examining pilot results, and show the uncertainty. A small pilot with zero severe failures does not establish that severe failures are rare.

## Start small; expand on evidence

**First workflow:** establish the baseline, owners, intent examples, consumers and rule sources. Use the existing repository and CI. Select an agent that fits the environment and review model.

**First release:** demonstrate the known failure case and compatibility checks, bind results to a release, and staff the operational exceptions. Prove recovery for in-flight work before expanding the cohort.

**Second team:** measure onboarding effort, custom adapters, repeated context gaps and support requests. Promote repeated contracts into the platform. Keep one-off domain decisions with the domain.

**Steady operation:** retire obsolete rules, prompts, models, skills, credentials and duplicate paths. A complete lifecycle includes removal; otherwise the ecosystem accumulates contradictory instructions faster than it accumulates useful knowledge.

