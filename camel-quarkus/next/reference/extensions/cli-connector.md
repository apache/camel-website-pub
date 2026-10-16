# CLI Connector

JVM since3.2.0 Nativeunsupported

Runtime adapter connecting with Camel CLI

## What’s inside

-   [CLI Connector](../../../../components/next/others/cli-connector.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-cli-connector</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### WebSocket transport

With `camel.cli.transport=websocket`, the application dials out to a developer tool over a WebSocket instead of exchanging files with the Camel CLI (see the [CLI Connector](../../../../components/next/others/cli-connector.md) documentation for the protocol and the options).

```properties
%dev.camel.cli.transport = websocket
%dev.camel.cli.websocket.url = ws://127.0.0.1:8000/connect?executionId=run-1
```

The tool gets full control of the application: the transport refuses to start with the Quarkus `prod` profile (the default profile of a packaged application), as with the Camel `prod` profile (`camel.main.profile=prod`). To use it from a packaged application, for example on a remote development cluster, run it with another profile.

#### WebSocket client

The connector uses the Vert.x WebSocket client of the application. The client in use is logged at startup (`Camel CLI connector uses the vertx WebSocket client`) and reported to the tool. Set `camel.cli.websocket.client=jdk` to use the JDK WebSocket client instead.

For a `wss://` tool, `quarkus.camel.cli.websocket.tls-configuration-name` selects a TLS configuration of the [Quarkus TLS registry](https://quarkus.io/guides/tls-registry-reference); otherwise the JVM default trust store is used.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.cli.enabled](#quarkus-camel-cli-enabled)`
Sets whether to enable Camel CLI Connector support.

 | `boolean` | `true` |
| `[quarkus.camel.cli.websocket.tls-configuration-name](#quarkus-camel-cli-websocket-tls-configuration-name)`

The name of the TLS configuration (from the Quarkus TLS registry) used to connect to a `wss://` tool. When not set, the JVM default trust store is used.

 | `string` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.