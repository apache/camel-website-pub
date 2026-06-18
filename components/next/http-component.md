# HTTP

**Since Camel 2.3**

**Only producer is supported**

The HTTP component provides HTTP-based endpoints for calling external HTTP resources (as a client to call external servers using HTTP).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-http</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

http:hostname\[:port\]\[/resourceUri\]\[?options\]

Will by default use port 80 for HTTP and 443 for HTTPS.

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

The HTTP component supports 50 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **logHttpActivity** (producer) | To enable logging HTTP request and response. You can use a custom LoggingHttpActivityListener as httpActivityListener to control logging options. | false | boolean |
| **skipControlHeaders** (producer) | Whether to skip Camel control headers (CamelHttp…​ headers) to influence this endpoint. Control headers from previous HTTP components can influence how this Camel component behaves such as CamelHttpPath, CamelHttpQuery, etc. | false | boolean |
| **skipRequestHeaders** (producer) | Whether to skip mapping all the Camel headers as HTTP request headers. This is useful when you know that calling the HTTP service should not include any custom headers. | false | boolean |
| **skipResponseHeaders** (producer) | Whether to skip mapping all the HTTP response headers to Camel headers. | false | boolean |
| **contentTypeCharsetEnabled** (producer (advanced)) | Whether the Content-Type header should automatic include charset for string based content. | true | boolean |
| **cookieStore** (producer (advanced)) | To use a custom org.apache.hc.client5.http.cookie.CookieStore. By default the org.apache.hc.client5.http.cookie.BasicCookieStore is used which is an in-memory only cookie store. Notice if bridgeEndpoint=true then the cookie store is forced to be a noop cookie store as cookie shouldn’t be stored as we are just bridging (eg acting as a proxy). |  | CookieStore |
| **copyHeaders** (producer (advanced)) | If this option is true then IN exchange headers will be copied to OUT exchange headers according to copy strategy. Setting this to false, allows to only include the headers from the HTTP response (not propagating IN headers). | true | boolean |
| **followRedirects** (producer (advanced)) | Whether to the HTTP request should follow redirects. By default the HTTP request does not follow redirects. | false | boolean |
| **httpActivityListener** (producer (advanced)) | **Autowired** To use a custom activity listener. |  | HttpActivityListener |
| **responsePayloadStreamingThreshold** (producer (advanced)) | This threshold in bytes controls whether the response payload should be stored in memory as a byte array or be streaming based. Set this to -1 to always use streaming mode. | 8192 | int |
| **userAgent** (producer (advanced)) | To set a custom HTTP User-Agent request header. |  | String |
| **allowJavaSerializedObject** (advanced) | Whether to allow java serialization when a request uses context-type=application/x-java-serialized-object. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | boolean |
| **authCachingDisabled** (advanced) | Disables authentication scheme caching. | false | boolean |
| **automaticRetriesDisabled** (advanced) | Disables automatic request recovery and re-execution. This is useful when a server responds with HTTP 429 (Too Many Requests) and includes a long Retry-After header, which would otherwise cause the client to wait (and appear to hang) before retrying. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientConnectionManager** (advanced) | To use a custom and shared HttpClientConnectionManager to manage connections. If this has been configured then this is always used for all endpoints created by this component. |  | HttpClientConnectionManager |
| **connectionsPerRoute** (advanced) | The maximum number of connections per route. | 20 | int |
| **connectionStateDisabled** (advanced) | Disables connection state tracking. | false | boolean |
| **connectionTimeToLive** (advanced) | The time for connection to live, the time unit is millisecond, the default value is always keepAlive. |  | long |
| **contentCompressionDisabled** (advanced) | Disables automatic content decompression. | false | boolean |
| **cookieManagementDisabled** (advanced) | Disables state (cookie) management. | false | boolean |
| **defaultUserAgentDisabled** (advanced) | Disables the default user agent set by this builder if none has been provided by the user. | false | boolean |
| **httpBinding** (advanced) | To use a custom HttpBinding to control the mapping between Camel message and HttpClient. |  | HttpBinding |
| **httpClientConfigurer** (advanced) | To use the custom HttpClientConfigurer to perform configuration of the HttpClient that will be used. |  | HttpClientConfigurer |
| **httpConfiguration** (advanced) | To use the shared HttpConfiguration as base configuration. |  | HttpConfiguration |
| **httpContext** (advanced) | To use a custom org.apache.hc.core5.http.protocol.HttpContext when executing requests. |  | HttpContext |
| **maxTotalConnections** (advanced) | The maximum number of connections. | 200 | int |
| **redirectHandlingDisabled** (advanced) | Disables automatic redirect handling. | false | boolean |
| **useSystemProperties** (advanced) | To use System Properties as fallback for configuration for configuring HTTP Client. | false | boolean |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **nonProxyHosts** (proxy) | Comma-separated list of hosts that should bypass the proxy. Supports wildcards, e.g., localhost,.example.com,192.168.. |  | String |
| **proxyAuthDomain** (proxy) | Proxy authentication domain to use with NTLM. |  | String |
| **proxyAuthHost** (proxy) | **Deprecated** Proxy server host. |  | String |
| **proxyAuthMethod** (proxy) | 
Proxy authentication method to use (NTLM is deprecated).

Enum values:

-   Basic
    
-   Digest
    
-   NTLM
    





 |  | String |
| **proxyAuthNtHost** (proxy) | Proxy authentication domain (workstation name) to use with NTLM (NTLM is deprecated). |  | String |
| **proxyAuthPassword** (proxy) | Proxy server password. |  | String |
| **proxyAuthPort** (proxy) | **Deprecated** Proxy server port. |  | Integer |
| **proxyAuthScheme** (proxy) | 

Proxy server authentication protocol scheme to use.

Enum values:

-   http
    
-   https
    





 |  | String |
| **proxyAuthUsername** (proxy) | Proxy server username. |  | String |
| **proxyHost** (proxy) | Proxy server host. |  | String |
| **proxyPort** (proxy) | Proxy server port. |  | Integer |
| **hostnameVerificationPolicy** (security) | 

Controls how hostname verification is performed during the TLS handshake. CLIENT (default) delegates entirely to the configured x509HostnameVerifier, preserving the behaviour of httpclient 5.5 and earlier a NoopHostnameVerifier will disable verification. BUILTIN uses the JDK SSLParameters hostname check only, ignoring the configured verifier. BOTH runs the JDK built-in check first and then the configured verifier; a NoopHostnameVerifier cannot bypass the built-in check under BUILTIN or BOTH. Prefer BOTH when no custom verifier semantics are needed for stronger out-of-the-box security.

Enum values:

-   CLIENT
    
-   BUILTIN
    
-   BOTH
    





 | CLIENT | HostnameVerificationPolicy |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. Important: Only one instance of org.apache.camel.support.jsse.SSLContextParameters is supported per HttpComponent. If you need to use 2 or more different instances, you need to define a new HttpComponent per instance you need. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **x509HostnameVerifier** (security) | To use a custom X509HostnameVerifier such as DefaultHostnameVerifier or NoopHostnameVerifier. |  | HostnameVerifier |
| **connectionRequestTimeout** (timeout) | Returns the connection lease request timeout (in millis) used when requesting a connection from the connection manager. A timeout value of zero is interpreted as a disabled timeout. | 180000 | long |
| **connectTimeout** (timeout) | Determines the timeout (in millis) until a new connection is fully established. A timeout value of zero is interpreted as an infinite timeout. | 180000 | long |
| **responseTimeout** (timeout) | Determines the timeout (in millis) until arrival of a response from the opposite endpoint. A timeout value of zero is interpreted as an infinite timeout. Please note that response timeout may be unsupported by HTTP transports with message multiplexing. |  | long |
| **soTimeout** (timeout) | Determines the default socket timeout (in millis) value for blocking I/O operations. | 180000 | long |

## Endpoint Options

The HTTP endpoint is configured using URI syntax:

http://httpUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **httpUri** (common) | **Required** The url of the HTTP endpoint to call. |  | URI |

### Query Parameters (67 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **disableStreamCache** (common) | Determines whether or not the raw input stream is cached or not. The Camel consumer (camel-servlet, camel-jetty etc.) will by default cache the input stream to support reading it multiple times to ensure it Camel can retrieve all data from the stream. However you can set this option to true when you for example need to access the raw stream, such as streaming it directly to a file or other persistent store. DefaultHttpBinding will copy the request input stream into a stream cache and put it into message body if this option is false to support reading the stream multiple times. If you use Servlet to bridge/proxy an endpoint then consider enabling this option to improve performance, in case you do not need to read the message payload multiple times. The producer (camel-http) will by default cache the response body stream. If setting this option to true, then the producers will not cache the response body stream but use the response stream as-is (the stream can only be read once) as the message body. | false | boolean |
| **headerFilterStrategy** (common (advanced)) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **bridgeEndpoint** (producer) | If the option is true, HttpProducer will ignore the Exchange.HTTP\_URI header, and use the endpoint’s URI for request. You may also set the option throwExceptionOnFailure to be false to let the HttpProducer send all the fault response back. | false | boolean |
| **connectionClose** (producer) | Specifies whether a Connection Close header must be added to HTTP Request. By default connectionClose is false. | false | boolean |
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
| **logHttpActivity** (producer) | To enable logging HTTP request and response. You can use a custom LoggingHttpActivityListener as httpActivityListener to control logging options. | false | boolean |
| **multipartUpload** (producer) | Whether to force using multipart/form-data for easy file uploads. This is only to be used for uploading the message body as a single entity form-data. For uploading multiple entries then use org.apache.hc.client5.http.entity.mime.MultipartEntityBuilder to build the form. | false | boolean |
| **multipartUploadName** (producer) | The name of the multipart/form-data when multipartUpload is enabled. | data | String |
| **skipControlHeaders** (producer) | Whether to skip Camel control headers (CamelHttp…​ headers) to influence this endpoint. Control headers from previous HTTP components can influence how this Camel component behaves such as CamelHttpPath, CamelHttpQuery, etc. | false | boolean |
| **skipRequestHeaders** (producer) | Whether to skip mapping the Camel headers as HTTP request headers. This is useful when you know that calling the HTTP service should not include any custom headers. | false | boolean |
| **skipResponseHeaders** (producer) | Whether to skip mapping all the HTTP response headers to Camel headers. | false | boolean |
| **throwExceptionOnFailure** (producer) | Option to disable throwing the HttpOperationFailedException in case of failed responses from the remote server. This allows you to get all responses regardless of the HTTP status code. | true | boolean |
| **clearExpiredCookies** (producer (advanced)) | Whether to clear expired cookies before sending the HTTP request. This ensures the cookies store does not keep growing by adding new cookies which is newer removed when they are expired. If the component has disabled cookie management then this option is disabled too. | true | boolean |
| **contentTypeCharsetEnabled** (producer (advanced)) | Whether the Content-Type header should automatic include charset for string based content. | true | boolean |
| **cookieHandler** (producer (advanced)) | Configure a cookie handler to maintain a HTTP session. |  | CookieHandler |
| **cookieStore** (producer (advanced)) | To use a custom CookieStore. By default the BasicCookieStore is used which is an in-memory only cookie store. Notice if bridgeEndpoint=true then the cookie store is forced to be a noop cookie store as cookie shouldn’t be stored as we are just bridging (eg acting as a proxy). If a cookieHandler is set then the cookie store is also forced to be a noop cookie store as cookie handling is then performed by the cookieHandler. |  | CookieStore |
| **copyHeaders** (producer (advanced)) | If this option is true then IN exchange headers will be copied to OUT exchange headers according to copy strategy. Setting this to false, allows to only include the headers from the HTTP response (not propagating IN headers). | true | boolean |
| **customHostHeader** (producer (advanced)) | To use custom host header for producer. When not set in query will be ignored. When set will override host header derived from url. |  | String |
| **deleteWithBody** (producer (advanced)) | Whether the HTTP DELETE should include the message body or not. By default HTTP DELETE do not include any HTTP body. However in some rare cases users may need to be able to include the message body. | false | boolean |
| **followRedirects** (producer (advanced)) | Whether to the HTTP request should follow redirects. By default the HTTP request does not follow redirects. | false | boolean |
| **getWithBody** (producer (advanced)) | Whether the HTTP GET should include the message body or not. By default HTTP GET do not include any HTTP body. However in some rare cases users may need to be able to include the message body. | false | boolean |
| **httpActivityListener** (producer (advanced)) | To use a custom activity listener. |  | HttpActivityListener |
| **ignoreResponseBody** (producer (advanced)) | If this option is true, The http producer won’t read response body and cache the input stream. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **okStatusCodeRange** (producer (advanced)) | The status codes which are considered a success response. The values are inclusive. Multiple ranges can be defined, separated by comma, e.g. 200-204,209,301-304. Each range must be a single number or from-to with the dash included. | 200-299 | String |
| **preserveHostHeader** (producer (advanced)) | If the option is true, HttpProducer will set the Host header to the value contained in the current exchange Host header, useful in reverse proxy applications where you want the Host header received by the downstream server to reflect the URL called by the upstream client, this allows applications which use the Host header to generate accurate URL’s for a proxied service. | false | boolean |
| **userAgent** (producer (advanced)) | To set a custom HTTP User-Agent request header. |  | String |
| **clientBuilder** (advanced) | Provide access to the http client request parameters used on new RequestConfig instances used by producers or consumers of this endpoint. |  | HttpClientBuilder |
| **clientConnectionManager** (advanced) | To use a custom HttpClientConnectionManager to manage connections. |  | HttpClientConnectionManager |
| **connectionsPerRoute** (advanced) | The maximum number of connections per route. | 20 | int |
| **httpClient** (advanced) | Sets a custom HttpClient to be used by the producer. |  | HttpClient |
| **httpClientConfigurer** (advanced) | Register a custom configuration strategy for new HttpClient instances created by producers or consumers such as to configure authentication mechanisms etc. |  | HttpClientConfigurer |
| **httpClientOptions** (advanced) | To configure the HttpClient using the key/values from the Map. This is a multi-value option with prefix: httpClient. |  | Map |
| **httpConnectionOptions** (advanced) | To configure the connection and the socket using the key/values from the Map. This is a multi-value option with prefix: httpConnection. |  | Map |
| **httpContext** (advanced) | To use a custom HttpContext instance. |  | HttpContext |
| **maxTotalConnections** (advanced) | The maximum number of connections. | 200 | int |
| **useSystemProperties** (advanced) | To use System Properties as fallback for configuration for configuring HTTP Client. | false | boolean |
| **nonProxyHosts** (proxy) | Comma-separated list of hosts that should bypass the proxy. Supports wildcards, e.g., localhost,.example.com,192.168.. |  | String |
| **proxyAuthDomain** (proxy) | **Deprecated** Proxy authentication domain to use with NTLM. |  | String |
| **proxyAuthHost** (proxy) | **Deprecated** Proxy server host. |  | String |
| **proxyAuthMethod** (proxy) | 

Proxy authentication method to use (NTLM is deprecated).

Enum values:

-   Basic
    
-   Bearer
    
-   NTLM
    





 |  | String |
| **proxyAuthNtHost** (proxy) | **Deprecated** Proxy authentication domain (workstation name) to use with NTLM. |  | String |
| **proxyAuthPassword** (proxy) | Proxy server password. |  | String |
| **proxyAuthPort** (proxy) | **Deprecated** Proxy server port. |  | int |
| **proxyAuthScheme** (proxy) | 

Proxy server authentication protocol scheme to use.

Enum values:

-   http
    
-   https
    





 |  | String |
| **proxyAuthUsername** (proxy) | Proxy server username. |  | String |
| **proxyHost** (proxy) | Proxy server host. |  | String |
| **proxyPort** (proxy) | Proxy server port. |  | int |
| **authBearerToken** (security) | Authentication bearer token. |  | String |
| **authDomain** (security) | **Deprecated** Authentication domain to use with NTLM. |  | String |
| **authenticationPreemptive** (security) | If this option is true, camel-http sends preemptive basic authentication to the server. | false | boolean |
| **authHost** (security) | **Deprecated** Authentication host to use with NTLM. |  | String |
| **authMethod** (security) | 

Authentication methods allowed to use as a comma separated list of values Basic, Bearer, or NTLM. (NTLM is deprecated).

Enum values:

-   Basic
    
-   Bearer
    
-   NTLM
    





 |  | String |
| **authPassword** (security) | Authentication password. |  | String |
| **authUsername** (security) | Authentication username. |  | String |
| **hostnameVerificationPolicy** (security) | 

Controls how hostname verification is performed during the TLS handshake. CLIENT (default) delegates entirely to the configured x509HostnameVerifier, preserving the behaviour of httpclient 5.5 and earlier a NoopHostnameVerifier will disable verification. BUILTIN uses the JDK SSLParameters hostname check only, ignoring the configured verifier. BOTH runs the JDK built-in check first and then the configured verifier; a NoopHostnameVerifier cannot bypass the built-in check under BUILTIN or BOTH. Prefer BOTH when no custom verifier semantics are needed for stronger out-of-the-box security.

Enum values:

-   CLIENT
    
-   BUILTIN
    
-   BOTH
    





 | CLIENT | HostnameVerificationPolicy |
| **oauth2BodyAuthentication** (security) | Whether to use OAuth2 body authentication. | false | boolean |
| **oauth2CachedTokensDefaultExpirySeconds** (security) | Default expiration time for cached OAuth2 tokens, in seconds. Used if token response does not contain 'expires\_in' field. | 3600 | long |
| **oauth2CachedTokensExpirationMarginSeconds** (security) | Amount of time which is deducted from OAuth2 tokens expiry time to compensate for the time it takes OAuth2 Token Endpoint to send the token over http, in seconds. Set this parameter to high value if you OAuth2 Token Endpoint answers slowly or you tokens expire quickly. If you set this parameter to too small value, you can get 4xx http errors because camel will think that the received token is still valid, while in reality the token is expired for the Authentication server. | 5 | long |
| **oauth2CacheTokens** (security) | Whether to cache OAuth2 client tokens. | false | boolean |
| **oauth2ClientId** (security) | OAuth2 client id. |  | String |
| **oauth2ClientSecret** (security) | OAuth2 client secret. |  | String |
| **oauth2ResourceIndicator** (security) | OAuth2 Token endpoint. |  | String |
| **oauth2Scope** (security) | OAuth2 scope. |  | String |
| **oauth2TokenEndpoint** (security) | OAuth2 Resource Indicator. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. Important: Only one instance of org.apache.camel.util.jsse.SSLContextParameters is supported per HttpComponent. If you need to use 2 or more different instances, you need to define a new HttpComponent per instance you need. |  | SSLContextParameters |
| **x509HostnameVerifier** (security) | To use a custom X509HostnameVerifier such as DefaultHostnameVerifier or NoopHostnameVerifier. |  | HostnameVerifier |

## Message Headers

The HTTP component supports 14 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **Content-Encoding** (producer) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#CONTENT_ENCODING) | The HTTP content encoding. Is set on both the IN and OUT message to provide a content encoding, such as gzip. |  | String |
| **CamelHttpResponseCode** (producer) Constant: [`HTTP_RESPONSE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_RESPONSE_CODE) | The HTTP response code from the external server. Is 200 for OK. |  | int |
| **CamelHttpResponseText** (producer) Constant: [`HTTP_RESPONSE_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_RESPONSE_TEXT) | The HTTP response text from the external server. |  | String |
| **CamelHttpQuery** (producer) Constant: [`HTTP_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_QUERY) | URI parameters. Will override existing URI parameters set directly on the endpoint. |  | String |
| **CamelHttpProtocolVersion** (producer) Constant: [`HTTP_PROTOCOL_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_PROTOCOL_VERSION) | The version of the http protocol used. |  | String |
| **Host** (producer) Constant: [`HTTP_HEADER_HOST`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_HEADER_HOST) | The target host. |  | String |
| **CamelRestHttpUri** (producer) Constant: [`REST_HTTP_URI`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#REST_HTTP_URI) | The rest http URI. |  | String |
| **CamelHttpUri** (producer) Constant: [`HTTP_URI`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_URI) | URI to call. Will override existing URI set directly on the endpoint. This uri is the uri of the http server to call. Its not the same as the Camel endpoint uri, where you can configure endpoint options such as security etc. This header does not support that, its only the uri of the http server. |  | String |
| **CamelHttpPath** (producer) Constant: [`HTTP_PATH`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_PATH) | Request URI’s path, the header will be used to build the request URI with the HTTP\_URI. |  | String |
| **CamelRestHttpQuery** (producer) Constant: [`REST_HTTP_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#REST_HTTP_QUERY) | The rest http query. |  | String |
| **CamelHttpRawQuery** (producer) Constant: [`HTTP_RAW_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_RAW_QUERY) | The http raw query. |  | String |
| **CamelHttpMethod** (producer) Constant: [`HTTP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_METHOD) | 
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
| **CamelHttpCharacterEncoding** (producer) Constant: [`HTTP_CHARACTER_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#HTTP_CHARACTER_ENCODING) | The character encoding. |  | String |
| **Content-Type** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-http/latest/org/apache/camel/component/http/HttpConstants.html#CONTENT_TYPE) | The HTTP content type. Is set on both the IN and OUT message to provide a content type, such as text/html. |  | String |

## Usage

### Message Body

Camel will store the HTTP response from the external server on the _OUT_ body. All headers from the _IN_ message will be copied to the _OUT_ message, so headers are preserved during routing. Additionally, Camel will add the HTTP response headers as well to the _OUT_ message headers.

### Using System Properties

When setting useSystemProperties to true, the HTTP Client will look for the following System Properties, and it will use it:

-   `ssl.TrustManagerFactory.algorithm`
    
-   `javax.net.ssl.trustStoreType`
    
-   `javax.net.ssl.trustStore`
    
-   `javax.net.ssl.trustStoreProvider`
    
-   `javax.net.ssl.trustStorePassword`
    
-   `java.home`
    
-   `ssl.KeyManagerFactory.algorithm`
    
-   `javax.net.ssl.keyStoreType`
    
-   `javax.net.ssl.keyStore`
    
-   `javax.net.ssl.keyStoreProvider`
    
-   `javax.net.ssl.keyStorePassword`
    
-   `http.proxyHost`
    
-   `http.proxyPort`
    
-   `http.nonProxyHosts`
    
-   `http.keepAlive`
    
-   `http.maxConnections`
    

### Response code

Camel will handle, according to the HTTP response code:

-   Response code is in the range 100..299, Camel regards it as a success response.
    
-   Response code is in the range 300..399, Camel regards it as a redirection response and will throw a `HttpOperationFailedException` with the information.
    
-   Response code is 400+, Camel regards it as an external server failure and will throw a `HttpOperationFailedException` with the information.
    

**throwExceptionOnFailure**

The option, `throwExceptionOnFailure`, can be set to `false` to prevent the `HttpOperationFailedException` from being thrown for failed response codes. This allows you to get any response from the remote server.

### Handling HTTP 429 Too Many Requests

When a server responds with HTTP 429 (Too Many Requests) and includes a `Retry-After` header, the underlying Apache HttpClient 5 will automatically wait for the specified duration before retrying the request. If the server returns a long retry delay (for example, `Retry-After: 3600` for one hour), the HTTP component will appear to hang for that duration.

To avoid this, you can disable automatic retries on the component:

_Java-only: programmatic `HttpComponent` configuration_

```java
HttpComponent httpComponent = context.getComponent("https", HttpComponent.class);
httpComponent.setAutomaticRetriesDisabled(true);
```

Or as a URI option on the endpoint:

```text
https://myhost/mypath?automaticRetriesDisabled=true
```

With automatic retries disabled, a 429 response is treated as an error and a `HttpOperationFailedException` is thrown immediately (unless `throwExceptionOnFailure=false`).

### Exceptions

`HttpOperationFailedException` exception contains the following information:

-   The HTTP status code
    
-   The HTTP status line (text of the status code)
    
-   Redirect location if server returned a redirect
    
-   Response body as a `java.lang.String`, if server provided a body as response
    

### Which HTTP method will be used

The following algorithm is used to determine what HTTP method should be used:  
1\. Use method provided as endpoint configuration (`httpMethod`).  
2\. Use method provided in header (`Exchange.HTTP_METHOD`).  
3\. `GET` if query string is provided in header.  
4\. `GET` if endpoint is configured with a query string.  
5\. `POST` if there is data to send (body is not `null`).  
6\. `GET` otherwise.

### Configuring URI to call

You can set the HTTP producer’s URI directly from the endpoint URI. In the route below, Camel will call out to the external server, `oldhost`, using HTTP.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("http://oldhost");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="http://oldhost"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: http://oldhost
```

You can override the HTTP endpoint URI by adding a header with the key `Exchange.HTTP_URI` on the message.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .setHeader("CamelHttpUri", constant("http://newhost"))
  .to("http://oldhost");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelHttpUri">
    <constant>http://newhost</constant>
  </setHeader>
  <to uri="http://oldhost"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelHttpUri
            constant: "http://newhost"
        - to:
            uri: http://oldhost
```

In the sample above, Camel will call the [http://newhost](http://newhost) despite the endpoint is configured with [http://oldhost](http://oldhost).  
If the http endpoint is working in bridge mode, it will ignore the message header of `Exchange.HTTP_URI`.

### Configuring URI Parameters

The **http** producer supports URI parameters to be sent to the HTTP server. The URI parameters can either be set directly on the endpoint URI or as a header with the key `Exchange.HTTP_QUERY` on the message.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("http://oldhost?order=123&detail=short");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="http://oldhost?order=123&amp;detail=short"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: http://oldhost
            parameters:
              order: 123
              detail: short
```

Or options provided in a header:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .setHeader("CamelHttpQuery", constant("order=123&detail=short"))
  .to("http://oldhost");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelHttpQuery">
    <constant>order=123&amp;detail=short</constant>
  </setHeader>
  <to uri="http://oldhost"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelHttpQuery
            constant: "order=123&detail=short"
        - to:
            uri: http://oldhost
```

### How to set the http method (GET/PATCH/POST/PUT/DELETE/HEAD/OPTIONS/TRACE) to the HTTP producer

The HTTP component provides a way to set the HTTP request method by setting the message header. Here is an example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .setHeader("CamelHttpMethod", constant("POST"))
  .to("http://www.google.com")
  .to("mock:results");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelHttpMethod">
      <constant>POST</constant>
  </setHeader>
  <to uri="http://www.google.com"/>
  <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelHttpMethod
            constant: POST
        - to:
            uri: http://www.google.com
        - to:
            uri: mock:results
```

### Using client timeout - SO\_TIMEOUT

See the [HttpSOTimeoutTest](https://github.com/apache/camel/blob/main/components/camel-http/src/test/java/org/apache/camel/component/http/HttpSOTimeoutTest.java) unit test.

### Configuring a Proxy

The HTTP component provides a way to configure a proxy.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("http://oldhost?proxyAuthHost=www.myproxy.com&proxyAuthPort=80");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="http://oldhost?proxyAuthHost=www.myproxy.com&amp;proxyAuthPort=80"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: http://oldhost
            parameters:
              proxyAuthHost: www.myproxy.com
              proxyAuthPort: 80
```

There is also support for proxy authentication via the `proxyAuthUsername` and `proxyAuthPassword` options.

#### Using proxy settings outside of URI

**Deprecated**

To avoid System properties conflicts, you can set proxy configuration only from the CamelContext or URI.  
Java DSL :

_Java-only: programmatic `CamelContext` global options configuration (deprecated)_

```java
context.getGlobalOptions().put("http.proxyHost", "172.168.18.9");
context.getGlobalOptions().put("http.proxyPort", "8080");
```

Spring XML

```xml
<camelContext>
    <properties>
        <property key="http.proxyHost" value="172.168.18.9"/>
        <property key="http.proxyPort" value="8080"/>
   </properties>
</camelContext>
```

Camel will first set the settings from Java System or CamelContext Properties and then the endpoint proxy options if provided. So you can override the system properties with the endpoint options.

There is also a `http.proxyScheme` property you can set to explicitly configure the scheme to use.

> **Important**
> Using GlobalOptions (as shown above) is deprecated. Instead, configure proxy settings on the HTTP component level.

### Configuring charset

If you are using `POST` to send data you can configure the `charset` using the `Exchange` property:

_Java-only: setting exchange property programmatically_

```java
exchange.setProperty(Exchange.CHARSET_NAME, "ISO-8859-1");
```

#### Example with scheduled poll

This sample polls the Google homepage every 10 seconds and write the page to the file `message.html`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer://foo?fixedRate=true&delay=0&period=10000")
  .to("http://www.google.com")
  .setHeader("CamelFileName", constant("message.html"))
  .to("file:target/google");
```

```xml
<route>
  <from uri="timer://foo?fixedRate=true&amp;delay=0&amp;period=10000"/>
  <to uri="http://www.google.com"/>
  <setHeader name="CamelFileName">
    <constant>message.html</constant>
  </setHeader>
  <to uri="file:target/google"/>
</route>
```

```yaml
- route:
    from:
      uri: timer://foo
      parameters:
        fixedRate: true
        delay: 0
        period: 10000
      steps:
        - to:
            uri: http://www.google.com
        - setHeader:
            name: CamelFileName
            constant: message.html
        - to:
            uri: file:target/google
```

#### URI Parameters from the endpoint URI

In this sample, we have the complete URI endpoint that is just what you would have typed in a web browser. Multiple URI parameters can of course be set using the `&` character as separator, just as you would in the web browser. Camel does no tricks here.

_Java-only: uses `ProducerTemplate` test API_

```java
// we query for Camel at the Google page
template.sendBody("http://www.google.com/search?q=Camel", null);
```

#### URI Parameters from the Message

_Java-only: uses `ProducerTemplate` test API with headers_

```java
Map headers = new HashMap();
headers.put(Exchange.HTTP_QUERY, "q=Camel&lr=lang_en");
// we query for Camel and English language at Google
template.sendBody("http://www.google.com/search", null, headers);
```

In the header value above notice that it should **not** be prefixed with `?` and you can separate parameters as usual with the `&` char.

#### Getting the Response Code

You can get the HTTP response code from the HTTP component by getting the value from the Out message header with `Exchange.HTTP_RESPONSE_CODE`.

_Java-only: uses `ProducerTemplate` and `Processor` to inspect response code_

```java
Exchange exchange = template.send("http://www.google.com/search", e -> {
    e.getIn().setHeader("CamelHttpQuery", "hl=en&q=activemq");
});
Message out = exchange.getMessage();
int responseCode = out.getHeader("CamelHttpResponseCode", Integer.class);
```

### Defining specific properties of Apache HTTP client via Camel parameters

There are different parameters you could set in a route, that will influence the behavior of the Apache HTTP Client.

Most of the option are available here: [Apache HttpClient Request Config Builder](https://hc.apache.org/httpcomponents-client-5.4.x/current/httpclient5/apidocs/org/apache/hc/client5/http/config/RequestConfig.Builder.md).

-   httpClient.authenticationEnabled - Determines whether authentication should be handled automatically.
    
-   httpClient.circularRedirectsAllowed - Determines whether circular redirects (redirects to the same location) should be allowed.
    
-   httpClient.connectionKeepAlive - Determines the default of value of connection keep-alive time period when not explicitly communicated by the origin server with a Keep-Alive response header.
    
-   httpClient.connectionRequestTimeout - Determines the connection lease request timeout used when requesting a connection from the connection manager.
    
-   httpClient.contentCompressionEnabled - Determines whether the target server is requested to compress content.
    
-   httpClient.cookieSpec - Determines the name of the cookie specification to be used for HTTP state management.
    
-   httpClient.defaultKeepAlive - Determines the default keep-alive
    
-   httpClient.expectContinueEnabled - Determines whether the 'Expect: 100-Continue' handshake is enabled for entity enclosing methods.
    
-   httpClient.hardCancellationEnabled - Determines whether request cancellation should kill the underlying connection.
    
-   httpClient.maxRedirects - Determines the maximum number of redirects to be followed.
    
-   httpClient.protocolUpgradeEnabled - Determines whether the client server should automatically attempt to upgrade to a safer or a newer version of the protocol, whenever possible.
    
-   httpClient.redirectsEnabled - Determines whether redirects should be handled automatically.
    
-   httpClient.responseTimeout - Determines the timeout until arrival of a response from the opposite endpoint.
    

### Disabling Cookies

To disable cookies in the CookieStore, you can set the HTTP Client to ignore cookies by adding this URI option: `httpClient.cookieSpec=ignore`. This doesn’t affect cookies manually set in the `Cookie` header

### Basic auth with the streaming message body

To avoid the `NonRepeatableRequestException`, you need to do the Preemptive Basic Authentication by adding the option: `authenticationPreemptive=true`

### OAuth2 Support

To get an access token from an Authorization Server and fill that in Authorization header to do requests to protected services, you will need to use `oauth2ClientId`, `oauth2ClientSecret` and `oauth2TokenEndpoint` properties, and those should be defined as specified at RFC 6749 and provided by your Authorization Server.

In below example camel will do an underlying request to `[https://localhost:8080/realms/master/protocol/openid-connect/token](https://localhost:8080/realms/master/protocol/openid-connect/token)` using provided credentials (client id and client secret), then will get `access_token` from response and lastly will fill it at `Authorization` header of request which will be done to `[https://localhost:9090](https://localhost:9090)`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("https://localhost:9090/?oauth2ClientId=my-client-id&oauth2ClientSecret=my-client-secret&oauth2TokenEndpoint=https://localhost:8080/realms/master/protocol/openid-connect/token&oauth2Scope=my-scope");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="https://localhost:9090/?oauth2ClientId=my-client-id&amp;oauth2ClientSecret=my-client-secret&amp;oauth2TokenEndpoint=https://localhost:8080/realms/master/protocol/openid-connect/token&amp;oauth2Scope=my-scope"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "https://localhost:9090/"
            parameters:
              oauth2ClientId: my-client-id
              oauth2ClientSecret: my-client-secret
              oauth2TokenEndpoint: "https://localhost:8080/realms/master/protocol/openid-connect/token"
              oauth2Scope: my-scope
```

Additional support for OAuth2 is for RFC 8707 where a _Resource Indicator_ must be provided in the body:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("https://localhost:9090/?oauth2ClientId=my-client-id&oauth2ClientSecret=my-client-secret&oauth2TokenEndpoint=https://localhost:8080/realms/master/protocol/openid-connect/token&oauth2Scope=my-scope&oauth2ResourceIndicator=https://localhost:9090");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="https://localhost:9090/?oauth2ClientId=my-client-id&amp;oauth2ClientSecret=my-client-secret&amp;oauth2TokenEndpoint=https://localhost:8080/realms/master/protocol/openid-connect/token&amp;oauth2Scope=my-scope&amp;oauth2ResourceIndicator=https://localhost:9090"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: "https://localhost:9090/"
            parameters:
              oauth2ClientId: my-client-id
              oauth2ClientSecret: my-client-secret
              oauth2TokenEndpoint: "https://localhost:8080/realms/master/protocol/openid-connect/token"
              oauth2Scope: my-scope
              oauth2ResourceIndicator: "https://localhost:9090"
```

> **Note**
> Resource Indicator is the URL to the actual endpoint as defined in the component URI.

> **Note**
> Camel only provides support for OAuth2 client credentials flow

> **Important**
> Camel does not perform any validation in access token. It’s up to the underlying service to validate it.

### Advanced Usage

If you need more control over the HTTP producer, you should use the `HttpComponent` where you can set various classes to give you custom behavior.

#### Setting up SSL for HTTP Client

Using the JSSE Configuration Utility

The HTTP component supports SSL/TLS configuration through the [Camel JSSE Configuration Utility](../../manual/camel-configuration-utilities.md). This utility greatly decreases the amount of component-specific code you need to write and is configurable at the endpoint and component levels. The following examples demonstrate how to use the utility with the HTTP component.

Programmatic configuration of the component

_Java-only: programmatic `SSLContextParameters` setup_

```java
KeyStoreParameters ksp = new KeyStoreParameters();
ksp.setResource("file:/users/home/server/keystore.jks");
ksp.setPassword("keystorePassword");

KeyManagersParameters kmp = new KeyManagersParameters();
kmp.setKeyStore(ksp);
kmp.setKeyPassword("keyPassword");

SSLContextParameters scp = new SSLContextParameters();
scp.setKeyManagers(kmp);

HttpComponent httpComponent = getContext().getComponent("https", HttpComponent.class);
httpComponent.setSslContextParameters(scp);
```

Spring DSL based configuration of endpoint

```xml
  <camel:sslContextParameters
      id="sslContextParameters">
    <camel:keyManagers
        keyPassword="keyPassword">
      <camel:keyStore
          resource="file:/users/home/server/keystore.jks"
          password="keystorePassword"/>
    </camel:keyManagers>
  </camel:sslContextParameters>

  <to uri="https://127.0.0.1/mail/?sslContextParameters=#sslContextParameters"/>
```

Configuring Apache HTTP Client Directly

Basically, a camel-http component is built on the top of [Apache HttpClient](https://hc.apache.org/httpcomponents-client-5.1.x/). Please refer to [SSL/TLS customization](https://hc.apache.org/httpcomponents-client-4.5.x/current/tutorial/html/connmgmt.md) (even if the link is referring to an article about version 4, it is still more or less relevant moreover there is no equivalent for version 5) for details or have a look into the `org.apache.camel.component.http.HttpsServerTestSupport` unit test base class.  
You can also implement a custom `org.apache.camel.component.http.HttpClientConfigurer` to do some configuration on the http client if you need full control of it.

However, if you _just_ want to specify the keystore and truststore, you can do this with Apache HTTP `HttpClientConfigurer`, for example:

_Java-only: programmatic `KeyStore` and `SchemeRegistry` setup_

```java
KeyStore keystore = ...;
KeyStore truststore = ...;

SchemeRegistry registry = new SchemeRegistry();
registry.register(new Scheme("https", 443, new SSLSocketFactory(keystore, "mypassword", truststore)));
```

And then you need to create a class that implements `HttpClientConfigurer`, and registers https protocol providing a keystore or truststore per the example above. Then, from your camel route builder class, you can hook it up like so:

_Java-only: programmatic `HttpClientConfigurer` setup_

```java
HttpComponent httpComponent = getContext().getComponent("http", HttpComponent.class);
httpComponent.setHttpClientConfigurer(new MyHttpClientConfigurer());
```

If you are doing this using the Spring DSL, you can specify your `HttpClientConfigurer` using the URI. For example:

```xml
<bean id="myHttpClientConfigurer"
 class="my.https.HttpClientConfigurer">
</bean>

<to uri="https://myhostname.com:443/myURL?httpClientConfigurer=myHttpClientConfigurer"/>
```

As long as you implement the `HttpClientConfigurer` and configure your keystore and truststore as described above, it will work fine.

Using HTTPS to authenticate gotchas

An end user reported that he had a problem with authenticating with HTTPS. The problem was eventually resolved by providing a custom configured `org.apache.hc.core5.http.protocol.HttpContext`:

-   1\. Create a (Spring) factory for HttpContexts:
    

_Java-only: custom `HttpContext` factory for preemptive basic authentication_

```java
public class HttpContextFactory {

  private String httpHost = "localhost";
  private String httpPort = 9001;
  private String user = "some-user";
  private String password = "my-secret";

  private HttpClientContext context = HttpClientContext.create();
  private BasicAuthCache authCache = new BasicAuthCache();
  private BasicScheme basicAuth = new BasicScheme();

  public HttpContext getObject() {
    UsernamePasswordCredentials credentials = new UsernamePasswordCredentials(user, password.toCharArray());
    BasicCredentialsProvider provider = new BasicCredentialsProvider();
    HttpHost host = new HttpHost(httpHost, httpPort);
    provider.setCredentials(host, credentials);

    authCache.put(host, basicAuth);

    httpContext.setAuthCache(authCache);
    httpContext.setCredentialsProvider(provider);

    return httpContext;
  }

  // getter and setter
}
```

-   2\. Declare an\` HttpContext\` in the Spring application context file:
    

```xml
<bean id="myHttpContext" factory-bean="httpContextFactory" factory-method="getObject"/>
```

-   3\. Reference the context in the http URL:
    

```xml
<to uri="https://myhostname.com:443/myURL?httpContext=myHttpContext"/>
```

Using different SSLContextParameters

The [HTTP](#) component only supports one instance of `org.apache.camel.support.jsse.SSLContextParameters` per component. If you need to use two or more different instances, then you need to set up multiple [HTTP](#) components as shown below. Where we have two components, each using their own instance of `sslContextParameters` property.

```xml
<bean id="http-foo" class="org.apache.camel.component.http.HttpComponent">
   <property name="sslContextParameters" ref="sslContextParams1"/>
   <property name="x509HostnameVerifier" ref="hostnameVerifier"/>
</bean>

<bean id="http-bar" class="org.apache.camel.component.http.HttpComponent">
   <property name="sslContextParameters" ref="sslContextParams2"/>
   <property name="x509HostnameVerifier" ref="hostnameVerifier"/>
</bean>
```

## Removing http protocol headers in the Camel Message

In camel there are a number of components that use the http protocol headers to do their business.

The components include camel-http, camel-jetty, camel-cxf, etc.

If you are using these component, you may pay attention to the HTTP protocol headers:

```text
  Exchange.CONTENT_ENCODING
  Exchange.CONTENT_TYPE
  Exchange.HTTP_BASE_URI
  Exchange.HTTP_CHARACTER_ENCODING
  Exchange.HTTP_METHOD
  Exchange.HTTP_PATH
  Exchange.HTTP_QUERY
  Exchange.HTTP_RESPONSE_CODE
```

If you don’t want these headers to bother your other endpoints, you can remove these headers using [Remove Headers](eips/removeHeaders-eip.md) EIP as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jetty://http://myhost:9000/myservice/")
  .removeHeaders("CamelHttp*")
  .to("otherEndpoint");
```

```xml
<route>
  <from uri="jetty://http://myhost:9000/myservice/"/>
  <removeHeaders pattern="CamelHttp*" />
  <to uri="otherEndpoint"/>
</route>
```

```yaml
- route:
    from:
      uri: jetty://http://myhost:9000/myservice/
      steps:
        - removeHeaders:
            pattern: "CamelHttp*"
        - to:
            uri: otherEndpoint
```

## Spring Boot Auto-Configuration

When using http with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-http-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 53 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.http.allow-java-serialized-object** | Whether to allow java serialization when a request uses context-type=application/x-java-serialized-object. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | Boolean |
| **camel.component.http.auth-caching-disabled** | Disables authentication scheme caching. | false | Boolean |
| **camel.component.http.automatic-retries-disabled** | Disables automatic request recovery and re-execution. This is useful when a server responds with HTTP 429 (Too Many Requests) and includes a long Retry-After header, which would otherwise cause the client to wait (and appear to hang) before retrying. | false | Boolean |
| **camel.component.http.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.http.client-connection-manager** | To use a custom and shared HttpClientConnectionManager to manage connections. If this has been configured then this is always used for all endpoints created by this component. The option is a org.apache.hc.client5.http.io.HttpClientConnectionManager type. |  | HttpClientConnectionManager |
| **camel.component.http.connect-timeout** | Determines the timeout (in millis) until a new connection is fully established. A timeout value of zero is interpreted as an infinite timeout. | 180000 | Long |
| **camel.component.http.connection-request-timeout** | Returns the connection lease request timeout (in millis) used when requesting a connection from the connection manager. A timeout value of zero is interpreted as a disabled timeout. | 180000 | Long |
| **camel.component.http.connection-state-disabled** | Disables connection state tracking. | false | Boolean |
| **camel.component.http.connection-time-to-live** | The time for connection to live, the time unit is millisecond, the default value is always keepAlive. |  | Long |
| **camel.component.http.connections-per-route** | The maximum number of connections per route. | 20 | Integer |
| **camel.component.http.content-compression-disabled** | Disables automatic content decompression. | false | Boolean |
| **camel.component.http.content-type-charset-enabled** | Whether the Content-Type header should automatic include charset for string based content. | true | Boolean |
| **camel.component.http.cookie-management-disabled** | Disables state (cookie) management. | false | Boolean |
| **camel.component.http.cookie-store** | To use a custom org.apache.hc.client5.http.cookie.CookieStore. By default the org.apache.hc.client5.http.cookie.BasicCookieStore is used which is an in-memory only cookie store. Notice if bridgeEndpoint=true then the cookie store is forced to be a noop cookie store as cookie shouldn’t be stored as we are just bridging (eg acting as a proxy). The option is a org.apache.hc.client5.http.cookie.CookieStore type. |  | CookieStore |
| **camel.component.http.copy-headers** | If this option is true then IN exchange headers will be copied to OUT exchange headers according to copy strategy. Setting this to false, allows to only include the headers from the HTTP response (not propagating IN headers). | true | Boolean |
| **camel.component.http.default-user-agent-disabled** | Disables the default user agent set by this builder if none has been provided by the user. | false | Boolean |
| **camel.component.http.enabled** | Whether to enable auto configuration of the http component. This is enabled by default. |  | Boolean |
| **camel.component.http.follow-redirects** | Whether to the HTTP request should follow redirects. By default the HTTP request does not follow redirects. | false | Boolean |
| **camel.component.http.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.http.hostname-verification-policy** | Controls how hostname verification is performed during the TLS handshake. CLIENT (default) delegates entirely to the configured x509HostnameVerifier, preserving the behaviour of httpclient 5.5 and earlier a NoopHostnameVerifier will disable verification. BUILTIN uses the JDK SSLParameters hostname check only, ignoring the configured verifier. BOTH runs the JDK built-in check first and then the configured verifier; a NoopHostnameVerifier cannot bypass the built-in check under BUILTIN or BOTH. Prefer BOTH when no custom verifier semantics are needed for stronger out-of-the-box security. | client | HostnameVerificationPolicy |
| **camel.component.http.http-activity-listener** | To use a custom activity listener. The option is a org.apache.camel.component.http.HttpActivityListener type. |  | HttpActivityListener |
| **camel.component.http.http-binding** | To use a custom HttpBinding to control the mapping between Camel message and HttpClient. The option is a org.apache.camel.http.common.HttpBinding type. |  | HttpBinding |
| **camel.component.http.http-client-configurer** | To use the custom HttpClientConfigurer to perform configuration of the HttpClient that will be used. The option is a org.apache.camel.component.http.HttpClientConfigurer type. |  | HttpClientConfigurer |
| **camel.component.http.http-configuration** | To use the shared HttpConfiguration as base configuration. The option is a org.apache.camel.http.common.HttpConfiguration type. |  | HttpConfiguration |
| **camel.component.http.http-context** | To use a custom org.apache.hc.core5.http.protocol.HttpContext when executing requests. The option is a org.apache.hc.core5.http.protocol.HttpContext type. |  | HttpContext |
| **camel.component.http.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.http.log-http-activity** | To enable logging HTTP request and response. You can use a custom LoggingHttpActivityListener as httpActivityListener to control logging options. | false | Boolean |
| **camel.component.http.max-total-connections** | The maximum number of connections. | 200 | Integer |
| **camel.component.http.non-proxy-hosts** | Comma-separated list of hosts that should bypass the proxy. Supports wildcards, e.g., localhost,.example.com,192.168.. |  | String |
| **camel.component.http.proxy-auth-domain** | Proxy authentication domain to use with NTLM. |  | String |
| **camel.component.http.proxy-auth-method** | Proxy authentication method to use (NTLM is deprecated). |  | String |
| **camel.component.http.proxy-auth-nt-host** | Proxy authentication domain (workstation name) to use with NTLM (NTLM is deprecated). |  | String |
| **camel.component.http.proxy-auth-password** | Proxy server password. |  | String |
| **camel.component.http.proxy-auth-scheme** | Proxy server authentication protocol scheme to use. |  | String |
| **camel.component.http.proxy-auth-username** | Proxy server username. |  | String |
| **camel.component.http.proxy-host** | Proxy server host. |  | String |
| **camel.component.http.proxy-port** | Proxy server port. |  | Integer |
| **camel.component.http.redirect-handling-disabled** | Disables automatic redirect handling. | false | Boolean |
| **camel.component.http.response-payload-streaming-threshold** | This threshold in bytes controls whether the response payload should be stored in memory as a byte array or be streaming based. Set this to -1 to always use streaming mode. | 8192 | Integer |
| **camel.component.http.response-timeout** | Determines the timeout (in millis) until arrival of a response from the opposite endpoint. A timeout value of zero is interpreted as an infinite timeout. Please note that response timeout may be unsupported by HTTP transports with message multiplexing. |  | Long |
| **camel.component.http.skip-control-headers** | Whether to skip Camel control headers (CamelHttp…​ headers) to influence this endpoint. Control headers from previous HTTP components can influence how this Camel component behaves such as CamelHttpPath, CamelHttpQuery, etc. | false | Boolean |
| **camel.component.http.skip-request-headers** | Whether to skip mapping all the Camel headers as HTTP request headers. This is useful when you know that calling the HTTP service should not include any custom headers. | false | Boolean |
| **camel.component.http.skip-response-headers** | Whether to skip mapping all the HTTP response headers to Camel headers. | false | Boolean |
| **camel.component.http.so-timeout** | Determines the default socket timeout (in millis) value for blocking I/O operations. | 180000 | Long |
| **camel.component.http.ssl-bundle** | The name of the Spring Boot SSL bundle to use for configuring SSL on the HTTP component. When set, the SSL bundle’s trust material and key material will be used to create the SSLContext for HTTPS connections. |  | String |
| **camel.component.http.ssl-bundle-hot-reload** | Whether to enable hot-reload of SSL certificates when the SSL bundle is updated. When enabled, certificate changes trigger recreation of the connection manager so new connections use the updated certificates. Requires the SSL bundle to have reload-on-update enabled in Spring Boot configuration. | false | Boolean |
| **camel.component.http.ssl-context-parameters** | To configure security using SSLContextParameters. Important: Only one instance of org.apache.camel.support.jsse.SSLContextParameters is supported per HttpComponent. If you need to use 2 or more different instances, you need to define a new HttpComponent per instance you need. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.http.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.http.use-system-properties** | To use System Properties as fallback for configuration for configuring HTTP Client. | false | Boolean |
| **camel.component.http.user-agent** | To set a custom HTTP User-Agent request header. |  | String |
| **camel.component.http.x509-hostname-verifier** | To use a custom X509HostnameVerifier such as DefaultHostnameVerifier or NoopHostnameVerifier. The option is a javax.net.ssl.HostnameVerifier type. |  | HostnameVerifier |
| **camel.component.http.proxy-auth-host** | **Deprecated** Proxy server host. |  | String |
| **camel.component.http.proxy-auth-port** | **Deprecated** Proxy server port. |  | Integer |