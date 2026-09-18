# A2A

JVM since3.38.0 Native since3.38.0

A2A endpoint for agent-to-agent communication.

## What’s inside

-   [A2A component](../../../../components/4.22.x/a2a-component.md), URI syntax: `a2a:agentCardSource`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-a2a)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-a2a</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Agent Card JSON files in native mode

If you use JSON files to define agent cards that are loaded from the classpath, you must ensure they are included in the native image. Add the `quarkus.native.resources.includes` configuration property to `application.properties`. For example:

```properties
quarkus.native.resources.includes=cards/*.json
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resources in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).

## Camel Quarkus limitations

### `HTTP+JSON` protocol binding not supported

The [A2A component](../../../../components/4.22.x/a2a-component.md) supports two protocol bindings: `JSONRPC` and `HTTP+JSON`. Only the `JSONRPC` binding works with the default Quarkus HTTP server (Vert.x / `platform-http`).

The `HTTP+JSON` binding uses A2A custom-method paths that contain colons, such as `/message:send`. Vert.x Web does not support colon characters in URI path segments, causing these routes to fail.