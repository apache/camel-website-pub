# camel-https-kafka-connector sink configuration

Connector Description: Send requests to external HTTP servers using Apache HTTP Client 5.x.

When using camel-https-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-https-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.https.CamelHttpsSinkConnector
```

The camel-https sink connector supports 116 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.sink.path.httpUri** | **Required** The url of the HTTP endpoint to call. |  | HIGH |
| **camel.sink.endpoint.disableStreamCache** | Determines whether or not the raw input stream is cached or not. The Camel consumer (camel-servlet, camel-jetty etc.) will by default cache the input stream to support reading it multiple times to ensure it Camel can retrieve all data from the stream. However you can set this option to true when you for example need to access the raw stream, such as streaming it directly to a file or other persistent store. DefaultHttpBinding will copy the request input stream into a stream cache and put it into message body if this option is false to support reading the stream multiple times. If you use Servlet to bridge/proxy an endpoint then consider enabling this option to improve performance, in case you do not need to read the message payload multiple times. The producer (camel-http) will by default cache the response body stream. If setting this option to true, then the producers will not cache the response body stream but use the response stream as-is (the stream can only be read once) as the message body. | false | MEDIUM |
| **camel.sink.endpoint.headerFilterStrategy** | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | MEDIUM |
| **camel.sink.endpoint.bridgeEndpoint** | If the option is true, HttpProducer will ignore the Exchange.HTTP\_URI header, and use the endpoint’s URI for request. You may also set the option throwExceptionOnFailure to be false to let the HttpProducer send all the fault response back. | false | MEDIUM |
| **camel.sink.endpoint.connectionClose** | Specifies whether a Connection Close header must be added to HTTP Request. By default connectionClose is false. | false | MEDIUM |
| **camel.sink.endpoint.httpMethod** | 
Configure the HTTP method to use. The HttpMethod header cannot override this option if set. One of: \[GET\] \[POST\] \[PUT\] \[DELETE\] \[HEAD\] \[OPTIONS\] \[TRACE\] \[PATCH\].

Enum values:

-   GET
    
-   POST
    
-   PUT
    
-   DELETE
    
-   HEAD
    
-   OPTIONS
    
-   TRACE
    
-   PATCH
    





 |  | MEDIUM |
| **camel.sink.endpoint.logHttpActivity** | To enable logging HTTP request and response. You can use a custom LoggingHttpActivityListener as httpActivityListener to control logging options. | false | MEDIUM |
| **camel.sink.endpoint.multipartUpload** | Whether to force using multipart/form-data for easy file uploads. This is only to be used for uploading the message body as a single entity form-data. For uploading multiple entries then use org.apache.hc.client5.http.entity.mime.MultipartEntityBuilder to build the form. | false | MEDIUM |
| **camel.sink.endpoint.multipartUploadName** | The name of the multipart/form-data when multipartUpload is enabled. | "data" | MEDIUM |
| **camel.sink.endpoint.skipControlHeaders** | Whether to skip Camel control headers (CamelHttp…​ headers) to influence this endpoint. Control headers from previous HTTP components can influence how this Camel component behaves such as CamelHttpPath, CamelHttpQuery, etc. | false | MEDIUM |
| **camel.sink.endpoint.skipRequestHeaders** | Whether to skip mapping the Camel headers as HTTP request headers. This is useful when you know that calling the HTTP service should not include any custom headers. | false | MEDIUM |
| **camel.sink.endpoint.skipResponseHeaders** | Whether to skip mapping all the HTTP response headers to Camel headers. | false | MEDIUM |
| **camel.sink.endpoint.throwExceptionOnFailure** | Option to disable throwing the HttpOperationFailedException in case of failed responses from the remote server. This allows you to get all responses regardless of the HTTP status code. | true | MEDIUM |
| **camel.sink.endpoint.clearExpiredCookies** | Whether to clear expired cookies before sending the HTTP request. This ensures the cookies store does not keep growing by adding new cookies which is newer removed when they are expired. If the component has disabled cookie management then this option is disabled too. | true | MEDIUM |
| **camel.sink.endpoint.contentTypeCharsetEnabled** | Whether the Content-Type header should automatic include charset for string based content. | true | MEDIUM |
| **camel.sink.endpoint.cookieHandler** | Configure a cookie handler to maintain a HTTP session. |  | MEDIUM |
| **camel.sink.endpoint.cookieStore** | To use a custom CookieStore. By default the BasicCookieStore is used which is an in-memory only cookie store. Notice if bridgeEndpoint=true then the cookie store is forced to be a noop cookie store as cookie shouldn’t be stored as we are just bridging (eg acting as a proxy). If a cookieHandler is set then the cookie store is also forced to be a noop cookie store as cookie handling is then performed by the cookieHandler. |  | MEDIUM |
| **camel.sink.endpoint.copyHeaders** | If this option is true then IN exchange headers will be copied to OUT exchange headers according to copy strategy. Setting this to false, allows to only include the headers from the HTTP response (not propagating IN headers). | true | MEDIUM |
| **camel.sink.endpoint.customHostHeader** | To use custom host header for producer. When not set in query will be ignored. When set will override host header derived from url. |  | MEDIUM |
| **camel.sink.endpoint.deleteWithBody** | Whether the HTTP DELETE should include the message body or not. By default HTTP DELETE do not include any HTTP body. However in some rare cases users may need to be able to include the message body. | false | MEDIUM |
| **camel.sink.endpoint.followRedirects** | Whether to the HTTP request should follow redirects. By default the HTTP request does not follow redirects. | false | MEDIUM |
| **camel.sink.endpoint.getWithBody** | Whether the HTTP GET should include the message body or not. By default HTTP GET do not include any HTTP body. However in some rare cases users may need to be able to include the message body. | false | MEDIUM |
| **camel.sink.endpoint.httpActivityListener** | To use a custom activity listener. |  | MEDIUM |
| **camel.sink.endpoint.ignoreResponseBody** | If this option is true, The http producer won’t read response body and cache the input stream. | false | MEDIUM |
| **camel.sink.endpoint.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.sink.endpoint.okStatusCodeRange** | The status codes which are considered a success response. The values are inclusive. Multiple ranges can be defined, separated by comma, e.g. 200-204,209,301-304. Each range must be a single number or from-to with the dash included. | "200-299" | MEDIUM |
| **camel.sink.endpoint.preserveHostHeader** | If the option is true, HttpProducer will set the Host header to the value contained in the current exchange Host header, useful in reverse proxy applications where you want the Host header received by the downstream server to reflect the URL called by the upstream client, this allows applications which use the Host header to generate accurate URL’s for a proxied service. | false | MEDIUM |
| **camel.sink.endpoint.userAgent** | To set a custom HTTP User-Agent request header. |  | MEDIUM |
| **camel.sink.endpoint.clientBuilder** | Provide access to the http client request parameters used on new RequestConfig instances used by producers or consumers of this endpoint. |  | MEDIUM |
| **camel.sink.endpoint.clientConnectionManager** | To use a custom HttpClientConnectionManager to manage connections. |  | MEDIUM |
| **camel.sink.endpoint.connectionsPerRoute** | The maximum number of connections per route. | 20 | MEDIUM |
| **camel.sink.endpoint.httpClient** | Sets a custom HttpClient to be used by the producer. |  | MEDIUM |
| **camel.sink.endpoint.httpClientConfigurer** | Register a custom configuration strategy for new HttpClient instances created by producers or consumers such as to configure authentication mechanisms etc. |  | MEDIUM |
| **camel.sink.endpoint.httpClientOptions** | To configure the HttpClient using the key/values from the Map. This is a multi-value option with prefix: httpClient. |  | MEDIUM |
| **camel.sink.endpoint.httpConnectionOptions** | To configure the connection and the socket using the key/values from the Map. This is a multi-value option with prefix: httpConnection. |  | MEDIUM |
| **camel.sink.endpoint.httpContext** | To use a custom HttpContext instance. |  | MEDIUM |
| **camel.sink.endpoint.maxTotalConnections** | The maximum number of connections. | 200 | MEDIUM |
| **camel.sink.endpoint.useSystemProperties** | To use System Properties as fallback for configuration for configuring HTTP Client. | false | MEDIUM |
| **camel.sink.endpoint.nonProxyHosts** | Comma-separated list of hosts that should bypass the proxy. Supports wildcards, e.g., localhost,.example.com,192.168.. |  | MEDIUM |
| **camel.sink.endpoint.proxyAuthDomain** | Proxy authentication domain to use with NTLM. |  | LOW |
| **camel.sink.endpoint.proxyAuthHost** | Proxy server host. |  | LOW |
| **camel.sink.endpoint.proxyAuthMethod** | 

Proxy authentication method to use (NTLM is deprecated) One of: \[Basic\] \[Bearer\] \[NTLM\].

Enum values:

-   Basic
    
-   Bearer
    
-   NTLM
    





 |  | MEDIUM |
| **camel.sink.endpoint.proxyAuthNtHost** | Proxy authentication domain (workstation name) to use with NTLM. |  | LOW |
| **camel.sink.endpoint.proxyAuthPassword** | Proxy server password. |  | MEDIUM |
| **camel.sink.endpoint.proxyAuthPort** | Proxy server port. |  | LOW |
| **camel.sink.endpoint.proxyAuthScheme** | 

Proxy server authentication protocol scheme to use One of: \[http\] \[https\].

Enum values:

-   http
    
-   https
    





 |  | MEDIUM |
| **camel.sink.endpoint.proxyAuthUsername** | Proxy server username. |  | MEDIUM |
| **camel.sink.endpoint.proxyHost** | Proxy server host. |  | MEDIUM |
| **camel.sink.endpoint.proxyPort** | Proxy server port. |  | MEDIUM |
| **camel.sink.endpoint.authBearerToken** | Authentication bearer token. |  | MEDIUM |
| **camel.sink.endpoint.authDomain** | Authentication domain to use with NTLM. |  | LOW |
| **camel.sink.endpoint.authenticationPreemptive** | If this option is true, camel-http sends preemptive basic authentication to the server. | false | MEDIUM |
| **camel.sink.endpoint.authHost** | Authentication host to use with NTLM. |  | LOW |
| **camel.sink.endpoint.authMethod** | 

Authentication methods allowed to use as a comma separated list of values Basic, Bearer, or NTLM. (NTLM is deprecated) One of: \[Basic\] \[Bearer\] \[NTLM\].

Enum values:

-   Basic
    
-   Bearer
    
-   NTLM
    





 |  | MEDIUM |
| **camel.sink.endpoint.authPassword** | Authentication password. |  | MEDIUM |
| **camel.sink.endpoint.authUsername** | Authentication username. |  | MEDIUM |
| **camel.sink.endpoint.oauth2BodyAuthentication** | Whether to use OAuth2 body authentication. | false | MEDIUM |
| **camel.sink.endpoint.oauth2CachedTokensDefaultExpirySeconds** | Default expiration time for cached OAuth2 tokens, in seconds. Used if token response does not contain 'expires\_in' field. | 3600L | MEDIUM |
| **camel.sink.endpoint.oauth2CachedTokensExpirationMarginSeconds** | Amount of time which is deducted from OAuth2 tokens expiry time to compensate for the time it takes OAuth2 Token Endpoint to send the token over http, in seconds. Set this parameter to high value if you OAuth2 Token Endpoint answers slowly or you tokens expire quickly. If you set this parameter to too small value, you can get 4xx http errors because camel will think that the received token is still valid, while in reality the token is expired for the Authentication server. | 5L | MEDIUM |
| **camel.sink.endpoint.oauth2CacheTokens** | Whether to cache OAuth2 client tokens. | false | MEDIUM |
| **camel.sink.endpoint.oauth2ClientId** | OAuth2 client id. |  | MEDIUM |
| **camel.sink.endpoint.oauth2ClientSecret** | OAuth2 client secret. |  | MEDIUM |
| **camel.sink.endpoint.oauth2ResourceIndicator** | OAuth2 Token endpoint. |  | MEDIUM |
| **camel.sink.endpoint.oauth2Scope** | OAuth2 scope. |  | MEDIUM |
| **camel.sink.endpoint.oauth2TokenEndpoint** | OAuth2 Resource Indicator. |  | MEDIUM |
| **camel.sink.endpoint.sslContextParameters** | To configure security using SSLContextParameters. Important: Only one instance of org.apache.camel.util.jsse.SSLContextParameters is supported per HttpComponent. If you need to use 2 or more different instances, you need to define a new HttpComponent per instance you need. |  | MEDIUM |
| **camel.sink.endpoint.x509HostnameVerifier** | To use a custom X509HostnameVerifier such as DefaultHostnameVerifier or NoopHostnameVerifier. |  | MEDIUM |
| **camel.component.https.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.component.https.logHttpActivity** | To enable logging HTTP request and response. You can use a custom LoggingHttpActivityListener as httpActivityListener to control logging options. | false | MEDIUM |
| **camel.component.https.skipControlHeaders** | Whether to skip Camel control headers (CamelHttp…​ headers) to influence this endpoint. Control headers from previous HTTP components can influence how this Camel component behaves such as CamelHttpPath, CamelHttpQuery, etc. | false | MEDIUM |
| **camel.component.https.skipRequestHeaders** | Whether to skip mapping all the Camel headers as HTTP request headers. This is useful when you know that calling the HTTP service should not include any custom headers. | false | MEDIUM |
| **camel.component.https.skipResponseHeaders** | Whether to skip mapping all the HTTP response headers to Camel headers. | false | MEDIUM |
| **camel.component.https.contentTypeCharsetEnabled** | Whether the Content-Type header should automatic include charset for string based content. | true | MEDIUM |
| **camel.component.https.cookieStore** | To use a custom org.apache.hc.client5.http.cookie.CookieStore. By default the org.apache.hc.client5.http.cookie.BasicCookieStore is used which is an in-memory only cookie store. Notice if bridgeEndpoint=true then the cookie store is forced to be a noop cookie store as cookie shouldn’t be stored as we are just bridging (eg acting as a proxy). |  | MEDIUM |
| **camel.component.https.copyHeaders** | If this option is true then IN exchange headers will be copied to OUT exchange headers according to copy strategy. Setting this to false, allows to only include the headers from the HTTP response (not propagating IN headers). | true | MEDIUM |
| **camel.component.https.followRedirects** | Whether to the HTTP request should follow redirects. By default the HTTP request does not follow redirects. | false | MEDIUM |
| **camel.component.https.httpActivityListener** | To use a custom activity listener. |  | MEDIUM |
| **camel.component.https.responsePayloadStreamingThreshold** | This threshold in bytes controls whether the response payload should be stored in memory as a byte array or be streaming based. Set this to -1 to always use streaming mode. | 8192 | MEDIUM |
| **camel.component.https.userAgent** | To set a custom HTTP User-Agent request header. |  | MEDIUM |
| **camel.component.https.allowJavaSerializedObject** | Whether to allow java serialization when a request uses context-type=application/x-java-serialized-object. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | MEDIUM |
| **camel.component.https.authCachingDisabled** | Disables authentication scheme caching. | false | MEDIUM |
| **camel.component.https.automaticRetriesDisabled** | Disables automatic request recovery and re-execution. | false | MEDIUM |
| **camel.component.https.autowiredEnabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | MEDIUM |
| **camel.component.https.clientConnectionManager** | To use a custom and shared HttpClientConnectionManager to manage connections. If this has been configured then this is always used for all endpoints created by this component. |  | MEDIUM |
| **camel.component.https.connectionsPerRoute** | The maximum number of connections per route. | 20 | MEDIUM |
| **camel.component.https.connectionStateDisabled** | Disables connection state tracking. | false | MEDIUM |
| **camel.component.https.connectionTimeToLive** | The time for connection to live, the time unit is millisecond, the default value is always keepAlive. |  | MEDIUM |
| **camel.component.https.contentCompressionDisabled** | Disables automatic content decompression. | false | MEDIUM |
| **camel.component.https.cookieManagementDisabled** | Disables state (cookie) management. | false | MEDIUM |
| **camel.component.https.defaultUserAgentDisabled** | Disables the default user agent set by this builder if none has been provided by the user. | false | MEDIUM |
| **camel.component.https.httpBinding** | To use a custom HttpBinding to control the mapping between Camel message and HttpClient. |  | MEDIUM |
| **camel.component.https.httpClientConfigurer** | To use the custom HttpClientConfigurer to perform configuration of the HttpClient that will be used. |  | MEDIUM |
| **camel.component.https.httpConfiguration** | To use the shared HttpConfiguration as base configuration. |  | MEDIUM |
| **camel.component.https.httpContext** | To use a custom org.apache.hc.core5.http.protocol.HttpContext when executing requests. |  | MEDIUM |
| **camel.component.https.maxTotalConnections** | The maximum number of connections. | 200 | MEDIUM |
| **camel.component.https.redirectHandlingDisabled** | Disables automatic redirect handling. | false | MEDIUM |
| **camel.component.https.useSystemProperties** | To use System Properties as fallback for configuration for configuring HTTP Client. | false | MEDIUM |
| **camel.component.https.headerFilterStrategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | MEDIUM |
| **camel.component.https.nonProxyHosts** | Comma-separated list of hosts that should bypass the proxy. Supports wildcards, e.g., localhost,.example.com,192.168.. |  | MEDIUM |
| **camel.component.https.proxyAuthDomain** | Proxy authentication domain to use with NTLM. |  | MEDIUM |
| **camel.component.https.proxyAuthHost** | Proxy server host. |  | LOW |
| **camel.component.https.proxyAuthMethod** | 

Proxy authentication method to use (NTLM is deprecated) One of: \[Basic\] \[Digest\] \[NTLM\].

Enum values:

-   Basic
    
-   Digest
    
-   NTLM
    





 |  | MEDIUM |
| **camel.component.https.proxyAuthNtHost** | Proxy authentication domain (workstation name) to use with NTLM (NTLM is deprecated). |  | MEDIUM |
| **camel.component.https.proxyAuthPassword** | Proxy server password. |  | MEDIUM |
| **camel.component.https.proxyAuthPort** | Proxy server port. |  | LOW |
| **camel.component.https.proxyAuthScheme** | 

Proxy server authentication protocol scheme to use One of: \[http\] \[https\].

Enum values:

-   http
    
-   https
    





 |  | MEDIUM |
| **camel.component.https.proxyAuthUsername** | Proxy server username. |  | MEDIUM |
| **camel.component.https.proxyHost** | Proxy server host. |  | MEDIUM |
| **camel.component.https.proxyPort** | Proxy server port. |  | MEDIUM |
| **camel.component.https.sslContextParameters** | To configure security using SSLContextParameters. Important: Only one instance of org.apache.camel.support.jsse.SSLContextParameters is supported per HttpComponent. If you need to use 2 or more different instances, you need to define a new HttpComponent per instance you need. |  | MEDIUM |
| **camel.component.https.useGlobalSslContextParameters** | Enable usage of global SSL context parameters. | false | MEDIUM |
| **camel.component.https.x509HostnameVerifier** | To use a custom X509HostnameVerifier such as DefaultHostnameVerifier or NoopHostnameVerifier. |  | MEDIUM |
| **camel.component.https.connectionRequestTimeout** | Returns the connection lease request timeout (in millis) used when requesting a connection from the connection manager. A timeout value of zero is interpreted as a disabled timeout. | 180000L | MEDIUM |
| **camel.component.https.connectTimeout** | Determines the timeout (in millis) until a new connection is fully established. A timeout value of zero is interpreted as an infinite timeout. | 180000L | MEDIUM |
| **camel.component.https.responseTimeout** | Determines the timeout (in millis) until arrival of a response from the opposite endpoint. A timeout value of zero is interpreted as an infinite timeout. Please note that response timeout may be unsupported by HTTP transports with message multiplexing. |  | MEDIUM |
| **camel.component.https.soTimeout** | Determines the default socket timeout (in millis) value for blocking I/O operations. | 180000L | MEDIUM |

The camel-https sink connector has no converters out of the box.

The camel-https sink connector has no transforms out of the box.

The camel-https sink connector has no aggregation strategies out of the box.