# Vert.x HTTP Client

**Since Camel 3.5**

**Only producer is supported**

The [Vert.x](https://vertx.io/) HTTP component provides the capability to produce messages to HTTP endpoints via the [Vert.x Web Client](https://vertx.io/docs/vertx-web-client/java/).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-vertx-http</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

vertx-http:hostname\[:port\]\[/resourceUri\]\[?options\]

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

The Vert.x HTTP Client component supports 20 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **responsePayloadAsByteArray** (producer) | Whether the response body should be byte or as io.vertx.core.buffer.Buffer. | true | boolean |
| **allowJavaSerializedObject** (advanced) | Whether to allow java serialization when a request has the Content-Type application/x-java-serialized-object This is disabled by default. If you enable this, be aware that Java will deserialize the incoming data from the request. This can be a potential security risk. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **tracingPolicy** (advanced) | 
The tracing policy used by the HTTP client when integrating with observability frameworks such as OpenTelemetry. If not specified the HTTP client applies a default tracing policy of PROPAGATE.

Enum values:

-   IGNORE
    
-   PROPAGATE
    
-   ALWAYS
    





 |  | TracingPolicy |
| **vertx** (advanced) | To use an existing vertx instead of creating a new instance. |  | Vertx |
| **vertxHttpBinding** (advanced) | A custom VertxHttpBinding which can control how to bind between Vert.x and Camel. |  | VertxHttpBinding |
| **vertxOptions** (advanced) | To provide a custom set of vertx options for configuring vertx. |  | VertxOptions |
| **webClientOptions** (advanced) | To provide a custom set of options for configuring vertx web client. |  | WebClientOptions |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **proxyHost** (proxy) | The proxy server host address. |  | String |
| **proxyPassword** (proxy) | The proxy server password if authentication is required. |  | String |
| **proxyPort** (proxy) | The proxy server port. |  | Integer |
| **proxyType** (proxy) | 

The proxy server type.

Enum values:

-   HTTP
    
-   SOCKS4
    
-   SOCKS5
    





 |  | ProxyType |
| **proxyUsername** (proxy) | The proxy server username if authentication is required. |  | String |
| **basicAuthPassword** (security) | The password to use for basic authentication. |  | String |
| **basicAuthUsername** (security) | The user name to use for basic authentication. |  | String |
| **bearerToken** (security) | The bearer token to use for bearer token authentication. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Vert.x HTTP Client endpoint is configured using URI syntax:

vertx-http:httpUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **httpUri** (producer) | **Required** The HTTP URI to connect to. |  | URI |

### Query Parameters (28 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeEndpoint** (producer) | If the option is true, the Exchange.HTTP\_URI header will be ignored and the endpoint URI will be used for the HTTP request. You may also set option throwExceptionOnFailure to false to return the fault response back to the client. | false | boolean |
| **connectTimeout** (producer) | The amount of time in milliseconds until a connection is established. A timeout value of zero is interpreted as an infinite timeout. | 60000 | int |
| **cookieStore** (producer) | A custom CookieStore to use when session management is enabled. If this option is not set then an in-memory CookieStore is used. | InMemoryCookieStore | CookieStore |
| **headerFilterStrategy** (producer) | A custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. | VertxHttpHeaderFilterStrategy | HeaderFilterStrategy |
| **httpMethod** (producer) | 
The HTTP method to use. The HttpMethod header cannot override this option if set.

Enum values:

-   OPTIONS
    
-   GET
    
-   HEAD
    
-   POST
    
-   PUT
    
-   DELETE
    
-   TRACE
    
-   CONNECT
    
-   PATCH
    
-   PROPFIND
    
-   PROPPATCH
    
-   MKCOL
    
-   COPY
    
-   MOVE
    
-   LOCK
    
-   UNLOCK
    
-   MKCALENDAR
    
-   VERSION\_CONTROL
    
-   REPORT
    
-   CHECKIN
    
-   CHECKOUT
    
-   UNCHECKOUT
    
-   MKWORKSPACE
    
-   UPDATE
    
-   LABEL
    
-   MERGE
    
-   BASELINE\_CONTROL
    
-   MKACTIVITY
    
-   ORDERPATCH
    
-   ACL
    
-   SEARCH
    





 |  | HttpMethod |
| **multipartUpload** (producer) | Whether to force using multipart/form-data for easy file uploads. This is only to be used for uploading the message body as a single entity form-data. For uploading multiple entries then use io.vertx.ext.web.multipart.MultipartForm to build the form. | false | boolean |
| **multipartUploadName** (producer) | The name of the multipart/form-data when multipartUpload is enabled. | data | String |
| **okStatusCodeRange** (producer) | The status codes which are considered a success response. The values are inclusive. Multiple ranges can be defined, separated by comma, e.g. 200-204,209,301-304. Each range must be a single number or from-to with the dash included. | 200-299 | String |
| **responsePayloadAsByteArray** (producer) | Whether the response body should be byte or as io.vertx.core.buffer.Buffer. | true | boolean |
| **sessionManagement** (producer) | Enables session management via WebClientSession. By default the client is configured to use an in-memory CookieStore. The cookieStore option can be used to override this. | false | boolean |
| **throwExceptionOnFailure** (producer) | Disable throwing HttpOperationFailedException in case of failed responses from the remote server. | true | boolean |
| **timeout** (producer) | The amount of time in milliseconds after which if the request does not return any data within the timeout period a TimeoutException fails the request. Setting zero or a negative value disables the timeout. | \-1 | long |
| **tracingPolicy** (producer) | 

The tracing policy used by the HTTP client when integrating with observability frameworks such as OpenTelemetry. If not specified the HTTP client applies a default tracing policy of PROPAGATE.

Enum values:

-   IGNORE
    
-   PROPAGATE
    
-   ALWAYS
    





 |  | TracingPolicy |
| **transferException** (producer) | If enabled and an Exchange failed processing on the consumer side, and if the caused Exception was sent back serialized in the response as a application/x-java-serialized-object content type. On the producer side the exception will be deserialized and thrown as is, instead of HttpOperationFailedException. The caused exception is required to be serialized. This is by default turned off. If you enable this then be aware that Camel will deserialize the incoming data from the request to a Java object, which can be a potential security risk. | false | boolean |
| **useCompression** (producer) | Set whether compression is enabled to handled compressed (E.g gzipped) responses. | false | boolean |
| **vertxHttpBinding** (producer) | A custom VertxHttpBinding which can control how to bind between Vert.x and Camel. |  | VertxHttpBinding |
| **webClientOptions** (producer) | Sets customized options for configuring the Vert.x WebClient. |  | WebClientOptions |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **proxyHost** (proxy) | The proxy server host address. |  | String |
| **proxyPassword** (proxy) | The proxy server password if authentication is required. |  | String |
| **proxyPort** (proxy) | The proxy server port. |  | Integer |
| **proxyType** (proxy) | 

The proxy server type.

Enum values:

-   HTTP
    
-   SOCKS4
    
-   SOCKS5
    





 |  | ProxyType |
| **proxyUsername** (proxy) | The proxy server username if authentication is required. |  | String |
| **basicAuthPassword** (security) | The password to use for basic authentication. |  | String |
| **basicAuthUsername** (security) | The user name to use for basic authentication. |  | String |
| **bearerToken** (security) | The bearer token to use for bearer token authentication. |  | String |
| **deserializationFilter** (security) | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied when deserializing Java objects from HTTP responses with Content-Type application/x-java-serialized-object. This is used when transferException is enabled (or when allowJavaSerializedObject is enabled on the component) and the remote side returns a serialized payload. When not set, the filter configured via the JVM system property jdk.serialFilter is used when present; otherwise a conservative default filter allowing java., javax. and org.apache.camel. packages is applied. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |

## Message Headers

The Vert.x HTTP Client component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHttpMethod** (producer) Constant: [`HTTP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-vertx-http/latest/org/apache/camel/component/vertx/http/VertxHttpConstants.html#HTTP_METHOD) | The http method. |  | HttpMethod |
| **CamelHttpResponseCode** (producer) Constant: [`HTTP_RESPONSE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-vertx-http/latest/org/apache/camel/component/vertx/http/VertxHttpConstants.html#HTTP_RESPONSE_CODE) | The HTTP response code from the external server. |  | Integer |
| **CamelHttpResponseText** (producer) Constant: [`HTTP_RESPONSE_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-vertx-http/latest/org/apache/camel/component/vertx/http/VertxHttpConstants.html#HTTP_RESPONSE_TEXT) | The HTTP response text from the external server. |  | String |
| **Content-Type** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-vertx-http/latest/org/apache/camel/component/vertx/http/VertxHttpConstants.html#CONTENT_TYPE) | The HTTP content type. Is set on both the IN and OUT message to provide a content type, such as text/html. |  | String |
| **CamelHttpQuery** (producer) Constant: [`HTTP_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-vertx-http/latest/org/apache/camel/component/vertx/http/VertxHttpConstants.html#HTTP_QUERY) | URI parameters. Will override existing URI parameters set directly on the endpoint. |  | String |
| **CamelHttpUri** (producer) Constant: [`HTTP_URI`](https://javadoc.io/doc/org.apache.camel/camel-vertx-http/latest/org/apache/camel/component/vertx/http/VertxHttpConstants.html#HTTP_URI) | URI to call. Will override the existing URI set directly on the endpoint. This URI is the URI of the http server to call. Its not the same as the Camel endpoint URI, where you can configure endpoint options such as security etc. This header does not support that, its only the URI of the http server. |  | String |
| **CamelHttpPath** (producer) Constant: [`HTTP_PATH`](https://javadoc.io/doc/org.apache.camel/camel-vertx-http/latest/org/apache/camel/component/vertx/http/VertxHttpConstants.html#HTTP_PATH) | Request URI’s path, the header will be used to build the request URI with the HTTP\_URI. |  | String |
| **Content-Encoding** (producer) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-vertx-http/latest/org/apache/camel/component/vertx/http/VertxHttpConstants.html#CONTENT_ENCODING) | The HTTP content encoding. Is set to provide a content encoding, such as gzip. |  | String |

## Usage

The following example shows how to send a request to an HTTP endpoint.

You can override the URI configured on the `vertx-http` producer via headers `Exchange.HTTP_URI` and `Exchange.HTTP_PATH`.

```java
from("direct:start")
    .to("vertx-http:https://camel.apache.org");
```

### URI Parameters

The `vertx-http` producer supports URI parameters to be sent to the HTTP server. The URI parameters can either be set directly on the endpoint URI, or as a header with the key `Exchange.HTTP_QUERY` on the message.

### Response code

Camel will handle, according to the HTTP response code:

-   Response code is in the range 100..299, Camel regards it as a success response.
    
-   Response code is in the range 300..399, Camel regards it as a redirection response and will throw a `HttpOperationFailedException` with the information.
    
-   Response code is 400+, Camel regards it as an external server failure and will throw a `HttpOperationFailedException` with the information.
    

### throwExceptionOnFailure

The option, `throwExceptionOnFailure`, can be set to `false` to prevent the `HttpOperationFailedException` from being thrown for failed response codes. This allows you to get any response from the remote server.

### Exceptions

`HttpOperationFailedException` exception contains the following information:

-   The HTTP status code
    
-   The HTTP status line (text of the status code)
    
-   Redirect location if server returned a redirect
    
-   Response body as a `java.lang.String`, if server provided a body as response
    

### HTTP method

The following algorithm determines the HTTP method to be used:  
1\. Use method provided as endpoint configuration (`httpMethod`).  
2\. Use method provided in header (`Exchange.HTTP_METHOD`).  
3\. `GET` if query string is provided in header.  
4\. `GET` if endpoint is configured with a query string.  
5\. `POST` if there is data to send (body is not `null`).  
6\. `GET` otherwise.

### HTTP form parameters

You can send HTTP form parameters in one of two ways.

1.  Set the `Exchange.CONTENT_TYPE` header to the value `application/x-www-form-urlencoded` and ensure the message body is a `String` formatted as form variables. For example `param1=value1&param2=value2`.
    
2.  Set the message body as a [MultiMap](https://vertx.io/docs/apidocs/io/vertx/core/MultiMap.md) which allows you to configure form parameter names and values.
    

### Multipart form data

You can upload text or binary files by setting the message body as a [MultipartForm](https://vertx.io/docs/apidocs/io/vertx/ext/web/multipart/MultipartForm.md).

### Customizing Vert.x Web Client options

When finer control of the Vert.x Web Client configuration is required, you can bind a custom [WebClientOptions](https://vertx.io/docs/apidocs/io/vertx/ext/web/client/WebClientOptions.md) instance to the registry.

```java
WebClientOptions options = new WebClientOptions().setMaxRedirects(5)
    .setIdleTimeout(10)
    .setConnectTimeout(3);

camelContext.getRegistry.bind("clientOptions", options);
```

Then reference the options on the `vertx-http` producer.

```java
from("direct:start")
    .to("vertx-http:http://localhost:8080?webClientOptions=#clientOptions")
```

### SSL

The Vert.x HTTP component supports SSL/TLS configuration through the [Camel JSSE Configuration Utility](../../manual/camel-configuration-utilities.md).

It is also possible to configure SSL options by providing a custom `WebClientOptions`.

### Session Management

Session management can be enabled via the `sessionManagement` URI option. When enabled, an in-memory cookie store is used to track cookies. This can be overridden by providing a custom `CookieStore` via the `cookieStore` URI option.

## Spring Boot Auto-Configuration

When using vertx-http with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-vertx-http-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 21 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.vertx-http.allow-java-serialized-object** | Whether to allow java serialization when a request has the Content-Type application/x-java-serialized-object This is disabled by default. If you enable this, be aware that Java will deserialize the incoming data from the request. This can be a potential security risk. | false | Boolean |
| **camel.component.vertx-http.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.vertx-http.basic-auth-password** | The password to use for basic authentication. |  | String |
| **camel.component.vertx-http.basic-auth-username** | The user name to use for basic authentication. |  | String |
| **camel.component.vertx-http.bearer-token** | The bearer token to use for bearer token authentication. |  | String |
| **camel.component.vertx-http.enabled** | Whether to enable auto configuration of the vertx-http component. This is enabled by default. |  | Boolean |
| **camel.component.vertx-http.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.vertx-http.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.vertx-http.proxy-host** | The proxy server host address. |  | String |
| **camel.component.vertx-http.proxy-password** | The proxy server password if authentication is required. |  | String |
| **camel.component.vertx-http.proxy-port** | The proxy server port. |  | Integer |
| **camel.component.vertx-http.proxy-type** | The proxy server type. |  | ProxyType |
| **camel.component.vertx-http.proxy-username** | The proxy server username if authentication is required. |  | String |
| **camel.component.vertx-http.response-payload-as-byte-array** | Whether the response body should be byte or as io.vertx.core.buffer.Buffer. | true | Boolean |
| **camel.component.vertx-http.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.vertx-http.tracing-policy** | The tracing policy used by the HTTP client when integrating with observability frameworks such as OpenTelemetry. If not specified the HTTP client applies a default tracing policy of PROPAGATE. |  | TracingPolicy |
| **camel.component.vertx-http.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.vertx-http.vertx** | To use an existing vertx instead of creating a new instance. The option is a io.vertx.core.Vertx type. |  | Vertx |
| **camel.component.vertx-http.vertx-http-binding** | A custom VertxHttpBinding which can control how to bind between Vert.x and Camel. The option is a org.apache.camel.component.vertx.http.VertxHttpBinding type. |  | VertxHttpBinding |
| **camel.component.vertx-http.vertx-options** | To provide a custom set of vertx options for configuring vertx. The option is a io.vertx.core.VertxOptions type. |  | VertxOptions |
| **camel.component.vertx-http.web-client-options** | To provide a custom set of options for configuring vertx web client. The option is a io.vertx.ext.web.client.WebClientOptions type. |  | WebClientOptions |