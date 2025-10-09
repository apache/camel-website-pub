# camel-netty-kafka-connector sink configuration

Connector Description: Socket level networking using TCP or UDP with Netty 4.x.

When using camel-netty-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-netty-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.netty.CamelNettySinkConnector
```

The camel-netty sink connector supports 115 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.sink.path.protocol** | 
**Required** The protocol to use which can be tcp or udp One of: \[tcp\] \[udp\].

Enum values:

-   tcp
    
-   udp
    





 |  | HIGH |
| **camel.sink.path.host** | **Required** The hostname. For the consumer the hostname is localhost or 0.0.0.0. For the producer the hostname is the remote host to connect to. |  | HIGH |
| **camel.sink.path.port** | **Required** The host port number. |  | HIGH |
| **camel.sink.endpoint.disconnect** | Whether or not to disconnect(close) from Netty Channel right after use. | false | MEDIUM |
| **camel.sink.endpoint.keepAlive** | Setting to ensure socket is not closed due to inactivity. | true | MEDIUM |
| **camel.sink.endpoint.reuseAddress** | Setting to facilitate socket multiplexing. | true | MEDIUM |
| **camel.sink.endpoint.reuseChannel** | This option allows producers and consumers (in client mode) to reuse the same Netty Channel for the lifecycle of processing the Exchange. This is useful if you need to call a server multiple times in a Camel route and want to use the same network connection. When using this, the channel is not returned to the connection pool until the Exchange is done; or disconnected if the disconnect option is set to true. The reused Channel is stored on the Exchange as an exchange property with the key CamelNettyChannel which allows you to obtain the channel during routing and use it as well. | false | MEDIUM |
| **camel.sink.endpoint.sync** | Setting to set endpoint as one-way (false) or request-response (true). | true | MEDIUM |
| **camel.sink.endpoint.tcpNoDelay** | Setting to improve TCP protocol performance. | true | MEDIUM |
| **camel.sink.endpoint.networkInterface** | When using UDP then this option can be used to specify a network interface by its name, such as eth0 to join a multicast group. |  | MEDIUM |
| **camel.sink.endpoint.connectTimeout** | Time to wait for a socket connection to be available. Value is in milliseconds. | 10000 | MEDIUM |
| **camel.sink.endpoint.requestTimeout** | Allows to use a timeout for the Netty producer when calling a remote server. By default no timeout is in use. The value is in milli seconds, so eg 30000 is 30 seconds. The requestTimeout is using Netty’s ReadTimeoutHandler to trigger the timeout. |  | MEDIUM |
| **camel.sink.endpoint.clientInitializerFactory** | To use a custom ClientInitializerFactory. |  | MEDIUM |
| **camel.sink.endpoint.correlationManager** | To use a custom correlation manager to manage how request and reply messages are mapped when using request/reply with the netty producer. This should only be used if you have a way to map requests together with replies such as if there is correlation ids in both the request and reply messages. This can be used if you want to multiplex concurrent messages on the same channel (aka connection) in netty. When doing this you must have a way to correlate the request and reply messages so you can store the right reply on the inflight Camel Exchange before its continued routed. We recommend extending the TimeoutCorrelationManagerSupport when you build custom correlation managers. This provides support for timeout and other complexities you otherwise would need to implement as well. See also the producerPoolEnabled option for more details. |  | MEDIUM |
| **camel.sink.endpoint.lazyChannelCreation** | Channels can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | MEDIUM |
| **camel.sink.endpoint.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.sink.endpoint.producerPoolBlockWhenExhausted** | Sets the value for the blockWhenExhausted configuration attribute. It determines whether to block when the borrowObject() method is invoked when the pool is exhausted (the maximum number of active objects has been reached). | true | MEDIUM |
| **camel.sink.endpoint.producerPoolEnabled** | Whether producer pool is enabled or not. Important: If you turn this off then a single shared connection is used for the producer, also if you are doing request/reply. That means there is a potential issue with interleaved responses if replies comes back out-of-order. Therefore you need to have a correlation id in both the request and reply messages so you can properly correlate the replies to the Camel callback that is responsible for continue processing the message in Camel. To do this you need to implement NettyCamelStateCorrelationManager as correlation manager and configure it via the correlationManager option. See also the correlationManager option for more details. | true | MEDIUM |
| **camel.sink.endpoint.producerPoolMaxIdle** | Sets the cap on the number of idle instances in the pool. | 100 | MEDIUM |
| **camel.sink.endpoint.producerPoolMaxTotal** | Sets the cap on the number of objects that can be allocated by the pool (checked out to clients, or idle awaiting checkout) at a given time. Use a negative value for no limit. Be careful to not set this value too low (such as 1) as the pool must have space to create a producer such as when performing retries. Be mindful that the option producerPoolBlockWhenExhausted is default true, and the pool will then block when there is no space, which can lead to the application to hang. | \-1 | MEDIUM |
| **camel.sink.endpoint.producerPoolMaxWait** | Sets the maximum duration (value in millis) the borrowObject() method should block before throwing an exception when the pool is exhausted and producerPoolBlockWhenExhausted is true. When less than 0, the borrowObject() method may block indefinitely. | \-1L | MEDIUM |
| **camel.sink.endpoint.producerPoolMinEvictableIdle** | Sets the minimum amount of time (value in millis) an object may sit idle in the pool before it is eligible for eviction by the idle object evictor. | 300000L | MEDIUM |
| **camel.sink.endpoint.producerPoolMinIdle** | Sets the minimum number of instances allowed in the producer pool before the evictor thread (if active) spawns new objects. |  | MEDIUM |
| **camel.sink.endpoint.udpConnectionlessSending** | This option supports connection less udp sending which is a real fire and forget. A connected udp send receive the PortUnreachableException if no one is listen on the receiving port. | false | MEDIUM |
| **camel.sink.endpoint.useByteBuf** | If the useByteBuf is true, netty producer will turn the message body into ByteBuf before sending it out. | false | MEDIUM |
| **camel.sink.endpoint.allowSerializedHeaders** | Only used for TCP when transferExchange is true. When set to true, serializable objects in headers and properties will be added to the exchange. Otherwise Camel will exclude any non-serializable objects and log it at WARN level. | false | MEDIUM |
| **camel.sink.endpoint.channelGroup** | To use an explicit ChannelGroup. |  | MEDIUM |
| **camel.sink.endpoint.nativeTransport** | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | MEDIUM |
| **camel.sink.endpoint.options** | Allows to configure additional netty options using option. as prefix. For example option.child.keepAlive=false. See the Netty documentation for possible options that can be used. This is a multi-value option with prefix: option. |  | MEDIUM |
| **camel.sink.endpoint.receiveBufferSize** | The TCP/UDP buffer sizes to be used during inbound communication. Size is bytes. | 65536 | MEDIUM |
| **camel.sink.endpoint.receiveBufferSizePredictor** | Configures the buffer size predictor. See details at Jetty documentation and this mail thread. |  | MEDIUM |
| **camel.sink.endpoint.sendBufferSize** | The TCP/UDP buffer sizes to be used during outbound communication. Size is bytes. | 65536 | MEDIUM |
| **camel.sink.endpoint.shutdownTimeout** | Shutdown await timeout in milliseconds. | 100 | MEDIUM |
| **camel.sink.endpoint.synchronous** | Sets whether synchronous processing should be strictly used. | false | MEDIUM |
| **camel.sink.endpoint.transferExchange** | Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | MEDIUM |
| **camel.sink.endpoint.udpByteArrayCodec** | For UDP only. If enabled the using byte array codec instead of Java serialization protocol. | false | MEDIUM |
| **camel.sink.endpoint.unixDomainSocketPath** | Path to unix domain socket to use instead of inet socket. Host and port parameters will not be used, however required. It is ok to set dummy values for them. Must be used with nativeTransport=true and clientMode=false. |  | MEDIUM |
| **camel.sink.endpoint.workerCount** | When netty works on nio mode, it uses default workerCount parameter from Netty (which is cpu\_core\_threads x 2). User can use this option to override the default workerCount from Netty. |  | MEDIUM |
| **camel.sink.endpoint.workerGroup** | To use a explicit EventLoopGroup as the boss thread pool. For example to share a thread pool with multiple consumers or producers. By default each consumer or producer has their own worker pool with 2 x cpu count core threads. |  | MEDIUM |
| **camel.sink.endpoint.allowDefaultCodec** | The netty component installs a default codec if both, encoder/decoder is null and textline is false. Setting allowDefaultCodec to false prevents the netty component from installing a default codec as the first element in the filter chain. | true | MEDIUM |
| **camel.sink.endpoint.autoAppendDelimiter** | Whether or not to auto append missing end delimiter when sending using the textline codec. | true | MEDIUM |
| **camel.sink.endpoint.decoderMaxLineLength** | The max line length to use for the textline codec. | 1024 | MEDIUM |
| **camel.sink.endpoint.decoders** | A list of decoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | MEDIUM |
| **camel.sink.endpoint.delimiter** | 

The delimiter to use for the textline codec. Possible values are LINE and NULL. One of: \[LINE\] \[NULL\].

Enum values:

-   LINE
    
-   NULL
    





 | "LINE" | MEDIUM |
| **camel.sink.endpoint.encoders** | A list of encoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | MEDIUM |
| **camel.sink.endpoint.encoding** | The encoding (a charset name) to use for the textline codec. If not provided, Camel will use the JVM default Charset. |  | MEDIUM |
| **camel.sink.endpoint.textline** | Only used for TCP. If no codec is specified, you can use this flag to indicate a text line based codec; if not specified or the value is false, then Object Serialization is assumed over TCP - however only Strings are allowed to be serialized by default. | false | MEDIUM |
| **camel.sink.endpoint.enabledProtocols** | Which protocols to enable when using SSL. | "TLSv1.2,TLSv1.3" | MEDIUM |
| **camel.sink.endpoint.hostnameVerification** | To enable/disable hostname verification on SSLEngine. | false | MEDIUM |
| **camel.sink.endpoint.keyStoreFormat** | Keystore format to be used for payload encryption. Defaults to JKS if not set. |  | MEDIUM |
| **camel.sink.endpoint.keyStoreResource** | Client side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | MEDIUM |
| **camel.sink.endpoint.passphrase** | Password to use for the keyStore and trustStore. The same password must be configured for both resources. |  | MEDIUM |
| **camel.sink.endpoint.securityProvider** | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | MEDIUM |
| **camel.sink.endpoint.ssl** | Setting to specify whether SSL encryption is applied to this endpoint. | false | MEDIUM |
| **camel.sink.endpoint.sslClientCertHeaders** | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | MEDIUM |
| **camel.sink.endpoint.sslContextParameters** | To configure security using SSLContextParameters. |  | MEDIUM |
| **camel.sink.endpoint.sslHandler** | Reference to a class that could be used to return an SSL Handler. |  | MEDIUM |
| **camel.sink.endpoint.trustStoreResource** | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | MEDIUM |
| **camel.component.netty.configuration** | To use the NettyConfiguration as configuration when creating endpoints. |  | MEDIUM |
| **camel.component.netty.disconnect** | Whether or not to disconnect(close) from Netty Channel right after use. | false | MEDIUM |
| **camel.component.netty.keepAlive** | Setting to ensure socket is not closed due to inactivity. | true | MEDIUM |
| **camel.component.netty.reuseAddress** | Setting to facilitate socket multiplexing. | true | MEDIUM |
| **camel.component.netty.reuseChannel** | This option allows producers and consumers (in client mode) to reuse the same Netty Channel for the lifecycle of processing the Exchange. This is useful if you need to call a server multiple times in a Camel route and want to use the same network connection. When using this, the channel is not returned to the connection pool until the Exchange is done; or disconnected if the disconnect option is set to true. The reused Channel is stored on the Exchange as an exchange property with the key CamelNettyChannel which allows you to obtain the channel during routing and use it as well. | false | MEDIUM |
| **camel.component.netty.sync** | Setting to set endpoint as one-way (false) or request-response (true). | true | MEDIUM |
| **camel.component.netty.tcpNoDelay** | Setting to improve TCP protocol performance. | true | MEDIUM |
| **camel.component.netty.networkInterface** | When using UDP then this option can be used to specify a network interface by its name, such as eth0 to join a multicast group. |  | MEDIUM |
| **camel.component.netty.connectTimeout** | Time to wait for a socket connection to be available. Value is in milliseconds. | 10000 | MEDIUM |
| **camel.component.netty.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.component.netty.requestTimeout** | Allows to use a timeout for the Netty producer when calling a remote server. By default no timeout is in use. The value is in milli seconds, so eg 30000 is 30 seconds. The requestTimeout is using Netty’s ReadTimeoutHandler to trigger the timeout. |  | MEDIUM |
| **camel.component.netty.clientInitializerFactory** | To use a custom ClientInitializerFactory. |  | MEDIUM |
| **camel.component.netty.correlationManager** | To use a custom correlation manager to manage how request and reply messages are mapped when using request/reply with the netty producer. This should only be used if you have a way to map requests together with replies such as if there is correlation ids in both the request and reply messages. This can be used if you want to multiplex concurrent messages on the same channel (aka connection) in netty. When doing this you must have a way to correlate the request and reply messages so you can store the right reply on the inflight Camel Exchange before its continued routed. We recommend extending the TimeoutCorrelationManagerSupport when you build custom correlation managers. This provides support for timeout and other complexities you otherwise would need to implement as well. See also the producerPoolEnabled option for more details. |  | MEDIUM |
| **camel.component.netty.lazyChannelCreation** | Channels can be lazily created to avoid exceptions, if the remote server is not up and running when the Camel producer is started. | true | MEDIUM |
| **camel.component.netty.producerPoolBlockWhenExhausted** | Sets the value for the blockWhenExhausted configuration attribute. It determines whether to block when the borrowObject() method is invoked when the pool is exhausted (the maximum number of active objects has been reached). | true | MEDIUM |
| **camel.component.netty.producerPoolEnabled** | Whether producer pool is enabled or not. Important: If you turn this off then a single shared connection is used for the producer, also if you are doing request/reply. That means there is a potential issue with interleaved responses if replies comes back out-of-order. Therefore you need to have a correlation id in both the request and reply messages so you can properly correlate the replies to the Camel callback that is responsible for continue processing the message in Camel. To do this you need to implement NettyCamelStateCorrelationManager as correlation manager and configure it via the correlationManager option. See also the correlationManager option for more details. | true | MEDIUM |
| **camel.component.netty.producerPoolMaxIdle** | Sets the cap on the number of idle instances in the pool. | 100 | MEDIUM |
| **camel.component.netty.producerPoolMaxTotal** | Sets the cap on the number of objects that can be allocated by the pool (checked out to clients, or idle awaiting checkout) at a given time. Use a negative value for no limit. Be careful to not set this value too low (such as 1) as the pool must have space to create a producer such as when performing retries. Be mindful that the option producerPoolBlockWhenExhausted is default true, and the pool will then block when there is no space, which can lead to the application to hang. | \-1 | MEDIUM |
| **camel.component.netty.producerPoolMaxWait** | Sets the maximum duration (value in millis) the borrowObject() method should block before throwing an exception when the pool is exhausted and producerPoolBlockWhenExhausted is true. When less than 0, the borrowObject() method may block indefinitely. | \-1L | MEDIUM |
| **camel.component.netty.producerPoolMinEvictableIdle** | Sets the minimum amount of time (value in millis) an object may sit idle in the pool before it is eligible for eviction by the idle object evictor. | 300000L | MEDIUM |
| **camel.component.netty.producerPoolMinIdle** | Sets the minimum number of instances allowed in the producer pool before the evictor thread (if active) spawns new objects. |  | MEDIUM |
| **camel.component.netty.udpConnectionlessSending** | This option supports connection less udp sending which is a real fire and forget. A connected udp send receive the PortUnreachableException if no one is listen on the receiving port. | false | MEDIUM |
| **camel.component.netty.useByteBuf** | If the useByteBuf is true, netty producer will turn the message body into ByteBuf before sending it out. | false | MEDIUM |
| **camel.component.netty.allowSerializedHeaders** | Only used for TCP when transferExchange is true. When set to true, serializable objects in headers and properties will be added to the exchange. Otherwise Camel will exclude any non-serializable objects and log it at WARN level. | false | MEDIUM |
| **camel.component.netty.autowiredEnabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | MEDIUM |
| **camel.component.netty.channelGroup** | To use an explicit ChannelGroup. |  | MEDIUM |
| **camel.component.netty.nativeTransport** | Whether to use native transport instead of NIO. Native transport takes advantage of the host operating system and is only supported on some platforms. You need to add the netty JAR for the host operating system you are using. See more details at: [http://netty.io/wiki/native-transports.html](http://netty.io/wiki/native-transports.md). | false | MEDIUM |
| **camel.component.netty.options** | Allows to configure additional netty options using option. as prefix. For example option.child.keepAlive=false. See the Netty documentation for possible options that can be used. This is a multi-value option with prefix: option. |  | MEDIUM |
| **camel.component.netty.receiveBufferSize** | The TCP/UDP buffer sizes to be used during inbound communication. Size is bytes. | 65536 | MEDIUM |
| **camel.component.netty.receiveBufferSizePredictor** | Configures the buffer size predictor. See details at Jetty documentation and this mail thread. |  | MEDIUM |
| **camel.component.netty.sendBufferSize** | The TCP/UDP buffer sizes to be used during outbound communication. Size is bytes. | 65536 | MEDIUM |
| **camel.component.netty.shutdownTimeout** | Shutdown await timeout in milliseconds. | 100 | MEDIUM |
| **camel.component.netty.transferExchange** | Only used for TCP. You can transfer the exchange over the wire instead of just the body. The following fields are transferred: In body, Out body, fault body, In headers, Out headers, fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | MEDIUM |
| **camel.component.netty.udpByteArrayCodec** | For UDP only. If enabled the using byte array codec instead of Java serialization protocol. | false | MEDIUM |
| **camel.component.netty.unixDomainSocketPath** | Path to unix domain socket to use instead of inet socket. Host and port parameters will not be used, however required. It is ok to set dummy values for them. Must be used with nativeTransport=true and clientMode=false. |  | MEDIUM |
| **camel.component.netty.workerCount** | When netty works on nio mode, it uses default workerCount parameter from Netty (which is cpu\_core\_threads x 2). User can use this option to override the default workerCount from Netty. |  | MEDIUM |
| **camel.component.netty.workerGroup** | To use a explicit EventLoopGroup as the boss thread pool. For example to share a thread pool with multiple consumers or producers. By default each consumer or producer has their own worker pool with 2 x cpu count core threads. |  | MEDIUM |
| **camel.component.netty.allowDefaultCodec** | The netty component installs a default codec if both, encoder/decoder is null and textline is false. Setting allowDefaultCodec to false prevents the netty component from installing a default codec as the first element in the filter chain. | true | MEDIUM |
| **camel.component.netty.autoAppendDelimiter** | Whether or not to auto append missing end delimiter when sending using the textline codec. | true | MEDIUM |
| **camel.component.netty.decoderMaxLineLength** | The max line length to use for the textline codec. | 1024 | MEDIUM |
| **camel.component.netty.decoders** | A list of decoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | MEDIUM |
| **camel.component.netty.delimiter** | 

The delimiter to use for the textline codec. Possible values are LINE and NULL. One of: \[LINE\] \[NULL\].

Enum values:

-   LINE
    
-   NULL
    





 | "LINE" | MEDIUM |
| **camel.component.netty.encoders** | A list of encoders to be used. You can use a String which have values separated by comma, and have the values be looked up in the Registry. Just remember to prefix the value with # so Camel knows it should lookup. |  | MEDIUM |
| **camel.component.netty.encoding** | The encoding (a charset name) to use for the textline codec. If not provided, Camel will use the JVM default Charset. |  | MEDIUM |
| **camel.component.netty.textline** | Only used for TCP. If no codec is specified, you can use this flag to indicate a text line based codec; if not specified or the value is false, then Object Serialization is assumed over TCP - however only Strings are allowed to be serialized by default. | false | MEDIUM |
| **camel.component.netty.enabledProtocols** | Which protocols to enable when using SSL. | "TLSv1.2,TLSv1.3" | MEDIUM |
| **camel.component.netty.hostnameVerification** | To enable/disable hostname verification on SSLEngine. | false | MEDIUM |
| **camel.component.netty.keyStoreFormat** | Keystore format to be used for payload encryption. Defaults to JKS if not set. |  | MEDIUM |
| **camel.component.netty.keyStoreResource** | Client side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | MEDIUM |
| **camel.component.netty.passphrase** | Password to use for the keyStore and trustStore. The same password must be configured for both resources. |  | MEDIUM |
| **camel.component.netty.securityProvider** | Security provider to be used for payload encryption. Defaults to SunX509 if not set. |  | MEDIUM |
| **camel.component.netty.ssl** | Setting to specify whether SSL encryption is applied to this endpoint. | false | MEDIUM |
| **camel.component.netty.sslClientCertHeaders** | When enabled and in SSL mode, then the Netty consumer will enrich the Camel Message with headers having information about the client certificate such as subject name, issuer name, serial number, and the valid date range. | false | MEDIUM |
| **camel.component.netty.sslContextParameters** | To configure security using SSLContextParameters. |  | MEDIUM |
| **camel.component.netty.sslHandler** | Reference to a class that could be used to return an SSL Handler. |  | MEDIUM |
| **camel.component.netty.trustStoreResource** | Server side certificate keystore to be used for encryption. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | MEDIUM |
| **camel.component.netty.useGlobalSslContextParameters** | Enable usage of global SSL context parameters. | false | MEDIUM |

The camel-netty sink connector has no converters out of the box.

The camel-netty sink connector has no transforms out of the box.

The camel-netty sink connector has no aggregation strategies out of the box.