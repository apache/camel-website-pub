# Contributing and releasing

Camel Kit is developed at [apache/camel-kit](https://github.com/apache/camel-kit) under the Apache Camel project. The CLI and agent skills live in `kit/`; the standalone Knowledge MCP server lives in `knowledge/`. Both share this repository and documentation, with independent versions and releases. Issues and pull requests go to that repository; questions go to the Camel [mailing lists](/community/mailing-list/). Contributors follow the [ASF code of conduct](https://www.apache.org/foundation/policies/conduct.md).

## Building

You need Java 17 or later, JBang, and Git; Maven comes with the wrapper. Always build with the wrapper, from the repository root.

```bash
./mvnw clean install                                      # all modules
./mvnw -B -Plinux-ship-certification clean install       # what CI runs (Linux)
./mvnw -B -Psourcecheck validate                          # the formatting gate
./mvnw test -pl kit/camel-kit-core                            # one module
./mvnw test -pl kit/camel-kit-core -Dtest=ShippedAssetStructureTest   # one test class

# run the CLI from source
jbang kit/camel-kit-main/src/main/jbang/main/CamelKit.java --help
```

 
| Module | Content |
| --- | --- |
| `kit/camel-kit-main` | The JBang entry point |
| `kit/camel-kit-core` | CLI commands, configuration, initialization and traits; all skills and templates as resources |
| `kit/camel-kit-graph` | The project graph: nine parsers and two post-processors |
| `kit/camel-kit-ship-resolver` | The classloader-isolated Maven resolver used for Ship evidence |
| `kit/camel-jbang-plugin-kit` | The Camel JBang plugin |

Install the shared parent once with `./mvnw -B -N install`, then build one product with `./mvnw -B -f kit/pom.xml clean install` or `./mvnw -B -f knowledge/pom.xml clean install`. The Knowledge reactor contains `schema`, `embedding`, `indexer`, `index` and `mcp`; ordinary builds use the committed index. All Java packages use `org.apache.camel.kit`, and Maven modules use `org.apache.camel`.

`distribution.properties` at the repository root is the single source of truth for every version pin; it is copied into the JAR and never duplicated by hand. `tools/sync_distribution_mirrors.py` copies the few literals Maven needs into `kit/pom.xml` and checks them with `--check`.

## Definition of done

A change is finished when all of the following hold:

-   The tests of every touched module pass, and `./mvnw clean install` from the root passes when the change spans modules or touches skills, templates or `distribution.properties`.
    
-   `./mvnw -Psourcecheck validate` passes.
    
-   A skill, template or trait change passes `ShippedAssetStructureTest`, and the active documents pass `ResourceConsistencyTest` (see [the contract tests](architecture.html#equalization)).
    
-   Every new skill is registered in the workflow manifest; a user-invocable one also in the templates of all eight agents and in the command reference.
    
-   No version is hardcoded where `distribution.properties` applies.
    
-   The documentation is updated, and `CHANGELOG.md` for significant changes.
    
-   Nothing was skipped, disabled or weakened to get a green build; a failing check is reported, not hidden.
    

Branches are named `feature/…​`, `fix/…​`, `docs/…​`, `command/…​` or `template/…​`. Rebase on `main` before opening a pull request, fill in the template, link the related issues and request a review. Commit messages are plain and descriptive.

## Adding a skill

A skill is a directory under `kit/camel-kit-core/src/main/resources/skills/` with a `SKILL.md` manifest (YAML front matter with `name`, `description` and `user_invocable`, then the steps and a guide table) and a `guides/` directory of instruction files loaded on demand. Every skill is registered in the workflow manifest `camel-kit-workflow.yaml`, which drives the generated command stubs, the trait application and the structural tests: a user-facing skill with its `generated_command`, documented in the command reference; an internal skill with `status: internal` and `generated_command: null`, referenced from the guide table of the skill that dispatches it. Shared guides under `skills/shared/` feed several skills, so check every caller before editing one. Agent-specific behaviour goes into trait files under `templates/traits/<agent>/`, which need no code registration. See [Skills system](skills.md) for the structure and the tiers.

## Documentation

This site is built from `docs/antora.yml` and `docs/modules/` in the repository with Antora, as a component of the Apache Camel website; edit the `.adoc` pages there and keep versions in the attributes of `antora.yml`. The repository also keeps `docs/commands.md`, `docs/architecture.md` and `docs/constitution.md`, which the consistency tests read, and `docs/user-guide.md`; keep them in step with these pages when behaviour changes.

## Releasing

The shared parent, Kit and Knowledge have independent versions and release schedules. A product release references a published, released shared parent. Use the corresponding POM (`pom.xml` with `-N`, `kit/pom.xml`, or `knowledge/pom.xml`) when preparing or staging a release; never deploy the root reactor to release one product.

Tags are `camel-kit-parent-X.Y.Z`, `camel-kit-X.Y.Z` and `camel-kit-knowledge-X.Y.Z`. `tools/release_target.py` validates the selected target, its module versions and its tag. The manually dispatched `Stage Maven Release` workflow checks the exact tag and reviewed commit SHA, tests and signs that target, and uploads a validated staging deployment. Automatic promotion is disabled.

Apache releases follow the [ASF release policy](https://www.apache.org/legal/release-policy.md) and the Camel [release guide](../../manual/release-guide.md), including a source release candidate and successful PMC vote before publication. The staging workflow does not automate that whole process. See `docs/releasing.md` in the repository for the preparation steps.

Kit pins a tested Knowledge runner using `knowledge.mcp.group-id` and `knowledge.mcp.version` in `distribution.properties`. Published Knowledge 0.0.2 retains its `io.github.luigidemasi` coordinates; migrated development builds use `org.apache.camel`. Adopting a new runner is explicit and does not require matching Kit and Knowledge versions. Synchronize Kit launchers from its POM with `./mvnw -B -f kit/pom.xml -N antrun:run@sync-jbang-launcher-versions`.

Index data is published independently under `knowledge-index-v1-YYYY.MM.DD-HHMMSS` tags. Maintainers rebuild it on a branch with `./mvnw -B -pl knowledge/index -am -Prebuild-index install`, review the generated data, and manually dispatch `Index Release` from `main` with the reviewed SHA. The workflow requires working vector retrieval and packages the reviewed index without regenerating it. See [Knowledge MCP](knowledge.md) for compatible discovery, explicit version pins and cache fallback.