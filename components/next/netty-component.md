# Netty

**Since Camel 2.14**

**Both producer and consumer are supported**

The Netty component in Camel is a socket communication component, based on the [Netty](http://netty.io/) project version 4. Netty is a NIO client server framework that enables quick and easy development of networkServerInitializerFactory applications such as protocol servers and clients. Netty greatly simplifies and streamlines network programming such as TCP and UDP socket server.

This Camel component supports both producer and consumer endpoints.

The Netty component has several options and allows fine-grained control of a number of TCP/UDP communication parameters (buffer sizes, `keepAlive`, `tcpNoDelay`, etc.), and facilitates both In-Only and In-Out communication on a Camel route.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-netty</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

The URI scheme for a netty component is as follows

TCP

netty:tcp://0.0.0.0:99999\[?options\]

UDP

netty:udp://remotehost:99999/\[?options\]

This component supports producer and consumer endpoints for both TCP and UDP.

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

The Netty component supports 75 options, which are listed below.

   
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
| **nativeTransport** (advanced) | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | boolean |
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
| **securityProvider** (security) | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | String |
| **ssl** (security) | Setting to specify whether SSL encryption is applied to this endpoint. | false | boolean |
| **sslClientCertHeaders** (security) | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **sslHandler** (security) | Reference to a class that could be used to return an SSL Handler. |  | SslHandler |
| **trustStoreResource** (security) | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Netty endpoint is configured using URI syntax:

netty:protocol://host:port

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **protocol** (common) | 
**Required** The protocol to use which can be tcp or udp.

Enum values:

-   tcp
    
-   udp
    





 |  | String |
| **host** (common) | **Required** The hostname. For the consumer the hostname is localhost or 0.0.0.0. For the producer the hostname is the remote host to connect to. |  | String |
| **port** (common) | **Required** The host port number. |  | int |

### Query Parameters (73 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **disconnect** (common) | Whether or not to disconnect(close) from Netty Channel right after use. | false | boolean |
| **keepAlive** (common) | Setting to ensure socket is not closed due to inactivity. | true | boolean |
| **reuseAddress** (common) | Setting to facilitate socket multiplexing. | true | boolean |
| **reuseChannel** (common) | This option allows producers and consumers (in client mode) to reuse the same Netty Channel for the lifecycle of processing the Exchange. This is useful if you need to call a server multiple times in a Camel route and want to use the same network connection. When using this, the channel is not returned to the connection pool until the Exchange is done; or disconnected if the disconnect option is set to true. The reused Channel is stored on the Exchange as an exchange property with the key CamelNettyChannel which allows you to obtain the channel during routing and use it as well. | false | boolean |
| **sync** (common) | Setting to set endpoint as one-way (false) or request-response (true). | true | boolean |
| **tcpNoDelay** (common) | Setting to improve TCP protocol performance. | true | boolean |
| **networkInterface** (common (advanced)) | When using UDP then this option can be used to specify a network interface by its name, such as eth0 to join a multicast group. |  | String |
| **clientMode** (consumer) | If the clientMode is true, netty consumer will connect the address as a TCP client. | false | boolean |
| **reconnect** (consumer) | Used only in clientMode in consumer, the consumer will attempt to reconnect on disconnection if this is enabled. | true | boolean |
| **reconnectInterval** (consumer) | Used if reconnect and clientMode is enabled. The interval in milli seconds to attempt reconnection. | 10000 | int |
| **backlog** (consumer (advanced)) | Allows to configure a backlog for netty consumer (server). Note the backlog is just a best effort depending on the OS. Setting this option to a value such as 200, 500 or 1000, tells the TCP stack how long the accept queue can be If this option is not configured, then the backlog depends on OS setting. |  | int |
| **bossCount** (consumer (advanced)) | When netty works on nio mode, it uses default bossCount parameter from Netty, which is 1. User can use this option to override the default bossCount from Netty. | 1 | int |
| **bossGroup** (consumer (advanced)) | Set the BossGroup which could be used for handling the new connection of the server side across the NettyEndpoint. |  | EventLoopGroup |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **broadcast** (consumer (advanced)) | Setting to choose Multicast over UDP. | false | boolean |
| **disconnectOnNoReply** (consumer (advanced)) | If sync is enabled then this option dictates NettyConsumer if it should disconnect where there is no reply to send back. | true | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
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
| **requestTimeout** (producer) | Allows to use a timeout for the Netty producer when calling a remote server. By default no timeout is in use. The value is in milli seconds, so eg 30000 is 30 seconds. The requestTimeout is using Netty’s ReadTimeoutHandler to trigger the timeout. |  | long |
| **clientInitializerFactory** (producer (advanced)) | To use a custom ClientInitializerFactory. |  | ClientInitializerFactory |
| **correlationManager** (producer (advanced)) | To use a custom correlation manager to manage how request and reply messages are mapped when using request/reply with the netty producer. This should only be used if you have a way to map requests together with replies such as if there is correlation ids in both the request and reply messages. This can be used if you want to multiplex concurrent messages on the same channel (aka connection) in netty. When doing this you must have a way to correlate the request and reply messages so you can store the right reply on the inflight Camel Exchange before its continued routed. We recommend extending the TimeoutCorrelationManagerSupport when you build custom correlation managers. This provides support for timeout and other complexities you otherwise would need to implement as well. See also the producerPoolEnabled option for more details. |  | NettyCamelStateCorrelationManager |
| **lazyChannelCreation** (producer (advanced)) | Channels can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
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
| **channelGroup** (advanced) | To use an explicit ChannelGroup. |  | ChannelGroup |
| **nativeTransport** (advanced) | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | boolean |
| **options** (advanced) | Allows to configure additional netty options using option. as prefix. For example option.child.keepAlive=false. See the Netty documentation for possible options that can be used. This is a multi-value option with prefix: option. |  | Map |
| **receiveBufferSize** (advanced) | The TCP/UDP buffer sizes to be used during inbound communication. Size is bytes. | 65536 | int |
| **receiveBufferSizePredictor** (advanced) | Configures the buffer size predictor. See details at Jetty documentation and this mail thread. |  | int |
| **sendBufferSize** (advanced) | The TCP/UDP buffer sizes to be used during outbound communication. Size is bytes. | 65536 | int |
| **shutdownTimeout** (advanced) | Shutdown await timeout in milliseconds. | 100 | int |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
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
| **securityProvider** (security) | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | String |
| **ssl** (security) | Setting to specify whether SSL encryption is applied to this endpoint. | false | boolean |
| **sslClientCertHeaders** (security) | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **sslHandler** (security) | Reference to a class that could be used to return an SSL Handler. |  | SslHandler |
| **trustStoreResource** (security) | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |

## Message Headers

The Netty component supports 12 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelNettyCloseChannelWhenComplete** (common) Constant: [`NETTY_CLOSE_CHANNEL_WHEN_COMPLETE`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_CLOSE_CHANNEL_WHEN_COMPLETE) | Indicates whether the channel should be closed after complete. |  | Boolean |
| **CamelNettyChannelHandlerContext** (common) Constant: [`NETTY_CHANNEL_HANDLER_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_CHANNEL_HANDLER_CONTEXT) | The channel handler context. |  | ChannelHandlerContext |
| **CamelNettyRemoteAddress** (common) Constant: [`NETTY_REMOTE_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_REMOTE_ADDRESS) | The remote address. |  | SocketAddress |
| **CamelNettyLocalAddress** (common) Constant: [`NETTY_LOCAL_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_LOCAL_ADDRESS) | The local address. |  | SocketAddress |
| **CamelNettySSLSession** (common) Constant: [`NETTY_SSL_SESSION`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_SESSION) | The SSL session. |  | SSLSession |
| **CamelNettySSLClientCertSubjectName** (common) Constant: [`NETTY_SSL_CLIENT_CERT_SUBJECT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_SUBJECT_NAME) | The SSL client certificate subject name. |  | String |
| **CamelNettySSLClientCertIssuerName** (common) Constant: [`NETTY_SSL_CLIENT_CERT_ISSUER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_ISSUER_NAME) | The SSL client certificate issuer name. |  | String |
| **CamelNettySSLClientCertSerialNumber** (common) Constant: [`NETTY_SSL_CLIENT_CERT_SERIAL_NO`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_SERIAL_NO) | The SSL client certificate serial number. |  | String |
| **CamelNettySSLClientCertNotBefore** (common) Constant: [`NETTY_SSL_CLIENT_CERT_NOT_BEFORE`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_NOT_BEFORE) | The SSL client certificate not before. |  | Date |
| **CamelNettySSLClientCertNotAfter** (common) Constant: [`NETTY_SSL_CLIENT_CERT_NOT_AFTER`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_SSL_CLIENT_CERT_NOT_AFTER) | The SSL client certificate not after. |  | Date |
| **CamelNettyRequestTimeout** (common) Constant: [`NETTY_REQUEST_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_REQUEST_TIMEOUT) | The read timeout. |  | Long |
| **CamelNettyChannel** (common) Constant: [`NETTY_CHANNEL`](https://javadoc.io/doc/org.apache.camel/camel-netty/latest/org/apache/camel/component/netty/NettyConstants.html#NETTY_CHANNEL) | The Netty Channel object. |  | Channel |

## Usage

### Registry-based Options

Codec Handlers and SSL Keystores can be enlisted in the Registry, such as in the Spring XML file. The values that could be passed in are the following:

 
| Name | Description |
| --- | --- |
| `passphrase` | Password to use for the keyStore and trustStore. The same password must be configured for both resources. |
| `keyStoreFormat` | keystore format to be used for payload encryption. Defaults to `JKS` if not set |
| `securityProvider` | Security provider to be used for payload encryption. Defaults to `SunX509` if not set. |
| `keyStoreResource` | Client side certificate keystore to be used for encryption. It is loaded by default from classpath, but you can prefix with `"classpath:"`, `"file:"`, or `"http:"` to load the resource from different systems. |
| `trustStoreResource` | Server side certificate keystore to be used for encryption. It is loaded by default from classpath, but you can prefix with `"classpath:"`, `"file:"`, or `"http:"` to load the resource from different systems. |
| `sslHandler` | Reference to a class that could be used to return an SSL Handler |
| `encoder` | A custom `ChannelHandler` class that can be used to perform special marshalling of outbound payloads. Must override `io.netty.channel.ChannelInboundHandlerAdapter`. |
| `encoders` | A list of encoders to be used. You can use a string that has values separated by comma, and have the values be looked up in the Registry. Remember to prefix the value with `#` so Camel knows it should look up. |
| `decoder` | A custom `ChannelHandler` class that can be used to perform special marshalling of inbound payloads. Must override `io.netty.channel.ChannelOutboundHandlerAdapter`. |
| `decoders` | A list of decoders to be used. You can use a string that has values separated by comma, and have the values be looked up in the Registry. Remember to prefix the value with `#` so Camel knows it should look up. |
> **Note**
> Read below about using non-shareable encoders/decoders.

#### Using non-shareable encoders or decoders

If your encoders or decoders are not shareable (e.g., they don’t have the @Shareable class annotation), then your encoder/decoder must implement the `org.apache.camel.component.netty.ChannelHandlerFactory` interface, and return a new instance in the `newChannelHandler` method. This is to ensure the encoder/decoder can safely be used. If this is not the case, then the Netty component will log a WARN when an endpoint is created.

The Netty component offers a `org.apache.camel.component.netty.ChannelHandlerFactories` factory class, that has a number of commonly used methods.

### Sending Messages to/from a Netty endpoint

#### Netty Producer

In Producer mode, the component provides the ability to send payloads to a socket endpoint using either TCP or UDP protocols (with optional SSL support).

The producer mode supports both one-way and request-response based operations.

#### Netty Consumer

In Consumer mode, the component provides the ability to:

-   listen to a specified socket using either TCP or UDP protocols (with optional SSL support),
    
-   receive requests on the socket using text/xml, binary and serialized object-based payloads and
    
-   send them along on a route as message exchanges.
    

The consumer mode supports both one-way and request-response based operations.

#### Using Multiple Codecs

In certain cases, it may be necessary to add chains of encoders and decoders to the netty pipeline. To add multiple codecs to a Camel netty endpoint, the `encoders` and `decoders` uri parameters should be used. Like the `encoder` and `decoder` parameters they are used to supply references (lists of `ChannelUpstreamHandlers` and `ChannelDownstreamHandlers`) that should be added to the pipeline.

Note that if encoders are specified, then the encoder param will be ignored, similarly for decoders and the decoder param.

> **Note**
> Read further about using [non-shareable encoders/decoders](#Netty-NonShareableEncodersOrDecoders).

The lists of codecs need to be added to the Camel’s registry, so they can be resolved when the endpoint is created.

_Java-only: Java programmatic registry configuration_

```java
ChannelHandlerFactory lengthDecoder = ChannelHandlerFactories.newLengthFieldBasedFrameDecoder(1048576, 0, 4, 0, 4);

StringDecoder stringDecoder = new StringDecoder();
registry.bind("length-decoder", lengthDecoder);
registry.bind("string-decoder", stringDecoder);

LengthFieldPrepender lengthEncoder = new LengthFieldPrepender(4);
StringEncoder stringEncoder = new StringEncoder();
registry.bind("length-encoder", lengthEncoder);
registry.bind("string-encoder", stringEncoder);

List<ChannelHandler> decoders = new ArrayList<ChannelHandler>();
decoders.add(lengthDecoder);
decoders.add(stringDecoder);

List<ChannelHandler> encoders = new ArrayList<ChannelHandler>();
encoders.add(lengthEncoder);
encoders.add(stringEncoder);

registry.bind("encoders", encoders);
registry.bind("decoders", decoders);
```

Spring’s native collections support can be used to specify the codec lists in an application context

```xml
<util:list id="decoders" list-class="java.util.LinkedList">
        <bean class="org.apache.camel.component.netty.ChannelHandlerFactories" factory-method="newLengthFieldBasedFrameDecoder">
            <constructor-arg value="1048576"/>
            <constructor-arg value="0"/>
            <constructor-arg value="4"/>
            <constructor-arg value="0"/>
            <constructor-arg value="4"/>
        </bean>
        <bean class="io.netty.handler.codec.string.StringDecoder"/>
    </util:list>

    <util:list id="encoders" list-class="java.util.LinkedList">
        <bean class="io.netty.handler.codec.LengthFieldPrepender">
            <constructor-arg value="4"/>
        </bean>
        <bean class="io.netty.handler.codec.string.StringEncoder"/>
    </util:list>

    <bean id="length-encoder" class="io.netty.handler.codec.LengthFieldPrepender">
        <constructor-arg value="4"/>
    </bean>
    <bean id="string-encoder" class="io.netty.handler.codec.string.StringEncoder"/>

    <bean id="length-decoder" class="org.apache.camel.component.netty.ChannelHandlerFactories" factory-method="newLengthFieldBasedFrameDecoder">
        <constructor-arg value="1048576"/>
        <constructor-arg value="0"/>
        <constructor-arg value="4"/>
        <constructor-arg value="0"/>
        <constructor-arg value="4"/>
    </bean>
    <bean id="string-decoder" class="io.netty.handler.codec.string.StringDecoder"/>
```

The bean names can then be used in netty endpoint definitions either as a comma-separated list or contained in a list, e.g.:

-   Java
    
-   XML
    
-   YAML
    

```java
 from("direct:multiple-codec").to("netty:tcp://0.0.0.0:{{port}}?encoders=#encoders&sync=false");

 from("netty:tcp://0.0.0.0:{{port}}?decoders=#length-decoder,#string-decoder&sync=false").to("mock:multiple-codec");
```

```xml
<route>
    <from uri="direct:multiple-codec"/>
    <to uri="netty:tcp://0.0.0.0:5150?encoders=#encoders&amp;sync=false"/>
</route>
<route>
    <from uri="netty:tcp://0.0.0.0:5150?decoders=#length-decoder,#string-decoder&amp;sync=false"/>
    <to uri="mock:multiple-codec"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:multiple-codec
      steps:
        - to:
            uri: "netty:tcp://0.0.0.0:5150"
            parameters:
              encoders: "#encoders"
              sync: false
- route:
    from:
      uri: "netty:tcp://0.0.0.0:5150"
      parameters:
        decoders: "#length-decoder,#string-decoder"
        sync: false
      steps:
        - to:
            uri: mock:multiple-codec
```

### Closing Channel When Complete

When acting as a server, you sometimes want to close the channel when, for example, a client conversion is finished. You can do this by simply setting the endpoint option `disconnect=true`.

However, you can also instruct Camel on a per-message basis as follows. To instruct Camel to close the channel, you should add a header with the key `CamelNettyCloseChannelWhenComplete` set to a boolean `true` value. For instance, the example below will close the channel after it has written the bye message back to the client:

_Java-only: inline Processor implementation_

```java
from("netty:tcp://0.0.0.0:8080").process(new Processor() {
    public void process(Exchange exchange) throws Exception {
        String body = exchange.getIn().getBody(String.class);
        exchange.getOut().setBody("Bye " + body);
        // some condition that determines if we should close
        if (close) {
            exchange.getOut().setHeader(NettyConstants.NETTY_CLOSE_CHANNEL_WHEN_COMPLETE, true);
        }
    }
});
```

Adding custom channel pipeline factories to gain complete control over a created pipeline

### Custom pipeline

Custom channel pipelines provide complete control to the user over the handler/interceptor chain by inserting custom handler(s), encoder(s) & decoder(s) without having to specify them in the Netty Endpoint URL in a straightforward way.

To add a custom pipeline, a custom channel pipeline factory must be created and registered with the context via the context registry (or the camel-spring `ApplicationContextRegistry`, etc).

A custom pipeline factory must be constructed as follows

-   A Producer-linked channel pipeline factory must extend the abstract class `ClientInitializerFactory`.
    
-   A Consumer-linked channel pipeline factory must extend the abstract class `ServerInitializerFactory`.
    
-   The classes should override the `initChannel()` method to insert custom handler(s), encoder(s) and decoder(s). Not overriding the `initChannel()` method creates a pipeline with no handlers, encoders or decoders wired to the pipeline.
    

The example below shows how `ServerInitializerFactory` factory may be created

#### Using custom pipeline factory

_Java-only: Java class definition_

```java
public class SampleServerInitializerFactory extends ServerInitializerFactory {
    private int maxLineSize = 1024;

    protected void initChannel(Channel ch) throws Exception {
        ChannelPipeline channelPipeline = ch.pipeline();

        channelPipeline.addLast("encoder-SD", new StringEncoder(CharsetUtil.UTF_8));
        channelPipeline.addLast("decoder-DELIM", new DelimiterBasedFrameDecoder(maxLineSize, true, Delimiters.lineDelimiter()));
        channelPipeline.addLast("decoder-SD", new StringDecoder(CharsetUtil.UTF_8));
        // here we add the default Camel ServerChannelHandler for the consumer, to allow Camel to route the message, etc.
        channelPipeline.addLast("handler", new ServerChannelHandler(consumer));
    }
}
```

The custom channel pipeline factory can then be added to the registry and instantiated/utilized on a Camel route in the following way

_Java-only: Java programmatic registry and route configuration_

```java
Registry registry = camelContext.getRegistry();
ServerInitializerFactory factory = new TestServerInitializerFactory();
registry.bind("spf", factory);
context.addRoutes(new RouteBuilder() {
  public void configure() {
      String netty_ssl_endpoint =
         "netty:tcp://0.0.0.0:5150?serverInitializerFactory=#spf"
      String return_string =
         "When You Go Home, Tell Them Of Us And Say,"
         + "For Your Tomorrow, We Gave Our Today.";

      from(netty_ssl_endpoint)
       .process(new Processor() {
          public void process(Exchange exchange) throws Exception {
            exchange.getOut().setBody(return_string);
          }
       }
  }
});
```

### Reusing Netty boss and worker thread pools

Netty has two kinds of thread pools: boss and worker. By default, each Netty consumer and producer has their private thread pools. If you want to reuse these thread pools among multiple consumers or producers, then the thread pools must be created and enlisted in the Registry.

For example, using Spring XML we can create a shared worker thread pool using the `NettyWorkerPoolBuilder` with two worker threads as shown below:

```xml
<!-- use the worker pool builder to help create the shared thread pool -->
<bean id="poolBuilder" class="org.apache.camel.component.netty.NettyWorkerPoolBuilder">
  <property name="workerCount" value="2"/>
</bean>

<!-- the shared worker thread pool -->
<bean id="sharedPool" class="org.jboss.netty.channel.socket.nio.WorkerPool"
      factory-bean="poolBuilder" factory-method="build" destroy-method="shutdown">
</bean>
```

> **Tip**
> For boss thread pool there is a `org.apache.camel.component.netty.NettyServerBossPoolBuilder` builder for Netty consumers, and a `org.apache.camel.component.netty.NettyClientBossPoolBuilder` for the Netty producers.

Then in the Camel routes we can refer to this worker pools by configuring the `workerPool` option in the URI as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("netty:tcp://0.0.0.0:5021?textline=true&sync=true&workerPool=#sharedPool&usingExecutorService=false")
    .to("log:result");
```

```xml
<route>
  <from uri="netty:tcp://0.0.0.0:5021?textline=true&amp;sync=true&amp;workerPool=#sharedPool&amp;usingExecutorService=false"/>
  <to uri="log:result"/>
</route>
```

```yaml
- route:
    from:
      uri: netty:tcp://0.0.0.0:5021
      parameters:
        textline: true
        sync: true
        workerPool: "#sharedPool"
        usingExecutorService: false
      steps:
        - to:
            uri: log:result
```

And if we have another route, we can refer to the shared worker pool:

-   Java
    
-   XML
    
-   YAML
    

```java
from("netty:tcp://0.0.0.0:5022?textline=true&sync=true&workerPool=#sharedPool&usingExecutorService=false")
    .to("log:result");
```

```xml
<route>
  <from uri="netty:tcp://0.0.0.0:5022?textline=true&amp;sync=true&amp;workerPool=#sharedPool&amp;usingExecutorService=false"/>
  <to uri="log:result"/>
</route>
```

```yaml
- route:
    from:
      uri: netty:tcp://0.0.0.0:5022
      parameters:
        textline: true
        sync: true
        workerPool: "#sharedPool"
        usingExecutorService: false
      steps:
        - to:
            uri: log:result
```

And so forth.

### Multiplexing concurrent messages over a single connection with request/reply

When using Netty for request/reply messaging via the netty producer, then by default, each message is sent via a non-shared connection (pooled). This ensures that replies are automatic being able to map to the correct request thread for further routing in Camel. In other words, correlation between request/reply messages happens out-of-the-box because the replies come back on the same connection that was used for sending the request; and this connection is not shared with others. When the response comes back, the connection is returned to the connection pool, where it can be reused by others.

However, if you want to multiplex concurrent request/responses on a single shared connection, then you need to turn off the connection pooling by setting `producerPoolEnabled=false`. Now this means there is a potential issue with interleaved responses if replies come back out-of-order. Therefore, you need to have a correlation id in both the request and reply messages, so you can properly correlate the replies to the Camel callback that is responsible for continue processing the message in Camel. To do this, you need to implement `NettyCamelStateCorrelationManager` as correlation manager and configure it via the `correlationManager=#myManager` option.

> **Note**
> We recommend extending the `TimeoutCorrelationManagerSupport` when you build custom correlation managers. This provides support for timeout and other complexities you otherwise would need to implement as well.

You can find an example with the Apache Camel source code in the examples directory under the `camel-example-netty-custom-correlation` directory.

### Native transport

To enable native transport, you need to add additional dependency for epoll or kqueue depending on your OS and CPU arch. To make it easier add the following extension to your `build` section of `pom.xml`:

```xml
<extensions>
    <extension>
        <groupId>kr.motd.maven</groupId>
        <artifactId>os-maven-plugin</artifactId>
    </extension>
</extensions>
```

So then you need to add the following dependency:

-   Linux/Unix
    
-   MacOS/BSD
    

```xml
<dependency>
    <groupId>io.netty</groupId>
    <artifactId>netty-transport-native-epoll</artifactId>
    <classifier>${os.detected.classifier}</classifier>
</dependency>
```

```xml
<dependency>
    <groupId>io.netty</groupId>
    <artifactId>netty-transport-native-kqueue</artifactId>
    <classifier>${os.detected.classifier}</classifier>
</dependency>
```

## Examples

### A UDP Netty endpoint using Request-Reply and serialized object payload

Note that Object serialization is not allowed by default, and so a decoder must be configured.

_Java-only: Java annotation and class definition_

```java
@BindToRegistry("decoder")
public ChannelHandler getDecoder() throws Exception {
    return new DefaultChannelHandlerFactory() {
        @Override
        public ChannelHandler newChannelHandler() {
            return new DatagramPacketObjectDecoder(ClassResolvers.weakCachingResolver(null));
        }
    };
}

RouteBuilder builder = new RouteBuilder() {
  public void configure() {
    from("netty:udp://0.0.0.0:5155?sync=true&decoders=#decoder")
      .process(new Processor() {
         public void process(Exchange exchange) throws Exception {
           Poetry poetry = (Poetry) exchange.getIn().getBody();
           // Process poetry in some way
           exchange.getOut().setBody("Message received);
         }
       }
    }
};
```

### A TCP-based Netty consumer endpoint using One-way communication

_Java-only: Java RouteBuilder class_

```java
RouteBuilder builder = new RouteBuilder() {
  public void configure() {
       from("netty:tcp://0.0.0.0:5150")
           .to("mock:result");
  }
};
```

### An SSL/TCP-based Netty consumer endpoint using Request-Reply communication

Using the JSSE Configuration Utility

The Netty component supports SSL/TLS configuration through the [Camel JSSE Configuration Utility](../../manual/camel-configuration-utilities.md). This utility greatly decreases the amount of component-specific code you need to write and is configurable at the endpoint and component levels. The following examples demonstrate how to use the utility with the Netty component.

Programmatic configuration of the component

_Java-only: Java programmatic SSL configuration_

```java
KeyStoreParameters ksp = new KeyStoreParameters();
ksp.setResource("/users/home/server/keystore.jks");
ksp.setPassword("keystorePassword");

KeyManagersParameters kmp = new KeyManagersParameters();
kmp.setKeyStore(ksp);
kmp.setKeyPassword("keyPassword");

SSLContextParameters scp = new SSLContextParameters();
scp.setKeyManagers(kmp);

NettyComponent nettyComponent = getContext().getComponent("netty", NettyComponent.class);
nettyComponent.getConfiguration().setSslContextParameters(scp);
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
  </camel:sslContextParameters>...
...
  <to uri="netty:tcp://0.0.0.0:5150?sync=true&ssl=true&sslContextParameters=#sslContextParameters"/>
...
```

Using Basic SSL/TLS configuration on the Jetty Component

_Java-only: Java programmatic SSL route configuration_

```java
context.addRoutes(new RouteBuilder() {
  public void configure() {
      String netty_ssl_endpoint =
         "netty:tcp://0.0.0.0:5150?sync=true&ssl=true&passphrase=changeit"
         + "&keyStoreResource=file:src/test/resources/keystore.jks&trustStoreResource=file:src/test/resources/keystore.jks";
      String return_string =
         "When You Go Home, Tell Them Of Us And Say,"
         + "For Your Tomorrow, We Gave Our Today.";

      from(netty_ssl_endpoint)
       .process(new Processor() {
          public void process(Exchange exchange) throws Exception {
            exchange.getOut().setBody(return_string);
          }
       }
  }
});
```

Getting access to SSLSession and the client certificate

You can get access to the `javax.net.ssl.SSLSession` if you e.g., need to get details about the client certificate. When `ssl=true` then the [Netty](#) component will store the `SSLSession` as a header on the Camel Message as shown below:

_Java-only: Java SSL session API_

```java
SSLSession session = exchange.getIn().getHeader(NettyConstants.NETTY_SSL_SESSION, SSLSession.class);
// get the first certificate which is client certificate
javax.security.cert.X509Certificate cert = session.getPeerCertificateChain()[0];
Principal principal = cert.getSubjectDN();
```

Remember to set `needClientAuth=true` to authenticate the client, otherwise `SSLSession` cannot access information about the client certificate, and you may get an exception `javax.net.ssl.SSLPeerUnverifiedException: peer not authenticated`. You may also get this exception if the client certificate is expired or not valid, etc.

> **Tip**
> The option `sslClientCertHeaders` can be set to `true` which then enriches the Camel Message with headers having details about the client certificate. For example, the subject name is readily available in the header `CamelNettySSLClientCertSubjectName`.

## Spring Boot Auto-Configuration

When using netty with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-netty-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 76 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.netty.allow-default-codec** | The netty component installs a default codec if both, encoder/decoder is null and textline is false. Setting allowDefaultCodec to false prevents the netty component from installing a default codec as the first element in the filter chain. | true | Boolean |
| **camel.component.netty.allow-serialized-headers** | Only used for TCP when transferExchange is true. When set to true, serializable objects in headers and properties will be added to the exchange. Otherwise Camel will exclude any non-serializable objects and log it at WARN level. | false | Boolean |
| **camel.component.netty.auto-append-delimiter** | Whether or not to auto append missing end delimiter when sending using the textline codec. | true | Boolean |
| **camel.component.netty.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.netty.backlog** | Allows to configure a backlog for netty consumer (server). Note the backlog is just a best effort depending on the OS. Setting this option to a value such as 200, 500 or 1000, tells the TCP stack how long the accept queue can be If this option is not configured, then the backlog depends on OS setting. |  | Integer |
| **camel.component.netty.boss-count** | When netty works on nio mode, it uses default bossCount parameter from Netty, which is 1. User can use this option to override the default bossCount from Netty. | 1 | Integer |
| **camel.component.netty.boss-group** | Set the BossGroup which could be used for handling the new connection of the server side across the NettyEndpoint. The option is a io.netty.channel.EventLoopGroup type. |  | EventLoopGroup |
| **camel.component.netty.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.netty.broadcast** | Setting to choose Multicast over UDP. | false | Boolean |
| **camel.component.netty.channel-group** | To use an explicit ChannelGroup. The option is a io.netty.channel.group.ChannelGroup type. |  | ChannelGroup |
| **camel.component.netty.client-initializer-factory** | To use a custom ClientInitializerFactory. The option is a org.apache.camel.component.netty.ClientInitializerFactory type. |  | ClientInitializerFactory |
| **camel.component.netty.client-mode** | If the clientMode is true, netty consumer will connect the address as a TCP client. | false | Boolean |
| **camel.component.netty.configuration** | To use the NettyConfiguration as configuration when creating endpoints. The option is a org.apache.camel.component.netty.NettyConfiguration type. |  | NettyConfiguration |
| **camel.component.netty.connect-timeout** | Time to wait for a socket connection to be available. Value is in milliseconds. | 10000 | Integer |
| **camel.component.netty.correlation-manager** | To use a custom correlation manager to manage how request and reply messages are mapped when using request/reply with the netty producer. This should only be used if you have a way to map requests together with replies such as if there is correlation ids in both the request and reply messages. This can be used if you want to multiplex concurrent messages on the same channel (aka connection) in netty. When doing this you must have a way to correlate the request and reply messages so you can store the right reply on the inflight Camel Exchange before its continued routed. We recommend extending the TimeoutCorrelationManagerSupport when you build custom correlation managers. This provides support for timeout and other complexities you otherwise would need to implement as well. See also the producerPoolEnabled option for more details. The option is a org.apache.camel.component.netty.NettyCamelStateCorrelationManager type. |  | NettyCamelStateCorrelationManager |
| **camel.component.netty.decoder-max-line-length** | The max line length to use for the textline codec. | 1024 | Integer |
| **camel.component.netty.decoders** | A list of decoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | String |
| **camel.component.netty.delimiter** | The delimiter to use for the textline codec. Possible values are LINE and NULL. | line | TextLineDelimiter |
| **camel.component.netty.disconnect** | Whether or not to disconnect(close) from Netty Channel right after use. | false | Boolean |
| **camel.component.netty.disconnect-on-no-reply** | If sync is enabled then this option dictates NettyConsumer if it should disconnect where there is no reply to send back. | true | Boolean |
| **camel.component.netty.enabled** | Whether to enable auto configuration of the netty component. This is enabled by default. |  | Boolean |
| **camel.component.netty.enabled-protocols** | Which protocols to enable when using SSL. | TLSv1.2,TLSv1.3 | String |
| **camel.component.netty.encoders** | A list of encoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | String |
| **camel.component.netty.encoding** | The encoding (a charset name) to use for the textline codec. If not provided, Camel will use the JVM default Charset. |  | String |
| **camel.component.netty.executor-service** | To use the given custom EventExecutorGroup. The option is a io.netty.util.concurrent.EventExecutorGroup type. |  | EventExecutorGroup |
| **camel.component.netty.hostname-verification** | To enable/disable hostname verification on SSLEngine. | false | Boolean |
| **camel.component.netty.keep-alive** | Setting to ensure socket is not closed due to inactivity. | true | Boolean |
| **camel.component.netty.key-store-format** | Keystore format to be used for payload encryption. Defaults to JKS if not set. |  | String |
| **camel.component.netty.key-store-resource** | Client side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **camel.component.netty.lazy-channel-creation** | Channels can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | Boolean |
| **camel.component.netty.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.netty.maximum-pool-size** | Sets a maximum thread pool size for the netty consumer ordered thread pool. The default size is 2 x cpu\_core plus 1. Setting this value to eg 10 will then use 10 threads unless 2 x cpu\_core plus 1 is a higher value, which then will override and be used. For example if there are 8 cores, then the consumer thread pool will be 17. This thread pool is used to route messages received from Netty by Camel. We use a separate thread pool to ensure ordering of messages and also in case some messages will block, then nettys worker threads (event loop) wont be affected. |  | Integer |
| **camel.component.netty.native-transport** | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | Boolean |
| **camel.component.netty.need-client-auth** | Configures whether the server needs client authentication when using SSL. | false | Boolean |
| **camel.component.netty.netty-server-bootstrap-factory** | To use a custom NettyServerBootstrapFactory. The option is a org.apache.camel.component.netty.NettyServerBootstrapFactory type. |  | NettyServerBootstrapFactory |
| **camel.component.netty.network-interface** | When using UDP then this option can be used to specify a network interface by its name, such as eth0 to join a multicast group. |  | String |
| **camel.component.netty.no-reply-log-level** | If sync is enabled this option dictates NettyConsumer which logging level to use when logging a there is no reply to send back. | warn | LoggingLevel |
| **camel.component.netty.options** | Allows to configure additional netty options using option. as prefix. For example option.child.keepAlive=false. See the Netty documentation for possible options that can be used. This is a multi-value option with prefix: option. |  | Map |
| **camel.component.netty.passphrase** | Password to use for the keyStore and trustStore. The same password must be configured for both resources. |  | String |
| **camel.component.netty.producer-pool-block-when-exhausted** | Sets the value for the blockWhenExhausted configuration attribute. It determines whether to block when the borrowObject() method is invoked when the pool is exhausted (the maximum number of active objects has been reached). | true | Boolean |
| **camel.component.netty.producer-pool-enabled** | Whether producer pool is enabled or not. Important: If you turn this off then a single shared connection is used for the producer, also if you are doing request/reply. That means there is a potential issue with interleaved responses if replies comes back out-of-order. Therefore you need to have a correlation id in both the request and reply messages so you can properly correlate the replies to the Camel callback that is responsible for continue processing the message in Camel. To do this you need to implement NettyCamelStateCorrelationManager as correlation manager and configure it via the correlationManager option. See also the correlationManager option for more details. | true | Boolean |
| **camel.component.netty.producer-pool-max-idle** | Sets the cap on the number of idle instances in the pool. | 100 | Integer |
| **camel.component.netty.producer-pool-max-total** | Sets the cap on the number of objects that can be allocated by the pool (checked out to clients, or idle awaiting checkout) at a given time. Use a negative value for no limit. Be careful to not set this value too low (such as 1) as the pool must have space to create a producer such as when performing retries. Be mindful that the option producerPoolBlockWhenExhausted is default true, and the pool will then block when there is no space, which can lead to the application to hang. | \-1 | Integer |
| **camel.component.netty.producer-pool-max-wait** | Sets the maximum duration (value in millis) the borrowObject() method should block before throwing an exception when the pool is exhausted and producerPoolBlockWhenExhausted is true. When less than 0, the borrowObject() method may block indefinitely. | \-1 | Long |
| **camel.component.netty.producer-pool-min-evictable-idle** | Sets the minimum amount of time (value in millis) an object may sit idle in the pool before it is eligible for eviction by the idle object evictor. | 300000 | Long |
| **camel.component.netty.producer-pool-min-idle** | Sets the minimum number of instances allowed in the producer pool before the evictor thread (if active) spawns new objects. |  | Integer |
| **camel.component.netty.receive-buffer-size** | The TCP/UDP buffer sizes to be used during inbound communication. Size is bytes. | 65536 | Integer |
| **camel.component.netty.receive-buffer-size-predictor** | Configures the buffer size predictor. See details at Jetty documentation and this mail thread. |  | Integer |
| **camel.component.netty.reconnect** | Used only in clientMode in consumer, the consumer will attempt to reconnect on disconnection if this is enabled. | true | Boolean |
| **camel.component.netty.reconnect-interval** | Used if reconnect and clientMode is enabled. The interval in milli seconds to attempt reconnection. | 10000 | Integer |
| **camel.component.netty.request-timeout** | Allows to use a timeout for the Netty producer when calling a remote server. By default no timeout is in use. The value is in milli seconds, so eg 30000 is 30 seconds. The requestTimeout is using Netty’s ReadTimeoutHandler to trigger the timeout. |  | Long |
| **camel.component.netty.reuse-address** | Setting to facilitate socket multiplexing. | true | Boolean |
| **camel.component.netty.reuse-channel** | This option allows producers and consumers (in client mode) to reuse the same Netty Channel for the lifecycle of processing the Exchange. This is useful if you need to call a server multiple times in a Camel route and want to use the same network connection. When using this, the channel is not returned to the connection pool until the Exchange is done; or disconnected if the disconnect option is set to true. The reused Channel is stored on the Exchange as an exchange property with the key CamelNettyChannel which allows you to obtain the channel during routing and use it as well. | false | Boolean |
| **camel.component.netty.security-provider** | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | String |
| **camel.component.netty.send-buffer-size** | The TCP/UDP buffer sizes to be used during outbound communication. Size is bytes. | 65536 | Integer |
| **camel.component.netty.server-closed-channel-exception-caught-log-level** | If the server (NettyConsumer) catches an java.nio.channels.ClosedChannelException then its logged using this logging level. This is used to avoid logging the closed channel exceptions, as clients can disconnect abruptly and then cause a flood of closed exceptions in the Netty server. | debug | LoggingLevel |
| **camel.component.netty.server-exception-caught-log-level** | If the server (NettyConsumer) catches an exception then its logged using this logging level. | warn | LoggingLevel |
| **camel.component.netty.server-initializer-factory** | To use a custom ServerInitializerFactory. The option is a org.apache.camel.component.netty.ServerInitializerFactory type. |  | ServerInitializerFactory |
| **camel.component.netty.shutdown-timeout** | Shutdown await timeout in milliseconds. | 100 | Integer |
| **camel.component.netty.ssl** | Setting to specify whether SSL encryption is applied to this endpoint. | false | Boolean |
| **camel.component.netty.ssl-client-cert-headers** | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | Boolean |
| **camel.component.netty.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.netty.ssl-handler** | Reference to a class that could be used to return an SSL Handler. The option is a io.netty.handler.ssl.SslHandler type. |  | SslHandler |
| **camel.component.netty.sync** | Setting to set endpoint as one-way (false) or request-response (true). | true | Boolean |
| **camel.component.netty.tcp-no-delay** | Setting to improve TCP protocol performance. | true | Boolean |
| **camel.component.netty.textline** | Only used for TCP. If no codec is specified, you can use this flag to indicate a text line based codec; if not specified or the value is false, then Object Serialization is assumed over TCP - however only Strings are allowed to be serialized by default. | false | Boolean |
| **camel.component.netty.transfer-exchange** | Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | Boolean |
| **camel.component.netty.trust-store-resource** | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **camel.component.netty.udp-byte-array-codec** | For UDP only. If enabled the using byte array codec instead of Java serialization protocol. | false | Boolean |
| **camel.component.netty.udp-connectionless-sending** | This option supports connection less udp sending which is a real fire and forget. A connected udp send receive the PortUnreachableException if no one is listen on the receiving port. | false | Boolean |
| **camel.component.netty.unix-domain-socket-path** | Path to unix domain socket to use instead of inet socket. Host and port parameters will not be used, however required. It is ok to set dummy values for them. Must be used with nativeTransport=true and clientMode=false. |  | String |
| **camel.component.netty.use-byte-buf** | If the useByteBuf is true, netty producer will turn the message body into ByteBuf before sending it out. | false | Boolean |
| **camel.component.netty.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.netty.using-executor-service** | Whether to use ordered thread pool, to ensure events are processed orderly on the same channel. | true | Boolean |
| **camel.component.netty.worker-count** | When netty works on nio mode, it uses default workerCount parameter from Netty (which is cpu\_core\_threads x 2). User can use this option to override the default workerCount from Netty. |  | Integer |
| **camel.component.netty.worker-group** | To use a explicit EventLoopGroup as the boss thread pool. For example to share a thread pool with multiple consumers or producers. By default each consumer or producer has their own worker pool with 2 x cpu count core threads. The option is a io.netty.channel.EventLoopGroup type. |  | EventLoopGroup |