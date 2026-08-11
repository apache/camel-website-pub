# Undertow

**Since Camel 2.16**

**Both producer and consumer are supported**

The Undertow component provides HTTP and WebSocket based endpoints for consuming and producing HTTP/WebSocket requests.

That is, the Undertow component behaves as a simple Web server. Undertow can also be used as an HTTP client that means you can also use it with Camel as a producer.

Since the component also supports WebSocket connections, it can serve as a drop-in replacement for the Camel websocket component or atmosphere-websocket component.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-undertow</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

HTTP

undertow:http://hostname\[:port\]\[/resourceUri\]\[?options\]
undertow:https://hostname\[:port\]\[/resourceUri\]\[?options\]

WebSocket

undertow:ws://hostname\[:port\]\[/resourceUri\]\[?options\]
undertow:wss://hostname\[:port\]\[/resourceUri\]\[?options\]

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

The Undertow component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **hostOptions** (advanced) | To configure common options, such as thread pools. |  | UndertowHostOptions |
| **undertowHttpBinding** (advanced) | To use a custom HttpBinding to control the mapping between Camel message and HttpClient. |  | UndertowHttpBinding |
| **allowedRoles** (security) | Configuration used by UndertowSecurityProvider. Comma separated list of allowed roles. |  | String |
| **securityConfiguration** (security) | Configuration used by UndertowSecurityProvider. Security configuration object for use from UndertowSecurityProvider. Configuration is UndertowSecurityProvider specific. Each provider decides, whether it accepts configuration. |  | Object |
| **securityProvider** (security) | Security provider allows plug in the provider, which will be used to secure requests. SPI approach could be used too (component then finds security provider using SPI). |  | UndertowSecurityProvider |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Undertow endpoint is configured using URI syntax:

undertow:httpURI

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **httpURI** (common) | **Required** The url of the HTTP endpoint to use. |  | URI |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **useStreaming** (common) | For HTTP endpoint: if true, text and binary messages will be wrapped as java.io.InputStream before they are passed to an Exchange; otherwise they will be passed as byte. For WebSocket endpoint: if true, text and binary messages will be wrapped as java.io.Reader and java.io.InputStream respectively before they are passed to an Exchange; otherwise they will be passed as String and byte respectively. | false | boolean |
| **accessLog** (consumer) | Whether or not the consumer should write access log. | false | Boolean |
| **httpMethodRestrict** (consumer) | Used to only allow consuming if the HttpMethod matches, such as GET/POST/PUT etc. Multiple methods can be specified separated by comma. |  | String |
| **matchOnUriPrefix** (consumer) | Whether or not the consumer should try to find a target consumer by matching the URI prefix if no exact match is found. | false | Boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | true | Boolean |
| **optionsEnabled** (consumer) | Specifies whether to enable HTTP OPTIONS for this Servlet consumer. By default OPTIONS is turned off. | false | boolean |
| **transferException** (consumer) | If enabled and an Exchange failed processing on the consumer side and if the caused Exception was send back serialized in the response as a application/x-java-serialized-object content type. On the producer side the exception will be deserialized and thrown as is instead of the HttpOperationFailedException. The caused exception is required to be serialized. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | Boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **handlers** (consumer (advanced)) | Specifies a comma-delimited set of io.undertow.server.HttpHandler instances to lookup in your Registry. These handlers are added to the Undertow handler chain (for example, to add security). Important: You can not use different handlers with different Undertow endpoints using the same port number. The handlers is associated to the port number. If you need different handlers, then use different port numbers. |  | String |
| **cookieHandler** (producer) | Configure a cookie handler to maintain a HTTP session. |  | CookieHandler |
| **keepAlive** (producer) | Setting to ensure socket is not closed due to inactivity. | true | Boolean |
| **options** (producer) | Sets additional channel options. The options that can be used are defined in org.xnio.Options. To configure from endpoint uri, then prefix each option with option., such as option.close-abort=true&option.send-buffer=8192. This is a multi-value option with prefix: option. |  | Map |
| **preserveHostHeader** (producer) | If the option is true, UndertowProducer will set the Host header to the value contained in the current exchange Host header, useful in reverse proxy applications where you want the Host header received by the downstream server to reflect the URL called by the upstream client, this allows applications which use the Host header to generate accurate URL’s for a proxied service. | true | boolean |
| **reuseAddresses** (producer) | Setting to facilitate socket multiplexing. | true | Boolean |
| **tcpNoDelay** (producer) | Setting to improve TCP protocol performance. | true | Boolean |
| **throwExceptionOnFailure** (producer) | Option to disable throwing the HttpOperationFailedException in case of failed responses from the remote server. This allows you to get all responses regardless of the HTTP status code. | true | Boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessLogReceiver** (advanced) | Which Undertow AccessLogReceiver should be used Will use JBossLoggingAccessLogReceiver if not specified. |  | AccessLogReceiver |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **undertowHttpBinding** (advanced) | To use a custom UndertowHttpBinding to control the mapping between Camel message and undertow. |  | UndertowHttpBinding |
| **allowedRoles** (security) | Configuration used by UndertowSecurityProvider. Comma separated list of allowed roles. |  | String |
| **oauthProfile** (security) | OAuth profile name for validating incoming Authorization: Bearer tokens. When set, the HTTP request or WebSocket upgrade request is authenticated before the route is processed. This requires an OAuthTokenValidationFactory; camel-oauth provides the default implementation. |  | String |
| **securityConfiguration** (security) | OConfiguration used by UndertowSecurityProvider. Security configuration object for use from UndertowSecurityProvider. Configuration is UndertowSecurityProvider specific. Each provider decides whether accepts configuration. |  | Object |
| **securityProvider** (security) | Security provider allows plug in the provider, which will be used to secure requests. SPI approach could be used too (endpoint then finds security provider using SPI). |  | UndertowSecurityProvider |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **fireWebSocketChannelEvents** (websocket) | if true, the consumer will post notifications to the route when a new WebSocket peer connects, disconnects, etc. See UndertowConstants.EVENT\_TYPE and EventType. | false | boolean |
| **sendTimeout** (websocket) | Timeout in milliseconds when sending to a websocket channel. The default timeout is 30000 (30 seconds). | 30000 | Integer |
| **sendToAll** (websocket) | To send to all websocket subscribers. Can be used to configure on endpoint level, instead of having to use the UndertowConstants.SEND\_TO\_ALL header on the message. | false | Boolean |

## Message Headers

The Undertow component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **websocket.connectionKey** (common) Constant: [`CONNECTION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#CONNECTION_KEY) | An identifier of WebSocketChannel through which the message was received or should be sent. |  | String |
| **websocket.connectionKey.list** (producer) Constant: [`CONNECTION_KEY_LIST`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#CONNECTION_KEY_LIST) | The list of websocket connection keys. |  | List |
| **websocket.sendToAll** (common) Constant: [`SEND_TO_ALL`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#SEND_TO_ALL) | To send to all websocket subscribers. Can be used to configure on endpoint level, instead of having to use the UndertowConstants.SEND\_TO\_ALL header on the message. |  | Boolean |
| **websocket.eventType** (consumer) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#EVENT_TYPE) | The numeric identifier of the type of websocket event. |  | Integer |
| **websocket.eventTypeEnum** (consumer) Constant: [`EVENT_TYPE_ENUM`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#EVENT_TYPE_ENUM) | 
The type of websocket event.

Enum values:

-   ONOPEN
    
-   ONCLOSE
    
-   ONERROR
    





 |  | EventType |
| **websocket.channel** (consumer) Constant: [`CHANNEL`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#CHANNEL) | The WebSocketChannel through which the message was received. |  | WebSocketChannel |
| **websocket.exchange** (consumer) Constant: [`EXCHANGE`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#EXCHANGE) | The exchange for the websocket transport, only available for ON\_OPEN events. |  | WebSocketHttpExchange |
| **CamelHttpResponseCode** (common) Constant: [`HTTP_RESPONSE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#HTTP_RESPONSE_CODE) | The http response code. |  | Integer |
| **Content-Type** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#CONTENT_TYPE) | The content type. |  | String |
| **CamelHttpCharacterEncoding** (consumer) Constant: [`HTTP_CHARACTER_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#HTTP_CHARACTER_ENCODING) | The http character encoding. |  | String |
| **CamelHttpPath** (common) Constant: [`HTTP_PATH`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#HTTP_PATH) | The http path. |  | String |
| **CamelHttpQuery** (common) Constant: [`HTTP_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#HTTP_QUERY) | The http query. |  | String |
| **CamelHttpUri** (common) Constant: [`HTTP_URI`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#HTTP_URI) | The http URI. |  | String |
| **CamelHttpMethod** (producer) Constant: [`HTTP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#HTTP_METHOD) | The http method. |  | String |
| **Host** (producer) Constant: [`HOST_STRING`](https://javadoc.io/doc/org.apache.camel/camel-undertow/latest/org/apache/camel/component/undertow/UndertowConstants.html#HOST_STRING) | The host http header. |  | String |

## OAuth Bearer token validation

Undertow HTTP and WebSocket consumers can validate incoming `Authorization: Bearer` tokens by setting the `oauthProfile` endpoint option. The profile is resolved through Camel’s `OAuthTokenValidationFactory` SPI. The [camel-oauth](others/oauth.md) component provides the default implementation for standalone Camel applications; see its documentation for validation profile options and production hardening (expected issuer and audience, HTTPS for JWKS, OIDC discovery, and introspection endpoints). Runtimes can also provide their own implementation.

> **Note**
> If `oauthProfile` is set but no `OAuthTokenValidationFactory` is available, the route fails to start. Add `camel-oauth` for the default provider or include a runtime-specific provider from the platform integration.

-   Java
    
-   XML
    
-   YAML
    

```java
from("undertow:http://0.0.0.0:8080/secure?oauthProfile=myprofile")
    .to("direct:businessLogic");
```

```xml
<route>
  <from uri="undertow:http://0.0.0.0:8080/secure?oauthProfile=myprofile"/>
  <to uri="direct:businessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: undertow:http://0.0.0.0:8080/secure
      parameters:
        oauthProfile: myprofile
      steps:
        - to:
            uri: direct:businessLogic
```

When `oauthProfile` is set, static profile configuration is resolved and validated at route startup. Updates to OAuth profile properties require restarting the route or Camel context before they take effect. HTTP requests and WebSocket upgrade requests without a Bearer token or with an invalid token are rejected with HTTP 401 before the route is processed; missing credentials receive a `WWW-Authenticate: Bearer` response header and invalid tokens receive `WWW-Authenticate: Bearer error="invalid_token"`. Malformed `Authorization` headers are rejected with HTTP 400 and `WWW-Authenticate: Bearer error="invalid_request"`. Token validation infrastructure failures are rejected with HTTP 503. For valid tokens, the token validation result is stored on the exchange as the `CamelOAuthTokenValidationResult` exchange property. The raw `Authorization` header is removed before the route is invoked.

> **Note**
> For WebSocket consumers, the token is validated during the HTTP upgrade handshake. The validation result is available on the `ONOPEN` event exchange when `fireWebSocketChannelEvents=true`, and on subsequent message exchanges for that connection; individual WebSocket messages are not revalidated.

> **Note**
> For HTTP consumers, automatic `OPTIONS` handling still runs before OAuth validation when `optionsEnabled=false`, so unauthenticated preflight and Allow requests keep the existing Undertow behavior. If an `OPTIONS` route is explicitly enabled, that route is protected by OAuth like other methods.
>
> Custom Undertow `handlers` and `UndertowSecurityProvider#wrapHttpHandler` wrap outside the OAuth handler and can observe the original request headers before OAuth validation. The `UndertowSecurityProvider#authenticate` callback runs after OAuth validation and sees the request after Camel has removed the `Authorization` header. See the Security provider section below for how `UndertowSecurityProvider` is configured.

## Host Options

The `hostOptions` component option allows configuring the underlying Undertow server. These options apply to all endpoints sharing the same host and port.

  
| Option | Type | Description |
| --- | --- | --- |
| `workerThreads` | `Integer` | The number of worker threads to use in the Undertow host. |
| `ioThreads` | `Integer` | The number of I/O threads to use in the Undertow host. |
| `bufferSize` | `Integer` | The buffer size of the Undertow host. |
| `directBuffers` | `Boolean` | Whether the Undertow host should use direct buffers. |
| `http2Enabled` | `Boolean` | Whether the Undertow host should use the HTTP/2 protocol. |
| `maxEntitySize` | `Long` | The maximum size of the HTTP entity body, in bytes. Requests with a body larger than this will be rejected. |
| `multipartMaxEntitySize` | `Long` | The maximum size of a multipart HTTP entity body, in bytes. Multipart requests larger than this will be rejected. |
| `maxHeaderSize` | `Integer` | The maximum size of an HTTP request header, in bytes. Requests with headers larger than this will be rejected. |
| `noRequestTimeout` | `Integer` | The amount of time in milliseconds a connection can be idle with no current requests before it is closed. |
| `idleTimeout` | `Integer` | The idle timeout in milliseconds after which the channel will be closed. |
| `requestParseTimeout` | `Integer` | The maximum time in milliseconds to parse an HTTP request. |
| `maxParameters` | `Integer` | The maximum number of query and path parameters that will be parsed. |
| `maxHeaders` | `Integer` | The maximum number of HTTP headers that will be parsed. |

Configuration example:

```properties
camel.component.undertow.host-options.max-entity-size = 10485760
camel.component.undertow.host-options.max-header-size = 65536
camel.component.undertow.host-options.no-request-timeout = 30000
```

## Usage

### Message Headers

Camel uses the same message headers as the [HTTP](http-component.md) component. It also uses `Exchange.HTTP_CHUNKED,CamelHttpChunked` header to turn on or turn off the chunked encoding on the camel-undertow consumer.

Camel also populates **all** `request.parameter` and `request.headers`. For example, given a client request with the URL, `http://myserver/myserver?orderid=123`, the exchange will contain a header named `orderid` with the value `123`.

### Using localhost as host

When you specify `localhost` in a URL, Camel exposes the endpoint only on the local TCP/IP network interface, so it cannot be accessed from outside the machine it operates on.

If you need to expose an Undertow endpoint on a specific network interface, the numerical IP address of this interface should be used as the host. If you need to expose an Undertow endpoint on all network interfaces, the `0.0.0.0` address should be used.

If you actually want to expose routes by HTTP and already have a Servlet, you should instead refer to the [Servlet Transport](servlet-component.md).

To listen across an entire URI prefix see next section.

### How do I let Undertow match wildcards?

By default, Undertow will only match on exact uri’s. But you can instruct Undertow to match prefixes. For example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("undertow:http://0.0.0.0:8123/foo").to("mock:foo");
```

```xml
<route>
  <from uri="undertow:http://0.0.0.0:8123/foo"/>
  <to uri="mock:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: undertow:http://0.0.0.0:8123/foo
      steps:
        - to:
            uri: mock:foo
```

In the route above Undertow will only match if the uri is an exact match, so it will match if you enter `http://0.0.0.0:8123/foo` but not match if you do `http://0.0.0.0:8123/foo/bar`.

So if you want to enable wildcard matching you need to set `matchOnUriPrefix=true` as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("undertow:http://0.0.0.0:8123/foo?matchOnUriPrefix=true").to("mock:foo");
```

```xml
<route>
  <from uri="undertow:http://0.0.0.0:8123/foo?matchOnUriPrefix=true"/>
  <to uri="mock:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: undertow:http://0.0.0.0:8123/foo
      parameters:
        matchOnUriPrefix: true
      steps:
        - to:
            uri: mock:foo
```

So now Undertow matches any endpoints with starts with `foo`.

To match **any** endpoint you can remove the prefix so it will match anything from the root:

-   Java
    
-   XML
    
-   YAML
    

```java
from("undertow:http://0.0.0.0:8123?matchOnUriPrefix=true").to("mock:foo");
```

```xml
<route>
  <from uri="undertow:http://0.0.0.0:8123?matchOnUriPrefix=true"/>
  <to uri="mock:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: undertow:http://0.0.0.0:8123
      parameters:
        matchOnUriPrefix: true
      steps:
        - to:
            uri: mock:foo
```

### Security provider

To plug in a security provider for endpoint authentication, implement SPI interface `org.apache.camel.component.undertow.spi.UndertowSecurityProvider`.

Undertow component locates all implementations of `UndertowSecurityProvider` using Java SPI (Service Provider Interfaces). If there is an object passed to the component as parameter `securityConfiguration` and provider accepts it. Provider will be used for authentication of all requests.

Property `requireServletContext` of security providers forces the Undertow server to start with servlet context. There will be no servlet actually handled. This feature is meant only for use with servlet filters, which needs servlet context for their functionality.

## Examples

### HTTP Producer Example

The following is a basic example of how to send an HTTP request to an existing HTTP endpoint.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("undertow:http://www.google.com");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="undertow:http://www.google.com"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: undertow:http://www.google.com
```

### HTTP Consumer Example

In this sample we define a route that exposes a HTTP service at `http://localhost:8080/myapp/myservice`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("undertow:http://localhost:8080/myapp/myservice")
    .to("bean:myBean");
```

```xml
<route>
  <from uri="undertow:http://localhost:8080/myapp/myservice"/>
  <to uri="bean:myBean"/>
</route>
```

```yaml
- route:
    from:
      uri: undertow:http://localhost:8080/myapp/myservice
      steps:
        - to:
            uri: bean:myBean
```

### WebSocket Example

In this sample we define a route that exposes a WebSocket service at `http://localhost:8080/myapp/mysocket` and returns back a response to the same channel:

-   Java
    
-   XML
    
-   YAML
    

```java
from("undertow:ws://localhost:8080/myapp/mysocket")
    .transform(simple("Echo ${body}"))
    .to("undertow:ws://localhost:8080/myapp/mysocket");
```

```xml
<route>
  <from uri="undertow:ws://localhost:8080/myapp/mysocket"/>
  <transform><simple>Echo ${body}</simple></transform>
  <to uri="undertow:ws://localhost:8080/myapp/mysocket"/>
</route>
```

```yaml
- route:
    from:
      uri: undertow:ws://localhost:8080/myapp/mysocket
      steps:
        - transform:
            simple: "Echo ${body}"
        - to:
            uri: undertow:ws://localhost:8080/myapp/mysocket
```