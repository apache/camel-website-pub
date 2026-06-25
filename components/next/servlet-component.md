# Servlet

**Since Camel 2.0**

**Only consumer is supported**

The Servlet component provides HTTP-based endpoints for consuming HTTP requests that arrive at an HTTP endpoint that is bound to a published Servlet.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-servlet</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

> **Note**
> **Stream**
>
> Servlet is stream-based, which means the input it receives is submitted to Camel as a stream. That means you will only be able to read the content of the stream **once**. If you find a situation where the message body appears to be empty, or you need to access the data multiple times (eg: doing multicasting, or redelivery error handling), you should use Stream caching or convert the message body to a `String` which is safe to be read multiple times.

## URI format

servlet://relative\_path\[?options\]

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

The Servlet component supports 12 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | true | boolean |
| **servletName** (consumer) | Default name of servlet to use. The default name is CamelServlet. | CamelServlet | String |
| **attachmentMultipartBinding** (consumer (advanced)) | Whether to automatic bind multipart/form-data as attachments on the Camel Exchange. The options attachmentMultipartBinding=true and disableStreamCache=false cannot work together. Remove disableStreamCache to use AttachmentMultipartBinding. This is turn off by default as this may require servlet specific configuration to enable this when using Servlet’s. | false | boolean |
| **fileNameExtWhitelist** (consumer (advanced)) | Whitelist of accepted filename extensions for accepting uploaded files. Multiple extensions can be separated by comma, such as txt,xml. |  | String |
| **httpRegistry** (consumer (advanced)) | To use a custom org.apache.camel.component.servlet.HttpRegistry. |  | HttpRegistry |
| **allowJavaSerializedObject** (advanced) | Whether to allow java serialization when a request uses context-type=application/x-java-serialized-object. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **httpBinding** (advanced) | To use a custom HttpBinding to control the mapping between Camel message and HttpClient. |  | HttpBinding |
| **httpConfiguration** (advanced) | To use the shared HttpConfiguration as base configuration. |  | HttpConfiguration |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **deserializationFilter** (security) | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied when deserializing Java objects from requests or responses with Content-Type application/x-java-serialized-object (only used when allowJavaSerializedObject or transferException is enabled). When not set, the JVM-wide jdk.serialFilter is used if present; otherwise a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. packages is applied. |  | String |

## Endpoint Options

The Servlet endpoint is configured using URI syntax:

servlet:contextPath

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **contextPath** (consumer) | **Required** The context-path to use. |  | String |

### Query Parameters (24 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **disableStreamCache** (common) | Determines whether or not the raw input stream is cached or not. The Camel consumer (camel-servlet, camel-jetty etc.) will by default cache the input stream to support reading it multiple times to ensure it Camel can retrieve all data from the stream. However you can set this option to true when you for example need to access the raw stream, such as streaming it directly to a file or other persistent store. DefaultHttpBinding will copy the request input stream into a stream cache and put it into message body if this option is false to support reading the stream multiple times. If you use Servlet to bridge/proxy an endpoint then consider enabling this option to improve performance, in case you do not need to read the message payload multiple times. The producer (camel-http) will by default cache the response body stream. If setting this option to true, then the producers will not cache the response body stream but use the response stream as-is (the stream can only be read once) as the message body. | false | boolean |
| **transferException** (common) | If enabled and an Exchange failed processing on the consumer side, and if the caused Exception was send back serialized in the response as a application/x-java-serialized-object content type. On the producer side the exception will be deserialized and thrown as is, instead of the HttpOperationFailedException. The caused exception is required to be serialized. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | boolean |
| **headerFilterStrategy** (common (advanced)) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **httpBinding** (common (advanced)) | To use a custom HttpBinding to control the mapping between Camel message and HttpClient. |  | HttpBinding |
| **async** (consumer) | Configure the consumer to work in async mode. | false | boolean |
| **chunked** (consumer) | If this option is false the Servlet will disable the HTTP streaming and set the content-length header on the response. | true | boolean |
| **httpMethodRestrict** (consumer) | Used to only allow consuming if the HttpMethod matches, such as GET/POST/PUT etc. Multiple methods can be specified separated by comma. |  | String |
| **logException** (consumer) | If enabled and an Exchange failed processing on the consumer side the exception’s stack trace will be logged when the exception stack trace is not sent in the response’s body. | false | boolean |
| **matchOnUriPrefix** (consumer) | Whether or not the consumer should try to find a target consumer by matching the URI prefix if no exact match is found. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | boolean |
| **responseBufferSize** (consumer) | To use a custom buffer size on the jakarta.servlet.ServletResponse. |  | Integer |
| **servletName** (consumer) | Name of the servlet to use. | CamelServlet | String |
| **attachmentMultipartBinding** (consumer (advanced)) | Whether to automatic bind multipart/form-data as attachments on the Camel Exchange. The options attachmentMultipartBinding=true and disableStreamCache=false cannot work together. Remove disableStreamCache to use AttachmentMultipartBinding. This is turn off by default as this may require servlet specific configuration to enable this when using Servlet’s. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **eagerCheckContentAvailable** (consumer (advanced)) | Whether to eager check whether the HTTP requests has content if the content-length header is 0 or not present. This can be turned on in case HTTP clients do not send streamed data. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **fileNameExtWhitelist** (consumer (advanced)) | Whitelist of accepted filename extensions for accepting uploaded files. Multiple extensions can be separated by comma, such as txt,xml. |  | String |
| **mapHttpMessageBody** (consumer (advanced)) | If this option is true then IN exchange Body of the exchange will be mapped to HTTP body. Setting this to false will avoid the HTTP mapping. | true | boolean |
| **mapHttpMessageFormUrlEncodedBody** (consumer (advanced)) | If this option is true then IN exchange Form Encoded body of the exchange will be mapped to HTTP. Setting this to false will avoid the HTTP Form Encoded body mapping. | true | boolean |
| **mapHttpMessageHeaders** (consumer (advanced)) | If this option is true then IN exchange Headers of the exchange will be mapped to HTTP headers. Setting this to false will avoid the HTTP Headers mapping. | true | boolean |
| **optionsEnabled** (consumer (advanced)) | Specifies whether to enable HTTP OPTIONS for this Servlet consumer. By default OPTIONS is turned off. | false | boolean |
| **traceEnabled** (consumer (advanced)) | Specifies whether to enable HTTP TRACE for this Servlet consumer. By default TRACE is turned off. | false | boolean |
| **oauthProfile** (security) | OAuth profile name for validating incoming Authorization: Bearer tokens. When set, the request is authenticated before the route is processed. This requires an OAuthTokenValidationFactory; camel-oauth provides the default implementation. This is Camel endpoint-level validation and does not replace servlet container or framework security. |  | String |

## OAuth Bearer token validation

Servlet consumers can validate incoming `Authorization: Bearer` tokens by setting the `oauthProfile` endpoint option. The profile is resolved through Camel’s `OAuthTokenValidationFactory` SPI. The [camel-oauth](../4.18.x/others/oauth.md) component provides the default implementation for standalone Camel applications; see its documentation for validation profile options and production hardening (expected issuer and audience, HTTPS for JWKS, OIDC discovery, and introspection endpoints). Runtimes can also provide their own implementation.

> **Note**
> If `oauthProfile` is set but no `OAuthTokenValidationFactory` is available, the route fails to start. Add `camel-oauth` for the default provider or include a runtime-specific provider from the platform integration.

-   Java
    
-   XML
    
-   YAML
    

```java
from("servlet:secure?oauthProfile=myprofile")
    .to("direct:businessLogic");
```

```xml
<route>
  <from uri="servlet:secure?oauthProfile=myprofile"/>
  <to uri="direct:businessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: servlet:secure
      parameters:
        oauthProfile: myprofile
      steps:
        - to:
            uri: direct:businessLogic
```

When `oauthProfile` is set, static profile configuration is resolved and validated at route startup. Updates to OAuth profile properties require restarting the route or Camel context before they take effect. Requests without a Bearer token or with an invalid token are rejected with HTTP 401 before the route is processed; missing credentials receive a `WWW-Authenticate: Bearer` response header and invalid tokens receive `WWW-Authenticate: Bearer error="invalid_token"`. Malformed `Authorization` headers are rejected with HTTP 400 and `WWW-Authenticate: Bearer error="invalid_request"`. Token validation infrastructure failures are rejected with HTTP 503. For valid tokens, the token validation result is stored on the exchange as the `CamelOAuthTokenValidationResult` exchange property. The raw `Authorization` header is removed from the Camel message before the route is invoked.

> **Note**
> Automatic `OPTIONS` handling runs before OAuth validation when `optionsEnabled=false`, so unauthenticated CORS preflight and Allow requests keep the existing servlet behavior. If an `OPTIONS` route is explicitly enabled, that route is protected by OAuth like other methods.

> **Note**
> This is Camel endpoint-level validation and does not replace servlet container security, filters, or runtime-specific authentication mechanisms. If route code accesses the native servlet request object directly, the container request still reflects the original inbound HTTP headers. If the servlet container or framework already authenticates requests, it may consume or transform the `Authorization` header before Camel sees it. In that case, prefer the container or framework security and do not set `oauthProfile` for the same path, to avoid double validation or missing-header failures; `oauthProfile` is intended for deployments where the container performs no authentication.

## Message Headers

Camel will apply the same Message Headers as the [HTTP](http-component.md) component.

Camel will also populate **all** `request.parameter` and `request.headers`. For example, if a client request has the URL, [http://myserver/myserver?orderid=123](http://myserver/myserver?orderid=123), the exchange will contain a header named `orderid` with the value `123`.

## Examples

You can consume only `from` endpoints generated by the Servlet component. Therefore, it should be used only as input into your Camel routes. To issue HTTP requests against other HTTP endpoints, use the [HTTP Component](http-component.md).

### Example `CamelHttpTransportServlet` configuration

#### Camel Spring Boot / Camel Quarkus

When running camel-servlet on the Spring Boot or Camel Quarkus runtimes, `CamelHttpTransportServlet` is configured for you automatically and is driven by configuration properties. Refer to the camel-servlet configuration documentation for these runtimes.

#### Servlet container / application server

If you’re running Camel standalone on a Servlet container or application server, you can use `web.xml` to configure `CamelHttpTransportServlet`.

For example, to define a route that exposes an HTTP service under the path `/services`.

_XML-only: web.xml servlet configuration_

```xml
<web-app>
  <servlet>
    <servlet-name>CamelServlet</servlet-name>
    <servlet-class>org.apache.camel.component.servlet.CamelHttpTransportServlet</servlet-class>
  </servlet>

  <servlet-mapping>
    <servlet-name>CamelServlet</servlet-name>
    <url-pattern>/services/*</url-pattern>
  </servlet-mapping>
</web-app>
```

### Example route

-   Java
    
-   XML
    
-   YAML
    

```java
from("servlet:hello")
    .setBody(simple("<b>Got Content-Type: ${header.Content-Type}, URI: ${header.CamelHttpUri}</b>"));
```

```xml
<route>
  <from uri="servlet:hello"/>
  <setBody>
    <simple>&lt;b&gt;Got Content-Type: ${header.Content-Type}, URI: ${header.CamelHttpUri}&lt;/b&gt;</simple>
  </setBody>
</route>
```

```yaml
- route:
    from:
      uri: servlet:hello
      steps:
        - setBody:
            simple: "<b>Got Content-Type: ${header.Content-Type}, URI: ${header.CamelHttpUri}</b>"
```

### Camel Servlet HTTP endpoint path

The full path where the camel-servlet HTTP endpoint is published depends on:

-   The Servlet application context path
    
-   The configured Servlet mapping URL patterns
    
-   The camel-servlet endpoint URI context path
    

For example, if the application context path is `/camel` and `CamelHttpTransportServlet` is configured with a URL mapping of `/services/*`. Then a Camel route like `from("servlet:hello")` would be published to a path like [http://localhost:8080/camel/services/hello](http://localhost:8080/camel/services/hello).

### Servlet asynchronous support

To enable Camel to benefit from Servlet asynchronous support, you must enable the `async` boolean init parameter by setting it to `true`.

By default, the servlet thread pool is used for exchange processing. However, to use a custom thread pool, you can configure an init parameter named `executorRef` with the String value set to the name of a bean bound to the Camel registry of type `Executor`. If no bean was found in the Camel registry, the Servlet component will attempt to fall back on an executor policy or default executor service.

If you want to force exchange processing to wait in another container background thread, you can set the `forceAwait` boolean init parameter to `true`.

On the Camel Quarkus runtime, these init parameters can be set via configuration properties. Refer to the Camel Quarkus Servlet extension documentation for more information.

On other runtimes you can configure these parameters in `web.xml` as follows.

_XML-only: web.xml with async servlet init parameters_

```xml
<web-app>
    <servlet>
        <servlet-name>CamelServlet</servlet-name>
        <servlet-class>org.apache.camel.component.servlet.CamelHttpTransportServlet</servlet-class>
        <init-param>
            <param-name>async</param-name>
            <param-value>true</param-value>
        </init-param>
        <init-param>
            <param-name>executorRef</param-name>
            <param-value>my-custom-thread-pool</param-value>
        </init-param>
    </servlet>

    <servlet-mapping>
        <servlet-name>CamelServlet</servlet-name>
        <url-pattern>/services/*</url-pattern>
    </servlet-mapping>
</web-app>
```

### Camel JARs on an application server boot classpath

If deploying into an application server / servlet container and you choose to have Camel JARs such as `camel-core`, `camel-servlet`, etc on the boot classpath. Then the servlet mapping list will be shared between multiple deployed Camel application in the app server.

> **Warning**
> Having Camel JARs on the boot classpath of the application server is not best practice.

In this scenario, you **must** define a custom and unique servlet name in each of your Camel applications. For example, in `web.xml`:

_XML-only: web.xml with custom servlet name_

```xml
<web-app>
    <servlet>
      <servlet-name>MyServlet</servlet-name>
      <servlet-class>org.apache.camel.component.servlet.CamelHttpTransportServlet</servlet-class>
      <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
      <servlet-name>MyServlet</servlet-name>
      <url-pattern>/*</url-pattern>
    </servlet-mapping>
</web-app>
```

In your Camel servlet endpoints, include the servlet name:

-   Java
    
-   XML
    
-   YAML
    

```java
from("servlet://foo?servletName=MyServlet")
```

```xml
<route>
  <from uri="servlet://foo?servletName=MyServlet"/>
  <!-- ... -->
</route>
```

```yaml
- route:
    from:
      uri: servlet://foo
      parameters:
        servletName: MyServlet
      steps:
        - to:
            uri: direct:businessLogic
```

Camel detects duplicate Servlet names and will fail to start the application. You can control and ignore such duplicates by setting the servlet init parameter `ignoreDuplicateServletName` to `true` as follows:

_XML-only: web.xml init parameter to ignore duplicate servlet names_

```xml
  <servlet>
    <servlet-name>CamelServlet</servlet-name>
    <display-name>Camel Http Transport Servlet</display-name>
    <servlet-class>org.apache.camel.component.servlet.CamelHttpTransportServlet</servlet-class>
    <init-param>
      <param-name>ignoreDuplicateServletName</param-name>
      <param-value>true</param-value>
    </init-param>
  </servlet>
```

But it is **strongly advised** to use unique `servlet-name` for each Camel application to avoid this duplication clash, as well any unforeseen side effects.