# Greenfield workflow

The greenfield workflow takes a new integration from requirements to generated routes, tests and runtime verification evidence. The agent runs a structured interview, writes a design specification that you approve, decomposes it into tasks, generates the implementation and reports which runtime checks passed, failed or could not run. The design approval is the only human gate: planning, execution and the final static validation proceed under it.

This page follows one example, an order processing integration, through the four stages. See [Stages, approval gate and Iron Laws](pipeline.md) for the stage contracts and [Command reference](commands.md) for every option.

## Initialize the project

```bash
camel-kit init order-processing --ai claude
cd order-processing
```

The agent now has the Camel Kit skills and the MCP servers (two by default; three with `--with-citrus-mcp`). The first pipeline run needs an active pipeline ID, which `init` does not create; `/camel-brainstorm` asks you to create it when none exists:

```bash
camel-kit nextId order-processing
# Output: 001-order-processing
```

## Design interview (`/camel-brainstorm`)

Start the interview with `/camel-start` (which routes new work to brainstorm) or directly with `/camel-brainstorm`. The agent first analyzes any requirements, examples or other project material you provide and does not ask again for facts that are already resolved; complete material can need no clarification at all. Open questions are asked one at a time, in three groups:

-   **Project questions** establish the name, the business purpose, the systems landscape and the integration goals or flow names.
    
-   **Per-flow questions** cover each flow’s intent and data, source, transformations, sink and error handling, with field-mapping, routing and resilience follow-ups only when needed.
    
-   **Cross-cutting questions** cover performance, security, monitoring, remaining constraints and deliberate scope exclusions; a category that does not apply is recorded with a rationale.
    

Example exchanges from the interview

Agent: What business problem does this integration solve?
You:   Process incoming orders from an HTTP API, validate them, enrich them with
       customer data and send them to the fulfillment system.

Agent: Where does the data come from and where does it go?
You:   Orders arrive as JSON on POST /api/orders. Customer data is in PostgreSQL.
       Validated orders go to the Kafka topic "fulfillment.orders".

Agent: How should the integration handle errors?
You:   Invalid orders go to the Kafka topic "orders.invalid" with the validation
       error. Database failures retry 3 times with exponential backoff.

Agent: Which related capabilities should this iteration not implement, and why?
You:   No order-status API; it needs a separate security design.

If no deliberate exclusions remain, the design records **None identified** instead of inventing scope boundaries. Before assembling the design, the agent verifies every source and sink component against the catalog through the `camel` MCP server; in the example it confirms that `kafka` exists for the selected Camel version and runtime.

## Review and approve the design specification

The interview produces `docs/camel-kit/001-order-processing/design-spec.md` with six numbered sections:

 
| Section | Content |
| --- | --- |
| 1\. Executive summary | Business purpose, business value and stakeholders |
| 2\. Systems landscape | Systems, protocols and source/target roles |
| 3\. Flow designs | Per flow: source, sink, processing, data, configuration, error handling and the verified technical choices |
| 4\. Cross-cutting concerns | Applicable performance, security, monitoring and constraints |
| 5\. Constitution compliance | How every flow satisfies the eight rules, plus the catalog verification evidence: matched runtime, platform BOM, returned Camel version, and each artifact’s `VERIFIED` result and tool provenance |
| 6\. Project structure | Planned routes, configuration, tests and supporting artifacts |

An unnumbered **Not Doing (and Why)** section at the top records each deliberately excluded capability and its rationale, so implementation and review treat it as a scope boundary. Review the specification carefully: your approval ("Looks good, let’s proceed") authorizes everything downstream. There is no second approval for the plan.

## Plan (`/camel-plan`)

After approval the pipeline invokes `/camel-plan`. It applies the **Not Doing** boundaries and decomposes the design into route, configuration, dependency, test and conditional infrastructure tasks, each with acceptance criteria, the catalog-verified components and patterns to use, the files to create and the verification steps. The plan is a recipe, not the implementation: it contains no generated code.

   
| Task | Acceptance criteria | Components and patterns | Wave |
| --- | --- | --- | --- |
| 1\. REST endpoint | Listen at `/api/orders`, POST, return 202 | `platform-http`, `jackson` | 1 |
| 2\. Validation | Check amount > 0 and customer ID present | `bean`, `choice` | 2 |
| 3\. Enrichment | Query PostgreSQL, add email and address | `sql`, `jackson` | 2 |
| 4\. Tax calculation | Compute tax, set total = amount + tax | `bean` | 3 |
| 5\. Kafka publisher | Publish to `fulfillment.orders` with the order ID as key | `kafka` | 4 |

Retry and dead-letter behaviour belongs to the affected route tasks unless error delivery is itself a business flow. A structured metadata block lists each task’s files, the logical resources it provides and consumes and its explicit dependencies; `/camel-execute` derives the waves from it. Tasks in the same wave can run in parallel on agents that support concurrent dispatch; later waves wait for their dependencies.

## Execute (`/camel-execute`)

`/camel-plan` then invokes `/camel-execute`, which runs all tasks without pausing between them. It first analyzes the dependency waves, probes the target environment, and batch-verifies the catalog artifacts needed by each wave. For every task it dispatches the persona and guides declared by the plan: route and configuration tasks use the internal `camel-implement` skill, test tasks use `camel-test`. Each task then goes through three reviews:

1.  **Adversarial review.** A fresh-context moderator and parallel critics inspect the task diff where the agent supports subagents; single-conversation agents run the critic lenses sequentially and record the missing isolation. Verified failures go back to implementation.
    
2.  **Spec compliance review.** The route matches the task’s acceptance criteria without adding capabilities excluded by **Not Doing (and Why)**.
    
3.  **Code quality review.** Constitution compliance: single responsibility, observability, external configuration and the other rules.
    

Wave 1/4: Task 1 (REST endpoint)
  - Implementing route...
  - Adversarial review: PASS
  - Spec compliance: PASS
  - Code quality: PASS
  - Task 1 complete

Wave 2/4: running 2 independent tasks concurrently where supported...
  Task 2 (Validation)      ... PASS
  Task 3 (Enrichment)      ... PASS

After all tasks, execute performs a cross-cutting review, dispatches the internal `camel-verify` skill once, and writes `execution-report.md`.

## Runtime verification

`camel-verify` runs three phases after the environment probe and embeds its evidence in the execution report:

  
| Phase | What happens | Outcome |
| --- | --- | --- |
| Build or startup smoke | Spring Boot and Quarkus projects compile with `./mvnw` (or the system `mvn` when there is no wrapper); Camel Main projects run a startup smoke test instead | PASS, SKIPPED or FAILED with the reason |
| Test | Discovers `*.it.yaml` files recursively and runs `camel test run` when the Camel test plugin is available. Tests that declare Testcontainers also need Docker; container-free and mock-only tests run without it | Passed-test count, or an explicit skip or failure |
| Report | Summarizes checks, fixes, failures and skipped phases | Verification status in the execution report: PASS, PARTIAL, FAIL or NOT\_RUN |

Build and test failures enter bounded classify, fix and retry loops of up to 15 attempts; the Camel Main startup smoke test allows up to 6. Missing tools skip their dependent checks with a recorded reason. Verification is informational: it does not block `/camel-execute` from finishing, so read the report and resolve failed or skipped checks before deployment. See [Runtime verification](verification.md).

## Validate (`/camel-validate`)

The pipeline ends with `/camel-validate`, a static quality gate over the generated routes: schemas, endpoint URIs, project-relative quality thresholds, security, anti-patterns and all constitution rules. It reports findings in `validation-report.md` without modifying the routes.

## Pipeline files

Every stage persists its artifact under `docs/camel-kit/<pipeline-id>/`, so a session can be closed and resumed; `.camel-kit/pipeline.json` records the active pipeline ID.

docs/camel-kit/001-order-processing/
  design-spec.md           <- brainstorm
  implementation-plan.md   <- plan
  execution-report.md      <- execute, including the verification evidence
  validation-report.md     <- validate

With Camel Main selected during design, the routes and properties are generated at the project root and no `pom.xml` is needed:

order-processing/
  order-reception.camel.yaml
  order-validation.camel.yaml
  customer-enrichment.camel.yaml
  tax-calculation.camel.yaml
  kafka-publisher.camel.yaml
  application.properties
  run.sh
  src/test/resources/
    order-reception.camel.it.yaml
    ... one .camel.it.yaml file per flow
    application-test.properties
    jbang.properties
  docker-compose.yaml      (only when external services require it)

Spring Boot and Quarkus projects use the Maven source layout instead, with routes under `src/main/resources/camel/`.

## Standalone stages and amendments

Every stage can be invoked on its own with a pipeline ID. Plan, execute and validate then read their input from the artifacts on disk instead of the conversation, and do not invoke the next stage. This supports resuming a session, triggering single stages from automation, and re-running only what changed:

/camel-plan 001-order-processing
/camel-execute 001-order-processing

To change an approved design, run `/camel-brainstorm 001-order-processing`. When `design-spec.md` already exists the skill enters amend mode: it loads the specification, applies your changes after approval, and marks each existing direct child stale with `camel-kit doc stale`. Regenerate the stale stages standalone, plan first and then execute. `camel-kit doc check <artifact>` shows the staleness state of any artifact; see [Command reference](commands.md).

## Variations and troubleshooting

-   **Asynchronous processing.** Say so during the interview ("process orders asynchronously with 10 concurrent threads") and the requirement is recorded in the flow design.
    
-   **Data mapping.** For JSON-to-JSON mapping, DataMapper uses inline Groovy when both schemas are absent or the mapping has fewer than 20 leaf fields, and XSLT only when the mapping has at least 20 leaf fields and at least one schema.
    
-   **Several environments.** Ask for dev, staging and production configurations and the agent generates one `application-<env>.properties` per environment.
    
-   **A route breaks later.** Run `/camel-debug` for a structured diagnosis outside the pipeline; failures during `/camel-execute` are handled by its own verification loop.
    
-   **Rules too strict.** Edit `docs/constitution.md` before running the pipeline; the eight rules are per project.