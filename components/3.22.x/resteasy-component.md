# Resteasy

> **Warning**
> **Deprecated:** This resteasy is deprecated and may be removed in a future release.

**Since Camel 3.4**

**Both producer and consumer are supported**

The **resteasy:** component provides HTTP based endpoints for consuming HTTP requests that arrive at a HTTP endpoint that is bound to a published Servlet.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-resteasy</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

resteasy://relative\_path\[?options\]

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

The Resteasy component supports 19 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | boolean |
| **proxyConsumersClasses** (consumer) | Proxy classes for consumer endpoints. Multiple classes can be separated by comma. |  | String |
| **followRedirects** (producer) | Whether to the HTTP request should follow redirects. By default the HTTP request does not follow redirects. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **copyHeaders** (producer (advanced)) | If this option is true then IN exchange headers will be copied to OUT exchange headers according to copy strategy. Setting this to false, allows to only include the headers from the HTTP response (not propagating IN headers). | true | boolean |
| **responsePayloadStreamingThreshold** (producer (advanced)) | This threshold in bytes controls whether the response payload should be stored in memory as a byte array or be streaming based. Set this to -1 to always use streaming mode. | 8192 | int |
| **skipRequestHeaders** (producer (advanced)) | Whether to skip mapping all the Camel headers as HTTP request headers. If there are no data from Camel headers needed to be included in the HTTP request then this can avoid parsing overhead with many object allocations for the JVM garbage collector. | false | boolean |
| **skipResponseHeaders** (producer (advanced)) | Whether to skip mapping all the HTTP response headers to Camel headers. If there are no data needed from HTTP headers then this can avoid parsing overhead with many object allocations for the JVM garbage collector. | false | boolean |
| **allowJavaSerializedObject** (advanced) | Whether to allow java serialization when a request uses context-type=application/x-java-serialized-object. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | boolean |
| **authCachingDisabled** (advanced) | Disables authentication scheme caching. | false | boolean |
| **automaticRetriesDisabled** (advanced) | Disables automatic request recovery and re-execution. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **connectionStateDisabled** (advanced) | Disables connection state tracking. | false | boolean |
| **contentCompressionDisabled** (advanced) | Disables automatic content decompression. | false | boolean |
| **cookieManagementDisabled** (advanced) | Disables state (cookie) management. | false | boolean |
| **defaultUserAgentDisabled** (advanced) | Disables the default user agent set by this builder if none has been provided by the user. | false | boolean |
| **redirectHandlingDisabled** (advanced) | Disables automatic redirect handling. | false | boolean |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Endpoint Options

The Resteasy endpoint is configured using URI syntax:

resteasy:httpUri

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **httpUri** (common) | **Required** The url of the HTTP endpoint to call. |  | URI |

### Query Parameters (41 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **disableStreamCache** (common) | Determines whether or not the raw input stream from Servlet is cached or not (Camel will read the stream into a in memory/overflow to file, Stream caching) cache. By default Camel will cache the Servlet input stream to support reading it multiple times to ensure it Camel can retrieve all data from the stream. However you can set this option to true when you for example need to access the raw stream, such as streaming it directly to a file or other persistent store. DefaultHttpBinding will copy the request input stream into a stream cache and put it into message body if this option is false to support reading the stream multiple times. If you use Servlet to bridge/proxy an endpoint then consider enabling this option to improve performance, in case you do not need to read the message payload multiple times. The http producer will by default cache the response body stream. If setting this option to true, then the producers will not cache the response body stream but use the response stream as-is as the message body. | false | boolean |
| **resteasyMethod** (common) | Sets the resteasy method to process the request. | GET | String |
| **servletName** (common) | Sets the servlet name. |  | String |
| **async** (consumer) | Configure the consumer to work in async mode. | false | boolean |
| **httpMethodRestrict** (consumer) | Used to only allow consuming if the HttpMethod matches, such as GET/POST/PUT etc. Multiple methods can be specified separated by comma. |  | String |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | boolean |
| **responseBufferSize** (consumer) | To use a custom buffer size on the javax.servlet.ServletResponse. |  | Integer |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **eagerCheckContentAvailable** (consumer (advanced)) | Whether to eager check whether the HTTP requests has content if the content-length header is 0 or not present. This can be turned on in case HTTP clients do not send streamed data. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **mapHttpMessageBody** (consumer (advanced)) | If this option is true then IN exchange Body of the exchange will be mapped to HTTP body. Setting this to false will avoid the HTTP mapping. | true | boolean |
| **mapHttpMessageFormUrlEncodedBody** (consumer (advanced)) | If this option is true then IN exchange Form Encoded body of the exchange will be mapped to HTTP. Setting this to false will avoid the HTTP Form Encoded body mapping. | true | boolean |
| **mapHttpMessageHeaders** (consumer (advanced)) | If this option is true then IN exchange Headers of the exchange will be mapped to HTTP headers. Setting this to false will avoid the HTTP Headers mapping. | true | boolean |
| **optionsEnabled** (consumer (advanced)) | Specifies whether to enable HTTP OPTIONS for this Servlet consumer. By default OPTIONS is turned off. | false | boolean |
| **traceEnabled** (consumer (advanced)) | Specifies whether to enable HTTP TRACE for this Servlet consumer. By default TRACE is turned off. | false | boolean |
| **bridgeEndpoint** (producer) | If the option is true, HttpProducer will ignore the Exchange.HTTP\_URI header, and use the endpoint’s URI for request. You may also set the option throwExceptionOnFailure to be false to let the HttpProducer send all the fault response back. | false | boolean |
| **connectionClose** (producer) | Specifies whether a Connection Close header must be added to HTTP Request. By default connectionClose is false. | false | boolean |
| **followRedirects** (producer) | Whether to the HTTP request should follow redirects. By default the HTTP request does not follow redirects. | false | boolean |
| **httpMethod** (producer) | 

Configure the HTTP method to use. The HttpMethod header cannot override this option if set.

Enum values:

-   GET
    
-   POST
    
-   PUT
    
-   DELETE
    
-   HEAD
    
-   OPTIONS
    
-   TRACE
    
-   PATCH
    





 |  | HttpMethods |
| **throwExceptionOnFailure** (producer) | Option to disable throwing the HttpOperationFailedException in case of failed responses from the remote server. This allows you to get all responses regardless of the HTTP status code. | true | boolean |
| **clearExpiredCookies** (producer (advanced)) | Whether to clear expired cookies before sending the HTTP request. This ensures the cookies store does not keep growing by adding new cookies which is newer removed when they are expired. If the component has disabled cookie management then this option is disabled too. | true | boolean |
| **cookieHandler** (producer (advanced)) | Configure a cookie handler to maintain a HTTP session. |  | CookieHandler |
| **copyHeaders** (producer (advanced)) | If this option is true then IN exchange headers will be copied to OUT exchange headers according to copy strategy. Setting this to false, allows to only include the headers from the HTTP response (not propagating IN headers). | true | boolean |
| **customHostHeader** (producer (advanced)) | To use custom host header for producer. When not set in query will be ignored. When set will override host header derived from url. |  | String |
| **deleteWithBody** (producer (advanced)) | Whether the HTTP DELETE should include the message body or not. By default HTTP DELETE do not include any HTTP body. However in some rare cases users may need to be able to include the message body. | false | boolean |
| **getWithBody** (producer (advanced)) | Whether the HTTP GET should include the message body or not. By default HTTP GET do not include any HTTP body. However in some rare cases users may need to be able to include the message body. | false | boolean |
| **ignoreResponseBody** (producer (advanced)) | If this option is true, The http producer won’t read response body and cache the input stream. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **okStatusCodeRange** (producer (advanced)) | The status codes which are considered a success response. The values are inclusive. Multiple ranges can be defined, separated by comma, e.g. 200-204,209,301-304. Each range must be a single number or from-to with the dash included. | 200-299 | String |
| **preserveHostHeader** (producer (advanced)) | If the option is true, HttpProducer will set the Host header to the value contained in the current exchange Host header, useful in reverse proxy applications where you want the Host header received by the downstream server to reflect the URL called by the upstream client, this allows applications which use the Host header to generate accurate URL’s for a proxied service. | false | boolean |
| **skipRequestHeaders** (producer (advanced)) | Whether to skip mapping all the Camel headers as HTTP request headers. If there are no data from Camel headers needed to be included in the HTTP request then this can avoid parsing overhead with many object allocations for the JVM garbage collector. | false | boolean |
| **skipResponseHeaders** (producer (advanced)) | Whether to skip mapping all the HTTP response headers to Camel headers. If there are no data needed from HTTP headers then this can avoid parsing overhead with many object allocations for the JVM garbage collector. | false | boolean |
| **userAgent** (producer (advanced)) | To set a custom HTTP User-Agent request header. |  | String |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **setHttpResponseDuringProcessing** (advanced) | Sets the flag to use the endpoint where you can either populate camel exchange from servlet response or use request itself which may be thought as if it is a proxy. |  | Boolean |
| **skipServletProcessing** (advanced) | Sets the flag to use skip servlet processing and let camel take over processing. |  | Boolean |
| **useSystemProperties** (advanced) | To use System Properties as fallback for configuration. | false | boolean |
| **proxyClientClass** (proxy) | Sets the resteasy proxyClientClass. |  | String |
| **password** (security) | Sets the password. |  | String |
| **username** (security) | Sets the username. |  | String |

## Message Headers

The Resteasy component supports 22 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelResteasyProxyMethod** (producer) Constant: [`RESTEASY_PROXY_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#RESTEASY_PROXY_METHOD) | The resteasy method to process the request. |  | String |
| **CamelResteasyProxyMethodArgs** (producer) Constant: [`RESTEASY_PROXY_METHOD_PARAMS`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#RESTEASY_PROXY_METHOD_PARAMS) | The proxy method params. |  | ArrayList |
| **CamelResteasyLogin** (producer) Constant: [`RESTEASY_USERNAME`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#RESTEASY_USERNAME) | The username. |  | String |
| **CamelResteasyPassword** (producer) Constant: [`RESTEASY_PASSWORD`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#RESTEASY_PASSWORD) | The password. |  | String |
| **CamelResteasyContextPath** (common) Constant: [`RESTEASY_CONTEXT_PATH`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#RESTEASY_CONTEXT_PATH) | The context path. |  | String |
| **CamelResteasyHttpMethod** (producer) Constant: [`RESTEASY_HTTP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#RESTEASY_HTTP_METHOD) | The resteasy method to process the request. |  | String |
| **CamelResteasyHttpRequest** (common) Constant: [`RESTEASY_HTTP_REQUEST`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#RESTEASY_HTTP_REQUEST) | The http request. |  | String |
| **CamelResteasyProxyProducerException** (producer) Constant: [`RESTEASY_PROXY_PRODUCER_EXCEPTION`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#RESTEASY_PROXY_PRODUCER_EXCEPTION) | The proxy client exception. |  | Exception |
| **CamelHttpQuery** (producer) Constant: [`HTTP_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#HTTP_QUERY) | The http query. |  | String |
| **Content-Type** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#CONTENT_TYPE) | The content type. |  | String |
| **CamelHttpPath** (common) Constant: [`HTTP_PATH`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/resteasy/ResteasyConstants.html#HTTP_PATH) | The http path. |  | String |
| **Content-Encoding** (producer) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#CONTENT_ENCODING) | The HTTP content encoding. Is set on both the IN and OUT message to provide a content encoding, such as gzip. |  | String |
| **CamelHttpResponseCode** (producer) Constant: [`HTTP_RESPONSE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_RESPONSE_CODE) | The HTTP response code from the external server. Is 200 for OK. |  | int |
| **CamelHttpResponseText** (producer) Constant: [`HTTP_RESPONSE_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_RESPONSE_TEXT) | The HTTP response text from the external server. |  | String |
| **CamelHttpProtocolVersion** (producer) Constant: [`HTTP_PROTOCOL_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_PROTOCOL_VERSION) | The version of the http protocol used. |  | String |
| **Host** (producer) Constant: [`HTTP_HEADER_HOST`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_HEADER_HOST) | The target host. |  | String |
| **CamelRestHttpUri** (producer) Constant: [`REST_HTTP_URI`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#REST_HTTP_URI) | The rest http URI. |  | String |
| **CamelHttpUri** (producer) Constant: [`HTTP_URI`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_URI) | URI to call. Will override existing URI set directly on the endpoint. This uri is the uri of the http server to call. Its not the same as the Camel endpoint uri, where you can configure endpoint options such as security etc. This header does not support that, its only the uri of the http server. |  | String |
| **CamelRestHttpQuery** (producer) Constant: [`REST_HTTP_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#REST_HTTP_QUERY) | The rest http query. |  | String |
| **CamelHttpRawQuery** (producer) Constant: [`HTTP_RAW_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_RAW_QUERY) | The http raw query. |  | String |
| **CamelHttpMethod** (producer) Constant: [`HTTP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_METHOD) | 
The http method to use.

Enum values:

-   GET
    
-   PATCH
    
-   POST
    
-   PUT
    
-   DELETE
    
-   HEAD
    
-   OPTIONS
    
-   TRACE
    





 |  | HttpMethods |
| **CamelHttpCharacterEncoding** (producer) Constant: [`HTTP_CHARACTER_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-resteasy/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_CHARACTER_ENCODING) | The character encoding. |  | String |

### Usage

Consumer endpoints are similar to endpoints generated by the Servlet component. Therefore, it should be used only as input into your Camel routes. To issue HTTP requests against other HTTP endpoints, use the [HTTP Component](http-component.md).

Producer endpoints rely on Resteasy Client API. [https://docs.jboss.org/resteasy/docs/4.5.3.Final/userguide/html\_single/index.html#RESTEasy\_Client\_Framework](https://docs.jboss.org/resteasy/docs/4.5.3.Final/userguide/html_single/index.html#RESTEasy_Client_Framework)

## Putting Camel JARs in the app server boot classpath

Refer same section of [Servlet Component](servlet-component.md).

## Sample

As a basic consumer with Spring example, first, you need to publish the servlet using the `Web.xml` file to publish

Notice that below two listeners are registered when application server is initialized. The org.jboss.resteasy.plugins.server.servlet.ResteasyBootstrap class is a ServletContextListener that configures an instance of an ResteasyProviderFactory and Registry. You can obtain instances of a ResteasyProviderFactory and Registry from the ServletContext attributes org.jboss.resteasy.spi.ResteasyProviderFactory and org.jboss.resteasy.spi.Registry. From these instances you can programmatically interact with RESTEasy registration interfaces. Please note that the SpringContextLoaderListener must be declared after ResteasyBootstrap as it uses ServletContext attributes initialized by it. For further details please refer to [https://docs.jboss.org/resteasy/docs/4.5.3.Final/userguide/html\_single/index.html#RESTEasy\_Spring\_Integration](https://docs.jboss.org/resteasy/docs/4.5.3.Final/userguide/html_single/index.html#RESTEasy_Spring_Integration)

```xml
<web-app>
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>WEB-INF/applicationContext.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.jboss.resteasy.plugins.server.servlet.ResteasyBootstrap</listener-class>
    </listener>

    <listener>
        <listener-class>org.jboss.resteasy.plugins.spring.SpringContextLoaderListener</listener-class>
    </listener>

    <servlet>
        <servlet-name>resteasy-camel-servlet</servlet-name>
        <servlet-class>org.apache.camel.component.resteasy.servlet.ResteasyCamelServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>resteasy-camel-servlet</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>

</web-app>
```

Then you can define your route as follows:

```xml
<context:component-scan base-package="org.apache.camel.component.resteasy.test">
    <context:include-filter type="annotation" expression="javax.ws.rs.Path"/>
</context:component-scan>

    ........

<camel:camelContext>

    <camel:route>
        <camel:from uri="resteasy:/customer/getAll?servletName=resteasy-camel-servlet"/>
        <camel:to uri="file://target/test/consumerTest?fileName=all.txt"/>
    </camel:route>

 </camel:camelContext>
```

Notice that component-scan is important to load resteasy servlet properly into container’s runtime.

## Spring Boot Auto-Configuration

When using resteasy with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-resteasy-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 20 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.resteasy.allow-java-serialized-object** | Whether to allow java serialization when a request uses context-type=application/x-java-serialized-object. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | Boolean |
| **camel.component.resteasy.auth-caching-disabled** | Disables authentication scheme caching. | false | Boolean |
| **camel.component.resteasy.automatic-retries-disabled** | Disables automatic request recovery and re-execution. | false | Boolean |
| **camel.component.resteasy.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.resteasy.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.resteasy.connection-state-disabled** | Disables connection state tracking. | false | Boolean |
| **camel.component.resteasy.content-compression-disabled** | Disables automatic content decompression. | false | Boolean |
| **camel.component.resteasy.cookie-management-disabled** | Disables state (cookie) management. | false | Boolean |
| **camel.component.resteasy.copy-headers** | If this option is true then IN exchange headers will be copied to OUT exchange headers according to copy strategy. Setting this to false, allows to only include the headers from the HTTP response (not propagating IN headers). | true | Boolean |
| **camel.component.resteasy.default-user-agent-disabled** | Disables the default user agent set by this builder if none has been provided by the user. | false | Boolean |
| **camel.component.resteasy.enabled** | Whether to enable auto configuration of the resteasy component. This is enabled by default. |  | Boolean |
| **camel.component.resteasy.follow-redirects** | Whether to the HTTP request should follow redirects. By default the HTTP request does not follow redirects. | false | Boolean |
| **camel.component.resteasy.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.resteasy.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.resteasy.mute-exception** | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | Boolean |
| **camel.component.resteasy.proxy-consumers-classes** | Proxy classes for consumer endpoints. Multiple classes can be separated by comma. |  | String |
| **camel.component.resteasy.redirect-handling-disabled** | Disables automatic redirect handling. | false | Boolean |
| **camel.component.resteasy.response-payload-streaming-threshold** | This threshold in bytes controls whether the response payload should be stored in memory as a byte array or be streaming based. Set this to -1 to always use streaming mode. | 8192 | Integer |
| **camel.component.resteasy.skip-request-headers** | Whether to skip mapping all the Camel headers as HTTP request headers. If there are no data from Camel headers needed to be included in the HTTP request then this can avoid parsing overhead with many object allocations for the JVM garbage collector. | false | Boolean |
| **camel.component.resteasy.skip-response-headers** | Whether to skip mapping all the HTTP response headers to Camel headers. If there are no data needed from HTTP headers then this can avoid parsing overhead with many object allocations for the JVM garbage collector. | false | Boolean |