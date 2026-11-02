# camel-validate

`/camel-validate` is the last stage of the pipeline: a static quality analysis of the generated Camel routes that writes a report and changes nothing. It covers correctness, security, anti-patterns, project conventions and the constitution. Runtime failures (build, startup, tests) belong to the verification loop inside `/camel-execute` (see [Runtime verification](verification.md)); a route broken outside a pipeline run belongs to [`/camel-debug`](camel-debug.md).

## When it runs

In a chained run `/camel-execute` continues to `/camel-validate` after the implementation and the runtime verification, with no further approval. A standalone `/camel-execute` stops after its summary, so invoke validation explicitly when you want the static gate:

/camel-validate <pipeline-id>
/camel-validate

With a pipeline ID, or with an active pipeline recorded in `.camel-kit/pipeline.json`, validation is pipeline-scoped: it cross-references the design, the plan and the execution report under `docs/camel-kit/<pipeline-id>/`, checks their provenance with `camel-kit doc check`, and stops on a stale artifact until you choose to regenerate it, abort, or proceed with that exact revision. Without any pipeline it is project-scoped and validates the routes found in the current project.

## Checks

The skill first builds the route inventory of every target module for the project’s runtime (module-root `*.camel.yaml` and `application.properties` for Camel Main, `src/main/resources/camel/` and `src/main/resources/application.properties` for Spring Boot and Quarkus), then runs:

-   Camel YAML DSL schema validation and endpoint configuration;
    
-   endpoint verification against the Camel catalog through the `camel` MCP server, for the project’s runtime and platform BOM;
    
-   quality metrics and thresholds, relative to the project norms when `.camel-kit/project-graph.json` exists;
    
-   security analysis from the shared checklist: hardcoded credentials, TLS, headers and unsafe endpoint settings;
    
-   the anti-pattern catalog;
    
-   all eight constitution rules;
    
-   structural retirement candidates from the project graph when it exists (see [Graph intelligence](graph.md)).
    

Validation is at least as strict as generation: a construct that Camel Kit refuses to generate does not pass validation because it was added by hand.

## Report

Pipeline-scoped validation writes `docs/camel-kit/<pipeline-id>/validation-report.md`; project-scoped validation writes `docs/validation-report-YYYY-MM-DD_HH-mm.md`. The report records the project, runtime and Camel version, a summary table with pass, fail and warn counts per category, the findings, the constitution rule results, and the recommendations: priority fixes for the failures, suggested improvements for the warnings.

    
| Category | Pass | Fail | Warn | Total |
| --- | --- | --- | --- | --- |
| Schema validation | . | . | . | . |
| Endpoint verification | . | . | . | . |
| Quality checks | . | . | . | . |
| Security analysis | . | . | . | . |
| Anti-patterns | . | . | . | . |
| Constitution compliance | . | . | . | . |

The report carries provenance metadata from `camel-kit doc init`, linked to the execution report when one exists. Fixing the findings is a separate step: edit the routes, or amend the design and rerun the affected stages, then validate again.