# Jetty

**Since Camel 1.2**

**Only consumer is supported**

The Jetty component provides HTTP-based endpoints for consuming and producing HTTP requests. That is, the Jetty component behaves as a simple Web server.

**Stream**

Jetty is stream-based, which means the input it receives is submitted to Camel as a stream. That means you will only be able to read the content of the stream **once**. If you find a situation where the message body appears to be empty, or you need to access the Exchange.HTTP\_RESPONSE\_CODE data multiple times (e.g.: doing multicasting, or redelivery error handling), you should use Stream caching or convert the message body to a `String` which is safe to be re-read multiple times.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jetty</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

jetty:http://hostname\[:port\]\[/resourceUri\]\[?options\]

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

The Jetty component supports 38 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **continuationTimeout** (consumer) | Allows to set a timeout in millis when using Jetty as consumer (server). By default Jetty uses 30000. You can use a value of = 0 to never expire. If a timeout occurs then the request will be expired and Jetty will return back a http error 503 to the client. This option is only in use when using Jetty with the Asynchronous Routing Engine. | 30000 | Long |
| **enableJmx** (consumer) | If this option is true, Jetty JMX support will be enabled for this endpoint. | false | boolean |
| **maxThreads** (consumer) | To set a value for maximum number of threads in server thread pool. Notice that both a min and max size must be configured. |  | Integer |
| **minThreads** (consumer) | To set a value for minimum number of threads in server thread pool. Notice that both a min and max size must be configured. |  | Integer |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | true | boolean |
| **requestBufferSize** (consumer) | Allows to configure a custom value of the request buffer size on the Jetty connectors. |  | Integer |
| **requestHeaderSize** (consumer) | Allows to configure a custom value of the request header size on the Jetty connectors. |  | Integer |
| **responseBufferSize** (consumer) | Allows to configure a custom value of the response buffer size on the Jetty connectors. |  | Integer |
| **responseHeaderSize** (consumer) | Allows to configure a custom value of the response header size on the Jetty connectors. |  | Integer |
| **sendServerVersion** (consumer) | If the option is true, jetty will send the server header with the jetty version information to the client which sends the request. NOTE please make sure there is no any other camel-jetty endpoint is share the same port, otherwise this option may not work as expected. | true | boolean |
| **useContinuation** (consumer) | Whether or not to use Jetty continuations for the Jetty Server. | true | boolean |
| **useXForwardedForHeader** (consumer) | To use the X-Forwarded-For header in HttpServletRequest.getRemoteAddr. | false | boolean |
| **fileSizeThreshold** (consumer (advanced)) | The size threshold after which files will be written to disk for multipart/form-data requests. By default the files are not written to disk. | 0 | int |
| **filesLocation** (consumer (advanced)) | The directory location where files will be store for multipart/form-data requests. By default the files are written in the system temporary folder. |  | String |
| **maxFileSize** (consumer (advanced)) | The maximum size allowed for uploaded files. -1 means no limit. | \-1 | long |
| **maxRequestSize** (consumer (advanced)) | The maximum size allowed for multipart/form-data requests. -1 means no limit. | \-1 | long |
| **threadPool** (consumer (advanced)) | To use a custom thread pool for the server. This option should only be used in special circumstances. |  | ThreadPool |
| **allowJavaSerializedObject** (advanced) | Whether to allow java serialization when a request uses context-type=application/x-java-serialized-object. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **errorHandler** (advanced) | This option is used to set the ErrorHandler that Jetty server uses. |  | ErrorHandler |
| **httpBinding** (advanced) | Not to be used - use JettyHttpBinding instead. |  | HttpBinding |
| **httpConfiguration** (advanced) | Jetty component does not use HttpConfiguration. |  | HttpConfiguration |
| **mbContainer** (advanced) | To use a existing configured org.eclipse.jetty.jmx.MBeanContainer if JMX is enabled that Jetty uses for registering mbeans. |  | MBeanContainer |
| **requestLog** (advanced) | To configure Jetty request logging. |  | RequestLog |
| **secureRequestCustomizer** (advanced) | To use a custom SecureRequestCustomizer. The option is a org.eclipse.jetty.server.SecureRequestCustomizer type. |  | SecureRequestCustomizer |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **proxyHost** (proxy) | To use a http proxy to configure the hostname. |  | String |
| **proxyPort** (proxy) | To use a http proxy to configure the port number. |  | Integer |
| **keystore** (security) | Specifies the location of the Java keystore file, which contains the Jetty server’s own X.509 certificate in a key entry. |  | String |
| **socketConnectorProperties** (security) | A map which contains general HTTP connector properties. Uses the same principle as sslSocketConnectorProperties. |  | Map |
| **socketConnectors** (security) | A map which contains per port number specific HTTP connectors. Uses the same principle as sslSocketConnectors. |  | Map |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **sslKeyPassword** (security) | The key password, which is used to access the certificate’s key entry in the keystore (this is the same password that is supplied to the keystore command’s -keypass option). |  | String |
| **sslPassword** (security) | The ssl password, which is required to access the keystore file (this is the same password that is supplied to the keystore command’s -storepass option). |  | String |
| **sslSocketConnectorProperties** (security) | A map which contains general SSL connector properties. |  | Map |
| **sslSocketConnectors** (security) | A map which contains per port number specific SSL connectors. |  | Map |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Jetty endpoint is configured using URI syntax:

jetty:httpUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **httpUri** (common) | **Required** The url of the HTTP endpoint to call. |  | URI |

### Query Parameters (39 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **headerFilterStrategy** (common (advanced)) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **httpBinding** (common (advanced)) | To use a custom HttpBinding to control the mapping between Camel message and HttpClient. |  | HttpBinding |
| **chunked** (consumer) | If this option is false the Servlet will disable the HTTP streaming and set the content-length header on the response. | true | boolean |
| **disableStreamCache** (common) | Determines whether or not the raw input stream is cached or not. The Camel consumer (camel-servlet, camel-jetty etc.) will by default cache the input stream to support reading it multiple times to ensure it Camel can retrieve all data from the stream. However you can set this option to true when you for example need to access the raw stream, such as streaming it directly to a file or other persistent store. DefaultHttpBinding will copy the request input stream into a stream cache and put it into message body if this option is false to support reading the stream multiple times. If you use Servlet to bridge/proxy an endpoint then consider enabling this option to improve performance, in case you do not need to read the message payload multiple times. The producer (camel-http) will by default cache the response body stream. If setting this option to true, then the producers will not cache the response body stream but use the response stream as-is (the stream can only be read once) as the message body. | false | boolean |
| **transferException** (common) | If enabled and an Exchange failed processing on the consumer side, and if the caused Exception was send back serialized in the response as a application/x-java-serialized-object content type. On the producer side the exception will be deserialized and thrown as is, instead of the HttpOperationFailedException. The caused exception is required to be serialized. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | boolean |
| **async** (consumer) | Configure the consumer to work in async mode. | false | boolean |
| **continuationTimeout** (consumer) | Allows to set a timeout in millis when using Jetty as consumer (server). By default Jetty uses 30000. You can use a value of = 0 to never expire. If a timeout occurs then the request will be expired and Jetty will return back a http error 503 to the client. This option is only in use when using Jetty with the Asynchronous Routing Engine. | 30000 | Long |
| **enableCORS** (consumer) | If the option is true, Jetty server will setup the CrossOriginFilter which supports the CORS out of box. | false | boolean |
| **enableJmx** (consumer) | If this option is true, Jetty JMX support will be enabled for this endpoint. See Jetty JMX support for more details. | false | boolean |
| **enableMultipartFilter** (consumer) | Whether org.apache.camel.component.jetty.MultiPartFilter is enabled or not. You should set this value to false when bridging endpoints, to ensure multipart requests is proxied/bridged as well. | false | boolean |
| **httpMethodRestrict** (consumer) | Used to only allow consuming if the HttpMethod matches, such as GET/POST/PUT etc. Multiple methods can be specified separated by comma. |  | String |
| **logException** (consumer) | If enabled and an Exchange failed processing on the consumer side the exception’s stack trace will be logged when the exception stack trace is not sent in the response’s body. | false | boolean |
| **matchOnUriPrefix** (consumer) | Whether or not the consumer should try to find a target consumer by matching the URI prefix if no exact match is found. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | boolean |
| **responseBufferSize** (consumer) | To use a custom buffer size on the jakarta.servlet.ServletResponse. |  | Integer |
| **sendDateHeader** (consumer) | If the option is true, jetty server will send the date header to the client which sends the request. NOTE please make sure there is no any other camel-jetty endpoint is share the same port, otherwise this option may not work as expected. | false | boolean |
| **sendServerVersion** (consumer) | If the option is true, jetty will send the server header with the jetty version information to the client which sends the request. NOTE please make sure there is no any other camel-jetty endpoint is share the same port, otherwise this option may not work as expected. | true | boolean |
| **sessionSupport** (consumer) | Specifies whether to enable the session manager on the server side of Jetty. | false | boolean |
| **useContinuation** (consumer) | Whether or not to use Jetty continuations for the Jetty Server. | false | Boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **eagerCheckContentAvailable** (consumer (advanced)) | Whether to eager check whether the HTTP requests has content if the content-length header is 0 or not present. This can be turned on in case HTTP clients do not send streamed data. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **fileSizeThreshold** (consumer (advanced)) | The size threshold after which files will be written to disk for multipart/form-data requests. By default the files are not written to disk. |  | Integer |
| **filesLocation** (consumer (advanced)) | The directory location where files will be store for multipart/form-data requests. By default the files are written in the system temporary folder. |  | String |
| **filterInitParameters** (consumer (advanced)) | Configuration of the filter init parameters. These parameters will be applied to the filter list before starting the jetty server. This is a multi-value option with prefix: filter. |  | Map |
| **filters** (consumer (advanced)) | Allows using a custom filters which is putted into a list and can be find in the Registry. Multiple values can be separated by comma. |  | List |
| **handlers** (consumer (advanced)) | Specifies a comma-delimited set of Handler instances to lookup in your Registry. These handlers are added to the Jetty servlet context (for example, to add security). Important: You can not use different handlers with different Jetty endpoints using the same port number. The handlers is associated to the port number. If you need different handlers, then use different port numbers. |  | List |
| **idleTimeout** (consumer (advanced)) | The max idle time (in milli seconds) is applied to an HTTP request for IO operations and delayed dispatch. Idle time 0 implies an infinite timeout, -1 (default) implies no HTTP channel timeout and the connection timeout is used instead. | \-1 | long |
| **mapHttpMessageBody** (consumer (advanced)) | If this option is true then IN exchange Body of the exchange will be mapped to HTTP body. Setting this to false will avoid the HTTP mapping. | true | boolean |
| **mapHttpMessageFormUrlEncodedBody** (consumer (advanced)) | If this option is true then IN exchange Form Encoded body of the exchange will be mapped to HTTP. Setting this to false will avoid the HTTP Form Encoded body mapping. | true | boolean |
| **mapHttpMessageHeaders** (consumer (advanced)) | If this option is true then IN exchange Headers of the exchange will be mapped to HTTP headers. Setting this to false will avoid the HTTP Headers mapping. | true | boolean |
| **maxFileSize** (consumer (advanced)) | The maximum size allowed for uploaded files. -1 means no limit. |  | Long |
| **maxRequestSize** (consumer (advanced)) | The maximum size allowed for multipart/form-data requests. -1 means no limit. |  | Long |
| **multipartFilter** (consumer (advanced)) | Allows using a custom multipart filter. Note: setting multipartFilter forces the value of enableMultipartFilter to true. |  | Filter |
| **optionsEnabled** (consumer (advanced)) | Specifies whether to enable HTTP OPTIONS for this Servlet consumer. By default OPTIONS is turned off. | false | boolean |
| **traceEnabled** (consumer (advanced)) | Specifies whether to enable HTTP TRACE for this Servlet consumer. By default TRACE is turned off. | false | boolean |
| **oauthProfile** (security) | OAuth profile name for validating incoming Authorization: Bearer tokens. When set, the request is authenticated before the route is processed. This requires an OAuthTokenValidationFactory; camel-oauth provides the default implementation. This is Camel endpoint-level validation and does not replace Jetty handlers or container security. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |

## Message Headers

The Jetty component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelServletContextPath** (consumer) Constant: [`SERVLET_CONTEXT_PATH`](https://javadoc.io/doc/org.apache.camel/camel-jetty/latest/org/apache/camel/component/jetty/JettyHttpConstants.html#SERVLET_CONTEXT_PATH) | The servlet context path used. |  | String |
| **CamelHttpPath** (consumer) Constant: [`HTTP_PATH`](https://javadoc.io/doc/org.apache.camel/camel-jetty/latest/org/apache/camel/component/jetty/JettyHttpConstants.html#HTTP_PATH) | Request URI’s path, the header will be used to build the request URI with the HTTP\_URI. |  | String |

## OAuth Bearer token validation

Jetty consumers can validate incoming `Authorization: Bearer` tokens by setting the `oauthProfile` endpoint option. The profile is resolved through Camel’s `OAuthTokenValidationFactory` SPI. The [camel-oauth](../4.18.x/others/oauth.md) component provides the default implementation for standalone Camel applications; see its documentation for validation profile options and production hardening (expected issuer and audience, HTTPS for JWKS, OIDC discovery, and introspection endpoints). Runtimes can also provide their own implementation.

> **Note**
> If `oauthProfile` is set but no `OAuthTokenValidationFactory` is available, the route fails to start. Add `camel-oauth` for the default provider or include a runtime-specific provider from the platform integration.

-   Java
    
-   XML
    
-   YAML
    

```java
from("jetty:http://0.0.0.0:8080/secure?oauthProfile=myprofile")
    .to("direct:businessLogic");
```

```xml
<route>
  <from uri="jetty:http://0.0.0.0:8080/secure?oauthProfile=myprofile"/>
  <to uri="direct:businessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: jetty:http://0.0.0.0:8080/secure
      parameters:
        oauthProfile: myprofile
      steps:
        - to:
            uri: direct:businessLogic
```

When `oauthProfile` is set, static profile configuration is resolved and validated at route startup. Updates to OAuth profile properties require restarting the route or Camel context before they take effect. Requests without a Bearer token or with an invalid token are rejected with HTTP 401 before the route is processed; missing credentials receive a `WWW-Authenticate: Bearer` response header and invalid tokens receive `WWW-Authenticate: Bearer error="invalid_token"`. Malformed `Authorization` headers are rejected with HTTP 400 and `WWW-Authenticate: Bearer error="invalid_request"`. Token validation infrastructure failures are rejected with HTTP 503. For valid tokens, the token validation result is stored on the exchange as the `CamelOAuthTokenValidationResult` exchange property. The raw `Authorization` header is removed from the Camel message before the route is invoked.

> **Note**
> Automatic `OPTIONS` handling runs before OAuth validation when `optionsEnabled=false`, so unauthenticated CORS preflight and Allow requests keep the existing Jetty behavior. If an `OPTIONS` route is explicitly enabled, that route is protected by OAuth like other methods.

> **Note**
> This is Camel endpoint-level validation and does not replace Jetty handlers or other container security mechanisms. If route code accesses the native servlet request object directly, the container request still reflects the original inbound HTTP headers. When combining OAuth validation with custom Jetty handlers or container-managed security, see the Jetty handlers and security configuration section below.

## Message Headers

Camel uses the same message headers as the [HTTP](http-component.md) component. It also uses a header (`Exchange.HTTP_CHUNKED`, `CamelHttpChunked`) to turn on or turn off the chunked encoding on the camel-jetty consumer.

Camel also populates **all** `request.parameter` and `request.headers`. For example, given a client request with the URL, `http://myserver/myserver?orderid=123`, the exchange will contain a header named `orderid` with the value `123`.

You can get the `request.parameter` from the message header not only from Get Method, but also other HTTP methods.

## Usage

The Jetty component supports consumer endpoints.

### Consumer

In this sample we define a route that exposes an HTTP service at `http://localhost:8080/myapp/myservice`:

> **Note**
> **Usage of localhost**
>
> When you specify `localhost` in a URL, Camel exposes the endpoint only on the local TCP/IP network interface, so it cannot be accessed from outside the machine it operates on.
>
> If you need to expose a Jetty endpoint on a specific network interface, the numerical IP address of this interface should be used as the host. If you need to expose a Jetty endpoint on all network interfaces, the `0.0.0.0` address should be used.
>
> To listen across an entire URI prefix, see below.

### How do I let Jetty match wildcards?

By default, Jetty will only match on exact uri’s. But you can instruct Jetty to match prefixes. For example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jetty://0.0.0.0:8123/foo").to("mock:foo");
```

```xml
<route>
  <from uri="jetty:http://0.0.0.0:8123/foo"/>
  <to uri="mock:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: jetty:http://0.0.0.0:8123/foo
      steps:
        - to:
            uri: mock:foo
```

In the route above Jetty will only match if the uri is an exact match, so it will match if you enter `http://0.0.0.0:8123/foo` but not match if you do `http://0.0.0.0:8123/foo/bar`.

So if you want to enable wildcard matching you need to set `matchOnUriPrefix=true` as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jetty://0.0.0.0:8123/foo?matchOnUriPrefix=true").to("mock:foo");
```

```xml
<route>
  <from uri="jetty:http://0.0.0.0:8123/foo?matchOnUriPrefix=true"/>
  <to uri="mock:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: jetty:http://0.0.0.0:8123/foo
      parameters:
        matchOnUriPrefix: true
      steps:
        - to:
            uri: mock:foo
```

So now Jetty matches any endpoints with starts with `foo`.

To match **any** endpoint you can remove the prefix so it will match anything from the root:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jetty://0.0.0.0:8123?matchOnUriPrefix=true").to("mock:foo");
```

```xml
<route>
  <from uri="jetty:http://0.0.0.0:8123?matchOnUriPrefix=true"/>
  <to uri="mock:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: jetty:http://0.0.0.0:8123
      parameters:
        matchOnUriPrefix: true
      steps:
        - to:
            uri: mock:foo
```

### Servlets

If you actually want to expose routes by HTTP and already have a Servlet, you should instead refer to the [Servlet Transport](servlet-component.md).

### HTTP Request Parameters

So if a client sends the HTTP request, `http://serverUri?one=hello`, the Jetty component will copy the HTTP request parameter, `one` to the exchange’s `in.header`. We can then use the `simple` language to route exchanges that contain this header to a specific endpoint and all others to another. If we used a language more powerful than [Simple](languages/simple-language.md) (such as [OGNL](languages/ognl-language.md)), we could also test for the parameter value and do routing based on the header value as well.

### Session Support

The session support option, `sessionSupport`, can be used to enable a `HttpSession` object and access the session object while processing the exchange. For example, the following route enables sessions:

```xml
<route>
    <from uri="jetty:http://0.0.0.0/myapp/myservice/?sessionSupport=true"/>
    <process ref="myCode"/>
</route>
```

The `myCode` Processor can be instantiated by a Spring `bean` element:

```xml
<bean id="myCode" class="com.mycompany.MyCodeProcessor"/>
```

Where the processor implementation can access the `HttpSession` as follows:

_Java-only: inline Processor accessing HttpSession_

```java
public void process(Exchange exchange) throws Exception {
    HttpSession session = exchange.getIn(HttpMessage.class).getRequest().getSession();
    ...
}
```

### SSL Support (HTTPS)

Using the JSSE Configuration Utility

The Jetty component supports SSL/TLS configuration through the [Camel JSSE Configuration Utility](../../manual/camel-configuration-utilities.md). This utility greatly decreases the amount of component-specific code you need to write and is configurable at the endpoint and component levels. The following examples demonstrate how to use the utility with the Jetty component.

Programmatic configuration of the component

_Java-only: programmatic SSL configuration with KeyStore and SSLContext parameters_

```java
KeyStoreParameters ksp = new KeyStoreParameters();
ksp.setResource("/users/home/server/keystore.jks");
ksp.setPassword("keystorePassword");

KeyManagersParameters kmp = new KeyManagersParameters();
kmp.setKeyStore(ksp);
kmp.setKeyPassword("keyPassword");

SSLContextParameters scp = new SSLContextParameters();
scp.setKeyManagers(kmp);

JettyComponent jettyComponent = getContext().getComponent("jetty", JettyComponent.class);
jettyComponent.setSslContextParameters(scp);
```

Spring DSL based configuration of endpoint

```xml
  <camel:sslContextParameters
      id="sslContextParameters">
    <camel:keyManagers
        keyPassword="keyPassword">
      <camel:keyStore
          resource="/users/home/server/keystore.jks"
          password="keystorePassword"/>
    </camel:keyManagers>
  </camel:sslContextParameters>

  <to uri="jetty:https://127.0.0.1/mail/?sslContextParameters=#sslContextParameters"/>
```

Configuring Jetty Directly

Jetty provides SSL support out of the box. To enable Jetty to run in SSL mode, format the URI with the `\https://` prefix---for example:

```xml
<from uri="jetty:https://0.0.0.0/myapp/myservice/"/>
```

Jetty also needs to know where to load your keystore from and what passwords to use to load the correct SSL certificate. Set the following JVM System Properties:

-   `org.eclipse.jetty.ssl.keystore` specify the location of the Java keystore file, which contains the Jetty server’s own X.509 certificate in a _key entry_. A key entry stores the X.509 certificate (effectively, the _public key_) and also its associated private key.
    
-   `org.eclipse.jetty.ssl.password` the store password, which is required to access the keystore file (this is the same password that is supplied to the `keystore` command’s `-storepass` option).
    
-   `org.eclipse.jetty.ssl.keypassword` the key password, which is used to access the certificate’s key entry in the keystore (this is the same password that is supplied to the `keystore` command’s `-keypass` option).
    

For details of how to configure SSL on a Jetty endpoint, read the following documentation at the Jetty Site: [http://docs.codehaus.org/display/JETTY/How+to+configure+SSL](http://docs.codehaus.org/display/JETTY/How+to+configure+SSL)

Camel doesn’t expose some SSL properties directly. However, Camel does expose the underlying SslSocketConnector, which will allow you to set properties like needClientAuth for mutual authentication requiring a client certificate or wantClientAuth for mutual authentication where a client doesn’t need a certificate but can have one.

```xml
<bean id="jetty" class="org.apache.camel.component.jetty.JettyHttpComponent">
    <property name="sslSocketConnectors">
        <map>
            <entry key="8043">
                <bean class="org.eclipse.jetty.server.ssl.SslSelectChannelConnector">
                    <property name="password" value="..."/>
                    <property name="keyPassword" value="..."/>
                    <property name="keystore" value="..."/>
                    <property name="needClientAuth" value="..."/>
                    <property name="truststore" value="..."/>
                </bean>
            </entry>
        </map>
    </property>
</bean>
```

The value you use as keys in the above map is the port you configure Jetty to listen to.

#### Configuring general SSL properties

Instead of a per-port number specific SSL socket connector (as shown above), you can now configure general properties that apply for all SSL socket connectors (that are not explicitly configured as above with the port number as entry).

```xml
<bean id="jetty" class="org.apache.camel.component.jetty.JettyHttpComponent">
    <property name="sslSocketConnectorProperties">
        <map>
            <entry key="password" value="..."/>
            <entry key="keyPassword" value="..."/>
            <entry key="keystore" value="..."/>
            <entry key="needClientAuth" value="..."/>
            <entry key="truststore" value="..."/>
        </map>
    </property>
</bean>
```

#### How to obtain reference to the X509Certificate

Jetty stores a reference to the certificate in the HttpServletRequest which you can access from code as follows:

_Java-only: accessing X509Certificate from HttpServletRequest_

```java
HttpServletRequest req = exchange.getIn().getBody(HttpServletRequest.class);
X509Certificate cert = (X509Certificate) req.getAttribute("javax.servlet.request.X509Certificate")
```

#### Configuring general HTTP properties

Instead of a per-port number specific HTTP socket connector (as shown above), you can now configure general properties that apply for all HTTP socket connectors (that are not explicitly configured as above with the port number as entry).

```xml
<bean id="jetty" class="org.apache.camel.component.jetty.JettyHttpComponent">
    <property name="socketConnectorProperties">
        <map>
            <entry key="acceptors" value="4"/>
            <entry key="maxIdleTime" value="300000"/>
        </map>
    </property>
</bean>
```

#### Obtaining X-Forwarded-For header with HttpServletRequest.getRemoteAddr()

If the HTTP requests are handled by an Apache server and forwarded to jetty with mod\_proxy, the original client IP address is in the X-Forwarded-For header and the HttpServletRequest.getRemoteAddr() will return the address of the Apache proxy.

Jetty has a forwarded property which takes the value from X-Forwarded-For and places it in the HttpServletRequest remoteAddr property. This property is not available directly through the endpoint configuration, but it can be easily added using the socketConnectors property:

```xml
<bean id="jetty" class="org.apache.camel.component.jetty.JettyHttpComponent">
    <property name="socketConnectors">
        <map>
            <entry key="8080">
                <bean class="org.eclipse.jetty.server.nio.SelectChannelConnector">
                    <property name="forwarded" value="true"/>
                </bean>
            </entry>
        </map>
    </property>
</bean>
```

This is particularly useful when an existing Apache server handles TLS connections for a domain and proxies them to application servers internally.

### Default behavior for returning HTTP status codes

The default behavior of HTTP status codes is defined by the `org.apache.camel.component.http.DefaultHttpBinding` class, which handles how a response is written and also sets the HTTP status code.

If the exchange was processed successfully, the 200 HTTP status code is returned.  
If the exchange failed with an exception, the 500 HTTP status code is returned, and the stacktrace is returned in the body. If you want to specify which HTTP status code to return, set the code in the `Exchange.HTTP_RESPONSE_CODE` header of the OUT message.

### Customizing HttpBinding

By default, Camel uses the `org.apache.camel.component.http.DefaultHttpBinding` to handle how a response is written. If you like, you can customize this behavior either by implementing your own `HttpBinding` class or by extending `DefaultHttpBinding` and overriding the appropriate methods.

The following example shows how to customize the `DefaultHttpBinding` in order to change how exceptions are returned:

We can then create an instance of our binding and register it in the Spring registry as follows:

```xml
<bean id="mybinding" class="com.mycompany.MyHttpBinding"/>
```

And then we can reference this binding when we define the route:

```xml
<route>
  <from uri="jetty:http://0.0.0.0:8080/myapp/myservice?httpBinding=#mybinding"/>
  <to uri="bean:doSomething"/>
</route>
```

### Jetty handlers and security configuration

You can configure a list of Jetty handlers on the endpoint, which can be useful for enabling advanced Jetty security features. These handlers are configured in Spring XML as follows:

```xml
<bean id="userRealm" class="org.mortbay.jetty.plus.jaas.JAASUserRealm">
    <property name="name" value="tracker-users"/>
    <property name="loginModuleName" value="ldaploginmodule"/>
</bean>

<bean id="constraint" class="org.mortbay.jetty.security.Constraint">
    <property name="name" value="BASIC"/>
    <property name="roles" value="tracker-users"/>
    <property name="authenticate" value="true"/>
</bean>

<bean id="constraintMapping" class="org.mortbay.jetty.security.ConstraintMapping">
    <property name="constraint" ref="constraint"/>
    <property name="pathSpec" value="/*"/>
</bean>

<bean id="securityHandler" class="org.mortbay.jetty.security.SecurityHandler">
    <property name="userRealm" ref="userRealm"/>
    <property name="constraintMappings" ref="constraintMapping"/>
</bean>
```

You can configure a list of Jetty handlers as follows:

```xml
<bean id="constraint" class="org.eclipse.jetty.http.security.Constraint">
    <property name="name" value="BASIC"/>
    <property name="roles" value="tracker-users"/>
    <property name="authenticate" value="true"/>
</bean>

<bean id="constraintMapping" class="org.eclipse.jetty.security.ConstraintMapping">
    <property name="constraint" ref="constraint"/>
    <property name="pathSpec" value="/*"/>
</bean>

<bean id="securityHandler" class="org.eclipse.jetty.security.ConstraintSecurityHandler">
    <property name="authenticator">
        <bean class="org.eclipse.jetty.security.authentication.BasicAuthenticator"/>
    </property>
    <property name="constraintMappings">
        <list>
            <ref bean="constraintMapping"/>
        </list>
    </property>
</bean>
```

You can then define the endpoint as:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jetty:http://0.0.0.0:9080/myservice?handlers=securityHandler");
```

```xml
<route>
    <from uri="jetty:http://0.0.0.0:9080/myservice?handlers=securityHandler"/>
    <!-- ... -->
</route>
```

```yaml
- route:
    from:
      uri: jetty:http://0.0.0.0:9080/myservice
      parameters:
        handlers: securityHandler
    steps:
      # ...
```

If you need more handlers, set the `handlers` option equal to a comma-separated list of bean IDs.

### How to return a custom HTTP 500 reply message

You may want to return a custom reply message when something goes wrong, instead of the default reply message Camel [Jetty](#) replies to with. You could use a custom `HttpBinding` to be in control of the message mapping, but often it may be easier to use Camel’s Exception Clause to construct the custom reply message. For example, as show here, where we return `Dude something went wrong` with HTTP error code 500:

### Multipart Form support

The camel-jetty component supports multipart form post out of the box. The submitted form-data are mapped into the message header. Camel Jetty creates an attachment for each uploaded file. The file name is mapped to the name of the attachment. The content type is set as the content type of the attachment file name. You can find the example here.

### Jetty JMX support

The camel-jetty component supports the enabling of Jetty’s JMX capabilities at the component and endpoint level with the endpoint configuration taking priority. Note that JMX must be enabled within the Camel context to enable JMX support in this component as the component provides Jetty with a reference to the MBeanServer registered with the Camel context. Because the camel-jetty component caches and reuses Jetty resources for a given protocol/host/port pairing, this configuration option will only be evaluated during the creation of the first endpoint to use a protocol/host/port pairing. For example, given two routes created from the following XML fragments, JMX support would remain enabled for all endpoints listening on `[https://0.0.0.0](https://0.0.0.0)`.

```xml
<from uri="jetty:https://0.0.0.0/myapp/myservice1/?enableJmx=true"/>
```

```xml
<from uri="jetty:https://0.0.0.0/myapp/myservice2/?enableJmx=false"/>
```

The camel-jetty component also provides for direct configuration of the Jetty MBeanContainer. Jetty creates MBean names dynamically. If you are running another instance of Jetty outside of the Camel context and sharing the same MBeanServer between the instances, you can provide both instances with a reference to the same MBeanContainer to avoid name collisions when registering Jetty MBeans.

## Spring Boot Auto-Configuration

When using jetty with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jetty-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 39 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jetty.allow-java-serialized-object** | Whether to allow java serialization when a request uses context-type=application/x-java-serialized-object. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | Boolean |
| **camel.component.jetty.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jetty.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.jetty.continuation-timeout** | Allows to set a timeout in millis when using Jetty as consumer (server). By default Jetty uses 30000. You can use a value of = 0 to never expire. If a timeout occurs then the request will be expired and Jetty will return back a http error 503 to the client. This option is only in use when using Jetty with the Asynchronous Routing Engine. | 30000 | Long |
| **camel.component.jetty.enable-jmx** | If this option is true, Jetty JMX support will be enabled for this endpoint. | false | Boolean |
| **camel.component.jetty.enabled** | Whether to enable auto configuration of the jetty component. This is enabled by default. |  | Boolean |
| **camel.component.jetty.error-handler** | This option is used to set the ErrorHandler that Jetty server uses. The option is a org.eclipse.jetty.server.handler.ErrorHandler type. |  | ErrorHandler |
| **camel.component.jetty.file-size-threshold** | The size threshold after which files will be written to disk for multipart/form-data requests. By default the files are not written to disk. | 0 | Integer |
| **camel.component.jetty.files-location** | The directory location where files will be store for multipart/form-data requests. By default the files are written in the system temporary folder. |  | String |
| **camel.component.jetty.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.jetty.http-binding** | Not to be used - use JettyHttpBinding instead. The option is a org.apache.camel.http.common.HttpBinding type. |  | HttpBinding |
| **camel.component.jetty.http-configuration** | Jetty component does not use HttpConfiguration. The option is a org.apache.camel.http.common.HttpConfiguration type. |  | HttpConfiguration |
| **camel.component.jetty.keystore** | Specifies the location of the Java keystore file, which contains the Jetty server’s own X.509 certificate in a key entry. |  | String |
| **camel.component.jetty.max-file-size** | The maximum size allowed for uploaded files. -1 means no limit. | \-1 | Long |
| **camel.component.jetty.max-request-size** | The maximum size allowed for multipart/form-data requests. -1 means no limit. | \-1 | Long |
| **camel.component.jetty.max-threads** | To set a value for maximum number of threads in server thread pool. Notice that both a min and max size must be configured. |  | Integer |
| **camel.component.jetty.mb-container** | To use a existing configured org.eclipse.jetty.jmx.MBeanContainer if JMX is enabled that Jetty uses for registering mbeans. The option is a org.eclipse.jetty.jmx.MBeanContainer type. |  | MBeanContainer |
| **camel.component.jetty.min-threads** | To set a value for minimum number of threads in server thread pool. Notice that both a min and max size must be configured. |  | Integer |
| **camel.component.jetty.mute-exception** | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | true | Boolean |
| **camel.component.jetty.proxy-host** | To use a http proxy to configure the hostname. |  | String |
| **camel.component.jetty.proxy-port** | To use a http proxy to configure the port number. |  | Integer |
| **camel.component.jetty.request-buffer-size** | Allows to configure a custom value of the request buffer size on the Jetty connectors. |  | Integer |
| **camel.component.jetty.request-header-size** | Allows to configure a custom value of the request header size on the Jetty connectors. |  | Integer |
| **camel.component.jetty.request-log** | To configure Jetty request logging. The option is a org.eclipse.jetty.server.RequestLog type. |  | RequestLog |
| **camel.component.jetty.response-buffer-size** | Allows to configure a custom value of the response buffer size on the Jetty connectors. |  | Integer |
| **camel.component.jetty.response-header-size** | Allows to configure a custom value of the response header size on the Jetty connectors. |  | Integer |
| **camel.component.jetty.secure-request-customizer** | To use a custom SecureRequestCustomizer. The option is a org.eclipse.jetty.server.SecureRequestCustomizer type. The option is a org.eclipse.jetty.server.SecureRequestCustomizer type. |  | SecureRequestCustomizer |
| **camel.component.jetty.send-server-version** | If the option is true, jetty will send the server header with the jetty version information to the client which sends the request. NOTE please make sure there is no any other camel-jetty endpoint is share the same port, otherwise this option may not work as expected. | true | Boolean |
| **camel.component.jetty.socket-connector-properties** | A map which contains general HTTP connector properties. Uses the same principle as sslSocketConnectorProperties. |  | Map |
| **camel.component.jetty.socket-connectors** | A map which contains per port number specific HTTP connectors. Uses the same principle as sslSocketConnectors. |  | Map |
| **camel.component.jetty.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.jetty.ssl-key-password** | The key password, which is used to access the certificate’s key entry in the keystore (this is the same password that is supplied to the keystore command’s -keypass option). |  | String |
| **camel.component.jetty.ssl-password** | The ssl password, which is required to access the keystore file (this is the same password that is supplied to the keystore command’s -storepass option). |  | String |
| **camel.component.jetty.ssl-socket-connector-properties** | A map which contains general SSL connector properties. |  | Map |
| **camel.component.jetty.ssl-socket-connectors** | A map which contains per port number specific SSL connectors. |  | Map |
| **camel.component.jetty.thread-pool** | To use a custom thread pool for the server. This option should only be used in special circumstances. The option is a org.eclipse.jetty.util.thread.ThreadPool type. |  | ThreadPool |
| **camel.component.jetty.use-continuation** | Whether or not to use Jetty continuations for the Jetty Server. | true | Boolean |
| **camel.component.jetty.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.jetty.use-x-forwarded-for-header** | To use the X-Forwarded-For header in HttpServletRequest.getRemoteAddr. | false | Boolean |