# Camel CLI - Running Camel

This page covers the essential options for running Camel integrations — dev mode, properties, profiles, HTTP endpoints, dependencies, and runtimes.

For advanced techniques like running from GitHub, clipboard, or stub components, see [Tips and Recipes](camel-jbang-tips.md).

## Dev mode with live reload

Run with `--dev` to get automatic reload when you edit and save your source files:

```bash
camel run foo.yaml --dev
```

This works for all DSLs (YAML, Java, XML).

> **Note**
> Live reload is for development purposes. If you encounter JVM class loading issues, restart the integration. Java files are not live-reloadable in Spring Boot runtime.

### Source directory

Use `--source-dir` for more flexibility — Camel watches the entire directory (including subfolders) and automatically detects new, modified, and deleted files:

```bash
camel run --source-dir=mycode --dev
```

Without `--source-dir`, Camel only watches the specific files you listed on the command line.

> **Note**
> You cannot combine files and source dir: `camel run abc.java --source-dir=mycode` is not allowed.

### Live reload of resource files

In dev mode, Camel disables `contentCache` on resource-based components (such as `xslt`) so that edits to resource files are picked up on the next message without restarting.

User properties (e.g. `camel.component.xslt.contentCache=true`) and explicit endpoint settings are always respected.

### Loading new routes into existing Camel

**Available as of Camel 4.17**

The `camel cmd load` command loads new routes into a running Camel application:

```bash
camel cmd load --source=bar.java
```

> **Important**
> Assign _ids_ to your routes so the `load` command detects previously loaded routes and avoids duplicates.

> **Tip**
> Use `--restart` to restart all routes after the new route is loaded.

## Using properties

Set properties with `--property` or load them from a file with `--properties`:

```bash
camel run foo.yaml --property=my-key=my-value
camel run foo.yaml --properties=/var/my-app/config.properties
```

> **Note**
> Use the `=` sign directly after `--property` (no space).

If both are used, the properties are merged into a single `application.properties` file.

## Using profiles

**Available from Camel 4.5**

Camel CLI has three profiles:

-   `dev` — development (default), enables tracing, extra metrics, and developer-focused features
    
-   `test` — testing (currently same as production)
    
-   `prod` — production
    

Run with a specific profile:

```bash
camel run hello.java --profile=prod
```

Use profile-specific configuration files:

-   `application.properties` — common configuration (always loaded)
    
-   `application-dev.properties` — dev profile overrides
    
-   `application-prod.properties` — production profile overrides
    

> **Note**
> Since Camel 4.21, `camel run` and `camel export` auto-detect `application.properties` (and profile-specific variants) in the current directory.

## Using the platform-http component

When a route uses `platform-http`, Camel CLI automatically starts a VertX HTTP server on port 8080:

```yaml
- route:
    from:
      uri: platform-http:/hello
      steps:
        - set-body:
            constant: "Hello World"
```

```bash
camel run server.yaml
```

```bash
$ curl http://localhost:8080/hello
Hello World%
```

> **Note**
> Camel CLI only supports `platform-http` for HTTP serving and REST DSL. It does not support `camel-servlet` or `camel-jetty`.

## Adding custom JARs

Camel CLI automatically detects and downloads dependencies for Camel components. For 3rd-party JARs, use `--dep` with Maven GAV syntax:

```bash
camel run foo.java --dep=com.foo:acme:1.0
```

For Camel dependencies, use the shorthand syntax:

```bash
camel run foo.java --dep=camel-saxon
```

Multiple dependencies can be separated by comma:

```bash
camel run foo.java --dep=camel-saxon,com.foo:acme:1.0
```

## Using 3rd-party Maven repositories

By default, Camel CLI downloads from the local Maven repository and Maven Central. To add other repositories:

```bash
camel run foo.java --repos=https://packages.atlassian.com/maven-external
```

> **Tip**
> Separate multiple repositories with commas.

You can also configure repositories in `application.properties`:

```properties
camel.jbang.repos=https://packages.atlassian.com/maven-external
```

Or set a global default via environment variable:

```bash
export JAVA_TOOL_OPTIONS="-Dcamel.extra.repos=repo1=https://repo1.example.com/maven2,repo2=https://repo2.example.com/releases"
```

## Downloading JARs over the internet

Camel CLI automatically resolves and downloads dependencies in this order:

1.  Local Maven repository (`~/.m2/repository`)
    
2.  Maven Central
    
3.  Custom 3rd-party repositories
    
4.  Repositories from `~/.m2/settings.xml`
    

To disable automatic downloading:

```bash
camel run foo.java --download=false
```

## Running with Spring Boot or Quarkus

Camel CLI can run integrations using Spring Boot or Quarkus runtimes:

```bash
camel run foo.camel.yaml --runtime=spring-boot
camel run foo.camel.yaml --runtime=quarkus
```

This does an export to a temporary folder and runs using Maven. Source changes are reloaded via Spring Boot dev-tools or Quarkus dev mode.

Limitations:

-   Spring Boot and Quarkus cannot auto-detect new components (stop and run again to update dependencies)
    
-   Quarkus versions are locked to a specific Camel version (`camel version list --runtime=quarkus`)
    
-   Spring Boot is more flexible — you can choose different versions:
    

```bash
camel run foo.camel.yaml --runtime=spring-boot --spring-boot-version=3.2.3 --camel-version=4.4.1
camel run foo.camel.yaml --runtime=quarkus --quarkus-version=3.9.4
```

## Running local Kamelets

Run local Kamelets without publishing them:

```bash
camel run --local-kamelet-dir=/path/to/local/kamelets earthquake.yaml
```

> **Tip**
> Local Kamelets support live reload in dev mode.

You can also point to a GitHub folder:

```bash
camel run --local-kamelet-dir=https://github.com/apache/camel-kamelets-examples/tree/main/custom-kamelets user.java
```

> **Note**
> Kamelets loaded from GitHub cannot be live reloaded.

## Creating a new Kamelet

Create a new Kamelet using naming conventions — the suffix determines the type:

```bash
camel init cheese-source.kamelet.yaml    # creates a source kamelet
camel init wine-sink.kamelet.yaml        # creates a sink kamelet
```

Use the new Kamelet in a route:

```yaml
- route:
    from:
      uri: kamelet:cheese-source
      parameters:
        period: "2000"
        message: "Hello World"
      steps:
        - to:
            uri: kamelet:wine-sink
```

To base a new Kamelet on an existing one:

```bash
camel init orderdb-sink.kamelet.yaml --from-kamelet=mysql-sink
```