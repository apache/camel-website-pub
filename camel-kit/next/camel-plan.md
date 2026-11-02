# camel-plan

`/camel-plan` is the planning stage. It turns the approved design specification into an implementation plan: a task-by-task recipe with acceptance criteria, the components and guides each task uses, dependency waves and a two-stage review specification. The plan describes what to generate and how to verify it; it never contains the generated routes, properties, dependencies or tests, so that `/camel-execute` always generates them from the current guides and catalog.

In a chained run the design approval in `/camel-brainstorm` or `/camel-migrate` invokes `/camel-plan` directly, and the plan hands off to `/camel-execute` without a second approval. Invoked standalone (`/camel-plan` or `/camel-plan <pipeline-id>`), it reads `design-spec.md` from disk, checks its provenance and staleness with `camel-kit doc check`, writes the plan and stops; a stale or unverified design stops the skill until you choose to amend it, abort, or plan from that exact revision.

Do not use it for ad-hoc changes, single-file edits or quick fixes, when no approved design exists, or to generate code.

## Input

The planner reads all sections of `docs/camel-kit/<pipeline-id>/design-spec.md`: the executive summary for the goal and constraints, the systems landscape for the external systems, the flow designs for the implementation tasks and contracts, the cross-cutting concerns for errors, security, resilience, observability and configuration, the constitution compliance section with its catalog verification evidence, and the project structure for the runtime-specific layout. A migration design adds the migration context section.

The **Not Doing (and Why)** list is binding: the planner never creates a task or an acceptance criterion for an excluded capability. If another approved section requires one, planning stops so the contradiction can be resolved and re-approved, instead of passing an impossible plan to execution.

If the design covers several independent subsystems or more than about ten flows, the planner suggests one plan per subsystem, each producing working software on its own.

## How the plan is built

1.  **Templates.** The planner loads the greenfield or the migration task template plus the testing template, and emits one Citrus test task per flow after the implementation tasks it depends on.
    
2.  **Flow-to-task mapping.** Each flow becomes one or more tasks; a routing decision with several destinations becomes several route tasks, following the separation-of-concerns rule. Scaffold, configuration, runtime dependency and conditional infrastructure tasks complete the plan.
    
3.  **Acceptance criteria.** Each task states what "done" means in checkable terms, for example "listens at `/api/orders`, POST, returns 202" or "queries PostgreSQL with `sql`, sets the `credit-status` header, retries three times with exponential backoff". The spec compliance review checks the generated artifact against these criteria.
    
4.  **Components, guides and tools.** Each task lists the Camel artifacts it uses, the guides the implementer loads and the catalog tool calls with the runtime and platform BOM parameters.
    
5.  **Dependencies and waves.** Tasks declare the files they create or modify, the logical resources they provide and consume (routes, endpoints, properties, schemas, test data, beans, external services, route contracts) and explicit dependencies. `camel-kit plan analyze` derives the waves from them.
    
6.  **Self-review.** Every flow maps to a task, no placeholders or "similar to task N", every guide path exists, every task has both review stages and a verification step with an exact command and expected result.
    

## Plan format

The plan is written to `docs/camel-kit/<pipeline-id>/implementation-plan.md` with provenance front matter added by `camel-kit doc init`. A fenced block with the info string `yaml plan-metadata` precedes the first task and holds one entry per task:

```yaml
tasks:
  - id: 2
    title: Order intake route
    files:
      creates:
        - src/main/resources/camel/order-intake.camel.yaml
    provides:
      routes:
        - order-intake
      endpoints:
        - direct:validate-order
    consumes:
      properties:
        - orders.api.path
    dependsOn: [1]
```

Each `# Task N` section then carries the execution recipe:

```markdown
### Task 2: Order intake route

**Agent:** implementation-engineer

**Files:**
- Create: `src/main/resources/camel/order-intake.camel.yaml`

**Guides to Load:**
- `camel-implement/guides/orchestrator.md`
- `camel-implement/guides/yaml-structure.md`

**MCP Tools:**
- `camel_catalog_component_doc(component="platform-http", runtime="spring-boot", ...)`

**Design Spec Section:** Section 3, Flow: order-intake

- [ ] **Step 1:** ...
- [ ] **Step N:** Verify with `<command>` and expect `<result>`

**Review:**
- [ ] Spec compliance: components and structure match the design
- [ ] Code quality: constitution rules, security, anti-patterns
```

The agent persona is one of `integration-architect`, `implementation-engineer`, `migration-specialist` or `test-engineer`. Plans must contain no `TBD`, deferred work, vague steps, implicit file paths, or verification without an exact command and expected result. Older Markdown-only plans still execute; new plans always carry the metadata block.

## Waves

`camel-kit plan analyze <plan>` sorts the tasks topologically: tasks with no dependencies form wave 1, the tasks that depend only on them form wave 2, and so on. Tasks in the same wave touch different files and are concurrency candidates: agents with independent subagent conversations run them in parallel, the others run them sequentially in plan order. A later wave never starts before its dependencies complete. A circular dependency is reported as an error that names the tasks involved.

A task depends on another when it consumes its data (a lookup result used for enrichment), when it is invoked by it (a route consuming from a queue the first route feeds), or when the plan declares it explicitly. Independent flows, such as a REST endpoint and a scheduled synchronization, share a wave.

Wave 1: Task 1 (runtime configuration and dependencies)
Wave 2: Task 2 (order intake route)
Wave 3: Task 3 (credit lookup route), Task 7 (invalid-order publisher)
Wave 4: Task 4 (routing decision)
Wave 5: Task 5 (warehouse publisher), Task 6 (pending-order publisher)

## Two-stage review specification

Every implementation task ends with a review section for Iron Law 4: spec compliance first (are all acceptance criteria met, does the route do what the task says, are the declared components used), then code quality (the eight constitution rules, security, anti-patterns). A task that fails the first stage goes back to its implementer without a quality review. Project-specific checks, for example "no hardcoded secrets", can be added to the generated plan skill’s task template; the two stages and their order stay.

## Handoff and reuse

After saving the plan the skill adds the provenance metadata, marks existing downstream artifacts stale with `camel-kit doc stale --cascade`, and then either invokes `/camel-execute` (chained mode) or prints the next command and stops (standalone mode). Agent traits can replace the default handoff, for example Claude Code stays out of its native plan mode so that no second approval appears.

The plan stays valid while its design is unchanged. After a transient environment failure, fix the environment and rerun `/camel-execute <pipeline-id>`; execution restarts from the first task because there is no task-level resume. If the design changes, amend it with `/camel-brainstorm <pipeline-id>` and regenerate the stale plan before executing again.