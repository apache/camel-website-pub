# Simple JMS2

**Since Camel 2.19**

**Both producer and consumer are supported**

The Simple JMS Component is a JMS component that only uses JMS APIs and no third-party framework such as Spring JMS.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-sjms2</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

sjms2:\[queue:|topic:\]destinationName\[?options\]

Where `destinationName` is a JMS queue or topic name. By default, the `destinationName` is interpreted as a queue name. For example, to connect to the queue, `FOO.BAR` use:

sjms2:FOO.BAR

You can include the optional `queue:` prefix, if you prefer:

sjms2:queue:FOO.BAR

To connect to a topic, you _must_ include the `topic:` prefix. For example, to connect to the topic, `Stocks.Prices`, use:

sjms2:topic:Stocks.Prices

You append query options to the URI using the following format, `?option=value&option=value&…​`

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

The Simple JMS2 component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | Sets the JMS client ID to use. Note that this value, if specified, must be unique and can only be used by a single JMS connection instance. It is typically only required for durable topic subscriptions. If using Apache ActiveMQ you may prefer to use Virtual Topics instead. |  | String |
| **connectionFactory** (common) | **Autowired** The connection factory to be use. A connection factory must be configured either on the component or endpoint. |  | ConnectionFactory |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **destinationCreationStrategy** (advanced) | To use a custom DestinationCreationStrategy. |  | DestinationCreationStrategy |
| **exceptionListener** (advanced) | Specifies the JMS Exception Listener that is to be notified of any underlying JMS exceptions. |  | ExceptionListener |
| **jmsKeyFormatStrategy** (advanced) | Pluggable strategy for encoding and decoding JMS keys so they can be compliant with the JMS specification. Camel provides one implementation out of the box: default. The default strategy will safely marshal dots and hyphens (. and -). Can be used for JMS brokers which do not care whether JMS header keys contain illegal characters. You can provide your own implementation of the org.apache.camel.component.jms.JmsKeyFormatStrategy and refer to it using the # notation. |  | JmsKeyFormatStrategy |
| **messageCreatedStrategy** (advanced) | To use the given MessageCreatedStrategy which are invoked when Camel creates new instances of jakarta.jms.Message objects when Camel is sending a JMS message. |  | MessageCreatedStrategy |
| **objectMessageEnabled** (advanced) | Whether to enable sending and receiving JMS ObjectMessage. By default this is disabled because Java object serialization is a known source of security vulnerabilities. Enable this option only if you trust the source of the messages and need to send or receive Java serialized objects via JMS. When disabled, Camel will refuse to create or read JMS ObjectMessage instances. Options that rely on ObjectMessage internally (such as transferException) require this option to be enabled. | false | boolean |
| **recoveryInterval** (advanced) | Specifies the interval between recovery attempts, i.e. when a connection is being refreshed, in milliseconds. The default is 5000 ms, that is, 5 seconds. | 5000 | long |
| **replyToOnTimeoutMaxConcurrentConsumers** (advanced) | Specifies the maximum number of concurrent consumers for continue routing when timeout occurred when using request/reply over JMS. | 1 | int |
| **requestTimeoutCheckerInterval** (advanced) | Configures how often Camel should check for timed out Exchanges when doing request/reply over JMS. By default Camel checks once per second. But if you must react faster when a timeout occurs, then you can lower this interval, to check more frequently. The timeout is determined by the option requestTimeout. | 1000 | long |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **deserializationFilter** (security) | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied as a defense-in-depth check on the class of the body returned by jakarta.jms.ObjectMessage.getObject(). The pattern is evaluated after the JMS provider has deserialized the payload, so this option alone does not prevent gadget-chain execution that happens inside the provider’s ObjectInputStream; to block such attacks, also configure the JMS provider’s own deserialization filter and/or the JVM-wide -Djdk.serialFilter. When this option is not set and no JVM-wide filter is configured, a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. is applied. |  | String |

## Endpoint Options

The Simple JMS2 endpoint is configured using URI syntax:

sjms2:destinationType:destinationName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **destinationType** (common) | 
The kind of destination to use.

Enum values:

-   queue
    
-   topic
    





 | queue | String |
| **destinationName** (common) | **Required** DestinationName is a JMS queue or topic name. By default, the destinationName is interpreted as a queue name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **acknowledgementMode** (common) | 
The JMS acknowledgement name, which is one of: SESSION\_TRANSACTED, CLIENT\_ACKNOWLEDGE, AUTO\_ACKNOWLEDGE, DUPS\_OK\_ACKNOWLEDGE.

Enum values:

-   SESSION\_TRANSACTED
    
-   CLIENT\_ACKNOWLEDGE
    
-   AUTO\_ACKNOWLEDGE
    
-   DUPS\_OK\_ACKNOWLEDGE
    





 | AUTO\_ACKNOWLEDGE | SessionAcknowledgementType |
| **connectionFactory** (common) | The connection factory to be use. A connection factory must be configured either on the component or endpoint. |  | ConnectionFactory |
| **disableReplyTo** (common) | Specifies whether Camel ignores the JMSReplyTo header in messages. If true, Camel does not send a reply back to the destination specified in the JMSReplyTo header. You can use this option if you want Camel to consume from a route and you do not want Camel to automatically send back a reply message because another component in your code handles the reply message. You can also use this option if you want to use Camel as a proxy between different message brokers and you want to route message from one system to another. | false | boolean |
| **replyTo** (common) | Provides an explicit ReplyTo destination (overrides any incoming value of Message.getJMSReplyTo() in consumer). |  | String |
| **testConnectionOnStartup** (common) | Specifies whether to test the connection on startup. This ensures that when Camel starts that all the JMS consumers have a valid connection to the JMS broker. If a connection cannot be granted then Camel throws an exception on startup. This ensures that Camel is not started with failed connections. The JMS producers is tested as well. | false | boolean |
| **asyncConsumer** (consumer) | Whether the JmsConsumer processes the Exchange asynchronously. If enabled then the JmsConsumer may pickup the next message from the JMS queue, while the previous message is being processed asynchronously (by the Asynchronous Routing Engine). This means that messages may be processed not 100% strictly in order. If disabled (as default) then the Exchange is fully processed before the JmsConsumer will pickup the next message from the JMS queue. Note if transacted has been enabled, then asyncConsumer=true does not run asynchronously, as transaction must be executed synchronously (Camel 3.0 may support async transactions). | false | boolean |
| **autoStartup** (consumer) | Specifies whether the consumer container should auto-startup. | true | boolean |
| **clientId** (consumer) | Sets the JMS client ID to use. Note that this value, if specified, must be unique and can only be used by a single JMS connection instance. It is typically only required for durable topic subscriptions. If using Apache ActiveMQ you may prefer to use Virtual Topics instead. |  | String |
| **concurrentConsumers** (consumer) | Specifies the number of concurrent consumers when consuming from JMS (not for request/reply over JMS). The concurrent consumer is fixed at startup and cannot be dynamic scaled like the camel-jms component. When doing request/reply over JMS then the option replyToConcurrentConsumers is used to control number of concurrent consumers on the reply message listener. | 1 | int |
| **durable** (consumer) | Sets the topic to be durable. | false | boolean |
| **durableSubscriptionName** (consumer) | The durable subscriber name for specifying durable topic subscriptions. The clientId option must be configured as well. |  | String |
| **replyToDeliveryPersistent** (consumer) | Specifies whether to use persistent delivery by default for replies. | true | boolean |
| **shared** (consumer) | Sets the topic to be shared. | false | boolean |
| **subscriptionId** (consumer) | Sets the topic subscription id, required for durable or shared topics. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **eagerLoadingOfProperties** (consumer (advanced)) | Enables eager loading of JMS properties and payload as soon as a message is loaded which generally is inefficient as the JMS properties may not be required but sometimes can catch early any issues with the underlying JMS provider and the use of JMS properties. See also the option eagerPoisonBody. | false | boolean |
| **eagerPoisonBody** (consumer (advanced)) | If eagerLoadingOfProperties is enabled and the JMS message payload (JMS body or JMS properties) is poison (cannot be read/mapped), then set this text as the message body instead so the message can be processed (the cause of the poison are already stored as exception on the Exchange). This can be turned off by setting eagerPoisonBody=false. See also the option eagerLoadingOfProperties. | Poison JMS message due to ${exception.message} | String |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **messageSelector** (consumer (advanced)) | Sets the JMS Message selector syntax. |  | String |
| **replyToSameDestinationAllowed** (consumer (advanced)) | Whether a JMS consumer is allowed to send a reply message to the same destination that the consumer is using to consume from. This prevents an endless loop by consuming and sending back the same message to itself. | false | boolean |
| **deliveryMode** (producer) | 

Specifies the delivery mode to be used. Possible values are those defined by jakarta.jms.DeliveryMode. NON\_PERSISTENT = 1 and PERSISTENT = 2.

Enum values:

-   1
    
-   2
    





 |  | Integer |
| **deliveryPersistent** (producer) | Specifies whether persistent delivery is used by default. | true | boolean |
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
| **replyToConcurrentConsumers** (producer) | Specifies the default number of concurrent consumers when doing request/reply over JMS. | 1 | int |
| **replyToOverride** (producer) | Provides an explicit ReplyTo destination in the JMS message, which overrides the setting of replyTo. It is useful if you want to forward the message to a remote Queue and receive the reply message from the ReplyTo destination. |  | String |
| **replyToType** (producer) | 

Allows for explicitly specifying which kind of strategy to use for replyTo queues when doing request/reply over JMS. Possible values are: Temporary or Exclusive. By default Camel will use temporary queues. However if replyTo has been configured, then Exclusive is used.

Enum values:

-   Temporary
    
-   Exclusive
    





 |  | ReplyToType |
| **requestTimeout** (producer) | The timeout for waiting for a reply when using the InOut Exchange Pattern (in milliseconds). The default is 20 seconds. You can include the header CamelJmsRequestTimeout to override this endpoint configured timeout value, and thus have per message individual timeout values. See also the requestTimeoutCheckerInterval option. | 20000 | long |
| **timeToLive** (producer) | When sending messages, specifies the time-to-live of the message (in milliseconds). | \-1 | long |
| **allowNullBody** (producer (advanced)) | Whether to allow sending messages with no body. If this option is false and the message body is null, then an JMSException is thrown. | true | boolean |
| **disableTimeToLive** (producer (advanced)) | Use this option to force disabling time to live. For example when you do request/reply over JMS, then Camel will by default use the requestTimeout value as time to live on the message being sent. The problem is that the sender and receiver systems have to have their clocks synchronized, so they are in sync. This is not always so easy to archive. So you can use disableTimeToLive=true to not set a time to live value on the sent message. Then the message will not expire on the receiver system. See below in section About time to live for more details. | false | boolean |
| **explicitQosEnabled** (producer (advanced)) | Set if the deliveryMode, priority or timeToLive qualities of service should be used when sending messages. This option is based on Spring’s JmsTemplate. The deliveryMode, priority and timeToLive options are applied to the current endpoint. This contrasts with the preserveMessageQos option, which operates at message granularity, reading QoS properties exclusively from the Camel In message headers. | false | Boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **preserveMessageQos** (producer (advanced)) | Set to true, if you want to send message using the QoS settings specified on the message, instead of the QoS settings on the JMS endpoint. The following three headers are considered JMSPriority, JMSDeliveryMode, and JMSExpiration. You can provide all or only some of them. If not provided, Camel will fall back to use the values from the endpoint instead. So, when using this option, the headers override the values from the endpoint. The explicitQosEnabled option, by contrast, will only use options set on the endpoint, and not values from the message header. | false | boolean |
| **asyncStartListener** (advanced) | Whether to startup the consumer message listener asynchronously, when starting a route. For example if a JmsConsumer cannot get a connection to a remote JMS broker, then it may block while retrying and/or fail over. This will cause Camel to block while starting routes. By setting this option to true, you will let routes startup, while the JmsConsumer connects to the JMS broker using a dedicated thread in asynchronous mode. If this option is used, then beware that if the connection could not be established, then an exception is logged at WARN level, and the consumer will not be able to receive messages; You can then restart the route to retry. | false | boolean |
| **asyncStopListener** (advanced) | Whether to stop the consumer message listener asynchronously, when stopping a route. | false | boolean |
| **destinationCreationStrategy** (advanced) | To use a custom DestinationCreationStrategy. |  | DestinationCreationStrategy |
| **exceptionListener** (advanced) | Specifies the JMS Exception Listener that is to be notified of any underlying JMS exceptions. |  | ExceptionListener |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **includeAllJMSXProperties** (advanced) | Whether to include all JMSXxxx properties when mapping from JMS to Camel Message. Setting this to true will include properties such as JMSXAppID, and JMSXUserID etc. Note: If you are using a custom headerFilterStrategy then this option does not apply. | false | boolean |
| **jmsKeyFormatStrategy** (advanced) | Pluggable strategy for encoding and decoding JMS keys so they can be compliant with the JMS specification. Camel provides two implementations out of the box: default and passthrough. The default strategy will safely marshal dots and hyphens (. and -). The passthrough strategy leaves the key as is. Can be used for JMS brokers which do not care whether JMS header keys contain illegal characters. You can provide your own implementation of the org.apache.camel.component.jms.JmsKeyFormatStrategy and refer to it using the # notation. |  | JmsKeyFormatStrategy |
| **jmsMessageType** (advanced) | 

Allows you to force the use of a specific jakarta.jms.Message implementation for sending JMS messages. Possible values are: Bytes, Map, Object, Stream, Text. By default, Camel would determine which JMS message type to use from the In body type. This option allows you to specify it.

Enum values:

-   Bytes
    
-   Map
    
-   Object
    
-   Stream
    
-   Text
    





 |  | JmsMessageType |
| **mapJmsMessage** (advanced) | Specifies whether Camel should auto map the received JMS message to a suited payload type, such as jakarta.jms.TextMessage to a String etc. See section about how mapping works below for more details. | true | boolean |
| **messageCreatedStrategy** (advanced) | To use the given MessageCreatedStrategy which are invoked when Camel creates new instances of jakarta.jms.Message objects when Camel is sending a JMS message. |  | MessageCreatedStrategy |
| **objectMessageEnabled** (advanced) | Whether to enable sending and receiving JMS ObjectMessage. By default this is disabled because Java object serialization is a known source of security vulnerabilities. Enable this option only if you trust the source of the messages and need to send or receive Java serialized objects via JMS. When disabled, Camel will refuse to create or read JMS ObjectMessage instances. Options that rely on ObjectMessage internally (such as transferException) require this option to be enabled. | false | boolean |
| **recoveryInterval** (advanced) | Specifies the interval between recovery attempts, i.e. when a connection is being refreshed, in milliseconds. The default is 5000 ms, that is, 5 seconds. | 5000 | long |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **transferException** (advanced) | If enabled and you are using Request Reply messaging (InOut) and an Exchange failed on the consumer side, then the caused Exception will be send back in response as a jakarta.jms.ObjectMessage. If the client is Camel, the returned Exception is rethrown. This allows you to use Camel JMS as a bridge in your routing - for example, using persistent queues to enable robust routing. Notice that if you also have transferExchange enabled, this option takes precedence. The caught exception is required to be serializable. The original Exception on the consumer side can be wrapped in an outer exception such as org.apache.camel.RuntimeCamelException when returned to the producer. Use this with caution as the data is using Java Object serialization and requires the received to be able to deserialize the data at Class level, which forces a strong coupling between the producers and consumer!. | false | boolean |
| **deserializationFilter** (security) | Sets an ObjectInputFilter pattern (jdk.serialFilter syntax) applied as a defense-in-depth check on the class of the body returned by jakarta.jms.ObjectMessage.getObject(). The pattern is evaluated after the JMS provider has deserialized the payload, so this option alone does not prevent gadget-chain execution that happens inside the provider’s ObjectInputStream; to block such attacks, also configure the JMS provider’s own deserialization filter and/or the JVM-wide -Djdk.serialFilter. When this option is not set and no JVM-wide filter is configured, a conservative default filter denying java.net. and otherwise allowing java., javax. and org.apache.camel. is applied. |  | String |
| **transacted** (transaction) | Specifies whether to use transacted mode. | false | boolean |

## Message Headers

The Simple JMS2 component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJMSDestinationName** (producer) Constant: [`JMS_DESTINATION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-sjms2/latest/org/apache/camel/component/sjms/SjmsConstants.html#JMS_DESTINATION_NAME) | DestinationName is a JMS queue or topic name. By default, the destinationName is interpreted as a queue name. |  | String |
| **CamelJmsRequestTimeout** (producer) Constant: [`JMS_REQUEST_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-sjms2/latest/org/apache/camel/component/sjms/SjmsConstants.html#JMS_REQUEST_TIMEOUT) | The timeout for waiting for a reply when using the InOut Exchange Pattern (in milliseconds). |  | long |
| **JMSCorrelationID** (producer) Constant: [`JMS_CORRELATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-sjms2/latest/org/apache/camel/component/sjms/SjmsConstants.html#JMS_CORRELATION_ID) | The correlation ID. |  | String |
| **JMSReplyTo** (producer) Constant: [`JMS_REPLY_TO`](https://javadoc.io/doc/org.apache.camel/camel-sjms2/latest/org/apache/camel/component/sjms/SjmsConstants.html#JMS_REPLY_TO) | Provides an explicit ReplyTo destination (overrides any incoming value of Message.getJMSReplyTo() in consumer). |  | String |

## Usage

The component was reworked from Camel 3.8 onwards to be similar to the existing Camel JMS component that is based on Spring JMS.

The reason is to offer many of the same features and functionality from the JMS component, but for users that require lightweight without having to include the Spring Framework.

There are some advanced features in the Spring JMS component that has been omitted, such as shared queues for request/reply. Spring JMS offers fine-grained tunings for concurrency settings, which can be tweaked for dynamic scaling up and down depending on load. This is a special feature in Spring JMS that would require substantial code to implement in SJMS2.

The SJMS2 component does not support for Spring or JTA Transaction, however, support for internal local transactions is supported using JMS or Transaction or Client Acknowledge Mode. See further details below.

### Reuse endpoint and send to different destinations computed at runtime

If you need to send messages to a lot of different JMS destinations, it makes sense to reuse a SJMS endpoint and specify the real destination in a message header. This allows Camel to reuse the same endpoint, but send to different destinations. This greatly reduces the number of endpoints created and economizes on memory and thread resources.

> **Tip**
> Using [toD](eips/toD-eip.md) is easier than specifying the dynamic destination with a header

You can specify the destination in the following headers:

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelJmsDestinationName` | `String` | The destination name. |

For example, the following route shows how you can compute a destination at run time and use it to override the destination appearing in the JMS URL:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://inbox")
  .to("bean:computeDestination")
  .to("sjms2:queue:dummy");
```

```xml
<route>
  <from uri="file://inbox"/>
  <to uri="bean:computeDestination"/>
  <to uri="sjms2:queue:dummy"/>
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
            uri: sjms2:queue:dummy
```

The queue name, `dummy`, is just a placeholder. It must be provided as part of the JMS endpoint URL, but it will be ignored in this example.

In the `computeDestination` bean, specify the real destination by setting the `CamelJmsDestinationName` header as follows:

_Java-only: programmatic header manipulation with Exchange API_

```java
public void setJmsHeader(Exchange exchange) {
   String id = ....
   exchange.getIn().setHeader("CamelJmsDestinationName", "order:" + id");
}
```

Then Camel will read this header and use it as the destination instead of the one configured on the endpoint. So, in this example Camel sends the message to `sjms2:queue:order:2`, assuming the `id` value was 2.

Keep in mind that the JMS producer removes both `CamelJmsDestinationName` headers from the exchange and do not propagate them to the created JMS message to avoid the accidental loops in the routes (in scenarios when the message will be forwarded to another JMS endpoint).

### Using toD

If you need to send messages to a lot of different JMS destinations, it makes sense to reuse a SJMS2 endpoint and specify the dynamic destinations with simple language using [toD](eips/toD-eip.md).

For example, suppose you need to send messages to queues with order types, then using toD could, for example, be done as follows:

Example SJMS2 route with `toD`

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:order")
  .toD("sjms2:order-${header.orderType}");
```

```xml
<route>
  <from uri="direct:order"/>
  <toD uri="sjms2:order-${header.orderType}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:order
      steps:
        - toD:
            uri: "sjms2:order-${header.orderType}"
```

### Local transactions

When using `transacted=true` then JMS Transacted Acknowledge Mode are in use. The SJMS2 component supports this from both the consumer and producers. If a consumer is transacted, then the active JMS Session will commit or rollback at the end of processing the message.

SJMS2 producers that are `transacted=true` will also defer until the end of processing the message before the active JMS Session will commit or rollback.

You can combine consumer and producer, such as:

Example transacted SJMS2 route with consumer and producer

-   Java
    
-   XML
    
-   YAML
    

```java
from("sjms2:cheese?transacted=true")
  .to("bean:foo")
  .to("sjms2:foo?transacted=true")
  .to("bean:bar");
```

```xml
<route>
  <from uri="sjms2:cheese?transacted=true"/>
  <to uri="bean:foo"/>
  <to uri="sjms2:foo?transacted=true"/>
  <to uri="bean:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: sjms2:cheese
      parameters:
        transacted: true
      steps:
        - to:
            uri: bean:foo
        - to:
            uri: sjms2:foo
            parameters:
              transacted: true
        - to:
            uri: bean:bar
```

Here the consumer and producer are both transacted, which means that only at the end of processing the message, then both the consumer and the producer will commit (or rollback in case of an exception during routing).

### Message Header Format

The SJMS2 Component uses the same header format strategy used in the Camel JMS Component. This pluggable strategy ensures that messages sent over the wire conform to the JMS Message spec.

For the `exchange.in.header` the following rules apply for the header keys:

-   Keys starting with `JMS` or `JMSX` are reserved.
    
-   `exchange.in.headers` keys must be literals and all be valid Java identifiers (do not use dots in the key name).
    
-   Camel replaces dots & hyphens and the reverse when consuming JMS messages:
    
    -   it is replaced by _DOT_ and the reverse replacement when Camel consumes the message.
        
    -   it is replaced by _HYPHEN_ and the reverse replacement when Camel consumes the message.See also the option `jmsKeyFormatStrategy`, which allows use of your own custom strategy for formatting keys.
        
    

### Message Content

To deliver content over the wire, we must ensure that the body of the message that is being delivered adheres to the JMS Message Specification. Therefore, all that are produced must either be primitives or their counter-objects (such as `Integer`, `Long`, `Character`). The types, `String`, `CharSequence`, `Date`, `BigDecimal` and `BigInteger` are all converted to their `toString()` representation. All other types are dropped.

### Clustering

When using _InOut_ with SJMS2 in a clustered environment, you must either use TemporaryQueue destinations or use a unique reply to destination per InOut producer endpoint. The producer handles message correlation, not with message selectors at the broker.

> **Note**
> You should only use queues as reply-to destination types, topics are not recommended or fully supported.

Currently, the only correlation strategy is to use the `JMSCorrelationId`. The _InOut_ Consumer uses this strategy as well ensuring that all response messages to the included `JMSReplyTo` destination also have the `JMSCorrelationId` copied from the request as well.