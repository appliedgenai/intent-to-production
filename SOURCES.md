# Primary sources and scope

Primary sources reviewed 28 September 2026. The six-layer architecture, worked onboarding example and operating recommendations are the author's synthesis. The numerical examples illustrate arithmetic; no measured employer results are asserted.

## Architecture research added in this revision

| Source | Contribution | Boundary |
|---|---|---|
| [Birgitta Böckeler: Understanding SDD](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html), 15 Oct 2025 | Spec-first, spec-anchored and spec-as-source; specification overhead. | Published on Martin Fowler's site, authored by Böckeler. Historical product observations are not current feature comparisons. |
| [Böckeler: Context engineering](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html), 5 Feb 2026 | Instructions, guidance, tools, skills and loading mechanisms. | Our context service and authorization model are architectural proposals. |
| [Böckeler: Harness engineering](https://martinfowler.com/articles/harness-engineering.html), 2 Apr 2026 | Guidance and feedback, including computational and model-based checks. | No guarantee of correctness or endorsement of our stack. |
| [Kiro steering](https://kiro.dev/docs/steering/), [hooks](https://kiro.dev/docs/hooks/), [MCP](https://kiro.dev/docs/mcp/) | Reusable guidance, event-triggered commands/prompts and tool/context access. | Capabilities vary by deployment mode; instructions alone are not enforcement. |
| [GitHub Spec Kit reference](https://github.github.com/spec-kit/reference/agentic-sdd.html) | Specification workflow and optional task-to-issue conversion. | The latter requires a GitHub origin and GitHub MCP issue tools; not Jira synchronization. |
| [Jira](https://www.atlassian.com/jira/solutions/planning), [Azure Boards](https://learn.microsoft.com/en-us/azure/devops/boards/get-started/what-is-azure-boards?view=azure-devops), [Linear](https://linear.app/docs), [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects) | Work-management alternatives. | Selection depends on existing processes, reporting and integrations. |
| [Atlassian governed agent loops](https://www.atlassian.com/blog/jira/governed-agent-loops), Sep 2026 | Announced agent capabilities. | Agent loops, Standards and AI Review were described as private early access. |
| [Neo4j GraphRAG](https://neo4j.com/docs/neo4j-graphrag-python/current/user_guide_rag.html) | Vector, hybrid and graph-augmented retrieval. | Ontology, edge validation, freshness and access propagation are enterprise responsibilities. |
| [OpenSearch](https://docs.opensearch.org/latest/vector-search/), [pgvector](https://github.com/pgvector/pgvector), [LlamaIndex](https://developers.llamaindex.ai/python/framework/) | Search, indexing and retrieval primitives. | Tool capability does not prove source authority or correct task context. |
| [LangGraph](https://docs.langchain.com/oss/python/langgraph/overview) | Stateful agent orchestration. | Distinct from Temporal's durable workflow role; neither is mandatory for every team. |
| [ArchUnit](https://www.archunit.org/) | Java architecture constraints expressed as tests. | An example of deterministic checks, not a language-independent policy solution. |

The full paper distinguishes DORA's five defined measures from proposed intent-to-production, context, evidence and business measures. Candidate combinations require integration testing and procurement review.

## Additional primary references

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
