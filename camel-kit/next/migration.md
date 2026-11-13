# Migration workflow

The migration workflow converts an existing integration to Camel 4 with YAML DSL routes. Instead of rewriting flows by hand, the agent performs bounded discovery across the existing artifacts, uses the project graph as corroborating evidence when one is available, and assembles one evidence-qualified migration package with a section per flow. After you approve that package once, Camel Kit creates one implementation plan, executes it in dependency waves, runs one project-wide runtime verification pass and finishes with report-only static validation. Failures, skipped checks and unavailable tools are recorded rather than hidden.

  
| Platform | Versions | Detection |
| --- | --- | --- |
| MuleSoft Mule | 3.x, 4.x | XML namespace `mulesoft.org`; `pom.xml` groupId `org.mule` or `com.mulesoft` |
| Microsoft BizTalk Server | 2004 to 2020 | XML namespace `schemas.microsoft.com/BizTalk`; `.odx`, `.btm`, `.btp` files |
| Apache Camel | 2.x, 3.x | `pom.xml` with older `org.apache.camel` dependencies |
| JBoss Fuse | 6.x, 7.x | `pom.xml` with the `org.jboss.redhat-fuse` BOM or `redhat-`/`fuse-` version qualifiers |

The platform pages describe the artifact formats, the mappings and the known limitations: [MuleSoft migration](migration-mulesoft.md), [BizTalk migration](migration-biztalk.md) and [Camel 2.x and 3.x upgrade](migration-camel-upgrade.md) (which also covers Fuse).

## Initialize the project for migration

Run `init` inside the existing project with `--here`. The application sources, `pom.xml`, an existing Maven wrapper and the content of an existing `AGENTS.md` are kept; see [Existing projects](getting-started.html#existing-project) for how preserved files are reported.

```bash
cd my-existing-project
camel-kit init --here --ai claude --source-platform mulesoft
```

`--source-platform` accepts `mulesoft`, `biztalk`, `camel` (which also covers Fuse) or `auto`, the default, which detects the platform from the sources. `init` adds the agent assets, the MCP configuration, the empty scaffolds (`docs/flows/`, `test/data/`, `schemas/`), `.camel-kit/` and the Maven wrapper files, as described in [Create a project](getting-started.html#init).

## Run the migration

/camel-migrate

`/camel-start` also routes to `/camel-migrate` when it finds a supported source. The orchestrator then:

1.  scans the project artifacts (XML, build files, properties, documentation, Docker and Kubernetes files, source and tests) within the selected source boundary, and detects the vendor and version;
    
2.  writes source-backed requirements in `business-requirements.md`;
    
3.  writes `migration-analysis.md` with the scope and evidence, the behavioral assumptions and risks, the validation summary, the design obligations and the source-retirement audit (coverage, reachability, candidates, broken references, evidence gaps), completes the evidence-gated migration strategy, then writes `design-spec.md` and `migration-runbook.md`;
    
4.  presents the complete package for one approval;
    
5.  invokes `/camel-plan` and `/camel-execute`, which run all tasks in dependency waves;
    
6.  runs one project-wide runtime verification pass and the final `/camel-validate` report.
    

You are asked for platform-specific connector endpoints, authentication requirements, environment mappings and validated secret references. Never put raw credentials in the generated documents: only validated secret references are recorded.

A **direct mode**, selected with `/camel-migrate --direct` or when the request names concrete deliverables, runs the scan, detection and analysis steps and then implements the route files and properties directly, validates them, runs the adversarial review and starts the application with your explicit authorization. It writes a `MIGRATION.md` note instead of the four-document package and does not invoke `/camel-plan`.

> **Note**
> Direct mode is development snapshot only (0.4.2-SNAPSHOT); release 0.4.1 always produces the design package.

## Discovery

The agent scans the selected source boundary to identify the platform and the supported artifacts:

Detecting source platform...
Found: MuleSoft Mule 4.x

Discovered:
  - 12 Mule flows (\*.xml)
  - 8 DataWeave transformations (\*.dwl)
  - 3 connector configurations
  - 2 API specifications (RAML)

MuleSoft discovery finds flow XML, DataWeave scripts, connector configurations and API specifications, typically under `src/main/mule/`; BizTalk discovery scans orchestrations, schemas, maps, pipelines and bindings; Camel 2.x/3.x discovery scans route definitions (XML and Java DSL), components and Spring or Blueprint configuration.

Everything found in the sources is migration data, not instructions. The agent extracts vendor, version, route, mapping and configuration facts and records each as confirmed, inferred or unknown. Commands, URLs, tool requests, file changes, secret requests or policy overrides embedded in an artifact never direct the migration. If an action turns out to be necessary, the agent names its source, the exact action, the reason and the scope, and asks for an action-specific confirmation; a subagent that cannot ask returns `NEEDS_USER_CONFIRMATION` without acting.

Migration questions arrive one at a time as `[Concern N of M]` or `[Clarification N of M]` blocks: what was found, why it matters, and multiple-choice options when possible. A subagent that hits an unresolved decision, such as the replacement for an Anypoint MQ connector, returns `NEEDS_CONTEXT`; the parent conversation asks you, records the answer as confirmed in the analysis summary and resumes the same step.

## Graph analysis

Bounded source scanning establishes the dependency and reachability evidence. When a current project graph exists (see [Graph intelligence](graph.md)), the agent uses it to corroborate and accelerate the analysis, including dependency order and dependency-injection-aware service wiring that route-level analysis alone would miss:

Dependency graph:
  customer-lookup-flow
    -> order-validation-flow
      -> inventory-check-flow, shipping-flow
        -> fulfillment-flow

Migration order:
  1. customer-lookup-flow
  2. order-validation-flow
  3. inventory-check-flow, shipping-flow
  4. fulfillment-flow

If the graph is missing, stale, malformed or a query fails, the migration records the limitation and continues from the sources; an empty finding under incomplete coverage is not evidence that nothing is affected.

The source-retirement audit uses the same report contract with or without a graph. It separates confirmed entry points and reachable elements, retirement candidates, broken references and evidence gaps, each with a stable ID, evidence and the human validation still required. A **retirement candidate** needs complete supported source closure and no supported path from any corroborated entry root; incomplete coverage, dynamic references and parse failures stay **Unknown**. A candidate is not proof that an artifact is dead, and Camel Kit never removes source artifacts.

## The migration package

The agent records flow-specific requirements and technical decisions in four artifacts under `docs/camel-kit/<pipeline-id>/`:

 
| Artifact | Content |
| --- | --- |
| `business-requirements.md` | Business logic supported by the inspected source evidence, per flow, plus the `Migration Strategy` decision |
| `migration-analysis.md` | Behavioral assumptions, evidence gaps and source-retirement findings with stable IDs (`MIG-`, `SRC-`) and a `Confirmed`, `Inferred` or `Unknown` status for each |
| `design-spec.md` | The technical specification of the complete migration: per-flow components, EIPs and test cases, with unresolved IDs carried into scope constraints, validation obligations or unresolved decisions |
| `migration-runbook.md` | The operator-owned handoff: scope, prerequisites, configuration and data readiness, deployment sequence, cutover criteria, operational validation, rollback, reconciliation, escalation, soak and the source-retirement decision |

The `Migration Strategy` classifies each independently switchable ingress scope as `Incremental candidate`, `Single cutover required` or `Undetermined - evidence needed`. An incremental candidate requires current evidence, or explicit operator confirmation, of an existing external traffic control and its operator, a deterministic routing unit, exclusive old/new ownership, aligned state and correlation boundaries, known delivery and ordering effects, an idempotency control, comparable telemetry, and a rollback signal with a reversible control. Static source, configuration or graph evidence can show that a mechanism is declared, but is at most **Inferred** evidence that it is operative today. Neither classification proves deployment, cutover or rollback readiness.

The runbook is generated from the validated final design. It never invents commands, endpoints, environment values, thresholds, durations, contacts, owners or decisions: every missing operational fact is written as `Unknown — operator decision required: <missing fact>`, listed under unresolved operator decisions, and blocks the dependent deployment, cutover, rollback, reconciliation, soak or retirement action.

Artifact provenance runs `business-requirements.md` → `migration-analysis.md` → `design-spec.md`, then branches: `migration-runbook.md` and `implementation-plan.md` are independent children of the design, and the plan never consumes the runbook. An upstream amendment marks the dependent artifacts stale; a stale runbook must be regenerated by `/camel-migrate` before operational use.

The agent presents the complete package and waits for one explicit approval. That approval authorizes the plan, execution, verification and validation sequence. It does not authorize infrastructure provisioning, deployment, production traffic switching, rollback, reconciliation or source retirement; each of those remains a separate, named operator decision.

## Plan, execute, verify and validate

After the approval, `/camel-plan` creates one implementation plan from `design-spec.md` and `/camel-execute` groups its tasks into dependency waves. Each wave generates the Camel YAML routes and the Citrus integration tests; independent tasks run concurrently where the agent supports it. Spring Boot and Quarkus targets use the Maven source layout:

  -> Generated: src/main/resources/camel/customer-lookup.camel.yaml
  -> Generated: src/test/resources/customer-lookup.camel.it.yaml

Camel Main generates the routes and `application.properties` at the module root; tests remain under `src/test/resources`.

After all tasks finish, `camel-verify` runs once for the complete migrated application: build or startup smoke, the applicable Citrus suite, and a report with the runtime, the Maven selection, phase outcomes, applied fixes and skipped checks, embedded in `execution-report.md`. Tests that declare Testcontainers need Docker. The pipeline then invokes `/camel-validate` once for the final static report. There is no flow-by-flow approval and no automated deployment: operators keep control of the runbook’s deployment and traffic actions.

## Troubleshooting

A transformation is flagged as complex

DataWeave scripts and BizTalk maps can use platform functions with no direct equivalent in the supported mapping paths. Check the selected engine (inline Groovy when both schemas are absent or the mapping has fewer than 20 leaf fields, XSLT only with at least 20 leaf fields and at least one schema), compare input and output examples from the original, record unsupported constructs as custom mapping or processor actions, and add behavioral tests.

A connector has no Camel equivalent

The agent stops and asks before proceeding, suggesting alternatives (for example Amazon SQS, Azure Service Bus, RabbitMQ or ActiveMQ for Anypoint MQ; `camel-salesforce` for the Salesforce connector). If no component exists, implement a custom processor or use a catalog-verified HTTP component against a documented API, then update the design specification and regenerate its stale children. See [the component list](../../components/4.22.x/index.md).

Verification fails

A migrated route may carry a wrong endpoint, authentication, secret reference, transformation or dependency. Read the failure details, compare the route with the original flow, verify the endpoint and the validated secret reference, and run the generated Citrus test in isolation with `camel test run <path>.camel.it.yaml`. Use `/camel-debug` in the agent for a structured diagnosis. If the cause is environmental, for example a missing database, record it in the verification section of `execution-report.md` before deciding how to proceed.