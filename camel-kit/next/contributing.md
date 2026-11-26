# Contributing and releasing

Camel Kit is developed at [apache/camel-kit](https://github.com/apache/camel-kit) under the Apache Camel project. The CLI and agent skills live in `kit/`; the standalone Knowledge MCP server lives in `knowledge/`. Both share this repository and documentation, with independent versions and releases. Issues and pull requests go to that repository; questions go to the Camel [mailing lists](/community/mailing-list/). Contributors follow the [ASF code of conduct](https://www.apache.org/foundation/policies/conduct.md).

## Building

You need Java 21 or later for Kit and Knowledge, JBang, and Git; Maven comes with the wrapper. Always build with the wrapper, from the repository root.

```bash
./mvnw clean install                                      # all modules
./mvnw -B -Plinux-ship-certification clean install       # what CI runs (Linux)
./mvnw -B -Psourcecheck validate                          # the formatting gate
./mvnw test -pl kit/camel-kit-core                            # one module
./mvnw test -pl kit/camel-kit-core -Dtest=ShippedAssetStructureTest   # one test class

# run the CLI from source
jbang kit/camel-kit-main/src/main/jbang/main/CamelKit.java --help
```

The standalone JBang launcher enables native access for its terminal libraries. When invoking `org.apache.camel.kit.CamelKitMain` directly with `java`, include `--enable-native-access=ALL-UNNAMED` before the main class, as the launcher does.

 
| Module | Content |
| --- | --- |
| `kit/camel-kit-main` | The JBang entry point |
| `kit/camel-kit-core` | CLI commands, configuration, initialization and traits; all skills and templates as resources |
| `kit/camel-kit-graph` | The project graph: nine parsers and two post-processors |
| `kit/camel-kit-ship-resolver` | The classloader-isolated Maven resolver used for Ship evidence |
| `kit/camel-jbang-plugin-kit` | The Camel JBang plugin |

Install the shared parent once with `./mvnw -B -N install`, then build one product with `./mvnw -B -f kit/pom.xml clean install` or `./mvnw -B -f knowledge/pom.xml clean install`. The Knowledge reactor contains `schema`, `embedding`, `indexer`, `index` and `mcp`; ordinary builds use the committed index. All Java packages use `org.apache.camel.kit`, and Maven modules use `org.apache.camel`.

`distribution.properties` at the repository root is the single source of truth for every version pin; it is copied into the JAR and never duplicated by hand. `tools/sync_distribution_mirrors.py` copies the few literals Maven needs into `kit/pom.xml` and checks them with `--check`.

The CLI uses Aesh’s tokenized, one-shot argv API. Keep option binding in commands and business logic in services/controllers; preserve usage-error exit code 2 and stdout/stderr separation. `KitOptionParser` preserves strict scalar options and token-based list values; Ship additionally records context order. The standalone runner does not acquire an Aesh interactive terminal. JLine/TamboUI still own standalone rendering, while the plugin uses the host’s terminal. `camel.cli.version` and `aesh.version` pin the CLI host/parser separately from `camel.main.version`, which controls generated integration defaults. See [host compatibility](getting-started.html#cli-host).

## Definition of done

A change is finished when all of the following hold:

-   The tests of every touched module pass, and `./mvnw clean install` from the root passes when the change spans modules or touches skills, templates or `distribution.properties`.
    
-   `./mvnw -Psourcecheck validate` passes.
    
-   A skill, template or trait change passes `ShippedAssetStructureTest`, and the active documents pass `ResourceConsistencyTest` (see [the contract tests](architecture.html#equalization)).
    
-   Register each core skill in the workflow manifest and document its public command. Pack skills use their descriptor. Check the generated entry points for all eight agents.
    
-   No version is hardcoded where `distribution.properties` applies.
    
-   The documentation is updated, and `CHANGELOG.md` for significant changes.
    
-   Nothing was skipped, disabled or weakened to get a green build; a failing check is reported, not hidden.
    

Branches are named `feature/…​`, `fix/…​`, `docs/…​`, `command/…​` or `template/…​`. Rebase on `main` before opening a pull request, fill in the template, link the related issues and request a review. Commit messages are plain and descriptive.

## Adding a skill

A skill is a directory under `kit/camel-kit-core/src/main/resources/skills/` with a `SKILL.md` manifest (YAML front matter with `name`, `description` and `user_invocable`, then the steps and a guide table) and a `guides/` directory of instruction files loaded on demand. Every skill is registered in the workflow manifest `camel-kit-workflow.yaml`, which drives the generated command stubs, the trait application and the structural tests: a user-facing skill with its `generated_command`, documented in the command reference; an internal skill with `status: internal` and `generated_command: null`, referenced from the guide table of the skill that dispatches it. Shared guides under `skills/shared/` feed several skills, so check every caller before editing one. Agent-specific behaviour goes into trait files under `templates/traits/<agent>/`, which need no code registration. See [Skills system](skills.md) for the structure and the tiers.

## Contributing a skill pack

Put a descriptor in `src/main/resources/META-INF/camel-kit/packs/<id>/pack.yaml`. Resource paths in the descriptor are relative to that directory. Pack IDs and the names of skills, stages, steps and providers start with a lowercase ASCII letter and continue with lowercase letters, digits or hyphens. List selected pack IDs in the distribution build. The compiler always includes `core`. It supplies the bundled Mule and BizTalk adapters alongside the migration guides. A selected module can contain only instructions and resources.

The example distribution adds report guidance and a required route-coverage check to validation.

pack.yaml

```yaml
id: report-review
schema: 1
requires: [core]
add:
  step/validate/report/review:
    contract: 1
    resource: review.md
  skill/camel-review-coverage:
    contract: 1
    resource: coverage.md
    handles: [step/validate/report/coverage]
    requires: [resource/camel-review-coverage/guides/coverage.py]
  resource/camel-review-coverage/guides/coverage.py:
    contract: 1
    resource: coverage.py
  step/validate/report/coverage:
    contract: 1
    hook:
      handler: skill/camel-review-coverage
      targets: [quarkus, spring-boot]
      checks: {route-coverage: inventory}
```

review.md

```markdown
List the routes that the validation run covered and record any routes that still need review.
```

coverage.md

```markdown
---
name: camel-review-coverage
description: Check a validation suite's route inventory against a workflow hook request.
user_invocable: false
---

When invoked for the coverage hook, save the supplied request object as JSON in a temporary file.
From the project root, run `python3 <this skill directory>/guides/coverage.py <request file>`.
Return its JSON result to the caller for submission to Kit. The caller handles developer questions.
```

coverage.py

```python
"""Example skill helper. Run from the project root with the hook request as its argument."""
import json
import sys
from pathlib import Path


def review(request):
    decisions = request["decisions"]
    if not decisions:
        return {"request": request, "status": "needs-input",
                "question": "Which validation suite should cover these routes?"}

    suite = decisions[-1]["answer"]
    inventory = Path(request["artifacts"]["inventory"]["path"])
    rows = inventory.read_text(encoding="utf-8").splitlines()
    covered = {row.removeprefix(suite + "\t") for row in rows if row.startswith(suite + "\t")}
    missing = sorted(request["sources"].keys() - covered)
    evidence = (f"Suite {suite}: missing {', '.join(missing)}" if missing
                else f"Suite {suite} covers all {len(request['sources'])} scoped routes in {inventory}.")
    return {"request": request, "status": "failed" if missing else "passed",
            "checks": {"route-coverage": {"passed": not missing, "evidence": evidence}}}


if __name__ == "__main__":
    print(json.dumps(review(json.loads(Path(sys.argv[1]).read_text(encoding="utf-8")))))
```

### Composition rules

-   `schema: 1` versions the pack descriptor. Each added or replaced entry declares `contract: 1` for its contribution kind. A pack’s optional `requires` lists other selected pack IDs. A contribution’s optional `requires` lists other contribution keys that must survive composition. The compiler also tracks literal references in Markdown to declared guides, shared files and skill entry files. Declare indirect dependencies explicitly, including providers selected by name and commands invoked in prose. For example, a skill that directs users to `/camel-knowledge` declares `requires: [skill/camel-knowledge]`.
    
-   `add` maps new keys to declarations. `replace` maps existing keys to new declarations. `exclude` lists existing keys. Each key has one defining pack and at most one replacement or exclusion. A pack editing a key must declare a direct dependency on its defining pack. A provider replacement keeps its service interface and a skill replacement keeps its visibility. Separate guide entries survive an entry-file replacement.
    
-   Removing a skill also removes its command, generated route and resources supplied under that skill by its owner. A core workflow stage must retain its skill. Each artifact must retain every producing and consuming skill. Use `replace` to change the instructions for any of those skills. When a remaining instruction still names an excluded guide, the build reports the consumer, missing resource and excluding pack. Replace that instruction or keep the guide. The core router also declares the skills in its decision tree. Core supplies host-specific Ship delegates. A replacement owns the skill text for every host and must preserve delegation to the Ship controller. Excluding the Ship skill also removes Bob’s Ship mode. Native worker presets remain available to the independent `camel-kit ship --backend` command.
    
-   Resolve every requested module and single-origin resource on the build classpath. The compiler rejects duplicate keys, competing edits, dependency cycles, unknown targets, missing files and unsupported contracts before packaging. For example, if both `team-a` and `team-b` replace `step/validate/report/timestamp`, the diagnostic names both packs and the key. Select one replacement in the distribution.
    

 
| Contribution key | Declaration and effect |
| --- | --- |
| `skill/<name>` | Set `resource` to a Markdown entry with matching `name`, a nonempty `description` and boolean `user_invocable` in its YAML frontmatter. For a new skill, `true` creates a public entry and `false` creates an internal skill. Kit generates the host visibility flags. |
| `resource/<skill-or-shared>/<path>` | Set `resource` to the bundled file. Its key determines its destination beneath the assistant’s skills directory. Use `skill/<name>` for the top-level `SKILL.md`. On retirement, Kit ignores LF/CRLF differences in UTF-8 `.md`, `.adoc`, `.txt`, `.yaml`, `.yml`, `.json`, `.xml`, `.xsl`, `.sh`, `.toml` and `.properties` files. Other resources and files containing a NUL byte or invalid UTF-8 must match the recorded bytes exactly. |
| `step/<stage>/<step>/<name>` | Set `resource` to Markdown guidance or a check. The stage comes from the workflow manifest. Its skill must contain the line `<!-- camel-kit:step <step> -→` exactly once. The compiler inserts active contributions there in key order. Set `hook` to require an executable check at that point. Core exposes `route/choose` before the router’s decision tree and `validate/report` while preparing the report. |
| `provider/<name>` | Set `provider.service` and `provider.implementation` to fully qualified Java names. The compiler checks the public interface, a public concrete implementation and its public zero-argument constructor without initializing the class. Keep the provider classes on the distribution’s runtime classpath. |

For example, a validation pack can supply an alternate timestamp instruction and require a separately declared guide.

```yaml
id: team-report
schema: 1
requires: [core]
add:
  resource/camel-validate/guides/report-format.md:
    contract: 1
    resource: format.md
replace:
  step/validate/report/timestamp:
    contract: 1
    resource: timestamp.md
    requires: [resource/camel-validate/guides/report-format.md]
```

### Implement a workflow hook

A step declares either a guidance resource or a `hook`. Its `handler` selects one effective `skill/<id>` or `provider/<id>`. The handler advertises that step ID in its own `handles` list. The compiler checks the match and records the dependency. List supported target IDs in `targets` and map each mandatory check ID to an evidence artifact role in `checks`. Use the same lowercase ID syntax as pack IDs. A replacement can switch the implementation while preserving the targets and checks. An explicit `exclude` of the step removes both the hook and its invocation from that distribution. The handler remains available for other hooks. Each ID in `handles` must name a hook declared by the selected packs, including hooks explicitly excluded during composition.

The caller supplies project-relative file paths with `/` separators. Each source and evidence path must refer to a regular file within the project through directories without symbolic links. Artifact keys must match the declared roles exactly. The CLI prepares a version 1 request containing the step and handler identities, their owning packs, the assembled catalog SHA-256, the skill entry or Java class, target, source paths and SHA-256 digests, artifact paths and SHA-256 digests, check-to-role map and ordered list of confirmed questions and answers.

A skill returns a JSON object with the following fields. A Java implementation of `org.apache.camel.kit.workflow.WorkflowHookProvider` receives the project root and the same typed `Request` and returns a `Result`. Both handlers can call their own helpers.

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top">Field</td><td class="tableblock halign-left valign-top">Value</td></tr><tr><td class="tableblock halign-left valign-top"><code>request</code></td><td class="tableblock halign-left valign-top">Echo the entire request object supplied by Kit.</td></tr><tr><td class="tableblock halign-left valign-top"><code>status</code></td><td class="tableblock halign-left valign-top"><code>needs-input</code>, <code>failed</code> or <code>passed</code>.</td></tr><tr><td class="tableblock halign-left valign-top"><code>question</code></td><td class="tableblock halign-left valign-top">A nonblank question for <code>needs-input</code>. Omit or use <code>null</code> for a terminal result.</td></tr><tr><td class="tableblock halign-left valign-top"><code>checks</code></td><td class="tableblock halign-left valign-top">Omit or use an empty object while awaiting a decision. For a terminal result, provide exactly the declared IDs, each with a boolean <code>passed</code> and nonblank <code>evidence</code> describing the observation for its assigned artifact. A failure identifies at least one failed check.</td></tr></tbody></table>

For example, the bundled example skill reads the inventory as tab-separated suite and source-path pairs. It asks which suite to use, then checks that every source appears in that suite. Its Python helper returns `{"passed":false,"evidence":"Suite integration: missing routes/orders.yaml"}` under `checks.route-coverage` when the inventory omits the route. See [invocation and diagnostics](skills.html#workflow-hooks).

To use a compiled handler, package a public implementation with a public zero-argument constructor on the distribution classpath, declare it as below, and set the step’s `hook.handler` to `provider/coverage`.

```yaml
add:
  provider/coverage:
    contract: 1
    handles: [step/validate/report/coverage]
    provider:
      service: org.apache.camel.kit.workflow.WorkflowHookProvider
      implementation: example.CoverageProvider
```

### Build and try the example

From the repository root, build Kit and then package the example against the installed Kit version. The example POM binds `org.apache.camel.kit.workflow.SkillPackCompiler` to `process-classes` on the Maven runtime classpath. Its arguments are the output archive and a comma-separated list of selected IDs. In a multi-module distribution, add the pack JARs as dependencies of the module running the compiler.

```bash
./mvnw -B clean install
example="$PWD/docs/modules/ROOT/examples/skill-pack"
./mvnw -B -f "$example/pom.xml" -Dcamel-kit.version=0.4.2-SNAPSHOT \
  package dependency:build-classpath -Dmdep.outputFile="$example/target/classpath.txt"
classpath="$example/target/kit-with-report-review-1.0-SNAPSHOT.jar:$(cat "$example/target/classpath.txt")"
workspace=$(mktemp -d)
(
  cd "$workspace" || exit 1
  java -cp "$classpath" org.apache.camel.kit.CamelKitMain init --here --ai bob2 --no-fetch
  grep 'List the routes' .bob/skills/camel-validate/SKILL.md
  java -cp "$classpath" org.apache.camel.kit.CamelKitMain doctor
)
```

The example ships `META-INF/camel-kit/catalog.zip` in its JAR. A custom distribution supplies exactly one archive at that path. With the standard Kit alone, the loader uses `META-INF/camel-kit/default-catalog.zip`. To select additional packs while building core itself, add the pack modules as build/runtime dependencies and set `-Dcamel.kit.packs=pack-a,pack-b`. This property supplies the complete selection beyond core. See [how the catalog reaches the assistant](architecture.html#skill-packs).

### Contributing a migration parser

The `legacy-flows` example reads a legacy format in which each `.flow` file names one integration flow. Its pack descriptor registers a public Java class with a public zero-argument constructor. The contribution key gives the parser its stable ID. The inventory step requires both `provider/legacy-flow` for parsing and `provider/legacy` for analysis. This checks the dependency at build time. Include the runtime invocation and its failure handling in the step’s own instructions so the installed workflow checks the provider before consuming its graph. The pack compiler checks duplicate keys, dependencies, the contribution contract and the packaged classes.

```yaml
id: legacy-flows
schema: 1
requires: [core]
add:
  provider/legacy-flow:
    contract: 1
    provider:
      service: org.apache.camel.kit.graph.parser.MigrationParser
      implementation: example.LegacyFlowParser
  provider/legacy:
    contract: 1
    provider:
      service: org.apache.camel.kit.graph.model.GraphTypeAdapter
      implementation: example.LegacyGraphAdapter
  step/validate/report/legacy-inventory:
    contract: 1
    resource: inventory.md
    requires: [provider/legacy-flow, provider/legacy]
```

The example contributes these instructions at `validate/report`.

```markdown
For the legacy flow inventory, apply `shared/graph-availability.md` and use the installed `{COMMAND_PREFIX}`.
Run `graph generate --require-parser legacy-flow --project-dir SOURCE --output GRAPH` as separate argv elements.
Use the canonical source directory selected for validation as SOURCE and the graph destination authorized for this
validation as GRAPH. If either is missing, ask for it and leave the inventory incomplete.
Run the command even if a previous graph exists. On failure, report the diagnostic and leave the inventory incomplete.
Run `graph analyze legacy --graph-file GRAPH` with the same installed command prefix and authorized GRAPH.
If analysis fails, report the diagnostic and leave the inventory incomplete. On success report the adapter summary,
or zero legacy flows when the adapter returns `matched: false`.
```

Implement `org.apache.camel.kit.graph.parser.MigrationParser` from `org.apache.camel:camel-kit-graph`. Return the API version against which the provider was compiled. Kit checks it when constructing the graph builder. Declare lowercase input extensions without a dot. Discovery counts those files against the same byte budget as built-in sources. For formats sharing an extension, use `acceptsContent` to inspect a bounded candidate. Providers declaring `xml` receive all size-checked XML candidates, including `pom.xml`. Mule uses this check to recognize its XML namespace.

Kit passes all matching files in path order to `parseFiles` once, so a parser can resolve cross-file references. With zero matching files it skips that call. The fragment starts with Maven context. Emit graph nodes and edges using core or pack-owned types. Prefix pack-specific node IDs with a stable namespace to avoid collisions. Use `GraphParser.relativeFileName` to record source-relative `file` properties with forward slashes on every platform. The example projects its private `Flow` record onto a `legacy:flow` node and links it to its source file. Return per-file observations through `warnings()` and clear them in `resetWarnings()` if the parser keeps state. A thrown exception or timeout discards that parser’s fragment. Callers of `buildWithDiagnostics` can inspect the scanned paths, warnings, failures and produced counts alongside the graph. For migration providers, the scanned paths are the files selected for parsing. A failure or timeout before content selection finishes reports an empty list. Library callers using the graph artifact alone can pass their own ID-to-parser map to `new GraphBuilder(map)`. Supply a separate parser instance for each ID. The no-argument constructor retains the standard parser set, including Mule.

```java
package example;

import java.io.IOException;
import java.io.UncheckedIOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.List;
import java.util.Set;

import org.apache.camel.kit.graph.ProjectGraph;
import org.apache.camel.kit.graph.parser.GraphParser;
import org.apache.camel.kit.graph.parser.MigrationParser;

public class LegacyFlowParser implements MigrationParser {
    private final List<String> warnings = new ArrayList<>();

    @Override
    public int apiVersion() {
        return API_VERSION;
    }

    @Override
    public Set<String> inputExtensions() {
        return Set.of("flow");
    }

    @Override
    public void parseFiles(Path root, List<Path> files, ProjectGraph fragment) {
        GraphParser.requireSafeFiles(root, files);
        for (Path file : files) {
            String source = GraphParser.relativeFileName(root, file);
            try {
                var flow = new LegacyGraphAdapter.Flow(new String(GraphParser.readSource(file), StandardCharsets.UTF_8).strip(), source);
                if (flow.name().isEmpty()) {
                    warnings.add("Missing flow name in " + source);
                    continue;
                }
                flow.addTo(fragment);
            } catch (IOException e) {
                throw new UncheckedIOException("Cannot read " + source, e);
            }
        }
    }

    @Override
    public List<String> warnings() {
        return List.copyOf(warnings);
    }

    @Override
    public void resetWarnings() {
        warnings.clear();
    }
}
```

### Registering a graph adapter

Register the public, zero-argument implementation of `GraphTypeAdapter` as a `provider/<namespace>` contribution with contract 1. Its `nodeTypes()` and `edgeTypes()` map wire names to typed Java identifiers. Register a new type under its own name. For a legacy type, register the uppercase alias as the key and the canonical type as the value. Kit registers both names and rejects aliases that conflict with another mapping or a core type of the same kind. Kit registers core providers first and uses ascending namespace order within the core and optional groups. A conflicting or malformed adapter becomes unavailable as a whole. An alias conflict identifies both providers or the reserved core type. Other adapters and generic graph queries remain available. During `init`, an adapter failure produces a warning. Kit still saves the graph, reports the other summaries and detects the runtime. A pack can declare only types in its provider namespace. Both parts of `namespace:type` start with a lowercase ASCII letter and may contain lowercase letters, digits and hyphens.

Implement `summarize` using the pack’s domain rules. Return an empty optional for a graph without matching evidence. To set the position of a matching summary in the `init` output, override `summaryOrder()`. Lower values appear first. The default is zero, and ties retain registration order. Java callers migrating from the enum API must recompile. Replace enum switches and identity comparisons with value comparisons using `equals`. Resolve filter strings with `registry.nodeType(name)` or `registry.edgeType(name)`. The registry’s `nodeNames()` and `edgeNames()` list registered names and aliases. A saved graph may also contain unregistered types. Use `GraphSerializer.read(path, registry)` for alias resolution and `GraphSerializer.read(path)` to retain the original wire names. Both can read unknown types in a supported format.

```java
package example;

import java.util.Map;
import java.util.Optional;

import org.apache.camel.kit.graph.ProjectGraph;
import org.apache.camel.kit.graph.model.EdgeType;
import org.apache.camel.kit.graph.model.GraphTypeAdapter;
import org.apache.camel.kit.graph.model.GraphNode;
import org.apache.camel.kit.graph.model.GraphEdge;
import org.apache.camel.kit.graph.model.NodeType;

public final class LegacyGraphAdapter implements GraphTypeAdapter {
    static final NodeType FLOW = new NodeType("legacy:flow");
    static final EdgeType DECLARED_IN = new EdgeType("legacy:declared-in");

    record Flow(String name, String source) {
        void addTo(ProjectGraph graph) {
            String flowId = "legacy-flow:" + source;
            String fileId = "legacy-file:" + source;
            graph.addNode(new GraphNode(flowId, FLOW, Map.of("name", name, "file", source)));
            graph.addNode(new GraphNode(fileId, NodeType.RESOURCE_FILE, Map.of("file", source)));
            graph.addEdge(new GraphEdge(flowId, fileId, DECLARED_IN, Map.of()));
        }

        static Flow from(GraphNode node) {
            String name = node.properties().get("name");
            String file = node.properties().get("file");
            if (name == null || name.isBlank() || file == null || file.isBlank()) {
                throw new IllegalArgumentException("Legacy flow " + node.id() + " requires name and file properties");
            }
            return new Flow(name, file);
        }
    }

    @Override
    public Map<String, NodeType> nodeTypes() {
        return Map.of(FLOW.name(), FLOW);
    }

    @Override
    public Map<String, EdgeType> edgeTypes() {
        return Map.of(DECLARED_IN.name(), DECLARED_IN);
    }

    @Override
    public Optional<String> summarize(ProjectGraph graph) {
        var flows = graph.findByType(FLOW);
        if (flows.isEmpty()) {
            return Optional.empty();
        }
        long files = flows.stream().map(Flow::from).map(Flow::source).distinct().count();
        return Optional.of("Legacy flow inventory (flows=" + flows.size() + ", source files=" + files + ")");
    }
}
```

After installing Kit locally, run the example from the repository root. It uses the same example POM as the report-review pack and selects only `legacy-flows` in addition to core.

```bash
example="$PWD/docs/modules/ROOT/examples/skill-pack"
./mvnw -B -f "$example/pom.xml" -Dcamel-kit.version=0.4.2-SNAPSHOT \
  -Dexample.packs=legacy-flows clean package dependency:build-classpath -Dmdep.outputFile="$example/target/classpath.txt"
classpath="$example/target/kit-with-report-review-1.0-SNAPSHOT.jar:$(cat "$example/target/classpath.txt")"
workspace=$(mktemp -d)
(
  cd "$workspace" || exit 1
  java -cp "$classpath" org.apache.camel.kit.CamelKitMain init --here --ai claude --no-fetch --silent
  grep -F -- 'graph generate --require-parser legacy-flow' .claude/skills/camel-validate/SKILL.md
  echo Orders > orders.flow
  java -cp "$classpath" org.apache.camel.kit.CamelKitMain graph generate --require-parser legacy-flow
  java -cp "$classpath" org.apache.camel.kit.CamelKitMain graph find --type legacy:flow --name Orders
  java -cp "$classpath" org.apache.camel.kit.CamelKitMain graph analyze legacy
)
```

The result includes `legacy-flow:orders.flow` with `file=orders.flow`. Keep the Java classes on the Kit runtime classpath and rebuild the catalog with the distribution when upgrading Kit. Providers execute with the CLI’s permissions. Package trusted implementations and treat every source file as data. See [using the bundled Mule provider](graph.html#migration-parsers) for partial results and required-parser failures.

## Documentation

This site is built from `docs/antora.yml` and `docs/modules/` in the repository with Antora, as a component of the Apache Camel website; edit the `.adoc` pages there and keep versions in the attributes of `antora.yml`. The repository also keeps `docs/commands.md`, `docs/architecture.md` and `docs/constitution.md`, which the consistency tests read, and `docs/user-guide.md`; keep them in step with these pages when behaviour changes.

## Releasing

The shared parent, Kit and Knowledge have independent versions and release schedules. A product release references a published, released shared parent. All release jobs use Java 21. Kit release validation also requires a released `camel.cli.version` and a synchronized Maven mirror; snapshot and prerelease host pins cannot be staged. Verify the released Aesh-based host with the CLI compatibility suite. Use the corresponding POM (`pom.xml` with `-N`, `kit/pom.xml`, or `knowledge/pom.xml`) when preparing or staging a release; never deploy the root reactor to release one product.

Tags are `camel-kit-parent-X.Y.Z`, `camel-kit-X.Y.Z` and `camel-kit-knowledge-X.Y.Z`. `tools/release_target.py` validates the selected target, its module versions and its tag. The manually dispatched `Stage Maven Release` workflow checks the exact tag and reviewed commit SHA, tests and signs that target, and uploads a validated staging deployment. Automatic promotion is disabled.

Apache releases follow the [ASF release policy](https://www.apache.org/legal/release-policy.md) and the Camel [release guide](../../manual/release-guide.md), including a source release candidate and successful PMC vote before publication. The staging workflow does not automate that whole process. See `docs/releasing.md` in the repository for the preparation steps.

Kit pins a tested Knowledge runner using `knowledge.mcp.group-id` and `knowledge.mcp.version` in `distribution.properties`. Published Knowledge 0.0.2 retains its `io.github.luigidemasi` coordinates; migrated development builds use `org.apache.camel`. Adopting a new runner is explicit and does not require matching Kit and Knowledge versions. Synchronize Kit launchers from its POM with `./mvnw -B -f kit/pom.xml -N antrun:run@sync-jbang-launcher-versions`.

Index data is published independently under `knowledge-index-v1-YYYY.MM.DD-HHMMSS` tags. Maintainers rebuild it on a branch with `./mvnw -B -pl knowledge/index -am -Prebuild-index install`, review the generated data, and manually dispatch `Index Release` from `main` with the reviewed SHA. The workflow requires working vector retrieval and packages the reviewed index without regenerating it. See [Knowledge MCP](knowledge.md) for compatible discovery, explicit version pins and cache fallback.