# File Watch

JVM since1.0.0 Native since1.0.0

Get notified about file events in a directory using java.nio.file.WatchService.

## What’s inside

-   [File Watch component](../../../../components/4.22.x/file-watch-component.md), URI syntax: `file-watch:path`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-file-watch)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-file-watch</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

### macOS native mode limitations

Depending on the platform, the underlying Camel component configures the Directory Watcher differently in native mode.

On macOS, a `WatchService` implementation based on JNA is used to access native filesystem events. This provides better performance and scalability, compared to the JDK’s default macOS implementation.

Since JNA is not supported on GraalVM, `camel-quarkus-file-watch` cannot use the macOS-specific native `WatchService`. To maintain compatibility, the `WatchService` is forcefully overridden to `java.nio.file.WatchService`. This implementation may be slower compared to the JNA-based version.