# ActiveMQ 6.x

**Since Camel 4.7**

**Both producer and consumer are supported**

The ActiveMQ component is an extension to the JMS component and has been pre-configured for using Apache ActiveMQ 6.x (not Artemis). Users of Apache ActiveMQ Artemis should use the JMS component.

> **Important**
> The camel-activemq6 component is best intended for ActiveMQ 6.x brokers. If you use ActiveMQ 5.x brokers, then use the camel-activemq 5.x component instead.

> **Tip**
> **More documentation**
>
> See the JMS component for more documentation and examples

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-activemq6</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

activemq:\[queue:|topic:\]destinationName\[?options\]

Where `destinationName` is a JMS queue or topic name. By default, the `destinationName` is interpreted as a queue name. For example, to connect to the queue, `foo` use:

activemq:foo

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

The ActiveMQ 6.x component supports 112 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **brokerURL** (common) | Sets the broker URL to use to connect to ActiveMQ. If none configured then localhost:61616 is used by default (however can be overridden by configuration from environment variables). |  | String |
| **clientId** (common) | Sets the JMS client ID to use. Note that this value, if specified, must be unique and can only be used by a single JMS connection instance. It is typically only required for durable topic subscriptions with JMS 1.1. |  | String |
| **connectionFactory** (common) | The connection factory to be use. A connection factory must be configured either on the component or endpoint. |  | ConnectionFactory |
| **disableReplyTo** (common) | Specifies whether Camel ignores the JMSReplyTo header in messages. If true, Camel does not send a reply back to the destination specified in the JMSReplyTo header. You can use this option if you want Camel to consume from a route and you do not want Camel to automatically send back a reply message because another component in your code handles the reply message. You can also use this option if you want to use Camel as a proxy between different message brokers and you want to route message from one system to another. | false | boolean |
| **durableSubscriptionName** (common) | The durable subscriber name for specifying durable topic subscriptions. The clientId option must be configured as well. |  | String |
| **embedded** (common) | Use an embedded in-memory (non-persistent) ActiveMQ broker for development and testing purposes. You must have activemq-broker JAR on the classpath. | false | boolean |
| **jmsMessageType** (common) | 
Allows you to force the use of a specific jakarta.jms.Message implementation for sending JMS messages. Possible values are: Bytes, Map, Object, Stream, Text. By default, Camel would determine which JMS message type to use from the In body type. This option allows you to specify it.

Enum values:

-   Bytes
    
-   Map
    
-   Object
    
-   Stream
    
-   Text
    





 |  | JmsMessageType |
| **replyTo** (common) | Provides an explicit ReplyTo destination (overrides any incoming value of Message.getJMSReplyTo() in consumer). |  | String |
| **testConnectionOnStartup** (common) | Specifies whether to test the connection on startup. This ensures that when Camel starts that all the JMS consumers have a valid connection to the JMS broker. If a connection cannot be granted then Camel throws an exception on startup. This ensures that Camel is not started with failed connections. The JMS producers is tested as well. | false | boolean |
| **usePooledConnection** (common) | Enables or disables whether a PooledConnectionFactory will be used so that when messages are sent to ActiveMQ from outside a message consuming thread, pooling will be used rather than the default with the Spring JmsTemplate which will create a new connection, session, producer for each message then close them all down again. The default value is true. | true | boolean |
| **useSingleConnection** (common) | Enables or disables whether a Spring SingleConnectionFactory will be used so that when messages are sent to ActiveMQ from outside a message consuming thread, pooling will be used rather than the default with the Spring JmsTemplate which will create a new connection, session, producer for each message then close them all down again. The default value is false and a pooled connection is used by default. | false | boolean |
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
| **trustAllPackages** (advanced) | Define if all Java packages are trusted or not (for Java object JMS message types). Notice its not recommended practice to send Java serialized objects over network. Setting this to true can expose security risks, so use this with care. | false | boolean |
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

The ActiveMQ 6.x endpoint is configured using URI syntax:

activemq6:destinationType:destinationName

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

### Query Parameters (103 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | Sets the JMS client ID to use. Note that this value, if specified, must be unique and can only be used by a single JMS connection instance. It is typically only required for durable topic subscriptions with JMS 1.1. |  | String |
| **connectionFactory** (common) | The connection factory to be use. A connection factory must be configured either on the component or endpoint. |  | ConnectionFactory |
| **disableReplyTo** (common) | Specifies whether Camel ignores the JMSReplyTo header in messages. If true, Camel does not send a reply back to the destination specified in the JMSReplyTo header. You can use this option if you want Camel to consume from a route and you do not want Camel to automatically send back a reply message because another component in your code handles the reply message. You can also use this option if you want to use Camel as a proxy between different message brokers and you want to route message from one system to another. | false | boolean |
| **durableSubscriptionName** (common) | The durable subscriber name for specifying durable topic subscriptions. The clientId option must be configured as well. |  | String |
| **jmsMessageType** (common) | 
Allows you to force the use of a specific jakarta.jms.Message implementation for sending JMS messages. Possible values are: Bytes, Map, Object, Stream, Text. By default, Camel would determine which JMS message type to use from the In body type. This option allows you to specify it.

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
| **destinationOptions** (consumer (advanced)) | Destination Options are a way to provide extended configuration options to a JMS consumer without having to extend the JMS API. The options are encoded using URL query syntax in the destination name that the consumer is created on. See more details at [https://activemq.apache.org/destination-options](https://activemq.apache.org/destination-options). This is a multi-value option with prefix: destination. |  | Map |
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

## Examples

You’ll need to provide a connectionFactory to the ActiveMQ Component, to have the following examples working.

### Producer Example

```java
from("timer:mytimer?period=5000")
        .setBody(constant("HELLO from Camel!"))
        .to("activemq:queue:HELLO.WORLD");
```

### Consumer Example

```java
from("activemq:queue:HELLO.WORLD")
        .log("Received a message - ${body}");
```

## Spring Boot Auto-Configuration

When using activemq6 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-activemq6-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 113 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.activemq6.accept-messages-while-stopping** | Specifies whether the consumer accept messages while it is stopping. You may consider enabling this option, if you start and stop JMS routes at runtime, while there are still messages enqueued on the queue. If this option is false, and you stop the JMS route, then messages may be rejected, and the JMS broker would have to attempt redeliveries, which yet again may be rejected, and eventually the message may be moved at a dead letter queue on the JMS broker. To avoid this its recommended to enable this option. | false | Boolean |
| **camel.component.activemq6.acknowledgement-mode-name** | The JMS acknowledgement name, which is one of: SESSION\_TRANSACTED, CLIENT\_ACKNOWLEDGE, AUTO\_ACKNOWLEDGE, DUPS\_OK\_ACKNOWLEDGE. | AUTO\_ACKNOWLEDGE | String |
| **camel.component.activemq6.allow-additional-headers** | This option is used to allow additional headers which may have values that are invalid according to JMS specification. For example, some message systems, such as WMQ, do this with header names using prefix JMS\_IBM\_MQMD\_ containing values with byte array or other invalid types. You can specify multiple header names separated by comma, and use as suffix for wildcard matching. |  | String |
| **camel.component.activemq6.allow-auto-wired-connection-factory** | Whether to auto-discover ConnectionFactory from the registry, if no connection factory has been configured. If only one instance of ConnectionFactory is found then it will be used. This is enabled by default. | true | Boolean |
| **camel.component.activemq6.allow-auto-wired-destination-resolver** | Whether to auto-discover DestinationResolver from the registry, if no destination resolver has been configured. If only one instance of DestinationResolver is found then it will be used. This is enabled by default. | true | Boolean |
| **camel.component.activemq6.allow-null-body** | Whether to allow sending messages with no body. If this option is false and the message body is null, then an JMSException is thrown. | true | Boolean |
| **camel.component.activemq6.allow-reply-manager-quick-stop** | Whether the DefaultMessageListenerContainer used in the reply managers for request-reply messaging allow the DefaultMessageListenerContainer.runningAllowed flag to quick stop in case JmsConfiguration#isAcceptMessagesWhileStopping is enabled, and org.apache.camel.CamelContext is currently being stopped. This quick stop ability is enabled by default in the regular JMS consumers but to enable for reply managers you must enable this flag. | false | Boolean |
| **camel.component.activemq6.allow-serialized-headers** | Controls whether or not to include serialized headers. Applies only when transferExchange is true. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. | false | Boolean |
| **camel.component.activemq6.always-copy-message** | If true, Camel will always make a JMS message copy of the message when it is passed to the producer for sending. Copying the message is needed in some situations, such as when a replyToDestinationSelectorName is set (incidentally, Camel will set the alwaysCopyMessage option to true, if a replyToDestinationSelectorName is set). | false | Boolean |
| **camel.component.activemq6.artemis-consumer-priority** | Consumer priorities allow you to ensure that high priority consumers receive messages while they are active. Normally, active consumers connected to a queue receive messages from it in a round-robin fashion. When consumer priorities are in use, messages are delivered round-robin if multiple active consumers exist with the same high priority. Messages will only going to lower priority consumers when the high priority consumers do not have credit available to consume the message, or those high priority consumers have declined to accept the message (for instance because it does not meet the criteria of any selectors associated with the consumer). |  | Integer |
| **camel.component.activemq6.artemis-streaming-enabled** | Whether optimizing for Apache Artemis streaming mode. This can reduce memory overhead when using Artemis with JMS StreamMessage types. This option must only be enabled if Apache Artemis is being used. | false | Boolean |
| **camel.component.activemq6.async-consumer** | Whether the JmsConsumer processes the Exchange asynchronously. If enabled then the JmsConsumer may pickup the next message from the JMS queue, while the previous message is being processed asynchronously (by the Asynchronous Routing Engine). This means that messages may be processed not 100% strictly in order. If disabled (as default) then the Exchange is fully processed before the JmsConsumer will pickup the next message from the JMS queue. Note if transacted has been enabled, then asyncConsumer=true does not run asynchronously, as transaction must be executed synchronously. | false | Boolean |
| **camel.component.activemq6.async-start-listener** | Whether to startup the JmsConsumer message listener asynchronously, when starting a route. For example if a JmsConsumer cannot get a connection to a remote JMS broker, then it may block while retrying and/or fail-over. This will cause Camel to block while starting routes. By setting this option to true, you will let routes startup, while the JmsConsumer connects to the JMS broker using a dedicated thread in asynchronous mode. If this option is used, then beware that if the connection could not be established, then an exception is logged at WARN level, and the consumer will not be able to receive messages; You can then restart the route to retry. | false | Boolean |
| **camel.component.activemq6.async-stop-listener** | Whether to stop the JmsConsumer message listener asynchronously, when stopping a route. | false | Boolean |
| **camel.component.activemq6.auto-startup** | Specifies whether the consumer container should auto-startup. | true | Boolean |
| **camel.component.activemq6.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.activemq6.broker-u-r-l** | Sets the broker URL to use to connect to ActiveMQ. If none configured then localhost:61616 is used by default (however can be overridden by configuration from environment variables). |  | String |
| **camel.component.activemq6.browse-limit** | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | Integer |
| **camel.component.activemq6.cache-level** | Sets the cache level by ID for the underlying JMS resources. See cacheLevelName option for more details. |  | Integer |
| **camel.component.activemq6.cache-level-name** | Sets the cache level by name for the underlying JMS resources. Possible values are: CACHE\_AUTO, CACHE\_CONNECTION, CACHE\_CONSUMER, CACHE\_NONE, and CACHE\_SESSION. The default setting is CACHE\_AUTO. See the Spring documentation and Transactions Cache Levels for more information. | CACHE\_AUTO | String |
| **camel.component.activemq6.client-id** | Sets the JMS client ID to use. Note that this value, if specified, must be unique and can only be used by a single JMS connection instance. It is typically only required for durable topic subscriptions with JMS 1.1. |  | String |
| **camel.component.activemq6.concurrent-consumers** | Specifies the default number of concurrent consumers when consuming from JMS (not for request/reply over JMS). See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. When doing request/reply over JMS then the option replyToConcurrentConsumers is used to control number of concurrent consumers on the reply message listener. | 1 | Integer |
| **camel.component.activemq6.configuration** | To use a shared JMS configuration. The option is a org.apache.camel.component.jms.JmsConfiguration type. |  | JmsConfiguration |
| **camel.component.activemq6.connection-factory** | The connection factory to be use. A connection factory must be configured either on the component or endpoint. The option is a jakarta.jms.ConnectionFactory type. |  | ConnectionFactory |
| **camel.component.activemq6.consumer-type** | The consumer type to use, which can be one of: Simple, Default, or Custom. The consumer type determines which Spring JMS listener to use. Default will use org.springframework.jms.listener.DefaultMessageListenerContainer, Simple will use org.springframework.jms.listener.SimpleMessageListenerContainer. When Custom is specified, the MessageListenerContainerFactory defined by the messageListenerContainerFactory option will determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use. | default | ConsumerType |
| **camel.component.activemq6.correlation-property** | When using InOut exchange pattern use this JMS property instead of JMSCorrelationID JMS property to correlate messages. If set messages will be correlated solely on the value of this property JMSCorrelationID property will be ignored and not set by Camel. |  | String |
| **camel.component.activemq6.default-task-executor-type** | Specifies what default TaskExecutor type to use in the DefaultMessageListenerContainer, for both consumer endpoints and the ReplyTo consumer of producer endpoints. Possible values: SimpleAsync (uses Spring’s SimpleAsyncTaskExecutor) or ThreadPool (uses Spring’s ThreadPoolTaskExecutor with optimal values - cached thread-pool-like). If not set, it defaults to the previous behaviour, which uses a cached thread pool for consumer endpoints and SimpleAsync for reply consumers. The use of ThreadPool is recommended to reduce thread trash in elastic configurations with dynamically increasing and decreasing concurrent consumers. |  | DefaultTaskExecutorType |
| **camel.component.activemq6.delivery-delay** | Sets delivery delay to use for send calls for JMS. This option requires JMS 2.0 compliant broker. | \-1 | Long |
| **camel.component.activemq6.delivery-mode** | Specifies the delivery mode to be used. Possible values are those defined by jakarta.jms.DeliveryMode. NON\_PERSISTENT = 1 and PERSISTENT = 2. |  | Integer |
| **camel.component.activemq6.delivery-persistent** | Specifies whether persistent delivery is used by default. | true | Boolean |
| **camel.component.activemq6.deserialization-filter** | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied as a defense-in-depth check on the class of the body returned by jakarta.jms.ObjectMessage.getObject(). The pattern is evaluated after the JMS provider has deserialized the payload, so this option alone does not prevent gadget-chain execution that happens inside the provider’s ObjectInputStream; to block such attacks, also configure the JMS provider’s own deserialization filter and/or the JVM-wide -Djdk.serialFilter. When this option is not set and no JVM-wide filter is configured, a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. is applied. |  | String |
| **camel.component.activemq6.destination-resolver** | A pluggable org.springframework.jms.support.destination.DestinationResolver that allows you to use your own resolver (for example, to lookup the real destination in a JNDI registry). The option is a org.springframework.jms.support.destination.DestinationResolver type. |  | DestinationResolver |
| **camel.component.activemq6.disable-reply-to** | Specifies whether Camel ignores the JMSReplyTo header in messages. If true, Camel does not send a reply back to the destination specified in the JMSReplyTo header. You can use this option if you want Camel to consume from a route and you do not want Camel to automatically send back a reply message because another component in your code handles the reply message. You can also use this option if you want to use Camel as a proxy between different message brokers and you want to route message from one system to another. | false | Boolean |
| **camel.component.activemq6.disable-time-to-live** | Use this option to force disabling time to live. For example when you do request/reply over JMS, then Camel will by default use the requestTimeout value as time to live on the message being sent. The problem is that the sender and receiver systems have to have their clocks synchronized, so they are in sync. This is not always so easy to archive. So you can use disableTimeToLive=true to not set a time to live value on the sent message. Then the message will not expire on the receiver system. See below in section About time to live for more details. | false | Boolean |
| **camel.component.activemq6.durable-subscription-name** | The durable subscriber name for specifying durable topic subscriptions. The clientId option must be configured as well. |  | String |
| **camel.component.activemq6.eager-loading-of-properties** | Enables eager loading of JMS properties and payload as soon as a message is loaded which generally is inefficient as the JMS properties may not be required but sometimes can catch early any issues with the underlying JMS provider and the use of JMS properties. See also the option eagerPoisonBody. | false | Boolean |
| **camel.component.activemq6.eager-poison-body** | If eagerLoadingOfProperties is enabled and the JMS message payload (JMS body or JMS properties) is poison (cannot be read/mapped), then set this text as the message body instead so the message can be processed (the cause of the poison are already stored as exception on the Exchange). This can be turned off by setting eagerPoisonBody=false. See also the option eagerLoadingOfProperties. | Poison JMS message due to ${exception.message} | String |
| **camel.component.activemq6.embedded** | Use an embedded in-memory (non-persistent) ActiveMQ broker for development and testing purposes. You must have activemq-broker JAR on the classpath. | false | Boolean |
| **camel.component.activemq6.enabled** | Whether to enable auto configuration of the activemq6 component. This is enabled by default. |  | Boolean |
| **camel.component.activemq6.error-handler** | Specifies a org.springframework.util.ErrorHandler to be invoked in case of any uncaught exceptions thrown while processing a Message. By default these exceptions will be logged at the WARN level, if no errorHandler has been configured. You can configure logging level and whether stack traces should be logged using errorHandlerLoggingLevel and errorHandlerLogStackTrace options. This makes it much easier to configure, than having to code a custom errorHandler. The option is a org.springframework.util.ErrorHandler type. |  | ErrorHandler |
| **camel.component.activemq6.error-handler-log-stack-trace** | Allows to control whether stack-traces should be logged or not, by the default errorHandler. | true | Boolean |
| **camel.component.activemq6.error-handler-logging-level** | Allows to configure the default errorHandler logging level for logging uncaught exceptions. | warn | LoggingLevel |
| **camel.component.activemq6.exception-listener** | Specifies the JMS Exception Listener that is to be notified of any underlying JMS exceptions. The option is a jakarta.jms.ExceptionListener type. |  | ExceptionListener |
| **camel.component.activemq6.explicit-qos-enabled** | Set if the deliveryMode, priority or timeToLive qualities of service should be used when sending messages. This option is based on Spring’s JmsTemplate. The deliveryMode, priority and timeToLive options are applied to the current endpoint. This contrasts with the preserveMessageQos option, which operates at message granularity, reading QoS properties exclusively from the Camel In message headers. | false | Boolean |
| **camel.component.activemq6.expose-listener-session** | Specifies whether the listener session should be exposed when consuming messages. | false | Boolean |
| **camel.component.activemq6.force-send-original-message** | When using mapJmsMessage=false Camel will create a new JMS message to send to a new JMS destination if you touch the headers (get or set) during the route. Set this option to true to force Camel to send the original JMS message that was received. | false | Boolean |
| **camel.component.activemq6.format-date-headers-to-iso8601** | Sets whether JMS date properties should be formatted according to the ISO 8601 standard. | false | Boolean |
| **camel.component.activemq6.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.activemq6.idle-consumer-limit** | Specify the limit for the number of consumers that are allowed to be idle at any given time. | 1 | Integer |
| **camel.component.activemq6.idle-receives-per-task-limit** | Marks the consumer as idle after the specified number of idle receives have been reached. An idle receive is counted from the moment a null message is returned by the receiver after the potential setReceiveTimeout elapsed. This gives the opportunity to check if the idle task count exceeds setIdleTaskExecutionLimit and based on that decide if the task needs to be re-scheduled or not, saving resources that would otherwise be held. This setting differs from setMaxMessagesPerTask where the task is released and re-scheduled after this limit is reached, no matter if the received messages were null or non-null messages. This setting alone can be inflexible if one desires to have a large enough batch for each task but requires a quick(er) release from the moment there are no more messages to process. This setting differs from setIdleTaskExecutionLimit where this limit decides after how many iterations of being marked as idle, a task is released. For example: If setMaxMessagesPerTask is set to '500' and #setIdleReceivesPerTaskLimit is set to '60' and setReceiveTimeout is set to '1000' and setIdleTaskExecutionLimit is set to '1', then 500 messages per task would be processed unless there is a subsequent number of 60 idle messages received, the task would be marked as idle and released. This also means that after the last message was processed, the task would be released after 60 seconds as long as no new messages appear. |  | Integer |
| **camel.component.activemq6.idle-task-execution-limit** | Specifies the limit for idle executions of a receive task, not having received any message within its execution. If this limit is reached, the task will shut down and leave receiving to other executing tasks (in the case of dynamic scheduling; see the maxConcurrentConsumers setting). There is additional doc available from Spring. | 1 | Integer |
| **camel.component.activemq6.include-all-j-m-s-x-properties** | Whether to include all JMSX prefixed properties when mapping from JMS to Camel Message. Setting this to true will include properties such as JMSXAppID, and JMSXUserID etc. Note: If you are using a custom headerFilterStrategy then this option does not apply. | false | Boolean |
| **camel.component.activemq6.include-correlation-i-d-as-bytes** | Whether the JMS consumer should include JMSCorrelationIDAsBytes as a header on the Camel Message. | true | Boolean |
| **camel.component.activemq6.include-sent-j-m-s-message-i-d** | Only applicable when sending to JMS destination using InOnly (eg fire and forget). Enabling this option will enrich the Camel Exchange with the actual JMSMessageID that was used by the JMS client when the message was sent to the JMS destination. | false | Boolean |
| **camel.component.activemq6.jms-key-format-strategy** | Pluggable strategy for encoding and decoding JMS keys so they can be compliant with the JMS specification. Camel provides two implementations out of the box: default and passthrough. The default strategy will safely marshal dots and hyphens (. and -). The passthrough strategy leaves the key as is. Can be used for JMS brokers which do not care whether JMS header keys contain illegal characters. You can provide your own implementation of the org.apache.camel.component.jms.JmsKeyFormatStrategy and refer to it using the # notation. |  | JmsKeyFormatStrategy |
| **camel.component.activemq6.jms-message-type** | Allows you to force the use of a specific jakarta.jms.Message implementation for sending JMS messages. Possible values are: Bytes, Map, Object, Stream, Text. By default, Camel would determine which JMS message type to use from the In body type. This option allows you to specify it. |  | JmsMessageType |
| **camel.component.activemq6.lazy-create-transaction-manager** | If true, Camel will create a JmsTransactionManager, if there is no transactionManager injected when option transacted=true. | true | Boolean |
| **camel.component.activemq6.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.activemq6.map-jms-message** | Specifies whether Camel should auto map the received JMS message to a suited payload type, such as jakarta.jms.TextMessage to a String etc. | true | Boolean |
| **camel.component.activemq6.max-concurrent-consumers** | Specifies the maximum number of concurrent consumers when consuming from JMS (not for request/reply over JMS). See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. When doing request/reply over JMS then the option replyToMaxConcurrentConsumers is used to control number of concurrent consumers on the reply message listener. |  | Integer |
| **camel.component.activemq6.max-messages-per-task** | The number of messages per task. -1 is unlimited. If you use a range for concurrent consumers (eg min max), then this option can be used to set a value to eg 100 to control how fast the consumers will shrink when less work is required. | \-1 | Integer |
| **camel.component.activemq6.message-converter** | To use a custom Spring org.springframework.jms.support.converter.MessageConverter so you can be in control how to map to/from a jakarta.jms.Message. The option is a org.springframework.jms.support.converter.MessageConverter type. |  | MessageConverter |
| **camel.component.activemq6.message-created-strategy** | To use the given MessageCreatedStrategy which are invoked when Camel creates new instances of jakarta.jms.Message objects when Camel is sending a JMS message. The option is a org.apache.camel.component.jms.MessageCreatedStrategy type. |  | MessageCreatedStrategy |
| **camel.component.activemq6.message-id-enabled** | When sending, specifies whether message IDs should be added. This is just an hint to the JMS broker. If the JMS provider accepts this hint, these messages must have the message ID set to null; if the provider ignores the hint, the message ID must be set to its normal unique value. | true | Boolean |
| **camel.component.activemq6.message-listener-container-factory** | Registry ID of the MessageListenerContainerFactory used to determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use to consume messages. Setting this will automatically set consumerType to Custom. The option is a org.apache.camel.component.jms.MessageListenerContainerFactory type. |  | MessageListenerContainerFactory |
| **camel.component.activemq6.message-timestamp-enabled** | Specifies whether timestamps should be enabled by default on sending messages. This is just an hint to the JMS broker. If the JMS provider accepts this hint, these messages must have the timestamp set to zero; if the provider ignores the hint the timestamp must be set to its normal value. | true | Boolean |
| **camel.component.activemq6.password** | Password to use with the ConnectionFactory. You can also configure username/password directly on the ConnectionFactory. |  | String |
| **camel.component.activemq6.preserve-message-qos** | Set to true, if you want to send message using the QoS settings specified on the message, instead of the QoS settings on the JMS endpoint. The following three headers are considered JMSPriority, JMSDeliveryMode, and JMSExpiration. You can provide all or only some of them. If not provided, Camel will fall back to use the values from the endpoint instead. So, when using this option, the headers override the values from the endpoint. The explicitQosEnabled option, by contrast, will only use options set on the endpoint, and not values from the message header. | false | Boolean |
| **camel.component.activemq6.priority** | Values greater than 1 specify the message priority when sending (where 1 is the lowest priority and 9 is the highest). The explicitQosEnabled option must also be enabled in order for this option to have any effect. | 4 | Integer |
| **camel.component.activemq6.pub-sub-no-local** | Specifies whether to inhibit the delivery of messages published by its own connection. | false | Boolean |
| **camel.component.activemq6.queue-browse-strategy** | To use a custom QueueBrowseStrategy when browsing queues. The option is a org.apache.camel.component.jms.QueueBrowseStrategy type. |  | QueueBrowseStrategy |
| **camel.component.activemq6.receive-timeout** | The timeout for receiving messages (in milliseconds). The option is a long type. | 1000 | Long |
| **camel.component.activemq6.recovery-interval** | Specifies the interval between recovery attempts, i.e. when a connection is being refreshed, in milliseconds. The default is 5000 ms, that is, 5 seconds. The option is a long type. | 5000 | Long |
| **camel.component.activemq6.reply-to** | Provides an explicit ReplyTo destination (overrides any incoming value of Message.getJMSReplyTo() in consumer). |  | String |
| **camel.component.activemq6.reply-to-cache-level-name** | Sets the cache level by name for the reply consumer when doing request/reply over JMS. This option only applies when using fixed reply queues (not temporary). Camel will by default use: CACHE\_CONSUMER for exclusive or shared w/ replyToSelectorName. And CACHE\_SESSION for shared without replyToSelectorName. Some JMS brokers such as IBM WebSphere may require to set the replyToCacheLevelName=CACHE\_NONE to work. Note: If using temporary queues then CACHE\_NONE is not allowed, and you must use a higher value such as CACHE\_CONSUMER or CACHE\_SESSION. |  | String |
| **camel.component.activemq6.reply-to-concurrent-consumers** | Specifies the default number of concurrent consumers when doing request/reply over JMS. See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. | 1 | Integer |
| **camel.component.activemq6.reply-to-consumer-type** | The consumer type of the reply consumer (when doing request/reply), which can be one of: Simple, Default, or Custom. The consumer type determines which Spring JMS listener to use. Default will use org.springframework.jms.listener.DefaultMessageListenerContainer, Simple will use org.springframework.jms.listener.SimpleMessageListenerContainer. When Custom is specified, the MessageListenerContainerFactory defined by the messageListenerContainerFactory option will determine what org.springframework.jms.listener.AbstractMessageListenerContainer to use. | default | ConsumerType |
| **camel.component.activemq6.reply-to-delivery-persistent** | Specifies whether to use persistent delivery by default for replies. | true | Boolean |
| **camel.component.activemq6.reply-to-destination-selector-name** | Sets the JMS Selector using the fixed name to be used so you can filter out your own replies from the others when using a shared queue (that is, if you are not using a temporary reply queue). |  | String |
| **camel.component.activemq6.reply-to-max-concurrent-consumers** | Specifies the maximum number of concurrent consumers when using request/reply over JMS. See also the maxMessagesPerTask option to control dynamic scaling up/down of threads. |  | Integer |
| **camel.component.activemq6.reply-to-on-timeout-max-concurrent-consumers** | Specifies the maximum number of concurrent consumers for continue routing when timeout occurred when using request/reply over JMS. | 1 | Integer |
| **camel.component.activemq6.reply-to-override** | Provides an explicit ReplyTo destination in the JMS message, which overrides the setting of replyTo. It is useful if you want to forward the message to a remote Queue and receive the reply message from the ReplyTo destination. |  | String |
| **camel.component.activemq6.reply-to-same-destination-allowed** | Whether a JMS consumer is allowed to send a reply message to the same destination that the consumer is using to consume from. This prevents an endless loop by consuming and sending back the same message to itself. | false | Boolean |
| **camel.component.activemq6.reply-to-type** | Allows for explicitly specifying which kind of strategy to use for replyTo queues when doing request/reply over JMS. Possible values are: Temporary, Shared, or Exclusive. By default Camel will use temporary queues. However if replyTo has been configured, then Shared is used by default. This option allows you to use exclusive queues instead of shared ones. See Camel JMS documentation for more details, and especially the notes about the implications if running in a clustered environment, and the fact that Shared reply queues has lower performance than its alternatives Temporary and Exclusive. |  | ReplyToType |
| **camel.component.activemq6.request-timeout** | The timeout for waiting for a reply when using the InOut Exchange Pattern (in milliseconds). The default is 20 seconds. You can include the header CamelJmsRequestTimeout to override this endpoint configured timeout value, and thus have per message individual timeout values. See also the requestTimeoutCheckerInterval option. The option is a long type. | 20000 | Long |
| **camel.component.activemq6.request-timeout-checker-interval** | Configures how often Camel should check for timed out Exchanges when doing request/reply over JMS. By default Camel checks once per second. But if you must react faster when a timeout occurs, then you can lower this interval, to check more frequently. The timeout is determined by the option requestTimeout. The option is a long type. | 1000 | Long |
| **camel.component.activemq6.selector** | Sets the JMS selector to use. |  | String |
| **camel.component.activemq6.service-location-enabled** | Whether to detect the network address location of the JMS broker on startup. This information is gathered via reflection on the ConnectionFactory, and is vendor specific. This option can be used to turn this off. | true | Boolean |
| **camel.component.activemq6.stream-message-type-enabled** | Sets whether StreamMessage type is enabled or not. Message payloads of streaming kind such as files, InputStream, etc will either by sent as BytesMessage or StreamMessage. This option controls which kind will be used. By default BytesMessage is used which enforces the entire message payload to be read into memory. By enabling this option the message payload is read into memory in chunks and each chunk is then written to the StreamMessage until no more data. | false | Boolean |
| **camel.component.activemq6.subscription-durable** | Set whether to make the subscription durable. The durable subscription name to be used can be specified through the subscriptionName property. Default is false. Set this to true to register a durable subscription, typically in combination with a subscriptionName value (unless your message listener class name is good enough as subscription name). Only makes sense when listening to a topic (pub-sub domain), therefore this method switches the pubSubDomain flag as well. | false | Boolean |
| **camel.component.activemq6.subscription-name** | Set the name of a subscription to create. To be applied in case of a topic (pub-sub domain) with a shared or durable subscription. The subscription name needs to be unique within this client’s JMS client id. Default is the class name of the specified message listener. Note: Only 1 concurrent consumer (which is the default of this message listener container) is allowed for each subscription, except for a shared subscription (which requires JMS 2.0). |  | String |
| **camel.component.activemq6.subscription-shared** | Set whether to make the subscription shared. The shared subscription name to be used can be specified through the subscriptionName property. Default is false. Set this to true to register a shared subscription, typically in combination with a subscriptionName value (unless your message listener class name is good enough as subscription name). Note that shared subscriptions may also be durable, so this flag can (and often will) be combined with subscriptionDurable as well. Only makes sense when listening to a topic (pub-sub domain), therefore this method switches the pubSubDomain flag as well. Requires a JMS 2.0 compatible message broker. | false | Boolean |
| **camel.component.activemq6.synchronous** | Sets whether synchronous processing should be strictly used. | false | Boolean |
| **camel.component.activemq6.task-executor** | Allows you to specify a custom task executor for consuming messages. The option is a org.springframework.core.task.TaskExecutor type. |  | TaskExecutor |
| **camel.component.activemq6.temporary-queue-resolver** | A pluggable TemporaryQueueResolver that allows you to use your own resolver for creating temporary queues (some messaging systems has special requirements for creating temporary queues). The option is a org.apache.camel.component.jms.TemporaryQueueResolver type. |  | TemporaryQueueResolver |
| **camel.component.activemq6.test-connection-on-startup** | Specifies whether to test the connection on startup. This ensures that when Camel starts that all the JMS consumers have a valid connection to the JMS broker. If a connection cannot be granted then Camel throws an exception on startup. This ensures that Camel is not started with failed connections. The JMS producers is tested as well. | false | Boolean |
| **camel.component.activemq6.time-to-live** | When sending messages, specifies the time-to-live of the message (in milliseconds). | \-1 | Long |
| **camel.component.activemq6.transacted** | Specifies whether to use transacted mode. | false | Boolean |
| **camel.component.activemq6.transacted-in-out** | Specifies whether InOut operations (request reply) default to using transacted mode If this flag is set to true, then Spring JmsTemplate will have sessionTransacted set to true, and the acknowledgeMode as transacted on the JmsTemplate used for InOut operations. Note from Spring JMS: that within a JTA transaction, the parameters passed to createQueue, createTopic methods are not taken into account. Depending on the Java EE transaction context, the container makes its own decisions on these values. Analogously, these parameters are not taken into account within a locally managed transaction either, since Spring JMS operates on an existing JMS Session in this case. Setting this flag to true will use a short local JMS transaction when running outside of a managed transaction, and a synchronized local JMS transaction in case of a managed transaction (other than an XA transaction) being present. This has the effect of a local JMS transaction being managed alongside the main transaction (which might be a native JDBC transaction), with the JMS transaction committing right after the main transaction. | false | Boolean |
| **camel.component.activemq6.transaction-manager** | The Spring transaction manager to use. The option is a org.springframework.transaction.PlatformTransactionManager type. |  | PlatformTransactionManager |
| **camel.component.activemq6.transaction-name** | The name of the transaction to use. |  | String |
| **camel.component.activemq6.transaction-timeout** | The timeout value of the transaction (in seconds), if using transacted mode. | \-1 | Integer |
| **camel.component.activemq6.transfer-exception** | If enabled and you are using Request Reply messaging (InOut) and an Exchange failed on the consumer side, then the caused Exception will be send back in response as a jakarta.jms.ObjectMessage. If the client is Camel, the returned Exception is rethrown. This allows you to use Camel JMS as a bridge in your routing - for example, using persistent queues to enable robust routing. Notice that if you also have transferExchange enabled, this option takes precedence. The caught exception is required to be serializable. The original Exception on the consumer side can be wrapped in an outer exception such as org.apache.camel.RuntimeCamelException when returned to the producer. Use this with caution as the data is using Java Object serialization and requires the received to be able to deserialize the data at Class level, which forces a strong coupling between the producers and consumer!. | false | Boolean |
| **camel.component.activemq6.transfer-exchange** | You can transfer the exchange over the wire instead of just the body and headers. The following fields are transferred: In body, Out body, Fault body, In headers, Out headers, Fault headers, exchange properties, exchange exception. This requires that the objects are serializable. Camel will exclude any non-serializable objects and log it at WARN level. You must enable this option on both the producer and consumer side, so Camel knows the payloads is an Exchange and not a regular payload. Use this with caution as the data is using Java Object serialization and requires the receiver to be able to deserialize the data at Class level, which forces a strong coupling between the producers and consumers having to use compatible Camel versions!. | false | Boolean |
| **camel.component.activemq6.trust-all-packages** | Define if all Java packages are trusted or not (for Java object JMS message types). Notice its not recommended practice to send Java serialized objects over network. Setting this to true can expose security risks, so use this with care. | false | Boolean |
| **camel.component.activemq6.use-message-i-d-as-correlation-i-d** | Specifies whether JMSMessageID should always be used as JMSCorrelationID for InOut messages. | false | Boolean |
| **camel.component.activemq6.use-pooled-connection** | Enables or disables whether a PooledConnectionFactory will be used so that when messages are sent to ActiveMQ from outside a message consuming thread, pooling will be used rather than the default with the Spring JmsTemplate which will create a new connection, session, producer for each message then close them all down again. The default value is true. | true | Boolean |
| **camel.component.activemq6.use-single-connection** | Enables or disables whether a Spring SingleConnectionFactory will be used so that when messages are sent to ActiveMQ from outside a message consuming thread, pooling will be used rather than the default with the Spring JmsTemplate which will create a new connection, session, producer for each message then close them all down again. The default value is false and a pooled connection is used by default. | false | Boolean |
| **camel.component.activemq6.username** | Username to use with the ConnectionFactory. You can also configure username/password directly on the ConnectionFactory. |  | String |
| **camel.component.activemq6.wait-for-provision-correlation-to-be-updated-counter** | Number of times to wait for provisional correlation id to be updated to the actual correlation id when doing request/reply over JMS and when the option useMessageIDAsCorrelationID is enabled. | 50 | Integer |
| **camel.component.activemq6.wait-for-provision-correlation-to-be-updated-thread-sleeping-time** | Interval in millis to sleep each time while waiting for provisional correlation id to be updated. The option is a long type. | 100 | Long |
| **camel.component.activemq6.wait-for-temporary-reply-to-to-be-updated-counter** | Number of times to wait for temporary replyTo queue to be created and ready when doing request/reply over JMS. | 200 | Integer |
| **camel.component.activemq6.wait-for-temporary-reply-to-to-be-updated-thread-sleeping-time** | Interval in millis to sleep each time while waiting for temporary replyTo queue to be ready. The option is a long type. | 100 | Long |