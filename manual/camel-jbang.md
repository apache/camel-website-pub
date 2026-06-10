# Camel CLI

The Camel CLI is the command-line interface for Apache Camel. It gives you a complete, terminal-native development environment for building integrations — from a first prototype to a production-ready project — without requiring an IDE, a Maven project, or boilerplate code.

Write a route in YAML, Java, or XML. Run it. Debug it. Trace messages flowing through it. Spin up the infrastructure it needs. Export it to Spring Boot or Quarkus when you are ready. All from the terminal.

## Why Camel CLI

**Zero-to-running in seconds.** Create and run an integration in three commands — no project skeleton, no POM file, no IDE. The CLI auto-detects the Camel components your route needs and downloads them on the fly.

**Full development lifecycle.** The CLI is not just a runner. It includes a built-in route debugger, a message tracer, health checks, metrics, a data-transformation prototyper, and an export command that produces a production-ready Spring Boot or Quarkus project from your prototype files.

**Terminal-native and AI-ready.** Every capability is a structured CLI command — designed for both human operators and AI coding assistants that work through terminal prompts. The [Camel MCP Server](camel-jbang-mcp.md) exposes the full Camel catalog to AI tools (Claude Code, GitHub Copilot, JetBrains AI, and others), and the [Camel TUI](camel-jbang-tui.md) provides a visual dashboard in the terminal — useful over SSH, in containers, in CI, or in any environment where a browser is not available.

**300+ connectors, one CLI.** The entire Apache Camel ecosystem — Kafka, AWS, databases, REST, messaging, files, and hundreds more — is available through a single `camel run` command. No dependency management required.

**Graduated path to production.** Start with flat files for fast prototyping. When the integration is ready, use `camel export` to generate a full Maven project targeting Spring Boot, Quarkus, or standalone Camel Main. Your prototype code becomes your production code.

## Quick Start

Install the CLI (requires [JBang](https://www.jbang.dev/download/)):

```bash
jbang app install camel@apache/camel
```

Create a route and run it:

```bash
camel init hello.yaml
camel run hello.yaml
```

Run in dev mode with live reload:

```bash
camel run hello.yaml --dev
```

> **Tip**
> You can also install without JBang using the [Camel CLI Launcher](camel-jbang-launcher.md).

## What Can You Do

 
| Area | What it covers |
| --- | --- |
| [Getting Started](camel-jbang-getting-started.md) | Installation, shell completion, creating and running your first route. |
| [Installation Options](camel-jbang-installation.md) | Version-pinned installs, offline-safe setups, container images, installing without JBang. |
| [Running Camel](camel-jbang-running.md) | Dev mode with hot reload, profiles, properties, dependency management, Kamelets, platform-http, Spring Boot and Quarkus runtimes. |
| [Dev Services](camel-jbang-dev-services.md) | Start and manage local infrastructure services (databases, message brokers, etc.) for development and testing, powered by Camel test-infra and containers. |
| [Data Transformation](camel-jbang-transforming.md) | Transforming messages with live reload, using expression languages, components, data formats, and converting between route DSL formats. |
| [Development Tools](camel-jbang-devtools.md) | Sending and receiving messages, JDBC configuration, terminal scripting, IDE editing, validate plugin. |
| [AI Tools](camel-jbang-ai.md) | Ask questions about running integrations, explain routes, and get security hardening suggestions — powered by local or cloud LLMs. |
| [Debugging](camel-jbang-debugging.md) | Camel route debugging from the CLI, IDE integration (VSCode, IDEA), Java-level debugging. |
| [Managing Integrations](camel-jbang-managing.md) | Listing and stopping processes, route and group control, developer console, message history, log tailing, message tracing, health checks, metrics, circuit breaker status, Jolokia and Hawtio. |
| [Export to Maven](camel-jbang-projects.md) | Exporting to Spring Boot / Quarkus / Camel Main, SBOM generation, plugin management, version management, automated upgrades. |
| [Tips and Recipes](camel-jbang-tips.md) | Run from GitHub or clipboard, stub components, inline code, interactive prompts, upload via HTTP, Maven configuration. |
| [Java Beans](camel-jbang-beans.md) | Writing and wiring Java beans into routes using Camel, Spring Boot, or Quarkus annotations. |
| [Configuration](camel-jbang-configuration.md) | CLI configuration options, config commands, configuration precedence, troubleshooting. |
| [Command Reference](jbang-commands/camel-jbang-commands.md) | Complete reference for all CLI commands and their options. |

### Plugins and Extensions

 
| Extension | Description |
| --- | --- |
| [Camel CLI Launcher](camel-jbang-launcher.md) | Self-contained executable JAR — run the CLI without JBang. |
| [Kubernetes Plugin](camel-jbang-kubernetes.md) | Build and deploy Camel integrations to Kubernetes. |
| [Testing Plugin](camel-jbang-test.md) | Automated testing with the Citrus test framework. |
| [Camel TUI](camel-jbang-tui.md) | Terminal dashboard for visualizing route topology and message flow. |
| [Camel MCP Server](camel-jbang-mcp.md) | Expose the Camel catalog and tools to AI coding assistants via the Model Context Protocol. |

## How It Works

Camel CLI is powered by [JBang](https://www.jbang.dev/) under the hood. When you run `camel run`, JBang resolves and caches the required Camel JARs, then launches a JVM with your route. The CLI communicates with running integrations through a local connector, enabling management commands (`camel ps`, `camel get`, `camel log`, `camel trace`) to inspect and control them from a separate terminal.

For Spring Boot and Quarkus applications, adding the `camel-cli-connector` dependency lets the CLI manage those applications the same way.