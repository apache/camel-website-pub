# Camel Kit

![Camel Kit logo](_images/camel-kit-logo.png)

Camel Kit adds structured workflows for Apache Camel integration development to AI coding assistants. It guides an assistant through the integration lifecycle: requirements and design, planning, implementation, testing, and runtime verification, and it checks every component and option against the Camel catalog while it does so. It is available as a standalone command-line tool and as a Camel JBang plugin, and it generates the same skills for several coding agents.

This documentation follows the development branch of Camel Kit (0.4.2-SNAPSHOT). The latest release is Camel Kit 0.4.1 with Knowledge MCP 0.0.2, which target Camel 4.22.1; features that are not in the release are marked as development snapshot only.

## What it does

-   **AI-guided design.** Slash commands run a structured interview and produce a versionable design specification.
    
-   **Platform migration.** Detects the source platform and converts MuleSoft 3.x and 4.x, Microsoft BizTalk, Camel 2.x and 3.x, and JBoss Fuse projects to Camel 4 with YAML DSL routes.
    
-   **Catalog verification over MCP.** Components, endpoint options and infrastructure `forage.*` keys are verified against the Camel catalog and the Forage catalog at design and review time.
    
-   **Graph intelligence.** Nine parsers and two post-processors build a dependency-injection-aware property graph of the codebase for analysis and migration context.
    
-   **Runtime verification.** Build, startup and test checks run in the real environment; failures are classified, fixed within a bounded retry budget, and reported.
    
-   **Several AI agents.** The same skills are generated for eight coding agents (see [Supported AI agents](#agents)).
    

## The workflow

Entry:       /camel-start       routes to migration, planning,
                                execution, validation, debugging or
                                greenfield work based on context

Greenfield:  /camel-brainstorm  then the shared stages below
Migration:   /camel-migrate     then the shared stages below

Shared:      /camel-plan -> /camel-execute -> /camel-validate
                              |- implements (camel-implement)
                              |- verifies   (camel-verify, internal)
                              '- tests      (camel-test)

Utilities:   /camel-ship        Technology Preview: delegates to the
                                local Ship controller
             /camel-knowledge   documentation Q&A
             /camel-debug       standalone troubleshooting

 
| Command | Purpose |
| --- | --- |
| `/camel-start` | Entry point. Routes migration sources to migrate, approved designs to plan, ready plans to execute, generated routes to validate, broken projects outside a pipeline to debug, and other work to brainstorm. |
| `/camel-brainstorm` | Interactive design session that produces business requirements and a design specification. |
| `/camel-migrate` | Migration from MuleSoft, Microsoft BizTalk, legacy Camel or JBoss Fuse to Camel 4. |
| `/camel-plan` | Reviews the approved design and creates an implementation plan with wave analysis for parallel execution. |
| `/camel-execute` | Orchestrated execution: probes the environment, implements tasks in dependency waves, runs adversarial, spec and quality reviews, and performs the applicable smoke and runtime verification. |
| `/camel-validate` | Final static quality gate, or a standalone project check: schema, endpoints, quality, security, anti-patterns and constitution compliance, without modifying routes. |
| `/camel-debug` | Standalone troubleshooting outside a pipeline for broken routes, build failures, startup errors and runtime exceptions. |
| `/camel-ship` | Technology Preview. Thin entry point for the local Ship controller, which owns the end-to-end run with configurable oversight (`always`, `smart`, `never`). |
| `/camel-knowledge` | Documentation Q&A: semantic search over the Camel documentation, CVE advisories, release notes and the component catalog. |

See [Stages, approval gate and Iron Laws](pipeline.md) for the stages, the approval gate and the Iron Laws, and [Command reference](commands.md) for every option.

## Supported AI agents

`camel-kit init --ai <target>` generates the project layout for one agent. Each row is an alternative layout, not one combined tree. All targets share the same Markdown skills, adapted through agent-specific traits and native configuration.

   
| Agent | Init flag | Primary generated assets | MCP configuration |
| --- | --- | --- | --- |
| Anthropic Claude Code | `--ai claude` | `CLAUDE.md`, `.claude/commands/`, `.claude/skills/` | `.mcp.json` |
| IBM Bob 2 (default) | `--ai bob2` | `.bob/custom_modes.yaml`, rules, `.bob/skills/`, `.bob/agents/`, `.bob/personas/` | `.bob/mcp.json` |
| Google Antigravity | `--ai antigravity` | `AGENTS.md`, `.agents/skills/`, `.agents/agents/`, `.agents/camel-kit-personas/` | `.agents/mcp_config.json` |
| OpenAI Codex CLI | `--ai codex` | `AGENTS.md`, `.agents/skills/`, `.codex/agents/` | `.codex/config.toml` |
| GitHub Copilot CLI | `--ai copilot` | `.github/copilot-instructions.md`, `.github/agents/`, `.github/skills/` | `.github/mcp.json` |
| Pi | `--ai pi` | `AGENTS.md`, `.pi/skills/`, `.pi/prompts/`, guard extension and policy | `.mcp.json` via `pi-mcp-adapter` |
| Qwen | `--ai qwen` | `QWEN.md`, `.qwen/commands/`, `.qwen/skills/`, `.qwen/agents/`, `.qwen/camel-kit-personas/` | `.qwen/settings.json` |
| OpenCode | `--ai opencode` | `AGENTS.md`, `.opencode/commands/`, `.opencode/skills/`, `.opencode/agents/`, `.opencode/camel-kit-personas/` | `opencode.json` |

See [Supported AI agents](agents.md) for per-agent setup notes.

## How it is built

Camel Kit has four layers:

1.  **Agent instructions.** A generated `AGENTS.md` (or the agent’s equivalent) routes requests to the right skill; this is the cross-agent equalization layer.
    
2.  **Skills.** Composable Markdown instructions, loaded progressively: metadata first, the skill when triggered, shared guides only when referenced.
    
3.  **MCP servers.** Catalog verification, Citrus test guidance and documentation search, queried on demand instead of loading catalogs into the agent’s context.
    
4.  **Graph CLI.** Optional code intelligence for analysis and migration.
    

In the agent-run workflow the prompt is the product: generated instructions own the integration behaviour, and the compiled CLI supplies initialization, configuration, helper commands and the graph. The Ship workflow is the deliberate exception: its controller (stages, run state, oversight, evidence, guarded publication) is compiled code, and `/camel-ship` only delegates to it. See [Architecture overview](architecture.md).

## Where to go next

-   [Install and first project](getting-started.md) installs the standalone CLI or the Camel JBang plugin and creates a first project.
    
-   [Greenfield workflow](greenfield.md) and [Migration workflow](migration.md) walk through the two workflows end to end.
    
-   [Ship workflow (Technology Preview)](ship.md) describes the Technology Preview controller-owned workflow.
    
-   Source code and issue tracker: [apache/camel-kit](https://github.com/apache/camel-kit).