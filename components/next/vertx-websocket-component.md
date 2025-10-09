# Vert.x WebSocket

**Since Camel 3.5**

**Both producer and consumer are supported**

The [Vert.x](http://vertx.io/) WebSocket component provides WebSocket capabilities as a WebSocket server, or as a client to connect to an existing WebSocket.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-vertx-websocket</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

vertx-websocket://hostname\[:port\]\[/resourceUri\]\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Vert.x WebSocket component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **allowOriginHeader** (advanced) | Whether the WebSocket client should add the Origin header to the WebSocket handshake request. | true | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **defaultHost** (advanced) | Default value for host name that the WebSocket should bind to. | 0.0.0.0 | String |
| **defaultPort** (advanced) | Default value for the port that the WebSocket should bind to. | 0 | int |
| **originHeaderUrl** (advanced) | The value of the Origin header that the WebSocket client should use on the WebSocket handshake request. When not specified, the WebSocket client will automatically determine the value for the Origin from the request URL. |  | String |
| **router** (advanced) | To provide a custom vertx router to use on the WebSocket server. |  | Router |
| **vertx** (advanced) | To use an existing vertx instead of creating a new instance. |  | Vertx |
| **vertxOptions** (advanced) | To provide a custom set of vertx options for configuring vertx. |  | VertxOptions |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Vert.x WebSocket endpoint is configured using URI syntax:

vertx-websocket:host:port/path

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** WebSocket hostname, such as localhost or a remote host when in client mode. |  | String |
| **port** (common) | **Required** WebSocket port number to use. |  | int |
| **path** (common) | WebSocket path to use. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowedOriginPattern** (consumer) | Regex pattern to match the origin header sent by WebSocket clients. |  | String |
| **consumeAsClient** (consumer) | When set to true, the consumer acts as a WebSocket client, creating exchanges on each received WebSocket event. | false | boolean |
| **fireWebSocketConnectionEvents** (consumer) | Whether the server consumer will create a message exchange when a new WebSocket peer connects or disconnects. | false | boolean |
| **maxReconnectAttempts** (consumer) | When consumeAsClient is set to true this sets the maximum number of allowed reconnection attempts to a previously closed WebSocket. A value of 0 (the default) will attempt to reconnect indefinitely. |  | int |
| **reconnectInitialDelay** (consumer) | When consumeAsClient is set to true this sets the initial delay in milliseconds before attempting to reconnect to a previously closed WebSocket. |  | int |
| **reconnectInterval** (consumer) | When consumeAsClient is set to true this sets the interval in milliseconds at which reconnecting to a previously closed WebSocket occurs. | 1000 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **router** (consumer (advanced)) | To use an existing vertx router for the HTTP server. |  | Router |
| **serverOptions** (consumer (advanced)) | Sets customized options for configuring the HTTP server hosting the WebSocket for the consumer. |  | HttpServerOptions |
| **clientSubProtocols** (producer) | Comma separated list of WebSocket subprotocols that the client should use for the Sec-WebSocket-Protocol header. |  | String |
| **sendToAll** (producer) | To send to all websocket subscribers. Can be used to configure at the endpoint level, instead of providing the VertxWebsocketConstants.SEND\_TO\_ALL header on the message. Note that when using this option, the host name specified for the vertx-websocket producer URI must match one used for an existing vertx-websocket consumer. Note that this option only applies when producing messages to endpoints hosted by the vertx-websocket consumer and not to an externally hosted WebSocket. | false | boolean |
| **clientOptions** (producer (advanced)) | Sets customized options for configuring the WebSocket client used in the producer. |  | HttpClientOptions |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **allowOriginHeader** (security) | Whether the WebSocket client should add the Origin header to the WebSocket handshake request. | true | boolean |
| **handshakeHeaders** (security) | Headers to send in the HTTP handshake request. When the endpoint is a consumer, it only works when it consumes a remote host as a client (i.e. consumeAsClient is true). This is a multi-value option with prefix: handshake. |  | Map |
| **originHeaderUrl** (security) | The value of the Origin header that the WebSocket client should use on the WebSocket handshake request. When not specified, the WebSocket client will automatically determine the value for the Origin from the request URL. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |

## Message Headers

The Vert.x WebSocket component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelVertxWebsocket.connectionKey** (common) Constant: [`CONNECTION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-vertx-websocket/latest/org/apache/camel/component/vertx/websocket/VertxWebsocketConstants.html#CONNECTION_KEY) | Sends the message to the client with the given connection key. You can use a comma separated list of keys to send a message to multiple clients. Note that this option only applies when producing messages to endpoints hosted by the vertx-websocket consumer and not to an externally hosted WebSocket. |  | String |
| **CamelVertxWebsocket.sendToAll** (producer) Constant: [`SEND_TO_ALL`](https://javadoc.io/doc/org.apache.camel/camel-vertx-websocket/latest/org/apache/camel/component/vertx/websocket/VertxWebsocketConstants.html#SEND_TO_ALL) | Sends the message to all clients which are currently connected. You can use the sendToAll option on the endpoint instead of using this header. Note that this option only applies when producing messages to endpoints hosted by the vertx-websocket consumer and not to an externally hosted WebSocket. |  | boolean |
| **CamelVertxWebsocket.remoteAddress** (consumer) Constant: [`REMOTE_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-vertx-websocket/latest/org/apache/camel/component/vertx/websocket/VertxWebsocketConstants.html#REMOTE_ADDRESS) | The remote address. |  | SocketAddress |
| **CamelVertxWebsocket.event** (consumer) Constant: [`EVENT`](https://javadoc.io/doc/org.apache.camel/camel-vertx-websocket/latest/org/apache/camel/component/vertx/websocket/VertxWebsocketConstants.html#EVENT) | 
The WebSocket event that triggered the message exchange.

Enum values:

-   CLOSE
    
-   ERROR
    
-   MESSAGE
    
-   OPEN
    





 |  | VertxWebsocketEvent |

## Usage

The following example shows how to expose a WebSocket on [http://localhost:8080/echo](http://localhost:8080/echo) and returns an '_echo_' response back to the same channel:

```java
from("vertx-websocket:localhost:8080/echo")
    .transform().simple("Echo: ${body}")
    .to("vertx-websocket:localhost:8080/echo");
```

It’s also possible to configure the consumer to connect as a WebSocket client on a remote address with the `consumeAsClient` option:

```java
from("vertx-websocket:my.websocket.com:8080/chat?consumeAsClient=true")
    .log("Got WebSocket message ${body}");
```

### Path & query parameters

The WebSocket server consumer supports the configuration of parameterized paths. The path parameter value will be set as a Camel exchange header:

```java
from("vertx-websocket:localhost:8080/chat/{user}")
    .log("New message from ${header.user} >>> ${body}")
```

Similarly, you can retrieve any query parameter values used by the WebSocket client to connect to the server endpoint:

```java
from("direct:sendChatMessage")
    .to("vertx-websocket:localhost:8080/chat/camel?role=admin");

from("vertx-websocket:localhost:8080/chat/{user}")
    .log("New message from ${header.user} (${header.role}) >>> ${body}")
```

### Sending messages to peers connected to the vertx-websocket server consumer

> **Note**
> This section only applies when producing messages to a WebSocket hosted by the camel-vertx-websocket consumer. It is not relevant when producing messages to an externally hosted WebSocket.

To send a message to all peers connected to a WebSocket hosted by the vertx-websocket server consumer, use the `sendToAll=true` endpoint option, or the `CamelVertxWebsocket.sendToAll` header.

```java
from("vertx-websocket:localhost:8080/chat")
    .log("Got WebSocket message ${body}");

from("direct:broadcastMessage")
    .setBody().constant("This is a broadcast message!")
    .to("vertx-websocket:localhost:8080/chat?sendToAll=true");
```

Alternatively, you can send messages to specific peers by using the `CamelVertxWebsocket.connectionKey` header. Multiple peers can be specified as a comma separated list.

The value of the `connectionKey` can be determined whenever a peer triggers an event on the vertx-websocket consumer, where a unique key identifying the peer will be propagated via the `CamelVertxWebsocket.connectionKey` header.

```java
from("vertx-websocket:localhost:8080/chat")
    .log("Got WebSocket message ${body}");

from("direct:broadcastMessage")
    .setBody().constant("This is a broadcast message!")
    .setHeader(VertxWebsocketConstants.CONNECTION_KEY).constant("key-1,key-2,key-3")
    .to("vertx-websocket:localhost:8080/chat");
```

### SSL

By default, the `ws://` protocol is used, but secure connections with `wss://` are supported by configuring the consumer or producer via the `sslContextParameters` URI parameter and the [Camel JSSE Configuration Utility](../../manual/camel-configuration-utilities.md)

## Spring Boot Auto-Configuration

When using vertx-websocket with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-vertx-websocket-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 12 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.vertx-websocket.allow-origin-header** | Whether the WebSocket client should add the Origin header to the WebSocket handshake request. | true | Boolean |
| **camel.component.vertx-websocket.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.vertx-websocket.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.vertx-websocket.default-host** | Default value for host name that the WebSocket should bind to. | 0.0.0.0 | String |
| **camel.component.vertx-websocket.default-port** | Default value for the port that the WebSocket should bind to. | 0 | Integer |
| **camel.component.vertx-websocket.enabled** | Whether to enable auto configuration of the vertx-websocket component. This is enabled by default. |  | Boolean |
| **camel.component.vertx-websocket.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.vertx-websocket.origin-header-url** | The value of the Origin header that the WebSocket client should use on the WebSocket handshake request. When not specified, the WebSocket client will automatically determine the value for the Origin from the request URL. |  | String |
| **camel.component.vertx-websocket.router** | To provide a custom vertx router to use on the WebSocket server. The option is a io.vertx.ext.web.Router type. |  | Router |
| **camel.component.vertx-websocket.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.vertx-websocket.vertx** | To use an existing vertx instead of creating a new instance. The option is a io.vertx.core.Vertx type. |  | Vertx |
| **camel.component.vertx-websocket.vertx-options** | To provide a custom set of vertx options for configuring vertx. The option is a io.vertx.core.VertxOptions type. |  | VertxOptions |