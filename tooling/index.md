# Tooling

Apache Camel ships with a rich set of built-in developer tools and is supported by a growing ecosystem of third-party tooling. Whether you prefer the command line, an IDE, a visual editor, or AI-assisted development — there is tooling to help you build, test, debug, and manage your Camel integrations.

## Camel CLI

The Camel CLI, powered by [JBang](https://www.jbang.dev/), lets you get started with Camel instantly — no project setup, no build tool configuration. Install it once, then use the `camel` command to develop, run, test, and export your integrations.

`camel run` Run Camel routes from source files (Java, YAML, XML, etc.) with automatic classpath management

`camel dev` Run in developer mode with hot-reload — changes are picked up automatically without restarting

`camel trace` Live message tracing, step by step through your routes to see how messages are processed

`camel cmd send` Send test messages to running Camel routes for quick testing and debugging

`camel test` Run tests for your Camel routes (a plugin, installed with camel plugin add test)

`camel export` Export your Camel project to Spring Boot, Quarkus, or standalone Java for production deployment

See the [Camel CLI documentation](../manual/camel-jbang.md) for installation instructions and detailed usage.

## Camel TUI

The `camel tui` command launches a full terminal-based UI with route status, message flow, and tracing in a single view — plus a built-in mini source editor for YAML DSL routes with context-aware Tab completion, validation on save, and inline quick docs.

See the [Camel TUI documentation](../manual/camel-jbang-tui.md) for more details.

![Camel TUI Overview — four running integrations with live throughput chart and log](../tooling/camel-tui-overview.png)

AI-assisted development

## Camel MCP Server

Connects Apache Camel to AI coding assistants through the [Model Context Protocol](https://modelcontextprotocol.io/). It gives AI tools access to Camel's component catalog, DSL documentation, and integration patterns — so they can help you write, debug, and optimize Camel routes with full context. Supported tools include Claude Code, GitHub Copilot, Gemini CLI, Cursor, Windsurf, and any MCP-compatible assistant. See the [Camel MCP Server documentation](../manual/camel-jbang-mcp.md).

[Camel Kit](https://github.com/luigidemasi/camel-kit)

Structured slash commands for AI coding assistants that guide you through the complete integration lifecycle. Supports Claude Code, Gemini CLI, and more.

[Wanaku](https://wanaku.ai)

The Wanaku MCP Router is a router for AI-enabled applications powered by the Model Context Protocol and Apache Camel.

## Maven Plugins

For production projects, Camel provides a set of Maven plugins that integrate with your existing build workflow.

[Camel Maven Plugin](../manual/camel-maven-plugin.md)

Run and develop Camel applications from Maven: camel:run, camel:dev (hot-reload), camel:debug, camel:prepare-fatjar.

[Camel Report Maven Plugin](../manual/camel-report-maven-plugin.md)

Validates endpoint URIs, Simple expressions, duplicate route IDs, and generates route coverage reports after unit testing.

[Camel YAML DSL Validator Maven Plugin](../manual/camel-yaml-dsl-validator-maven-plugin.md)

Validates YAML DSL route files for syntax errors according to the spec, without needing to run Camel.

[Camel Component Maven Plugin](../manual/camel-component-maven-plugin.md)

Generates metadata and configuration Java classes for custom Camel components.

[Camel REST DSL OpenAPI Plugin](../manual/rest-dsl-openapi.md)

Generates REST DSL routes and DTOs from OpenAPI v3 specification files for a contract-first approach.

## Maven Archetypes

Camel provides [Maven Archetypes](../manual/camel-maven-archetypes.md) to quickly scaffold new projects.

camel-archetype-java

Creates a new Camel project using Java DSL

camel-archetype-main

Creates a new Camel project using standalone Camel Main

camel-archetype-spring-boot

Creates a new Camel project using Spring Boot

camel-archetype-component

Creates a new Camel component

camel-archetype-dataformat

Creates a new Camel data format

camel-archetype-api-component

Creates a new Camel component that wraps one or more API proxies

## IDE Plugins and Extensions

[Apache Camel IDEA Plugin](https://github.com/camel-tooling/camel-idea-plugin)

Camel editing capabilities for IntelliJ IDEA, including textual route debugging.

[VS Code Extension Pack for Camel](https://marketplace.visualstudio.com/items?itemName=redhat.apache-camel-extension-pack)

A set of VS Code extensions for developing Camel applications — language support, debugging, and more.

[Camel Language Server](https://github.com/camel-tooling/camel-language-server)

LSP implementation providing completion, validation, hover, and outline. Packaged for [VS Code](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-apache-camel) and [Eclipse Desktop](https://marketplace.eclipse.org/content/language-support-apache-camel).

[Camel Debug Adapter](https://github.com/camel-tooling/camel-debug-adapter)

DAP implementation providing Camel textual route debugging. Packaged for [VS Code](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-debug-adapter-apache-camel) and [Eclipse Desktop](https://marketplace.eclipse.org/content/textual-debugging-apache-camel).

## Visual Editing

[Camel Karavan](https://karavan.space/)

A rich graphical editor for designing and deploying integration routes.

[Kaoto](https://kaoto.io/)

An integration editor to create and deploy workflows in a visual, low-code way; with a code editor and deployments to the cloud.

## Monitoring and Management

[Camel Monitor Operator](https://camel-tooling.github.io/camel-dashboard/docs/installation-guide/advanced/operator/)

A Kubernetes operator that discovers and monitors Camel applications, with a GUI dashboard and Prometheus integration.

[hawt.io](http://hawt.io)

An open source HTML5 web application for visualizing, managing and tracing Camel routes & endpoints, ActiveMQ brokers, JMX, and more.

## Libraries

[Forage](https://kaotoio.github.io/forage/)

Opinionated bean factories for Apache Camel — configure data sources, connection factories, AI models, and more via properties. Works with Camel JBang, Spring Boot, and Quarkus.

If you are using or have developed tooling for Apache Camel please add an entry via a [pull request](https://github.com/apache/camel-website); or post to the [mailing list](../community/mailing-list/index.md).