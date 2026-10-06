# Camel CLI - Diagnostics

When an integration misbehaves — messages fail, hang, run slowly, or memory keeps growing — the Camel CLI can look inside the running process without restarting it or attaching a debugger.

All commands take the name or PID of a running integration (see [Managing Integrations](camel-jbang-managing.md)). The `camel get` commands also accept `--watch` to refresh continuously and `--json` for machine-readable output.

> **Tip**
> The [Camel TUI](camel-jbang-tui.md) shows the same data in tabs, see [Camel TUI Observing Integrations](camel-jbang-tui-observe.md).

## Errors and activity

### Routing errors

`camel get error` lists the routing errors captured by the [Error Registry](error-registry.md):

```bash
camel get error
camel get error myApp --route=orders --ago=5m
camel get error myApp --exception=SQLException --handled=false
```

Each row shows the route and node where the exchange failed, whether the error was handled, the exception and its message. The same failure repeating many times is collapsed: the `COUNT` column says how often it happened, and only the newest few exchanges of each kind are kept, so a burst of one failure does not push out every other error.

Show the details of an error:

```bash
camel get error myApp --last
camel get error myApp --id=<exchange-id> --show=body,headers,stackTrace
camel get error myApp --last --diagram
```

`--last` shows the newest error in full, `--detail` shows every error in full, and `--show` picks the sections (`body`, `headers`, `properties`, `variables`, `history`, `stackTrace`, or `all`). `--diagram` draws the route with the path of the failed exchange highlighted.

> **Note**
> The error registry is enabled by the `dev` profile, which `camel run` uses by default. For another profile, or for a Spring Boot or Quarkus application, set `camel.errorRegistry.enabled=true`.

### Recent activity

`camel get activity` lists the most recently completed exchanges, with their route, status, elapsed time, the number of messages sent to endpoints, and the endpoint they came from:

```bash
camel get activity
camel get activity --filter=route1
camel get activity --watch
```

Activity tracking is enabled by the `dev` profile.

### Inflight and blocked messages

`camel get inflight` lists the exchanges currently being processed, with the route and node they are at and how long they have been in flight.

`camel get blocked` lists the exchanges where a thread is blocked waiting for an asynchronous processor to complete, and for how long. A message that stays in this list points at a call that never returns.

```bash
camel get inflight --watch
camel get blocked
```

## JVM and memory

### Memory leaks

`camel cmd memory-leak` uses Java Flight Recorder (JFR) `OldObjectSample` events to find objects that survive garbage collection and keep piling up:

```bash
camel cmd memory-leak myApp --start
```

By default (`--mode=dual`) it makes two recordings, the second twice as long as the first (`--duration`, default 60 seconds), and compares them. Each allocation site gets a trend — `new`, `gone`, `growing`, `suspicious`, `shrinking` or `stable` — so you can tell steady memory use from memory that keeps growing. `--mode=single` makes one recording instead.

The recording runs in the integration; the results are kept there and can be queried again:

```bash
camel cmd memory-leak myApp --status
camel cmd memory-leak myApp --query --min-size=1MB --top=20
camel cmd memory-leak myApp --query --stacktrace
```

`--stop` ends a recording early and shows the results.

### Heap histogram

`camel cmd heap-histogram` shows which classes use the most heap memory:

```bash
camel cmd heap-histogram myApp
camel cmd heap-histogram myApp --filter=org.apache.camel --top=20
camel cmd heap-histogram myApp --sort=instances --watch
```

### Heap dump

`camel cmd heap-dump` writes a heap dump (`.hprof`) in the working directory of the integration, for analysis with tools such as Eclipse MAT or VisualVM:

```bash
camel cmd heap-dump myApp
camel cmd heap-dump myApp --dump-name=mydump --live=false
```

The file is named `heap-dump-<timestamp>.hprof` unless `--dump-name` is given. Only live objects are dumped unless `--live=false`. The command prints where the file was written.

### Garbage collection

Trigger a garbage collection, for instance before taking a heap histogram:

```bash
camel cmd gc myApp
```

Without a name, all running integrations are collected.

### Thread dump

List threads in a running Camel integration:

```bash
camel cmd thread-dump myApp
```

By default only Camel-related threads are shown. Use `--filter=all` for all JVM threads, or `--state=BLOCKED` to find blocked threads. Add `--trace` to include stack traces (`--depth` sets how many frames):

```bash
camel cmd thread-dump myApp --filter=all --state=BLOCKED --trace --depth=10
```

> **Tip**
> To profile CPU and allocations with JFR, run with `camel run --jfr`. The TUI JFR tab shows the recording, see [JFR Runtime Profiling](camel-jbang-tui-observe.html#_jfr_runtime_profiling).

## Startup and route structure

### Startup recording

`camel get startup-recorder` shows the steps Camel took while starting, with how long each took, to find what makes startup slow:

```bash
camel get startup-recorder myApp
camel get startup-recorder myApp --sort=duration
```

This needs a startup recorder that keeps the steps: run with `camel.main.startupRecorder=backlog`.

### Route structure

`camel cmd route-structure` shows the routes as a tree of their EIPs, with the source file and line of each:

```bash
camel cmd route-structure myApp
camel cmd route-structure orders.camel.yaml
camel cmd route-structure myApp --filter=myRoute --brief
camel cmd route-structure myApp --description
```

Give a source file instead of a running integration to see the structure without running it. `--brief` shortens each node, and `--description` shows the description of each node instead of its code.

### Route dump

`camel cmd route-dump` dumps the routes of the running integration in YAML (default), XML or Java DSL:

```bash
camel cmd route-dump myApp
camel cmd route-dump myApp --format=xml --filter=orders
```

This shows the routes as the running Camel holds them. To convert route files without running them, use `camel transform route` (see [Transforming route DSL format](camel-jbang-transforming.html#_transforming_route_dsl_format)).

## Data

### DataSources

`camel get datasource` lists the JDBC DataSources in the registry with their connection pool: active, idle and total connections, the maximum pool size, and threads waiting for a connection. HikariCP and Agroal pools are recognized.

```bash
camel get datasource --watch
```

### SQL trace

`camel get sql-trace` lists the recent SQL statements run by the `sql` and `jdbc` components, with the statement, the route, the duration, the number of rows and whether it failed:

```bash
camel get sql-trace myApp
camel get sql-trace myApp --watch
```

### Running SQL queries

`camel cmd sql` runs a SQL statement on a DataSource of the running integration, using its connection pool:

```bash
camel cmd sql myApp --query="SELECT * FROM orders"
camel cmd sql myApp --query="SELECT * FROM users" --datasource=myDS --max-rows=50
camel cmd sql myApp --query=file:query.sql
```

The DataSource is detected when there is only one; otherwise name it with `--datasource`.

> **Warning**
> The statement is executed as given, so an `UPDATE` or `DELETE` changes the database.

### Kafka consumers

`camel get kafka` lists the Kafka consumers of the routes, with their group id, topic, partition and offset:

```bash
camel get kafka
camel get kafka --committed
```

`--committed` also shows the committed offset, which asks the Kafka brokers and is therefore slower.

## Security

### Vault secrets

`camel get vault` lists the secrets the integration uses from the supported vaults (AWS Secrets Manager, Google Secret Manager, Azure Key Vault, HashiCorp Vault, Kubernetes Secrets and ConfigMaps), with when they were last updated and checked for refresh. Only the names of the secrets are shown, not their values.

```bash
camel get vault
```

## See Also

-   [Managing Integrations](camel-jbang-managing.md) — listing, stopping, logs, tracing, health checks and metrics
    
-   [Debugging](camel-jbang-debugging.md) — stepping through routes with the route debugger
    
-   [Camel TUI Observing Integrations](camel-jbang-tui-observe.md) — the same data in the terminal dashboard