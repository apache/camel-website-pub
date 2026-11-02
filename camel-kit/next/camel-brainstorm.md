# camel-brainstorm

`/camel-brainstorm` is the design stage for new integrations. It extracts what it can from the material you supply, asks one question at a time for what is still unresolved, verifies every component in the Camel catalog, and produces the design specification that you approve before anything is planned or generated. Migrations use [`/camel-migrate`](migration.md) instead, which has its own discovery and design contract.

Do not use it for quick property changes, version bumps or a single well-known component addition (edit the file), for Camel questions (`/camel-knowledge`), or when a design already exists (`/camel-plan`). Every other new integration goes through it, however small: short designs are fine, skipped designs are not.

## Invocation modes

Chained

`/camel-brainstorm` without an argument, or through `/camel-start`. Runs interview, design and approval, then invokes `/camel-plan` itself. If no pipeline is active it first asks you to create one with `camel-kit nextId <slug>`.

Standalone

`/camel-brainstorm <pipeline-id>` for a pipeline that has no design yet. Runs the same flow, writes the design to `docs/camel-kit/<pipeline-id>/design-spec.md` and stops.

Amend

`/camel-brainstorm <pipeline-id>` when `design-spec.md` already exists. The skill loads the specification, asks what to change, re-runs the affected parts of the interview and re-verifies changed components, presents the amended specification for approval, overwrites it, marks each existing direct child stale with `camel-kit doc stale` (the implementation plan, and the migration runbook for migration pipelines) and stops.

At start the skill reads `docs/constitution.md` (copying it from the bundled template if it is missing) and `.camel-kit/config.properties` when present.

## The interview

The interview is adaptive, not a fixed questionnaire. The agent analyzes the requirements, examples and other material you provide first and does not ask about facts that are already established; complete material can need no clarification at all. Open points are asked one at a time, never in batches, in three groups:

1.  **Project questions**: name, business purpose, systems landscape, integration goals or flow names.
    
2.  **Per-flow questions**: intent and data, source, transformations, sink and error handling, with field-mapping, multi-path routing and resilience follow-ups only when triggered.
    
3.  **Cross-cutting questions**: performance, security and monitoring when relevant, then remaining constraints and the deliberate scope exclusions. A category that does not apply is recorded as not applicable with the reason.
    

Topics the interview can cover, with example exchanges

Business purpose

"What business problem does this integration solve?" The answer is recorded in the executive summary and guides every later decision.

Systems and endpoints

"Where does data come from, and where does it go?" Sources, destinations, protocols and intermediary systems for enrichment or validation.

Data formats

Input and output formats, schemas, and whether a field-level mapping is needed. For a complex mapping the agent offers DataMapper, which uses inline Groovy when both schemas are absent or the mapping has fewer than 20 leaf fields and XSLT only with at least 20 leaf fields and at least one schema.

Processing requirements

Validations, business rules, calculations and enrichments, and conditional routing when several destinations are named.

Error handling

What happens when a source or a destination is unavailable. The agent offers a dead letter channel, retry with backoff (the recommended default), log and continue, or stop the route, and follows up on a circuit breaker for HTTP sources or sinks, an idempotent consumer for message brokers, and transactions for flows that write to several systems.

Performance and observability

Throughput, latency, metrics, logging and tracing when the project needs them.

Scope boundaries

"Which related capabilities should this iteration not implement, and why?" If nothing is excluded, the design records **None identified** instead of inventing boundaries.

The questions live in the generated interview guide of your agent, for example `.claude/skills/camel-brainstorm/guides/greenfield-interview.md` for Claude Code. You can add project-specific conditional follow-ups there, recording their answers under the cross-cutting section, without adding fixed rounds or changing the specification schema.

## Catalog verification

After the interview and before the design is assembled, the agent selects components through the `camel` MCP server, for the project’s runtime and full platform BOM, and reads the documentation of each candidate. For a requirement such as "connect to Kafka":

1.  It establishes one version binding with a `camel_catalog_components` probe and checks the returned Camel version.
    
2.  Under that binding it searches the component list by category and proposes a component by exact identity; a complete enumeration is required only before an artifact is recorded as not found.
    
3.  It calls `camel_catalog_component_doc` for the syntax and options and `camel_catalog_component_maven` for the runtime-specific coordinates; EIPs, data formats and languages use their own documentation tools.
    
4.  It records the binding and a `VERIFIED` result with tool provenance for each artifact in the **Catalog Verification Evidence** block of section 5.
    

If a requested component does not exist in the complete list, the agent asks for clarification or proposes an alternative from that list; it never writes an unverified name into the design. A detail-call error is not proof of absence. This is Iron Law 1 (see [Iron Laws](pipeline.html#iron-laws)).

## The design specification

After discovery and the Camel version selection, the agent assembles `design-spec.md`:

 
| Section | Content |
| --- | --- |
| Not Doing (and Why) | Unnumbered, at the top: each deliberately excluded capability and its rationale, so later stages treat it as a scope boundary |
| 1\. Executive summary | Business purpose, business value, stakeholders |
| 2\. Systems landscape | Systems, technologies, protocols and source or target roles |
| 3\. Flow designs | One design per named flow: target module, purpose, verified source and sink with their exact options, transformations, error handling, configuration properties and the rationale of each choice |
| 4\. Cross-cutting concerns | Performance, security, monitoring and constraints; when nothing special applies, the standard behaviour is recorded rather than invented |
| 5\. Constitution compliance | How every flow meets the eight rules, plus the catalog verification evidence |
| 6\. Project structure | The runtime-aware project tree: routes, properties, schemas, tests, DataMapper files and the conditional build or Docker files |

A migration design has the same six sections plus **7\. Migration Context**; it includes **Not Doing (and Why)** only when discovery captured explicit exclusions.

Before presenting the specification the agent reviews it for placeholders, contradictions, unverified components and flows that cross a scope boundary. You then approve ("Approved, looks good") or request changes, and the agent revises and presents again. In chained mode the approval invokes `/camel-plan` immediately; the skill never asks you to run it by hand.

## Common patterns

-   **Request-reply.** HTTP in, a database query, the result in the HTTP response: one synchronous flow.
    
-   **Fire-and-forget.** Accept with HTTP 202 and process in the background: two flows joined by an in-memory queue.
    
-   **Multi-system with compensation.** Parallel writes to several systems that must all succeed or be rolled back: several flows coordinated with the Saga pattern.