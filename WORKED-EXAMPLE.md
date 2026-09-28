# ONB-017: catch missing documents before submission

[Six-minute architecture brief](README.md) · [Ecosystem](ECOSYSTEM.md) · [Field guide](FIELD-GUIDE.md)

This is a synthetic specification and evidence-pack design. Identifiers below show how artifacts relate; they do not represent an implemented service, executed evaluation or employer incident.

## Intent contract

**Intent:** `ONB-017/v1` · **Tracker:** `CHG-42` · **Specification:** `SP-42@r3` · **Status:** proposed

**Outcome:** reduce avoidable missing-document returns for an explicitly agreed set of onboarding application types, while preserving draft saving and supported integration behavior.

**Owners:** product owns the benefit and eligible population; operations owns document-rule interpretation and exception handling; the service owner owns compatibility, release and recovery. Assign actual people before use.

**Scope:** assess document completeness and gate submission for eligible applications. This is not an identity/fraud determination, approval of an account or investment advice. Existing controls retain their own responsibilities.

**Invariants:** an incomplete draft can be saved; an unavailable or indeterminate rule must not produce “ready”; an existing contract is preserved or explicitly versioned; sensitive document content is not copied to ordinary delivery logs.

## Decisions that must precede the implementation

| ID | Question | Proposed decision | Evidence still required |
|---|---|---|---|
| D-01 | Where is the gate? | At submission; saving a draft remains permitted. | Confirm every save/submit path and shared helper. |
| D-02 | What defines “missing”? | The approved rule revision for an eligible application type. | Domain owner validates rule examples and effective dates. |
| D-03 | What if the rule cannot be read? | Preserve draft; submission remains unresolved and goes to an owned exception. | Operations accepts the queue, response time and recovery process. |
| D-04 | What about existing consumers? | Preserve supported behavior; otherwise version and migrate explicitly. | Consumer inventory and contract tests; unknown consumers remain a release risk. |
| D-05 | What does rollout reversal do? | Return the cohort to its previous supported path. | Demonstrate that in-flight applications and recorded decisions remain interpretable. |

These choices expose the tradeoff: blocking uncertain submissions can protect correctness while increasing operations work. Exception capacity and service availability must be part of the launch decision.

## Acceptance and preservation cases

| Case | Input / operation | Expected result | Source of expectation |
|---|---|---|---|
| A-01 | Incomplete application; save draft | Save succeeds; missing items remain visible. | D-01 and operations example. |
| A-02 | Eligible application; submit; one required item missing | Specific missing-item result; no transition to submitted. | D-02 and approved document rule. |
| A-03 | Eligible application; submit; all required items present | Completeness gate passes; other existing controls still apply. | D-02 plus existing submission contract. |
| A-04 | Rule source unavailable or unrecognized application category | No false “ready”; preserved draft and owned exception. | D-03. |
| A-05 | Supported legacy caller | Agreed status/response semantics preserved or explicit version routing used. | D-04 and consumer contract. |
| A-06 | Rule revision changes after assessment, before submission | Reassess under the applicable rule; do not silently reuse an obsolete readiness result. | Domain decision on rule effective dates. |
| A-07 | Cohort is disabled with requests in progress | In-flight state remains known; route by the documented recovery decision. | D-05. |

**The deliberately bad candidate:** put a blanket “required documents” guard inside a helper shared by save and submit. Tests using only complete applications pass. A-01 exposes the regression. This is an example of a missing expected behavior, not a syntax or model-quality failure.

## Context manifest

```yaml
intent: ONB-017/v1
task: assess-change-impact
environment: isolated-development
sources_required:
  - kind: document-rule
    revision: REQUIRED_BEFORE_EXECUTION
    authority: operations-rule-owner
  - kind: save-and-submit-code
    revision: REQUIRED_COMMIT_SHA
    authority: onboarding-service-owner
  - kind: consumer-contracts
    revision: REQUIRED_BEFORE_EXECUTION
    authority: each-supported-consumer-owner
  - kind: acceptance-cases
    revision: TEST-42/r2
known_gaps:
  - complete-consumer-inventory-not-yet-demonstrated
  - rule-effective-date-semantics-await-domain-confirmation
allowed_work:
  - inspect-approved-source
  - propose-impact-map-and-characterization-tests
blocked_work:
  - approve-release
  - assume-unknown-consumers-do-not-exist
```

The placeholders are intentional. A source's missing revision must be resolved before a decision relies on it. The pack can support discovery while remaining insufficient for release.

## Change decomposition

1. **Preserve:** document callers and establish characterization/consumer tests. Review differences between observed behavior and desired rules.
2. **Assess:** introduce a side-effect-free completeness assessment with explicit rule revision and known/unknown result states.
3. **Gate:** connect assessment to submission, preserving draft saving. Add domain cases and dependency-failure checks.
4. **Roll out:** enable a bounded cohort with an operational owner, monitoring and recovery criteria. Choose numbers from the baseline and risk tolerance; they are not invented here.

This decomposition has a cost: more individual changes and a transitional path. It buys smaller review surfaces and more precise recovery. Avoid leaving the transitional paths indefinitely.

## Release dossier

| Field | Required linkage |
|---|---|
| Intended change | Intent and decision revisions; eligible application types. |
| Built change | Code commit, rule revision, configuration and dependency versions. |
| Development inputs | Agent/tool/model references where available; context manifest and source revisions. |
| Checked behavior | Evaluation run, test-set revision, results and unresolved exceptions. No passing result is asserted by this example. |
| Human decisions | Design/release decision, responsible roles and explicit accepted limitations. |
| Rollout and recovery | Cohort definition, fallback routing, in-flight handling and operational owner. |
| Outcome | Return reasons, draft-save failures, handling effort and exception backlog linked to the release. |

If a new rule revision changes which documents are mandatory, use these links to find affected contexts, tests, pending changes and deployed cohorts. Re-evaluation can then follow known dependencies. Investigate gaps in the map rather than declaring unaffected behavior by default.


## A rule changes before the candidate ships

This is a hypothetical continuation, not an executed test result. Candidate `a71` corrects the save/submit boundary. Evaluation `EVAL-42` is imagined passing the agreed `TEST-42@r2` cases using `POL-17@v4`, `SP-42@r3` and `CTX-42`. Release candidate `REL-42` has not deployed.

The domain owner then makes `POL-17@v5` effective for the intended cohort, adding a required document. Preserve EVAL-42 as a historical result; its current applicability is insufficient for the changed requirement. Hold REL-42 until the affected spec/context/tests and candidate behavior are reviewed and requalified. A graph or ordinary relationship table helps locate known dependents; neither proves that unrecorded consumers do not exist.

The proposed replacement records are `SP-42@r4`, `CTX-43`, `TEST-43@r3` and `EVAL-43`; these are pending artifacts, not implied passing results. Change code/configuration if the rule requires it. Retain unaffected evidence with a documented basis and bind the final decision to the exact release bundle. Do not overwrite EVAL-42 or automatically restart deployment because tracker synchronization failed.

See the [structured change manifest](examples/change-manifest.json), [revalidation scenarios](examples/revalidation-cases.json) and [release applicability discussion](PAPER.md#a-passing-evaluation-is-a-claim-about-a-particular-candidate).
