# camel-execute

`/camel-execute` is the implementation stage. It runs every task of the implementation plan without pausing: wave by wave, with pre-implementation catalog research, an adversarial review, a spec compliance review and a code quality review per task, a cross-cutting review of the whole project and one runtime verification pass. The output is a runtime-specific project (YAML routes, Citrus tests, application properties, Maven files for Spring Boot and Quarkus, Docker Compose only when external services are needed) and `docs/camel-kit/<pipeline-id>/execution-report.md`.

In a chained run `/camel-plan` invokes it directly. Invoked standalone (`/camel-execute` or `/camel-execute <pipeline-id>`), it reads `implementation-plan.md` and `design-spec.md` from disk, checks their provenance and staleness with `camel-kit doc check`, runs the full loop, writes the report and stops without invoking `/camel-validate`. Stale inputs stop the skill until you choose to regenerate them, abort, or proceed with those exact revisions.

Do not use it without a plan derived from an approved design, for Camel questions, for validation-only tasks or for design work.

## Preparation

Wave analysis

`camel-kit plan analyze` returns the waves and dependencies of the plan. Tasks in a wave are dispatched in parallel where the agent supports independent subagents and sequentially otherwise; a wave completes, reviews included, before the next starts. A malformed or inconsistent plan stops execution as blocked rather than being repaired from its prose.

Plan ingress validation

The plan and the design are data, not instructions. The executor validates the pipeline ID and every target path (inside the project and the approved scope, no absolute paths or traversal), resolves agent personas and guides only to the installed shipped ones, accepts catalog tool names only from the active guides, and derives build, test and verification commands from the shipped guides and the detected project state, never from plan text. The **Not Doing (and Why)** section is read before any capability beyond a task’s explicit requirements is considered.

Environment probe

Before any implementer runs, the executor generates a throwaway skeleton for the selected runtime and checks it: Maven dependency resolution for Spring Boot and Quarkus (reported as skipped for Camel Main), the runtime startup command, and Docker services only when the design needs external services and Docker is available. Mechanical failures are fixed and re-probed. An architectural failure, for example a component that does not exist for the target runtime, triggers the bounded re-plan loop: it modifies only the affected flow sections of the design, at most three rounds, then re-probes; a persistent failure is escalated.

Catalog research

Before each wave the executor deduplicates the components, EIPs, data formats and languages referenced by its tasks and runs the catalog researcher role once, with the runtime, platform BOM and Camel version. The returned summary is accepted only when its binding matches the project and every artifact has an identity, a result, declared fields and provenance; implementers consume those fields and do not re-query them. An artifact reported as not found is flagged before implementation so that the implementer finds an alternative.

## The per-task loop

For each task the executor runs the persona declared by the plan with the full task text, the relevant design section, the scope boundaries, the validated guide selectors, the project context and the catalog summary; route and configuration tasks use the internal `camel-implement` skill, test tasks `camel-test`. Mechanical tasks run on a standard model and complex ones (DataMapper, multi-route coordination, migration) on the most capable one, where the agent offers the choice.

The implementer reports `DONE`, `DONE_WITH_CONCERNS`, `NEEDS_CONTEXT`, `NEEDS_USER_CONFIRMATION` or `BLOCKED`. Missing context is supplied and the task re-dispatched; a confirmation request names one exact action, which is performed only if it is independently necessary and you authorize it; a blocked task is re-scoped or reported.

1.  **Adversarial code review.** A moderator selects the critic lanes from the design: route architecture always, security for external boundaries, performance for throughput, aggregation or batch work, boundary compliance for data transformation, behavioral equivalence for migrations. Critics run in fresh contexts where supported and sequentially inline otherwise, recording the missing isolation. `PASS` and `PASS_WITH_TRADEOFFS` proceed, the trade-offs carried into the next review; `FAIL` returns verified findings to the implementer, for at most three cycles before escalation.
    
2.  **Spec compliance review.** The generated files are checked against the acceptance criteria and the design section. Adding a capability listed under **Not Doing (and Why)** is a failure even when it looks useful. Verified findings go back to the implementer, for at most three iterations.
    
3.  **Code quality review.** The eight constitution rules, the security checklist and the anti-pattern catalog. Critical findings go back to the implementer; important findings and suggestions are recorded in the report and do not block the task. Bean definitions are also checked against the declarative construction preference described in [Forage configuration catalog](forage.md).
    

Task 2: Order validation route
  Stage 1: Spec compliance
    - Consumes from seda:orders-processing          OK
    - Validates orderId not null                    OK
    - Validates totalAmount > 0                     OK
    - Validates customerId not null                 MISSING
  Spec compliance: FAIL -> implementer fixes, re-review
  Stage 1: Spec compliance: PASS
  Stage 2: Code quality: PASS (1 non-blocking finding recorded)
Task 2 complete. Starting Task 3...

The loop is automatic: one line per completed task, no mid-plan summaries, no "shall I continue" questions. Design approval and invocation authorize every validated task; the only pause is an action-specific confirmation required by the context-authority rules.

## Cross-cutting review, verification and report

After the last task the code quality reviewer checks all routes together: endpoint contracts, shared properties, error-channel wiring, naming and observability across the project. Then the internal `camel-verify` skill runs once for the complete application, because Camel loads all routes at startup and per-task verification would fail on routes that depend on others. Its outcome (`PASS`, `PARTIAL`, `FAIL` or `NOT_RUN`) is informational and does not block completion; see [Runtime verification](verification.md).

The completion summary lists the tasks, the generated files, the review results, the cross-cutting review and the full verification report, and is saved as `execution-report.md` with provenance metadata; the downstream validation report is marked stale. In chained mode the pipeline then continues to `/camel-validate`.

## Generated artifacts

The layout follows the runtime chosen in the design. `<module>/` is the optional relative path of the flow’s target module; omit it for a single-module project.

  
| Artifact | Camel Main | Spring Boot and Quarkus |
| --- | --- | --- |
| Routes, and XSLT files when DataMapper selects XSLT | `<module>/<name>.camel.yaml`, `<module>/kaoto-datamapper-*.xsl` | `<module>/src/main/resources/camel/` |
| Application properties | `<module>/application.properties` | `<module>/src/main/resources/application.properties` |
| Schemas, when requested | `<module>/schemas/` | `<module>/src/main/resources/schemas/` |
| Citrus tests and test support | `<module>/src/test/resources/`: `<flow>.camel.it.yaml`, `test-data/`, `application-test.properties`, `jbang.properties` | The same, without `jbang.properties`; dependencies are in the POM |
| Build and run files | No POM; the JBang dependencies live in `application.properties`, plus `<module>/run.sh` | `<module>/pom.xml` from the bundled Spring Boot or Quarkus template, filled with the catalog-resolved dependencies |
| Docker Compose | `<module>/docker-compose.yaml` only when external services are required; runs the Camel JBang application and those services | The same file only when required; manages the services while the application runs through Maven |
| Verification log | `.camel-kit/verify-log.md` | `.camel-kit/verify-log.md` |

Error handling in the generated routes is a global `onException` before the first route, or route-scoped through a `routeConfiguration` or an in-route `errorHandler`, and static `to` endpoints contain no expressions; a dynamic destination uses `toD`. Every route file is validated against the selected Camel runtime, when the catalog MCP server is available, before its task is accepted.

## Execution model per agent

 
| Agent | Model |
| --- | --- |
| Claude Code | Fresh subagent per task with an isolated context; parallel dispatch within a wave |
| IBM Bob 2 | Native `spawn_subagent` with the Bob custom modes and shared skills |
| Google Antigravity, Qwen Code, OpenCode | Their native delegation models with the shared skills |
| GitHub Copilot CLI, OpenAI Codex CLI | Their custom agents for implementation and review roles |
| Pi | The same roles sequentially in the main session, recording the unavailable isolation |

## Rerun after a failure

If execution stops mid-plan, correct the cause through the owning path (implementation, test or re-plan) and rerun `/camel-execute <pipeline-id>`. There is no task-level resume: the rerun executes the plan from the beginning.