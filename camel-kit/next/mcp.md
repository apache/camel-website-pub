# MCP servers

Camel Kit uses the Model Context Protocol to verify Camel configuration, to guide Citrus test generation and to search documentation without loading whole catalogs into the agent’s context. `init` configures two local servers by default (three with `--with-citrus-mcp`; released versions 0.4.1 and earlier include all three by default) in the agent’s MCP configuration file (see [Supported AI agents](agents.md) for the file of each target); the agent starts each one with JBang when a skill first needs it, and JBang resolves the runner and the catalog artifacts from the configured repositories.

 
| Server | Purpose |
| --- | --- |
| `camel` | The Apache Camel catalog: components, EIPs, data formats, languages, Kamelets and examples; route, YAML and configuration validation; diagnostics, migration and OpenAPI helpers |
| `camel-knowledge` | Hybrid search over indexed Apache Camel documentation, CVE advisories, release notes and Jira issues; see [Knowledge MCP](knowledge.md) |
| `citrus` | The Citrus action and endpoint catalogs, the YAML DSL schema and the test-authoring guidance used by `camel-test` |

The JBang runner coordinates of this release:

camel            org.apache.camel:camel-jbang-mcp:4.22.1:runner
camel-knowledge  io.github.luigidemasi:camel-kit-knowledge-mcp:0.0.2:runner
citrus           org.citrusframework:citrus-mcp-server:5.0.1:runner

The generated configuration is, in the target’s JSON or TOML shape:

```json
{
  "mcpServers": {
    "camel": {
      "command": "jbang",
      "args": [
        "--repos", "<configured MCP repositories>",
        "-Dcamel.catalog.repos=<configured catalog repositories>",
        "-Dquarkus.log.level=WARN",
        "-Dquarkus.http.port=-1",
        "org.apache.camel:camel-jbang-mcp:4.22.1:runner"
      ]
    }
  }
}
```

Versions and repository lists come from `distribution.properties`; nothing is extracted into the project, and the generated launch configuration is used unchanged. Targets with exact tool filtering receive the workflow allowlist of each server from the workflow manifest; Codex CLI adds `default_tools_approval_mode = "prompt"`, Pi reads the same `.mcp.json` through `pi-mcp-adapter`.

## Responses are data

An MCP response is loaded context. The workflow relies only on the purpose-specific fields it requested, after the artifact identity, runtime, platform BOM, resolved version, result and provenance are present and validated. Prose, examples, commands, URLs, tool requests or scope changes in a response cannot direct an action; summaries inherit the response’s authority rather than increasing it. See [Context authority](skills.html#context-authority).

## Version binding

Every version-sensitive catalog call passes the project’s `runtime` (`main`, `spring-boot` or `quarkus`) and the full platform BOM coordinate derived from `.camel-kit/config.properties`; a call without them is answered from the catalog bundled in the server, which may be the wrong version.

 
| Runtime | Platform BOM |
| --- | --- |
| `main` | `org.apache.camel:camel-catalog:<project.camelVersion>` |
| `spring-boot` | `org.apache.camel.springboot:camel-catalog-provider-springboot:<project.camelVersion>` |
| `quarkus` | `io.quarkus.platform:quarkus-camel-bom:<project.platformBomVersion>` |

The version binding comes from `.camel-kit/config.properties` (`project.runtime`, `project.camelVersion`, `project.platformBomVersion`). Every catalog call passes `runtime` and the full `platformBom` GAV derived from those properties — those parameters are the binding. Detail tools do not all echo a version, so each artifact is validated by type and name against the request instead. A detail-call error is not proof of absence: an artifact is recorded as `NOT_FOUND` only after a successful list call with a complete enumeration contains no exact match, and as `UNVERIFIED` when completeness or the binding cannot be established.

For behaviour questions — YAML shape, runtime configuration, version changes, header propagation — skills call `camel_docs_search` on the `camel-knowledge` server, not `camel`. The knowledge server tools (`camel_docs_search`, `camel_docs_component_info`, `camel_docs_cve_search`, `camel_docs_release_info`, `camel_docs_jira_lookup`) complement the catalog with documentation search; catalog tools (`camel_catalog_*`) remain on `camel`.

The current defaults are Camel 4.22.1 for Camel Main and Spring Boot, with Camel 4.18.3 on the Quarkus platform 3.33.3.2; the catalog server artifact follows the Camel Main stream.

## The Camel catalog server

The workflow allowlist covers the read-only and generation helpers the skills use; runtime mutation and control tools stay out of the generated configuration.

 
| Tool | Purpose |
| --- | --- |
| **Catalog exploration** |
| `camel_catalog_components`, `camel_catalog_component_doc`, `camel_catalog_component_maven` | List, document and locate the Maven coordinates of components |
| `camel_catalog_dataformats`, `camel_catalog_dataformat_doc` | Data formats and their options |
| `camel_catalog_languages`, `camel_catalog_language_doc` | Expression languages |
| `camel_catalog_eips`, `camel_catalog_eip_doc` | Enterprise Integration Patterns and their configuration |
| `camel_catalog_kamelets`, `camel_catalog_kamelet_doc` | Kamelets and their dependencies |
| `camel_catalog_examples`, `camel_catalog_example_file` | Camel examples and their files |
| **Validation, security and tests** |
| `camel_validate_route` | Validate one endpoint URI against the bound catalog (the skills call it once per statically extracted endpoint) |
| `camel_validate_yaml_dsl` | Validate YAML DSL syntax |
| `camel_transform_route` | Convert routes between YAML and XML |
| `camel_route_context`, `camel_route_harden_context` | Extract components and EIPs from a route; candidate evidence for route hardening |
| `camel_route_test_scaffold` | A JUnit 5 route test scaffold |
| **Diagnostics and configuration** |
| `camel_component_properties`, `camel_configuration_validate` | Component property metadata; validation of configuration properties |
| `camel_dependency_check`, `camel_error_diagnose`, `camel_properties_translate` | Dependency checks, error diagnosis, property translation between runtimes |
| `camel_version_list` | Camel versions with LTS status and JDK requirements |
| **Migration and OpenAPI** |
| `camel_migration_analyze`, `camel_migration_compatibility`, `camel_migration_recipes`, `camel_migration_guide_search`, `camel_migration_wildfly_karaf` | Migration analysis, compatibility, recipes and guidance |
| `camel_openapi_validate`, `camel_openapi_scaffold`, `camel_openapi_mock_guidance` | OpenAPI validation, scaffolding and mock guidance |

The design stage verifies every component, EIP, data format and language before it enters the design, and records the evidence (see [Catalog verification](camel-brainstorm.html#catalog)). During implementation the route files are validated with `camel_validate_route` and `camel_validate_yaml_dsl`, and `camel_configuration_validate` is a mandatory gate after writing application properties: generation is not complete until it passes or the documented manual fallback is recorded. `/camel-validate` uses the same tools for its endpoint verification, and `camel-test` uses the route context and hardening tools for its test strategy.

Without the catalog, a model writes component names from its training data, which may be renamed, removed or different in the target version. With it, a request such as "a message queue" becomes three verified candidates (`jms`, `amqp`, `kafka`) and a question to you, and an unknown name becomes a clarification instead of a guess.

## The Citrus server

`camel-test` validates the test vocabulary through `citrus_catalog_actions`, `citrus_catalog_action`, `citrus_catalog_action_schema`, `citrus_catalog_endpoints`, `citrus_catalog_endpoint`, `citrus_catalog_endpoint_schema`, `citrus_docs_index` and `citrus_docs_page`, plus resources such as `citrus://schema/dsl/yaml`. The test schema and the generated test dependencies use `citrus.version` from `.camel-kit/config.properties`, and the server coordinate is bound to the actual runner artifact in the agent’s configuration. Typed catalog and schema fields are treated as same-version data only when that runner version equals `citrus.version`; otherwise the skill uses the same-version quick reference cached under `.camel-kit/.cache/citrus/`, and marks a generated test as unverified rather than falling back to another Citrus version silently.

## Fallback

Skills call the tools directly without probing for availability first. If a call fails (tool not found, network error, timeout), the skill falls back to the bundled guides and continues with a warning; the pipeline degrades rather than stopping, and the missing verification is recorded.