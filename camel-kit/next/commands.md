# Command reference

Camel Kit has two command surfaces: the CLI, run in a terminal, and the skills, invoked inside the coding agent. The CLI is `camel-kit` when installed standalone and `camel kit` when installed as a Camel JBang plugin; both provide the same commands. `camel-kit --version` prints the version. The skill invocation form depends on the agent: `/camel-start` in Claude Code, Bob IDE, Antigravity, Qwen Code and OpenCode, `$camel-start` in Bob Shell and Codex CLI, "Use the `/camel-start` skill" in GitHub Copilot CLI, `/skill:camel-start` in Pi (see [Supported AI agents](agents.md)).

## CLI commands

### init

Creates a project, or adds Camel Kit to the current directory with `--here`. See [Create a project](getting-started.html#init) for what is generated.

camel-kit init <project-name> \[options\]
camel-kit init --here \[options\]

  
| Option | Default | Description |
| --- | --- | --- |
| `--ai`, `-a` | `bob2` | Coding agent to configure: `bob2`, `antigravity`, `claude`, `codex`, `copilot`, `pi`, `qwen` or `opencode` |
| `--here` | `false` | Initialize in the current directory |
| `--force` | `false` | Overwrite an existing project (one with `AGENTS.md` or `.camel-kit/`) without prompting |
| `--source-platform` | `auto` | Source platform of a migration: `mulesoft`, `biztalk`, `camel` or `auto` |
| `--citrus-version` | the configured `citrus.version` (5.0.1) | Citrus version for the test schemas and the generated test dependencies |
| `--with-citrus-mcp` | `false` | _(development snapshot only)_ Include the Citrus MCP server in agent configuration. When omitted, no Citrus server is generated; use this flag if your project needs Citrus test integration. Released versions (0.4.1 and earlier) include Citrus by default. |
| `--no-fetch` | `false` | Skip the external catalog fetch |
| `-p`, `--property` |  | Override a configuration property, repeatable: `-p "camel.main.version=4.18.4"` |
| `-c`, `--config` | `~/.camel-kit/config.properties` | Configuration properties file |
| `--silent` | `false` | No banner, TUI, progress or summary, for scripted use |

Configuration is read in three layers, the later overriding the earlier: the built-in `distribution.properties`, the user file given with `-c` or at its default path, and the `-p` flags. Any distribution property can be overridden; the common ones are `camel.main.version`, `camel.springboot.version`, `springboot.bom.version`, `camel.quarkus.version`, `quarkus.platform.version`, `camel.mcp.version`, `knowledge.mcp.group-id`, `knowledge.mcp.version`, `citrus.version` and `citrus.mcp.version`. The selected runtime and versions are persisted in `.camel-kit/config.properties`.

The default Knowledge runner is the published 0.0.2 artifact under `io.github.luigidemasi`. To use a migrated source build, override both `knowledge.mcp.group-id=org.apache.camel` and `knowledge.mcp.version=0.0.3-SNAPSHOT`. Changing the group alone would request an artifact that was never published.

`init` checks Java, JBang, Camel JBang and the Camel test plugin and reports missing tools as warnings; it never fails on them. On terminals with a native image protocol it shows a split-screen progress view, falling back to coloured text elsewhere.

### doctor

Validates a generated workspace and prints `PASS`, `WARN` and `FAIL` findings with remediation text. Missing external prerequisites are warnings; broken generated files are failures and return exit code 1.

camel-kit doctor \[--project-dir <path>\] \[--json\]

It checks `.camel-kit/config.properties`, the command stubs where the target uses them, the skill directories and manifests, the registered workspace templates, the exposure of user-invocable commands, the MCP filtering and permission fields the runtime supports, graph availability, the command prefix, the prerequisites and common stale references in generated files. Target specifics: for Codex it parses `.codex/config.toml`, the exact MCP allowlists, the prompt approval modes and the required fields of every custom-agent file; for Bob 2 it fails each public skill hidden by `user-invocable: false`; for Qwen it checks `includeTools` and `trust`; for OpenCode it evaluates all configuration layers as one and names the file that defines each rule. Configurations that predate the current filter and permission fields produce upgrade warnings; malformed current ones fail. Internal skills must exist as skills but must not be exposed as command stubs.

In the development snapshot, Citrus MCP configuration is optional. When the project has not opted in, `doctor` accepts a missing `citrus` entry; when opted in, a missing entry is a failure. Any existing Citrus entry is validated, including the tool filtering and permission fields supported by the target. An invalid entry produces a `FAIL` finding and exit code 1 even when the project has not opted in. These checks inspect configuration without starting the Citrus server or testing its availability. For compatibility, projects with `citrus.mcp.version` but no `citrus.mcp.enabled` are treated as opted in.

### nextId

Creates the next numbered pipeline directory under `docs/camel-kit/` and prints its ID. The slug is lowercase letters, digits and single hyphens.

$ camel-kit nextId order-processing
001-order-processing
$ camel-kit nextId inventory-sync
002-inventory-sync

Exit code 1 means an invalid slug or a directory that could not be created.

### doc

Manages the provenance and staleness of pipeline artifacts through YAML front matter.

camel-kit doc init --by <skill> \[--from <source>\] <file>
camel-kit doc check <file>
camel-kit doc stale --reason "..." \[--cascade\] <file>
camel-kit doc unstale <file>

Each artifact carries two blocks: `generated` (when, by which skill, from which upstream artifact; written once by `doc init`, which is idempotent) and `staleness` (written by `doc stale` and `doc unstale`). `doc check` prints the state as JSON and exits 0 whether or not the file is stale; a file without front matter reports `stale: false`. Every subcommand exits 1 on a missing file, an I/O failure or invalid arguments such as a blank `--reason`. `doc stale` always marks its target; with `--cascade` it also walks the sibling files whose `generated.from` names the target and marks them stale, recursively. After amending a design, mark each direct child separately (the implementation plan, and the migration runbook for migration pipelines) rather than the fresh design itself.

```bash
camel-kit doc init --by camel-plan --from design-spec.md \
  docs/camel-kit/001-order-processing/implementation-plan.md
camel-kit doc init --by camel-brainstorm \
  docs/camel-kit/001-order-processing/design-spec.md
camel-kit doc check docs/camel-kit/001-order-processing/implementation-plan.md
camel-kit doc stale --reason "design spec was amended" --cascade \
  docs/camel-kit/001-order-processing/implementation-plan.md
camel-kit doc unstale docs/camel-kit/001-order-processing/implementation-plan.md
```

### graph

Builds and queries the project’s property graph, persisted at `.camel-kit/project-graph.json`.

camel-kit graph generate                      # build or rebuild the graph
camel-kit graph stats                         # availability, node and edge counts
camel-kit graph find --type CAMEL\_ROUTE       # nodes by type, name or ID
camel-kit graph neighbors <node-id>           # connected nodes
camel-kit graph path <from> <to>              # shortest path
camel-kit graph subgraph <node-id>            # the subgraph around a node
camel-kit graph route-flow <route-id>         # ordered steps of a route
camel-kit graph impact <node-id>              # bounded transitive reachability
camel-kit graph route-topology                # route-to-route connections
camel-kit graph dead-code                     # structural retirement candidates
camel-kit graph project-norms                 # naming, error-handling and step norms
camel-kit graph project-context               # context for implementation
camel-kit graph route-context <route-id>      # context for testing
camel-kit graph migration-context <route-id> \[--depth N\]
camel-kit graph visualize                     # interactive HTML page

See [Graph intelligence](graph.html#commands) for what each command returns.

### plan analyze

Reads the `yaml plan-metadata` block of an implementation plan (falling back to the Markdown tasks for older plans) and prints the dependency waves and the task dependencies as JSON. `/camel-execute` runs it before dispatching tasks; see [Waves](camel-plan.html#waves).

camel-kit plan analyze docs/camel-kit/001-order-processing/implementation-plan.md

### ship

Starts, inspects, resumes or aborts a Ship run (Technology Preview). The full option table, the oversight policies, the state and recovery rules and the examples are on the [Ship page](ship.html#command).

camel-kit ship \[--text TEXT\]... \[--document PATH\]... \[--ask always|smart|never\]
               \[--start-from STAGE\]
camel-kit ship --resume RUN\_ID | --status RUN\_ID | --abort RUN\_ID
camel-kit ship --submit RUN\_ID --result PATH \[--json\]

## Skills

  
| Command | Purpose | Page |
| --- | --- | --- |
| `/camel-start` | Routes the request to the right stage or utility | [camel-start](camel-start.md) |
| `/camel-brainstorm` | Design interview and design specification; `/camel-brainstorm <pipeline-id>` runs standalone, or amends an existing design | [camel-brainstorm](camel-brainstorm.md) |
| `/camel-migrate` | Migration discovery, analysis, design and runbook; `--direct` implements concrete deliverables directly (development snapshot only) | [Migration workflow](migration.md) |
| `/camel-plan` | Implementation plan from the approved design; `/camel-plan <pipeline-id>` runs standalone | [camel-plan](camel-plan.md) |
| `/camel-execute` | Wave-based implementation with adversarial, spec and quality reviews and one runtime verification pass; `/camel-execute <pipeline-id>` runs standalone | [camel-execute](camel-execute.md) |
| `/camel-validate` | Static quality report of the generated routes; with a pipeline ID, the active pipeline, or the whole project | [camel-validate](camel-validate.md) |
| `/camel-ship` | Forwards its options once to `camel-kit ship` (Technology Preview) | [Ship workflow (Technology Preview)](ship.md) |
| `/camel-knowledge` | Apache Camel documentation questions through the Knowledge MCP server | [Knowledge MCP](knowledge.html#skill) |
| `/camel-debug` | Diagnosis and repair of a broken route outside a pipeline | [camel-debug](camel-debug.md) |

In a chained run started with `/camel-start`, or with `/camel-brainstorm` or `/camel-migrate` without a pipeline ID, the stages hand off to each other after the single design approval. A stage invoked with a pipeline ID reads its input from disk, writes its artifact and stops. The internal skills (`camel-design`, `camel-implement`, `camel-test`, `camel-verify`) have no command; see [Internal skills](pipeline.html#internal-skills).

## Cheat sheet

\# CLI
camel-kit init my-project --ai claude            # create a project
camel-kit init --here --ai claude --source-platform mulesoft
camel-kit doctor                                 # validate the workspace
camel-kit nextId order-processing                # next pipeline ID
camel-kit doc check docs/camel-kit/001-order-processing/design-spec.md
camel-kit graph stats                            # is the graph available?
camel-kit plan analyze docs/camel-kit/001-order-processing/implementation-plan.md
camel-kit ship --document requirements.md        # Technology Preview

# In the agent
/camel-start                                     # route the request
/camel-brainstorm   /camel-migrate               # design stage
/camel-plan         /camel-execute   /camel-validate
/camel-knowledge    /camel-debug     /camel-ship