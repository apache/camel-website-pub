# Netty HTTP

**Since Camel 2.14**

**Both producer and consumer are supported**

The Netty HTTP component is an extension to [Netty](netty-component.md) component to simplify HTTP transport with [Netty](netty-component.md).

> **Note**
> **Stream**
>
> Netty is stream-based, which means the input it receives is submitted to Camel as a stream. That means you will only be able to read the content of the stream **once**. If you find a situation where the message body appears to be empty, or you need to access the data multiple times (eg: doing multicasting, or redelivery error handling), you should use Stream caching or convert the message body to a `String` which is safe to be re-read multiple times.
>
> Note also that Netty HTTP reads the entire stream into memory using `io.netty.handler.codec.http.HttpObjectAggregator` to build the entire full http message. But the resulting message is still a stream-based message that is readable once.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-netty-http</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

The URI scheme for a netty component is as follows

netty-http:http://0.0.0.0:8080\[?options\]

> **Note**
> **Query parameters vs. endpoint options**
>
> You may be wondering how Camel recognizes URI query parameters and endpoint options. For example, you might create endpoint URI as follows: `netty-http:http//example.com?myParam=myValue&compression=true` . In this example `myParam` is the HTTP parameter, while `compression` is the Camel endpoint option. The strategy used by Camel in such situations is to resolve available endpoint options and remove them from the URI. It means that for the discussed example, the HTTP request sent by Netty HTTP producer to the endpoint will look as follows: `http//example.com?myParam=myValue`, because `compression` endpoint option will be resolved and removed from the target URL.
>
> Keep also in mind that you cannot specify endpoint options using dynamic headers (like `CamelHttpQuery`). Endpoint options can be specified only at the endpoint URI definition level (like `to` or `from` DSL elements).

> **Important**
> **A lot more options**
>
> This component inherits all the options from [Netty](netty-component.md), so make sure to look at the [Netty](netty-component.md) documentation as well. Notice that some options from [Netty](netty-component.md) are not applicable when using this Netty HTTP component, such as options related to UDP transport.

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

The Netty HTTP component supports 79 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | To use the NettyConfiguration as configuration when creating endpoints. |  | NettyConfiguration |
| **disconnect** (common) | Whether or not to disconnect(close) from Netty Channel right after use. | false | boolean |
| **keepAlive** (common) | Setting to ensure socket is not closed due to inactivity. | true | boolean |
| **reuseAddress** (common) | Setting to facilitate socket multiplexing. | true | boolean |
| **reuseChannel** (common) | This option allows producers and consumers (in client mode) to reuse the same Netty Channel for the lifecycle of processing the Exchange. This is useful if you need to call a server multiple times in a Camel route and want to use the same network connection. When using this, the channel is not returned to the connection pool until the Exchange is done; or disconnected if the disconnect option is set to true. The reused Channel is stored on the Exchange as an exchange property with the key CamelNettyChannel which allows you to obtain the channel during routing and use it as well. | false | boolean |
| **sync** (common) | Setting to set endpoint as one-way (false) or request-response (true). | true | boolean |
| **tcpNoDelay** (common) | Setting to improve TCP protocol performance. | true | boolean |
| **networkInterface** (common (advanced)) | When using UDP then this option can be used to specify a network interface by its name, such as eth0 to join a multicast group. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **clientMode** (consumer) | If the clientMode is true, netty consumer will connect the address as a TCP client. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | boolean |
| **reconnect** (consumer) | Used only in clientMode in consumer, the consumer will attempt to reconnect on disconnection if this is enabled. | true | boolean |
| **reconnectInterval** (consumer) | Used if reconnect and clientMode is enabled. The interval in milli seconds to attempt reconnection. | 10000 | int |
| **backlog** (consumer (advanced)) | Allows to configure a backlog for netty consumer (server). Note the backlog is just a best effort depending on the OS. Setting this option to a value such as 200, 500 or 1000, tells the TCP stack how long the accept queue can be If this option is not configured, then the backlog depends on OS setting. |  | int |
| **bossCount** (consumer (advanced)) | When netty works on nio mode, it uses default bossCount parameter from Netty, which is 1. User can use this option to override the default bossCount from Netty. | 1 | int |
| **bossGroup** (consumer (advanced)) | Set the BossGroup which could be used for handling the new connection of the server side across the NettyEndpoint. |  | EventLoopGroup |
| **broadcast** (consumer (advanced)) | Setting to choose Multicast over UDP. | false | boolean |
| **disconnectOnNoReply** (consumer (advanced)) | If sync is enabled then this option dictates NettyConsumer if it should disconnect where there is no reply to send back. | true | boolean |
| **executorService** (consumer (advanced)) | To use the given custom EventExecutorGroup. |  | EventExecutorGroup |
| **maximumPoolSize** (consumer (advanced)) | Sets a maximum thread pool size for the netty consumer ordered thread pool. The default size is 2 x cpu\_core plus 1. Setting this value to eg 10 will then use 10 threads unless 2 x cpu\_core plus 1 is a higher value, which then will override and be used. For example if there are 8 cores, then the consumer thread pool will be 17. This thread pool is used to route messages received from Netty by Camel. We use a separate thread pool to ensure ordering of messages and also in case some messages will block, then nettys worker threads (event loop) wont be affected. |  | int |
| **nettyServerBootstrapFactory** (consumer (advanced)) | To use a custom NettyServerBootstrapFactory. |  | NettyServerBootstrapFactory |
| **noReplyLogLevel** (consumer (advanced)) | 
If sync is enabled this option dictates NettyConsumer which logging level to use when logging a there is no reply to send back.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | WARN | LoggingLevel |
| **serverClosedChannelExceptionCaughtLogLevel** (consumer (advanced)) | 

If the server (NettyConsumer) catches an java.nio.channels.ClosedChannelException then its logged using this logging level. This is used to avoid logging the closed channel exceptions, as clients can disconnect abruptly and then cause a flood of closed exceptions in the Netty server.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | DEBUG | LoggingLevel |
| **serverExceptionCaughtLogLevel** (consumer (advanced)) | 

If the server (NettyConsumer) catches an exception then its logged using this logging level.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | WARN | LoggingLevel |
| **serverInitializerFactory** (consumer (advanced)) | To use a custom ServerInitializerFactory. |  | ServerInitializerFactory |
| **usingExecutorService** (consumer (advanced)) | Whether to use ordered thread pool, to ensure events are processed orderly on the same channel. | true | boolean |
| **connectTimeout** (producer) | Time to wait for a socket connection to be available. Value is in milliseconds. | 10000 | int |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **requestTimeout** (producer) | Allows to use a timeout for the Netty producer when calling a remote server. By default no timeout is in use. The value is in milli seconds, so eg 30000 is 30 seconds. The requestTimeout is using Netty’s ReadTimeoutHandler to trigger the timeout. |  | long |
| **clientInitializerFactory** (producer (advanced)) | To use a custom ClientInitializerFactory. |  | ClientInitializerFactory |
| **correlationManager** (producer (advanced)) | To use a custom correlation manager to manage how request and reply messages are mapped when using request/reply with the netty producer. This should only be used if you have a way to map requests together with replies such as if there is correlation ids in both the request and reply messages. This can be used if you want to multiplex concurrent messages on the same channel (aka connection) in netty. When doing this you must have a way to correlate the request and reply messages so you can store the right reply on the inflight Camel Exchange before its continued routed. We recommend extending the TimeoutCorrelationManagerSupport when you build custom correlation managers. This provides support for timeout and other complexities you otherwise would need to implement as well. See also the producerPoolEnabled option for more details. |  | NettyCamelStateCorrelationManager |
| **lazyChannelCreation** (producer (advanced)) | Channels can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | boolean |
| **producerPoolBlockWhenExhausted** (producer (advanced)) | Sets the value for the blockWhenExhausted configuration attribute. It determines whether to block when the borrowObject() method is invoked when the pool is exhausted (the maximum number of active objects has been reached). | true | boolean |
| **producerPoolEnabled** (producer (advanced)) | Whether producer pool is enabled or not. Important: If you turn this off then a single shared connection is used for the producer, also if you are doing request/reply. That means there is a potential issue with interleaved responses if replies comes back out-of-order. Therefore you need to have a correlation id in both the request and reply messages so you can properly correlate the replies to the Camel callback that is responsible for continue processing the message in Camel. To do this you need to implement NettyCamelStateCorrelationManager as correlation manager and configure it via the correlationManager option. See also the correlationManager option for more details. | true | boolean |
| **producerPoolMaxIdle** (producer (advanced)) | Sets the cap on the number of idle instances in the pool. | 100 | int |
| **producerPoolMaxTotal** (producer (advanced)) | Sets the cap on the number of objects that can be allocated by the pool (checked out to clients, or idle awaiting checkout) at a given time. Use a negative value for no limit. Be careful to not set this value too low (such as 1) as the pool must have space to create a producer such as when performing retries. Be mindful that the option producerPoolBlockWhenExhausted is default true, and the pool will then block when there is no space, which can lead to the application to hang. | \-1 | int |
| **producerPoolMaxWait** (producer (advanced)) | Sets the maximum duration (value in millis) the borrowObject() method should block before throwing an exception when the pool is exhausted and producerPoolBlockWhenExhausted is true. When less than 0, the borrowObject() method may block indefinitely. | \-1 | long |
| **producerPoolMinEvictableIdle** (producer (advanced)) | Sets the minimum amount of time (value in millis) an object may sit idle in the pool before it is eligible for eviction by the idle object evictor. | 300000 | long |
| **producerPoolMinIdle** (producer (advanced)) | Sets the minimum number of instances allowed in the producer pool before the evictor thread (if active) spawns new objects. |  | int |
| **udpConnectionlessSending** (producer (advanced)) | This option supports connection less udp sending which is a real fire and forget. A connected udp send receive the PortUnreachableException if no one is listen on the receiving port. | false | boolean |
| **useByteBuf** (producer (advanced)) | If the useByteBuf is true, netty producer will turn the message body into ByteBuf before sending it out. | false | boolean |
| **allowSerializedHeaders** (advanced) | Only used for TCP when transferExchange is true. When set to true, serializable objects in headers and properties will be added to the exchange. Otherwise Camel will exclude any non-serializable objects and log it at WARN level. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **channelGroup** (advanced) | To use an explicit ChannelGroup. |  | ChannelGroup |
| **headerFilterStrategy** (advanced) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter headers. |  | HeaderFilterStrategy |
| **nativeTransport** (advanced) | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | boolean |
| **nettyHttpBinding** (advanced) | To use a custom org.apache.camel.component.netty.http.NettyHttpBinding for binding to/from Netty and Camel Message API. |  | NettyHttpBinding |
| **options** (advanced) | Allows to configure additional netty options using option. as prefix. For example option.child.keepAlive=false. See the Netty documentation for possible options that can be used. This is a multi-value option with prefix: option. |  | Map |
| **receiveBufferSize** (advanced) | The TCP/UDP buffer sizes to be used during inbound communication. Size is bytes. | 65536 | int |
| **receiveBufferSizePredictor** (advanced) | Configures the buffer size predictor. See details at Jetty documentation and this mail thread. |  | int |
| **sendBufferSize** (advanced) | The TCP/UDP buffer sizes to be used during outbound communication. Size is bytes. | 65536 | int |
| **shutdownTimeout** (advanced) | Shutdown await timeout in milliseconds. | 100 | int |
| **transferExchange** (advanced) | Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | boolean |
| **udpByteArrayCodec** (advanced) | For UDP only. If enabled the using byte array codec instead of Java serialization protocol. | false | boolean |
| **unixDomainSocketPath** (advanced) | Path to unix domain socket to use instead of inet socket. Host and port parameters will not be used, however required. It is ok to set dummy values for them. Must be used with nativeTransport=true and clientMode=false. |  | String |
| **workerCount** (advanced) | When netty works on nio mode, it uses default workerCount parameter from Netty (which is cpu\_core\_threads x 2). User can use this option to override the default workerCount from Netty. |  | int |
| **workerGroup** (advanced) | To use a explicit EventLoopGroup as the boss thread pool. For example to share a thread pool with multiple consumers or producers. By default each consumer or producer has their own worker pool with 2 x cpu count core threads. |  | EventLoopGroup |
| **allowDefaultCodec** (codec) | The netty component installs a default codec if both, encoder/decoder is null and textline is false. Setting allowDefaultCodec to false prevents the netty component from installing a default codec as the first element in the filter chain. | true | boolean |
| **autoAppendDelimiter** (codec) | Whether or not to auto append missing end delimiter when sending using the textline codec. | true | boolean |
| **decoderMaxLineLength** (codec) | The max line length to use for the textline codec. | 1024 | int |
| **decoders** (codec) | A list of decoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | String |
| **delimiter** (codec) | 

The delimiter to use for the textline codec. Possible values are LINE and NULL.

Enum values:

-   LINE
    
-   NULL
    





 | LINE | TextLineDelimiter |
| **encoders** (codec) | A list of encoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | String |
| **encoding** (codec) | The encoding (a charset name) to use for the textline codec. If not provided, Camel will use the JVM default Charset. |  | String |
| **textline** (codec) | Only used for TCP. If no codec is specified, you can use this flag to indicate a text line based codec; if not specified or the value is false, then Object Serialization is assumed over TCP - however only Strings are allowed to be serialized by default. | false | boolean |
| **enabledProtocols** (security) | Which protocols to enable when using SSL. | TLSv1.2,TLSv1.3 | String |
| **hostnameVerification** (security) | To enable/disable hostname verification on SSLEngine. | false | boolean |
| **keyStoreFormat** (security) | Keystore format to be used for payload encryption. Defaults to JKS if not set. |  | String |
| **keyStoreResource** (security) | Client side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **needClientAuth** (security) | Configures whether the server needs client authentication when using SSL. | false | boolean |
| **passphrase** (security) | Password to use for the keyStore and trustStore. The same password must be configured for both resources. |  | String |
| **securityConfiguration** (security) | Refers to a org.apache.camel.component.netty.http.NettyHttpSecurityConfiguration for configuring secure web resources. |  | NettyHttpSecurityConfiguration |
| **securityProvider** (security) | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | String |
| **ssl** (security) | Setting to specify whether SSL encryption is applied to this endpoint. | false | boolean |
| **sslClientCertHeaders** (security) | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **sslHandler** (security) | Reference to a class that could be used to return an SSL Handler. |  | SslHandler |
| **trustStoreResource** (security) | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Netty HTTP endpoint is configured using URI syntax:

netty-http:protocol://host:port/path

With the following _path_ and _query_ parameters:

### Path Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **protocol** (common) | 
**Required** The protocol to use which is either http, https or proxy (consumer only).

Enum values:

-   http
    
-   https
    
-   proxy
    





 |  | String |
| **host** (common) | **Required** The local hostname such as localhost, or 0.0.0.0 when being a consumer. The remote HTTP server hostname when using producer. |  | String |
| **port** (common) | The host port number. |  | int |
| **path** (common) | Resource path. |  | String |

### Query Parameters (85 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeEndpoint** (common) | If the option is true, the producer will ignore the NettyHttpConstants.HTTP\_URI header, and use the endpoint’s URI for request. You may also set the throwExceptionOnFailure to be false to let the producer send all the fault response back. The consumer working in the bridge mode will skip the gzip compression and WWW URL form encoding (by adding the Exchange.SKIP\_GZIP\_ENCODING and Exchange.SKIP\_WWW\_FORM\_URLENCODED headers to the consumed exchange). | false | boolean |
| **disconnect** (common) | Whether or not to disconnect(close) from Netty Channel right after use. | false | boolean |
| **keepAlive** (common) | Setting to ensure socket is not closed due to inactivity. | true | boolean |
| **reuseAddress** (common) | Setting to facilitate socket multiplexing. | true | boolean |
| **reuseChannel** (common) | This option allows producers and consumers (in client mode) to reuse the same Netty Channel for the lifecycle of processing the Exchange. This is useful if you need to call a server multiple times in a Camel route and want to use the same network connection. When using this, the channel is not returned to the connection pool until the Exchange is done; or disconnected if the disconnect option is set to true. The reused Channel is stored on the Exchange as an exchange property with the key CamelNettyChannel which allows you to obtain the channel during routing and use it as well. | false | boolean |
| **sync** (common) | Setting to set endpoint as one-way (false) or request-response (true). | true | boolean |
| **tcpNoDelay** (common) | Setting to improve TCP protocol performance. | true | boolean |
| **matchOnUriPrefix** (consumer) | Whether or not Camel should try to find a target consumer by matching the URI prefix if no exact match is found. | false | boolean |
| **muteException** (consumer) | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | boolean |
| **send503whenSuspended** (consumer) | Whether to send back HTTP status code 503 when the consumer has been suspended. If the option is false then the Netty Acceptor is unbound when the consumer is suspended, so clients cannot connect anymore. | true | boolean |
| **backlog** (consumer (advanced)) | Allows to configure a backlog for netty consumer (server). Note the backlog is just a best effort depending on the OS. Setting this option to a value such as 200, 500 or 1000, tells the TCP stack how long the accept queue can be If this option is not configured, then the backlog depends on OS setting. |  | int |
| **bossCount** (consumer (advanced)) | When netty works on nio mode, it uses default bossCount parameter from Netty, which is 1. User can use this option to override the default bossCount from Netty. | 1 | int |
| **bossGroup** (consumer (advanced)) | Set the BossGroup which could be used for handling the new connection of the server side across the NettyEndpoint. |  | EventLoopGroup |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **chunkedMaxContentLength** (consumer (advanced)) | Value in bytes the max content length per chunked frame received on the Netty HTTP server. | 1048576 | int |
| **compression** (consumer (advanced)) | Allow using gzip/deflate for compression on the Netty HTTP server if the client supports it from the HTTP headers. | false | boolean |
| **disconnectOnNoReply** (consumer (advanced)) | If sync is enabled then this option dictates NettyConsumer if it should disconnect where there is no reply to send back. | true | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **httpMethodRestrict** (consumer (advanced)) | To disable HTTP methods on the Netty HTTP consumer. You can specify multiple separated by comma. |  | String |
| **logWarnOnBadRequest** (consumer (advanced)) | Whether Netty HTTP server should log a WARN if decoding the HTTP request failed and a HTTP Status 400 (bad request) is returned. | true | boolean |
| **mapHeaders** (consumer (advanced)) | If this option is enabled, then during binding from Netty to Camel Message then the headers will be mapped as well (eg added as header to the Camel Message as well). You can turn off this option to disable this. The headers can still be accessed from the org.apache.camel.component.netty.http.NettyHttpMessage message with the method getHttpRequest() that returns the Netty HTTP request io.netty.handler.codec.http.HttpRequest instance. | true | boolean |
| **maxChunkSize** (consumer (advanced)) | The maximum length of the content or each chunk. If the content length (or the length of each chunk) exceeds this value, the content or chunk will be split into multiple io.netty.handler.codec.http.HttpContents whose length is maxChunkSize at maximum. See io.netty.handler.codec.http.HttpObjectDecoder. | 8192 | int |
| **maxHeaderSize** (consumer (advanced)) | The maximum length of all headers. If the sum of the length of each header exceeds this value, a io.netty.handler.codec.TooLongFrameException will be raised. | 8192 | int |
| **maxInitialLineLength** (consumer (advanced)) | The maximum length of the initial line (e.g. \\{code GET / HTTP/1.0} or \\{code HTTP/1.0 200 OK}) If the length of the initial line exceeds this value, a TooLongFrameException will be raised. See io.netty.handler.codec.http.HttpObjectDecoder. | 4096 | int |
| **nettyServerBootstrapFactory** (consumer (advanced)) | To use a custom NettyServerBootstrapFactory. |  | NettyServerBootstrapFactory |
| **nettySharedHttpServer** (consumer (advanced)) | To use a shared Netty HTTP server. See Netty HTTP Server Example for more details. |  | NettySharedHttpServer |
| **noReplyLogLevel** (consumer (advanced)) | 

If sync is enabled this option dictates NettyConsumer which logging level to use when logging a there is no reply to send back.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | WARN | LoggingLevel |
| **serverClosedChannelExceptionCaughtLogLevel** (consumer (advanced)) | 

If the server (NettyConsumer) catches an java.nio.channels.ClosedChannelException then its logged using this logging level. This is used to avoid logging the closed channel exceptions, as clients can disconnect abruptly and then cause a flood of closed exceptions in the Netty server.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | DEBUG | LoggingLevel |
| **serverExceptionCaughtLogLevel** (consumer (advanced)) | 

If the server (NettyConsumer) catches an exception then its logged using this logging level.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | WARN | LoggingLevel |
| **serverInitializerFactory** (consumer (advanced)) | To use a custom ServerInitializerFactory. |  | ServerInitializerFactory |
| **traceEnabled** (consumer (advanced)) | Specifies whether to enable HTTP TRACE for this Netty HTTP consumer. By default TRACE is turned off. | false | boolean |
| **urlDecodeHeaders** (consumer (advanced)) | If this option is enabled, then during binding from Netty to Camel Message then the header values will be URL decoded (eg %20 will be a space character. Notice this option is used by the default org.apache.camel.component.netty.http.NettyHttpBinding and therefore if you implement a custom org.apache.camel.component.netty.http.NettyHttpBinding then you would need to decode the headers accordingly to this option. | false | boolean |
| **usingExecutorService** (consumer (advanced)) | Whether to use ordered thread pool, to ensure events are processed orderly on the same channel. | true | boolean |
| **connectTimeout** (producer) | Time to wait for a socket connection to be available. Value is in milliseconds. | 10000 | int |
| **cookieHandler** (producer) | Configure a cookie handler to maintain a HTTP session. |  | CookieHandler |
| **requestTimeout** (producer) | Allows to use a timeout for the Netty producer when calling a remote server. By default no timeout is in use. The value is in milli seconds, so eg 30000 is 30 seconds. The requestTimeout is using Netty’s ReadTimeoutHandler to trigger the timeout. |  | long |
| **throwExceptionOnFailure** (producer) | Option to disable throwing the HttpOperationFailedException in case of failed responses from the remote server. This allows you to get all responses regardless of the HTTP status code. | true | boolean |
| **clientInitializerFactory** (producer (advanced)) | To use a custom ClientInitializerFactory. |  | ClientInitializerFactory |
| **lazyChannelCreation** (producer (advanced)) | Channels can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **okStatusCodeRange** (producer (advanced)) | The status codes which are considered a success response. The values are inclusive. Multiple ranges can be defined, separated by comma, e.g. 200-204,209,301-304. Each range must be a single number or from-to with the dash included. The default range is 200-299. | 200-299 | String |
| **producerPoolBlockWhenExhausted** (producer (advanced)) | Sets the value for the blockWhenExhausted configuration attribute. It determines whether to block when the borrowObject() method is invoked when the pool is exhausted (the maximum number of active objects has been reached). | true | boolean |
| **producerPoolEnabled** (producer (advanced)) | Whether producer pool is enabled or not. Important: If you turn this off then a single shared connection is used for the producer, also if you are doing request/reply. That means there is a potential issue with interleaved responses if replies comes back out-of-order. Therefore you need to have a correlation id in both the request and reply messages so you can properly correlate the replies to the Camel callback that is responsible for continue processing the message in Camel. To do this you need to implement NettyCamelStateCorrelationManager as correlation manager and configure it via the correlationManager option. See also the correlationManager option for more details. | true | boolean |
| **producerPoolMaxIdle** (producer (advanced)) | Sets the cap on the number of idle instances in the pool. | 100 | int |
| **producerPoolMaxTotal** (producer (advanced)) | Sets the cap on the number of objects that can be allocated by the pool (checked out to clients, or idle awaiting checkout) at a given time. Use a negative value for no limit. Be careful to not set this value too low (such as 1) as the pool must have space to create a producer such as when performing retries. Be mindful that the option producerPoolBlockWhenExhausted is default true, and the pool will then block when there is no space, which can lead to the application to hang. | \-1 | int |
| **producerPoolMaxWait** (producer (advanced)) | Sets the maximum duration (value in millis) the borrowObject() method should block before throwing an exception when the pool is exhausted and producerPoolBlockWhenExhausted is true. When less than 0, the borrowObject() method may block indefinitely. | \-1 | long |
| **producerPoolMinEvictableIdle** (producer (advanced)) | Sets the minimum amount of time (value in millis) an object may sit idle in the pool before it is eligible for eviction by the idle object evictor. | 300000 | long |
| **producerPoolMinIdle** (producer (advanced)) | Sets the minimum number of instances allowed in the producer pool before the evictor thread (if active) spawns new objects. |  | int |
| **useRelativePath** (producer (advanced)) | Sets whether to use a relative path in HTTP requests. | true | boolean |
| **allowSerializedHeaders** (advanced) | Only used for TCP when transferExchange is true. When set to true, serializable objects in headers and properties will be added to the exchange. Otherwise Camel will exclude any non-serializable objects and log it at WARN level. | false | boolean |
| **channelGroup** (advanced) | To use an explicit ChannelGroup. |  | ChannelGroup |
| **configuration** (advanced) | To use a custom configured NettyHttpConfiguration for configuring this endpoint. |  | NettyHttpConfiguration |
| **disableStreamCache** (advanced) | Determines whether or not the raw input stream from Netty HttpRequest#getContent() or HttpResponset#getContent() is cached or not (Camel will read the stream into a in light-weight memory based Stream caching) cache. By default Camel will cache the Netty input stream to support reading it multiple times to ensure it Camel can retrieve all data from the stream. However you can set this option to true when you for example need to access the raw stream, such as streaming it directly to a file or other persistent store. Mind that if you enable this option, then you cannot read the Netty stream multiple times out of the box, and you would need manually to reset the reader index on the Netty raw stream. Also Netty will auto-close the Netty stream when the Netty HTTP server/HTTP client is done processing, which means that if the asynchronous routing engine is in use then any asynchronous thread that may continue routing the org.apache.camel.Exchange may not be able to read the Netty stream, because Netty has closed it. | false | boolean |
| **headerFilterStrategy** (advanced) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter headers. |  | HeaderFilterStrategy |
| **nativeTransport** (advanced) | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | boolean |
| **nettyHttpBinding** (advanced) | To use a custom org.apache.camel.component.netty.http.NettyHttpBinding for binding to/from Netty and Camel Message API. |  | NettyHttpBinding |
| **options** (advanced) | Allows to configure additional netty options using option. as prefix. For example option.child.keepAlive=false. See the Netty documentation for possible options that can be used. This is a multi-value option with prefix: option. |  | Map |
| **receiveBufferSize** (advanced) | The TCP/UDP buffer sizes to be used during inbound communication. Size is bytes. | 65536 | int |
| **receiveBufferSizePredictor** (advanced) | Configures the buffer size predictor. See details at Jetty documentation and this mail thread. |  | int |
| **sendBufferSize** (advanced) | The TCP/UDP buffer sizes to be used during outbound communication. Size is bytes. | 65536 | int |
| **shutdownTimeout** (advanced) | Shutdown await timeout in milliseconds. | 100 | int |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **transferException** (advanced) | If enabled and an Exchange failed processing on the consumer side, and if the caused Exception was send back serialized in the response as a application/x-java-serialized-object content type. On the producer side the exception will be deserialized and thrown as is, instead of the HttpOperationFailedException. The caused exception is required to be serialized. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | boolean |
| **transferExchange** (advanced) | Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | boolean |
| **unixDomainSocketPath** (advanced) | Path to unix domain socket to use instead of inet socket. Host and port parameters will not be used, however required. It is ok to set dummy values for them. Must be used with nativeTransport=true and clientMode=false. |  | String |
| **workerCount** (advanced) | When netty works on nio mode, it uses default workerCount parameter from Netty (which is cpu\_core\_threads x 2). User can use this option to override the default workerCount from Netty. |  | int |
| **workerGroup** (advanced) | To use a explicit EventLoopGroup as the boss thread pool. For example to share a thread pool with multiple consumers or producers. By default each consumer or producer has their own worker pool with 2 x cpu count core threads. |  | EventLoopGroup |
| **decoders** (codec) | A list of decoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | String |
| **encoders** (codec) | A list of encoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | String |
| **deserializationFilter** (security) | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied when deserializing Java objects from HTTP responses with Content-Type application/x-java-serialized-object. This is used when transferException is enabled and the remote side returns a serialized exception. When not set, the filter configured via the JVM system property jdk.serialFilter is used when present; otherwise a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. packages is applied. |  | String |
| **enabledProtocols** (security) | Which protocols to enable when using SSL. | TLSv1.2,TLSv1.3 | String |
| **hostnameVerification** (security) | To enable/disable hostname verification on SSLEngine. | false | boolean |
| **keyStoreFormat** (security) | Keystore format to be used for payload encryption. Defaults to JKS if not set. |  | String |
| **keyStoreResource** (security) | Client side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **needClientAuth** (security) | Configures whether the server needs client authentication when using SSL. | false | boolean |
| **passphrase** (security) | Password to use for the keyStore and trustStore. The same password must be configured for both resources. |  | String |
| **securityConfiguration** (security) | Refers to a org.apache.camel.component.netty.http.NettyHttpSecurityConfiguration for configuring secure web resources. |  | NettyHttpSecurityConfiguration |
| **securityOptions** (security) | To configure NettyHttpSecurityConfiguration using key/value pairs from the map. This is a multi-value option with prefix: securityConfiguration. |  | Map |
| **securityProvider** (security) | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | String |
| **ssl** (security) | Setting to specify whether SSL encryption is applied to this endpoint. | false | boolean |
| **sslClientCertHeaders** (security) | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **sslHandler** (security) | Reference to a class that could be used to return an SSL Handler. |  | SslHandler |
| **trustStoreResource** (security) | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |

## Message Headers

The Netty HTTP component supports 24 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHttpAuthentication** (common) Constant: [`HTTP_AUTHENTICATION`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_AUTHENTICATION) | If the user was authenticated using HTTP Basic then this header is added with the value Basic. |  | String |
| **Content-Type** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#CONTENT_TYPE) | To set the content-type of the HTTP body. For example: text/plain; charset=UTF-8. |  | String |
| **connection** (common) Constant: [`CONNECTION`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#CONNECTION) | The value of the HTTP header connection to use. |  | String |
| **CamelNettyCloseChannelWhenComplete** (common) Constant: [`NETTY_CLOSE_CHANNEL_WHEN_COMPLETE`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#NETTY_CLOSE_CHANNEL_WHEN_COMPLETE) | Indicates whether the channel should be closed after complete. |  | Boolean |
| **CamelHttpResponseCode** (common) Constant: [`HTTP_RESPONSE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_RESPONSE_CODE) | Allows to set the HTTP Status code to use. By default 200 is used for success, and 500 for failure. |  | Integer |
| **CamelHttpProtocolVersion** (common) Constant: [`HTTP_PROTOCOL_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_PROTOCOL_VERSION) | The version of the HTTP protocol. | HTTP/1.1 | String |
| **CamelHttpMethod** (common) Constant: [`HTTP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_METHOD) | The HTTP method used, such as GET, POST, TRACE etc. | GET | String |
| **CamelHttpQuery** (common) Constant: [`HTTP_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_QUERY) | Any query parameters, such as foo=bar&beer=yes. |  | String |
| **CamelHttpPath** (common) Constant: [`HTTP_PATH`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_PATH) | Allows to provide URI context-path and query parameters as a String value that overrides the endpoint configuration. This allows to reuse the same producer for calling same remote http server, but using a dynamic context-path and query parameters. |  | String |
| **CamelHttpRawQuery** (common) Constant: [`HTTP_RAW_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_RAW_QUERY) | Any query parameters, such as foo=bar&beer=yes. Stored in the raw form, as they arrived to the consumer (i.e. before URL decoding). |  | String |
| **CamelHttpUrl** (common) Constant: [`HTTP_URL`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_URL) | The URL including protocol, host and port, etc: [http://0.0.0.0:8080/myapp](http://0.0.0.0:8080/myapp). |  | String |
| **CamelHttpCharacterEncoding** (common) Constant: [`HTTP_CHARACTER_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_CHARACTER_ENCODING) | The charset from the content-type header. |  | String |
| **CamelHttpUri** (common) Constant: [`HTTP_URI`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/http/NettyHttpConstants.html#HTTP_URI) | The URI without protocol, host and port, etc: /myapp. |  | String |
| **CamelNettyChannelHandlerContext** (common) Constant: [`NETTY_CHANNEL_HANDLER_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_CHANNEL_HANDLER_CONTEXT) | The channel handler context. |  | ChannelHandlerContext |
| **CamelNettyRemoteAddress** (common) Constant: [`NETTY_REMOTE_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_REMOTE_ADDRESS) | The remote address. |  | SocketAddress |
| **CamelNettyLocalAddress** (common) Constant: [`NETTY_LOCAL_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_LOCAL_ADDRESS) | The local address. |  | SocketAddress |
| **CamelNettySSLSession** (common) Constant: [`NETTY_SSL_SESSION`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_SESSION) | The SSL session. |  | SSLSession |
| **CamelNettySSLClientCertSubjectName** (common) Constant: [`NETTY_SSL_CLIENT_CERT_SUBJECT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_SUBJECT_NAME) | The SSL client certificate subject name. |  | String |
| **CamelNettySSLClientCertIssuerName** (common) Constant: [`NETTY_SSL_CLIENT_CERT_ISSUER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_ISSUER_NAME) | The SSL client certificate issuer name. |  | String |
| **CamelNettySSLClientCertSerialNumber** (common) Constant: [`NETTY_SSL_CLIENT_CERT_SERIAL_NO`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_SERIAL_NO) | The SSL client certificate serial number. |  | String |
| **CamelNettySSLClientCertNotBefore** (common) Constant: [`NETTY_SSL_CLIENT_CERT_NOT_BEFORE`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_NOT_BEFORE) | The SSL client certificate not before. |  | Date |
| **CamelNettySSLClientCertNotAfter** (common) Constant: [`NETTY_SSL_CLIENT_CERT_NOT_AFTER`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_NOT_AFTER) | The SSL client certificate not after. |  | Date |
| **CamelNettyRequestTimeout** (common) Constant: [`NETTY_REQUEST_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_REQUEST_TIMEOUT) | The read timeout. |  | Long |
| **CamelNettyChannel** (common) Constant: [`NETTY_CHANNEL`](https://javadoc.io/doc/org.apache.camel/camel-netty-http/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_CHANNEL) | The Netty Channel object. |  | Channel |

## Usage

### Access to Netty types

This component uses the `org.apache.camel.component.netty.http.NettyHttpMessage` as the message implementation on the Exchange. This allows end users to get access to the original Netty request/response instances if needed, as shown below. Mind that the original response may not be accessible at all times.

```java
io.netty.handler.codec.http.HttpRequest request = exchange.getIn(NettyHttpMessage.class).getHttpRequest();
```

### Using HTTP Basic Authentication

The Netty HTTP consumer supports HTTP basic authentication by specifying the security realm name to use, as shown below

```java
<route>
   <from uri="netty-http:http://0.0.0.0:{{port}}/foo?securityConfiguration.realm=someRealm"/>
   ...
</route>
```

The realm name is mandatory to enable basic authentication. By default, the JAAS based authenticator is used, which will use the realm name specified (`_someRealm_` in the example above) and use the JAAS realm and the `JAAS \{{LoginModule}}s` of this realm for authentication.

#### Specifying ACL on web resources

The `org.apache.camel.component.netty.http.SecurityConstraint` allows to define constraints on web resources. And the `org.apache.camel.component.netty.http.SecurityConstraintMapping` is provided out of the box, allowing to easily define inclusions and exclusions with roles.

For example, as shown below in the XML DSL, we define the constraint bean:

```xml
  <bean id="constraint" class="org.apache.camel.component.netty.http.SecurityConstraintMapping">
    <!-- inclusions defines url -> roles restrictions -->
    <!-- a * should be used for any role accepted (or even no roles) -->
    <property name="inclusions">
      <map>
        <entry key="/*" value="*"/>
        <entry key="/admin/*" value="admin"/>
        <entry key="/guest/*" value="admin,guest"/>
      </map>
    </property>
    <!-- exclusions is used to define public urls, which requires no authentication -->
    <property name="exclusions">
      <set>
        <value>/public/*</value>
      </set>
    </property>
  </bean>
```

The constraint above is defined so that

-   access to /\* is restricted and any roles are accepted (also if user has no roles)
    
-   access to /admin/\* requires the admin role
    
-   access to /guest/\* requires the admin or guest role
    
-   access to /public/\* is an exclusion that means no authentication is necessary, and is therefore public for everyone without logging in
    

To use this constraint, we just need to refer to the bean id as shown below:

```xml
<route>
   <from uri="netty-http:http://0.0.0.0:{{port}}/foo?matchOnUriPrefix=true&amp;securityConfiguration.realm=someRealm&amp;securityConfiguration.securityConstraint=#constraint"/>
   ...
</route>
```

## Examples

In the route below, we use Netty HTTP as an HTTP server, which returns a hardcoded _"Bye World"_ message.

```java
    from("netty-http:http://0.0.0.0:8080/foo")
      .transform().constant("Bye World");
```

And we can call this HTTP server using Camel also, with the ProducerTemplate as shown below:

```java
    String out = template.requestBody("netty-http:http://0.0.0.0:8080/foo", "Hello World", String.class);
    System.out.println(out);
```

And we get _"Bye World"_ as the output.

### How do I let Netty match wildcards?

By default, Netty HTTP will only match on exact uri’s. But you can instruct Netty to match prefixes. For example

```java
from("netty-http:http://0.0.0.0:8123/foo").to("mock:foo");
```

In the route above Netty HTTP will only match if the uri is an exact match, so it will match if you enter  
`http://0.0.0.0:8123/foo` but not match if you do `http://0.0.0.0:8123/foo/bar`.

So if you want to enable wildcard matching, you do as follows:

```java
from("netty-http:http://0.0.0.0:8123/foo?matchOnUriPrefix=true").to("mock:foo");
```

So now Netty matches any endpoints with starts with `foo`.

To match **any** endpoint, you can do:

```java
from("netty-http:http://0.0.0.0:8123?matchOnUriPrefix=true").to("mock:foo");
```

### Using multiple routes with same port

In the same CamelContext you can have multiple routes from Netty HTTP that shares the same port (e.g., a `io.netty.bootstrap.ServerBootstrap` instance). Doing this requires a number of bootstrap options to be identical in the routes, as the routes will share the same `io.netty.bootstrap.ServerBootstrap` instance. The instance will be configured with the options from the first route created.

The options the routes must be identical configured is all the options defined in the `org.apache.camel.component.netty.NettyServerBootstrapConfiguration` configuration class. If you have configured another route with different options, Camel will throw an exception on startup, indicating the options are not identical. To mitigate this ensure all options are identical.

Here is an example with two routes that share the same port.

**Two routes sharing the same port**

```java
from("netty-http:http://0.0.0.0:{{port}}/foo")
  .to("mock:foo")
  .transform().constant("Bye World");

from("netty-http:http://0.0.0.0:{{port}}/bar")
  .to("mock:bar")
  .transform().constant("Bye Camel");
```

And here is an example of a mis-configured second route that does not have identical `org.apache.camel.component.netty.NettyServerBootstrapConfiguration` option as the first route. This will cause Camel to fail on startup.

**Two routes are sharing the same port, but the second route is misconfigured and will fail on starting**

```java
from("netty-http:http://0.0.0.0:{{port}}/foo")
  .to("mock:foo")
  .transform().constant("Bye World");

// we cannot have a 2nd route on the same port with SSL enabled, when the 1st route is NOT
from("netty-http:http://0.0.0.0:{{port}}/bar?ssl=true")
  .to("mock:bar")
  .transform().constant("Bye Camel");
```

### Reusing the same server bootstrap configuration with multiple routes

By configuring the common server bootstrap option in a single instance of a `org.apache.camel.component.netty.NettyServerBootstrapConfiguration` type, we can use the `bootstrapConfiguration` option on the Netty HTTP consumers to refer and reuse the same options across all consumers.

```xml
<bean id="nettyHttpBootstrapOptions" class="org.apache.camel.component.netty.NettyServerBootstrapConfiguration">
  <property name="backlog" value="200"/>
  <property name="connectionTimeout" value="20000"/>
  <property name="workerCount" value="16"/>
</bean>
```

And in the routes you refer to this option as shown below

```xml
<route>
  <from uri="netty-http:http://0.0.0.0:{{port}}/foo?bootstrapConfiguration=#nettyHttpBootstrapOptions"/>
  ...
</route>

<route>
  <from uri="netty-http:http://0.0.0.0:{{port}}/bar?bootstrapConfiguration=#nettyHttpBootstrapOptions"/>
  ...
</route>

<route>
  <from uri="netty-http:http://0.0.0.0:{{port}}/beer?bootstrapConfiguration=#nettyHttpBootstrapOptions"/>
  ...
</route>
```

### Implementing a reverse proxy

Netty HTTP component can act as a reverse proxy, in that case `Exchange.HTTP_SCHEME`, `Exchange.HTTP_HOST` and `Exchange.HTTP_PORT` headers are populated from the absolute URL received on the request line of the HTTP request.

Here’s an example of an HTTP proxy that simply transforms the response from the origin server to uppercase.

```java
from("netty-http:proxy://0.0.0.0:8080")
    .toD("netty-http:"
        + "${headers." + Exchange.HTTP_SCHEME + "}://"
        + "${headers." + Exchange.HTTP_HOST + "}:"
        + "${headers." + Exchange.HTTP_PORT + "}")
    .process(this::processResponse);

void processResponse(final Exchange exchange) {
    final NettyHttpMessage message = exchange.getIn(NettyHttpMessage.class);
    final FullHttpResponse response = message.getHttpResponse();

    final ByteBuf buf = response.content();
    final String string = buf.toString(StandardCharsets.UTF_8);

    buf.resetWriterIndex();
    ByteBufUtil.writeUtf8(buf, string.toUpperCase(Locale.US));
}
```

## Spring Boot Auto-Configuration

When using netty-http with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-netty-http-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 66 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.netty-http.allow-serialized-headers** | Only used for TCP when transferExchange is true. When set to true, serializable objects in headers and properties will be added to the exchange. Otherwise Camel will exclude any non-serializable objects and log it at WARN level. | false | Boolean |
| **camel.component.netty-http.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.netty-http.backlog** | Allows to configure a backlog for netty consumer (server). Note the backlog is just a best effort depending on the OS. Setting this option to a value such as 200, 500 or 1000, tells the TCP stack how long the accept queue can be If this option is not configured, then the backlog depends on OS setting. |  | Integer |
| **camel.component.netty-http.boss-count** | When netty works on nio mode, it uses default bossCount parameter from Netty, which is 1. User can use this option to override the default bossCount from Netty. | 1 | Integer |
| **camel.component.netty-http.boss-group** | Set the BossGroup which could be used for handling the new connection of the server side across the NettyEndpoint. The option is a io.netty.channel.EventLoopGroup type. |  | EventLoopGroup |
| **camel.component.netty-http.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.netty-http.channel-group** | To use an explicit ChannelGroup. The option is a io.netty.channel.group.ChannelGroup type. |  | ChannelGroup |
| **camel.component.netty-http.client-initializer-factory** | To use a custom ClientInitializerFactory. The option is a org.apache.camel.component.netty.ClientInitializerFactory type. |  | ClientInitializerFactory |
| **camel.component.netty-http.configuration** | To use the NettyConfiguration as configuration when creating endpoints. The option is a org.apache.camel.component.netty.NettyConfiguration type. |  | NettyConfiguration |
| **camel.component.netty-http.connect-timeout** | Time to wait for a socket connection to be available. Value is in milliseconds. | 10000 | Integer |
| **camel.component.netty-http.correlation-manager** | To use a custom correlation manager to manage how request and reply messages are mapped when using request/reply with the netty producer. This should only be used if you have a way to map requests together with replies such as if there is correlation ids in both the request and reply messages. This can be used if you want to multiplex concurrent messages on the same channel (aka connection) in netty. When doing this you must have a way to correlate the request and reply messages so you can store the right reply on the inflight Camel Exchange before its continued routed. We recommend extending the TimeoutCorrelationManagerSupport when you build custom correlation managers. This provides support for timeout and other complexities you otherwise would need to implement as well. See also the producerPoolEnabled option for more details. The option is a org.apache.camel.component.netty.NettyCamelStateCorrelationManager type. |  | NettyCamelStateCorrelationManager |
| **camel.component.netty-http.decoders** | A list of decoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | String |
| **camel.component.netty-http.disconnect** | Whether or not to disconnect(close) from Netty Channel right after use. | false | Boolean |
| **camel.component.netty-http.disconnect-on-no-reply** | If sync is enabled then this option dictates NettyConsumer if it should disconnect where there is no reply to send back. | true | Boolean |
| **camel.component.netty-http.enabled** | Whether to enable auto configuration of the netty-http component. This is enabled by default. |  | Boolean |
| **camel.component.netty-http.enabled-protocols** | Which protocols to enable when using SSL. | TLSv1.2,TLSv1.3 | String |
| **camel.component.netty-http.encoders** | A list of encoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | String |
| **camel.component.netty-http.executor-service** | To use the given custom EventExecutorGroup. The option is a io.netty.util.concurrent.EventExecutorGroup type. |  | EventExecutorGroup |
| **camel.component.netty-http.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter headers. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.netty-http.hostname-verification** | To enable/disable hostname verification on SSLEngine. | false | Boolean |
| **camel.component.netty-http.keep-alive** | Setting to ensure socket is not closed due to inactivity. | true | Boolean |
| **camel.component.netty-http.key-store-format** | Keystore format to be used for payload encryption. Defaults to JKS if not set. |  | String |
| **camel.component.netty-http.key-store-resource** | Client side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **camel.component.netty-http.lazy-channel-creation** | Channels can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | Boolean |
| **camel.component.netty-http.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.netty-http.maximum-pool-size** | Sets a maximum thread pool size for the netty consumer ordered thread pool. The default size is 2 x cpu\_core plus 1. Setting this value to eg 10 will then use 10 threads unless 2 x cpu\_core plus 1 is a higher value, which then will override and be used. For example if there are 8 cores, then the consumer thread pool will be 17. This thread pool is used to route messages received from Netty by Camel. We use a separate thread pool to ensure ordering of messages and also in case some messages will block, then nettys worker threads (event loop) wont be affected. |  | Integer |
| **camel.component.netty-http.mute-exception** | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | Boolean |
| **camel.component.netty-http.native-transport** | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | Boolean |
| **camel.component.netty-http.need-client-auth** | Configures whether the server needs client authentication when using SSL. | false | Boolean |
| **camel.component.netty-http.netty-http-binding** | To use a custom org.apache.camel.component.netty.http.NettyHttpBinding for binding to/from Netty and Camel Message API. The option is a org.apache.camel.component.netty.http.NettyHttpBinding type. |  | NettyHttpBinding |
| **camel.component.netty-http.netty-server-bootstrap-factory** | To use a custom NettyServerBootstrapFactory. The option is a org.apache.camel.component.netty.NettyServerBootstrapFactory type. |  | NettyServerBootstrapFactory |
| **camel.component.netty-http.no-reply-log-level** | If sync is enabled this option dictates NettyConsumer which logging level to use when logging a there is no reply to send back. | warn | LoggingLevel |
| **camel.component.netty-http.options** | Allows to configure additional netty options using option. as prefix. For example option.child.keepAlive=false. See the Netty documentation for possible options that can be used. This is a multi-value option with prefix: option. |  | Map |
| **camel.component.netty-http.passphrase** | Password to use for the keyStore and trustStore. The same password must be configured for both resources. |  | String |
| **camel.component.netty-http.producer-pool-block-when-exhausted** | Sets the value for the blockWhenExhausted configuration attribute. It determines whether to block when the borrowObject() method is invoked when the pool is exhausted (the maximum number of active objects has been reached). | true | Boolean |
| **camel.component.netty-http.producer-pool-enabled** | Whether producer pool is enabled or not. Important: If you turn this off then a single shared connection is used for the producer, also if you are doing request/reply. That means there is a potential issue with interleaved responses if replies comes back out-of-order. Therefore you need to have a correlation id in both the request and reply messages so you can properly correlate the replies to the Camel callback that is responsible for continue processing the message in Camel. To do this you need to implement NettyCamelStateCorrelationManager as correlation manager and configure it via the correlationManager option. See also the correlationManager option for more details. | true | Boolean |
| **camel.component.netty-http.producer-pool-max-idle** | Sets the cap on the number of idle instances in the pool. | 100 | Integer |
| **camel.component.netty-http.producer-pool-max-total** | Sets the cap on the number of objects that can be allocated by the pool (checked out to clients, or idle awaiting checkout) at a given time. Use a negative value for no limit. Be careful to not set this value too low (such as 1) as the pool must have space to create a producer such as when performing retries. Be mindful that the option producerPoolBlockWhenExhausted is default true, and the pool will then block when there is no space, which can lead to the application to hang. | \-1 | Integer |
| **camel.component.netty-http.producer-pool-max-wait** | Sets the maximum duration (value in millis) the borrowObject() method should block before throwing an exception when the pool is exhausted and producerPoolBlockWhenExhausted is true. When less than 0, the borrowObject() method may block indefinitely. | \-1 | Long |
| **camel.component.netty-http.producer-pool-min-evictable-idle** | Sets the minimum amount of time (value in millis) an object may sit idle in the pool before it is eligible for eviction by the idle object evictor. | 300000 | Long |
| **camel.component.netty-http.producer-pool-min-idle** | Sets the minimum number of instances allowed in the producer pool before the evictor thread (if active) spawns new objects. |  | Integer |
| **camel.component.netty-http.receive-buffer-size** | The TCP/UDP buffer sizes to be used during inbound communication. Size is bytes. | 65536 | Integer |
| **camel.component.netty-http.receive-buffer-size-predictor** | Configures the buffer size predictor. See details at Jetty documentation and this mail thread. |  | Integer |
| **camel.component.netty-http.request-timeout** | Allows to use a timeout for the Netty producer when calling a remote server. By default no timeout is in use. The value is in milli seconds, so eg 30000 is 30 seconds. The requestTimeout is using Netty’s ReadTimeoutHandler to trigger the timeout. |  | Long |
| **camel.component.netty-http.reuse-address** | Setting to facilitate socket multiplexing. | true | Boolean |
| **camel.component.netty-http.reuse-channel** | This option allows producers and consumers (in client mode) to reuse the same Netty Channel for the lifecycle of processing the Exchange. This is useful if you need to call a server multiple times in a Camel route and want to use the same network connection. When using this, the channel is not returned to the connection pool until the Exchange is done; or disconnected if the disconnect option is set to true. The reused Channel is stored on the Exchange as an exchange property with the key CamelNettyChannel which allows you to obtain the channel during routing and use it as well. | false | Boolean |
| **camel.component.netty-http.security-configuration** | Refers to a org.apache.camel.component.netty.http.NettyHttpSecurityConfiguration for configuring secure web resources. The option is a org.apache.camel.component.netty.http.NettyHttpSecurityConfiguration type. |  | NettyHttpSecurityConfiguration |
| **camel.component.netty-http.security-provider** | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | String |
| **camel.component.netty-http.send-buffer-size** | The TCP/UDP buffer sizes to be used during outbound communication. Size is bytes. | 65536 | Integer |
| **camel.component.netty-http.server-closed-channel-exception-caught-log-level** | If the server (NettyConsumer) catches an java.nio.channels.ClosedChannelException then its logged using this logging level. This is used to avoid logging the closed channel exceptions, as clients can disconnect abruptly and then cause a flood of closed exceptions in the Netty server. | debug | LoggingLevel |
| **camel.component.netty-http.server-exception-caught-log-level** | If the server (NettyConsumer) catches an exception then its logged using this logging level. | warn | LoggingLevel |
| **camel.component.netty-http.server-initializer-factory** | To use a custom ServerInitializerFactory. The option is a org.apache.camel.component.netty.ServerInitializerFactory type. |  | ServerInitializerFactory |
| **camel.component.netty-http.shutdown-timeout** | Shutdown await timeout in milliseconds. | 100 | Integer |
| **camel.component.netty-http.ssl** | Setting to specify whether SSL encryption is applied to this endpoint. | false | Boolean |
| **camel.component.netty-http.ssl-client-cert-headers** | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | Boolean |
| **camel.component.netty-http.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.netty-http.ssl-handler** | Reference to a class that could be used to return an SSL Handler. The option is a io.netty.handler.ssl.SslHandler type. |  | SslHandler |
| **camel.component.netty-http.sync** | Setting to set endpoint as one-way (false) or request-response (true). | true | Boolean |
| **camel.component.netty-http.tcp-no-delay** | Setting to improve TCP protocol performance. | true | Boolean |
| **camel.component.netty-http.transfer-exchange** | Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | Boolean |
| **camel.component.netty-http.trust-store-resource** | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **camel.component.netty-http.unix-domain-socket-path** | Path to unix domain socket to use instead of inet socket. Host and port parameters will not be used, however required. It is ok to set dummy values for them. Must be used with nativeTransport=true and clientMode=false. |  | String |
| **camel.component.netty-http.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.netty-http.using-executor-service** | Whether to use ordered thread pool, to ensure events are processed orderly on the same channel. | true | Boolean |
| **camel.component.netty-http.worker-count** | When netty works on nio mode, it uses default workerCount parameter from Netty (which is cpu\_core\_threads x 2). User can use this option to override the default workerCount from Netty. |  | Integer |
| **camel.component.netty-http.worker-group** | To use a explicit EventLoopGroup as the boss thread pool. For example to share a thread pool with multiple consumers or producers. By default each consumer or producer has their own worker pool with 2 x cpu count core threads. The option is a io.netty.channel.EventLoopGroup type. |  | EventLoopGroup |