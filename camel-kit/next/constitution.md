# Constitution

The constitution is the set of eight rules every generated route must satisfy. `init` renders it into the project as `docs/constitution.md` from the shipped template (version 2.1), where project data can strengthen or specialize it through typed customization fields before the pipeline runs; the design stage records how every flow meets it, the code quality review checks each task against it, and `/camel-validate` reports every rule in its final report. Iron Law 2 is the pipeline rule that enforces it (see [Iron Laws](pipeline.html#iron-laws)). Everything else about route design, such as error handling strategy, retry policy, throttling, idempotency, transactions or data formats, is decided per flow during design, not fixed here.

## The eight rules

1.  **Route structure.** Every route has a source (`from`) and a sink (a final `to`). `direct` and `seda` sub-routes may omit an external sink. A route without a source or sink fails validation; a pass-through route with no processing step produces a warning.
    
2.  **Single responsibility.** One route, one purpose, explainable in one sentence. A description that needs more than one "and" means several routes. More than seven processing steps produces a review warning.
    
3.  **Separation of concerns.** Complex integrations are decomposed into composable routes along ingestion, processing and delivery; `direct` for synchronous internal routing, `seda` for asynchronous. Business logic lives in beans, integration logic in routes.
    
4.  **Naming conventions.** Route IDs follow `<domain>-<action>[-<qualifier>]`, for example `order-ingestion` or `customer-enrichment`. Internal endpoints are `direct:<route-id>` and `seda:<domain>-<purpose>`. Camel built-in headers keep their `CamelCase` names; custom headers and properties use kebab-case (`order-id`, `correlation-id`). A route ID outside the convention produces a warning.
    
5.  **Observability.** Every route declares a `routeId` and a `description`. Correlation IDs (for example `X-Correlation-ID`) trace a request across routes; logging happens at decision points, not at every step. A route without an ID fails validation.
    
6.  **External configuration.** No hardcoded connection strings, credentials or environment-specific values: every configurable value is a `{{placeholder}}`, resolved from environment variables, then system properties, then `application.properties`, then the bundled defaults. A hardcoded credential or connection string fails validation.
    
7.  **Component catalog verification.** Every component in a route is verified to exist in the Camel catalog for the target version, under the project’s runtime and platform BOM binding, through `camel_catalog_component_doc`. A failed detail call is unverified, not absence: absence requires a complete component list with no exact scheme. A component that is not found produces a warning, the version-bound list is searched for candidates that are validated in turn, and the decision to switch is yours.
    
8.  **Infrastructure through Forage.** Infrastructure beans are declared with `forage.*` properties when Forage covers them, following the configuration ladder (Forage, then component properties, then a hand-written bean with a stated reason). A hand-written bean, in `camel.beans.*` or in a YAML `beans` block, needs a one-line reason comment. An unknown `forage.*` key, or a hand-written bean with a Forage equivalent and no reason, fails validation; a hand-written bean whose only alternative is a scalar component property produces a warning. See [Forage configuration catalog](forage.md).
    

## Project customizations

The generated `docs/constitution.md` ends with commented sections through which project data can strengthen or specialize the rules; `/camel-validate` parses them as a fixed, typed schema:

```yaml
# allowedComponents:
#   - kafka
#   - http
#   - jpa

# routeIdPattern: "myteam-{domain}-{action}"

# deadLetterPatterns:
#   order: kafka:order-dlq
#   default: kafka:integration-dlq

# security:
#   requireTLS: true
#   sensitiveHeaders: [Authorization, X-API-Key, Cookie]
```

`allowedComponents` is a bounded list of exact, catalog-validated component schemes; `routeIdPattern` is at most 128 characters of literals plus the `{domain}` and `{action}` placeholders only, not a regular expression; `deadLetterPatterns` names the error channel per domain; `security` carries typed fields such as `requireTLS` and `sensitiveHeaders`. The fields cannot override the shipped safety and authority rules or add executable instructions: the mapping is parsed strictly, duplicate keys and unknown fields are reported and ignored, and prose or comments carry no instructions.

## Constitution and Iron Laws

The constitution says what makes a good route. The six Iron Laws say when and how the pipeline enforces quality: catalog verification, constitution compliance, no code without an approved design and a plan, spec compliance before quality, adversarial review, surgical changes. Iron Law 2 incorporates the constitution; the two sets are complementary. See [Iron Laws](pipeline.html#iron-laws).