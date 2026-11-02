# Ship workflow (Technology Preview)

> **Important**
> Camel Ship is a Technology Preview. It is still being stabilized, its behaviour and interfaces may change, and it is not recommended for production use. This applies to every Ship backend: tested host and runtime combinations and passing checks do not mean production readiness. For the established staged workflow, start with `/camel-start`.

Ship is a local workflow controller. The command `camel-kit ship` (or `camel kit ship` with the Camel JBang plugin) starts, inspects, resumes or aborts a run on your machine. One run takes an integration from requirements to published code through five controller-owned stages: discovery, design, plan, execute and validate. The agent entry points (`/camel-ship`, `$camel-ship`, `/skill:camel-ship`) are thin delegates: they forward your options to the registered command once and add nothing. The controller, not the agent, owns the stages, the run state, the oversight pauses, the evidence, the publication and the recovery; it never stores its state in the manual pipeline file.

Ship is a local orchestrator. It is not a daemon, a secrets service, a hostile-process sandbox or a release attestation system. Provider credentials stay with the active agent host or the external Pi worker; Ship does not persist them or write them into arguments, logs, reports or project artifacts.

Use it when you want one resumable run from requirements to validated, published code, when you need to resume an interrupted run by its ID, or when you have an approved manual design and want the controller to start at planning. Do not use it for single-file changes, quick fixes, exploratory work, or when only one pipeline stage is needed.

## Requirements

-   A Linux host.
    
-   A Camel Main project with YAML DSL routes named `<routeId>.camel.yaml`, Simple expressions, no Java artifacts, and one Citrus test per route at `test/<routeId>.camel.it.yaml`. Spring Boot and Quarkus projects are rejected until deterministic evidence support exists for them.
    
-   For the default Pi backend, the Pi and Node executables, found on `PATH` or given with `--pi` and `--node`. The maintained versions are Pi `0.84.2` or `0.83.0` with Node `22.22.2`; any other version is labelled experimental and runs only with `--accept-experimental`, and a version with a known missing capability is rejected.
    
-   Outbound access to Maven Central for the catalog and validation payloads.
    

Ship targets Camel Main at the configured `camel.main.version`: a `-p camel.main.version=…​` override, then the `-c` file or `~/.camel-kit/config.properties`, then the bundled default.

## Command and options

camel-kit ship \[--text TEXT\]... \[--document PATH\]... \[--ask always|smart|never\]
               \[--start-from STAGE\]
camel-kit ship --resume RUN\_ID | --status RUN\_ID | --abort RUN\_ID
camel-kit ship --submit RUN\_ID --result PATH \[--json\]

Context is optional: a bare `camel-kit ship` starts a short discovery conversation. Text and documents are added to the discovery input before any question, and open points come back as grouped unresolved questions.

  
| Option | Default | Description |
| --- | --- | --- |
| `--text TEXT` |  | Text context, repeatable |
| `--document PATH` |  | Document context, repeatable |
| `--ask POLICY` | `smart` | Oversight for a new run: `always`, `smart` or `never` |
| `--resume RUN_ID` |  | Resume a run; `--text` and `--document` add context to a paused run |
| `--status RUN_ID` |  | Read the latest durable state without starting the workflow runtime |
| `--abort RUN_ID` |  | Abort a run that has not completed; aborted runs cannot be resumed |
| `--start-from STAGE` |  | Start a new run at `discovery`, `design` or `plan` |
| `--backend MODE` | `pi` | `pi`, `bob2-native`, `copilot-native`, `claude-native`, `antigravity-native`, `qwen-native` or, in the development snapshot, `codex-native`; a run keeps its mode for its lifetime |
| `--json` | off | Structured run state and any pending native task |
| `--submit RUN_ID --result PATH` |  | Relay one native child result |
| `--pi PATH`, `--node PATH` | found on `PATH` | Executables for the Pi backend; rejected for native runs |
| `--maven-repository PATH` | under the state directory | Private Maven repository for the validation payloads |
| `--stage-timeout DURATION` | `10m` | Limit for one stage attempt, for example `90s` or `1h` |
| `--accept-experimental` | off | Continue after the warning for an experimental Pi or Node version |
| `-c`, `--config PATH` | `~/.camel-kit/config.properties` | Configuration file |
| `-p`, `--property KEY=VALUE` |  | Configuration override, repeatable |

`--resume`, `--status`, `--abort`, `--submit` and `--start-from` are mutually exclusive. Runtime and configuration options apply when starting, resuming or submitting; repeat `--stage-timeout`, `--maven-repository` and `-c`/`-p` on every resume and submission, because they are not persisted. With `--json`, a failed workflow returns the run state with exit code 1; some command errors return only stderr.

## Oversight

 
| Policy | Where the controller pauses |
| --- | --- |
| `always` | After design, plan, execute and validate, including before publication, and on material ambiguity |
| `smart` | After plan (before any implementation) and after execute, and on material ambiguity; a fully passing validation proceeds to guarded publication |
| `never` | Never for ambiguity: the worker records each unanswered question with the default it applied. The run still stops for missing tools, failed mandatory checks or authority you did not grant |

Unanswered questions and applied defaults are kept per stage and listed in the final summary and in `--status`; later stages receive them as worker-reported context, not as human-confirmed answers. Under `always` and `smart`, answer a paused question with `--resume <run-id> --text "…​"`.

## Stages

1.  **Discovery** gathers the requirements from the supplied context or a short conversation. Read-only for your sources.
    
2.  **Design** produces the integration design from the discovery output. Read-only.
    
3.  **Plan** decomposes the design into an implementation plan. Read-only; `smart` pauses here.
    
4.  **Execute** implements the plan in a controller-owned staged copy of the project prepared from a baseline snapshot. The live project is not modified, and changed files containing known secrets from the environment are rejected.
    
5.  **Validate** is deterministic and controller-owned: route and artifact policy, catalog and schema validation, dependency and runtime consistency, direct JVM YAML validation, Camel Main resolution and startup, and the required Citrus tests. The commands run in a separate JVM with a pinned, controller-resolved classpath, a scrubbed environment and a frozen read-only copy of the accepted tree; in-memory stubs replace every non-direct endpoint, so no application I/O leaves the machine, while catalog resolution may still download from Maven Central. No worker prose decides the outcome.
    

The result of validation is the **Stamp**: a local run report with a pass or fail status derived from the required checks. For each command it records the executable and its version, the redacted arguments, the exit status and timing, and the retained logs with their digests. A failed mandatory check fails the run under every policy; there is no waiver. The Stamp describes what ran on this machine and is not a signed attestation.

## Run state, resume and publication

Run state lives under `.camel-kit/ship/state/` in the project, or under `CAMEL_KIT_SHIP_STATE_HOME`. The `.camel-kit/ship/` subtree is reserved for the controller: never copied into the staged workspace, never part of the staleness digests, never published, and ignored by its own `.gitignore`. Git discovery stops at the staged workspace, so commands run by the execute worker or by validation do not see the project’s repository; for that reason project and state paths containing a colon are rejected. Runs recorded by pre-0.4.0 development builds under the user state directory are found only when `CAMEL_KIT_SHIP_STATE_HOME` points there.

Each run prints its ID. `--status` shows the stage, the policy, any pause report and the next actionable command. `--resume` re-reads the recorded inputs and artifacts, compares their digests, and restarts the earliest stale or incomplete stage; later stages are reset, so your own edits are detected rather than ignored. Context can be added only to a paused run; adding it after validation restarts from discovery and discards the Stamp, with a warning first.

`--start-from design` needs text or document context and a manual active pipeline in `.camel-kit/pipeline.json`; `--start-from plan` also imports that pipeline’s approved `design-spec.md`. Existing plans, execution reports and validation reports cannot be imported, and starting from execute or validate is unsupported because those stages need the controller’s own plan and evidence.

Accepted changes reach the live project only after the configured approval and validation gates. Before applying anything the controller re-verifies every completed stage as recorded and checks that the live tree has not changed; a changed tree stops publication and asks you to resume. The apply is journaled: if it is interrupted, the next locked mutating operation attempts a rollback first, and may stop for manual resolution. Ordinary process interruption is recoverable with the run ID; OS or power loss is not guaranteed against, and the invoking OS account is trusted.

## Native subagents

With the Pi backend, Ship runs an external Pi worker. Eligible IBM Bob 2, GitHub Copilot CLI, Claude Code and Google Antigravity and Qwen Code sessions can instead relay the controller’s stage tasks to their own read-only native subagents; OpenAI Codex CLI joins them in the development snapshot. The contract is the same for every host:

1.  The controller creates one pending task with its run, stage, attempt, input digest, deadline and a unique task ID, and returns to the parent session.
    
2.  The parent dispatches a fresh `camel-ship-worker` child with the controller’s complete prompt, copied verbatim, and submits the observed result through `ship --submit RUN_ID --result PATH --json`.
    
3.  The worker never edits project files, writes to the candidate or the state directory, calls MCP servers, delegates or publishes. On Bob 2, Copilot CLI, Claude Code, Antigravity and Qwen Code it has read and search tools only; on Codex CLI it may use the host’s file-reading means, shell commands included, for the named inputs and sources, under the host’s permissions. For execute it returns complete text proposals for the approved route and test paths, `pom.xml` and `.camel-kit/config.properties`; arbitrary extra resources, binary files and deletions are outside the contract.
    
4.  The controller validates the proposals, writes its private candidate, computes the hashes and runs the mandatory checks. A returned child result is a transport result, not proof that validation passed. Only the controller advances a stage or pauses.
    

The skill selects the native backend for an eligible new run unless you choose one explicitly; when native dispatch is unavailable, a new run keeps the Pi model, and an existing run keeps its recorded backend for its lifetime: hosts never switch during recovery. Native stages use the active session’s authentication and model; Camel Kit starts no second host process and does not look for Pi or Node. Host versions are caller-reported diagnostics, not a certification.

 
| Host | Specifics |
| --- | --- |
| IBM Bob 2 | `$camel-ship` in Bob Shell, `/camel-ship` in Bob IDE, in the normal agent mode or the generated Camel Ship mode. The parent calls `spawn_subagent` with the `camel-ship-worker` preset and `fork_context: false`; the preset has only read tools. Interactive sign-in is sufficient. Accepted on Bob Shell 2.0.2 on Linux on 2026-09-09. |
| GitHub Copilot CLI | `/camel-ship` from the generated skill in a trusted session that exposes `task` and the `camel-ship-worker` custom agent; the worker allows only the `read` and `search` aliases. Plan mode allows `--status` only. Accepted on Copilot CLI 1.0.83 on Linux on 2026-09-09. |
| Claude Code | `/camel-ship` from `.claude/skills/` in a trusted session that exposes the `Agent` tool and the `camel-ship-worker` subagent, which declares exactly `tools: Read, Grep, Glob`. The skill never leaves plan mode or changes the permission mode, and the generated settings do not pre-approve the Ship command. Accepted on Claude Code 2.1.267 on Linux on 2026-09-10. |
| OpenAI Codex CLI (development snapshot only) | `$camel-ship` in a trusted session with the `camel_ship_worker` custom agent, declared with `sandbox_mode = "read-only"` and no MCP servers. Where the host does not enforce the sandbox, the worker’s instructions are the operative restriction. If `--backend codex-native` is requested and dispatch is unavailable the skill stops without starting a run. |
| Google Antigravity | `/camel-ship` from the generated skill in a session that exposes `invoke_subagent` and the `camel-ship-worker` custom agent, which declares `commandExecutionPolicy: "off"`, `inheritMcp: false` and only read and search tools. Unlike the general `camel-worker` and `camel-reviewer` agents, the Ship worker does not inherit MCP servers. The skill respects Antigravity’s permission prompts and sandbox settings. |
| Qwen Code | `/camel-ship` from the generated skill in a session that exposes the `camel-ship-worker` named agent, which declares `approvalMode: default`, an explicit read-only `tools:` allowlist and `disallowedTools: [agent]`. The skill never uses `fork` or `fork_turns`; dispatch is through the named-agent mechanism. If `--backend qwen-native` is requested and dispatch is unavailable the skill stops without starting a run. Generated skill and worker assets verified on Qwen Code 0.25.3 (parser/command-loader probe); live child execution acceptance is pending. |

A fresh context is not an OS sandbox: read access follows the parent’s permitted paths. Do not broaden permissions, add directories or substitute another role when a task cannot reach its inputs.

Recovery is shared. After an interruption inspect `--status --json`, wait for a still-running child or submit its saved response, and never dispatch the same pending task twice. A task keeps its deadline; `--resume` after expiry fails that attempt and a second explicit resume issues a new task. `handoff-read-failed` means the pending task could not be verified: resume once to record the failure, then resume again for a fresh task, without editing the stored evidence. Ship cannot stop a host-owned child; use the host’s cancellation controls, and `--abort` invalidates the run and rejects late results. Failed runs return JSON with exit code 1 and `run.message`; stop after any command error, including `stale-stage-input` or a permission denial, and wait for a new instruction.

## Entry points per agent

-   **Claude Code** and **GitHub Copilot CLI** expose `/camel-ship` through their skill directories and relay eligible runs to their read-only worker; Claude Code’s compatibility command stub only points at the skill.
    
-   **IBM Bob 2** exposes the native skill as `$camel-ship` in Bob Shell and `/camel-ship` in Bob IDE.
    
-   **OpenAI Codex CLI** exposes `$camel-ship` with no generated command file.
    
-   **Google Antigravity** exposes `/camel-ship` through its skills directory and relays eligible runs to its read-only worker via `invoke_subagent`.
    
-   **Qwen Code** exposes `/camel-ship` through its skills directory and relays eligible runs to its read-only worker via named-agent dispatch.
    
-   **OpenCode** generates a `/camel-ship` command stub that forwards the options once.
    
-   **Pi** exposes Ship only as `/skill:camel-ship`; there is deliberately no `/camel-ship` prompt, because Pi’s prompt expansion flattens quoted option values.
    

Workspaces generated before the controller-owned Ship must be regenerated with the same agent and command surface (`camel-kit init --here --ai <same-agent> --force`, after backing up customizations). Re-initialization installs the current entry point and removes the obsolete prompt-owned Ship guides. A pre-controller `.camel-kit/ship-state.json`, or a `.camel-kit/pipeline.json` not in manual mode, makes Ship fail closed: archive it outside the project first.

## Examples

```bash
# No context: a short discovery conversation
camel-kit ship

# Document and text context, pausing at every gate
camel-kit ship --document requirements.md --text "Prefer YAML; no Java" --ask always

# Resume, answer an open question, inspect, abort
camel-kit ship --resume <run-id>
camel-kit ship --resume <run-id> --text "Use eu-west-1"
camel-kit ship --status <run-id>
camel-kit ship --abort <run-id>

# Import the active manual design and start at planning
camel-kit ship --start-from plan

# The same through the agent entry points
/camel-ship --document requirements.md
$camel-ship --document requirements.md
/skill:camel-ship --document requirements.md
```

## Ship and the manual pipeline

  
|  | Manual pipeline | Ship |
| --- | --- | --- |
| Who runs the stages | The agent; chained stages hand off automatically | The local controller |
| Approval gates | One, the design approval | By policy: after plan and execute (`smart`), at every stage (`always`), or none for ambiguity (`never`); missing tools, failed checks and ungranted authority always stop |
| Resume | From the artifacts on disk, by stage | By run ID, from the earliest stale stage |
| Where changes happen | The working tree | A staged workspace, published after the gates |
| Runtimes | Camel Main, Spring Boot, Quarkus | Camel Main with YAML DSL |

Maintainers run the Pi live gate manually with the `linux-ship-certification` Maven profile and the `CAMEL_KIT_SHIP_LIVE_PI` and `CAMEL_KIT_SHIP_LIVE_NODE` variables; it is not part of CI and not something users run.