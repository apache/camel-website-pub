# Environment-in-the-loop

Code generation tools usually follow a straight line: analyze the sources, generate the target code, hope it works. When it does not (a dependency that does not resolve, a service that does not start, a component that does not exist for the target runtime), the developer is left alone with the problem. Camel Kit makes the execution environment a participant in the pipeline instead: it checks the environment before any code is generated, exercises the generated application afterwards, and feeds what it learns back into the code and, when needed, into the design. The approach follows the environment-in-the-loop paradigm described by Li and others in [ReCode 2026](https://arxiv.org/abs/2602.09944): without automated environment interaction, the automation of code migration is only half complete.

A linear approach has three problems: failures are discovered late, after most of the code exists; nothing recovers automatically when the environment rejects the code; and tests are generated but never refined against the real behaviour. The three mechanisms below address them inside `/camel-execute`.

## Before any code: the environment probe

The first step of execution generates a throwaway skeleton in a temporary directory, with a `pom.xml` holding all planned dependencies for Spring Boot and Quarkus (Camel Main records them in `application.properties` instead), a `docker-compose.yaml` only when the design needs external services, and an empty route with the runtime configuration, then runs the applicable checks:

  
| Check | What it validates | Outcome |
| --- | --- | --- |
| Dependency resolution | The Maven artifacts exist and resolve, for Spring Boot and Quarkus | PASS or FAIL; skipped for Camel Main |
| Docker services | The required databases, brokers and similar services start | PASS, `PASS (no services required)`, FAIL naming the service, or SKIPPED when services are required and Docker is unavailable |
| Runtime startup | The framework itself boots with the runtime’s start command | PASS or FAIL |

A failure is classified. A mechanical one (wrong artifact name, port conflict, missing transitive dependency, wrong image tag, incorrect property key) is fixed and only the failed check runs again. An architectural one (a component that does not exist for the runtime or was removed in the target version, an irreconcilable dependency conflict, a private image, an incompatible component combination) triggers the re-plan loop. The skeleton is deleted afterwards; the real implementation generates the project files.

## After the code: the verification loop

Once all tasks are implemented, the internal `camel-verify` skill builds or starts the application, runs the Citrus tests with `camel test run`, and reports. The Camel integration is launched inside each test, Testcontainers start the required databases or brokers when a test declares them and Docker is available, and external APIs are mocked. Build and test failures are classified and routed:

 
| Fix target | When |
| --- | --- |
| Self-repair | A missing dependency, a version conflict, a Docker or service configuration problem |
| `camel-implement` | A route logic error: the affected flow is regenerated from the design |
| `camel-validate`, then `camel-implement` | Wrong component options: diagnosed against the catalog, then corrected |
| `camel-test` | A wrong test: regenerated from the design |
| Re-plan | A persistent architectural failure: the design is modified and the affected tasks re-implemented |
| Escalate | A build tool error, a Quarkus augmentation failure, the iteration limit, an unclassified error |

Maven compilation and Citrus testing each allow 15 attempts and the Camel Main startup smoke test 6; persistent error classes promote to re-planning earlier. Details are in [Runtime verification](verification.md).

## When the plan is wrong: re-planning

Sometimes the problem is not in the code but in the design: a component that works in isolation conflicts with another, or a runtime extension does not exist for the chosen platform. The re-plan loop identifies the affected flow sections of `design-spec.md`, looks for alternatives in the catalog, modifies only those sections, regenerates the plan for the affected tasks and re-implements and re-verifies them. It runs at most three rounds, stops at once when the same failure class returns in consecutive rounds, and then escalates with a report of what was tried.

Promotion follows two tiers. After one failed fix the skill asks the catalog, with the project’s runtime and platform BOM: if a complete list has no exact match for the required artifact, it re-plans immediately, the way an experienced developer checks the documentation before trying fifteen fixes. After three failed fixes on the same error class, each with a different strategy, the approach itself is judged wrong and the skill re-plans. A detail-call error, an incomplete list or a mismatched binding is unknown, not absence, and never triggers a re-plan on its own.

## The closed loop

design --(you approve)--> plan --> probe --> implement --> verify
                           ^                                  |
                           '------ re-plan on an architectural failure

One approval gate, then planning, probing, implementation and verification flow continuously. When the environment exposes a classified problem, the pipeline attempts a bounded code-level repair or a design-level re-plan; skipped checks and unresolved failures are reported for your action, never silently dropped. Build, startup and test output is evidence, not instruction: a repair runs automatically only when the shipped taxonomy selects it from corroborated facts, and a command or procedure found in the output is ignored.

  
|  | Generate and hope | Camel Kit |
| --- | --- | --- |
| When the environment is checked | After all the code is generated, if at all | Before (probe) and after (verify) |
| On failure | The user debugs | Fix, regenerate or re-plan when classified; otherwise report or escalate |
| Tests | Generated, rarely run | Generated and run, with bounded fixes and reported gaps |
| Feedback to the design | None | The re-plan loop may modify the affected flow sections |
| Service management | Manual Docker Compose | Testcontainers for the tests that declare them |