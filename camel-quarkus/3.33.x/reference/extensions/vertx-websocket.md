# Vert.x WebSocket

JVM since1.1.0 Native since1.1.0

This extension enables you to create WebSocket endpoints to that act as either a WebSocket server, or as a client to connect an existing WebSocket .

It is built on top of the Eclipse Vert.x HTTP server provided by the `quarkus-vertx-http` extension.

## What’s inside

-   [Vert.x WebSocket component](../../../../components/4.18.x/vertx-websocket-component.md), URI syntax: `vertx-websocket:host:port/path`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-vertx-websocket)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-vertx-websocket</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Vert.x WebSocket consumers

When you create a Vert.x WebSocket consumer (E.g. with `from("vertx-websocket")`), the host and port configuration in the URI are redundant since the WebSocket will always be hosted on the Quarkus HTTP server.

The configuration of the consumer can be simplified to only include the resource path of the WebSocket. For example.

```java
from("vertx-websocket:/my-websocket-path")
    .setBody().constant("Hello World");
```

> **Note**
> While you do not need to explicitly configure the host/port on the vertx-websocket consumer. If you choose to, the host & port must exactly match the value of the Quarkus HTTP server configuration values for `quarkus.http.host` and `quarkus.http.port`. Otherwise, an exception will be thrown at runtime.

### Vert.x WebSocket producers

Similar to above, if you want to produce messages to the internal Vert.x WebSocket consumer, then you can omit the host and port from the endpoint URI.

```java
from("vertx-websocket:/my-websocket-path")
    .log("Got body: ${body}");

from("direct:sendToWebSocket")
    .log("vertx-websocket:/my-websocket-path");
```

Or alternatively, you can refer to the full host & port configuration for the Quarkus HTTP server.

```java
from("direct:sendToWebSocket")
    .log("vertx-websocket:{{quarkus.http.host}}:{{quarkus.http.port}}/my-websocket-path");
```

When producing messages to an external WebSocket server, then you must always provide the host name and port (if required).

## Additional Camel Quarkus configuration

### Vert.x WebSocket server configuration

Configuration of the Vert.x WebSocket server is managed by Quarkus. Refer to the [Quarkus HTTP configuration guide](https://quarkus.io/guides/all-config#quarkus-vertx-http_quarkus-vertx-http-eclipse-vert.x-http) for the full list of configuration options.

To configure SSL for the Vert.x WebSocket server, follow the [secure connections with SSL guide](https://quarkus.io/guides/http-reference#ssl). Note that configuring the server for SSL with `SSLContextParameters` is not currently supported.

### Character encodings

Check the [Character encodings section](../../user-guide/native-mode.html#charsets) of the Native mode guide if you expect your application to send or receive requests using non-default encodings.