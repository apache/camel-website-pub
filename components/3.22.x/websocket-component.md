# Jetty Websocket

**Since Camel 2.10**

**Both producer and consumer are supported**

The WebSocket component provides websocket endpoints for communicating with clients using websocket. The component uses Eclipse Jetty Server which implements the [IETF](http://tools.ietf.org/html/rfc6455) specification (drafts and RFC 6455). It supports the protocols ws:// and wss://. To use wss:// protocol, the SSLContextParameters must be defined.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-websocket</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

websocket://hostname\[:port\]\[/resourceUri\]\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Jetty Websocket component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | The hostname. The default value is 0.0.0.0. | 0.0.0.0 | String |
| **port** (common) | The port number. The default value is 9292. | 9292 | Integer |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **staticResources** (consumer) | Set a resource path for static resources (such as .html files etc). The resources can be loaded from classpath, if you prefix with classpath:, otherwise the resources is loaded from file system or from JAR files. For example to load from root classpath use classpath:., or classpath:WEB-INF/static If not configured (eg null) then no static resource is in use. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **enableJmx** (advanced) | If this option is true, Jetty JMX support will be enabled for this endpoint. See Jetty JMX support for more details. | false | boolean |
| **maxThreads** (advanced) | To set a value for maximum number of threads in server thread pool. MaxThreads/minThreads or threadPool fields are required due to switch to Jetty9. The default values for maxThreads is 1 2 noCores. |  | Integer |
| **minThreads** (advanced) | To set a value for minimum number of threads in server thread pool. MaxThreads/minThreads or threadPool fields are required due to switch to Jetty9. The default values for minThreads is 1. |  | Integer |
| **subprotocol** (advanced) | This is a comma-separated list of subprotocols that are supported by the application. The list is in priority order. The first subprotocol on this list that is proposed by the client is the one that will be accepted. If no subprotocol on this list is proposed by the client, then the websocket connection is refused. The special value 'any' means that any subprotocol is acceptable. 'any' can be used on its own, or as a failsafe at the end of a list of more specific protocols. 'any' will also match the case where no subprotocol is proposed by the client. | any | String |
| **threadPool** (advanced) | To use a custom thread pool for the server. MaxThreads/minThreads or threadPool fields are required due to switch to Jetty9. |  | ThreadPool |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **sslKeyPassword** (security) | The password for the keystore when using SSL. |  | String |
| **sslKeystore** (security) | The path to the keystore. |  | String |
| **sslPassword** (security) | The password when using SSL. |  | String |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Jetty Websocket endpoint is configured using URI syntax:

websocket:host:port/resourceUri

with the following path and query parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | The hostname. The default value is 0.0.0.0. Setting this option on the component will use the component configured value as default. | 0.0.0.0 | String |
| **port** (common) | The port number. The default value is 9292. Setting this option on the component will use the component configured value as default. | 9292 | Integer |
| **resourceUri** (common) | **Required** Name of the websocket channel to use. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **maxBinaryMessageSize** (common) | Can be used to set the size in bytes that the websocket created by the websocketServlet may be accept before closing. (Default is -1 - or unlimited). | \-1 | Integer |
| **sessionSupport** (consumer) | Whether to enable session support which enables HttpSession for each http request. | false | boolean |
| **staticResources** (consumer) | Set a resource path for static resources (such as .html files etc). The resources can be loaded from classpath, if you prefix with classpath:, otherwise the resources is loaded from file system or from JAR files. For example to load from root classpath use classpath:., or classpath:WEB-INF/static If not configured (eg null) then no static resource is in use. |  | String |
| **subprotocol** (consumer) | This is a comma-separated list of subprotocols that are supported by the application. The list is in priority order. The first subprotocol on this list that is proposed by the client is the one that will be accepted. If no subprotocol on this list is proposed by the client, then the websocket connection is refused. The special value 'any' means that any subprotocol is acceptable. 'any' can be used on its own, or as a failsafe at the end of a list of more specific protocols. 'any' will also match the case where no subprotocol is proposed by the client. | any | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **sendTimeout** (producer) | Timeout in millis when sending to a websocket channel. The default timeout is 30000 (30 seconds). | 30000 | Integer |
| **sendToAll** (producer) | To send to all websocket subscribers. Can be used to configure on endpoint level, instead of having to use the WebsocketConstants.SEND\_TO\_ALL header on the message. |  | Boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **bufferSize** (advanced) | Set the buffer size of the websocketServlet, which is also the max frame byte size (default 8192). | 8192 | Integer |
| **maxIdleTime** (advanced) | Set the time in ms that the websocket created by the websocketServlet may be idle before closing. (default is 300000). | 300000 | Integer |
| **maxTextMessageSize** (advanced) | Can be used to set the size in characters that the websocket created by the websocketServlet may be accept before closing. |  | Integer |
| **minVersion** (advanced) | Can be used to set the minimum protocol version accepted for the websocketServlet. (Default 13 - the RFC6455 version). | 13 | Integer |
| **allowedOrigins** (cors) | The CORS allowed origins. Use to allow all. |  | String |
| **crossOriginFilterOn** (cors) | Whether to enable CORS. | false | boolean |
| **filterPath** (cors) | Context path for filtering CORS. |  | String |
| **enableJmx** (monitoring) | If this option is true, Jetty JMX support will be enabled for this endpoint. See Jetty JMX support for more details. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |

## Message Headers

The Jetty Websocket component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **websocket.connectionKey** (common) Constant: [`CONNECTION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-websocket/latest/org/apache/camel/component/websocket/WebsocketConstants.html#CONNECTION_KEY) | Producer: Sends the message to all clients which are currently connected. You can use the sendToAll option on the endpoint instead of using this header. Consumer: Connection key identifying an individual client connection. You can save this and specify it again when routing to a producer endpoing in order to direct messages to a specific connected client. |  | String |
| **websocket.sendToAll** (producer) Constant: [`SEND_TO_ALL`](https://javadoc.io/doc/org.apache.camel/camel-websocket/latest/org/apache/camel/component/websocket/WebsocketConstants.html#SEND_TO_ALL) | Sends the message to all clients which are currently connected. You can use the sendToAll option on the endpoint instead of using this header. |  | Boolean |
| **websocket.remoteAddress** (consumer) Constant: [`REMOTE_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-websocket/latest/org/apache/camel/component/websocket/WebsocketConstants.html#REMOTE_ADDRESS) | Remote address of the websocket session. |  | InetSocketAddress |
| **websocket.subprotocol** (consumer) Constant: [`SUBPROTOCOL`](https://javadoc.io/doc/org.apache.camel/camel-websocket/latest/org/apache/camel/component/websocket/WebsocketConstants.html#SUBPROTOCOL) | If a specific subprotocol was negotiated, it will be specfied in this header. Note that if you specify the any subprotocol to be supported, and a client requests a specific subprotocol, the connection will be accepted without a specific subprotocol being used. You need to specifically support a given protocol by name if you want it returned to the client and to show up in the message header. |  | String |
| **websocket.relativePath** (consumer) Constant: [`RELATIVE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-websocket/latest/org/apache/camel/component/websocket/WebsocketConstants.html#RELATIVE_PATH) | If you specify a wildcard URI path for an endpoint, and a websocket client connects to that websocket endpoing, the relative path that the client specified will be provided in this header. For example, if you specified websocket://0.0.0.0:80/api/ as your endpoint URI, and a client connects to the server at ws://host.com/api/specialized/apipath then specialized/apipath is provided in the relative path header of all messages from that client. |  | String |

## Usage

In this example we let Camel exposes a websocket server which clients can communicate with. The websocket server uses the default host and port, which would be `0.0.0.0:9292`.  
The example will send back an echo of the input. To send back a message, we need to send the transformed message to the same endpoint `"websocket://echo"`. This is needed  
because by default the messaging is InOnly.

This example is part of an unit test, which you can find [here](https://svn.apache.org/repos/asf/camel/trunk/components/camel-websocket/src/test/java/org/apache/camel/component/websocket/WebsocketRouteExampleTest.java). As a client we use Java’s own HTTP client which offers support for web socket as well.

Here is another example where webapp resources location have been defined to allow the Jetty Application Server to not only register the WebSocket servlet but also to expose web resources for the browser. Resources should be defined under the webapp directory.

```java
from("activemq:topic:newsTopic")
   .routeId("fromJMStoWebSocket")
   .to("websocket://localhost:8443/newsTopic?sendToAll=true&staticResources=classpath:webapp");
```

## Setting up SSL for WebSocket Component

### Using the JSSE Configuration Utility

The WebSocket component supports SSL/TLS configuration through the [Camel JSSE Configuration Utility](../../manual/camel-configuration-utilities.md). This utility greatly decreases the amount of component specific code you need to write and is configurable at the endpoint and component levels. The following examples demonstrate how to use the utility with the Cometd component.

Programmatic configuration of the component

```java
KeyStoreParameters ksp = new KeyStoreParameters();
ksp.setResource("/users/home/server/keystore.jks");
ksp.setPassword("keystorePassword");

KeyManagersParameters kmp = new KeyManagersParameters();
kmp.setKeyStore(ksp);
kmp.setKeyPassword("keyPassword");

TrustManagersParameters tmp = new TrustManagersParameters();
tmp.setKeyStore(ksp);

SSLContextParameters scp = new SSLContextParameters();
scp.setKeyManagers(kmp);
scp.setTrustManagers(tmp);

CometdComponent commetdComponent = getContext().getComponent("cometds", CometdComponent.class);
commetdComponent.setSslContextParameters(scp);
```

Spring DSL based configuration of endpoint

```xml
...
  <camel:sslContextParameters
      id="sslContextParameters">
    <camel:keyManagers
        keyPassword="keyPassword">
      <camel:keyStore
          resource="/users/home/server/keystore.jks"
          password="keystorePassword"/>
    </camel:keyManagers>
    <camel:trustManagers>
      <camel:keyStore
          resource="/users/home/server/keystore.jks"
          password="keystorePassword"/>
    </camel:trustManagers>
  </camel:sslContextParameters>...
...
  <to uri="websocket://127.0.0.1:8443/test?sslContextParameters=#sslContextParameters"/>...
```

Java DSL based configuration of endpoint

```java
...
    protected RouteBuilder createRouteBuilder() throws Exception {
        return new RouteBuilder() {
            public void configure() {

                String uri = "websocket://127.0.0.1:8443/test?sslContextParameters=#sslContextParameters";

                from(uri)
                     .log(">>> Message received from WebSocket Client : ${body}")
                     .to("mock:client")
                     .loop(10)
                         .setBody().constant(">> Welcome on board!")
                         .to(uri);
...
```

## Spring Boot Auto-Configuration

When using websocket with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-websocket-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 17 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.websocket.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.websocket.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.websocket.enable-jmx** | If this option is true, Jetty JMX support will be enabled for this endpoint. See Jetty JMX support for more details. | false | Boolean |
| **camel.component.websocket.enabled** | Whether to enable auto configuration of the websocket component. This is enabled by default. |  | Boolean |
| **camel.component.websocket.host** | The hostname. The default value is 0.0.0.0. | 0.0.0.0 | String |
| **camel.component.websocket.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.websocket.max-threads** | To set a value for maximum number of threads in server thread pool. MaxThreads/minThreads or threadPool fields are required due to switch to Jetty9. The default values for maxThreads is 1 2 noCores. |  | Integer |
| **camel.component.websocket.min-threads** | To set a value for minimum number of threads in server thread pool. MaxThreads/minThreads or threadPool fields are required due to switch to Jetty9. The default values for minThreads is 1. |  | Integer |
| **camel.component.websocket.port** | The port number. The default value is 9292. | 9292 | Integer |
| **camel.component.websocket.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.websocket.ssl-key-password** | The password for the keystore when using SSL. |  | String |
| **camel.component.websocket.ssl-keystore** | The path to the keystore. |  | String |
| **camel.component.websocket.ssl-password** | The password when using SSL. |  | String |
| **camel.component.websocket.static-resources** | Set a resource path for static resources (such as .html files etc). The resources can be loaded from classpath, if you prefix with classpath:, otherwise the resources is loaded from file system or from JAR files. For example to load from root classpath use classpath:., or classpath:WEB-INF/static If not configured (eg null) then no static resource is in use. |  | String |
| **camel.component.websocket.subprotocol** | This is a comma-separated list of subprotocols that are supported by the application. The list is in priority order. The first subprotocol on this list that is proposed by the client is the one that will be accepted. If no subprotocol on this list is proposed by the client, then the websocket connection is refused. The special value 'any' means that any subprotocol is acceptable. 'any' can be used on its own, or as a failsafe at the end of a list of more specific protocols. 'any' will also match the case where no subprotocol is proposed by the client. | any | String |
| **camel.component.websocket.thread-pool** | To use a custom thread pool for the server. MaxThreads/minThreads or threadPool fields are required due to switch to Jetty9. The option is a org.eclipse.jetty.util.thread.ThreadPool type. |  | ThreadPool |
| **camel.component.websocket.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |