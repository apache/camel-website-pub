# camel-netty-http-kafka-connector source configuration

Connector Description: Netty HTTP server and client using the Netty 4.x.

When using camel-netty-http-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-netty-http-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.nettyhttp.CamelNettyhttpSourceConnector
```

The camel-netty-http source connector supports 136 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.source.path.protocol** | 
**Required** The protocol to use which is either http, https or proxy (consumer only). One of: \[http\] \[https\] \[proxy\].

Enum values:

-   http
    
-   https
    
-   proxy
    





 |  | HIGH |
| **camel.source.path.host** | **Required** The local hostname such as localhost, or 0.0.0.0 when being a consumer. The remote HTTP server hostname when using producer. |  | HIGH |
| **camel.source.path.port** | The host port number. |  | MEDIUM |
| **camel.source.path.path** | Resource path. |  | MEDIUM |
| **camel.source.endpoint.bridgeEndpoint** | If the option is true, the producer will ignore the NettyHttpConstants.HTTP\_URI header, and use the endpoint’s URI for request. You may also set the throwExceptionOnFailure to be false to let the producer send all the fault response back. The consumer working in the bridge mode will skip the gzip compression and WWW URL form encoding (by adding the Exchange.SKIP\_GZIP\_ENCODING and Exchange.SKIP\_WWW\_FORM\_URLENCODED headers to the consumed exchange). | false | MEDIUM |
| **camel.source.endpoint.disconnect** | Whether or not to disconnect(close) from Netty Channel right after use. | false | MEDIUM |
| **camel.source.endpoint.keepAlive** | Setting to ensure socket is not closed due to inactivity. | true | MEDIUM |
| **camel.source.endpoint.reuseAddress** | Setting to facilitate socket multiplexing. | true | MEDIUM |
| **camel.source.endpoint.reuseChannel** | This option allows producers and consumers (in client mode) to reuse the same Netty Channel for the lifecycle of processing the Exchange. This is useful if you need to call a server multiple times in a Camel route and want to use the same network connection. When using this, the channel is not returned to the connection pool until the Exchange is done; or disconnected if the disconnect option is set to true. The reused Channel is stored on the Exchange as an exchange property with the key CamelNettyChannel which allows you to obtain the channel during routing and use it as well. | false | MEDIUM |
| **camel.source.endpoint.sync** | Setting to set endpoint as one-way (false) or request-response (true). | true | MEDIUM |
| **camel.source.endpoint.tcpNoDelay** | Setting to improve TCP protocol performance. | true | MEDIUM |
| **camel.source.endpoint.matchOnUriPrefix** | Whether or not Camel should try to find a target consumer by matching the URI prefix if no exact match is found. | false | MEDIUM |
| **camel.source.endpoint.muteException** | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | MEDIUM |
| **camel.source.endpoint.send503whenSuspended** | Whether to send back HTTP status code 503 when the consumer has been suspended. If the option is false then the Netty Acceptor is unbound when the consumer is suspended, so clients cannot connect anymore. | true | MEDIUM |
| **camel.source.endpoint.backlog** | Allows to configure a backlog for netty consumer (server). Note the backlog is just a best effort depending on the OS. Setting this option to a value such as 200, 500 or 1000, tells the TCP stack how long the accept queue can be If this option is not configured, then the backlog depends on OS setting. |  | MEDIUM |
| **camel.source.endpoint.bossCount** | When netty works on nio mode, it uses default bossCount parameter from Netty, which is 1. User can use this option to override the default bossCount from Netty. | 1 | MEDIUM |
| **camel.source.endpoint.bossGroup** | Set the BossGroup which could be used for handling the new connection of the server side across the NettyEndpoint. |  | MEDIUM |
| **camel.source.endpoint.bridgeErrorHandler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | MEDIUM |
| **camel.source.endpoint.chunkedMaxContentLength** | Value in bytes the max content length per chunked frame received on the Netty HTTP server. | 1048576 | MEDIUM |
| **camel.source.endpoint.compression** | Allow using gzip/deflate for compression on the Netty HTTP server if the client supports it from the HTTP headers. | false | MEDIUM |
| **camel.source.endpoint.disconnectOnNoReply** | If sync is enabled then this option dictates NettyConsumer if it should disconnect where there is no reply to send back. | true | MEDIUM |
| **camel.source.endpoint.exceptionHandler** | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | MEDIUM |
| **camel.source.endpoint.exchangePattern** | 

Sets the exchange pattern when the consumer creates an exchange. One of: \[InOnly\] \[InOut\].

Enum values:

-   InOnly
    
-   InOut
    





 |  | MEDIUM |
| **camel.source.endpoint.httpMethodRestrict** | To disable HTTP methods on the Netty HTTP consumer. You can specify multiple separated by comma. |  | MEDIUM |
| **camel.source.endpoint.logWarnOnBadRequest** | Whether Netty HTTP server should log a WARN if decoding the HTTP request failed and a HTTP Status 400 (bad request) is returned. | true | MEDIUM |
| **camel.source.endpoint.mapHeaders** | If this option is enabled, then during binding from Netty to Camel Message then the headers will be mapped as well (eg added as header to the Camel Message as well). You can turn off this option to disable this. The headers can still be accessed from the org.apache.camel.component.netty.http.NettyHttpMessage message with the method getHttpRequest() that returns the Netty HTTP request io.netty.handler.codec.http.HttpRequest instance. | true | MEDIUM |
| **camel.source.endpoint.maxChunkSize** | The maximum length of the content or each chunk. If the content length (or the length of each chunk) exceeds this value, the content or chunk will be split into multiple io.netty.handler.codec.http.HttpContents whose length is maxChunkSize at maximum. See io.netty.handler.codec.http.HttpObjectDecoder. | 8192 | MEDIUM |
| **camel.source.endpoint.maxHeaderSize** | The maximum length of all headers. If the sum of the length of each header exceeds this value, a io.netty.handler.codec.TooLongFrameException will be raised. | 8192 | MEDIUM |
| **camel.source.endpoint.maxInitialLineLength** | The maximum length of the initial line (e.g. \\{code GET / HTTP/1.0} or \\{code HTTP/1.0 200 OK}) If the length of the initial line exceeds this value, a TooLongFrameException will be raised. See io.netty.handler.codec.http.HttpObjectDecoder. | 4096 | MEDIUM |
| **camel.source.endpoint.nettyServerBootstrapFactory** | To use a custom NettyServerBootstrapFactory. |  | MEDIUM |
| **camel.source.endpoint.nettySharedHttpServer** | To use a shared Netty HTTP server. See Netty HTTP Server Example for more details. |  | MEDIUM |
| **camel.source.endpoint.noReplyLogLevel** | 

If sync is enabled this option dictates NettyConsumer which logging level to use when logging a there is no reply to send back. One of: \[TRACE\] \[DEBUG\] \[INFO\] \[WARN\] \[ERROR\] \[OFF\].

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | "WARN" | MEDIUM |
| **camel.source.endpoint.serverClosedChannelExceptionCaughtLogLevel** | 

If the server (NettyConsumer) catches an java.nio.channels.ClosedChannelException then its logged using this logging level. This is used to avoid logging the closed channel exceptions, as clients can disconnect abruptly and then cause a flood of closed exceptions in the Netty server. One of: \[TRACE\] \[DEBUG\] \[INFO\] \[WARN\] \[ERROR\] \[OFF\].

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | "DEBUG" | MEDIUM |
| **camel.source.endpoint.serverExceptionCaughtLogLevel** | 

If the server (NettyConsumer) catches an exception then its logged using this logging level. One of: \[TRACE\] \[DEBUG\] \[INFO\] \[WARN\] \[ERROR\] \[OFF\].

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | "WARN" | MEDIUM |
| **camel.source.endpoint.serverInitializerFactory** | To use a custom ServerInitializerFactory. |  | MEDIUM |
| **camel.source.endpoint.traceEnabled** | Specifies whether to enable HTTP TRACE for this Netty HTTP consumer. By default TRACE is turned off. | false | MEDIUM |
| **camel.source.endpoint.urlDecodeHeaders** | If this option is enabled, then during binding from Netty to Camel Message then the header values will be URL decoded (eg %20 will be a space character. Notice this option is used by the default org.apache.camel.component.netty.http.NettyHttpBinding and therefore if you implement a custom org.apache.camel.component.netty.http.NettyHttpBinding then you would need to decode the headers accordingly to this option. | false | MEDIUM |
| **camel.source.endpoint.usingExecutorService** | Whether to use ordered thread pool, to ensure events are processed orderly on the same channel. | true | MEDIUM |
| **camel.source.endpoint.allowSerializedHeaders** | Only used for TCP when transferExchange is true. When set to true, serializable objects in headers and properties will be added to the exchange. Otherwise Camel will exclude any non-serializable objects and log it at WARN level. | false | MEDIUM |
| **camel.source.endpoint.channelGroup** | To use an explicit ChannelGroup. |  | MEDIUM |
| **camel.source.endpoint.configuration** | To use a custom configured NettyHttpConfiguration for configuring this endpoint. |  | MEDIUM |
| **camel.source.endpoint.disableStreamCache** | Determines whether or not the raw input stream from Netty HttpRequest#getContent() or HttpResponset#getContent() is cached or not (Camel will read the stream into a in light-weight memory based Stream caching) cache. By default Camel will cache the Netty input stream to support reading it multiple times to ensure it Camel can retrieve all data from the stream. However you can set this option to true when you for example need to access the raw stream, such as streaming it directly to a file or other persistent store. Mind that if you enable this option, then you cannot read the Netty stream multiple times out of the box, and you would need manually to reset the reader index on the Netty raw stream. Also Netty will auto-close the Netty stream when the Netty HTTP server/HTTP client is done processing, which means that if the asynchronous routing engine is in use then any asynchronous thread that may continue routing the org.apache.camel.Exchange may not be able to read the Netty stream, because Netty has closed it. | false | MEDIUM |
| **camel.source.endpoint.headerFilterStrategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter headers. |  | MEDIUM |
| **camel.source.endpoint.nativeTransport** | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | MEDIUM |
| **camel.source.endpoint.nettyHttpBinding** | To use a custom org.apache.camel.component.netty.http.NettyHttpBinding for binding to/from Netty and Camel Message API. |  | MEDIUM |
| **camel.source.endpoint.options** | Allows to configure additional netty options using option. as prefix. For example option.child.keepAlive=false. See the Netty documentation for possible options that can be used. This is a multi-value option with prefix: option. |  | MEDIUM |
| **camel.source.endpoint.receiveBufferSize** | The TCP/UDP buffer sizes to be used during inbound communication. Size is bytes. | 65536 | MEDIUM |
| **camel.source.endpoint.receiveBufferSizePredictor** | Configures the buffer size predictor. See details at Jetty documentation and this mail thread. |  | MEDIUM |
| **camel.source.endpoint.sendBufferSize** | The TCP/UDP buffer sizes to be used during outbound communication. Size is bytes. | 65536 | MEDIUM |
| **camel.source.endpoint.shutdownTimeout** | Shutdown await timeout in milliseconds. | 100 | MEDIUM |
| **camel.source.endpoint.synchronous** | Sets whether synchronous processing should be strictly used. | false | MEDIUM |
| **camel.source.endpoint.transferException** | If enabled and an Exchange failed processing on the consumer side, and if the caused Exception was send back serialized in the response as a application/x-java-serialized-object content type. On the producer side the exception will be deserialized and thrown as is, instead of the HttpOperationFailedException. The caused exception is required to be serialized. This is by default turned off. If you enable this then be aware that Java will deserialize the incoming data from the request to Java and that can be a potential security risk. | false | MEDIUM |
| **camel.source.endpoint.transferExchange** | Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | MEDIUM |
| **camel.source.endpoint.unixDomainSocketPath** | Path to unix domain socket to use instead of inet socket. Host and port parameters will not be used, however required. It is ok to set dummy values for them. Must be used with nativeTransport=true and clientMode=false. |  | MEDIUM |
| **camel.source.endpoint.workerCount** | When netty works on nio mode, it uses default workerCount parameter from Netty (which is cpu\_core\_threads x 2). User can use this option to override the default workerCount from Netty. |  | MEDIUM |
| **camel.source.endpoint.workerGroup** | To use a explicit EventLoopGroup as the boss thread pool. For example to share a thread pool with multiple consumers or producers. By default each consumer or producer has their own worker pool with 2 x cpu count core threads. |  | MEDIUM |
| **camel.source.endpoint.decoders** | A list of decoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | MEDIUM |
| **camel.source.endpoint.encoders** | A list of encoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | MEDIUM |
| **camel.source.endpoint.enabledProtocols** | Which protocols to enable when using SSL. | "TLSv1.2,TLSv1.3" | MEDIUM |
| **camel.source.endpoint.hostnameVerification** | To enable/disable hostname verification on SSLEngine. | false | MEDIUM |
| **camel.source.endpoint.keyStoreFormat** | Keystore format to be used for payload encryption. Defaults to JKS if not set. |  | MEDIUM |
| **camel.source.endpoint.keyStoreResource** | Client side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | MEDIUM |
| **camel.source.endpoint.needClientAuth** | Configures whether the server needs client authentication when using SSL. | false | MEDIUM |
| **camel.source.endpoint.passphrase** | Password to use for the keyStore and trustStore. The same password must be configured for both resources. |  | MEDIUM |
| **camel.source.endpoint.securityConfiguration** | Refers to a org.apache.camel.component.netty.http.NettyHttpSecurityConfiguration for configuring secure web resources. |  | MEDIUM |
| **camel.source.endpoint.securityOptions** | To configure NettyHttpSecurityConfiguration using key/value pairs from the map. This is a multi-value option with prefix: securityConfiguration. |  | MEDIUM |
| **camel.source.endpoint.securityProvider** | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | MEDIUM |
| **camel.source.endpoint.ssl** | Setting to specify whether SSL encryption is applied to this endpoint. | false | MEDIUM |
| **camel.source.endpoint.sslClientCertHeaders** | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | MEDIUM |
| **camel.source.endpoint.sslContextParameters** | To configure security using SSLContextParameters. |  | MEDIUM |
| **camel.source.endpoint.sslHandler** | Reference to a class that could be used to return an SSL Handler. |  | MEDIUM |
| **camel.source.endpoint.trustStoreResource** | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | MEDIUM |
| **camel.component.netty-http.configuration** | To use the NettyConfiguration as configuration when creating endpoints. |  | MEDIUM |
| **camel.component.netty-http.disconnect** | Whether or not to disconnect(close) from Netty Channel right after use. | false | MEDIUM |
| **camel.component.netty-http.keepAlive** | Setting to ensure socket is not closed due to inactivity. | true | MEDIUM |
| **camel.component.netty-http.reuseAddress** | Setting to facilitate socket multiplexing. | true | MEDIUM |
| **camel.component.netty-http.reuseChannel** | This option allows producers and consumers (in client mode) to reuse the same Netty Channel for the lifecycle of processing the Exchange. This is useful if you need to call a server multiple times in a Camel route and want to use the same network connection. When using this, the channel is not returned to the connection pool until the Exchange is done; or disconnected if the disconnect option is set to true. The reused Channel is stored on the Exchange as an exchange property with the key CamelNettyChannel which allows you to obtain the channel during routing and use it as well. | false | MEDIUM |
| **camel.component.netty-http.sync** | Setting to set endpoint as one-way (false) or request-response (true). | true | MEDIUM |
| **camel.component.netty-http.tcpNoDelay** | Setting to improve TCP protocol performance. | true | MEDIUM |
| **camel.component.netty-http.networkInterface** | When using UDP then this option can be used to specify a network interface by its name, such as eth0 to join a multicast group. |  | MEDIUM |
| **camel.component.netty-http.bridgeErrorHandler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | MEDIUM |
| **camel.component.netty-http.clientMode** | If the clientMode is true, netty consumer will connect the address as a TCP client. | false | MEDIUM |
| **camel.component.netty-http.muteException** | If enabled and an Exchange failed processing on the consumer side the response’s body won’t contain the exception’s stack trace. | false | MEDIUM |
| **camel.component.netty-http.reconnect** | Used only in clientMode in consumer, the consumer will attempt to reconnect on disconnection if this is enabled. | true | MEDIUM |
| **camel.component.netty-http.reconnectInterval** | Used if reconnect and clientMode is enabled. The interval in milli seconds to attempt reconnection. | 10000 | MEDIUM |
| **camel.component.netty-http.backlog** | Allows to configure a backlog for netty consumer (server). Note the backlog is just a best effort depending on the OS. Setting this option to a value such as 200, 500 or 1000, tells the TCP stack how long the accept queue can be If this option is not configured, then the backlog depends on OS setting. |  | MEDIUM |
| **camel.component.netty-http.bossCount** | When netty works on nio mode, it uses default bossCount parameter from Netty, which is 1. User can use this option to override the default bossCount from Netty. | 1 | MEDIUM |
| **camel.component.netty-http.bossGroup** | Set the BossGroup which could be used for handling the new connection of the server side across the NettyEndpoint. |  | MEDIUM |
| **camel.component.netty-http.broadcast** | Setting to choose Multicast over UDP. | false | MEDIUM |
| **camel.component.netty-http.disconnectOnNoReply** | If sync is enabled then this option dictates NettyConsumer if it should disconnect where there is no reply to send back. | true | MEDIUM |
| **camel.component.netty-http.executorService** | To use the given custom EventExecutorGroup. |  | MEDIUM |
| **camel.component.netty-http.maximumPoolSize** | Sets a maximum thread pool size for the netty consumer ordered thread pool. The default size is 2 x cpu\_core plus 1. Setting this value to eg 10 will then use 10 threads unless 2 x cpu\_core plus 1 is a higher value, which then will override and be used. For example if there are 8 cores, then the consumer thread pool will be 17. This thread pool is used to route messages received from Netty by Camel. We use a separate thread pool to ensure ordering of messages and also in case some messages will block, then nettys worker threads (event loop) wont be affected. |  | MEDIUM |
| **camel.component.netty-http.nettyServerBootstrapFactory** | To use a custom NettyServerBootstrapFactory. |  | MEDIUM |
| **camel.component.netty-http.noReplyLogLevel** | 

If sync is enabled this option dictates NettyConsumer which logging level to use when logging a there is no reply to send back. One of: \[TRACE\] \[DEBUG\] \[INFO\] \[WARN\] \[ERROR\] \[OFF\].

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | "WARN" | MEDIUM |
| **camel.component.netty-http.serverClosedChannelExceptionCaughtLogLevel** | 

If the server (NettyConsumer) catches an java.nio.channels.ClosedChannelException then its logged using this logging level. This is used to avoid logging the closed channel exceptions, as clients can disconnect abruptly and then cause a flood of closed exceptions in the Netty server. One of: \[TRACE\] \[DEBUG\] \[INFO\] \[WARN\] \[ERROR\] \[OFF\].

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | "DEBUG" | MEDIUM |
| **camel.component.netty-http.serverExceptionCaughtLogLevel** | 

If the server (NettyConsumer) catches an exception then its logged using this logging level. One of: \[TRACE\] \[DEBUG\] \[INFO\] \[WARN\] \[ERROR\] \[OFF\].

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | "WARN" | MEDIUM |
| **camel.component.netty-http.serverInitializerFactory** | To use a custom ServerInitializerFactory. |  | MEDIUM |
| **camel.component.netty-http.usingExecutorService** | Whether to use ordered thread pool, to ensure events are processed orderly on the same channel. | true | MEDIUM |
| **camel.component.netty-http.allowSerializedHeaders** | Only used for TCP when transferExchange is true. When set to true, serializable objects in headers and properties will be added to the exchange. Otherwise Camel will exclude any non-serializable objects and log it at WARN level. | false | MEDIUM |
| **camel.component.netty-http.autowiredEnabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | MEDIUM |
| **camel.component.netty-http.channelGroup** | To use an explicit ChannelGroup. |  | MEDIUM |
| **camel.component.netty-http.headerFilterStrategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter headers. |  | MEDIUM |
| **camel.component.netty-http.nativeTransport** | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | MEDIUM |
| **camel.component.netty-http.nettyHttpBinding** | To use a custom org.apache.camel.component.netty.http.NettyHttpBinding for binding to/from Netty and Camel Message API. |  | MEDIUM |
| **camel.component.netty-http.options** | Allows to configure additional netty options using option. as prefix. For example option.child.keepAlive=false. See the Netty documentation for possible options that can be used. This is a multi-value option with prefix: option. |  | MEDIUM |
| **camel.component.netty-http.receiveBufferSize** | The TCP/UDP buffer sizes to be used during inbound communication. Size is bytes. | 65536 | MEDIUM |
| **camel.component.netty-http.receiveBufferSizePredictor** | Configures the buffer size predictor. See details at Jetty documentation and this mail thread. |  | MEDIUM |
| **camel.component.netty-http.sendBufferSize** | The TCP/UDP buffer sizes to be used during outbound communication. Size is bytes. | 65536 | MEDIUM |
| **camel.component.netty-http.shutdownTimeout** | Shutdown await timeout in milliseconds. | 100 | MEDIUM |
| **camel.component.netty-http.transferExchange** | Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | MEDIUM |
| **camel.component.netty-http.udpByteArrayCodec** | For UDP only. If enabled the using byte array codec instead of Java serialization protocol. | false | MEDIUM |
| **camel.component.netty-http.unixDomainSocketPath** | Path to unix domain socket to use instead of inet socket. Host and port parameters will not be used, however required. It is ok to set dummy values for them. Must be used with nativeTransport=true and clientMode=false. |  | MEDIUM |
| **camel.component.netty-http.workerCount** | When netty works on nio mode, it uses default workerCount parameter from Netty (which is cpu\_core\_threads x 2). User can use this option to override the default workerCount from Netty. |  | MEDIUM |
| **camel.component.netty-http.workerGroup** | To use a explicit EventLoopGroup as the boss thread pool. For example to share a thread pool with multiple consumers or producers. By default each consumer or producer has their own worker pool with 2 x cpu count core threads. |  | MEDIUM |
| **camel.component.netty-http.allowDefaultCodec** | The netty component installs a default codec if both, encoder/decoder is null and textline is false. Setting allowDefaultCodec to false prevents the netty component from installing a default codec as the first element in the filter chain. | true | MEDIUM |
| **camel.component.netty-http.autoAppendDelimiter** | Whether or not to auto append missing end delimiter when sending using the textline codec. | true | MEDIUM |
| **camel.component.netty-http.decoderMaxLineLength** | The max line length to use for the textline codec. | 1024 | MEDIUM |
| **camel.component.netty-http.decoders** | A list of decoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | MEDIUM |
| **camel.component.netty-http.delimiter** | 

The delimiter to use for the textline codec. Possible values are LINE and NULL. One of: \[LINE\] \[NULL\].

Enum values:

-   LINE
    
-   NULL
    





 | "LINE" | MEDIUM |
| **camel.component.netty-http.encoders** | A list of encoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | MEDIUM |
| **camel.component.netty-http.encoding** | The encoding (a charset name) to use for the textline codec. If not provided, Camel will use the JVM default Charset. |  | MEDIUM |
| **camel.component.netty-http.textline** | Only used for TCP. If no codec is specified, you can use this flag to indicate a text line based codec; if not specified or the value is false, then Object Serialization is assumed over TCP - however only Strings are allowed to be serialized by default. | false | MEDIUM |
| **camel.component.netty-http.enabledProtocols** | Which protocols to enable when using SSL. | "TLSv1.2,TLSv1.3" | MEDIUM |
| **camel.component.netty-http.hostnameVerification** | To enable/disable hostname verification on SSLEngine. | false | MEDIUM |
| **camel.component.netty-http.keyStoreFormat** | Keystore format to be used for payload encryption. Defaults to JKS if not set. |  | MEDIUM |
| **camel.component.netty-http.keyStoreResource** | Client side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | MEDIUM |
| **camel.component.netty-http.needClientAuth** | Configures whether the server needs client authentication when using SSL. | false | MEDIUM |
| **camel.component.netty-http.passphrase** | Password to use for the keyStore and trustStore. The same password must be configured for both resources. |  | MEDIUM |
| **camel.component.netty-http.securityConfiguration** | Refers to a org.apache.camel.component.netty.http.NettyHttpSecurityConfiguration for configuring secure web resources. |  | MEDIUM |
| **camel.component.netty-http.securityProvider** | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | MEDIUM |
| **camel.component.netty-http.ssl** | Setting to specify whether SSL encryption is applied to this endpoint. | false | MEDIUM |
| **camel.component.netty-http.sslClientCertHeaders** | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | MEDIUM |
| **camel.component.netty-http.sslContextParameters** | To configure security using SSLContextParameters. |  | MEDIUM |
| **camel.component.netty-http.sslHandler** | Reference to a class that could be used to return an SSL Handler. |  | MEDIUM |
| **camel.component.netty-http.trustStoreResource** | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | MEDIUM |
| **camel.component.netty-http.useGlobalSslContextParameters** | Enable usage of global SSL context parameters. | false | MEDIUM |

The camel-netty-http source connector has no converters out of the box.

The camel-netty-http source connector has no transforms out of the box.

The camel-netty-http source connector has no aggregation strategies out of the box.