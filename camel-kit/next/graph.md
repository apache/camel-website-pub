# Graph intelligence

Camel Kit can build a property graph of an integration project: nodes for classes, routes, endpoints, beans, Maven artifacts and configuration properties, edges for inheritance, injection, route flow, bean references and configuration bindings. The graph feeds migration analysis, impact analysis, project-aware validation and retirement-candidate reporting. The standard skills use it for optional acceleration and can continue with source inspection when it is unavailable. A migration pack can require a particular parser for one of its steps.

![Graph visualization of a MuleSoft project: nodes are flows, connectors, Maven artifacts and configuration properties](_images/graph-visualize.png)

## How the graph is built

In the default distribution, `camel-kit graph generate` runs nine content parsers and two post-processors. It writes the graph to `.camel-kit/project-graph.json`. Use `--output` to choose another path and `--graph-file` to query that graph. `PomParser` runs first because the other parsers use its Maven artifacts for runtime detection and the dependency allowlist. The other eight parsers run in parallel. Kit merges their fragments in a fixed order so the result is independent of completion timing. Parser diagnostics record the scanned files, warnings, failures, timeouts and produced counts.

  
| Parser | Purpose | Files |
| --- | --- | --- |
| `PomParser` | Maven dependencies and properties, runtime detection | `pom.xml` |
| `JavaGraphParser` | Classes, methods, fields, DI annotations, Java DSL routes | `*.java` |
| `GroovyGraphParser` | Groovy scripts and classes | `*.groovy` |
| `XmlRouteParser` | Camel XML routes, recognized by the `route` element in any namespace | `*.xml` except POM, Mule and BizTalk inputs |
| `YamlRouteParser` | Camel YAML DSL routes | `*.yaml`, `*.yml` except `application*` |
| `ConfigParser` | Every application property, not only the `camel.*` keys | `application.properties`, `application-*.properties` |
| `MuleXmlFlowParser` | Mule 3.x and 4.x flows, sub-flows, connectors, endpoints, transforms, error handlers | `*.xml` with the Mule namespace |
| `DataWeaveParser` | DataWeave version, content types, functions, field access patterns | `*.dwl` |
| `BizTalkParser` | Orchestrations, maps, pipelines and bindings, through four StAX sub-parsers | `.odx`, `.btm`, `.btp`, binding `.xml` |

The post-processors run on the assembled graph: `CrossLinker` links producer and consumer routes through `direct` and `seda` endpoints, maps component usage to Maven artifacts, binds configuration to endpoints and creates the interface shortcuts described below; `PropertyBindingParser` then reads the property values for Camel’s `PropertyBindingSupport` syntax. Mule and BizTalk files are detected by their namespaces and extensions, so no configuration is needed; `init --source-platform` only hints the platform for unusual layouts. `camel-kit graph visualize` writes an interactive page to `.camel-kit/project-graph.html`.

## Migration parser providers

The distribution catalog identifies migration parsers by `provider/<id>`. The default catalog includes `provider/mule-xml`. Excluding this provider removes Mule XML parsing. DataWeave and BizTalk remain built in. To inventory a Mule project, run these commands from its source directory.

```shell
camel-kit graph generate --require-parser mule-xml
camel-kit graph find --type mule:flow
```

The first command checks that the named parser is available and builds the graph with all selected parsers. The second lists flow nodes and their source-relative `file` properties. A directory without Mule XML yields zero Mule flows. A malformed Mule document produces a warning naming the file while valid flows from other documents remain available. A missing provider or incompatible API produces an error and exit code 1 before the CLI writes a graph. A workflow that requires the parser must check that exit code before using the output.

Kit loads a fresh provider instance for each CLI graph build. Migration providers merge in catalog ID order between the Camel XML and DataWeave fragments. If two migration providers produce different nodes with the same ID, the later provider replaces the earlier node and the build reports a warning naming both providers. The [worked parser pack](contributing.html#migration-parser) adds a file format and a private source model through the same interface.

## Reading a saved graph

Kit writes JSON format `1.1` and reads both `1.0` and `1.1`. A node’s object key is its ID. An edge records its `from` and `to` IDs. Both records have a `type` and may have a `properties` object containing string values. IDs must contain a non-whitespace character. An edge can point to an external ID, such as a superclass outside the project. Duplicate JSON keys, malformed records and unsupported versions produce a diagnostic. Older Kit versions that only read `1.0` need a graph generated with that version.

Common types keep their existing names, including `CAMEL_ROUTE` and `ROUTES_TO`. Migration types use a provider namespace, for example `mule:flow`, `mule:flow-contains` or `biztalk:orchestration`. The core pack supplies the Mule and BizTalk adapters in stock and custom distributions. They map old names in saved graphs and query filters to the same types. For example, `graph find --type MULE_FLOW` and `graph find --type mule:flow` return the same nodes with canonical types.

```shell
camel-kit graph analyze mule --graph-file .camel-kit/project-graph.json
```

`analyze` returns the adapter’s summary, or `matched: false` when its rules find no matching project. If the adapter is missing, the command identifies the unavailable provider and exits with status 1. If its summary fails, the command names the provider, reports the cause and exits with status 1. A workflow that requires this analysis must leave its step incomplete. Generic commands such as `find`, `neighbors`, `stats` and `visualize` still work with the recorded type names. A library caller can read, traverse, write and reload such a graph, including its properties and relationships. A type filter accepts registered names and types present in the loaded graph. A misspelling returns an error with the valid names. Unmapped legacy names retain their spelling until a reader has the corresponding adapter. See [registering a graph adapter](contributing.html#graph-adapter).

## Commands

 
| Command | Purpose |
| --- | --- |
| **Analysis** |
| `analyze <namespace>` | Run the migration pack’s graph summary |
| `stats` | `available`, node and edge totals, nodes by type |
| `find` | Nodes by type, with a regular expression on the name or fully qualified name, falling back to the node ID |
| `neighbors` | Incoming, outgoing or both directions, optionally filtered by edge type and depth |
| `path` | The shortest path between two nodes |
| `subgraph` | The subgraph around a node, by breadth-first search with a depth limit |
| **Camel-specific** |
| `route-flow` | The ordered `FROM`, `PROCESSOR` and `TO` steps of an exact `CAMEL_ROUTE` node, or of the route consuming a given endpoint with `--from-endpoint` |
| `impact` | Bounded transitive reachability, up to 50 nodes per direction; `--direction upstream`, `downstream` or `both` (the default) |
| `route-topology` | Route-to-route connections with the target route, endpoint scheme and URI |
| `dead-code` | Structural retirement candidates: non-framework `camel-*` artifacts with no component usage, `direct` and `seda` consumers no route produces for, `camel.*` properties that configure nothing |
| **Context** |
| `project-norms` | Route ID naming, error-handling coverage, property prefixes and route step-count norms, including the observed P75 |
| `project-context` | Property conventions, existing beans, dependency versions and the route directory |
| `route-context` | Upstream, downstream, classified endpoints and the error flow of a route |
| `migration-context` | Bounded bidirectional context around a route for migration, see below |
| **Output** |
| `generate` | Build or rebuild the graph from the sources |
| `visualize` | Render the interactive HTML visualization |

Every result is a candidate within the graph’s coverage, not proof: a `dead-code` entry means the graph found no path, not that the code is safe to remove. Regenerate the graph after source changes so queries reflect the current project.

## Dependency-injection-aware analysis

`JavaGraphParser` understands injection across frameworks. Every field and constructor parameter of an allowed type creates a `USES_TYPE` edge, and `@Inject` or `@Autowired` marks that edge as an injection; `@Component`, `@Service`, `@Repository`, `@Controller`, `@Named`, `@Singleton`, `@ApplicationScoped` and `@RequestScoped` mark managed beans; `@Value` and `@ConfigProperty` create `INJECTS_INTO` edges from configuration properties to the fields that consume them. A POM-driven scope guard keeps the graph focused: `USES_TYPE` edges are created only for project-local classes, Apache Camel types and the framework types (Spring, Quarkus, Mule) found in the Maven dependencies, never for JDK types.

When class A injects interface I and class C implements I, `CrossLinker` adds a `DEPENDS_ON_VIA_INTERFACE` shortcut from A to C, and the traversal used by `impact` and `migration-context` crosses it. Without it, an upstream impact query on `OrderServiceImpl` returns nothing, because the route class only knows the `OrderService` interface; with it, the query returns the consumer classes, `OrderRoute` among them. `impact` follows incoming edges only, so the route’s endpoints are not part of that result: `route-context` or `migration-context` on the route shows its `kafka` source and `direct:payment` target.

`PropertyBindingParser` turns `application.properties` into part of the graph: `#class:` creates `INSTANTIATES` edges, `#bean:`, `#autowired` and `#type:` create `REFERENCES_BEAN` edges, `#property:` creates `REFERENCES_PROPERTY` edges, and placeholders in endpoint URIs create `CONFIGURES` edges to the matching properties. Spring Boot and Quarkus data source conventions become synthetic bean nodes, and Quarkus build-time properties are marked as such. A shared `RuntimeDetector` identifies Spring Boot, Quarkus, Camel Main or Karaf from the Maven dependencies; `init` persists the result in `.camel-kit/config.properties`.

## Migration context

```bash
camel-kit graph migration-context <routeId> [--depth N]
```

The command performs a bidirectional, interface-aware breadth-first search from one route (the ID without the `route:` prefix), with depth 3 by default and at most 50 expanded nodes, and returns structured JSON: the reached `routes` with their source endpoint and file, the deduplicated `components`, the `services` (bean class and name), the Maven `artifacts`, the `properties` with their outgoing edge type and target, and `warnings` for every reached node that was inferred rather than parsed. `runtime` comes from the project configuration. The result is focused local context, not a complete dependency map, and the command makes no MCP call: documentation, CVE or compatibility lookups are separate actions through the Knowledge server, using the reported components as input. See [Graph analysis](migration.html#graph) for how the migration uses it.

## Background

The interface-consumer expansion and the bidirectional traversal follow the deterministic knowledge base approach of Chinthareddy, [Reliable Graph-RAG for Codebases: AST-Derived Graphs vs LLM-Extracted Knowledge Graphs](https://arxiv.org/abs/2601.08773) (2026), which found deterministic AST-derived graphs both more correct and far cheaper than model-extracted knowledge graphs for multi-hop questions on Java codebases. Camel Kit departs from the paper where Camel projects differ from self-contained applications: it parses with JavaParser rather than Tree-sitter, tracks framework types from the POM instead of project-local types only, models the Maven dependency layer and the component-to-artifact mapping, and treats property-based bean wiring and configuration-to-code links as part of the architecture.

## Where the graph is used

-   `/camel-migrate` corroborates and accelerates its source analysis with the graph when one is current.
    
-   `camel-implement` loads `project-context` and `camel-test` loads `route-context` when a graph exists.
    
-   `/camel-validate` consumes `project-norms` and includes the `dead-code` report.
    
-   `/camel-start` and `/camel-knowledge` do not use it.
    

## Input safety and limits

Graph analysis reads sources without running the project. It skips symbolic-link files and directories below the selected root, rejects outside-root inputs, and accepts an explicitly selected root alias. Each source is limited to 16 MiB; recognized source files together are limited to 256 MiB, and discovery stops after 100,000 filesystem entries. Large unrelated binary artifacts do not count toward the source-byte limit. Discovery prunes directories named `.git`, `.svn`, `.hg`, `target`, `build`, and `node_modules` below the selected root before reading their contents. This avoids parsing copied resources in build outputs. The selected root itself is always scanned, even when it has one of these names.

If a source or discovery limit is exceeded, graph generation reports the limit and fails; `init --here` reports a warning and continues initialization. Select a smaller project/module when a source tree exceeds these bounds.

Each parser, including POM parsing, has a 60-second timeout. A timed-out parser contributes no partial result and produces a diagnostic. Cancellation is cooperative; these are input and waiting-time limits, not an operating-system memory or CPU sandbox.