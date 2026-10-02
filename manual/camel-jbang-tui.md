# Camel TUI

**Available as of Camel 4.21**

Camel TUI is a terminal dashboard for developing, prototyping, and understanding Camel integrations. With over 40 screens organized across tabs, it makes your entire integration visible — you can browse your project source code with inline documentation, see your route topology, watch messages flow through processors, step through exchanges like scrubbing through a video timeline, inspect Kafka topics, run SQL queries against your DataSources, audit CVE vulnerabilities, and understand what Camel actually does with your routes. No more black box.

![TUI Overview showing multiple routes](_images/jbang/camel-tui-overview.png)

## Key Features

-   **Run anything** — your own routes, the built-in examples, or an existing Spring Boot or Quarkus project ([Getting started](camel-jbang-tui-getting-started.md)).
    
-   **Write routes with help** — a [source editor](camel-jbang-tui-source-editor.md) that checks YAML, Java and XML routes as you type, completes endpoint options, fixes problems and shows the live run data of each line.
    
-   **See the integration** — the [diagram](camel-jbang-tui-diagram.md) from the architecture down to one route, with live message counts.
    
-   **Watch and troubleshoot** — [live activity, message history, errors, traces](camel-jbang-tui-observe.md), and deep dives into Kafka, SQL, memory leaks, JFR and CVEs.
    
-   **Ask the AI** — the [AI panel](camel-jbang-tui-ai.md) (**F8**) with a hosted or a local model, and [AI coding agents](camel-jbang-tui-ai-agents.md) that see and drive the TUI over MCP and ACP.
    
-   **Make it yours** — [themes, settings](camel-jbang-tui-settings.md), the embedded shell, browser access and demo recording.
    

## Getting Started

```bash
camel run my-route.yaml   # in one terminal
camel tui                 # in another: auto-discovers every running integration

camel tui .               # or open a project directory and press F10 to run it
```

No route yet? Press **F2** and pick _Run an example…​_ to run one of the built-in examples on Camel Main, Spring Boot, Quarkus or JBang.

See [Camel TUI Getting Started](camel-jbang-tui-getting-started.md) for each way to start, and for connecting existing Spring Boot and Quarkus applications.

> **Tip**
> Press **F1** or **?** on any screen for context-sensitive help. Keyboard shortcuts are always shown in the footer bar.

## Tabs Overview

The TUI organizes information into tabs. Press number keys **1** through **0** to jump directly to any tab, or use **Tab** / **Shift+Tab** to cycle.

  
| Key | Tab | What It Shows |
| --- | --- | --- |
| 1 | Overview | All running integrations and infrastructure services. Start here. |
| 2 | Source | File explorer and editor for your project code, with Camel checks, completion and documentation. |
| 3 | Log | Real-time application logs with search and filtering. |
| 4 | Activity | Live exchange activity with elapsed times, endpoint sends, and failure tracking. |
| 5 | Diagram | Visual route topology with drill-down into individual routes. |
| 6 | Routes | Route list with message counts, throughput, and processing times. |
| 7 | Endpoints | All registered endpoints with usage statistics. |
| 8 | Inspect | Message history and tracing — step through exchanges processor by processor. |
| 9 | Errors | Failures with stack traces and exchange context. |
| 0 | More | 30+ additional tabs organized by category (see below). |

The **More** menu (key **0**) opens a popup with tabs organized into groups:

-   **Routing** — Browse Endpoints, Consumers, HTTP, Inflight, Producers, Route Controller
    
-   **Observability** — Circuit Breaker, Health, JFR, Metrics, Network Services, Exchange Events, Recovery Tasks, OpenTelemetry Spans
    
-   **AI** — Ollama (listed when an Ollama server is detected)
    
-   **Data** — JDBC DataSource, Kafka, SQL Query, SQL Trace
    
-   **JVM** — Classpath, Heap Memory Histogram, Memory Usage, Memory Leak, Process, Startup, Threads
    
-   **Project** — Beans, Catalog, Configuration, CVE Audit, Maven Dependencies, Type Converters, Data Type Transformers
    

Tabs appear dynamically based on what the integration uses. For example, the Kafka tab appears when a Kafka component is in use, SQL tabs when a DataSource is present, Circuit Breaker when resilience4j is in use, Spans when OpenTelemetry is enabled, and JFR when `camel-jfr` is on the classpath. The TUI adapts to show only what’s relevant to your integration.

Tab badges show live counts — the Errors tab shows a red badge when errors exist and Routes shows the route count.

Two panels can be opened on top of any tab: **F6** opens an [embedded shell](camel-jbang-tui-settings.html#_embedded_shell_f6) for running `camel` commands, and **F8** opens the [AI panel](camel-jbang-tui-ai.md) for asking questions about the running integrations.

## More about the TUI

 
| Page | What it covers |
| --- | --- |
| [Getting Started](camel-jbang-tui-getting-started.md) | Your own routes, the built-in examples, opening a project, connecting Spring Boot and Quarkus applications |
| [Source Editor](camel-jbang-tui-source-editor.md) | Reading and writing routes: checks as you type, quick fixes, fix with AI, completion, quick documentation, navigation, live run data |
| [Diagram](camel-jbang-tui-diagram.md) | The architecture, topology and route views, external endpoints, metrics |
| [Observing Integrations](camel-jbang-tui-observe.md) | Activity, message history, errors, spans, process, HTTP probe, CVE audit, Kafka, SQL, memory leaks, JFR, catalog |
| [AI Panel](camel-jbang-tui-ai.md) | AI providers, slash commands, project overview, AI log |
| [Local Models](camel-jbang-tui-local-models.md) | Ollama and OpenAI-compatible servers, the tool set for local models, what a question costs, the Ollama tab |
| [AI Agents](camel-jbang-tui-ai-agents.md) | MCP and ACP: what an AI agent can see and do, edits you confirm |
| [Actions, Settings and Themes](camel-jbang-tui-settings.md) | The actions menu, embedded shell, themes, settings, browser access, recording demos |

## Keyboard Shortcuts

### Global (All Tabs)

 
| Key | Action |
| --- | --- |
| **1** - **0** | Jump to tab by number |
| **Tab** / **Shift+Tab** | Next / previous tab |
| **F1** / **?** | Context-sensitive help (toggle) |
| **F2** | Actions menu |
| **F3** | Switch between integrations (when multiple running) |
| **Ctrl+F** | Browse the selected integration’s source files (the Overview tab also has plain **f**) |
| **F6** / **Shift+F6** | Toggle the embedded shell panel / cycle its height |
| **F8** / **Shift+F8** | Toggle the AI prompt panel / cycle its height |
| **F10** | Run menu (run, stop, restart, kill) |
| **Shift+F5** | Take screenshot |
| **Ctrl+C** / **Q** / **F2** → Quit | Quit |
| **Esc** | Close popup / go back / return to Overview |

### Source Tab

See the [keyboard shortcuts](camel-jbang-tui-source-editor.html#_keyboard_shortcuts) of the Source Editor.

## Command Line Options

  
| Option | Description | Default |
| --- | --- | --- |
| `[name|pid|directory]` | Name, PID, or directory path of a Camel integration. When a directory is given, the TUI opens it as a project in the Source tab — you can browse the source code and run it with **F10**. When omitted, the TUI auto-discovers running integrations. |  |
| `--mcp` | Enable the embedded MCP server for AI agent access to the TUI. | `false` |
| `--mcp-port` | Port for the embedded MCP server. | `8123` |
| `--web` | Enable the browser-accessible terminal (WebSocket) server. | `false` |
| `--web-port` | Port for the web terminal server. | `8090` |
| `--refresh` | Screen refresh interval in milliseconds. | `100` |
| `--theme` | Color theme for this session (e.g., `dark`, `tokyo-night`, `dracula`). See [Theme](camel-jbang-tui-settings.html#_theme) for the full list of 21 themes. Overrides the persisted `camel.tui.theme` preference when set. |  |
| `--record` | Replay a `.tape` file and record the session to an Asciinema `.cast` file. |  |
| `--record-size` | Size of the recorded terminal for `--record`, as `<cols>x<rows>`. | `200x50` |
| `--record-fps` | Frames per second captured by `--record`. | `10` |
| `--record-duration` | Maximum duration in milliseconds captured by `--record`. | `120000` |