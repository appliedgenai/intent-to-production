# Sources and scope

Primary sources reviewed 28 September 2026. The six-layer architecture, worked onboarding example and operating recommendations are the author's synthesis. The numerical examples illustrate arithmetic; no measured employer results are asserted.

| Source | Supports | Boundary |
|---|---|---|
| [AWS AI-DLC](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/) | AI proposals, human validation and the inception/construction/operations framing. | The six layers here are not an AWS-prescribed stack. |
| [Kiro specs](https://kiro.dev/docs/specs/) | Structured requirements, design and implementation tasks. | Generated artifacts still need correct domain decisions. |
| [Backstage catalog](https://backstage.io/docs/features/software-catalog/) | Service metadata and ownership capabilities. | Indexing does not establish source authority or prove consumer completeness. |
| [Bedrock Knowledge Bases](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html) | Managed retrieval capability example. | Permission behavior must be validated against the actual source and integration. |
| [GitHub Copilot cloud agent](https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-cloud-agent) | Coding-agent capability example. | Deployment fit and controls require evaluation. |
| [Temporal](https://docs.temporal.io/) | Durable workflow capability example. | Not every CI task requires durable orchestration. |
| [GitHub environments](https://docs.github.com/en/actions/reference/workflows-and-actions/deployments-and-environments) | Deployment controls. | Availability varies by repository and plan. |
| [OPA](https://www.openpolicyagent.org/docs) | Policy evaluation. | Business policy, enforcement integration and accountability remain enterprise responsibilities. |
| [Promptfoo](https://www.promptfoo.dev/docs/intro/) | Model evaluation/testing capability example. | Deterministic application logic also needs ordinary software tests and domain cases. |
| [Langfuse](https://langfuse.com/docs) | AI observability/evaluation capability example. | A trace store alone is not a complete recordkeeping system. |
| [OpenTelemetry GenAI conventions](https://github.com/open-telemetry/semantic-conventions-genai) | Instrumentation conventions. | Relevant specifications are evolving; pin versions and define business-specific events. |
| [DORA metrics](https://dora.dev/guides/dora-metrics/) | Deployment stability/recovery definitions used in the field guide. | Broader intent and business-outcome measures are separately proposed. |

Product names illustrate capabilities rather than a tested integration or procurement recommendation. Author background is based on the supplied professional history. The repository contains no employer implementation or client records. The worked artifacts are proposed specifications, not executed acceptance evidence.
