# Install and first project

Camel Kit runs as a standalone command-line tool installed with JBang, or as a plugin of [Camel JBang](../../manual/camel-jbang.md). Both forms provide the same commands (`init`, `doctor`, `doc`, `graph`, `plan`, `nextId`, `ship`) and the same eight AI targets. The examples on this page use the standalone form, `camel-kit`; replace it with `camel kit` when you use the plugin.

## Prerequisites

  
| Requirement | Purpose | Install |
| --- | --- | --- |
| Java 17 or later | Runtime for Camel Kit, Camel JBang and the generated projects | SDKMAN, Adoptium or your package manager |
| [JBang](https://www.jbang.dev/) | Launcher for Camel Kit and for the MCP servers it configures | See the installation commands below |
| [Camel JBang](../../manual/camel-jbang.md) | `camel run` and `camel run --check` for route execution and validation | `jbang app install camel@apache/camel` |
| Camel JBang test plugin | `camel test run` for the Citrus integration tests in the verification loop | `camel plugin add test` |
| Docker (conditional) | Environment probes for external services and full Citrus/Testcontainers verification | Docker Engine or Docker Desktop |

Camel JBang and its test plugin are needed for the complete execution and verification loops. When Docker is not available, the checks that need containers are reported as skipped; design, planning and the container-free checks still work. `camel-kit init` checks Java, JBang, Camel JBang and the test plugin and reports missing tools as warnings without stopping.

## Release channels

This documentation follows the development branch (0.4.2-SNAPSHOT). The latest release is Camel Kit 0.4.1, which pairs with Knowledge MCP 0.0.2; features that are not in the release are marked as development snapshot only. Pin the release when you need a reproducible installation.

  
| Channel | Install source | Version |
| --- | --- | --- |
| Release | Tagged JBang catalog, or the Camel JBang plugin from Maven Central | `0.4.1` |
| Development | Unqualified JBang catalog alias, or a source build | `0.4.2-SNAPSHOT` |

The unqualified catalog alias follows the latest deployed snapshot, which may lag the `main` branch. Build from source for an exact revision.

## Install

-   Standalone (JBang)
    
-   Camel JBang plugin
    
-   Development snapshot
    
-   Build from source
    

```bash
# Install JBang (if not already installed)
curl -Ls https://sh.jbang.dev | bash -s - app setup        # Linux/macOS
iex "& { $(iwr -useb https://ps.jbang.dev) } app setup"    # Windows PowerShell

# Install the release globally
jbang app install camel-kit@luigidemasi/camel-kit/camel-kit-0.4.1

# Verify: prints 0.4.1
camel-kit --version
```

To run the release once without installing it:

```bash
jbang run camel-kit@luigidemasi/camel-kit/camel-kit-0.4.1 \
  init my-integration --ai claude
```

```bash
camel plugin add kit \
  --gav io.github.luigidemasi:camel-jbang-plugin-kit:0.4.1 \
  --description "Design Apache Camel Integrations with AI"

camel kit init my-integration --ai claude
```

```bash
# Latest deployed 0.4.2-SNAPSHOT
jbang app install --force camel-kit@luigidemasi/camel-kit
```

```bash
git clone https://github.com/apache/camel-kit.git
cd camel-kit
./mvnw -B clean install

# Install the development version globally via JBang
jbang app install --name camel-kit --force \
  kit/camel-kit-main/src/main/jbang/main/CamelKit.java

# Or install the matching Camel JBang plugin from the local Maven repository
camel plugin add kit \
  --gav org.apache.camel:camel-jbang-plugin-kit:0.4.2-SNAPSHOT \
  --description "Design Apache Camel Integrations with AI"

camel-kit --help
```

The Knowledge MCP server is built from `knowledge/` in the same repository. To build it independently:

```bash
./mvnw -B -f knowledge/pom.xml clean install
java -Dknowledge.index.path=knowledge/index/src/main/resources/knowledge-index \
  -jar knowledge/mcp/target/camel-kit-knowledge-mcp-0.0.3-SNAPSHOT-runner.jar
```

Source-built Knowledge uses `org.apache.camel` Maven coordinates and Java packages under `org.apache.camel.kit.knowledge`. Kit retains its published server pin until explicitly changed. For a local integration check, initialize a disposable workspace with `-p knowledge.mcp.group-id=org.apache.camel -p knowledge.mcp.version=0.0.3-SNAPSHOT`.

> **Note**
> The released 0.4.1 artifacts are published under the JBang catalog `luigidemasi/camel-kit` and the Maven coordinate `io.github.luigidemasi:camel-jbang-plugin-kit`. Development snapshots built from `apache/camel-kit` use the `org.apache.camel` group. The first release from the Apache repository will change the release coordinates; this page is updated with it.

## Upgrading

Reinstall the standalone CLI with `jbang app install --force` and the release alias above, or run the plugin installation again. To apply updated generated assets to an existing project, commit or back up customized generated files, then run `camel-kit init --here --ai <your-agent> --force` from the project root. This rewrites the generated assets, except shared files you changed (see [Existing projects](#existing-project)).

From 0.4.0

Camel Main, Camel Spring Boot and Camel MCP default to Camel 4.22.1; the supported older LTS patch is 4.18.4. Spring Boot uses 4.1.1. Camel 4.22.1 maps to Forage 1.6.1. Version 0.4.1 also updates the shared generation and review guidance to prefer verified declarative bean construction after Forage and component configuration (see [Forage configuration catalog](forage.md)), and Knowledge MCP 0.0.2 validates endpoints against the Camel 4.22.1 catalog.

From 0.3.1

The `gemini` and `bob` targets were removed in 0.4.0 and replaced by `antigravity` and `bob2` (the default). Reinitialize with the replacement target; see [Retired targets](agents.html#retired-targets).

## Create a project

```bash
camel-kit init my-integration --ai claude
cd my-integration
```

`init` creates the directory, runs the prerequisite check, and generates the shared project files plus the agent-native assets selected by `--ai` (see [Supported AI agents](agents.md) for the eight targets; `bob2` is the default). To add Camel Kit to an existing directory, for example a project to migrate, run it with `--here`:

```bash
camel-kit init --here --ai claude --source-platform mulesoft
```

If the directory already contains `.camel-kit/`, `init` warns and exits; pass `--force` to reinitialize. An `AGENTS.md` of your own does not block `init`.

### Existing projects

`init` does not replace files an existing project already owns. Application sources, `pom.xml` and other build files are never written. Files that both a project and Camel Kit may provide are handled in one of two ways.

Instruction files are merged

`AGENTS.md`, `CLAUDE.md`, `QWEN.md` and `.github/copilot-instructions.md` hold Camel Kit’s content inside a marked block:

<!-- CAMEL-KIT-MANAGED-BLOCK-START: camel-kit-generated -->
...
<!-- CAMEL-KIT-MANAGED-BLOCK-END: camel-kit-generated -->

In a file that has no block, `init` appends one after your content. On later runs it replaces only the block, so keep your own text outside it. A file whose block lost one of its markers is preserved as described below.

Other shared files are written only while they are Camel Kit’s

`docs/constitution.md`, `.claude/settings.json`, `.qwenignore`, `.bob/custom_modes.yaml` and the Maven wrapper (`mvnw`, `mvnw.cmd`, `.mvn/wrapper/maven-wrapper.properties`) are written when missing or still identical to what Camel Kit last wrote. A project without a wrapper gets the complete one. Once any wrapper file is the project’s own, Camel Kit adds no further wrapper file and writes only the ones named with `--replace`.

A shared file that was not written by Camel Kit, or was changed afterwards, is left untouched and listed under _Existing files preserved_ at the end of the run. The version Camel Kit would have written is saved under `.camel-kit/conflicts/` at the same relative path, so you can merge it by hand. To let Camel Kit replace a file in full, name it explicitly:

```bash
camel-kit init --here --ai claude --force --replace docs/constitution.md
```

To see what a run would do to these files without writing anything, add `--dry-run`:

```bash
camel-kit init --here --ai claude --dry-run
```

An existing JSON MCP configuration is merged: Camel Kit adds or updates its own servers and keeps other servers and settings. A file that is not valid JSON stops `init` before any project file is changed. On reinitialization, properties you added to `.camel-kit/config.properties` are kept.

Camel Kit records the hash of each tracked file it wrote in `.camel-kit/managed-files.properties`; commit it with the project. Known limits:

-   Files Camel Kit ships under its own names, such as the `camel-*` skills, subagents, personas and `.camel-kit/templates/`, are regenerated on every run; changes to them are not preserved. Your own skills and files next to them are not touched.
    
-   A workspace initialized by an earlier Camel Kit has no ledger, and a missing record never counts as ownership. On its first reinitialization the unmarked instruction files get the block appended and the other shared files are preserved and reported, even if Camel Kit generated them. Replace those you want refreshed with `--replace <path>`.
    
    What every target gets
    
-   `AGENTS.md`, or the agent’s equivalent entry file, with the routing table for the skills.
    
-   The agent-native skills and entry points, for example `.claude/commands/` and `.claude/skills/` for Claude Code, or `.agents/skills/` for Codex.
    
-   `docs/constitution.md`, the architecture rules every generated route must follow (see [Constitution](constitution.md)).
    
-   `docs/flows/`, `test/data/` and `schemas/`, empty scaffolds; pipeline artifacts use the selected runtime’s paths.
    
-   `.camel-kit/` with the project configuration, cached catalogs and templates, and later the pipeline state.
    
-   The MCP configuration for the target: JSON for most agents, `.codex/config.toml` for Codex, `.mcp.json` read through `pi-mcp-adapter` for Pi.
    
-   `mvnw`, `mvnw.cmd` and `.mvn/wrapper/maven-wrapper.properties`, created for new projects or when missing. For existing projects with a Maven wrapper, the existing wrapper is preserved unless `--replace-wrapper` is specified.
    

### Using Camel Kit with Existing Projects

Camel Kit can enhance **existing Camel 4 applications** in addition to creating new projects. When you run `init` on a directory with an existing `pom.xml`:

-   Your `pom.xml`, existing routes, and configuration are **preserved**
    
-   Camel Kit detects your Camel version, runtime (Spring Boot, Quarkus, etc.), and DSL type
    
-   The Maven wrapper is **skipped** if it already exists
    
-   Skills are added; the files Camel Kit ships are refreshed on reinit, and files you add are never touched
    

The workflow is the same (`/camel-start` → `/camel-brainstorm` → `/camel-plan` → `/camel-execute` → `/camel-validate`), but with additional safeguards:

-   **Scope protection** - only approved files are modified
    
-   **Baseline validation** - the per-test baseline is captured before the first edit, and later compared test by test
    
-   **Version locking** - the versions your pom declares are recorded and not upgraded
    

See [Adding Capabilities to Existing Camel Applications](existing-project.md) for the complete guide with a worked example.

> **Tip**
> Use `--dry-run` to preview changes before initializing: `camel-kit init --here --ai claude --dry-run`

### Configuration

All defaults (Camel version, BOM versions, MCP server versions) come from the `distribution.properties` file bundled in Camel Kit. Three layers override them, the later winning:

1.  the built-in defaults;
    
2.  `~/.camel-kit/config.properties`, or the file given with `-c`;
    
3.  `-p key=value` flags, repeatable.
    

```bash
camel-kit init my-integration --ai claude -p "camel.main.version=4.18.4"
camel-kit init my-integration --ai claude -c /path/to/my-config.properties
```

The most common keys are `camel.main.version`, `camel.springboot.version`, `camel.quarkus.version`, `quarkus.platform.version`, `knowledge.mcp.version` and `citrus.version`. See [Command reference](commands.md) for the full option list, including `--no-fetch` and `--silent`.

### Check the workspace

```bash
camel-kit doctor
camel-kit doctor --json   # for automation
```

`doctor` checks the generated configuration, command stubs where the target uses them, skill files, MCP filtering and permission fields, the project graph, the command prefix, the prerequisites and common stale generated references. It prints `PASS`, `WARN` and `FAIL` findings with remediation text. Missing external tools such as JBang are warnings; broken generated workspace files are failures.

## Run the first command

Open your coding agent in the project directory and start the router:

/camel-start

`/camel-start` reads the project state and routes to the right stage: migration for an existing MuleSoft, BizTalk, Fuse or Camel 2.x/3.x source, planning for an approved design, execution for a plan, validation for generated routes, debugging for a broken project outside a pipeline, and the design interview for everything else. You can also describe the work in plain words, for example "I want to build an integration that reads from Kafka and writes to a database"; the agent reads the routing table and invokes the skill.

The invocation form depends on the agent: `/camel-start` in Claude Code, Bob IDE, Antigravity, Qwen and OpenCode; `$camel-start` in Bob Shell and Codex; "Use the `/camel-start` skill" in GitHub Copilot CLI; `/skill:camel-start` in Pi. See [Supported AI agents](agents.md).

The first pipeline run needs an active pipeline ID. `init` does not create one, so the agent asks you to create it before the interview continues:

```bash
camel-kit nextId kafka-to-database
# Output: 001-kafka-to-database
```

The ID names the directory under `docs/camel-kit/` where the pipeline artifacts are written, so you can close the session and resume later.

## Where to go next

-   [Greenfield workflow](greenfield.md) builds a new integration from requirements to verified routes.
    
-   [Migration workflow](migration.md) converts an existing MuleSoft, BizTalk, Fuse or Camel 2.x/3.x project.
    
-   [Stages, approval gate and Iron Laws](pipeline.md) explains the stages, the single approval gate and the Iron Laws.
    
-   [Command reference](commands.md) lists every CLI and slash command option.