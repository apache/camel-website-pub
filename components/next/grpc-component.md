# gRPC

**Since Camel 2.19**

**Both producer and consumer are supported**

The gRPC component allows you to call or expose Remote Procedure Call (RPC) services using [Protocol Buffers (protobuf)](https://developers.google.com/protocol-buffers/docs/overview) exchange format over HTTP/2 transport.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-grpc</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

grpc:host:port/service\[?options\]

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

The gRPC component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The gRPC endpoint is configured using URI syntax:

grpc:host:port/service

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** The gRPC server host name. This is localhost or 0.0.0.0 when being a consumer or remote server host name when using producer. |  | String |
| **port** (common) | **Required** The gRPC local or remote server port. |  | int |
| **service** (common) | **Required** Fully qualified service name from the protocol buffer descriptor file (package dot service definition name). |  | String |

### Query Parameters (42 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **flowControlWindow** (common) | The HTTP/2 flow control window size (MiB). | 1048576 | int |
| **maxMessageSize** (common) | The maximum message size allowed to be received/sent (MiB). | 4194304 | int |
| **autoDiscoverServerInterceptors** (consumer) | Setting the autoDiscoverServerInterceptors mechanism, if true, the component will look for a ServerInterceptor instance in the registry automatically otherwise it will skip that checking. | true | boolean |
| **consumerStrategy** (consumer) | 
This option specifies the top-level strategy for processing service requests and responses in streaming mode. If an aggregation strategy is selected, all requests will be accumulated in the list, then transferred to the flow, and the accumulated responses will be sent to the sender. If a propagation strategy is selected, request is sent to the stream, and the response will be immediately sent back to the sender. If a delegation strategy is selected, request is sent to the stream, but no response generated under the assumption that all necessary responses will be sent at another part of route. Delegation strategy always comes with routeControlledStreamObserver=true to be able to achieve the assumption.

Enum values:

-   AGGREGATION
    
-   PROPAGATION
    
-   DELEGATION
    





 | PROPAGATION | GrpcConsumerStrategy |
| **forwardOnCompleted** (consumer) | Determines if onCompleted events should be pushed to the Camel route. | false | boolean |
| **forwardOnError** (consumer) | Determines if onError events should be pushed to the Camel route. Exceptions will be set as message body. | false | boolean |
| **initialFlowControlWindow** (consumer) | Sets the initial flow control window in bytes. | 1048576 | int |
| **keepAliveTime** (consumer) | Sets a custom keepalive time in milliseconds, the delay time for sending next keepalive ping. A value of Long.MAX\_VALUE or a value greater or equal to NettyServerBuilder.AS\_LARGE\_AS\_INFINITE will disable keepalive. | 7200000 | long |
| **keepAliveTimeout** (consumer) | Sets a custom keepalive timeout in milliseconds, the timeout for keepalive ping requests. | 20000 | long |
| **maxConcurrentCallsPerConnection** (consumer) | The maximum number of concurrent calls permitted for each incoming server connection. Defaults to no limit. | 2147483647 | int |
| **maxConnectionAge** (consumer) | Sets a custom max connection age in milliseconds. Connections lasting longer than which will be gracefully terminated. A random jitter of /-10% will be added to the value. A value of Long.MAX\_VALUE (the default) or a value greater or equal to NettyServerBuilder.AS\_LARGE\_AS\_INFINITE will disable max connection age. | 9223372036854776000 | long |
| **maxConnectionAgeGrace** (consumer) | Sets a custom grace time in milliseconds for the graceful connection termination. A value of Long.MAX\_VALUE (the default) or a value greater or equal to NettyServerBuilder.AS\_LARGE\_AS\_INFINITE is considered infinite. | 9223372036854776000 | long |
| **maxConnectionIdle** (consumer) | Sets a custom max connection idle time in milliseconds. Connection being idle for longer than which will be gracefully terminated. A value of Long.MAX\_VALUE (the default) or a value greater or equal to NettyServerBuilder.AS\_LARGE\_AS\_INFINITE will disable max connection idle. | 9223372036854776000 | long |
| **maxInboundMetadataSize** (consumer) | Sets the maximum size of metadata allowed to be received. The default is 8 KiB. | 8192 | int |
| **maxRstFramesPerWindow** (consumer) | Limits the rate of incoming RST\_STREAM frames per connection to maxRstFramesPerWindow per maxRstPeriodSeconds. This option MUST be used in conjunction with maxRstPeriodSeconds for it to be effective. | 0 | int |
| **maxRstPeriodSeconds** (consumer) | Limits the rate of incoming RST\_STREAM frames per maxRstPeriodSeconds. This option MUST be used in conjunction with maxRstFramesPerWindow for it to be effective. | 0 | int |
| **permitKeepAliveTime** (consumer) | Sets the most aggressive keep-alive time in milliseconds that clients are permitted to configure. The server will try to detect clients exceeding this rate and will forcefully close the connection. | 300000 | long |
| **permitKeepAliveWithoutCalls** (consumer) | Sets whether to allow clients to send keep-alive HTTP/ 2 PINGs even if there are no outstanding RPCs on the connection. | false | boolean |
| **routeControlledStreamObserver** (consumer) | Lets the route to take control over stream observer. If this value is set to true, then the response observer of gRPC call will be set with the name GrpcConstants.GRPC\_RESPONSE\_OBSERVER in the Exchange object. Please note that the stream observer’s onNext(), onError(), onCompleted() methods should be called in the route. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **autoDiscoverClientInterceptors** (producer) | Setting the autoDiscoverClientInterceptors mechanism, if true, the component will look for a ClientInterceptor instance in the registry automatically otherwise it will skip that checking. | true | boolean |
| **inheritExchangePropertiesForReplies** (producer) | Copies exchange properties from original exchange to all exchanges created for route defined by streamRepliesTo. | false | boolean |
| **method** (producer) | gRPC method name. |  | String |
| **producerStrategy** (producer) | 

The mode used to communicate with a remote gRPC server. In SIMPLE mode a single exchange is translated into a remote procedure call. In STREAMING mode all exchanges will be sent within the same request (input and output of the recipient gRPC service must be of type 'stream').

Enum values:

-   SIMPLE
    
-   STREAMING
    





 | SIMPLE | GrpcProducerStrategy |
| **streamRepliesTo** (producer) | When using STREAMING client mode, it indicates the endpoint where responses should be forwarded. |  | String |
| **toRouteControlledStreamObserver** (producer) | Expects that exchange property GrpcConstants.GRPC\_RESPONSE\_OBSERVER is set. Takes its value and calls onNext, onError and onComplete on that StreamObserver. All other gRPC parameters are ignored. | false | boolean |
| **userAgent** (producer) | The user agent header passed to the server. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **authenticationType** (security) | 

Authentication method type in advance to the SSL/TLS negotiation.

Enum values:

-   NONE
    
-   GOOGLE
    
-   JWT
    





 | NONE | GrpcAuthType |
| **jwtAlgorithm** (security) | 

JSON Web Token sign algorithm.

Enum values:

-   HMAC256
    
-   HMAC384
    
-   HMAC512
    
-   RSA256
    
-   RSA384
    
-   RSA512
    





 | HMAC256 | JwtAlgorithm |
| **jwtIssuer** (security) | JSON Web Token issuer. |  | String |
| **jwtSecret** (security) | JSON Web Token secret. |  | String |
| **jwtSubject** (security) | JSON Web Token subject. |  | String |
| **keyCertChainResource** (security) | The X.509 certificate chain file resource in PEM format link. |  | String |
| **keyPassword** (security) | The PKCS#8 private key file password. |  | String |
| **keyResource** (security) | The PKCS#8 private key file resource in PEM format link. |  | String |
| **negotiationType** (security) | 

Identifies the security negotiation type used for HTTP/2 communication.

Enum values:

-   PLAINTEXT
    
-   TLS
    





 | PLAINTEXT | NegotiationType |
| **serviceAccountResource** (security) | Service Account key file in JSON format resource link supported by the Google Cloud SDK. |  | String |
| **trustCertCollectionResource** (security) | The trusted certificates collection file resource in PEM format for verifying the remote endpoint’s certificate. |  | String |

## Message Headers

The gRPC component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGrpcMethodName** (consumer) Constant: [`GRPC_METHOD_NAME_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-grpc/latest/org/apache/camel/component/grpc/GrpcConstants.html#GRPC_METHOD_NAME_HEADER) | Method name handled by the consumer service. |  | String |
| **CamelGrpcUserAgent** (consumer) Constant: [`GRPC_USER_AGENT_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-grpc/latest/org/apache/camel/component/grpc/GrpcConstants.html#GRPC_USER_AGENT_HEADER) | If provided, the given agent will prepend the gRPC library’s user agent information. |  | String |
| **CamelGrpcEventType** (consumer) Constant: [`GRPC_EVENT_TYPE_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-grpc/latest/org/apache/camel/component/grpc/GrpcConstants.html#GRPC_EVENT_TYPE_HEADER) | Received event type from the sent request. Possible values: onNext onCompleted onError. |  | String |

## Usage

### Transport security and authentication support

The following [authentication](https://grpc.io/docs/guides/auth.md) mechanisms are built-in to gRPC and available in this component:

-   **SSL/TLS:** gRPC has SSL/TLS integration and promotes the use of SSL/TLS to authenticate the server, and to encrypt all the data exchanged between the client and the server. Optional mechanisms are available for clients to provide certificates for mutual authentication.
    
-   **Token-based authentication with Google:** gRPC provides a generic mechanism to attach metadata-based credentials to requests and responses. Additional support for acquiring access tokens while accessing Google APIs through gRPC is provided. In general, this mechanism must be used as well as SSL/TLS on the channel.
    

To enable these features, the following component properties combinations must be configured:

    
| Num. | Option | Parameter | Value | Required/Optional |
| --- | --- | --- | --- | --- |
| 1 | **SSL/TLS** | negotiationType | TLS | Required |
|  |  | keyCertChainResource |  | Required |
|  |  | keyResource |  | Required |
|  |  | keyPassword |  | Optional |
|  |  | trustCertCollectionResource |  | Optional |
| 2 | **Token-based authentication with Google API** | authenticationType | GOOGLE | Required |
|  |  | negotiationType | TLS | Required |
|  |  | serviceAccountResource |  | Required |
| 3 | **Custom JSON Web Token implementation authentication** | authenticationType | JWT | Required |
|  |  | negotiationType | NONE or TLS | Optional. The TLS/SSL not checking for this type, but strongly recommended. |
|  |  | jwtAlgorithm | HMAC256(default) or (HMAC384,HMAC512) | Optional |
|  |  | jwtSecret |  | Required |
|  |  | jwtIssuer |  | Optional |
|  |  | jwtSubject |  | Optional |

### gRPC producer resource type mapping

The table below shows the types of objects in the message body, depending on the types (simple or stream) of incoming and outgoing parameters, as well as the invocation style (synchronous or asynchronous). Please note that invocation of the procedures with incoming stream parameter in asynchronous style is not allowed.

    
| Invocation style | Request type | Response type | Request Body Type | Result Body Type |
| --- | --- | --- | --- | --- |
| **synchronous** | simple | simple | Object | Object |
| **synchronous** | simple | stream | Object | List<Object> |
| synchronous | stream | simple | not allowed | not allowed |
| synchronous | stream | stream | not allowed | not allowed |
| **asynchronous** | simple | simple | Object | List<Object> |
| **asynchronous** | simple | stream | Object | List<Object> |
| **asynchronous** | stream | simple | Object or List<Object> | List<Object> |
| **asynchronous** | stream | stream | Object or List<Object> | List<Object> |

### gRPC Proxy

It is not possible to create a universal proxy-route for all methods, so you need to divide your gRPC service into several services by method’s type: unary, server streaming, client streaming and bidirectional streaming.

#### Unary

For unary requests, it is enough to write the following code:

-   Java
    
-   XML
    
-   YAML
    

```java
from("grpc://localhost:1101/org.apache.camel.component.grpc.PingPong")
    .toD("grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=${header.CamelGrpcMethodName}");
```

```xml
<route>
  <from uri="grpc://localhost:1101/org.apache.camel.component.grpc.PingPong"/>
  <toD uri="grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=${header.CamelGrpcMethodName}"/>
</route>
```

```yaml
- route:
    from:
      uri: grpc://localhost:1101/org.apache.camel.component.grpc.PingPong
      steps:
        - toD:
            uri: grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong
            parameters:
              method: "${header.CamelGrpcMethodName}"
```

### Server streaming

Server streaming may be done by the same approach as unary, but in that configuration Camel route will wait stream for completion and will aggregate all responses to a list before sending that data as response stream. If this behavior is unacceptable, you need to apply a number of options:

1.  Set `routeControlledStreamObserver=true` for consumer. Later it will be used to publish responses;
    
2.  Set `streamRepliesTo` option for producer to handle streaming nature of responses;
    
3.  Set forwarding of `onError` and `onCompleted` for producer;
    
4.  Set `inheritExchangePropertiesForReplies=true` to inherit `StreamObserver` obtained on the first step;
    
5.  Create another route to process streamed data. That route must contain gRPC-producer step with the only parameter `toRouteControlledStreamObserver=true` which will publish incoming exchanges as response stream elements.
    

Example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?routeControlledStreamObserver=true")
    .toD("grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=${header.CamelGrpcMethodName}&streamRepliesTo=direct:next&forwardOnError=true&forwardOnCompleted=true&inheritExchangePropertiesForReplies=true");

from("direct:next")
    .to("grpc://dummy:0/?toRouteControlledStreamObserver=true");
```

```xml
<route>
  <from uri="grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?routeControlledStreamObserver=true"/>
  <toD uri="grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=${header.CamelGrpcMethodName}&amp;streamRepliesTo=direct:next&amp;forwardOnError=true&amp;forwardOnCompleted=true&amp;inheritExchangePropertiesForReplies=true"/>
</route>
<route>
  <from uri="direct:next"/>
  <to uri="grpc://dummy:0/?toRouteControlledStreamObserver=true"/>
</route>
```

```yaml
- route:
    from:
      uri: grpc://localhost:1101/org.apache.camel.component.grpc.PingPong
      parameters:
        routeControlledStreamObserver: true
      steps:
        - toD:
            uri: grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong
            parameters:
              method: "${header.CamelGrpcMethodName}"
              streamRepliesTo: direct:next
              forwardOnError: true
              forwardOnCompleted: true
              inheritExchangePropertiesForReplies: true
- route:
    from:
      uri: direct:next
      steps:
        - to:
            uri: grpc://dummy:0/
            parameters:
              toRouteControlledStreamObserver: true
```

### Client streaming and bidirectional streaming

Both client streaming and bidirectional streaming gRPC methods expose `StreamObserver` as responses' handler. Therefore, you need the same technique as described in the server streaming section (all 5 steps).

But there is another thing: requests also come in streaming mode. So you need the following:

1.  Set consumer strategy to DELEGATION - that differs from the default PROPAGATION option in the fact that consumer will not produce responses at all. If you set PROPAGATION, then you will receive more responses than you expected;
    
2.  Forward `onError` and `onCompletion` on consumer;
    
3.  Set producer strategy to STREAMING.
    

Example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?routeControlledStreamObserver=true&consumerStrategy=DELEGATION&forwardOnError=true&forwardOnCompleted=true")
    .toD("grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=${header.CamelGrpcMethodName}&producerStrategy=STREAMING&streamRepliesTo=direct:next&forwardOnError=true&forwardOnCompleted=true&inheritExchangePropertiesForReplies=true");

from("direct:next")
    .to("grpc://dummy:0/?toRouteControlledStreamObserver=true");
```

```xml
<route>
  <from uri="grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?routeControlledStreamObserver=true&amp;consumerStrategy=DELEGATION&amp;forwardOnError=true&amp;forwardOnCompleted=true"/>
  <toD uri="grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=${header.CamelGrpcMethodName}&amp;producerStrategy=STREAMING&amp;streamRepliesTo=direct:next&amp;forwardOnError=true&amp;forwardOnCompleted=true&amp;inheritExchangePropertiesForReplies=true"/>
</route>
<route>
  <from uri="direct:next"/>
  <to uri="grpc://dummy:0/?toRouteControlledStreamObserver=true"/>
</route>
```

```yaml
- route:
    from:
      uri: grpc://localhost:1101/org.apache.camel.component.grpc.PingPong
      parameters:
        routeControlledStreamObserver: true
        consumerStrategy: DELEGATION
        forwardOnError: true
        forwardOnCompleted: true
      steps:
        - toD:
            uri: grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong
            parameters:
              method: "${header.CamelGrpcMethodName}"
              producerStrategy: STREAMING
              streamRepliesTo: direct:next
              forwardOnError: true
              forwardOnCompleted: true
              inheritExchangePropertiesForReplies: true
- route:
    from:
      uri: direct:next
      steps:
        - to:
            uri: grpc://dummy:0/
            parameters:
              toRouteControlledStreamObserver: true
```

## Examples

Below is a simple synchronous method invoke with host and port parameters

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:grpc-sync")
    .to("grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=sendPing&synchronous=true");
```

```xml
<route>
  <from uri="direct:grpc-sync"/>
  <to uri="grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=sendPing&amp;synchronous=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:grpc-sync
      steps:
        - to:
            uri: grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong
            parameters:
              method: sendPing
              synchronous: true
```

An asynchronous method invoke

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:grpc-async")
    .to("grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=pingAsyncResponse");
```

```xml
<route>
  <from uri="direct:grpc-async"/>
  <to uri="grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=pingAsyncResponse"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:grpc-async
      steps:
        - to:
            uri: grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong
            parameters:
              method: pingAsyncResponse
```

gRPC service consumer with propagation consumer strategy

-   Java
    
-   XML
    
-   YAML
    

```java
from("grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?consumerStrategy=PROPAGATION")
    .to("direct:grpc-service");
```

```xml
<route>
  <from uri="grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?consumerStrategy=PROPAGATION"/>
  <to uri="direct:grpc-service"/>
</route>
```

```yaml
- route:
    from:
      uri: grpc://localhost:1101/org.apache.camel.component.grpc.PingPong
      parameters:
        consumerStrategy: PROPAGATION
      steps:
        - to:
            uri: direct:grpc-service
```

gRPC service producer with streaming producer strategy (requires a service that uses "stream" mode as input and output)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:grpc-request-stream")
    .to("grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=PingAsyncAsync&producerStrategy=STREAMING&streamRepliesTo=direct:grpc-response-stream");

from("direct:grpc-response-stream")
    .log("Response received: ${body}");
```

```xml
<route>
  <from uri="direct:grpc-request-stream"/>
  <to uri="grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong?method=PingAsyncAsync&amp;producerStrategy=STREAMING&amp;streamRepliesTo=direct:grpc-response-stream"/>
</route>
<route>
  <from uri="direct:grpc-response-stream"/>
  <log message="Response received: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:grpc-request-stream
      steps:
        - to:
            uri: grpc://remotehost:1101/org.apache.camel.component.grpc.PingPong
            parameters:
              method: PingAsyncAsync
              producerStrategy: STREAMING
              streamRepliesTo: direct:grpc-response-stream
- route:
    from:
      uri: direct:grpc-response-stream
      steps:
        - log: "Response received: ${body}"
```

gRPC service consumer TLS/SSL security negotiation enabled

-   Java
    
-   XML
    
-   YAML
    

```java
from("grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?consumerStrategy=PROPAGATION&negotiationType=TLS&keyCertChainResource=file:src/test/resources/certs/server.pem&keyResource=file:src/test/resources/certs/server.key&trustCertCollectionResource=file:src/test/resources/certs/ca.pem")
    .to("direct:tls-enable");
```

```xml
<route>
  <from uri="grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?consumerStrategy=PROPAGATION&amp;negotiationType=TLS&amp;keyCertChainResource=file:src/test/resources/certs/server.pem&amp;keyResource=file:src/test/resources/certs/server.key&amp;trustCertCollectionResource=file:src/test/resources/certs/ca.pem"/>
  <to uri="direct:tls-enable"/>
</route>
```

```yaml
- route:
    from:
      uri: grpc://localhost:1101/org.apache.camel.component.grpc.PingPong
      parameters:
        consumerStrategy: PROPAGATION
        negotiationType: TLS
        keyCertChainResource: "file:src/test/resources/certs/server.pem"
        keyResource: "file:src/test/resources/certs/server.key"
        trustCertCollectionResource: "file:src/test/resources/certs/ca.pem"
      steps:
        - to:
            uri: direct:tls-enable
```

gRPC service producer with custom JSON Web Token (JWT) implementation authentication

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:grpc-jwt")
    .to("grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?method=pingSyncSync&synchronous=true&authenticationType=JWT&jwtSecret=supersecuredsecret");
```

```xml
<route>
  <from uri="direct:grpc-jwt"/>
  <to uri="grpc://localhost:1101/org.apache.camel.component.grpc.PingPong?method=pingSyncSync&amp;synchronous=true&amp;authenticationType=JWT&amp;jwtSecret=supersecuredsecret"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:grpc-jwt
      steps:
        - to:
            uri: grpc://localhost:1101/org.apache.camel.component.grpc.PingPong
            parameters:
              method: pingSyncSync
              synchronous: true
              authenticationType: JWT
              jwtSecret: supersecuredsecret
```

## Configuration

It is recommended to use the `protobuf-maven-plugin`, which calls the Protocol Buffer Compiler (protoc) to generate Java source files from .proto (protocol buffer definition) files. This plugin will generate procedure request and response classes, their builders and gRPC procedures stubs classes as well.

The following steps are required:

Insert operating system and CPU architecture detection extension inside **<build>** tag of the project `pom.xml` or set `${os.detected.classifier}` parameter manually

```xml
<extensions>
  <extension>
    <groupId>kr.motd.maven</groupId>
    <artifactId>os-maven-plugin</artifactId>
    <version>1.7.1</version>
  </extension>
</extensions>
```

Insert the gRPC and protobuf Java code generator plugins into the **<plugins>** tag of the project pom.xml

```xml
<plugin>
  <groupId>org.xolstice.maven.plugins</groupId>
  <artifactId>protobuf-maven-plugin</artifactId>
  <version>0.6.1</version>
  <configuration>
    <protocArtifact>com.google.protobuf:protoc:${protobuf-version}:exe:${os.detected.classifier}</protocArtifact>
    <pluginId>grpc-java</pluginId>
    <pluginArtifact>io.grpc:protoc-gen-grpc-java:${grpc-version}:exe:${os.detected.classifier}</pluginArtifact>
  </configuration>
  <executions>
    <execution>
      <goals>
        <goal>compile</goal>
        <goal>compile-custom</goal>
        <goal>test-compile</goal>
        <goal>test-compile-custom</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

## More information

See these resources:

-   [gRPC project site](https://www.grpc.io/)
    
-   [Maven Protocol Buffers Plugin](https://www.xolstice.org/protobuf-maven-plugin)