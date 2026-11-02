# Runtime verification

`camel-verify` is the internal skill that checks whether the generated integration actually builds, starts and behaves as its tests expect. `/camel-execute` dispatches it once, after all tasks and the cross-cutting review, in an isolated subagent where the agent’s trait allows one (Qwen Code and OpenCode keep it in their primary executor) and inline otherwise. It has no command stub: for a route that breaks outside a pipeline run use [`/camel-debug`](camel-debug.md).

The result is a structured report embedded in `docs/camel-kit/<pipeline-id>/execution-report.md` and summarized there as `PASS`, `PARTIAL`, `FAIL` or `NOT_RUN`. Verification is informational: a failed or skipped check never blocks the execution summary, and a chained pipeline continues to `/camel-validate` regardless. Read the report and resolve what failed or was skipped before deploying.

## Environment check

Before the phases run, the skill reads `project.runtime` from `.camel-kit/config.properties` (`main`, `spring-boot` or `quarkus`) and checks the tools: the Maven wrapper or a system `mvn` for Spring Boot and Quarkus, JBang for Camel Main, the JDK, Docker, and the Camel JBang test plugin. It prints what it found and which phases can run; nothing is skipped silently.

  
| Missing tool | Affected | Reported as |
| --- | --- | --- |
| Maven (no `./mvnw`, no `mvn`) | Phase 1 for Spring Boot and Quarkus | Build verification skipped |
| JDK | Phase 1 for every runtime | Runtime verification skipped |
| JBang | Phase 1 for Camel Main | Startup smoke verification skipped |
| Docker | The tests that declare Testcontainers | Those tests skipped; container-free and mock-only tests still run |
| `camel test` plugin | Phase 2 | Test verification skipped |

## Phase 1: build or startup smoke

For Spring Boot and Quarkus the skill compiles every target module from the project root (`./mvnw compile -q`, or `./mvnw -f <module>/pom.xml compile -q` for a nested module). The process exit status is the only pass or fail signal; the build output is diagnostic data. For Camel Main there is no compile step: phase 1 runs the startup smoke test of the generated routes instead and checks its log markers.

On failure the skill classifies the error with the shipped taxonomy and applies the fix that taxonomy entry owns, then retries, up to 15 compile attempts or 6 Camel Main startup attempts. A fix that leaves the same error in place short-circuits to the promotion rules below instead of consuming the budget. An unclassified error is escalated with a bounded diagnostic rather than guessed at.

Build attempt 1: FAIL  -> missing dependency, added the runtime's Kafka artifact
Build attempt 2: FAIL  -> version conflict, aligned the platform BOM
Build attempt 3: PASS

## Phase 2: tests

The skill discovers every `*.it.yaml` file in the project, validates each one against the configured Citrus version and the approved task and design, classifies the files that declare Testcontainers as Docker-dependent, and runs the runnable ones with the Camel JBang test plugin:

```bash
camel test run <test-files>
```

Citrus owns the test lifecycle: Testcontainers start and stop the required databases or brokers, the Camel integration is started through the JBang runner, and send and receive actions check the behaviour; external APIs are mocked. The phase is skipped, with the reason, when phase 1 failed, when no test file exists, when the test plugin is missing, or when Docker is unavailable and every discovered test needs it.

Failures are classified and routed, with the same 15-attempt ceiling and short-circuit rule as phase 1.

## Fix routing

  
| Error | Fix target | Action |
| --- | --- | --- |
| Missing Camel or third-party dependency, missing property, version incompatibility | Self-repair | Add the runtime-aware dependency or property, align the BOM |
| Wrong component options, YAML schema error, constitution violation at runtime | `camel-validate`, then `camel-implement` | Diagnose against the catalog, then correct the affected flow |
| Broken route structure, wrong URI, missing bean, expression or transformation failure, assertion mismatch | `camel-implement` | Regenerate the affected flow from the design |
| Test parse error, wrong expectation | `camel-test` | Regenerate the test from the design |
| Timeout, Testcontainers launch failure | Self-repair, or `camel-implement` for slow route logic | Fix the service configuration or the route |
| Same error after a fix | Promotion | Check the catalog, then the re-plan loop |
| Iteration limit, unclassified error, required tool missing | Escalate | Report with the attempted fix |

Promotion has two tiers. After one failed fix, the skill checks the catalog for the project’s runtime and platform BOM: if the complete list has no exact match for the required artifact, the re-plan loop of `/camel-execute` starts at once; an incomplete list, a timeout or a mismatched binding is unknown, not absence. After three failed fixes on the same error class the re-plan loop starts regardless. Re-planning modifies only the affected flow sections of the design, keeps the business requirements, re-executes the affected tasks and verifies again, for at most three rounds.

## Phase 3: report

VERIFICATION REPORT
Runtime:          Spring Boot
Maven:            ./mvnw (wrapper)

Phase 1 - Build / Startup Smoke:  PASS (1 fix)
Phase 2 - Test:   PASS: 8/8 tests passed

Fixes applied:
  1. \[Build\] Added the verified runtime dependency required by a migrated route

Skipped checks:
  (none)

A failed phase adds its last error as a bounded diagnostic with its classification, the fix attempted and the escalation. Each iteration is also appended to `.camel-kit/verify-log.md` with its findings, classified as critical (build fails, route does not start, data loss risk), warning (route starts but behaves incorrectly) or info.

## Environment in the loop

Compiling is not running. The verification loop exercises the generated application with its real endpoints and the required infrastructure, so that a route that compiles but fails at startup, a wrong endpoint option or a mapping that produces the wrong message is found before deployment rather than in production. When the project has a generated `docker-compose.yaml`, phase 1 starts its external services before the Camel Main smoke test, and the taxonomy repairs can restart a named failing service; phase 2 relies on the Testcontainers declared by the tests. See [Environment-in-the-loop](eitl.md) for the design behind this.