# Camel CLI - Export to Maven

Export your Camel CLI integrations to production-ready Maven projects, manage dependencies, and upgrade Camel versions.

## Creating Projects

Export your Camel CLI integration to a Maven-based project for Spring Boot, Quarkus, or standalone Camel Main.

```bash
camel export --runtime=spring-boot --gav=com.foo:acme:1.0-SNAPSHOT
camel export --runtime=quarkus --gav=com.foo:acme:1.0-SNAPSHOT
camel export --runtime=camel-main --gav=com.foo:acme:1.0-SNAPSHOT
```

> **Note**
> Without `--directory`, files are exported to the current directory. Use `--directory=../myproject` to copy to a separate folder.

> **Tip**
> Run `camel export --help` for all options.

Notes:

-   The Quarkus platform version is automatically resolved from the registry based on the Camel version.
    
-   The `--profile` option is not supported when exporting to Quarkus.
    
-   For Spring Boot, you can override versions with `--camel-spring-boot-version`.
    

### Exporting with a parent POM

When organizations run many Camel integrations, they typically use a parent POM to standardize plugin versions, required extensions, and common dependencies. Use `--parent-pom` to set the parent POM in the exported project:

```bash
camel export --runtime=quarkus --gav=com.foo:acme:1.0-SNAPSHOT --parent-pom=com.ourorg:camel-parent:1.0
```

This generates the `<parent>` block in the exported `pom.xml`:

```xml
<parent>
    <groupId>com.ourorg</groupId>
    <artifactId>camel-parent</artifactId>
    <version>1.0</version>
    <relativePath/>
</parent>
```

For Spring Boot, specifying `--parent-pom` replaces the default `spring-boot-starter-parent`. The Spring Boot BOM (`spring-boot-dependencies`) remains in `<dependencyManagement>`, so version management continues to work.

You can also configure this in `application.properties`:

```properties
camel.jbang.parentPom=com.ourorg:camel-parent:1.0
```

### Exporting with Java Agent included

> **Note**
> Only `camel-main` runtime supports Java Agents.

Specify the agent with `agent:` prefix in `application.properties`:

```properties
camel.jbang.dependencies=camel:opentelemetry,agent:io.opentelemetry.javaagent:opentelemetry-javaagent:1.31.0
camel.opentelemetry.enabled=true
```

Export and run:

```bash
camel export --runtime=camel-main --gav=com.foo:acme:1.0-SNAPSHOT --directory=../myproject
cd ../myproject
mvn clean package
java -javaagent:agent/opentelemetry-javaagent-1.31.0.jar -jar target/acme-1.0-SNAPSHOT.jar
```

The agent JAR is downloaded from Maven and saved to the `agent/` folder.

### Exporting with selected files

By default, all files from the current directory are exported. Specify files explicitly to split into multiple projects:

```bash
camel export Foo.java --runtime=quarkus --gav=com.foo:acme:1.0-SNAPSHOT --directory=../export1
camel export bar.xml cheese.yaml --runtime=spring-boot --gav=com.foo:cheese:1.0-SNAPSHOT --directory=../export2
```

> **Note**
> `application.properties` is included in all exports automatically.

### Including JMX management or CLI connector

JMX management and CLI connector are not included by default. Add them with `--dep`:

```bash
camel export --runtime=quarkus --gav=com.foo:acme:1.0-SNAPSHOT --dep=camel:management
camel export --runtime=quarkus --gav=com.foo:acme:1.0-SNAPSHOT --dep=camel:cli-connector
```

### Troubleshooting exporting

Use `--verbose` and `--logging` for more detail, or `--logging-level=DEBUG` for full output. Try `--ignore-loading-error` if custom Java code prevents export.

> **Tip**
> Export logs are stored in `~/.camel/camel-export.log` by default.

### Configuring exporting

Export loads configuration from `application.properties`, where you can set runtime, Java version, and other parameters. See [Configuration](camel-jbang-configuration.md) for all `camel.jbang.*` options.

## Gathering list of dependencies

List the Camel components and JARs required to run your integration:

```bash
camel dependency list
org.apache.camel:camel-dsl-modeline:3.20.0
org.apache.camel:camel-health:3.20.0
org.apache.camel:camel-kamelet:3.20.0
org.apache.camel:camel-log:3.20.0
...
```

Output defaults to GAV format. Use `--output=maven` for Maven XML format. Use `--runtime=spring-boot` or `--runtime=quarkus` for runtime-specific dependencies.

## Generating SBOM report

Generate a Software Bill of Materials for your integration:

```bash
camel sbom
camel sbom --sbom-format=spdx
camel sbom --runtime=quarkus
```

Defaults to CycloneDX format (`sbom.json`) with `camel-main` runtime.

### Copying dependency JARs

Copy required JARs to a folder (defaults to `lib/`):

```bash
camel dependency copy
```

> **Important**
> Both `camel dependency copy` and `camel dependency list` require Apache Maven (`mvn`) in PATH.

## Manage plugins

Plugins extend the CLI with additional commands. List available plugins (ASF and community):

```bash
camel plugin get --all
```

Add, list installed, and remove plugins:

```bash
camel plugin add generate
camel plugin add forage --version=1.2.3
camel plugin get
camel plugin delete <plugin-name>
```

### Building custom plugins

It is possible to build custom Camel CLI plugins. We suggest to take a look at one of the [existing plugins](https://github.com/apache/camel/tree/main/dsl/camel-jbang), to see how that is done.

> **Important**
> The name of the plugin Maven **artifactId** must start with `camel-jbang-plugin-`. For example if the plugin is named `cheese`, then the maven artifact must be named `camel-jbang-plugin-cheese`.

## Generate JSON schema plugin

Generate JSON Schema definitions from Java objects for use with visual development tools (Kaoto, Karavan):

```bash
camel generate schema fhir org.hl7.fhir.r4.model.Patient
Schema saved to: ./org.hl7.fhir.r4.model.Patient-schema.json
```

## Version management

Show the current Camel CLI version:

```bash
camel version
```

### Running with a different version

Use `--camel-version` to run with a specific Camel version:

```bash
camel run * --camel-version=3.18.4
```

Or set a persistent version override:

```bash
camel version set 3.18.2
camel version set --reset
```

> **Important**
> You cannot combine `camel version set` with `--camel-version`.

For SNAPSHOT versions:

```bash
jbang --fresh -Dcamel.jbang.version=3.21.0-SNAPSHOT camel@apache/camel [command]
```

### Listing available releases

Show available Camel releases from Maven Central:

```bash
camel version list
 CAMEL VERSION   JDK   KIND     RELEASED     SUPPORTED UNTIL
    3.18.0      11,17  LTS        July 2022        July 2023
    3.20.0      11,17  LTS    December 2022    December 2023
   4.0.0-M1        17   RC    February 2023
   ...
```

Use `--runtime=quarkus` or `--runtime=spring-boot` to see runtime-specific versions. Use `--from-version=3.0` to show older releases (back to Camel 2.18).

> **Tip**
> Run `camel version list --help` for all options.

## Automated updates (OpenRewrite)

Update Camel applications automatically using [OpenRewrite recipes](https://github.com/apache/camel-upgrade-recipes). Supports Camel Main, Spring Boot, and Quarkus.

List available updates and run:

```bash
camel update list
camel update run 4.9.0 --runtime=spring-boot --dry-run
```

> **Note**
> Run from the project directory containing `pom.xml`.

Options: `--runtime` (camel-main, spring-boot, quarkus), `--repos` (extra Maven repos), `--dry-run` (preview only), `--extraActiveRecipes`, `--extraRecipeArtifactCoordinates`.

> **Tip**
> Run `camel update run --help` for all options.