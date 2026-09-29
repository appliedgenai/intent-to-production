# Tools and build-versus-buy decisions by layer

[Architecture overview](README.md) · [Full paper](PAPER.md) · [Acceptance exercises](FIELD-GUIDE.md#make-build-versus-buy-a-testable-decision)

Start from the capability and its required behavior. A product may cover several layers; none of the rows requires a new product. These are candidates to evaluate in the intended deployment mode, not a tested bundle.

| Layer | Candidate capabilities and tools | What could justify building or adapting a component? |
|---|---|---|
| **Intent** | Existing Jira, Azure Boards, Linear or GitHub Projects; Kiro specs or Spec Kit for specification work. | Native links cannot preserve work/specification/PR identity and approved status transitions. Build the missing adapter, not another tracker. |
| **Knowledge** | Git and document sources; Backstage catalog; existing search, OpenSearch or pgvector; Neo4j when relationship queries justify it. | Required source semantics, permissions or validated relationships cannot be maintained by available connectors. Domain owners still steward meaning. |
| **Context** | Native code search and repository guidance; LlamaIndex, Neo4j GraphRAG or managed retrieval where needed. | Repeated selection, authorization or freshness failures justify a shared context assembler. Measure omissions and stewardship effort before adding infrastructure. |
| **Execution** | Kiro or an approved coding agent; isolated runners and existing CI. LangGraph or Temporal address different orchestration needs when required. | Required domain tools, cancellation or recovery are unsupported through configuration. An adapter cannot create missing provider guarantees. |
| **Control** | Existing CI/tests and deployment controls; OPA, ArchUnit or Promptfoo for relevant policy, architecture or AI checks. | Domain acceptance cases or binding evidence to the actual release cannot be expressed through current controls. Prompts do not enforce this boundary. |
| **Memory & Evidence** | Git/CI artifacts, incident systems and telemetry; OpenTelemetry conventions and Langfuse for relevant instrumentation and analysis. | Teams cannot correlate a change's decisions and outcomes or promote reviewed learning. Add the missing links and review workflow before replacing storage. |

Keep enterprise identity, secrets, model access, data lifecycle and cost attribution shared where existing services meet the need. Assign an owner to every integration and specify how it handles access changes, failures, duplicate events and recovery.

Compare build and buy against the same [layer-specific acceptance exercises](FIELD-GUIDE.md#make-build-versus-buy-a-testable-decision). Include licenses, integration, source stewardship, review, support and exit costs. Purchasing implementation does not transfer accountability for business rules or release decisions.

The [full paper](PAPER.md#the-six-layer-architecture) explains the boundaries and links to product documentation. The [source register](SOURCES.md) distinguishes documented capabilities from this proposed integration.

