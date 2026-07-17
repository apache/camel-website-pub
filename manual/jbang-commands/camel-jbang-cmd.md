# camel cmd

Performs commands in the running Camel integrations, such as start/stop route, or change logging levels.

## Usage

```bash
camel cmd [options]
```

## Subcommands

 
| Subcommand | Description |
| --- | --- |
| [browse](camel-jbang-cmd-browse.md) | Browse pending messages on endpoints |
| [disable-processor](camel-jbang-cmd-disable-processor.md) | Disable Camel processor |
| [enable-processor](camel-jbang-cmd-enable-processor.md) | Enable Camel processor |
| [gc](camel-jbang-cmd-gc.md) | Trigger Java Memory Garbage Collector |
| [heap-dump](camel-jbang-cmd-heap-dump.md) | Write a heap dump (.hprof) file for deep memory analysis |
| [heap-histogram](camel-jbang-cmd-heap-histogram.md) | Display class-level heap memory usage in a running Camel integration |
| [load](camel-jbang-cmd-load.md) | Loads new source files into an existing Camel |
| [logger](camel-jbang-cmd-logger.md) | List or change logging levels |
| [memory-leak](camel-jbang-cmd-memory-leak.md) | Diagnose memory leaks in a running Camel integration |
| [receive](camel-jbang-cmd-receive.md) | Receive and dump messages from remote endpoints |
| [reload](camel-jbang-cmd-reload.md) | Trigger reloading Camel |
| [reset-stats](camel-jbang-cmd-reset-stats.md) | Reset performance statistics |
| [resume-route](camel-jbang-cmd-resume-route.md) | Resume Camel routes |
| [route-diagram](camel-jbang-cmd-route-diagram.md) | Display Camel route diagram in the terminal |
| [route-dump](camel-jbang-cmd-route-dump.md) | Dump Camel route in XML, YAML, or Java DSL format |
| [route-structure](camel-jbang-cmd-route-structure.md) | Dump Camel route structure |
| [route-topology](camel-jbang-cmd-route-topology.md) | Display inter-route topology connections |
| [send](camel-jbang-cmd-send.md) | Send messages to endpoints |
| [span](camel-jbang-cmd-span.md) | Display OpenTelemetry spans from running Camel integrations |
| [sql](camel-jbang-cmd-sql.md) | Execute SQL query on a DataSource |
| [start-group](camel-jbang-cmd-start-group.md) | Start Camel route groups |
| [start-route](camel-jbang-cmd-start-route.md) | Start Camel routes |
| [stop-group](camel-jbang-cmd-stop-group.md) | Stop Camel route groups |
| [stop-route](camel-jbang-cmd-stop-route.md) | Stop Camel routes |
| [stub](camel-jbang-cmd-stub.md) | Browse stub endpoints |
| [suspend-route](camel-jbang-cmd-suspend-route.md) | Suspend Camel routes |
| [thread-dump](camel-jbang-cmd-thread-dump.md) | List threads in a running Camel integration |

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `-h,--help` | Display the help and sub-commands |  | boolean |