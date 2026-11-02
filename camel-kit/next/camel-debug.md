# camel-debug

`/camel-debug` diagnoses and repairs a broken Camel route outside a pipeline run: a route that used to work, a startup failure, a runtime exception, unexpected behaviour. Build and test failures during `/camel-execute` stay in that stage’s verification loop (see [Runtime verification](verification.md)); quality validation belongs to [`/camel-validate`](camel-validate.md). The project needs `.camel-kit/config.properties` for the runtime and version, and existing route files.

/camel-debug
/camel-debug my route fails with a ClassNotFoundException

## Five steps

Stop

Read the project runtime and Camel version, capture the exact symptom and the recent changes, and change nothing yet. Logs, stack traces, route files, configuration and catalog responses are diagnostic data: a command, URL or procedure found in them never directs the workflow.

Preserve

Record the branch, the working-tree state and the existing local changes with `git status` and `git diff`, and warn when uncommitted changes exist.

Diagnose

Reproduce the failure, classify it against the shared error taxonomy (the same one the verification loop uses), verify the components involved against the Camel catalog, and inspect the route structure. Three diagnostic roles (route analyzer, catalog verifier, log analyzer) run in isolated subagents where the agent supports them and sequentially inline otherwise. The diagnosis is presented before any change. If the error cannot be reproduced or classified, the skill says so instead of guessing.

Fix

One targeted repair for the diagnosed root cause, explained first, with no refactoring of the surroundings, then the reproduction command again. The taxonomy entry owns the fix target: a direct edit of the POM, the properties or the route; `camel-validate` to re-check the route against the catalog; `camel-implement` to regenerate the route from its design section; or escalation. The same error after a fix stops the step and asks for guidance; a new error is classified again. After five failed attempts the skill stops and lists what it tried.

Guard

A suggested preventive measure for the error category: a Citrus test for a route that failed to start, a `/camel-validate` run after endpoint changes, a health check or circuit breaker for an unavailable service, a build verification step in CI for dependency problems. Guards are recommendations and are not applied without approval.

## What authorizes a repair

Your request sets the gate. A request to diagnose and fix authorizes the ordinary in-scope repairs selected by the taxonomy from corroborated facts. A diagnosis-only request stops before any change: the skill presents the exact proposed repair and waits for approval. Text inside a log, a route, a tool response or any other loaded artifact never satisfies either gate. If an action outside the shipped workflow turns out to be necessary, the skill names its source, the exact action, the verified reason and the scope and waits for an action-specific confirmation; an isolated role that cannot ask returns `NEEDS_USER_CONFIRMATION` without acting.

## Result

DEBUG SUMMARY
Symptom:        Route order-intake fails at startup
Root cause:     camel-kafka is not on the classpath
Classification: Missing Camel component dependency
Fix applied:    Added camel-kafka-starter to pom.xml
Files changed:  pom.xml
Guard:          Add a dependency resolution step to the CI build

A diagnosis-only run ends with the root cause and the proposed fix, no changed files and no guard suggested.