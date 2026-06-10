# Camel CLI - Getting Started

Three commands. That is all it takes to go from zero to a running integration.

## Install

The Camel CLI runs on [JBang](https://www.jbang.dev/). Install JBang first (see [download instructions](https://www.jbang.dev/download/)), then install the Camel CLI:

```bash
jbang app install camel@apache/camel
```

Verify that it works:

```bash
camel version
```

```none
Camel CLI version: 4.21.0
```

That is it. No Maven project, no POM file, no IDE required.

> **Note**
> The CLI requires internet access to download dependencies on first use. If you are behind a proxy, see [JBang proxy configuration](https://www.jbang.dev/documentation/jbang/latest/configuration.html#proxy-configuration).

> **Tip**
> For version-pinned installs, offline-safe setups, container images, or installing without JBang, see [Installation Options](camel-jbang-installation.md).

## Create your first route

Use `camel init` to scaffold a new route. The file extension determines the DSL.

### YAML

```bash
camel init hello.yaml
camel run hello.yaml
```

You should see Camel start up and begin logging:

```none
... Started hello (timer://yaml)
... Hello Camel from route1
... Hello Camel from route1
```

Press `Ctrl+C` to stop.

### Java

```bash
camel init Hello.java
camel run Hello.java
```

Same workflow, same result — just a different DSL. XML works the same way (`camel init hello.xml`).

## Dev mode — edit and reload instantly

Run any route in dev mode to get live reload:

```bash
camel run hello.yaml --dev
```

Now edit the file in your editor and save. Camel detects the change and reloads the route automatically — no restart needed. This works for all DSLs (YAML, Java, XML).

> **Tip**
> Dev mode is the fastest way to prototype integrations. Keep it running while you iterate on your routes.

> **Tip**
> Want a visual overview of your running routes, message flow, and health status — right in the terminal? Just type `camel tui` — the plugin auto-installs on first use, no setup needed. See [Camel TUI](camel-jbang-tui.md) for details.

## Try a built-in example

Don’t have a route yet? The CLI ships with a catalog of ready-to-run examples:

```bash
camel run --example
```

This lists all available examples grouped by difficulty (beginner, intermediate, advanced), with icons showing whether they are bundled (work offline), require Docker, or include Citrus tests.

Run one directly:

```bash
camel run --example=timer-log
camel run --example=rest-api --dev
```

> **Tip**
> Combine with `--dev` for live reload while exploring the example.

### Running multiple files

You can run several files together, even mixing DSLs:

```bash
camel run one.yaml Hello.java
```

Or use wildcards to run everything in a directory:

```bash
camel run *.yaml
camel run *
```

> **Tip**
> The CLI automatically picks up `application.properties` files in the same directory.

## Browse the component catalog

Discover what Camel offers — components, data formats, languages, and Kamelets:

```bash
camel catalog component
camel catalog kamelet
```

> **Tip**
> Run `camel catalog --help` to see all sub-commands.

### Component documentation

Show quick reference documentation (description + all configuration options):

```bash
camel doc kafka
camel doc jackson
camel doc aws-kinesis-sink
```

> **Note**
> This shows catalog-level documentation with option tables, not the full website documentation.

If a component and data format share the same name, prefix with `dataformat:` (e.g., `camel doc dataformat:thrift`).

Open the online documentation in a browser with `--open-url`, or get just the URL with `--url`:

```bash
camel doc kafka --open-url
```

Filter options by name, description, or group (producer, security, advanced, etc.):

```bash
camel doc kafka --filter=security
camel doc kafka --filter=timeout
```

### Open API

Camel CLI supports contract-first REST development — each OpenAPI operation is bridged to a Camel route via `direct:<operationId>`.

See the [open-api example](https://github.com/apache/camel-kamelets-examples/tree/main/jbang/open-api) for details.

## Enable shell completion

Tab completion makes discovering commands much easier:

```bash
source <(camel completion)
```

To make it permanent:

```bash
echo 'source <(camel completion)' >> ~/.bashrc
```

## Interactive shell

Launch an interactive shell with command history, autocompletion, and alias support:

```bash
camel shell
```

All CLI commands are available inside the shell without the `camel` prefix. The shell stores history in `~/.camel-jbang-history` and aliases in `~/.camel-jbang-aliases`.

## Check your environment

Run the doctor to verify that your environment is set up correctly:

```bash
camel doctor
```

This checks Camel and Java versions, JBang availability, Maven repository connectivity, container runtime (Docker/Podman), and disk space.

## Explore commands

Every command supports `--help`:

```bash
camel run --help
camel init --help
```

For the full list of commands, see the [Command Reference](jbang-commands/camel-jbang-commands.md).

## What’s next

 
| Next step | When to use it |
| --- | --- |
| [Running Camel](camel-jbang-running.md) | Dev mode options, profiles, properties, GitHub-hosted routes, Spring Boot and Quarkus runtimes. |
| [Dev Services](camel-jbang-dev-services.md) | Spin up databases, message brokers, and other infrastructure for your routes. |
| [Development Tools](camel-jbang-devtools.md) | Send and receive test messages, configure JDBC, set up dependency injection. |
| [Debugging](camel-jbang-debugging.md) | Step through routes with the built-in debugger or connect your IDE. |
| [Export to Maven](camel-jbang-projects.md) | Export to Spring Boot, Quarkus, or Camel Main for production. Manage dependencies and versions. |