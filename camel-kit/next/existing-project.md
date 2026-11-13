# Adding Capabilities to Existing Camel Applications

Learn how to use Camel Kit to add new capabilities to your existing Apache Camel 4 applications without disrupting working code.

> **Tip**
> A runnable example fixture is available at [`fixtures/existing-project-spring-boot`](https://github.com/apache/camel-kit/tree/main/kit/camel-kit-core/src/test/resources/fixtures/existing-project-spring-boot) with a complete workflow example in [`fixtures/existing-project-example-workflow`](https://github.com/apache/camel-kit/tree/main/kit/camel-kit-core/src/test/resources/fixtures/existing-project-example-workflow).

## Overview

Camel Kit can enhance **existing Camel 4 applications** in addition to creating new greenfield projects. When you run `init` on an existing project, Camel Kit:

-   Detects your current Camel version, runtime, and DSL
    
-   Preserves your `pom.xml`, existing routes, and configuration (init writes none of them)
    
-   Adds Camel Kit skills; the shipped skill, guide and shared files are refreshed on every reinit, and files you add next to them are never touched
    
-   Records the versions your pom declares and uses them instead of upgrading or choosing others
    

The workflow follows the same **design → plan → execute → validate** pipeline, but with additional safeguards to protect existing functionality.

## Prerequisites

Your existing project must meet these requirements:

-   **Camel 4.x** (Camel 3.x is not supported - use `/camel-migrate` to upgrade first)
    
-   **Maven-based** project structure
    
-   One of these runtimes:
    
    -   Spring Boot
        
    -   Quarkus
        
    -   Camel Main / JBang
        
    
-   **YAML routes**. Projects whose routes are only XML, Java or Groovy are reported as an unsupported combination, and Karaf (`camel-blueprint`) is not supported. Camel Kit never converts the DSL or switches the runtime.
    

> **Note**
> Multi-module Maven projects are supported with `.camel-kit/` at the root.

## Safe Adoption

Camel Kit `init` is **safe to run over existing projects** with these protections:

 
| What’s Protected | How |
| --- | --- |
| `pom.xml` | Never modified during init |
| Maven wrapper (`mvnw`, `.mvn/`) | Skipped if exists (use `--replace-wrapper` to force replacement) |
| `AGENTS.md` and `CLAUDE.md` | Use managed blocks - customizations preserved on reinit |
| Skill files | Files Camel Kit ships are refreshed on reinit so they match the installed version. Edit a copy, or add your own file next to them: files Camel Kit does not ship are never touched |
| Existing routes | Never modified unless explicitly listed in design spec |

### Dry-Run Mode

Preview changes before writing files:

```bash
camel-kit init --here --ai claude --dry-run
```

The preview lists shared files with a `create`, `replace`, `merge` or `preserve` action, using the same ownership and replacement rules as initialization. It does not write files or run baseline tests, even when `--record-baseline` is also supplied. See [Existing projects](getting-started.html#existing-project) for file ownership and `--replace <path>` behavior.

## Getting Started

### 1\. Initialize Camel Kit

From your existing project root:

```bash
cd my-existing-camel-app
camel-kit init --here --ai claude
```

Camel Kit detects:

```none
Detected existing Maven project (pom.xml found)
Project graph: 41 nodes, 21 edges
   Detected: Apache Camel 4.8.0 on Spring Boot (3 routes)
Generated .camel-kit/config.properties with detected metadata
Generated CLAUDE.md and skills
```

`init` does not run your project’s build or tests. The baseline test status is recorded as `not_run`. The test baseline has to exist **before** anything is edited, because results captured afterwards would include the new changes and hide regressions. There are two ways to get it:

-   Pass `--record-baseline` to `init`. It runs `./mvnw test` once in your project and writes `.camel-kit/baseline-test-results.json`.
    
-   Otherwise `/camel-execute` captures it as its first step, before the first edit.
    

If neither happened, `/camel-validate` reports baseline preservation as `UNVERIFIED`. It does not run the tests afterwards and call that the baseline.

`.camel-kit/baseline-test-results.json` stores the outcome of every individual test (`[module:]class#method` mapped to `passed`, `failed`, `error` or `skipped`), the Git revision the tests ran against, whether tracked files had uncommitted changes, and whether all test reports were successfully parsed. Validation compares tests by identity, so a test that now fails, was skipped, or disappeared is a regression even when the number of failures is unchanged.

Camel Kit warns when the project uses an unsupported Camel version (3.x), an unsupported runtime or DSL, or when no routes were found in the project graph. In the last case the route baseline is incomplete, so read the existing route sources before changing them.

### 2\. Review Detected Configuration

Check `.camel-kit/config.properties`:

```properties
project.type=existing
project.runtime=spring-boot
project.camelVersion=4.8.0
project.detectedCamelVersion=4.8.0
project.platformBomVersion=4.8.0
project.springBootVersion=3.3.4
project.primaryDsl=yaml
project.routeCount=3
project.hasTests=true
project.baselineTestStatus=not_run
project.configFilesCount=1
```

`project.modules` and `project.moduleCount` appear only for multi-module projects. `project.beansCount` counts classes the graph recognizes as beans through annotations such as `@Component` or `@Service`, plus entries in a Camel YAML `beans:` block. Beans registered through `@Bean` methods in `@Configuration` classes are not counted. `project.configFilesCount` counts `application*.properties` and `application*.yml` / `.yaml` files. A key that is missing means discovery found nothing for it, not that the project has none.

`project.contractFilesCount` counts interface contract files (OpenAPI/Swagger/AsyncAPI documents, WSDL, XSD, protobuf and Avro schemas) and `.camel-kit/baseline-contracts.txt` lists them. Init only inventories these files so later stages can protect them; it does not analyse their content (tracked in #111).

Only values your project declares are recorded. `project.camelVersion` comes from the `camel.version` property, an `org.apache.camel` dependency, or an imported Camel BOM. `project.platformBomVersion` is the imported `camel-spring-boot-bom` or `quarkus-bom` and `project.springBootVersion` is the imported `spring-boot-dependencies` or the `spring-boot-starter-parent`, with `${property}` references resolved from the pom. Nothing is filled in from Camel Kit’s own version tables. If a value cannot be established it is left out and reported as a gap.

If the pom shows two runtimes (for example `camel-spring-boot-starter` and `camel-quarkus-core`) or two different Camel versions, Camel Kit does not pick one: `project.runtime` or `project.camelVersion` is left out and `project.discoveryGaps` names the evidence. The workflow stops until you align the pom.

Two further keys appear only when needed:

-   `project.discoveryGaps` - something discovery could not determine, for example conflicting runtimes or Camel versions, a BOM version that could not be resolved, a pom that could not be read, no routes found in the graph or routes in more than one DSL. The workflow inspects the source for these items and asks you about anything still unclear.
    
-   `project.unsupportedCombination` - the detected runtime or DSL is outside the supported scope (for example a Karaf runtime, or no YAML routes). The workflow stops instead of guessing; Camel Kit never converts the DSL.
    

### 3\. Add a New Capability

Start the workflow:

```bash
# In Claude Code, VS Code, or your AI agent
/camel-start
```

Claude Code detects this is an existing project and asks:

> I’ve analyzed your project:
> 
> -   **Camel 4.8.0** on Spring Boot 3.3.4
>     
> -   **3 existing YAML routes** using rest, timer, and http components
>     
> -   Error handling via `errorHandler` with `deadLetterChannel`
>     
> -   Tests using Spring Boot Test
>     
> 
> **What new capability would you like to add to this integration?**

### 4\. Design the Addition

The brainstorm phase:

1.  Reads your existing routes from the project graph
    
2.  Asks **only unresolved questions** (doesn’t re-ask about runtime, version, or DSL)
    
3.  Identifies integration points with existing routes
    
4.  Produces a design spec with:
    
    -   **Requested Additions** - what’s being added
        
    -   **Integration Points** - how new routes connect to existing ones
        
    -   **Affected Files** - which files will be modified
        
    -   **Unchanged Behavior Constraints** - routes that must stay the same
        
    

### 5\. Plan and Execute

The plan phase:

-   Limits changes to approved scope (won’t modify protected files)
    
-   Preserves your Camel version (no upgrades)
    
-   Generates new routes in your primary DSL (currently YAML; XML/Java support tracked in #52)
    
-   Adds dependencies to your existing `pom.xml` in place. It never replaces the pom with a template, and never changes its parent, BOMs or versions
    

The execute phase:

-   Captures the per-test baseline before the first edit (unless `init --record-baseline` already did)
    
-   Validates scope compliance before and after each task
    
-   Verifies no unrelated files are touched
    
-   Checks that versions stay unchanged
    

### 6\. Validate

The validate phase:

-   **Uses the baseline captured before the edits** - it never creates one afterwards
    
-   **Separates concerns** - validates new routes separately from existing ones
    
-   **Detects regressions per test** - compares each baseline test with its current outcome
    

```none
## Baseline Test Results

| Test | Baseline | Current | Verdict |
|------|----------|---------|---------|
| com.example.OrderTest#create | passed | passed | OK |
| com.example.OrderTest#cancel | failed | failed | Pre-existing failure |
| com.example.UserTest#lookup | passed | failed | REGRESSION |

VERDICT: REGRESSION - 1 baseline test no longer passes
```

A test that disappeared or is now skipped counts as a regression unless the design spec approves it. When no usable baseline exists, the verdict is `UNVERIFIED` and the report lists what is missing under **Unavailable Evidence**.

## Worked Example: Add REST Endpoint

### Scenario

You have an existing Camel 4.8.0 Spring Boot application with:

-   3 YAML routes (REST API for users and health, timer-based task)
    
-   Spring Boot 3.3.4
    
-   Tests using `camel-test-spring-junit5`
    

**Goal:** Add a new REST endpoint `/api/orders` that follows the same pattern as the existing `/api/users` endpoint.

> **Note**
> This example is based on the fixture at `kit/camel-kit-core/src/test/resources/fixtures/existing-project-spring-boot`.

### Step-by-Step

1.  **Initialize**
    
    ```bash
    camel-kit init --here --ai claude
    ```
    
2.  **Start the workflow**
    
    ```none
    /camel-start
    ```
    
3.  **Request the new capability**
    
    > **User:** "Add a new REST endpoint `/api/orders` that returns a list of orders, similar to the existing `/api/users` endpoint."
    
4.  **Brainstorm discovers existing structure**
    
    > **Claude:** "I see you have existing REST routes using `rest:` DSL and platform-http. Should the new `/api/orders` endpoint follow the same pattern as `/api/users`?"
    > 
    > **User:** "Yes, same pattern."
    > 
    > **Claude:** "Should I create integration tests similar to your existing `ExistingRoutesTest`?"
    > 
    > **User:** "Yes."
    
5.  **Design spec generated**
    
    The spec includes:
    
    ```markdown
    ## Requested Additions
    
    - New route: `get-orders-api`
    - REST endpoint: `GET /api/orders`
    - Response format: JSON array of order objects
    
    ## Integration Points
    
    | New Route | Connects To | Mechanism |
    |-----------|-------------|-----------|
    | get-orders-api | Existing REST infrastructure | Uses same `rest:` DSL and platform-http component |
    
    ## Affected Files
    
    - `src/main/resources/camel/order-routes.yaml` (CREATE)
    - `src/test/java/org/apache/camel/kit/test/fixture/OrderApiTest.java` (CREATE)
    
    ## Unchanged Behavior Constraints
    
    - `/api/users` route: MUST remain unchanged
    - `application.properties`: MUST NOT modify
    - `pom.xml`: MUST NOT modify (all components already present)
    ```
    
6.  **Plan generated**
    
    Tasks include:
    
    -   Create `order-routes.yaml` with new REST route
        
    -   Create integration test
        
    -   **Validate scope compliance** (verify only approved files touched)
        
    -   **Verify existing functionality** (rerun existing tests)
        
    
7.  **Execution**
    
    ```none
    Task 1: Create order-routes.yaml
    Task 2: Create OrderApiTest
    Task 3: Validate scope compliance
      Modified files: order-routes.yaml, OrderApiTest.java (approved)
      No protected files touched
      Camel version unchanged (4.8.0)
    Task 4: Verify existing functionality
      Existing tests: 3 passed (baseline preserved)
      New tests: 4 passed
    ```
    
8.  **Validation report**
    
    ```markdown
    # Validation Report (Existing Project Enhancement)
    
    ## Baseline Preservation
    
    - Existing routes (3): All passed validation
    - Existing tests (3): All passed
    - No regressions detected
    
    ## New Capabilities Validation
    
    - New route: get-orders-api - PASS
    - Integration tests: OrderApiTest (4 tests) - PASS
    
    VERDICT: Baseline Preserved, New Capability Works
    ```
    

## Supported Combinations

   
| Runtime | Camel Versions | DSL | Status |
| --- | --- | --- | --- |
| Spring Boot | 4.8.x | YAML | Tested (fixture) |
| Spring Boot | 4.4.x - 4.7.x | YAML | Expected to work (not tested) |
| Quarkus | 3.15.x (Camel 4.8.x) | YAML | Expected to work (not tested) |
| Camel Main | 4.8.x | YAML | Expected to work (not tested) |
| Karaf (`camel-blueprint`), or no YAML routes | Any | Any | Not supported (reported as `project.unsupportedCombination`) |
| Camel 3.x | Any | Any | Not supported (use `/camel-migrate` first) |

## Limitations

### Version 1 Scope

-   **Multi-module projects** - Discovery supports multi-module Maven projects with `.camel-kit/` at the root. Full end-to-end workflow validation across multiple modules is tracked in follow-up work
    
-   **YAML DSL only** - Version 1 supports YAML DSL. XML, Java and Groovy routes are detected and reported through `project.unsupportedCombination` when no YAML routes exist, but the workflow stops instead of planning additions (broader Java DSL support is tracked in issue #52)
    
-   **Discovery is a starting point** - The graph reads Maven poms, Java/Groovy/XML/YAML routes, `beans:` blocks and `application*.properties` / `application*.yml`. Anything else, such as beans created by `@Bean` methods, is not counted and is listed in `project.discoveryGaps` or must be inspected in the source
    
-   **One runtime** - Cannot mix Spring Boot and Quarkus in the same project
    

### Not Supported

-   Upgrading Camel versions (use `/camel-migrate` instead)
    
-   Converting DSL types (YAML → Java, etc.)
    
-   Modifying protected routes not in design spec
    
-   Breaking existing API contracts
    

## Troubleshooting

### "No Maven version detected"

**Cause:** `pom.xml` uses `${camel.version}` property but doesn’t define it, or no Camel version is declared at all. Camel Kit never guesses a version for an existing project.

**Fix:** Define the property:

```xml
<properties>
    <camel.version>4.8.0</camel.version>
</properties>
```

### "Conflicting runtimes" or "Conflicting Camel versions"

**Cause:** The pom shows more than one runtime (for example both Spring Boot and Quarkus Camel artifacts) or more than one Camel version (for example `camel.version` is 4.8.0 but a `camel-core` dependency says 4.10.0).

**Fix:** Align the pom. Until then `project.runtime` or `project.camelVersion` is not recorded, and `/camel-plan` and `/camel-execute` stop. `project.discoveryGaps` lists the files and artifacts that disagree.

### "Unsupported Camel version 3.x"

**Cause:** Your project uses Camel 3.x.

**Fix:** Use the migration workflow:

```bash
/camel-migrate
```

### "Mixed DSL detected"

**Cause:** Your project has both YAML and XML routes.

**Fix:** New routes use YAML and the other DSLs are never converted. If you want consistency:

1.  Choose one DSL
    
2.  Convert routes to that DSL
    
3.  Reinitialize Camel Kit
    

### "Tests failed after adding capability"

**Cause:** Regression introduced.

**Fix:** Check the validation report:

```markdown
### Regression Analysis

New failures detected:
- TestName: testExistingUserRoute()
  Baseline: PASS
  Current: FAIL
  Reason: Bean 'userDatabaseBean' not found
```

The new route may have accidentally removed a shared bean. Review the execution report and revert problematic changes.

## Best Practices

### Before You Start

1.  **Commit your changes** - `git commit` before running `camel-kit init`
    
2.  **Run tests** - Verify existing tests pass
    
3.  **Use dry-run** - Preview changes with `--dry-run`
    

### During Design

1.  **Be specific about scope** - List files that should NOT be modified
    
2.  **Identify integration points** - Explicitly state how new routes connect to existing ones
    
3.  **Reuse existing beans** - Reference beans by exact name
    

### After Execution

1.  **Review the diff** - `git diff` to see exactly what changed
    
2.  **Check the validation report** - Verify no regressions
    
3.  **Test manually** - Run the app and test the new capability
    

## Next Steps

-   Learn about [Camel Kit pipeline](pipeline.md)
    
-   Explore [available skills](skills.md)
    
-   Read about [design rules](constitution.md)
    
-   See [Getting Started](getting-started.md) for greenfield projects
    

## Related Topics

-   [Migrating from other platforms](migration.md)
    
-   [Route validation](camel-validate.md)
    
-   [Runtime verification](verification.md)