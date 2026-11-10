# Supported AI agents

`camel-kit init --ai <target>` generates the project layout for one coding agent. All targets share the same Markdown skills; `init` adapts them with agent-specific traits and writes the agent’s native configuration, so the workflow is the same everywhere and only the way you invoke it differs.

  
| Agent | Init flag | Start the workflow |
| --- | --- | --- |
| Anthropic Claude Code | `--ai claude` | `/camel-start` |
| IBM Bob 2 (default) | `--ai bob2` | `$camel-start` in Bob Shell, `/camel-start` in Bob IDE |
| Google Antigravity | `--ai antigravity` | `/camel-start`, or ask for the `camel-start` skill by name |
| OpenAI Codex CLI | `--ai codex` | `$camel-start` after trusting the repository |
| GitHub Copilot CLI | `--ai copilot` | Ask Copilot to "Use the `/camel-start` skill" |
| Pi | `--ai pi` | `/skill:camel-start` after `/trust` |
| Qwen Code | `--ai qwen` | `/camel-start` |
| OpenCode | `--ai opencode` | `/camel-start` |

The generated assets and the MCP configuration file of each target are listed in [the overview](index.html#agents). Every target gets two MCP servers by default _(development snapshot; released versions include all three)_ — `camel` (catalog, route validation, migration and security analysis) and `camel-knowledge` (documentation, CVE, release and component search) — with an optional third, `citrus` (test actions, endpoints and schemas), enabled via `--with-citrus-mcp`. All are configured as local JBang processes whose versions come from the Camel Kit distribution. See [MCP servers](mcp.md).

The pipeline skills delegate independent implementation and review tasks to fresh subagent contexts where the agent supports it. Where it does not, the skills run inline in the main session and record the missing isolation in their reports.

## Anthropic Claude Code

`init` writes `CLAUDE.md` (which points to `AGENTS.md`), the slash commands under `.claude/commands/`, the skills under `.claude/skills/`, project settings in `.claude/settings.json` and the MCP servers in `.mcp.json`. Start with `/camel-start`. During `/camel-execute`, independent tasks of the same wave are dispatched to parallel subagents with isolated context windows.

## IBM Bob 2

Use `--ai bob2` for both Bob Shell and Bob IDE; the generated assets are verified with Bob Shell 2.0.2 and Bob IDE 2.1.0. `init` writes `.bob/custom_modes.yaml`, rules, the shared skills under `.bob/skills/`, scoped agent presets under `.bob/agents/`, the role personas under `.bob/personas/` and the MCP servers in `.bob/mcp.json`.

In Bob Shell, start from the project root, open `/skills` or type `$camel-`, and select one of the nine public skills: `camel-start`, `camel-brainstorm`, `camel-migrate`, `camel-plan`, `camel-execute`, `camel-validate`, `camel-ship`, `camel-knowledge` and `camel-debug`. Enter the request after the skill name:

$camel-migrate MuleSoft flows in src/main/mule

Bob Shell’s native skill picker uses `$camel-*`; its `/` picker holds built-in commands and MCP prompts, so a `/camel-*` name in this documentation corresponds to a `$camel-*` skill there. Bob IDE exposes the same skills as `/camel-*`. Legacy command stubs stay installed for compatibility. The four internal helper skills are hidden.

If a public skill does not appear in the picker, run `camel-kit doctor`: it reports each affected `SKILL.md` as `FAIL` with regeneration instructions. Regenerate from the project root with `camel-kit init --here --ai bob2 --force` (after committing or backing up customized generated files) and restart Bob.

## Google Antigravity

Install Antigravity following [Google’s getting-started guide](https://antigravity.google/docs/getting-started), then:

```bash
camel-kit init my-integration --ai antigravity
```

`init` writes `AGENTS.md`, the skills under `.agents/skills/`, three custom agents under `.agents/agents/` (`camel-worker` with file and sandboxed command tools, `camel-reviewer` with read and search tools plus the inherited MCP access, `camel-ship-worker` with read and search tools for Ship stages), the role personas under `.agents/camel-kit-personas/` and the MCP servers in `.agents/mcp_config.json` (two by default; three with `--with-citrus-mcp`). Open the project root in Antigravity and invoke `/camel-start` in the CLI, or ask it to use the `camel-start` skill by name; `/skills` lists the native skills and `/mcp` the connections.

The primary conversation owns questions, approvals, orchestration and report writes, and dispatches independent tasks with the native `invoke_subagent`; the children inherit the workspace permissions and MCP servers. Tool calls stay subject to Antigravity’s permissions: Camel Kit generates no auto-approval policy. Reinitialization preserves unrelated MCP servers, settings and comments in `mcp_config.json`, which must contain a JSON object (`{}` when empty).

## OpenAI Codex CLI

```bash
camel-kit init my-integration --ai codex
cd my-integration
codex
```

`init` writes `AGENTS.md`, the skills under `.agents/skills/`, the custom agent roles under `.codex/agents/` (planner, implementer, tester, validator, migrator, catalog researcher and security reviewer; the development snapshot adds a Ship worker) and the MCP servers in `.codex/config.toml` (two by default; three with `--with-citrus-mcp`). It does not create `.codex/commands/`: Codex discovers the skills directly, so you start with `$camel-start` after trusting the repository, and inspect skills with `/skills` and servers with `/mcp`.

Codex loads the repository `.codex/` configuration only for trusted projects. Review the repository before trusting it; until then the custom agents and the MCP servers are not active. The setup stays repository-scoped: Camel Kit does not edit `~/.codex/config.toml`, credentials or login state, generates no hooks, and does not loosen the sandbox or the approval policy. Keep the sandbox enabled and grant only the narrow approval needed when a command is blocked: repository trust lets the project configuration load, it is not a reason to approve every command. Each generated MCP server table carries an exact tool allowlist and `default_tools_approval_mode = "prompt"`. If `.codex/config.toml` already exists with valid unrelated settings they are preserved; invalid TOML or a conflicting server table makes `init` fail without changing the file.

`camel-kit doctor` validates the TOML, the server tables and their allowlists, the prompt approval defaults, the skills, the required custom-agent fields and the read-only sandbox of the research and security agents.

## GitHub Copilot CLI

`init` writes `.github/copilot-instructions.md`, the skills under `.github/skills/`, the custom agents under `.github/agents/`, the MCP servers in `.github/mcp.json` and a safety hook in `.github/hooks/camel-kit-safety.json` that denies destructive or secret-sensitive shell commands while leaving the normal permission prompts in place. Start by asking Copilot to "Use the `/camel-start` skill"; `/skills list` shows the project skills.

## Pi

```bash
camel-kit init my-integration --ai pi
cd my-integration
pi install npm:pi-mcp-adapter@2.11.0
```

`init` writes `AGENTS.md`, the skills under `.pi/skills/`, prompt templates under `.pi/prompts/`, `.mcp.json` for `pi-mcp-adapter`, and a guard extension (`.pi/extensions/camel-kit-guard.ts` with its JSON policy). In Pi, trust the project with `/trust`, then run `/skill:camel-start`. Headless checks must use `pi -a`.

Pi has no native subagents: the pipeline runs in the main session and records the missing isolation. For isolated read-only research, start a separate Pi session with constrained tools, for example `pi --tools read,grep,find,ls`, and bring the findings back.

## Qwen Code

`init` writes `QWEN.md`, the commands under `.qwen/commands/`, the skills under `.qwen/skills/`, five bounded leaf agents under `.qwen/agents/` (implementer, reviewer, tester, validator, ship-worker), the personas under `.qwen/camel-kit-personas/` and the MCP servers in `.qwen/settings.json`. Start with `/camel-start`. Interviews, approvals and phase handoffs stay in the primary session; only bounded work goes to the leaf agents. Eligible sessions relay Ship controller stages to the read-only `camel-ship-worker` named agent via `--backend qwen-native`; the worker returns structured results and artifact proposals without editing files or calling MCP tools.

## OpenCode

`init` writes `AGENTS.md`, the commands under `.opencode/commands/`, the skills under `.opencode/skills/`, the agent definitions under `.opencode/agents/`, the personas under `.opencode/camel-kit-personas/` and the MCP servers in `opencode.json`. Start with `/camel-start`. When a project configuration already exists (`opencode.json`, `opencode.jsonc`, or the same files under `.opencode/`), `init` preserves unrelated settings, permissions and MCP servers and writes its own entries to the highest-precedence file; invalid or conflicting configuration fails before any file is changed. The generated executor can delegate to allowlisted child agents one level deep; you can also address them directly with the `@agent-name` syntax.

OpenCode supports the native Ship backend. Eligible sessions that have the `subagent` tool available and the `camel-ship-worker` agent installed (generated by `init` under `.opencode/agents/`) dispatch controller tasks to a read-only worker child; the worker has `edit: deny`, `bash: deny` and `subagent: deny` permissions and denies all inherited MCP server tools via per-server glob rules. The `/camel-ship` command stub in `.opencode/commands/` is the entry point; the native skill handles dispatch and falls back to the existing CLI model when native dispatch is unavailable.

## Retired targets

Camel Kit 0.4.0 replaced the `gemini` target with Google Antigravity and removed IBM Bob v1. Reinitialize an existing project from its root with the replacement target, then check it:

```bash
# Former Gemini target
camel-kit init --here --ai antigravity --force

# Former IBM Bob v1 target
camel-kit init --here --ai bob2 --force

camel-kit doctor
```

Before reinitializing, `.agents/mcp_config.json` must be valid JSON without duplicate keys (`doctor` reports duplicates as failures), and `AGENTS.md`, `GEMINI.md` and everything under `.agents/` must be real files or directories, so replace symbolic links first; these checks run before any project file is changed. `--force` replaces the generated `AGENTS.md`, skills and configuration, so preserve custom additions to those files first; custom project rules can live in `GEMINI.md`, which Antigravity also reads. Antigravity reinitialization removes the four old Camel Kit `@.gemini/…​` imports from `GEMINI.md` and keeps custom text, imports and other `.gemini/` files. Move custom MCP servers from `.gemini/settings.json` to `.agents/mcp_config.json` using Google’s MCP schema, and custom skills from `.gemini/skills/<name>/` to `.agents/skills/<name>/`. Bob 2 reinitialization replaces the generated gate skills and modes with the shared pipeline and native subagents, removing only the known obsolete Bob v1 mode-rule files.