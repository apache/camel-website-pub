# File Watch

JVM since1.0.0 Native since1.0.0

Get notified about file events in a directory using java.nio.file.WatchService.

## What’s inside

-   [File Watch component](../../../../components/4.14.x/file-watch-component.md), URI syntax: `file-watch:path`
    

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

The underlying Camel component configures the Directory Watcher in a platform specific way:

-   On Mac, the `io.methvin.watchservice.MacOSXListeningWatchService` is used that depends on `[net.java.dev.jna:jna](https://github.com/java-native-access/jna)`.
    
-   Other platforms use `java.nio.file.WatchService` provided by the Java Runtime.
    

Because JNA is [not supported on GraalVM](https://github.com/oracle/graal/issues/673) yet, we made the component to behave differently on Camel Quarkus: We are substituting the respective Directory Watcher method do use the stock `java.nio.file.WatchService` also on Mac.