# camel-start

`/camel-start` is the entry point of the pipeline. It reads the request and the project state and loads only the stage or utility that applies, so an existing project can enter the pipeline midway without repeating completed work. The invocation form depends on the agent: `$camel-start` in Bob Shell and Codex, `/skill:camel-start` in Pi, "Use the `/camel-start` skill" in GitHub Copilot CLI, `/camel-start` elsewhere (see [Supported AI agents](agents.md)).

## Routing

The router answers these questions in order; the first "yes" wins.

  
| # | Request state | Route |
| --- | --- | --- |
| 1 | Existing MuleSoft, BizTalk, Fuse or Camel 2.x/3.x source to migrate | [`/camel-migrate`](migration.md) |
| 2 | An approved design specification ready for task decomposition | [`/camel-plan`](camel-plan.md) |
| 3 | An implementation plan derived from an approved design, ready to build | [`/camel-execute`](camel-execute.md) |
| 4 | Generated routes that need static quality validation | [`/camel-validate`](camel-validate.md) |
| 5 | A build, startup or runtime failure outside a pipeline run | [`/camel-debug`](camel-debug.md) |
| 6 | A new integration, a new feature, or an unclear request | [`/camel-brainstorm`](camel-brainstorm.md) |

Greenfield: /camel-brainstorm -> /camel-plan -> /camel-execute -> /camel-validate
Migration:  /camel-migrate    -> /camel-plan -> /camel-execute -> /camel-validate

Both pipelines share plan, execute and validate; only the design entry differs. Runtime verification runs inside execute (see [Runtime verification](verification.md)).

## Skill tiers

  
| Tier | Skills | Role |
| --- | --- | --- |
| Entry | `camel-start` | Routes to the right pipeline stage |
| Pipeline | `camel-brainstorm`, `camel-migrate`, `camel-plan`, `camel-execute`, `camel-validate` | Five skills for the four stages; brainstorm and migrate are the alternative design entries |
| Utilities | `camel-ship`, `camel-knowledge`, `camel-debug` | Standalone, usable at any time without changing the active pipeline state |
| Internal | `camel-design`, `camel-implement`, `camel-test`, `camel-verify` | Dispatched by the pipeline skills; not user-invocable |

## When not to use each skill

 
| Skill | Not for |
| --- | --- |
| `/camel-brainstorm` | Quick property changes, version bumps, single-component additions, Camel questions, migrations from another platform |
| `/camel-migrate` | Greenfield projects, Camel 4.x minor upgrades, projects without source artifacts to analyze |
| `/camel-plan` | Ad-hoc changes, single-file edits, quick fixes, or when no approved design exists |
| `/camel-execute` | When no plan derived from an approved design exists; Camel questions; validation-only tasks; design work |
| `/camel-validate` | Runtime debugging (build failures, startup errors), generating routes, design work, fixing the findings |
| `/camel-ship` | Single-file changes, quick fixes, exploratory work, or when only one pipeline stage is needed |
| `/camel-debug` | Build and test failures during `/camel-execute` (its own verification loop handles them), quality validation, design work |
| `/camel-knowledge` | Implementation, code generation, route validation, design work |

Use a stage directly when the destination is already known, for example `/camel-plan` with an approved design or `/camel-debug` for a broken route. Use `/camel-start` when the request is new or its current stage is uncertain.