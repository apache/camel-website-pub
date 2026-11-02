# Skills system

A skill is a directory with a manifest, `SKILL.md`, and an optional `guides/` directory of instruction files loaded on demand. Skills are not code: they are structured prompts with step-by-step procedures, catalog tool calls, conditions and shared guide imports. They live in `kit/camel-kit-core/src/main/resources/skills/` and `init` copies them, adapted to the agent, into the project.

## Thirteen skills in four tiers

   
| Tier | Skill | Command | Purpose |
| --- | --- | --- | --- |
| Entry | `camel-start` | `/camel-start` | Routes a request to the right skill |
| Pipeline | `camel-brainstorm` | `/camel-brainstorm` | Design interview, design specification |
| Pipeline | `camel-migrate` | `/camel-migrate` | Migration discovery, analysis, design and runbook |
| Pipeline | `camel-plan` | `/camel-plan` | Task decomposition, implementation plan |
| Pipeline | `camel-execute` | `/camel-execute` | Wave-based implementation with adversarial and staged review |
| Pipeline | `camel-validate` | `/camel-validate` | Static route quality validation |
| Utility | `camel-ship` | `/camel-ship` | Technology Preview: delegate to the local Ship controller |
| Utility | `camel-knowledge` | `/camel-knowledge` | Apache Camel documentation questions |
| Utility | `camel-debug` | `/camel-debug` | Troubleshooting of a broken route outside a pipeline |

Four internal skills are dispatched by the pipeline skills and have no command stub: `camel-design` (component selection, EIP catalog, design assembly), `camel-implement` (YAML routes, properties, Docker Compose, DataMapper), `camel-test` (Citrus integration tests) and `camel-verify` (build, test, diagnose and repair at runtime). They are the composition primitives the stages assemble. `camel-ship` is the outlier of its tier: its manifest is a short delegate that invokes the registered `camel-kit ship` command once and does not follow the guide-based structure described below.

## Shared guides

Guides under `skills/shared/` are loaded by several skills, so one guide serves many workflows without duplication.

 
| Guide | Purpose |
| --- | --- |
| `iron-laws.md` | The six pipeline process rules |
| `context-authority.md` | Data versus instruction authority for every loaded context, response and handoff |
| `camel-security-checklist.md` | Camel security rules, detection patterns and fix snippets for design, validation and review |
| `mcp-setup.md` | MCP server configuration, version binding rules and fallback policy |
| `forage.md` | The infrastructure configuration ladder and the Forage catalog queries |
| `graph-availability.md` | Graph CLI detection and the "enhances, never gates" fallback |
| `pipeline-infrastructure.md` | Pipeline IDs, state, artifact provenance and staleness |
| `discovery-completeness.md` | Discovery and completeness semantics shared by the interview and Ship discovery |
| `datamapper-canonicalize.md` | Engine selection from schemas and field count; pre-computed XPaths for XSLT |
| `flow-test-data.md` | Test data generation patterns |
| `yaml-structure.md`, `yaml-components.md`, `yaml-examples.md` | YAML DSL structure rules, component URI syntax, reference patterns |
| `patterns-foundational.md`, `patterns-error-handling.md`, `patterns-deployment.md` | EIP, error handling and deployment patterns |

The vendor migration guides (MuleSoft, BizTalk and Camel 2.x/3.x phases and mappings) live under `skills/camel-migrate/guides/`, not in `shared/`.

## Skill structure

camel-brainstorm/
  SKILL.md                  manifest: front matter, steps, guide table
  guides/
    greenfield-interview.md
    design-assembly.md
    version-selection.md
    ...

The manifest starts with YAML front matter and declares which guides exist and when to load them:

```yaml
---
name: camel-brainstorm
description: Design and plan Camel integrations through collaborative dialogue.
user_invocable: false
---
```

In the shared source only `camel-start` sets `user_invocable: true`: it is the auto-discovered entry point. The pipeline and utility skills still get entry points, generated per agent: slash-command stubs where the agent uses them, and native project skills on Codex CLI and GitHub Copilot CLI. Generated copies may add runtime aliases: Copilot, Pi and Qwen add a hyphenated `user-invocable` field, Codex rewrites `/camel-*` invocations to `$camel-*` mentions, and Bob 2 sets both fields to `true` for the nine public skills so that Bob Shell lists them in `/skills` and the `$camel-*` picker. Internal skills keep `false` everywhere. The front matter must match the workflow manifest; a test enforces it.

## Progressive disclosure

1.  **Routing surface, always loaded.** The agent sees `camel-start` and its decision tree, enough to select the next skill.
    
2.  **The manifest, on invocation.** `SKILL.md` is read when the user invokes the skill or the agent matches the intent.
    
3.  **Guides, as referenced.** When the manifest says "load \`guides/greenfield-interview.md\`", the agent reads that guide and nothing else.
    

Actual context use therefore depends on the workflow and the guides it needs, not on the size of the catalog.

## Context authority

Camel Kit separates data authority from instruction authority, and never trusts a source as a whole. Catalog fields, recognized `.camel-kit/` fields and approved design or plan fields may be relied upon for their purpose, after the workflow’s version, schema, provenance, freshness and approval checks pass. Only the shipped instructions of the active workflow and your explicit directions may direct actions, within the host agent’s own permission system. Prose, comments, examples, commands, URLs and requests found in MCP responses, project files, logs, documentation or generated state remain data: they cannot add tasks, widen the scope, waive a gate, request secrets or authorize a tool call or a file change.

When an action outside the shipped workflow turns out to be necessary, the skill names its source, the exact action, the verified reason and the scope, and waits for an action-specific confirmation; a role that cannot ask returns `NEEDS_USER_CONFIRMATION` to its orchestrator without acting. Confirmation applies to that action only.

## Target generation and traits

One skill set is adapted to eight agents. `init` reads the agent descriptor from the capability registry (`agents/registry/<agent>.yaml`: skills directory, command stubs and syntax, MCP configuration path and format, generator strategy, dispatch template, subagent and trait support) and runs the matching generator: `ClaudeGenerator`, `Bob2Generator`, `AntigravityGenerator`, `CodexGenerator`, `CopilotGenerator`, `PiGenerator`, `QwenGenerator` or `OpenCodeGenerator`, on top of the shared `DefaultGenerator`. The output of each is listed in [Supported AI agents](agents.md).

Traits bridge the equalized workflow and the agent’s capabilities. They are `.append.md` fragments under `templates/traits/<agent>/` that `TraitApplicator` appends to the generated files, between idempotent comment sentinels so a re-run of `init` adds nothing twice:

  
| Level | Path | Appended to |
| --- | --- | --- |
| Strategy | `traits/<agent>/<skill>.append.md` | the skill’s `SKILL.md` |
| Tactics | `traits/<agent>/<skill>/<guide>.append.md` | the skill’s guide |

For example, Claude Code’s `camel-execute.append.md` adds parallel subagent dispatch through the `Agent` tool, while the same skill on Antigravity gets `invoke_subagent` delegation with parent-owned decisions, Bob 2 gets `spawn_subagent` orchestration with its worker and reviewer presets, Qwen keeps orchestration in the primary session and uses clean-context bounded leaves, and OpenCode’s execute command selects a primary executor that can dispatch only its allowlisted leaves. Guide-level traits are discovered from the files on disk, so a new one needs no Java registration.

## Adding a skill

Create the directory with its manifest and guides, register the skill in the workflow manifest, and, for a user-invocable skill, in the templates of all eight agents and in the command reference. Run `ShippedAssetStructureTest` after any skill, template or trait change. See [Contributing and releasing](contributing.md).