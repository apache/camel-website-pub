# JMS

**Since Camel 1.0**

**Both producer and consumer are supported**

This component allows messages to be sent to (or consumed from) a [JMS](http://java.sun.com/products/jms/) Queue or Topic. It uses Spring’s JMS support for declarative transactions, including Spring’s `JmsTemplate` for sending and a `MessageListenerContainer` for consuming.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jms</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

> **Tip**
> **Using ActiveMQ**
>
> If you are using [Apache ActiveMQ](http://activemq.apache.org/), you should prefer the ActiveMQ component as it has been optimized for ActiveMQ. All the options and samples on this page are also valid for the ActiveMQ component.

> **Note**
> **Transacted and caching**
>
> See section _Transactions and Cache Levels_ below if you are using transactions with [JMS](#) as it can impact performance.

> **Note**
> **Request/Reply over JMS**
>
> Make sure to read the section _Request-reply over JMS_ further below on this page for important notes about request/reply, as Camel offers a number of options to configure for performance, and clustered environments.

## URI format

jms:\[queue:|topic:\]destinationName\[?options\]

Where `destinationName` is a JMS queue or topic name. By default, the `destinationName` is interpreted as a queue name. For example, to connect to the queue, `FOO.BAR` use:

jms:FOO.BAR

You can include the optional `queue:` prefix, if you prefer:

jms:queue:FOO.BAR

To connect to a topic, you _must_ include the `topic:` prefix. For example, to  
connect to the topic, `Stocks.Prices`, use:

jms:topic:Stocks.Prices

You append query options to the URI by using the following format, `?option=value&option=value&…​`

## Notes

### Using ActiveMQ

The JMS component reuses Spring 2’s `JmsTemplate` for sending messages. This is not ideal for use in a non-J2EE container and typically requires some caching in the JMS provider to avoid [poor performance](http://activemq.apache.org/jmstemplate-gotchas.md).

If you intend to use [Apache ActiveMQ](http://activemq.apache.org/) as your message broker, the recommendation is that you do one of the following:

-   Use the ActiveMQ component, which is already optimized to use ActiveMQ efficiently
    
-   Use the `PoolingConnectionFactory` in ActiveMQ.
    

### Transactions and Cache Levels

If you are consuming messages and using transactions (`transacted=true`) then the default settings for cache level can impact performance.

If you are using XA transactions, then you cannot cache as it can cause the XA transaction to not work properly.

If you are **not** using XA, then you should consider caching as it speeds up performance, such as setting `cacheLevelName=CACHE_CONSUMER`.

The default setting for `cacheLevelName` is `CACHE_AUTO`. This default auto-detects the mode and sets the cache level accordingly to:

-   `CACHE_CONSUMER` if `transacted=false`
    
-   `CACHE_NONE` if `transacted=true`
    

So you can say the default setting is conservative. Consider using `cacheLevelName=CACHE_CONSUMER` if you are using non-XA transactions.

### Durable Subscriptions

#### Durable Subscriptions with JMS 2.0

If you wish to use durable topic subscriptions, you need to specify the `durableSubscriptionName`.

#### Durable Subscriptions with JMS 1.1

If you wish to use durable topic subscriptions, you need to specify both `clientId` and `durableSubscriptionName`. The value of the `clientId` must be unique and can only be used by a single JMS connection instance in your entire network.

> **Note**
> If you are using the [Apache ActiveMQ Classic](https://activemq.apache.org/components/classic/) or [Apache ActiveMQ Artemis](https://activemq.apache.org/components/artemis/), you may prefer to use a feature called Virtual Topic. This should remove the necessity of having a unique `clientId`.
>
> You can consult the specific documentation for [Artemis](https://activemq.apache.org/components/artemis/migration-documentation/VirtualTopics.md) or for [ActiveMQ Classic](https://activemq.apache.org/virtual-destinations.md) for details about how to leverage this feature.
>
> You can find more details about durable messaging for ActiveMQ Classic [here](http://activemq.apache.org/how-do-durable-queues-and-topics-work.md).

### Message Header Mapping

When using message headers, the JMS specification states that header names must be valid Java identifiers. So try to name your headers to be valid Java identifiers. One benefit of doing this is that you can then use your headers inside a JMS Selector (whose SQL92 syntax mandates Java identifier syntax for headers).

The current header name strategy for accepting header names in Camel is as follows:

-   Dots are replaced by `_DOT_` and the replacement is reversed when Camel consume the message
    
-   Hyphen is replaced by `_HYPHEN_` and the replacement is reversed when Camel consumes the message
    

Camel comes with two implementations of `HeaderFilterStrategy`:

-   `org.apache.camel.component.jms.ClassicJmsHeaderFilterStrategy` - classic strategy used until Camel 4.8.
    
-   `org.apache.camel.component.jms.JmsHeaderFilterStrategy` - newer default strategy from Camel 4.9 onwards.
    

#### ClassicJmsHeaderFilterStrategy

A classic strategy for mapping header names is used in Camel 4.8 or older.

This strategy also includes Camel internal headers such as `CamelFileName` and `CamelBeanMethodName` which means that you can send Camel messages over JMS to another Camel instance and preserve this information. However, this also means that JMS messages contains properties with `Camel…​` keys. This is not desirable always, and therefore we changed default from Camel 4.9 onwards.

> **Note**
> You can always configure a custom `HeaderFilterStrategy` to remove all `Camel…​` headers in Camel 4.8 or older.

#### JmsHeaderFilterStrategy

The new default strategy from Camel 4.9 onwards behaves similar to other components, where `Camel…​` headers are removed, and only allowing explicit end user headers.

> **Warning**
> **Mapping to Spring JMS**
>
> Many of these properties map to properties on Spring JMS, which Camel uses for sending and receiving messages. So you can get more information about these properties by consulting the relevant Spring documentation.

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

The JMS component supports 109 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | Sets the JMS client ID to use. Note that this value, if specified, must be unique and can only be used by a single JMS connection instance. It is typically only required for durable topic subscriptions with JMS 1.1. |  | String |
| **connectionFactory** (common) | The connection factory to be use. A connection factory must be configured either on the component or endpoint. |  | ConnectionFactory |
| **disableReplyTo** (common) | Specifies whether Camel ignores the JMSReplyTo header in messages. If true, Camel does not send a reply back to the destination specified in the JMSReplyTo header. You can use this option if you want Camel to consume from a route and you do not want Camel to automatically send back a reply message because another component in your code handles the reply message. You can also use this option if you want to use Camel as a proxy between different message brokers and you want to route message from one system to another. | false | boolean |
| **durableSubscriptionName** (common) | The durable subscriber name for specifying durable topic subscriptions. The clientId option must be configured as well. |  | String |
| **jmsMessageType** (common) | 
Allows you to force the use of a specific jakarta.jms.Message implementation for sending JMS messages from Camel to the broker (also when Camel is used for request/reply). This is not in use when Camel receives messages as the message is locked to the type from the client that sent the message to the broker. Possible values are: Bytes, Map, Object, Stream, Text. By default, Camel would determine which JMS message type to use from the message body type. This option allows you to specify it.

Enum values:

-   Bytes
    
-   Map
    
-   Object
    
-   Stream
    
-   Text
    





 |  | JmsMessageType |
| **replyTo** (common) | Provides an explicit ReplyTo destination (overrides any incoming value of Message.getJMSReplyTo() in consumer). |  | String |
| **testConnectionOnStartup** (common) | Specifies whether to test the connection on startup. This ensures that when Camel starts that all the JMS consumers have a valid connection to the JMS broker. If a connection cannot be granted then Camel throws an exception on startup. This ensures that Camel is not started with failed connections. The JMS producers is tested as well. | false | boolean |
| **acknowledgementModeName** (consumer) | 

The JMS acknowledgement name, which is one of: SESSION\_TRANSACTED, CLIENT\_ACKNOWLEDGE, AUTO\_ACKNOWLEDGE, DUPS\_OK\_ACKNOWLEDGE.

Enum values:

-   SESSION\_TRANSACTED
    
-   CLIENT\_ACKNOWLEDGE
    
-   AUTO\_ACKNOWLEDGE
    
-   DUPS\_OK\_ACKNOWLEDGE
    





 | AUTO\_ACKNOWLEDGE | String |
| **artemisConsumerPriority** (consumer) | Consumer priorities allow you to ensure that high priority consumers receive messages while they are active. Normally, active consumers connected to a queue receive messages from it in a round-robin fashion. When consumer priorities are in use, messages are delivered round-robin if multiple active consumers exist with the same high priority. Messages will only going to lower priority consumers when the high priority consumers do not have credit available to consume the message, or those high priority consumers have declined to accept the message (for instance because it does not meet the criteria of any selectors associated with the consumer). |  | int |
| **asyncConsumer** (consumer) | Whether the JmsConsumer processes the Exchange asynchronously. If enabled then the JmsConsumer may pickup the next message from the JMS queue, while the previous message is being processed asynchronously (by the Asynchronous Routing Engine). This means that messages may be processed not 100% strictly in order. If disabled (as default) then the Exchange is fully processed before the JmsConsumer will pickup the next message from the JMS queue. Note if transacted has been enabled, then asyncConsumer=true does not run asynchronously, as transaction must be executed synchronously. | false | boolean |
| **autoStartup** (consumer) | Specifies whether the consumer container should auto-startup. | true | boolean |
| **cacheLevel** (consumer) | Sets the cache level by ID for the underlying JMS resources. See cacheLevelName option for more details. |  | int |
| **cacheLevelName** (consumer) | 

Sets the cache level by name for the underlying JMS resources. Possible values are: CACHE\_AUTO, CACHE\_CONNECTION, CACHE\_CONSUMER, CACHE\_NONE, and CACHE\_SESSION. The default setting is CACHE\_AUTO. See the Spring documentation and Transactions Cache Levels for more information.

Enum values:

-   CACHE\_AUTO
    
-   CACHE\_CONNECTION
    
-   CACHE\_CONSUMER
    
-   CACHE\_NONE
    
-   CACHE\_SESSION
    





 | CACHE\_AUTO | String |
| **concurrentConsumers** (consumer) | Specifies the default number of concurrent consumers when consuming from JMS (not for request/reply over JMS). See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. When doing request/reply over JMS then the option replyToConcurrentConsumers is used to control number of concurrent consumers on the reply message listener. | 1 | int |
| **maxConcurrentConsumers** (consumer) | Specifies the maximum number of concurrent consumers when consuming from JMS (not for request/reply over JMS). See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. When doing request/reply over JMS then the option replyToMaxConcurrentConsumers is used to control number of concurrent consumers on the reply message listener. |  | int |
| **replyToDeliveryPersistent** (consumer) | Specifies whether to use persistent delivery by default for replies. | true | boolean |
| **selector** (consumer) | Sets the JMS selector to use. |  | String |
| **subscriptionDurable** (consumer) | Set whether to make the subscription durable. The durable subscription name to be used can be specified through the subscriptionName property. Default is false. Set this to true to register a durable subscription, typically in combination with a subscriptionName value (unless your message listener class name is good enough as subscription name). Only makes sense when listening to a topic (pub-sub domain), therefore this method switches the pubSubDomain flag as well. | false | boolean |
| **subscriptionName** (consumer) | Set the name of a subscription to create. To be applied in case of a topic (pub-sub domain) with a shared or durable subscription. The subscription name needs to be unique within this client’s JMS client id. Default is the class name of the specified message listener. Note: Only 1 concurrent consumer (which is the default of this message listener container) is allowed for each subscription, except for a shared subscription (which requires JMS 2.0). |  | String |
| **subscriptionShared** (consumer) | Set whether to make the subscription shared. The shared subscription name to be used can be specified through the subscriptionName property. Default is false. Set this to true to register a shared subscription, typically in combination with a subscriptionName value (unless your message listener class name is good enough as subscription name). Note that shared subscriptions may also be durable, so this flag can (and often will) be combined with subscriptionDurable as well. Only makes sense when listening to a topic (pub-sub domain), therefore this method switches the pubSubDomain flag as well. Requires a JMS 2.0 compatible message broker. | false | boolean |
| **acceptMessagesWhileStopping** (consumer (advanced)) | Specifies whether the consumer accept messages while it is stopping. You may consider enabling this option, if you start and stop JMS routes at runtime, while there are still messages enqueued on the queue. If this option is false, and you stop the JMS route, then messages may be rejected, and the JMS broker would have to attempt redeliveries, which yet again may be rejected, and eventually the message may be moved at a dead letter queue on the JMS broker. To avoid this its recommended to enable this option. | false | boolean |
| **allowReplyManagerQuickStop** (consumer (advanced)) | Whether the DefaultMessageListenerContainer used in the reply managers for request-reply messaging allow the DefaultMessageListenerContainer.runningAllowed flag to quick stop in case JmsConfiguration#isAcceptMessagesWhileStopping is enabled, and org.apache.camel.CamelContext is currently being stopped. This quick stop ability is enabled by default in the regular JMS consumers but to enable for reply managers you must enable this flag. | false | boolean |
| **consumerType** (consumer (advanced)) | 

The consumer type to use, which can be one of: Simple, Default, or Custom. The consumer type determines which Spring JMS listener to use. Default will use org.springframework.jms.listener.DefaultMessageListenerContainer, Simple will use org.springframework.jms.listener.SimpleMessageListenerContainer. When Custom is specified, the MessageListenerContainerFactory defined by the messageListenerContainerFactory option will determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use.

Enum values:

-   Simple
    
-   Default
    
-   Custom
    





 | Default | ConsumerType |
| **defaultTaskExecutorType** (consumer (advanced)) | 

Specifies what default TaskExecutor type to use in the DefaultMessageListenerContainer, for both consumer endpoints and the ReplyTo consumer of producer endpoints. Possible values: SimpleAsync (uses Spring’s SimpleAsyncTaskExecutor) or ThreadPool (uses Spring’s ThreadPoolTaskExecutor with optimal values - cached thread-pool-like). If not set, it defaults to the previous behaviour, which uses a cached thread pool for consumer endpoints and SimpleAsync for reply consumers. The use of ThreadPool is recommended to reduce thread trash in elastic configurations with dynamically increasing and decreasing concurrent consumers.

Enum values:

-   ThreadPool
    
-   SimpleAsync
    





 |  | DefaultTaskExecutorType |
| **eagerLoadingOfProperties** (consumer (advanced)) | Enables eager loading of JMS properties and payload as soon as a message is loaded which generally is inefficient as the JMS properties may not be required but sometimes can catch early any issues with the underlying JMS provider and the use of JMS properties. See also the option eagerPoisonBody. | false | boolean |
| **eagerPoisonBody** (consumer (advanced)) | If eagerLoadingOfProperties is enabled and the JMS message payload (JMS body or JMS properties) is poison (cannot be read/mapped), then set this text as the message body instead so the message can be processed (the cause of the poison are already stored as exception on the Exchange). This can be turned off by setting eagerPoisonBody=false. See also the option eagerLoadingOfProperties. | Poison JMS message due to ${exception.message} | String |
| **exposeListenerSession** (consumer (advanced)) | Specifies whether the listener session should be exposed when consuming messages. | false | boolean |
| **replyToConsumerType** (consumer (advanced)) | 

The consumer type of the reply consumer (when doing request/reply), which can be one of: Simple, Default, or Custom. The consumer type determines which Spring JMS listener to use. Default will use org.springframework.jms.listener.DefaultMessageListenerContainer, Simple will use org.springframework.jms.listener.SimpleMessageListenerContainer. When Custom is specified, the MessageListenerContainerFactory defined by the messageListenerContainerFactory option will determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use.

Enum values:

-   Simple
    
-   Default
    
-   Custom
    





 | Default | ConsumerType |
| **replyToSameDestinationAllowed** (consumer (advanced)) | Whether a JMS consumer is allowed to send a reply message to the same destination that the consumer is using to consume from. This prevents an endless loop by consuming and sending back the same message to itself. | false | boolean |
| **taskExecutor** (consumer (advanced)) | Allows you to specify a custom task executor for consuming messages. |  | TaskExecutor |
| **deliveryDelay** (producer) | Sets delivery delay to use for send calls for JMS. This option requires JMS 2.0 compliant broker. | \-1 | long |
| **deliveryMode** (producer) | 

Specifies the delivery mode to be used. Possible values are those defined by jakarta.jms.DeliveryMode. NON\_PERSISTENT = 1 and PERSISTENT = 2.

Enum values:

-   1
    
-   2
    





 |  | Integer |
| **deliveryPersistent** (producer) | Specifies whether persistent delivery is used by default. | true | boolean |
| **explicitQosEnabled** (producer) | Set if the deliveryMode, priority or timeToLive qualities of service should be used when sending messages. This option is based on Spring’s JmsTemplate. The deliveryMode, priority and timeToLive options are applied to the current endpoint. This contrasts with the preserveMessageQos option, which operates at message granularity, reading QoS properties exclusively from the Camel In message headers. | false | Boolean |
| **formatDateHeadersToIso8601** (producer) | Sets whether JMS date properties should be formatted according to the ISO 8601 standard. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **preserveMessageQos** (producer) | Set to true, if you want to send message using the QoS settings specified on the message, instead of the QoS settings on the JMS endpoint. The following three headers are considered JMSPriority, JMSDeliveryMode, and JMSExpiration. You can provide all or only some of them. If not provided, Camel will fall back to use the values from the endpoint instead. So, when using this option, the headers override the values from the endpoint. The explicitQosEnabled option, by contrast, will only use options set on the endpoint, and not values from the message header. | false | boolean |
| **priority** (producer) | 

Values greater than 1 specify the message priority when sending (where 1 is the lowest priority and 9 is the highest). The explicitQosEnabled option must also be enabled in order for this option to have any effect.

Enum values:

-   1
    
-   2
    
-   3
    
-   4
    
-   5
    
-   6
    
-   7
    
-   8
    
-   9
    





 | 4 | int |
| **replyToConcurrentConsumers** (producer) | Specifies the default number of concurrent consumers when doing request/reply over JMS. See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. | 1 | int |
| **replyToMaxConcurrentConsumers** (producer) | Specifies the maximum number of concurrent consumers when using request/reply over JMS. See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. |  | int |
| **replyToOnTimeoutMaxConcurrentConsumers** (producer) | Specifies the maximum number of concurrent consumers for continue routing when timeout occurred when using request/reply over JMS. | 1 | int |
| **replyToOverride** (producer) | Provides an explicit ReplyTo destination in the JMS message, which overrides the setting of replyTo. It is useful if you want to forward the message to a remote Queue and receive the reply message from the ReplyTo destination. |  | String |
| **replyToType** (producer) | 

Allows for explicitly specifying which kind of strategy to use for replyTo queues when doing request/reply over JMS. Possible values are: Temporary, Shared, or Exclusive. By default Camel will use temporary queues. However if replyTo has been configured, then Shared is used by default. This option allows you to use exclusive queues instead of shared ones. See Camel JMS documentation for more details, and especially the notes about the implications if running in a clustered environment, and the fact that Shared reply queues has lower performance than its alternatives Temporary and Exclusive.

Enum values:

-   Temporary
    
-   Shared
    
-   Exclusive
    





 |  | ReplyToType |
| **requestTimeout** (producer) | The timeout for waiting for a reply when using the InOut Exchange Pattern (in milliseconds). The default is 20 seconds. You can include the header CamelJmsRequestTimeout to override this endpoint configured timeout value, and thus have per message individual timeout values. See also the requestTimeoutCheckerInterval option. | 20000 | long |
| **timeToLive** (producer) | When sending messages, specifies the time-to-live of the message (in milliseconds). | \-1 | long |
| **allowAdditionalHeaders** (producer (advanced)) | This option is used to allow additional headers which may have values that are invalid according to JMS specification. For example, some message systems, such as WMQ, do this with header names using prefix JMS\_IBM\_MQMD\_ containing values with byte array or other invalid types. You can specify multiple header names separated by comma, and use as suffix for wildcard matching. |  | String |
| **allowNullBody** (producer (advanced)) | Whether to allow sending messages with no body. If this option is false and the message body is null, then an JMSException is thrown. | true | boolean |
| **alwaysCopyMessage** (producer (advanced)) | If true, Camel will always make a JMS message copy of the message when it is passed to the producer for sending. Copying the message is needed in some situations, such as when a replyToDestinationSelectorName is set (incidentally, Camel will set the alwaysCopyMessage option to true, if a replyToDestinationSelectorName is set). | false | boolean |
| **correlationProperty** (producer (advanced)) | When using InOut exchange pattern use this JMS property instead of JMSCorrelationID JMS property to correlate messages. If set messages will be correlated solely on the value of this property JMSCorrelationID property will be ignored and not set by Camel. |  | String |
| **disableTimeToLive** (producer (advanced)) | Use this option to force disabling time to live. For example when you do request/reply over JMS, then Camel will by default use the requestTimeout value as time to live on the message being sent. The problem is that the sender and receiver systems have to have their clocks synchronized, so they are in sync. This is not always so easy to archive. So you can use disableTimeToLive=true to not set a time to live value on the sent message. Then the message will not expire on the receiver system. See below in section About time to live for more details. | false | boolean |
| **forceSendOriginalMessage** (producer (advanced)) | When using mapJmsMessage=false Camel will create a new JMS message to send to a new JMS destination if you touch the headers (get or set) during the route. Set this option to true to force Camel to send the original JMS message that was received. | false | boolean |
| **includeSentJMSMessageID** (producer (advanced)) | Only applicable when sending to JMS destination using InOnly (eg fire and forget). Enabling this option will enrich the Camel Exchange with the actual JMSMessageID that was used by the JMS client when the message was sent to the JMS destination. | false | boolean |
| **replyCorrelationProperty** (producer (advanced)) | When using InOut exchange pattern use this JMS property instead of JMSCorrelationID JMS property to correlate reply message. Difference between this and 'correlationProperty' is that 'correlationProperty' tells which request property holds the correlation id value and it does not affect the selector for the reply (JMSCorrelationID=<correlation id>), while 'replyCorrelationProperty' tells which reply property will hold the correlation id value and it does affect the selector for the reply (<replyCorrelationProperty>=<correlation id>). |  | String |
| **replyToCacheLevelName** (producer (advanced)) | 

Sets the cache level by name for the reply consumer when doing request/reply over JMS. This option only applies when using fixed reply queues (not temporary). Camel will by default use: CACHE\_CONSUMER for exclusive or shared w/ replyToSelectorName. And CACHE\_SESSION for shared without replyToSelectorName. Some JMS brokers such as IBM WebSphere may require to set the replyToCacheLevelName=CACHE\_NONE to work. Note: If using temporary queues then CACHE\_NONE is not allowed, and you must use a higher value such as CACHE\_CONSUMER or CACHE\_SESSION.

Enum values:

-   CACHE\_AUTO
    
-   CACHE\_CONNECTION
    
-   CACHE\_CONSUMER
    
-   CACHE\_NONE
    
-   CACHE\_SESSION
    





 |  | String |
| **replyToDestinationSelectorName** (producer (advanced)) | Sets the JMS Selector using the fixed name to be used so you can filter out your own replies from the others when using a shared queue (that is, if you are not using a temporary reply queue). |  | String |
| **streamMessageTypeEnabled** (producer (advanced)) | Sets whether StreamMessage type is enabled or not. Message payloads of streaming kind such as files, InputStream, etc will either by sent as BytesMessage or StreamMessage. This option controls which kind will be used. By default BytesMessage is used which enforces the entire message payload to be read into memory. By enabling this option the message payload is read into memory in chunks and each chunk is then written to the StreamMessage until no more data. | false | boolean |
| **allowAutoWiredConnectionFactory** (advanced) | Whether to auto-discover ConnectionFactory from the registry, if no connection factory has been configured. If only one instance of ConnectionFactory is found then it will be used. This is enabled by default. | true | boolean |
| **allowAutoWiredDestinationResolver** (advanced) | Whether to auto-discover DestinationResolver from the registry, if no destination resolver has been configured. If only one instance of DestinationResolver is found then it will be used. This is enabled by default. | true | boolean |
| **allowSerializedHeaders** (advanced) | Controls whether or not to include serialized headers. Applies only when transferExchange is true. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | boolean |
| **artemisStreamingEnabled** (advanced) | Whether optimizing for Apache Artemis streaming mode. This can reduce memory overhead when using Artemis with JMS StreamMessage types. This option must only be enabled if Apache Artemis is being used. | false | boolean |
| **asyncStartListener** (advanced) | Whether to startup the JmsConsumer message listener asynchronously, when starting a route. For example if a JmsConsumer cannot get a connection to a remote JMS broker, then it may block while retrying and/or fail-over. This will cause Camel to block while starting routes. By setting this option to true, you will let routes startup, while the JmsConsumer connects to the JMS broker using a dedicated thread in asynchronous mode. If this option is used, then beware that if the connection could not be established, then an exception is logged at WARN level, and the consumer will not be able to receive messages; You can then restart the route to retry. | false | boolean |
| **asyncStopListener** (advanced) | Whether to stop the JmsConsumer message listener asynchronously, when stopping a route. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **browseLimit** (advanced) | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | int |
| **configuration** (advanced) | To use a shared JMS configuration. |  | JmsConfiguration |
| **destinationResolver** (advanced) | A pluggable org.springframework.jms.support.destination.DestinationResolver that allows you to use your own resolver (for example, to lookup the real destination in a JNDI registry). |  | DestinationResolver |
| **errorHandler** (advanced) | Specifies a org.springframework.util.ErrorHandler to be invoked in case of any uncaught exceptions thrown while processing a Message. By default these exceptions will be logged at the WARN level, if no errorHandler has been configured. You can configure logging level and whether stack traces should be logged using errorHandlerLoggingLevel and errorHandlerLogStackTrace options. This makes it much easier to configure, than having to code a custom errorHandler. |  | ErrorHandler |
| **exceptionListener** (advanced) | Specifies the JMS Exception Listener that is to be notified of any underlying JMS exceptions. |  | ExceptionListener |
| **idleConsumerLimit** (advanced) | Specify the limit for the number of consumers that are allowed to be idle at any given time. | 1 | int |
| **idleReceivesPerTaskLimit** (advanced) | Marks the consumer as idle after the specified number of idle receives have been reached. An idle receive is counted from the moment a null message is returned by the receiver after the potential setReceiveTimeout elapsed. This gives the opportunity to check if the idle task count exceeds setIdleTaskExecutionLimit and based on that decide if the task needs to be re-scheduled or not, saving resources that would otherwise be held. This setting differs from setMaxMessagesPerTask where the task is released and re-scheduled after this limit is reached, no matter if the received messages were null or non-null messages. This setting alone can be inflexible if one desires to have a large enough batch for each task but requires a quick(er) release from the moment there are no more messages to process. This setting differs from setIdleTaskExecutionLimit where this limit decides after how many iterations of being marked as idle, a task is released. For example: If setMaxMessagesPerTask is set to '500' and #setIdleReceivesPerTaskLimit is set to '60' and setReceiveTimeout is set to '1000' and setIdleTaskExecutionLimit is set to '1', then 500 messages per task would be processed unless there is a subsequent number of 60 idle messages received, the task would be marked as idle and released. This also means that after the last message was processed, the task would be released after 60 seconds as long as no new messages appear. |  | int |
| **idleTaskExecutionLimit** (advanced) | Specifies the limit for idle executions of a receive task, not having received any message within its execution. If this limit is reached, the task will shut down and leave receiving to other executing tasks (in the case of dynamic scheduling; see the maxConcurrentConsumers setting). There is additional doc available from Spring. | 1 | int |
| **includeAllJMSXProperties** (advanced) | Whether to include all JMSX prefixed properties when mapping from JMS to Camel Message. Setting this to true will include properties such as JMSXAppID, and JMSXUserID etc. Note: If you are using a custom headerFilterStrategy then this option does not apply. | false | boolean |
| **includeCorrelationIDAsBytes** (advanced) | Whether the JMS consumer should include JMSCorrelationIDAsBytes as a header on the Camel Message. | true | boolean |
| **jmsKeyFormatStrategy** (advanced) | 

Pluggable strategy for encoding and decoding JMS keys so they can be compliant with the JMS specification. Camel provides two implementations out of the box: default and passthrough. The default strategy will safely marshal dots and hyphens (. and -). The passthrough strategy leaves the key as is. Can be used for JMS brokers which do not care whether JMS header keys contain illegal characters. You can provide your own implementation of the org.apache.camel.component.jms.JmsKeyFormatStrategy and refer to it using the # notation.

Enum values:

-   default
    
-   passthrough
    





 |  | JmsKeyFormatStrategy |
| **mapJmsMessage** (advanced) | Specifies whether Camel should auto map the received JMS message to a suited payload type, such as jakarta.jms.TextMessage to a String etc. | true | boolean |
| **maxMessagesPerTask** (advanced) | The number of messages per task. -1 is unlimited. If you use a range for concurrent consumers (eg min max), then this option can be used to set a value to eg 100 to control how fast the consumers will shrink when less work is required. | \-1 | int |
| **messageConverter** (advanced) | To use a custom Spring org.springframework.jms.support.converter.MessageConverter so you can be in control how to map to/from a jakarta.jms.Message. |  | MessageConverter |
| **messageCreatedStrategy** (advanced) | To use the given MessageCreatedStrategy which are invoked when Camel creates new instances of jakarta.jms.Message objects when Camel is sending a JMS message. |  | MessageCreatedStrategy |
| **messageIdEnabled** (advanced) | When sending, specifies whether message IDs should be added. This is just an hint to the JMS broker. If the JMS provider accepts this hint, these messages must have the message ID set to null; if the provider ignores the hint, the message ID must be set to its normal unique value. | true | boolean |
| **messageListenerContainerFactory** (advanced) | Registry ID of the MessageListenerContainerFactory used to determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use to consume messages. Setting this will automatically set consumerType to Custom. |  | MessageListenerContainerFactory |
| **messageTimestampEnabled** (advanced) | Specifies whether timestamps should be enabled by default on sending messages. This is just an hint to the JMS broker. If the JMS provider accepts this hint, these messages must have the timestamp set to zero; if the provider ignores the hint the timestamp must be set to its normal value. | true | boolean |
| **objectMessageEnabled** (advanced) | Whether to enable sending and receiving JMS ObjectMessage. By default this is disabled because Java object serialization is a known source of security vulnerabilities. Enable this option only if you trust the source of the messages and need to send or receive Java serialized objects via JMS. When disabled, Camel will refuse to create or read JMS ObjectMessage instances. Options that rely on ObjectMessage internally (such as transferExchange and transferException) require this option to be enabled. | false | boolean |
| **pubSubNoLocal** (advanced) | Specifies whether to inhibit the delivery of messages published by its own connection. | false | boolean |
| **queueBrowseStrategy** (advanced) | To use a custom QueueBrowseStrategy when browsing queues. |  | QueueBrowseStrategy |
| **receiveTimeout** (advanced) | The timeout for receiving messages (in milliseconds). | 1000 | long |
| **recoveryInterval** (advanced) | Specifies the interval between recovery attempts, i.e. when a connection is being refreshed, in milliseconds. The default is 5000 ms, that is, 5 seconds. | 5000 | long |
| **requestTimeoutCheckerInterval** (advanced) | Configures how often Camel should check for timed out Exchanges when doing request/reply over JMS. By default Camel checks once per second. But if you must react faster when a timeout occurs, then you can lower this interval, to check more frequently. The timeout is determined by the option requestTimeout. | 1000 | long |
| **serviceLocationEnabled** (advanced) | Whether to detect the network address location of the JMS broker on startup. This information is gathered via reflection on the ConnectionFactory, and is vendor specific. This option can be used to turn this off. | true | boolean |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **temporaryQueueResolver** (advanced) | A pluggable TemporaryQueueResolver that allows you to use your own resolver for creating temporary queues (some messaging systems has special requirements for creating temporary queues). |  | TemporaryQueueResolver |
| **transferException** (advanced) | If enabled and you are using Request Reply messaging (InOut) and an Exchange failed on the consumer side, then the caused Exception will be send back in response as a jakarta.jms.ObjectMessage. If the client is Camel, the returned Exception is rethrown. This allows you to use Camel JMS as a bridge in your routing - for example, using persistent queues to enable robust routing. Notice that if you also have transferExchange enabled, this option takes precedence. The caught exception is required to be serializable. The original Exception on the consumer side can be wrapped in an outer exception such as org.apache.camel.RuntimeCamelException when returned to the producer. Use this with caution as the data is using Java Object serialization and requires the received to be able to deserialize the data at Class level, which forces a strong coupling between the producers and consumer!. | false | boolean |
| **transferExchange** (advanced) | You can transfer the exchange over the wire instead of just the body and headers. The following fields are transferred: In body, Out body, Fault body, In headers, Out headers, Fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. You must enable this option on both the producer and consumer side, so Camel knows the payloads is an Exchange and not a regular payload. Use this with caution as the data is using Java Object serialization and requires the receiver to be able to deserialize the data at Class level, which forces a strong coupling between the producers and consumers having to use compatible Camel versions!. | false | boolean |
| **useMessageIDAsCorrelationID** (advanced) | Specifies whether JMSMessageID should always be used as JMSCorrelationID for InOut messages. | false | boolean |
| **waitForProvisionCorrelationToBeUpdatedCounter** (advanced) | Number of times to wait for provisional correlation id to be updated to the actual correlation id when doing request/reply over JMS and when the option useMessageIDAsCorrelationID is enabled. | 50 | int |
| **waitForProvisionCorrelationToBeUpdatedThreadSleepingTime** (advanced) | Interval in millis to sleep each time while waiting for provisional correlation id to be updated. | 100 | long |
| **waitForTemporaryReplyToToBeUpdatedCounter** (advanced) | Number of times to wait for temporary replyTo queue to be created and ready when doing request/reply over JMS. | 200 | int |
| **waitForTemporaryReplyToToBeUpdatedThreadSleepingTime** (advanced) | Interval in millis to sleep each time while waiting for temporary replyTo queue to be ready. | 100 | long |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **errorHandlerLoggingLevel** (logging) | 

Allows to configure the default errorHandler logging level for logging uncaught exceptions.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | WARN | LoggingLevel |
| **errorHandlerLogStackTrace** (logging) | Allows to control whether stack-traces should be logged or not, by the default errorHandler. | true | boolean |
| **deserializationFilter** (security) | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied as a defense-in-depth check on the class of the body returned by jakarta.jms.ObjectMessage.getObject(). The pattern is evaluated after the JMS provider has deserialized the payload, so this option alone does not prevent gadget-chain execution that happens inside the provider’s ObjectInputStream; to block such attacks, also configure the JMS provider’s own deserialization filter and/or the JVM-wide -Djdk.serialFilter. When this option is not set and no JVM-wide filter is configured, a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. is applied. |  | String |
| **password** (security) | Password to use with the ConnectionFactory. You can also configure username/password directly on the ConnectionFactory. |  | String |
| **username** (security) | Username to use with the ConnectionFactory. You can also configure username/password directly on the ConnectionFactory. |  | String |
| **transacted** (transaction) | Specifies whether to use transacted mode. | false | boolean |
| **transactedInOut** (transaction) | Specifies whether InOut operations (request reply) default to using transacted mode If this flag is set to true, then Spring JmsTemplate will have sessionTransacted set to true, and the acknowledgeMode as transacted on the JmsTemplate used for InOut operations. Note from Spring JMS: that within a JTA transaction, the parameters passed to createQueue, createTopic methods are not taken into account. Depending on the Java EE transaction context, the container makes its own decisions on these values. Analogously, these parameters are not taken into account within a locally managed transaction either, since Spring JMS operates on an existing JMS Session in this case. Setting this flag to true will use a short local JMS transaction when running outside of a managed transaction, and a synchronized local JMS transaction in case of a managed transaction (other than an XA transaction) being present. This has the effect of a local JMS transaction being managed alongside the main transaction (which might be a native JDBC transaction), with the JMS transaction committing right after the main transaction. | false | boolean |
| **lazyCreateTransactionManager** (transaction (advanced)) | If true, Camel will create a JmsTransactionManager, if there is no transactionManager injected when option transacted=true. | true | boolean |
| **transactionManager** (transaction (advanced)) | The Spring transaction manager to use. |  | PlatformTransactionManager |
| **transactionName** (transaction (advanced)) | The name of the transaction to use. |  | String |
| **transactionTimeout** (transaction (advanced)) | The timeout value of the transaction (in seconds), if using transacted mode. | \-1 | int |

## Endpoint Options

The JMS endpoint is configured using URI syntax:

jms:destinationType:destinationName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **destinationType** (common) | 
The kind of destination to use.

Enum values:

-   queue
    
-   topic
    
-   temp-queue
    
-   temp-topic
    





 | queue | String |
| **destinationName** (common) | **Required** Name of the queue or topic to use as destination. |  | String |

### Query Parameters (104 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | Sets the JMS client ID to use. Note that this value, if specified, must be unique and can only be used by a single JMS connection instance. It is typically only required for durable topic subscriptions with JMS 1.1. |  | String |
| **connectionFactory** (common) | The connection factory to be use. A connection factory must be configured either on the component or endpoint. |  | ConnectionFactory |
| **disableReplyTo** (common) | Specifies whether Camel ignores the JMSReplyTo header in messages. If true, Camel does not send a reply back to the destination specified in the JMSReplyTo header. You can use this option if you want Camel to consume from a route and you do not want Camel to automatically send back a reply message because another component in your code handles the reply message. You can also use this option if you want to use Camel as a proxy between different message brokers and you want to route message from one system to another. | false | boolean |
| **durableSubscriptionName** (common) | The durable subscriber name for specifying durable topic subscriptions. The clientId option must be configured as well. |  | String |
| **jmsMessageType** (common) | 
Allows you to force the use of a specific jakarta.jms.Message implementation for sending JMS messages from Camel to the broker (also when Camel is used for request/reply). This is not in use when Camel receives messages as the message is locked to the type from the client that sent the message to the broker. Possible values are: Bytes, Map, Object, Stream, Text. By default, Camel would determine which JMS message type to use from the message body type. This option allows you to specify it.

Enum values:

-   Bytes
    
-   Map
    
-   Object
    
-   Stream
    
-   Text
    





 |  | JmsMessageType |
| **replyTo** (common) | Provides an explicit ReplyTo destination (overrides any incoming value of Message.getJMSReplyTo() in consumer). |  | String |
| **testConnectionOnStartup** (common) | Specifies whether to test the connection on startup. This ensures that when Camel starts that all the JMS consumers have a valid connection to the JMS broker. If a connection cannot be granted then Camel throws an exception on startup. This ensures that Camel is not started with failed connections. The JMS producers is tested as well. | false | boolean |
| **acknowledgementModeName** (consumer) | 

The JMS acknowledgement name, which is one of: SESSION\_TRANSACTED, CLIENT\_ACKNOWLEDGE, AUTO\_ACKNOWLEDGE, DUPS\_OK\_ACKNOWLEDGE.

Enum values:

-   SESSION\_TRANSACTED
    
-   CLIENT\_ACKNOWLEDGE
    
-   AUTO\_ACKNOWLEDGE
    
-   DUPS\_OK\_ACKNOWLEDGE
    





 | AUTO\_ACKNOWLEDGE | String |
| **artemisConsumerPriority** (consumer) | Consumer priorities allow you to ensure that high priority consumers receive messages while they are active. Normally, active consumers connected to a queue receive messages from it in a round-robin fashion. When consumer priorities are in use, messages are delivered round-robin if multiple active consumers exist with the same high priority. Messages will only going to lower priority consumers when the high priority consumers do not have credit available to consume the message, or those high priority consumers have declined to accept the message (for instance because it does not meet the criteria of any selectors associated with the consumer). |  | int |
| **asyncConsumer** (consumer) | Whether the JmsConsumer processes the Exchange asynchronously. If enabled then the JmsConsumer may pickup the next message from the JMS queue, while the previous message is being processed asynchronously (by the Asynchronous Routing Engine). This means that messages may be processed not 100% strictly in order. If disabled (as default) then the Exchange is fully processed before the JmsConsumer will pickup the next message from the JMS queue. Note if transacted has been enabled, then asyncConsumer=true does not run asynchronously, as transaction must be executed synchronously. | false | boolean |
| **autoStartup** (consumer) | Specifies whether the consumer container should auto-startup. | true | boolean |
| **cacheLevel** (consumer) | Sets the cache level by ID for the underlying JMS resources. See cacheLevelName option for more details. |  | int |
| **cacheLevelName** (consumer) | 

Sets the cache level by name for the underlying JMS resources. Possible values are: CACHE\_AUTO, CACHE\_CONNECTION, CACHE\_CONSUMER, CACHE\_NONE, and CACHE\_SESSION. The default setting is CACHE\_AUTO. See the Spring documentation and Transactions Cache Levels for more information.

Enum values:

-   CACHE\_AUTO
    
-   CACHE\_CONNECTION
    
-   CACHE\_CONSUMER
    
-   CACHE\_NONE
    
-   CACHE\_SESSION
    





 | CACHE\_AUTO | String |
| **concurrentConsumers** (consumer) | Specifies the default number of concurrent consumers when consuming from JMS (not for request/reply over JMS). See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. When doing request/reply over JMS then the option replyToConcurrentConsumers is used to control number of concurrent consumers on the reply message listener. | 1 | int |
| **maxConcurrentConsumers** (consumer) | Specifies the maximum number of concurrent consumers when consuming from JMS (not for request/reply over JMS). See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. When doing request/reply over JMS then the option replyToMaxConcurrentConsumers is used to control number of concurrent consumers on the reply message listener. |  | int |
| **replyToDeliveryPersistent** (consumer) | Specifies whether to use persistent delivery by default for replies. | true | boolean |
| **selector** (consumer) | Sets the JMS selector to use. |  | String |
| **subscriptionDurable** (consumer) | Set whether to make the subscription durable. The durable subscription name to be used can be specified through the subscriptionName property. Default is false. Set this to true to register a durable subscription, typically in combination with a subscriptionName value (unless your message listener class name is good enough as subscription name). Only makes sense when listening to a topic (pub-sub domain), therefore this method switches the pubSubDomain flag as well. | false | boolean |
| **subscriptionName** (consumer) | Set the name of a subscription to create. To be applied in case of a topic (pub-sub domain) with a shared or durable subscription. The subscription name needs to be unique within this client’s JMS client id. Default is the class name of the specified message listener. Note: Only 1 concurrent consumer (which is the default of this message listener container) is allowed for each subscription, except for a shared subscription (which requires JMS 2.0). |  | String |
| **subscriptionShared** (consumer) | Set whether to make the subscription shared. The shared subscription name to be used can be specified through the subscriptionName property. Default is false. Set this to true to register a shared subscription, typically in combination with a subscriptionName value (unless your message listener class name is good enough as subscription name). Note that shared subscriptions may also be durable, so this flag can (and often will) be combined with subscriptionDurable as well. Only makes sense when listening to a topic (pub-sub domain), therefore this method switches the pubSubDomain flag as well. Requires a JMS 2.0 compatible message broker. | false | boolean |
| **acceptMessagesWhileStopping** (consumer (advanced)) | Specifies whether the consumer accept messages while it is stopping. You may consider enabling this option, if you start and stop JMS routes at runtime, while there are still messages enqueued on the queue. If this option is false, and you stop the JMS route, then messages may be rejected, and the JMS broker would have to attempt redeliveries, which yet again may be rejected, and eventually the message may be moved at a dead letter queue on the JMS broker. To avoid this its recommended to enable this option. | false | boolean |
| **allowReplyManagerQuickStop** (consumer (advanced)) | Whether the DefaultMessageListenerContainer used in the reply managers for request-reply messaging allow the DefaultMessageListenerContainer.runningAllowed flag to quick stop in case JmsConfiguration#isAcceptMessagesWhileStopping is enabled, and org.apache.camel.CamelContext is currently being stopped. This quick stop ability is enabled by default in the regular JMS consumers but to enable for reply managers you must enable this flag. | false | boolean |
| **consumerType** (consumer (advanced)) | 

The consumer type to use, which can be one of: Simple, Default, or Custom. The consumer type determines which Spring JMS listener to use. Default will use org.springframework.jms.listener.DefaultMessageListenerContainer, Simple will use org.springframework.jms.listener.SimpleMessageListenerContainer. When Custom is specified, the MessageListenerContainerFactory defined by the messageListenerContainerFactory option will determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use.

Enum values:

-   Simple
    
-   Default
    
-   Custom
    





 | Default | ConsumerType |
| **defaultTaskExecutorType** (consumer (advanced)) | 

Specifies what default TaskExecutor type to use in the DefaultMessageListenerContainer, for both consumer endpoints and the ReplyTo consumer of producer endpoints. Possible values: SimpleAsync (uses Spring’s SimpleAsyncTaskExecutor) or ThreadPool (uses Spring’s ThreadPoolTaskExecutor with optimal values - cached thread-pool-like). If not set, it defaults to the previous behaviour, which uses a cached thread pool for consumer endpoints and SimpleAsync for reply consumers. The use of ThreadPool is recommended to reduce thread trash in elastic configurations with dynamically increasing and decreasing concurrent consumers.

Enum values:

-   ThreadPool
    
-   SimpleAsync
    





 |  | DefaultTaskExecutorType |
| **eagerLoadingOfProperties** (consumer (advanced)) | Enables eager loading of JMS properties and payload as soon as a message is loaded which generally is inefficient as the JMS properties may not be required but sometimes can catch early any issues with the underlying JMS provider and the use of JMS properties. See also the option eagerPoisonBody. | false | boolean |
| **eagerPoisonBody** (consumer (advanced)) | If eagerLoadingOfProperties is enabled and the JMS message payload (JMS body or JMS properties) is poison (cannot be read/mapped), then set this text as the message body instead so the message can be processed (the cause of the poison are already stored as exception on the Exchange). This can be turned off by setting eagerPoisonBody=false. See also the option eagerLoadingOfProperties. | Poison JMS message due to ${exception.message} | String |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **exposeListenerSession** (consumer (advanced)) | Specifies whether the listener session should be exposed when consuming messages. | false | boolean |
| **replyToConsumerType** (consumer (advanced)) | 

The consumer type of the reply consumer (when doing request/reply), which can be one of: Simple, Default, or Custom. The consumer type determines which Spring JMS listener to use. Default will use org.springframework.jms.listener.DefaultMessageListenerContainer, Simple will use org.springframework.jms.listener.SimpleMessageListenerContainer. When Custom is specified, the MessageListenerContainerFactory defined by the messageListenerContainerFactory option will determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use.

Enum values:

-   Simple
    
-   Default
    
-   Custom
    





 | Default | ConsumerType |
| **replyToSameDestinationAllowed** (consumer (advanced)) | Whether a JMS consumer is allowed to send a reply message to the same destination that the consumer is using to consume from. This prevents an endless loop by consuming and sending back the same message to itself. | false | boolean |
| **taskExecutor** (consumer (advanced)) | Allows you to specify a custom task executor for consuming messages. |  | TaskExecutor |
| **deliveryDelay** (producer) | Sets delivery delay to use for send calls for JMS. This option requires JMS 2.0 compliant broker. | \-1 | long |
| **deliveryMode** (producer) | 

Specifies the delivery mode to be used. Possible values are those defined by jakarta.jms.DeliveryMode. NON\_PERSISTENT = 1 and PERSISTENT = 2.

Enum values:

-   1
    
-   2
    





 |  | Integer |
| **deliveryPersistent** (producer) | Specifies whether persistent delivery is used by default. | true | boolean |
| **explicitQosEnabled** (producer) | Set if the deliveryMode, priority or timeToLive qualities of service should be used when sending messages. This option is based on Spring’s JmsTemplate. The deliveryMode, priority and timeToLive options are applied to the current endpoint. This contrasts with the preserveMessageQos option, which operates at message granularity, reading QoS properties exclusively from the Camel In message headers. | false | Boolean |
| **formatDateHeadersToIso8601** (producer) | Sets whether JMS date properties should be formatted according to the ISO 8601 standard. | false | boolean |
| **preserveMessageQos** (producer) | Set to true, if you want to send message using the QoS settings specified on the message, instead of the QoS settings on the JMS endpoint. The following three headers are considered JMSPriority, JMSDeliveryMode, and JMSExpiration. You can provide all or only some of them. If not provided, Camel will fall back to use the values from the endpoint instead. So, when using this option, the headers override the values from the endpoint. The explicitQosEnabled option, by contrast, will only use options set on the endpoint, and not values from the message header. | false | boolean |
| **priority** (producer) | 

Values greater than 1 specify the message priority when sending (where 1 is the lowest priority and 9 is the highest). The explicitQosEnabled option must also be enabled in order for this option to have any effect.

Enum values:

-   1
    
-   2
    
-   3
    
-   4
    
-   5
    
-   6
    
-   7
    
-   8
    
-   9
    





 | 4 | int |
| **replyToConcurrentConsumers** (producer) | Specifies the default number of concurrent consumers when doing request/reply over JMS. See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. | 1 | int |
| **replyToMaxConcurrentConsumers** (producer) | Specifies the maximum number of concurrent consumers when using request/reply over JMS. See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. |  | int |
| **replyToOnTimeoutMaxConcurrentConsumers** (producer) | Specifies the maximum number of concurrent consumers for continue routing when timeout occurred when using request/reply over JMS. | 1 | int |
| **replyToOverride** (producer) | Provides an explicit ReplyTo destination in the JMS message, which overrides the setting of replyTo. It is useful if you want to forward the message to a remote Queue and receive the reply message from the ReplyTo destination. |  | String |
| **replyToType** (producer) | 

Allows for explicitly specifying which kind of strategy to use for replyTo queues when doing request/reply over JMS. Possible values are: Temporary, Shared, or Exclusive. By default Camel will use temporary queues. However if replyTo has been configured, then Shared is used by default. This option allows you to use exclusive queues instead of shared ones. See Camel JMS documentation for more details, and especially the notes about the implications if running in a clustered environment, and the fact that Shared reply queues has lower performance than its alternatives Temporary and Exclusive.

Enum values:

-   Temporary
    
-   Shared
    
-   Exclusive
    





 |  | ReplyToType |
| **requestTimeout** (producer) | The timeout for waiting for a reply when using the InOut Exchange Pattern (in milliseconds). The default is 20 seconds. You can include the header CamelJmsRequestTimeout to override this endpoint configured timeout value, and thus have per message individual timeout values. See also the requestTimeoutCheckerInterval option. | 20000 | long |
| **timeToLive** (producer) | When sending messages, specifies the time-to-live of the message (in milliseconds). | \-1 | long |
| **allowAdditionalHeaders** (producer (advanced)) | This option is used to allow additional headers which may have values that are invalid according to JMS specification. For example, some message systems, such as WMQ, do this with header names using prefix JMS\_IBM\_MQMD\_ containing values with byte array or other invalid types. You can specify multiple header names separated by comma, and use as suffix for wildcard matching. |  | String |
| **allowNullBody** (producer (advanced)) | Whether to allow sending messages with no body. If this option is false and the message body is null, then an JMSException is thrown. | true | boolean |
| **alwaysCopyMessage** (producer (advanced)) | If true, Camel will always make a JMS message copy of the message when it is passed to the producer for sending. Copying the message is needed in some situations, such as when a replyToDestinationSelectorName is set (incidentally, Camel will set the alwaysCopyMessage option to true, if a replyToDestinationSelectorName is set). | false | boolean |
| **correlationProperty** (producer (advanced)) | When using InOut exchange pattern use this JMS property instead of JMSCorrelationID JMS property to correlate messages. If set messages will be correlated solely on the value of this property JMSCorrelationID property will be ignored and not set by Camel. |  | String |
| **disableTimeToLive** (producer (advanced)) | Use this option to force disabling time to live. For example when you do request/reply over JMS, then Camel will by default use the requestTimeout value as time to live on the message being sent. The problem is that the sender and receiver systems have to have their clocks synchronized, so they are in sync. This is not always so easy to archive. So you can use disableTimeToLive=true to not set a time to live value on the sent message. Then the message will not expire on the receiver system. See below in section About time to live for more details. | false | boolean |
| **forceSendOriginalMessage** (producer (advanced)) | When using mapJmsMessage=false Camel will create a new JMS message to send to a new JMS destination if you touch the headers (get or set) during the route. Set this option to true to force Camel to send the original JMS message that was received. | false | boolean |
| **includeSentJMSMessageID** (producer (advanced)) | Only applicable when sending to JMS destination using InOnly (eg fire and forget). Enabling this option will enrich the Camel Exchange with the actual JMSMessageID that was used by the JMS client when the message was sent to the JMS destination. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **replyCorrelationProperty** (producer (advanced)) | When using InOut exchange pattern use this JMS property instead of JMSCorrelationID JMS property to correlate reply message. Difference between this and 'correlationProperty' is that 'correlationProperty' tells which request property holds the correlation id value and it does not affect the selector for the reply (JMSCorrelationID=<correlation id>), while 'replyCorrelationProperty' tells which reply property will hold the correlation id value and it does affect the selector for the reply (<replyCorrelationProperty>=<correlation id>). |  | String |
| **replyToCacheLevelName** (producer (advanced)) | 

Sets the cache level by name for the reply consumer when doing request/reply over JMS. This option only applies when using fixed reply queues (not temporary). Camel will by default use: CACHE\_CONSUMER for exclusive or shared w/ replyToSelectorName. And CACHE\_SESSION for shared without replyToSelectorName. Some JMS brokers such as IBM WebSphere may require to set the replyToCacheLevelName=CACHE\_NONE to work. Note: If using temporary queues then CACHE\_NONE is not allowed, and you must use a higher value such as CACHE\_CONSUMER or CACHE\_SESSION.

Enum values:

-   CACHE\_AUTO
    
-   CACHE\_CONNECTION
    
-   CACHE\_CONSUMER
    
-   CACHE\_NONE
    
-   CACHE\_SESSION
    





 |  | String |
| **replyToDestinationSelectorName** (producer (advanced)) | Sets the JMS Selector using the fixed name to be used so you can filter out your own replies from the others when using a shared queue (that is, if you are not using a temporary reply queue). |  | String |
| **streamMessageTypeEnabled** (producer (advanced)) | Sets whether StreamMessage type is enabled or not. Message payloads of streaming kind such as files, InputStream, etc will either by sent as BytesMessage or StreamMessage. This option controls which kind will be used. By default BytesMessage is used which enforces the entire message payload to be read into memory. By enabling this option the message payload is read into memory in chunks and each chunk is then written to the StreamMessage until no more data. | false | boolean |
| **allowSerializedHeaders** (advanced) | Controls whether or not to include serialized headers. Applies only when transferExchange is true. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | boolean |
| **artemisStreamingEnabled** (advanced) | Whether optimizing for Apache Artemis streaming mode. This can reduce memory overhead when using Artemis with JMS StreamMessage types. This option must only be enabled if Apache Artemis is being used. | false | boolean |
| **asyncStartListener** (advanced) | Whether to startup the JmsConsumer message listener asynchronously, when starting a route. For example if a JmsConsumer cannot get a connection to a remote JMS broker, then it may block while retrying and/or fail-over. This will cause Camel to block while starting routes. By setting this option to true, you will let routes startup, while the JmsConsumer connects to the JMS broker using a dedicated thread in asynchronous mode. If this option is used, then beware that if the connection could not be established, then an exception is logged at WARN level, and the consumer will not be able to receive messages; You can then restart the route to retry. | false | boolean |
| **asyncStopListener** (advanced) | Whether to stop the JmsConsumer message listener asynchronously, when stopping a route. | false | boolean |
| **browseLimit** (advanced) | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | int |
| **destinationResolver** (advanced) | A pluggable org.springframework.jms.support.destination.DestinationResolver that allows you to use your own resolver (for example, to lookup the real destination in a JNDI registry). |  | DestinationResolver |
| **errorHandler** (advanced) | Specifies a org.springframework.util.ErrorHandler to be invoked in case of any uncaught exceptions thrown while processing a Message. By default these exceptions will be logged at the WARN level, if no errorHandler has been configured. You can configure logging level and whether stack traces should be logged using errorHandlerLoggingLevel and errorHandlerLogStackTrace options. This makes it much easier to configure, than having to code a custom errorHandler. |  | ErrorHandler |
| **exceptionListener** (advanced) | Specifies the JMS Exception Listener that is to be notified of any underlying JMS exceptions. |  | ExceptionListener |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **idleConsumerLimit** (advanced) | Specify the limit for the number of consumers that are allowed to be idle at any given time. | 1 | int |
| **idleReceivesPerTaskLimit** (advanced) | Marks the consumer as idle after the specified number of idle receives have been reached. An idle receive is counted from the moment a null message is returned by the receiver after the potential setReceiveTimeout elapsed. This gives the opportunity to check if the idle task count exceeds setIdleTaskExecutionLimit and based on that decide if the task needs to be re-scheduled or not, saving resources that would otherwise be held. This setting differs from setMaxMessagesPerTask where the task is released and re-scheduled after this limit is reached, no matter if the received messages were null or non-null messages. This setting alone can be inflexible if one desires to have a large enough batch for each task but requires a quick(er) release from the moment there are no more messages to process. This setting differs from setIdleTaskExecutionLimit where this limit decides after how many iterations of being marked as idle, a task is released. For example: If setMaxMessagesPerTask is set to '500' and #setIdleReceivesPerTaskLimit is set to '60' and setReceiveTimeout is set to '1000' and setIdleTaskExecutionLimit is set to '1', then 500 messages per task would be processed unless there is a subsequent number of 60 idle messages received, the task would be marked as idle and released. This also means that after the last message was processed, the task would be released after 60 seconds as long as no new messages appear. |  | int |
| **idleTaskExecutionLimit** (advanced) | Specifies the limit for idle executions of a receive task, not having received any message within its execution. If this limit is reached, the task will shut down and leave receiving to other executing tasks (in the case of dynamic scheduling; see the maxConcurrentConsumers setting). There is additional doc available from Spring. | 1 | int |
| **includeAllJMSXProperties** (advanced) | Whether to include all JMSX prefixed properties when mapping from JMS to Camel Message. Setting this to true will include properties such as JMSXAppID, and JMSXUserID etc. Note: If you are using a custom headerFilterStrategy then this option does not apply. | false | boolean |
| **jmsKeyFormatStrategy** (advanced) | 

Pluggable strategy for encoding and decoding JMS keys so they can be compliant with the JMS specification. Camel provides two implementations out of the box: default and passthrough. The default strategy will safely marshal dots and hyphens (. and -). The passthrough strategy leaves the key as is. Can be used for JMS brokers which do not care whether JMS header keys contain illegal characters. You can provide your own implementation of the org.apache.camel.component.jms.JmsKeyFormatStrategy and refer to it using the # notation.

Enum values:

-   default
    
-   passthrough
    





 |  | JmsKeyFormatStrategy |
| **mapJmsMessage** (advanced) | Specifies whether Camel should auto map the received JMS message to a suited payload type, such as jakarta.jms.TextMessage to a String etc. | true | boolean |
| **maxMessagesPerTask** (advanced) | The number of messages per task. -1 is unlimited. If you use a range for concurrent consumers (eg min max), then this option can be used to set a value to eg 100 to control how fast the consumers will shrink when less work is required. | \-1 | int |
| **messageConverter** (advanced) | To use a custom Spring org.springframework.jms.support.converter.MessageConverter so you can be in control how to map to/from a jakarta.jms.Message. |  | MessageConverter |
| **messageCreatedStrategy** (advanced) | To use the given MessageCreatedStrategy which are invoked when Camel creates new instances of jakarta.jms.Message objects when Camel is sending a JMS message. |  | MessageCreatedStrategy |
| **messageIdEnabled** (advanced) | When sending, specifies whether message IDs should be added. This is just an hint to the JMS broker. If the JMS provider accepts this hint, these messages must have the message ID set to null; if the provider ignores the hint, the message ID must be set to its normal unique value. | true | boolean |
| **messageListenerContainerFactory** (advanced) | Registry ID of the MessageListenerContainerFactory used to determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use to consume messages. Setting this will automatically set consumerType to Custom. |  | MessageListenerContainerFactory |
| **messageTimestampEnabled** (advanced) | Specifies whether timestamps should be enabled by default on sending messages. This is just an hint to the JMS broker. If the JMS provider accepts this hint, these messages must have the timestamp set to zero; if the provider ignores the hint the timestamp must be set to its normal value. | true | boolean |
| **objectMessageEnabled** (advanced) | Whether to enable sending and receiving JMS ObjectMessage. By default this is disabled because Java object serialization is a known source of security vulnerabilities. Enable this option only if you trust the source of the messages and need to send or receive Java serialized objects via JMS. When disabled, Camel will refuse to create or read JMS ObjectMessage instances. Options that rely on ObjectMessage internally (such as transferExchange and transferException) require this option to be enabled. | false | boolean |
| **pubSubNoLocal** (advanced) | Specifies whether to inhibit the delivery of messages published by its own connection. | false | boolean |
| **receiveTimeout** (advanced) | The timeout for receiving messages (in milliseconds). | 1000 | long |
| **recoveryInterval** (advanced) | Specifies the interval between recovery attempts, i.e. when a connection is being refreshed, in milliseconds. The default is 5000 ms, that is, 5 seconds. | 5000 | long |
| **requestTimeoutCheckerInterval** (advanced) | Configures how often Camel should check for timed out Exchanges when doing request/reply over JMS. By default Camel checks once per second. But if you must react faster when a timeout occurs, then you can lower this interval, to check more frequently. The timeout is determined by the option requestTimeout. | 1000 | long |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **temporaryQueueResolver** (advanced) | A pluggable TemporaryQueueResolver that allows you to use your own resolver for creating temporary queues (some messaging systems has special requirements for creating temporary queues). |  | TemporaryQueueResolver |
| **transferException** (advanced) | If enabled and you are using Request Reply messaging (InOut) and an Exchange failed on the consumer side, then the caused Exception will be send back in response as a jakarta.jms.ObjectMessage. If the client is Camel, the returned Exception is rethrown. This allows you to use Camel JMS as a bridge in your routing - for example, using persistent queues to enable robust routing. Notice that if you also have transferExchange enabled, this option takes precedence. The caught exception is required to be serializable. The original Exception on the consumer side can be wrapped in an outer exception such as org.apache.camel.RuntimeCamelException when returned to the producer. Use this with caution as the data is using Java Object serialization and requires the received to be able to deserialize the data at Class level, which forces a strong coupling between the producers and consumer!. | false | boolean |
| **transferExchange** (advanced) | You can transfer the exchange over the wire instead of just the body and headers. The following fields are transferred: In body, Out body, Fault body, In headers, Out headers, Fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. You must enable this option on both the producer and consumer side, so Camel knows the payloads is an Exchange and not a regular payload. Use this with caution as the data is using Java Object serialization and requires the receiver to be able to deserialize the data at Class level, which forces a strong coupling between the producers and consumers having to use compatible Camel versions!. | false | boolean |
| **useMessageIDAsCorrelationID** (advanced) | Specifies whether JMSMessageID should always be used as JMSCorrelationID for InOut messages. | false | boolean |
| **waitForProvisionCorrelationToBeUpdatedCounter** (advanced) | Number of times to wait for provisional correlation id to be updated to the actual correlation id when doing request/reply over JMS and when the option useMessageIDAsCorrelationID is enabled. | 50 | int |
| **waitForProvisionCorrelationToBeUpdatedThreadSleepingTime** (advanced) | Interval in millis to sleep each time while waiting for provisional correlation id to be updated. | 100 | long |
| **waitForTemporaryReplyToToBeUpdatedCounter** (advanced) | Number of times to wait for temporary replyTo queue to be created and ready when doing request/reply over JMS. | 200 | int |
| **waitForTemporaryReplyToToBeUpdatedThreadSleepingTime** (advanced) | Interval in millis to sleep each time while waiting for temporary replyTo queue to be ready. | 100 | long |
| **errorHandlerLoggingLevel** (logging) | 

Allows to configure the default errorHandler logging level for logging uncaught exceptions.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | WARN | LoggingLevel |
| **errorHandlerLogStackTrace** (logging) | Allows to control whether stack-traces should be logged or not, by the default errorHandler. | true | boolean |
| **deserializationFilter** (security) | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied as a defense-in-depth check on the class of the body returned by jakarta.jms.ObjectMessage.getObject(). The pattern is evaluated after the JMS provider has deserialized the payload, so this option alone does not prevent gadget-chain execution that happens inside the provider’s ObjectInputStream; to block such attacks, also configure the JMS provider’s own deserialization filter and/or the JVM-wide -Djdk.serialFilter. When this option is not set and no JVM-wide filter is configured, a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. is applied. |  | String |
| **password** (security) | Password to use with the ConnectionFactory. You can also configure username/password directly on the ConnectionFactory. |  | String |
| **username** (security) | Username to use with the ConnectionFactory. You can also configure username/password directly on the ConnectionFactory. |  | String |
| **transacted** (transaction) | Specifies whether to use transacted mode. | false | boolean |
| **transactedInOut** (transaction) | Specifies whether InOut operations (request reply) default to using transacted mode If this flag is set to true, then Spring JmsTemplate will have sessionTransacted set to true, and the acknowledgeMode as transacted on the JmsTemplate used for InOut operations. Note from Spring JMS: that within a JTA transaction, the parameters passed to createQueue, createTopic methods are not taken into account. Depending on the Java EE transaction context, the container makes its own decisions on these values. Analogously, these parameters are not taken into account within a locally managed transaction either, since Spring JMS operates on an existing JMS Session in this case. Setting this flag to true will use a short local JMS transaction when running outside of a managed transaction, and a synchronized local JMS transaction in case of a managed transaction (other than an XA transaction) being present. This has the effect of a local JMS transaction being managed alongside the main transaction (which might be a native JDBC transaction), with the JMS transaction committing right after the main transaction. | false | boolean |
| **lazyCreateTransactionManager** (transaction (advanced)) | If true, Camel will create a JmsTransactionManager, if there is no transactionManager injected when option transacted=true. | true | boolean |
| **transactionManager** (transaction (advanced)) | The Spring transaction manager to use. |  | PlatformTransactionManager |
| **transactionName** (transaction (advanced)) | The name of the transaction to use. |  | String |
| **transactionTimeout** (transaction (advanced)) | The timeout value of the transaction (in seconds), if using transacted mode. | \-1 | int |

## Message Headers

The JMS component supports 18 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJmsDestination** (producer) Constant: [`JMS_DESTINATION`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_DESTINATION) | The destination. |  | Destination |
| **CamelJmsDestinationName** (producer) Constant: [`JMS_DESTINATION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_DESTINATION_NAME) | The name of the queue or topic to use as destination. |  | String |
| **CamelJMSDestinationProduced** (common) Constant: [`JMS_DESTINATION_NAME_PRODUCED`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_DESTINATION_NAME_PRODUCED) | The name of the queue or topic the message was sent to. |  | String |
| **JMSXGroupID** (common) Constant: [`JMS_X_GROUP_ID`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_X_GROUP_ID) | The JMS group ID. |  | String |
| **JMSMessageID** (common) Constant: [`JMS_HEADER_MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_MESSAGE_ID) | The JMS unique message ID. |  | String |
| **JMSCorrelationID** (common) Constant: [`JMS_HEADER_CORRELATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_CORRELATION_ID) | The JMS correlation ID. |  | String |
| **JMSCorrelationIDAsBytes** (common) Constant: [`JMS_HEADER_CORRELATION_ID_AS_BYTES`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_CORRELATION_ID_AS_BYTES) | The JMS correlation ID as bytes. |  | byte\[\] |
| **JMSDeliveryMode** (common) Constant: [`JMS_HEADER_DELIVERY_MODE`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_DELIVERY_MODE) | The JMS delivery mode. |  | int |
| **JMSDestination** (common) Constant: [`JMS_HEADER_DESTINATION`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_DESTINATION) | The JMS destination. |  | Destination |
| **JMSExpiration** (common) Constant: [`JMS_HEADER_EXPIRATION`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_EXPIRATION) | The JMS expiration. |  | long |
| **JMSPriority** (common) Constant: [`JMS_HEADER_PRIORITY`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_PRIORITY) | The JMS priority (with 0 as the lowest priority and 9 as the highest). |  | int |
| **JMSRedelivered** (common) Constant: [`JMS_HEADER_REDELIVERED`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_REDELIVERED) | Is the JMS message redelivered. |  | boolean |
| **JMSTimestamp** (common) Constant: [`JMS_HEADER_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_TIMESTAMP) | The JMS timestamp. |  | long |
| **JMSReplyTo** (common) Constant: [`JMS_HEADER_REPLY_TO`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_REPLY_TO) | The JMS reply-to destination. |  | Destination |
| **JMSType** (common) Constant: [`JMS_HEADER_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_TYPE) | The JMS type. |  | String |
| **JMSXUserID** (common) Constant: [`JMS_HEADER_XUSER_ID`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_HEADER_XUSER_ID) | The XUser id. |  | String |
| **CamelJmsMessageType** (common) Constant: [`JMS_MESSAGE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_MESSAGE_TYPE) | 
The message type.

Enum values:

-   Bytes
    
-   Map
    
-   Object
    
-   Stream
    
-   Text
    
-   Blob
    





 |  | JmsMessageType |
| **CamelJmsRequestTimeout** (producer) Constant: [`JMS_REQUEST_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-jms/latest/org/apache/camel/component/jms/JmsConstants.html#JMS_REQUEST_TIMEOUT) | The timeout for waiting for a reply when using the InOut Exchange Pattern (in milliseconds). | 20000 | long |

## Examples

JMS is used in many examples for other components as well. But we provide a few samples below to get started.

### Receiving from JMS

In the following sample, we configure a route that receives JMS messages and routes the message to a POJO:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms:queue:foo")
  .to("bean:myBusinessLogic");
```

```xml
<route>
  <from uri="jms:queue:foo"/>
  <to uri="bean:myBusinessLogic"/>
</route>
```

```yaml
- route:
    from:
      uri: jms:queue:foo
      steps:
        - to:
            uri: bean:myBusinessLogic
```

You can use any of the EIP patterns so the route can be context based. For example, here’s how to filter an order topic for the big spenders:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms:topic:OrdersTopic")
  .filter().method("myBean", "isGoldCustomer")
  .to("jms:queue:BigSpendersQueue");
```

```xml
<route>
  <from uri="jms:topic:OrdersTopic"/>
  <filter>
    <method ref="myBean" method="isGoldCustomer"/>
    <to uri="jms:queue:BigSpendersQueue"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: jms:topic:OrdersTopic
      steps:
        - filter:
            method:
              ref: myBean
              method: isGoldCustomer
            steps:
              - to:
                  uri: jms:queue:BigSpendersQueue
```

### Sending to JMS

In the sample below, we poll a file folder and send the file content to a JMS topic. As we want the content of the file as a `TextMessage` instead of a `BytesMessage`, we need to convert the body to a `String`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://orders")
  .convertBodyTo(String.class)
  .to("jms:topic:OrdersTopic");
```

```xml
<route>
  <from uri="file://orders"/>
  <convertBodyTo type="String"/>
  <to uri="jms:topic:OrdersTopic"/>
</route>
```

```yaml
- route:
    from:
      uri: file://orders
      steps:
        - convertBodyTo:
            type: String
        - to:
            uri: jms:topic:OrdersTopic
```

### Using Annotations

Camel also has annotations, so you can use [POJO Consuming](../../manual/pojo-consuming.md) and [POJO Producing](../../manual/pojo-producing.md).

### Other Examples

JMS appears in many of the examples for other components and EIP patterns, as well in this Camel documentation. So feel free to browse the documentation.

### Using JMS as a Dead Letter Queue storing Exchange

Normally, when using [JMS](#) as the transport, it only transfers the body and headers as the payload. If you want to use [JMS](#) with a [Dead Letter Channel](eips/dead-letter-channel.md), using a JMS queue as the Dead Letter Queue, then normally the caused Exception is not stored in the JMS message. You can, however, use the `transferExchange` option on the JMS dead letter queue to instruct Camel to store the entire Exchange in the queue as a `javax.jms.ObjectMessage` that holds a `org.apache.camel.support.DefaultExchangeHolder`. This allows you to consume from the Dead Letter Queue and retrieve the caused exception from the Exchange property with the key `Exchange.EXCEPTION_CAUGHT`. The demo below illustrates this:

_Java-only: `errorHandler` configuration is Java DSL specific_

```java
// setup error handler to use JMS as queue and store the entire Exchange
errorHandler(deadLetterChannel("jms:queue:dead?transferExchange=true"));
```

Then you can consume from the JMS queue and analyze the problem:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms:queue:dead").to("bean:myErrorAnalyzer");
```

```xml
<route>
  <from uri="jms:queue:dead"/>
  <to uri="bean:myErrorAnalyzer"/>
</route>
```

```yaml
- route:
    from:
      uri: jms:queue:dead
      steps:
        - to:
            uri: bean:myErrorAnalyzer
```

And in the `myErrorAnalyzer` bean:

_Java-only: programmatic access to exchange properties and exception_

```java
String body = exchange.getIn().getBody();
Exception cause = exchange.getProperty(Exchange.EXCEPTION_CAUGHT, Exception.class);
// the cause message is
String problem = cause.getMessage();
```

### Using JMS as a Dead Letter Channel storing error only

You can use JMS to store the cause error message or to store a custom body, which you can initialize yourself. The following example uses the Message Translator EIP to do a transformation on the failed exchange before it is moved to the [JMS](#) dead letter queue:

_Java-only: `errorHandler` and `exceptionMessage()` are Java DSL specific_

```java
// we sent it to a seda dead queue first
errorHandler(deadLetterChannel("seda:dead"));

// and on the seda dead queue we can do the custom transformation before its sent to the JMS queue
from("seda:dead").transform(exceptionMessage()).to("jms:queue:dead");
```

Here we only store the original cause error message in the transform. You can, however, use any Expression to send whatever you like. For example, you can invoke a method on a Bean or use a custom processor.

## Usage

### Message Mapping between JMS and Camel

Camel automatically maps messages between `javax.jms.Message` and `org.apache.camel.Message`.

When sending a JMS message, Camel converts the message body to the following JMS message types:

  
| Body Type | JMS Message | Comment |
| --- | --- | --- |
| `String` | `javax.jms.TextMessage` |  |
| `org.w3c.dom.Node` | `javax.jms.TextMessage` | The DOM will be converted to `String`. |
| `Map` | `javax.jms.MapMessage` |  |
| `java.io.Serializable` | `javax.jms.ObjectMessage` |  |
| `byte[]` | `javax.jms.BytesMessage` |  |
| `java.io.File` | `javax.jms.BytesMessage` |  |
| `java.io.Reader` | `javax.jms.BytesMessage` |  |
| `java.io.InputStream` | `javax.jms.BytesMessage` |  |
| `java.nio.ByteBuffer` | `javax.jms.BytesMessage` |  |

When receiving a JMS message, Camel converts the JMS message to the following body type:

 
| JMS Message | Body Type |
| --- | --- |
| `javax.jms.TextMessage` | `String` |
| `javax.jms.BytesMessage` | `byte[]` |
| `javax.jms.MapMessage` | `Map<String, Object>` |
| `javax.jms.ObjectMessage` | `Object` |

### Disabling auto-mapping of JMS messages

You can use the `mapJmsMessage` option to disable the auto-mapping above. If disabled, Camel will not try to map the received JMS message, but instead uses it directly as the payload. This allows you to avoid the overhead of mapping and let Camel just pass through the JMS message. For instance, it even allows you to route `javax.jms.ObjectMessage` JMS messages with classes you do **not** have on the classpath.

### Using a custom MessageConverter

You can use the `messageConverter` option to do the mapping yourself in a Spring `org.springframework.jms.support.converter.MessageConverter` class.

For example, in the route below, we use a custom message converter when sending a message to the JMS order queue:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://inbox/order").to("jms:queue:order?messageConverter=#myMessageConverter");
```

```xml
<route>
  <from uri="file://inbox/order"/>
  <to uri="jms:queue:order?messageConverter=#myMessageConverter"/>
</route>
```

```yaml
- route:
    from:
      uri: file://inbox/order
      steps:
        - to:
            uri: jms:queue:order
            parameters:
              messageConverter: "#myMessageConverter"
```

You can also use a custom message converter when consuming from a JMS destination.

### Controlling the mapping strategy selected

You can use the `jmsMessageType` option on the endpoint URL to force a specific message type for all messages.

In the route below, we poll files from a folder and send them as `javax.jms.TextMessage` as we have forced the JMS producer endpoint to use text messages:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://inbox/order").to("jms:queue:order?jmsMessageType=Text");
```

```xml
<route>
  <from uri="file://inbox/order"/>
  <to uri="jms:queue:order?jmsMessageType=Text"/>
</route>
```

```yaml
- route:
    from:
      uri: file://inbox/order
      steps:
        - to:
            uri: jms:queue:order
            parameters:
              jmsMessageType: Text
```

You can also specify the message type to use for each message by setting the header with the key `CamelJmsMessageType`. For example:

_Java-only: uses the `JmsMessageType` enum which requires Java code_

```java
from("file://inbox/order").setHeader("CamelJmsMessageType", JmsMessageType.Text).to("jms:queue:order");
```

The possible values are defined in the `enum` class, `org.apache.camel.jms.JmsMessageType`.

### Message format when sending

The exchange sent over the JMS wire must conform to the [JMS Message spec](http://java.sun.com/j2ee/1.4/docs/api/javax/jms/Message.md).

For the `exchange.in.header` the following rules apply for the header **keys**:

-   Keys starting with `JMS` or `JMSX` are reserved.
    
-   `exchange.in.headers` keys must be literals and all be valid Java identifiers (do not use dots in the key name).
    
-   Camel replaces dots & hyphens and the reverse when consuming JMS messages:  
    `.` is replaced by `_DOT_` and the reverse replacement when Camel consumes the message.  
    `-` is replaced by `_HYPHEN_` and the reverse replacement when Camel consumes the message.
    
-   See also the option `jmsKeyFormatStrategy`, which allows use of your own custom strategy for formatting keys.
    

For the `exchange.in.header`, the following rules apply for the header **values**:

-   The values must be primitives or their counter-objects (such as `Integer`, `Long`, `Character`). The types, `String`, `CharSequence`, `Date`, `BigDecimal` and `BigInteger` are all converted to their `toString()` representation. All other types are dropped.
    

Camel will log with category `org.apache.camel.component.jms.JmsBinding` at **DEBUG** level if it drops a given header value. For example:

2008-07-09 06:43:04,046 \[main           \] DEBUG JmsBinding
  - Ignoring non primitive header: order of class: org.apache.camel.component.jms.issues.DummyOrder with value: DummyOrder{orderId=333, itemId=4444, quantity=2}

### Message format when receiving

Camel adds the following properties to the `Exchange` when it receives a message:

  
| Property | Type | Description |
| --- | --- | --- |
| `org.apache.camel.jms.replyDestination` | `javax.jms.Destination` | The reply destination. |

Camel adds the following JMS properties to the In message headers when it receives a JMS message:

  
| Header | Type | Description |
| --- | --- | --- |
| `JMSCorrelationID` | `String` | The JMS correlation ID. |
| `JMSDeliveryMode` | `int` | The JMS delivery mode. |
| `JMSDestination` | `javax.jms.Destination` | The JMS destination. |
| `JMSExpiration` | `long` | The JMS expiration. |
| `JMSMessageID` | `String` | The JMS unique message ID. |
| `JMSPriority` | `int` | The JMS priority (with 0 as the lowest priority and 9 as the highest). |
| `JMSRedelivered` | `boolean` | Whether the JMS message is redelivered. |
| `JMSReplyTo` | `javax.jms.Destination` | The JMS reply-to destination. |
| `JMSTimestamp` | `long` | The JMS timestamp. |
| `JMSType` | `String` | The JMS type. |
| `JMSXGroupID` | `String` | The JMS group ID. |

As all the above information is standard JMS, you can check the [JMS documentation](http://java.sun.com/javaee/5/docs/api/javax/jms/Message.md) for further details.

### About using Camel to send and receive messages and JMSReplyTo

The JMS component is complex, and you have to pay close attention to how it works in some cases. So this is a short summary of some areas/pitfalls to look for.

When Camel sends a message using its `JMSProducer`, it checks the following conditions:

-   The message exchange pattern.
    
-   Whether a `JMSReplyTo` was set in the endpoint or in the message headers.
    
-   Whether any of the following options have been set on the JMS endpoint: `disableReplyTo`, `preserveMessageQos`, `explicitQosEnabled`.
    

All this can be a tad complex to understand and configure to support your use case.

#### JmsProducer

The `JmsProducer` behaves as follows, depending on configuration:

  
| Exchange Pattern | Other options | Description |
| --- | --- | --- |
| _InOut_ | \- | Camel will expect a reply, set a temporary `JMSReplyTo`, and after sending the message, it will start to listen for the reply message on the temporary queue. |
| _InOut_ | `JMSReplyTo` is set | Camel will expect a reply and, after sending the message, it will start to listen for the reply message on the specified `JMSReplyTo` queue. |
| _InOnly_ | \- | Camel will send the message and **not** expect a reply. |
| _InOnly_ | `JMSReplyTo` is set | By default, Camel discards the `JMSReplyTo` destination and clears the `JMSReplyTo` header before sending the message. Camel then sends the message and does **not** expect a reply. Camel logs this in the log at `WARN` level (changed to `DEBUG` level from **Camel 2.6** onwards. You can use `preserveMessageQuo=true` to instruct Camel to keep the `JMSReplyTo`. In all situations the `JmsProducer` does **not** expect any reply and thus continue after sending the message. |

#### JmsConsumer

The `JmsConsumer` behaves as follows, depending on configuration:

  
| Exchange Pattern | Other options | Description |
| --- | --- | --- |
| _InOut_ | \- | Camel will send the reply back to the `JMSReplyTo` queue. |
| _InOnly_ | \- | Camel will not send a reply back, as the pattern is _InOnly_. |
| \- | `disableReplyTo=true` | This option suppress replies. |

So pay attention to the message exchange pattern set on your exchanges.

If you send a message to a JMS destination in the middle of your route, you can specify the exchange pattern to use, see more at Request Reply.  
This is useful if you want to send an `InOnly` message to a JMS topic:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:queue:in")
   .to("bean:validateOrder")
   .to(ExchangePattern.InOnly, "activemq:topic:order")
   .to("bean:handleOrder");
```

```xml
<route>
  <from uri="activemq:queue:in"/>
  <to uri="bean:validateOrder"/>
  <inOnly uri="activemq:topic:order"/>
  <to uri="bean:handleOrder"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:queue:in
      steps:
        - to:
            uri: bean:validateOrder
        - inOnly:
            uri: activemq:topic:order
        - to:
            uri: bean:handleOrder
```

### Reuse endpoint and send to different destinations computed at runtime

If you need to send messages to a lot of different JMS destinations, it makes sense to reuse a JMS endpoint and specify the real destination in a message header. This allows Camel to reuse the same endpoint, but send to different destinations. This greatly reduces the number of endpoints created and economizes on memory and thread resources.

You can specify the destination in the following headers:

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelJmsDestination` | `javax.jms.Destination` | A destination object. |
| `CamelJmsDestinationName` | `String` | The destination name. |

For example, the following route shows how you can compute a destination at run time and use it to override the destination appearing in the JMS URL:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://inbox")
  .to("bean:computeDestination")
  .to("activemq:queue:dummy");
```

```xml
<route>
  <from uri="file://inbox"/>
  <to uri="bean:computeDestination"/>
  <to uri="activemq:queue:dummy"/>
</route>
```

```yaml
- route:
    from:
      uri: file://inbox
      steps:
        - to:
            uri: bean:computeDestination
        - to:
            uri: activemq:queue:dummy
```

The queue name, `dummy`, is just a placeholder. It must be provided as part of the JMS endpoint URL, but it will be ignored in this example.

In the `computeDestination` bean, specify the real destination by setting the `CamelJmsDestinationName` header as follows:

_Java-only: bean method that sets the destination header programmatically_

```java
public void setJmsHeader(Exchange exchange) {
   String id = ....
   exchange.getIn().setHeader("CamelJmsDestinationName", "order:" + id);
}
```

Then Camel will read this header and use it as the destination instead of the one configured on the endpoint. So, in this example Camel sends the message to `activemq:queue:order:2`, assuming the `id` value was 2.

If both the `CamelJmsDestination` and the `CamelJmsDestinationName` headers are set, `CamelJmsDestination` takes priority. Keep in mind that the JMS producer removes both `CamelJmsDestination` and `CamelJmsDestinationName` headers from the exchange and do not propagate them to the created JMS message to avoid the accidental loops in the routes (in scenarios when the message will be forwarded to another JMS endpoint).

### Configuring different JMS providers

You can configure your JMS provider in Spring XML as follows:

You can configure as many JMS component instances as you wish and give them **a unique name using the** `id` **attribute**. The preceding example configures an `activemq` component. You could do the same to configure MQSeries, TibCo, BEA, Sonic and so on.

Once you have a named JMS component, you can then refer to endpoints within that component using URIs. For example, for the component name, `activemq`, you can then refer to destinations using the URI format, `activemq:[queue:|topic:]destinationName`. You can use the same approach for all other JMS providers.

This works by the SpringCamelContext lazily fetching components from the spring context for the scheme name you use for Endpoint URIs and having the Component resolve the endpoint URIs.

#### Using JNDI to find the ConnectionFactory

If you are using a J2EE container, you might need to look up JNDI to find the JMS `ConnectionFactory` rather than use the usual `<bean>` mechanism in Spring. You can do this using Spring’s factory bean or the new Spring XML namespace. For example:

```xml
<bean id="weblogic" class="org.apache.camel.component.jms.JmsComponent">
  <property name="connectionFactory" ref="myConnectionFactory"/>
</bean>

<jee:jndi-lookup id="myConnectionFactory" jndi-name="jms/connectionFactory"/>
```

See [The jee schema](http://static.springsource.org/spring/docs/3.0.x/spring-framework-reference/html/xsd-config.html#xsd-config-body-schemas-jee) in the Spring reference documentation for more details about JNDI lookup.

### Concurrent Consuming

A common requirement with JMS is to consume messages concurrently in multiple threads to make an application more responsive. You can set the `concurrentConsumers` option to specify the number of threads servicing the JMS endpoint, as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms:SomeQueue?concurrentConsumers=20")
  .bean(MyClass.class);
```

```xml
<route>
  <from uri="jms:SomeQueue?concurrentConsumers=20"/>
  <to uri="bean:MyClass"/>
</route>
```

```yaml
- route:
    from:
      uri: jms:SomeQueue
      parameters:
        concurrentConsumers: 20
      steps:
        - to:
            uri: bean:MyClass
```

You can configure this option in one of the following ways:

-   On the `JmsComponent`,
    
-   On the endpoint URI or,
    
-   By invoking `setConcurrentConsumers()` directly on the `JmsEndpoint`.
    

#### Concurrent Consuming with async consumer

Notice that each concurrent consumer will only pick up the next available message from the JMS broker, when the current message has been fully processed. You can set the option `asyncConsumer=true` to let the consumer pick up the next message from the JMS queue, while the previous message is being processed asynchronously (by the Asynchronous Routing Engine). See more details in the table on top of the page about the `asyncConsumer` option.

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms:SomeQueue?concurrentConsumers=20&asyncConsumer=true")
  .bean(MyClass.class);
```

```xml
<route>
  <from uri="jms:SomeQueue?concurrentConsumers=20&amp;asyncConsumer=true"/>
  <to uri="bean:MyClass"/>
</route>
```

```yaml
- route:
    from:
      uri: jms:SomeQueue
      parameters:
        concurrentConsumers: 20
        asyncConsumer: true
      steps:
        - to:
            uri: bean:MyClass
```

### Request-reply over JMS

Camel supports Request Reply over JMS. In essence the MEP of the Exchange should be `InOut` when you send a message to a JMS queue.

Camel offers a number of options to configure request/reply over JMS that influence performance and clustered environments. The table below summaries the options.

   
| Option | Performance | Cluster | Description |
| --- | --- | --- | --- |
| `Temporary` | Fast | Yes | A temporary queue is used as reply queue, and automatic created by Camel. To use this, do **not** specify a `replyTo` queue name. And you can optionally configure `replyToType=Temporary` to make it stand out that temporary queues are in use. |
| `Shared` | Slow | Yes | A shared persistent queue is used as reply queue. The queue must be created beforehand, although some brokers can create them on the fly, such as Apache ActiveMQ. To use this, you must specify the replyTo queue name. And you can optionally configure `replyToType=Shared` to make it stand out that shared queues are in use. A shared queue can be used in a clustered environment with multiple nodes running this Camel application at the same time. All of them using the same shared reply queue. This is possible because JMS Message selectors are used to correlate expected reply messages; this impacts performance though. JMS Message selectors are slower, and therefore not as fast as `Temporary` or `Exclusive` queues. See further below how to tweak this for better performance. |
| `Exclusive` | Fast | No (\*Yes) | An exclusive persistent queue is used as reply queue. The queue must be created beforehand, although some brokers can create them on the fly, such as Apache ActiveMQ. To use this, you must specify the replyTo queue name. And you **must** configure `replyToType=Exclusive` to instruct Camel to use exclusive queues, as `Shared` is used by default, if a `replyTo` queue name was configured. When using exclusive reply queues, then JMS Message selectors are **not** in use, and therefore other applications must not use this queue as well. An exclusive queue **cannot** be used in a clustered environment with multiple nodes running this Camel application at the same time; as we do not have control if the reply queue comes back to the same node that sent the request message; that is why shared queues use JMS Message selectors to make sure of this. **Though** if you configure each Exclusive reply queue with a unique name per node, then you can run this in a clustered environment. As then the reply message will be sent back to that queue for the given node that awaits the reply message. |
| `concurrentConsumers` | Fast | Yes | Allows processing reply messages concurrently using concurrent message listeners in use. You can specify a range using the `concurrentConsumers` and `maxConcurrentConsumers` options. **Notice:** That using `Shared` reply queues may not work as well with concurrent listeners, so use this option with care. |
| `maxConcurrentConsumers` | Fast | Yes | Allows processing reply messages concurrently using concurrent message listeners in use. You can specify a range using the `concurrentConsumers` and `maxConcurrentConsumers` options. **Notice:** That using `Shared` reply queues may not work as well with concurrent listeners, so use this option with care. |

The `JmsProducer` detects the `InOut` and provides a `JMSReplyTo` header with the reply destination to be used. By default, Camel uses a temporary queue, but you can use the `replyTo` option on the endpoint to specify a fixed reply queue (see more below about fixed reply queue).

Camel will automatically set up a consumer that listens to on the reply queue, so you should **not** do anything.  
This consumer is a Spring `DefaultMessageListenerContainer` which listen for replies. However, it’s fixed to one concurrent consumer.  
That means replies will be processed in sequence as there is only one thread to process the replies. You can configure the listener to use concurrent threads using the `concurrentConsumers` and `maxConcurrentConsumers` options. This allows you to easier configure this in Camel as shown below:

_Java-only: uses `inOut()` Java DSL method for request-reply pattern_

```java
from(xxx)
.inOut().to("activemq:queue:foo?concurrentConsumers=5")
.to(yyy)
.to(zzz);
```

In this route, we instruct Camel to route replies asynchronously using a thread pool with five threads.

#### Request-reply over JMS and using a shared fixed reply queue

If you use a fixed reply queue when doing Request Reply over JMS as shown in the example below, then pay attention.

_Java-only: uses `inOut()` Java DSL method for request-reply pattern_

```java
from(xxx)
.inOut().to("activemq:queue:foo?replyTo=bar")
.to(yyy)
```

In this example, the fixed reply queue named "bar" is used. By default, Camel assumes the queue is shared when using fixed reply queues, and therefore it uses a `JMSSelector` to only pick up the expected reply messages (e.g., based on the `JMSCorrelationID`). See the next section for exclusive fixed reply queues. That means it’s not as fast as temporary queues. You can speed up how often Camel will pull for reply messages using the `receiveTimeout` option. By default, its 1000 milliseconds. So to make it faster, you can set it to 250 millis to pull 4 times per second as shown:

_Java-only: uses `inOut()` Java DSL method for request-reply pattern_

```java
from(xxx)
.inOut().to("activemq:queue:foo?replyTo=bar&receiveTimeout=250")
.to(yyy)
```

Notice this will cause the Camel to send pull requests to the message broker more frequently, and thus require more network traffic.  
It is generally recommended to use temporary queues if possible.

#### Request-reply over JMS and using an exclusive fixed reply queue

In the previous example, Camel would anticipate the fixed reply queue named "bar" was shared, and thus it uses a `JMSSelector` to only consume reply messages which it expects. However, there is a drawback to doing this as the JMS selector is slower. Also, the consumer on the reply queue is slower to update with new JMS selector ids. In fact, it only updates when the `receiveTimeout` option times out, which by default is 1 second. So in theory, the reply messages could take up till about 1 sec to be detected. On the other hand, if the fixed reply queue is exclusive to the Camel reply consumer, then we can avoid using the JMS selectors, and thus be more performant. In fact, as fast as using temporary queues. There is the `ReplyToType` option which you can configure to `Exclusive`  
to tell Camel that the reply queue is exclusive as shown in the example below:

_Java-only: uses `inOut()` Java DSL method for request-reply pattern_

```java
from(xxx)
.inOut().to("activemq:queue:foo?replyTo=bar&replyToType=Exclusive")
.to(yyy)
```

Mind that the queue must be exclusive to each and every endpoint. So if you have two routes, then they each need a unique reply queue as shown in the next example:

_Java-only: uses `inOut()` Java DSL method for request-reply pattern_

```java
from(xxx)
.inOut().to("activemq:queue:foo?replyTo=bar&replyToType=Exclusive")
.to(yyy)

from(aaa)
.inOut().to("activemq:queue:order?replyTo=order.reply&replyToType=Exclusive")
.to(bbb)
```

The same applies if you run in a clustered environment. Then each node in the cluster must use a unique reply queue name. As otherwise, each node in the cluster may pick up messages intended as a reply on another node. For clustered environments, it’s recommended to use shared reply queues instead.

### Synchronizing clocks between senders and receivers

When doing messaging between systems, it is desirable that the systems have synchronized clocks. For example, when sending a [JMS](#) message, then you can set a time to live value on the message. Then the receiver can inspect this value and determine if the message is already expired, and thus drop the message instead of consume and process it. However, this requires that both sender and receiver have synchronized clocks.

> **Note**
> If you are using [ActiveMQ](http://activemq.apache.org/), then you can use the [timestamp plugin](http://activemq.apache.org/timestampplugin.md) to synchronize clocks.

### About time to live

Read first above about synchronized clocks.

When you do request/reply (InOut) over [JMS](#) with Camel, then Camel uses a timeout on the sender side, which is default 20 seconds from the `requestTimeout` option. You can control this by setting a higher/lower value. However, the time to live value is still set on the [JMS](#) message being sent. So that requires the clocks to be synchronized between the systems. If they are not, then you may want to disable the time to live value being set. This is now possible using the `disableTimeToLive` option from **Camel 2.8** onwards. So if you set this option to `disableTimeToLive=true`, then Camel does **not** set any time to live value when sending [JMS](#) messages. **But** the request timeout is still active. So for example, if you do request/reply over [JMS](#) and have disabled time to live, then Camel will still use a timeout by 20 seconds (the `requestTimeout` option). That option can also be configured. So the two options `requestTimeout` and `disableTimeToLive` gives you Fine-grained control when doing request/reply.

You can provide a header in the message to override and use as the request timeout value instead of the endpoint configured value. For example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:someWhere")
  .to("jms:queue:foo?replyTo=bar&requestTimeout=30s")
  .to("bean:processReply");
```

```xml
<route>
  <from uri="direct:someWhere"/>
  <to uri="jms:queue:foo?replyTo=bar&amp;requestTimeout=30s"/>
  <to uri="bean:processReply"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:someWhere
      steps:
        - to:
            uri: jms:queue:foo
            parameters:
              replyTo: bar
              requestTimeout: 30s
        - to:
            uri: bean:processReply
```

In the route above we have an endpoint configured `requestTimeout` of 30 seconds. So Camel will wait up till 30 seconds for that reply message to come back on the bar queue. If no reply message is received then a `org.apache.camel.ExchangeTimedOutException` is set on the Exchange, and Camel continues routing the message, which would then fail due the exception, and Camel’s error handler reacts.

If you want to use a per message timeout value, you can set the header `CamelJmsRequestTimeout` with a timeout value as a long type.

> **Tip**
> The header name is `CamelJmsRequestTimeout`.

For example, we can use a bean to compute the timeout value per individual message, such as calling the `"whatIsTheTimeout"` method on the service bean as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:someWhere")
  .setHeader("CamelJmsRequestTimeout", method(ServiceBean.class, "whatIsTheTimeout"))
  .to("jms:queue:foo?replyTo=bar&requestTimeout=30s")
  .to("bean:processReply");
```

```xml
<route>
  <from uri="direct:someWhere"/>
  <setHeader name="CamelJmsRequestTimeout">
    <method ref="serviceBean" method="whatIsTheTimeout"/>
  </setHeader>
  <to uri="jms:queue:foo?replyTo=bar&amp;requestTimeout=30s"/>
  <to uri="bean:processReply"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:someWhere
      steps:
        - setHeader:
            name: CamelJmsRequestTimeout
            method:
              ref: serviceBean
              method: whatIsTheTimeout
        - to:
            uri: jms:queue:foo
            parameters:
              replyTo: bar
              requestTimeout: 30s
        - to:
            uri: bean:processReply
```

When you do fire and forget (InOut) over [JMS](#) with Camel, then Camel by default does **not** set any time to live value on the message. You can configure a value by using the `timeToLive` option. For example, to indicate a 5 sec., you set `timeToLive=5000`. The option `disableTimeToLive` can be used to force disabling the time to live, also for InOnly messaging. The `requestTimeout` option is not being used for InOnly messaging.

### Enabling Transacted Consumption

A common requirement is to consume from a queue in a transaction and then process the message using the Camel route. To do this, just ensure that you set the following properties on the component/endpoint:

-   `transacted` = true
    
-   `transactionManager` = a _Transsaction Manager_ - typically the `JmsTransactionManager`
    

See the Transactional Client EIP pattern for further details.

Transactions and \[Request Reply\] over JMS

When using Request Reply over JMS, you cannot use a single transaction; JMS will not send any messages until a commit is performed, so the server side won’t receive anything at all until the transaction commits. Therefore, to use [Request Reply](eips/requestReply-eip.md), you must commit a transaction after sending the request and then use a separate transaction for receiving the response.

To address this issue, the JMS component uses different properties to specify transaction use for oneway messaging and request reply messaging:

The `transacted` property applies **only** to the InOnly message Exchange Pattern (MEP).

You can leverage the [DMLC transacted session API](http://static.springsource.org/spring/docs/3.0.x/javadoc-api/org/springframework/jms/listener/AbstractPollingMessageListenerContainer.html#setSessionTransacted\(boolean\)) using the following properties on component/endpoint:

-   `transacted` = true
    
-   `lazyCreateTransactionManager` = false
    

The benefit of doing so is that the cacheLevel setting will be honored when using local transactions without a configured TransactionManager. When a TransactionManager is configured, no caching happens at DMLC level, and it is necessary to rely on a pooled connection factory. For more details about this kind of setup, see [here](http://tmielke.blogspot.com/2012/03/camel-jms-with-transactions-lessons.md) and [here](http://forum.springsource.org/showthread.php?123631-JMS-DMLC-not-caching%20connection-when-using-TX-despite-cacheLevel-CACHE_CONSUMER&p=403530&posted=1#post403530).

### Using JMSReplyTo for late replies

When using Camel as a JMS listener, it sets an Exchange property with the value of the ReplyTo `javax.jms.Destination` object, having the key `ReplyTo`. You can obtain this `Destination` as follows:

_Java-only: uses JMS `Destination` object and Camel Java API_

```java
Destination replyDestination = exchange.getIn().getHeader("JMSReplyTo", Destination.class);
```

And then later use it to send a reply using regular JMS or Camel.

_Java-only: uses `JmsEndpoint` and `ProducerTemplate` Java API_

```java
// we need to pass in the JMS component, and in this sample we use ActiveMQ
JmsEndpoint endpoint = JmsEndpoint.newInstance(replyDestination, activeMQComponent);
// now we have the endpoint we can use regular Camel API to send a message to it
template.sendBody(endpoint, "Here is the late reply.");
```

A different solution to sending a reply is to provide the `replyDestination` object in the same Exchange property when sending. Camel will then pick up this property and use it for the real destination. The endpoint URI must include a dummy destination, however. For example:

_Java-only: uses `ProducerTemplate` and `Processor` to set the JMS destination object programmatically_

```java
// we pretend to send it to some non-existing dummy queue
template.send("activemq:queue:dummy", exchange -> {
      // and here we override the destination with the ReplyTo destination object so the message is sent to there instead of dummy
      exchange.getIn().setHeader("CamelJmsDestination", replyDestination);
      exchange.getIn().setBody("Here is the late reply.");
});
```

### Using a request timeout

In the sample below we send a Request Reply style message Exchange (we use the `requestBody` method = `InOut`) to the slow queue for further processing in Camel, and we wait for a return reply:

### Sending an InOnly message and keeping the JMSReplyTo header

When sending to a [JMS](#) destination using **camel-jms**, the producer will use the MEP to detect if it is `InOnly` or `InOut` messaging. However, there can be times when you want to send an `InOnly` message but keeping the `JMSReplyTo` header. To do so, you have to instruct Camel to keep it, otherwise the `JMSReplyTo` header will be dropped.

For example, to send an `InOnly` message to the foo queue, but with a `JMSReplyTo` with bar queue you can do as follows:

_Java-only: uses `ProducerTemplate` test API to send with custom JMS headers_

```java
template.send("activemq:queue:foo?preserveMessageQos=true", exchange -> {
      exchange.getIn().setBody("World");
      exchange.getIn().setHeader("JMSReplyTo", "bar");
});
```

Notice we use `preserveMessageQos=true` to instruct Camel to keep the `JMSReplyTo` header.

### Setting JMS provider options on the destination

Some JMS providers, like IBM’s WebSphere MQ, need options to be set on the JMS destination. For example, you may need to specify the `targetClient` option. Since `targetClient` is a WebSphere MQ option and not a Camel URI option, you need to set that on the JMS destination name like so:

-   Java
    
-   XML
    
-   YAML
    

```java
// ...
.setHeader("CamelJmsDestinationName", constant("queue:///MY_QUEUE?targetClient=1"))
.to("wmq:queue:MY_QUEUE?useMessageIDAsCorrelationID=true");
```

```xml
<!-- ... -->
<setHeader name="CamelJmsDestinationName">
  <constant>queue:///MY_QUEUE?targetClient=1</constant>
</setHeader>
<to uri="wmq:queue:MY_QUEUE?useMessageIDAsCorrelationID=true"/>
```

```yaml
# ...
- setHeader:
    name: CamelJmsDestinationName
    constant: "queue:///MY_QUEUE?targetClient=1"
- to:
    uri: wmq:queue:MY_QUEUE
    parameters:
      useMessageIDAsCorrelationID: true
```

Some versions of WMQ won’t accept this option on the destination name, and you will get an exception like:

com.ibm.msg.client.jms.DetailedJMSException: JMSCC0005: The specified
value 'MY\_QUEUE?targetClient=1' is not allowed for
'XMSC\_DESTINATION\_NAME'

A workaround is to use a custom DestinationResolver:

_Java-only: programmatic JMS component configuration with custom \`DestinationResolver\`_

```java
JmsComponent wmq = new JmsComponent(connectionFactory);

wmq.setDestinationResolver((session, destinationName, pubSubDomain) -> {
    MQQueueSession wmqSession = (MQQueueSession) session;
    return wmqSession.createQueue("queue:///" + destinationName + "?targetClient=1");
});
```

## Spring Boot Auto-Configuration

When using jms with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jms-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 110 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jms.accept-messages-while-stopping** | Specifies whether the consumer accept messages while it is stopping. You may consider enabling this option, if you start and stop JMS routes at runtime, while there are still messages enqueued on the queue. If this option is false, and you stop the JMS route, then messages may be rejected, and the JMS broker would have to attempt redeliveries, which yet again may be rejected, and eventually the message may be moved at a dead letter queue on the JMS broker. To avoid this its recommended to enable this option. | false | Boolean |
| **camel.component.jms.acknowledgement-mode-name** | The JMS acknowledgement name, which is one of: SESSION\_TRANSACTED, CLIENT\_ACKNOWLEDGE, AUTO\_ACKNOWLEDGE, DUPS\_OK\_ACKNOWLEDGE. | AUTO\_ACKNOWLEDGE | String |
| **camel.component.jms.allow-additional-headers** | This option is used to allow additional headers which may have values that are invalid according to JMS specification. For example, some message systems, such as WMQ, do this with header names using prefix JMS\_IBM\_MQMD\_ containing values with byte array or other invalid types. You can specify multiple header names separated by comma, and use as suffix for wildcard matching. |  | String |
| **camel.component.jms.allow-auto-wired-connection-factory** | Whether to auto-discover ConnectionFactory from the registry, if no connection factory has been configured. If only one instance of ConnectionFactory is found then it will be used. This is enabled by default. | true | Boolean |
| **camel.component.jms.allow-auto-wired-destination-resolver** | Whether to auto-discover DestinationResolver from the registry, if no destination resolver has been configured. If only one instance of DestinationResolver is found then it will be used. This is enabled by default. | true | Boolean |
| **camel.component.jms.allow-null-body** | Whether to allow sending messages with no body. If this option is false and the message body is null, then an JMSException is thrown. | true | Boolean |
| **camel.component.jms.allow-reply-manager-quick-stop** | Whether the DefaultMessageListenerContainer used in the reply managers for request-reply messaging allow the DefaultMessageListenerContainer.runningAllowed flag to quick stop in case JmsConfiguration#isAcceptMessagesWhileStopping is enabled, and org.apache.camel.CamelContext is currently being stopped. This quick stop ability is enabled by default in the regular JMS consumers but to enable for reply managers you must enable this flag. | false | Boolean |
| **camel.component.jms.allow-serialized-headers** | Controls whether or not to include serialized headers. Applies only when transferExchange is true. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | Boolean |
| **camel.component.jms.always-copy-message** | If true, Camel will always make a JMS message copy of the message when it is passed to the producer for sending. Copying the message is needed in some situations, such as when a replyToDestinationSelectorName is set (incidentally, Camel will set the alwaysCopyMessage option to true, if a replyToDestinationSelectorName is set). | false | Boolean |
| **camel.component.jms.artemis-consumer-priority** | Consumer priorities allow you to ensure that high priority consumers receive messages while they are active. Normally, active consumers connected to a queue receive messages from it in a round-robin fashion. When consumer priorities are in use, messages are delivered round-robin if multiple active consumers exist with the same high priority. Messages will only going to lower priority consumers when the high priority consumers do not have credit available to consume the message, or those high priority consumers have declined to accept the message (for instance because it does not meet the criteria of any selectors associated with the consumer). |  | Integer |
| **camel.component.jms.artemis-streaming-enabled** | Whether optimizing for Apache Artemis streaming mode. This can reduce memory overhead when using Artemis with JMS StreamMessage types. This option must only be enabled if Apache Artemis is being used. | false | Boolean |
| **camel.component.jms.async-consumer** | Whether the JmsConsumer processes the Exchange asynchronously. If enabled then the JmsConsumer may pickup the next message from the JMS queue, while the previous message is being processed asynchronously (by the Asynchronous Routing Engine). This means that messages may be processed not 100% strictly in order. If disabled (as default) then the Exchange is fully processed before the JmsConsumer will pickup the next message from the JMS queue. Note if transacted has been enabled, then asyncConsumer=true does not run asynchronously, as transaction must be executed synchronously. | false | Boolean |
| **camel.component.jms.async-start-listener** | Whether to startup the JmsConsumer message listener asynchronously, when starting a route. For example if a JmsConsumer cannot get a connection to a remote JMS broker, then it may block while retrying and/or fail-over. This will cause Camel to block while starting routes. By setting this option to true, you will let routes startup, while the JmsConsumer connects to the JMS broker using a dedicated thread in asynchronous mode. If this option is used, then beware that if the connection could not be established, then an exception is logged at WARN level, and the consumer will not be able to receive messages; You can then restart the route to retry. | false | Boolean |
| **camel.component.jms.async-stop-listener** | Whether to stop the JmsConsumer message listener asynchronously, when stopping a route. | false | Boolean |
| **camel.component.jms.auto-startup** | Specifies whether the consumer container should auto-startup. | true | Boolean |
| **camel.component.jms.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jms.browse-limit** | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | Integer |
| **camel.component.jms.cache-level** | Sets the cache level by ID for the underlying JMS resources. See cacheLevelName option for more details. |  | Integer |
| **camel.component.jms.cache-level-name** | Sets the cache level by name for the underlying JMS resources. Possible values are: CACHE\_AUTO, CACHE\_CONNECTION, CACHE\_CONSUMER, CACHE\_NONE, and CACHE\_SESSION. The default setting is CACHE\_AUTO. See the Spring documentation and Transactions Cache Levels for more information. | CACHE\_AUTO | String |
| **camel.component.jms.client-id** | Sets the JMS client ID to use. Note that this value, if specified, must be unique and can only be used by a single JMS connection instance. It is typically only required for durable topic subscriptions with JMS 1.1. |  | String |
| **camel.component.jms.concurrent-consumers** | Specifies the default number of concurrent consumers when consuming from JMS (not for request/reply over JMS). See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. When doing request/reply over JMS then the option replyToConcurrentConsumers is used to control number of concurrent consumers on the reply message listener. | 1 | Integer |
| **camel.component.jms.configuration** | To use a shared JMS configuration. The option is a org.apache.camel.component.jms.JmsConfiguration type. |  | JmsConfiguration |
| **camel.component.jms.connection-factory** | The connection factory to be use. A connection factory must be configured either on the component or endpoint. The option is a jakarta.jms.ConnectionFactory type. |  | ConnectionFactory |
| **camel.component.jms.consumer-type** | The consumer type to use, which can be one of: Simple, Default, or Custom. The consumer type determines which Spring JMS listener to use. Default will use org.springframework.jms.listener.DefaultMessageListenerContainer, Simple will use org.springframework.jms.listener.SimpleMessageListenerContainer. When Custom is specified, the MessageListenerContainerFactory defined by the messageListenerContainerFactory option will determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use. | default | ConsumerType |
| **camel.component.jms.correlation-property** | When using InOut exchange pattern use this JMS property instead of JMSCorrelationID JMS property to correlate messages. If set messages will be correlated solely on the value of this property JMSCorrelationID property will be ignored and not set by Camel. |  | String |
| **camel.component.jms.default-task-executor-type** | Specifies what default TaskExecutor type to use in the DefaultMessageListenerContainer, for both consumer endpoints and the ReplyTo consumer of producer endpoints. Possible values: SimpleAsync (uses Spring’s SimpleAsyncTaskExecutor) or ThreadPool (uses Spring’s ThreadPoolTaskExecutor with optimal values - cached thread-pool-like). If not set, it defaults to the previous behaviour, which uses a cached thread pool for consumer endpoints and SimpleAsync for reply consumers. The use of ThreadPool is recommended to reduce thread trash in elastic configurations with dynamically increasing and decreasing concurrent consumers. |  | DefaultTaskExecutorType |
| **camel.component.jms.delivery-delay** | Sets delivery delay to use for send calls for JMS. This option requires JMS 2.0 compliant broker. | \-1 | Long |
| **camel.component.jms.delivery-mode** | Specifies the delivery mode to be used. Possible values are those defined by jakarta.jms.DeliveryMode. NON\_PERSISTENT = 1 and PERSISTENT = 2. |  | Integer |
| **camel.component.jms.delivery-persistent** | Specifies whether persistent delivery is used by default. | true | Boolean |
| **camel.component.jms.deserialization-filter** | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied as a defense-in-depth check on the class of the body returned by jakarta.jms.ObjectMessage.getObject(). The pattern is evaluated after the JMS provider has deserialized the payload, so this option alone does not prevent gadget-chain execution that happens inside the provider’s ObjectInputStream; to block such attacks, also configure the JMS provider’s own deserialization filter and/or the JVM-wide -Djdk.serialFilter. When this option is not set and no JVM-wide filter is configured, a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. is applied. |  | String |
| **camel.component.jms.destination-resolver** | A pluggable org.springframework.jms.support.destination.DestinationResolver that allows you to use your own resolver (for example, to lookup the real destination in a JNDI registry). The option is a org.springframework.jms.support.destination.DestinationResolver type. |  | DestinationResolver |
| **camel.component.jms.disable-reply-to** | Specifies whether Camel ignores the JMSReplyTo header in messages. If true, Camel does not send a reply back to the destination specified in the JMSReplyTo header. You can use this option if you want Camel to consume from a route and you do not want Camel to automatically send back a reply message because another component in your code handles the reply message. You can also use this option if you want to use Camel as a proxy between different message brokers and you want to route message from one system to another. | false | Boolean |
| **camel.component.jms.disable-time-to-live** | Use this option to force disabling time to live. For example when you do request/reply over JMS, then Camel will by default use the requestTimeout value as time to live on the message being sent. The problem is that the sender and receiver systems have to have their clocks synchronized, so they are in sync. This is not always so easy to archive. So you can use disableTimeToLive=true to not set a time to live value on the sent message. Then the message will not expire on the receiver system. See below in section About time to live for more details. | false | Boolean |
| **camel.component.jms.durable-subscription-name** | The durable subscriber name for specifying durable topic subscriptions. The clientId option must be configured as well. |  | String |
| **camel.component.jms.eager-loading-of-properties** | Enables eager loading of JMS properties and payload as soon as a message is loaded which generally is inefficient as the JMS properties may not be required but sometimes can catch early any issues with the underlying JMS provider and the use of JMS properties. See also the option eagerPoisonBody. | false | Boolean |
| **camel.component.jms.eager-poison-body** | If eagerLoadingOfProperties is enabled and the JMS message payload (JMS body or JMS properties) is poison (cannot be read/mapped), then set this text as the message body instead so the message can be processed (the cause of the poison are already stored as exception on the Exchange). This can be turned off by setting eagerPoisonBody=false. See also the option eagerLoadingOfProperties. | Poison JMS message due to ${exception.message} | String |
| **camel.component.jms.enabled** | Whether to enable auto configuration of the jms component. This is enabled by default. |  | Boolean |
| **camel.component.jms.error-handler** | Specifies a org.springframework.util.ErrorHandler to be invoked in case of any uncaught exceptions thrown while processing a Message. By default these exceptions will be logged at the WARN level, if no errorHandler has been configured. You can configure logging level and whether stack traces should be logged using errorHandlerLoggingLevel and errorHandlerLogStackTrace options. This makes it much easier to configure, than having to code a custom errorHandler. The option is a org.springframework.util.ErrorHandler type. |  | ErrorHandler |
| **camel.component.jms.error-handler-log-stack-trace** | Allows to control whether stack-traces should be logged or not, by the default errorHandler. | true | Boolean |
| **camel.component.jms.error-handler-logging-level** | Allows to configure the default errorHandler logging level for logging uncaught exceptions. | warn | LoggingLevel |
| **camel.component.jms.exception-listener** | Specifies the JMS Exception Listener that is to be notified of any underlying JMS exceptions. The option is a jakarta.jms.ExceptionListener type. |  | ExceptionListener |
| **camel.component.jms.explicit-qos-enabled** | Set if the deliveryMode, priority or timeToLive qualities of service should be used when sending messages. This option is based on Spring’s JmsTemplate. The deliveryMode, priority and timeToLive options are applied to the current endpoint. This contrasts with the preserveMessageQos option, which operates at message granularity, reading QoS properties exclusively from the Camel In message headers. | false | Boolean |
| **camel.component.jms.expose-listener-session** | Specifies whether the listener session should be exposed when consuming messages. | false | Boolean |
| **camel.component.jms.force-send-original-message** | When using mapJmsMessage=false Camel will create a new JMS message to send to a new JMS destination if you touch the headers (get or set) during the route. Set this option to true to force Camel to send the original JMS message that was received. | false | Boolean |
| **camel.component.jms.format-date-headers-to-iso8601** | Sets whether JMS date properties should be formatted according to the ISO 8601 standard. | false | Boolean |
| **camel.component.jms.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.jms.idle-consumer-limit** | Specify the limit for the number of consumers that are allowed to be idle at any given time. | 1 | Integer |
| **camel.component.jms.idle-receives-per-task-limit** | Marks the consumer as idle after the specified number of idle receives have been reached. An idle receive is counted from the moment a null message is returned by the receiver after the potential setReceiveTimeout elapsed. This gives the opportunity to check if the idle task count exceeds setIdleTaskExecutionLimit and based on that decide if the task needs to be re-scheduled or not, saving resources that would otherwise be held. This setting differs from setMaxMessagesPerTask where the task is released and re-scheduled after this limit is reached, no matter if the received messages were null or non-null messages. This setting alone can be inflexible if one desires to have a large enough batch for each task but requires a quick(er) release from the moment there are no more messages to process. This setting differs from setIdleTaskExecutionLimit where this limit decides after how many iterations of being marked as idle, a task is released. For example: If setMaxMessagesPerTask is set to '500' and #setIdleReceivesPerTaskLimit is set to '60' and setReceiveTimeout is set to '1000' and setIdleTaskExecutionLimit is set to '1', then 500 messages per task would be processed unless there is a subsequent number of 60 idle messages received, the task would be marked as idle and released. This also means that after the last message was processed, the task would be released after 60 seconds as long as no new messages appear. |  | Integer |
| **camel.component.jms.idle-task-execution-limit** | Specifies the limit for idle executions of a receive task, not having received any message within its execution. If this limit is reached, the task will shut down and leave receiving to other executing tasks (in the case of dynamic scheduling; see the maxConcurrentConsumers setting). There is additional doc available from Spring. | 1 | Integer |
| **camel.component.jms.include-all-j-m-s-x-properties** | Whether to include all JMSX prefixed properties when mapping from JMS to Camel Message. Setting this to true will include properties such as JMSXAppID, and JMSXUserID etc. Note: If you are using a custom headerFilterStrategy then this option does not apply. | false | Boolean |
| **camel.component.jms.include-correlation-i-d-as-bytes** | Whether the JMS consumer should include JMSCorrelationIDAsBytes as a header on the Camel Message. | true | Boolean |
| **camel.component.jms.include-sent-j-m-s-message-i-d** | Only applicable when sending to JMS destination using InOnly (eg fire and forget). Enabling this option will enrich the Camel Exchange with the actual JMSMessageID that was used by the JMS client when the message was sent to the JMS destination. | false | Boolean |
| **camel.component.jms.jms-key-format-strategy** | Pluggable strategy for encoding and decoding JMS keys so they can be compliant with the JMS specification. Camel provides two implementations out of the box: default and passthrough. The default strategy will safely marshal dots and hyphens (. and -). The passthrough strategy leaves the key as is. Can be used for JMS brokers which do not care whether JMS header keys contain illegal characters. You can provide your own implementation of the org.apache.camel.component.jms.JmsKeyFormatStrategy and refer to it using the # notation. |  | JmsKeyFormatStrategy |
| **camel.component.jms.jms-message-type** | Allows you to force the use of a specific jakarta.jms.Message implementation for sending JMS messages from Camel to the broker (also when Camel is used for request/reply). This is not in use when Camel receives messages as the message is locked to the type from the client that sent the message to the broker. Possible values are: Bytes, Map, Object, Stream, Text. By default, Camel would determine which JMS message type to use from the message body type. This option allows you to specify it. |  | JmsMessageType |
| **camel.component.jms.lazy-create-transaction-manager** | If true, Camel will create a JmsTransactionManager, if there is no transactionManager injected when option transacted=true. | true | Boolean |
| **camel.component.jms.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.jms.map-jms-message** | Specifies whether Camel should auto map the received JMS message to a suited payload type, such as jakarta.jms.TextMessage to a String etc. | true | Boolean |
| **camel.component.jms.max-concurrent-consumers** | Specifies the maximum number of concurrent consumers when consuming from JMS (not for request/reply over JMS). See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. When doing request/reply over JMS then the option replyToMaxConcurrentConsumers is used to control number of concurrent consumers on the reply message listener. |  | Integer |
| **camel.component.jms.max-messages-per-task** | The number of messages per task. -1 is unlimited. If you use a range for concurrent consumers (eg min max), then this option can be used to set a value to eg 100 to control how fast the consumers will shrink when less work is required. | \-1 | Integer |
| **camel.component.jms.message-converter** | To use a custom Spring org.springframework.jms.support.converter.MessageConverter so you can be in control how to map to/from a jakarta.jms.Message. The option is a org.springframework.jms.support.converter.MessageConverter type. |  | MessageConverter |
| **camel.component.jms.message-created-strategy** | To use the given MessageCreatedStrategy which are invoked when Camel creates new instances of jakarta.jms.Message objects when Camel is sending a JMS message. The option is a org.apache.camel.component.jms.MessageCreatedStrategy type. |  | MessageCreatedStrategy |
| **camel.component.jms.message-id-enabled** | When sending, specifies whether message IDs should be added. This is just an hint to the JMS broker. If the JMS provider accepts this hint, these messages must have the message ID set to null; if the provider ignores the hint, the message ID must be set to its normal unique value. | true | Boolean |
| **camel.component.jms.message-listener-container-factory** | Registry ID of the MessageListenerContainerFactory used to determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use to consume messages. Setting this will automatically set consumerType to Custom. The option is a org.apache.camel.component.jms.MessageListenerContainerFactory type. |  | MessageListenerContainerFactory |
| **camel.component.jms.message-timestamp-enabled** | Specifies whether timestamps should be enabled by default on sending messages. This is just an hint to the JMS broker. If the JMS provider accepts this hint, these messages must have the timestamp set to zero; if the provider ignores the hint the timestamp must be set to its normal value. | true | Boolean |
| **camel.component.jms.object-message-enabled** | Whether to enable sending and receiving JMS ObjectMessage. By default this is disabled because Java object serialization is a known source of security vulnerabilities. Enable this option only if you trust the source of the messages and need to send or receive Java serialized objects via JMS. When disabled, Camel will refuse to create or read JMS ObjectMessage instances. Options that rely on ObjectMessage internally (such as transferExchange and transferException) require this option to be enabled. | false | Boolean |
| **camel.component.jms.password** | Password to use with the ConnectionFactory. You can also configure username/password directly on the ConnectionFactory. |  | String |
| **camel.component.jms.preserve-message-qos** | Set to true, if you want to send message using the QoS settings specified on the message, instead of the QoS settings on the JMS endpoint. The following three headers are considered JMSPriority, JMSDeliveryMode, and JMSExpiration. You can provide all or only some of them. If not provided, Camel will fall back to use the values from the endpoint instead. So, when using this option, the headers override the values from the endpoint. The explicitQosEnabled option, by contrast, will only use options set on the endpoint, and not values from the message header. | false | Boolean |
| **camel.component.jms.priority** | Values greater than 1 specify the message priority when sending (where 1 is the lowest priority and 9 is the highest). The explicitQosEnabled option must also be enabled in order for this option to have any effect. | 4 | Integer |
| **camel.component.jms.pub-sub-no-local** | Specifies whether to inhibit the delivery of messages published by its own connection. | false | Boolean |
| **camel.component.jms.queue-browse-strategy** | To use a custom QueueBrowseStrategy when browsing queues. The option is a org.apache.camel.component.jms.QueueBrowseStrategy type. |  | QueueBrowseStrategy |
| **camel.component.jms.receive-timeout** | The timeout for receiving messages (in milliseconds). The option is a long type. | 1000 | Long |
| **camel.component.jms.recovery-interval** | Specifies the interval between recovery attempts, i.e. when a connection is being refreshed, in milliseconds. The default is 5000 ms, that is, 5 seconds. The option is a long type. | 5000 | Long |
| **camel.component.jms.reply-correlation-property** | When using InOut exchange pattern use this JMS property instead of JMSCorrelationID JMS property to correlate reply message. Difference between this and 'correlationProperty' is that 'correlationProperty' tells which request property holds the correlation id value and it does not affect the selector for the reply (JMSCorrelationID=<correlation id>), while 'replyCorrelationProperty' tells which reply property will hold the correlation id value and it does affect the selector for the reply (<replyCorrelationProperty>=<correlation id>). |  | String |
| **camel.component.jms.reply-to** | Provides an explicit ReplyTo destination (overrides any incoming value of Message.getJMSReplyTo() in consumer). |  | String |
| **camel.component.jms.reply-to-cache-level-name** | Sets the cache level by name for the reply consumer when doing request/reply over JMS. This option only applies when using fixed reply queues (not temporary). Camel will by default use: CACHE\_CONSUMER for exclusive or shared w/ replyToSelectorName. And CACHE\_SESSION for shared without replyToSelectorName. Some JMS brokers such as IBM WebSphere may require to set the replyToCacheLevelName=CACHE\_NONE to work. Note: If using temporary queues then CACHE\_NONE is not allowed, and you must use a higher value such as CACHE\_CONSUMER or CACHE\_SESSION. |  | String |
| **camel.component.jms.reply-to-concurrent-consumers** | Specifies the default number of concurrent consumers when doing request/reply over JMS. See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. | 1 | Integer |
| **camel.component.jms.reply-to-consumer-type** | The consumer type of the reply consumer (when doing request/reply), which can be one of: Simple, Default, or Custom. The consumer type determines which Spring JMS listener to use. Default will use org.springframework.jms.listener.DefaultMessageListenerContainer, Simple will use org.springframework.jms.listener.SimpleMessageListenerContainer. When Custom is specified, the MessageListenerContainerFactory defined by the messageListenerContainerFactory option will determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use. | default | ConsumerType |
| **camel.component.jms.reply-to-delivery-persistent** | Specifies whether to use persistent delivery by default for replies. | true | Boolean |
| **camel.component.jms.reply-to-destination-selector-name** | Sets the JMS Selector using the fixed name to be used so you can filter out your own replies from the others when using a shared queue (that is, if you are not using a temporary reply queue). |  | String |
| **camel.component.jms.reply-to-max-concurrent-consumers** | Specifies the maximum number of concurrent consumers when using request/reply over JMS. See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. |  | Integer |
| **camel.component.jms.reply-to-on-timeout-max-concurrent-consumers** | Specifies the maximum number of concurrent consumers for continue routing when timeout occurred when using request/reply over JMS. | 1 | Integer |
| **camel.component.jms.reply-to-override** | Provides an explicit ReplyTo destination in the JMS message, which overrides the setting of replyTo. It is useful if you want to forward the message to a remote Queue and receive the reply message from the ReplyTo destination. |  | String |
| **camel.component.jms.reply-to-same-destination-allowed** | Whether a JMS consumer is allowed to send a reply message to the same destination that the consumer is using to consume from. This prevents an endless loop by consuming and sending back the same message to itself. | false | Boolean |
| **camel.component.jms.reply-to-type** | Allows for explicitly specifying which kind of strategy to use for replyTo queues when doing request/reply over JMS. Possible values are: Temporary, Shared, or Exclusive. By default Camel will use temporary queues. However if replyTo has been configured, then Shared is used by default. This option allows you to use exclusive queues instead of shared ones. See Camel JMS documentation for more details, and especially the notes about the implications if running in a clustered environment, and the fact that Shared reply queues has lower performance than its alternatives Temporary and Exclusive. |  | ReplyToType |
| **camel.component.jms.request-timeout** | The timeout for waiting for a reply when using the InOut Exchange Pattern (in milliseconds). The default is 20 seconds. You can include the header CamelJmsRequestTimeout to override this endpoint configured timeout value, and thus have per message individual timeout values. See also the requestTimeoutCheckerInterval option. The option is a long type. | 20000 | Long |
| **camel.component.jms.request-timeout-checker-interval** | Configures how often Camel should check for timed out Exchanges when doing request/reply over JMS. By default Camel checks once per second. But if you must react faster when a timeout occurs, then you can lower this interval, to check more frequently. The timeout is determined by the option requestTimeout. The option is a long type. | 1000 | Long |
| **camel.component.jms.selector** | Sets the JMS selector to use. |  | String |
| **camel.component.jms.service-location-enabled** | Whether to detect the network address location of the JMS broker on startup. This information is gathered via reflection on the ConnectionFactory, and is vendor specific. This option can be used to turn this off. | true | Boolean |
| **camel.component.jms.stream-message-type-enabled** | Sets whether StreamMessage type is enabled or not. Message payloads of streaming kind such as files, InputStream, etc will either by sent as BytesMessage or StreamMessage. This option controls which kind will be used. By default BytesMessage is used which enforces the entire message payload to be read into memory. By enabling this option the message payload is read into memory in chunks and each chunk is then written to the StreamMessage until no more data. | false | Boolean |
| **camel.component.jms.subscription-durable** | Set whether to make the subscription durable. The durable subscription name to be used can be specified through the subscriptionName property. Default is false. Set this to true to register a durable subscription, typically in combination with a subscriptionName value (unless your message listener class name is good enough as subscription name). Only makes sense when listening to a topic (pub-sub domain), therefore this method switches the pubSubDomain flag as well. | false | Boolean |
| **camel.component.jms.subscription-name** | Set the name of a subscription to create. To be applied in case of a topic (pub-sub domain) with a shared or durable subscription. The subscription name needs to be unique within this client’s JMS client id. Default is the class name of the specified message listener. Note: Only 1 concurrent consumer (which is the default of this message listener container) is allowed for each subscription, except for a shared subscription (which requires JMS 2.0). |  | String |
| **camel.component.jms.subscription-shared** | Set whether to make the subscription shared. The shared subscription name to be used can be specified through the subscriptionName property. Default is false. Set this to true to register a shared subscription, typically in combination with a subscriptionName value (unless your message listener class name is good enough as subscription name). Note that shared subscriptions may also be durable, so this flag can (and often will) be combined with subscriptionDurable as well. Only makes sense when listening to a topic (pub-sub domain), therefore this method switches the pubSubDomain flag as well. Requires a JMS 2.0 compatible message broker. | false | Boolean |
| **camel.component.jms.synchronous** | Sets whether synchronous processing should be strictly used. | false | Boolean |
| **camel.component.jms.task-executor** | Allows you to specify a custom task executor for consuming messages. The option is a org.springframework.core.task.TaskExecutor type. |  | TaskExecutor |
| **camel.component.jms.temporary-queue-resolver** | A pluggable TemporaryQueueResolver that allows you to use your own resolver for creating temporary queues (some messaging systems has special requirements for creating temporary queues). The option is a org.apache.camel.component.jms.TemporaryQueueResolver type. |  | TemporaryQueueResolver |
| **camel.component.jms.test-connection-on-startup** | Specifies whether to test the connection on startup. This ensures that when Camel starts that all the JMS consumers have a valid connection to the JMS broker. If a connection cannot be granted then Camel throws an exception on startup. This ensures that Camel is not started with failed connections. The JMS producers is tested as well. | false | Boolean |
| **camel.component.jms.time-to-live** | When sending messages, specifies the time-to-live of the message (in milliseconds). | \-1 | Long |
| **camel.component.jms.transacted** | Specifies whether to use transacted mode. | false | Boolean |
| **camel.component.jms.transacted-in-out** | Specifies whether InOut operations (request reply) default to using transacted mode If this flag is set to true, then Spring JmsTemplate will have sessionTransacted set to true, and the acknowledgeMode as transacted on the JmsTemplate used for InOut operations. Note from Spring JMS: that within a JTA transaction, the parameters passed to createQueue, createTopic methods are not taken into account. Depending on the Java EE transaction context, the container makes its own decisions on these values. Analogously, these parameters are not taken into account within a locally managed transaction either, since Spring JMS operates on an existing JMS Session in this case. Setting this flag to true will use a short local JMS transaction when running outside of a managed transaction, and a synchronized local JMS transaction in case of a managed transaction (other than an XA transaction) being present. This has the effect of a local JMS transaction being managed alongside the main transaction (which might be a native JDBC transaction), with the JMS transaction committing right after the main transaction. | false | Boolean |
| **camel.component.jms.transaction-manager** | The Spring transaction manager to use. The option is a org.springframework.transaction.PlatformTransactionManager type. |  | PlatformTransactionManager |
| **camel.component.jms.transaction-name** | The name of the transaction to use. |  | String |
| **camel.component.jms.transaction-timeout** | The timeout value of the transaction (in seconds), if using transacted mode. | \-1 | Integer |
| **camel.component.jms.transfer-exception** | If enabled and you are using Request Reply messaging (InOut) and an Exchange failed on the consumer side, then the caused Exception will be send back in response as a jakarta.jms.ObjectMessage. If the client is Camel, the returned Exception is rethrown. This allows you to use Camel JMS as a bridge in your routing - for example, using persistent queues to enable robust routing. Notice that if you also have transferExchange enabled, this option takes precedence. The caught exception is required to be serializable. The original Exception on the consumer side can be wrapped in an outer exception such as org.apache.camel.RuntimeCamelException when returned to the producer. Use this with caution as the data is using Java Object serialization and requires the received to be able to deserialize the data at Class level, which forces a strong coupling between the producers and consumer!. | false | Boolean |
| **camel.component.jms.transfer-exchange** | You can transfer the exchange over the wire instead of just the body and headers. The following fields are transferred: In body, Out body, Fault body, In headers, Out headers, Fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. You must enable this option on both the producer and consumer side, so Camel knows the payloads is an Exchange and not a regular payload. Use this with caution as the data is using Java Object serialization and requires the receiver to be able to deserialize the data at Class level, which forces a strong coupling between the producers and consumers having to use compatible Camel versions!. | false | Boolean |
| **camel.component.jms.use-message-i-d-as-correlation-i-d** | Specifies whether JMSMessageID should always be used as JMSCorrelationID for InOut messages. | false | Boolean |
| **camel.component.jms.username** | Username to use with the ConnectionFactory. You can also configure username/password directly on the ConnectionFactory. |  | String |
| **camel.component.jms.wait-for-provision-correlation-to-be-updated-counter** | Number of times to wait for provisional correlation id to be updated to the actual correlation id when doing request/reply over JMS and when the option useMessageIDAsCorrelationID is enabled. | 50 | Integer |
| **camel.component.jms.wait-for-provision-correlation-to-be-updated-thread-sleeping-time** | Interval in millis to sleep each time while waiting for provisional correlation id to be updated. The option is a long type. | 100 | Long |
| **camel.component.jms.wait-for-temporary-reply-to-to-be-updated-counter** | Number of times to wait for temporary replyTo queue to be created and ready when doing request/reply over JMS. | 200 | Integer |
| **camel.component.jms.wait-for-temporary-reply-to-to-be-updated-thread-sleeping-time** | Interval in millis to sleep each time while waiting for temporary replyTo queue to be ready. The option is a long type. | 100 | Long |