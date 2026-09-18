# RocketMQ

**Since Camel 3.20**

**Both producer and consumer are supported**

The RocketMQ component allows you to produce and consume messages from [RocketMQ](https://rocketmq.apache.org/) instances.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-rocketmq</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

> **Note**
> Since RocketMQ 5.x API is compatible with 4.x, this component works with both RocketMQ 4.x and 5.x. Users could change RocketMQ dependencies on their own.

## URI format

rocketmq:topicName?\[options\]

The topic name determines the topic to which the produced messages will be sent to. In the case of consumers, the topic name determines the topic will be subscribed. This component uses RocketMQ push consumer by default.

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

The RocketMQ component supports 20 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accessChannel** (common) | Access channel of RocketMQ cluster. LOCAL or CLOUD, LOCAL by default. | LOCAL | String |
| **enableTrace** (common) | Whether to enable trace. | false | boolean |
| **namespace** (common) | Namespace of RocketMQ cluster. You need to specify this if you are using serverless version of RocketMQ. |  | String |
| **namesrvAddr** (common) | Name server address of RocketMQ cluster. | localhost:9876 | String |
| **sendTag** (common) | Each message would be sent with this tag. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerGroup** (consumer) | Consumer group name. |  | String |
| **messageSelectorType** (consumer) | Message Selector Type, TAG or SQL TAG by default. | tag | String |
| **subscribeSql** (consumer) | Subscribe SQL of consumer. See [https://rocketmq.apache.org/docs/featureBehavior/07messagefilter/#attribute-based-sql-filtering](https://rocketmq.apache.org/docs/featureBehavior/07messagefilter/#attribute-based-sql-filtering) for more details. | 1 = 1 | String |
| **subscribeTags** (consumer) | Subscribe tags of consumer. Multiple tags could be split by , such as TagATagB. | \* | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **producerGroup** (producer) | Producer group name. |  | String |
| **replyToConsumerGroup** (producer) | Consumer group name used for receiving response. |  | String |
| **replyToTopic** (producer) | Topic used for receiving response when using in-out pattern. |  | String |
| **waitForSendResult** (producer) | Whether waiting for send result before routing to next endpoint. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **requestTimeoutCheckerIntervalMillis** (advanced) | Check interval milliseconds of request timeout. | 1000 | long |
| **requestTimeoutMillis** (advanced) | Timeout milliseconds of receiving response when using in-out pattern. | 10000 | long |
| **accessKey** (secret) | Access key for RocketMQ ACL. |  | String |
| **secretKey** (secret) | Secret key for RocketMQ ACL. |  | String |

## Endpoint Options

The RocketMQ endpoint is configured using URI syntax:

rocketmq:topicName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topicName** (common) | **Required** Topic name of this endpoint. |  | String |

### Query Parameters (21 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accessChannel** (common) | 
Access channel of RocketMQ cluster. LOCAL or CLOUD, LOCAL by default.

Enum values:

-   LOCAL
    
-   CLOUD
    





 | LOCAL | String |
| **enableTrace** (common) | Whether to enable trace. | false | boolean |
| **namespace** (common) | Namespace of RocketMQ cluster. You need to specify this if you are using serverless version of RocketMQ. |  | String |
| **namesrvAddr** (common) | Name server address of RocketMQ cluster. | localhost:9876 | String |
| **consumerGroup** (consumer) | Consumer group name. |  | String |
| **messageSelectorType** (consumer) | 

Message Selector Type, TAG or SQL TAG by default.

Enum values:

-   tag
    
-   sql
    





 | tag | String |
| **subscribeSql** (consumer) | Subscribe SQL of consumer. See [https://rocketmq.apache.org/docs/featureBehavior/07messagefilter/#attribute-based-sql-filtering](https://rocketmq.apache.org/docs/featureBehavior/07messagefilter/#attribute-based-sql-filtering) for more details. | 1 = 1 | String |
| **subscribeTags** (consumer) | Subscribe tags of consumer. Multiple tags could be split by , such as TagATagB. | \* | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **producerGroup** (producer) | Producer group name. |  | String |
| **replyToConsumerGroup** (producer) | Consumer group name used for receiving response. |  | String |
| **replyToTopic** (producer) | Topic used for receiving response when using in-out pattern. |  | String |
| **sendTag** (producer) | Each message would be sent with this tag. |  | String |
| **waitForSendResult** (producer) | Whether waiting for send result before routing to next endpoint. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **requestTimeoutCheckerIntervalMillis** (advanced) | Check interval milliseconds of request timeout. | 1000 | long |
| **requestTimeoutMillis** (advanced) | Timeout milliseconds of receiving response when using in-out pattern. | 10000 | long |
| **accessKey** (security) | Access key for RocketMQ ACL. |  | String |
| **secretKey** (security) | Secret key for RocketMQ ACL. |  | String |

## Message Headers

The RocketMQ component supports 20 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelRockerMQTopic** (consumer) Constant: [`TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#TOPIC) | Topic of message. |  | String |
| **CamelRockerMQTag** (consumer) Constant: [`TAG`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#TAG) | Tag of message. |  | String |
| **CamelRockerMQKey** (consumer) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#KEY) | Key of message. |  | String |
| **CamelRockerMQOverrideTopicName** (producer) Constant: [`OVERRIDE_TOPIC_NAME`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#OVERRIDE_TOPIC_NAME) | If this header is set, the message will be routed to the topic specified by this header instead of the origin topic in endpoint. |  | String |
| **CamelRockerMQOverrideTag** (producer) Constant: [`OVERRIDE_TAG`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#OVERRIDE_TAG) | If this header is set, the message’s tag will be set to value specified by this header instead of the sendTag defined in endpoint. |  | String |
| **CamelRockerMQOverrideMessageKey** (producer) Constant: [`OVERRIDE_MESSAGE_KEY`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#OVERRIDE_MESSAGE_KEY) | Set keys for the message. When using in-out pattern, the value will be prepended to the generated keys. |  | String |
| **CamelRockerMQBrokerName** (consumer) Constant: [`BROKER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#BROKER_NAME) | Broker name. |  | String |
| **CamelRockerMQQueueId** (consumer) Constant: [`QUEUE_ID`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#QUEUE_ID) | Queue ID. |  | int |
| **CamelRockerMQStoreSize** (consumer) Constant: [`STORE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#STORE_SIZE) | Store size. |  | int |
| **CamelRockerMQQueueOffset** (consumer) Constant: [`QUEUE_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#QUEUE_OFFSET) | Queue offset. |  | long |
| **CamelRockerMQSysFlag** (consumer) Constant: [`SYS_FLAG`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#SYS_FLAG) | Sys flag. |  | int |
| **CamelRockerMQBornTimestamp** (consumer) Constant: [`BORN_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#BORN_TIMESTAMP) | Born timestamp. |  | long |
| **CamelRockerMQBornHost** (consumer) Constant: [`BORN_HOST`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#BORN_HOST) | Born host. |  | SocketAddress |
| **CamelRockerMQStoreTimestamp** (consumer) Constant: [`STORE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#STORE_TIMESTAMP) | Store timestamp. |  | long |
| **CamelRockerMQStoreHost** (consumer) Constant: [`STORE_HOST`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#STORE_HOST) | Store host. |  | SocketAddress |
| **CamelRockerMQMsgId** (consumer) Constant: [`MSG_ID`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#MSG_ID) | Msg ID. |  | String |
| **CamelRockerMQCommitLogOffset** (consumer) Constant: [`COMMIT_LOG_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#COMMIT_LOG_OFFSET) | Commit log offset. |  | long |
| **CamelRockerMQBodyCrc** (consumer) Constant: [`BODY_CRC`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#BODY_CRC) | Body CRC. |  | int |
| **CamelRockerMQReconsumeTimes** (consumer) Constant: [`RECONSUME_TIMES`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#RECONSUME_TIMES) | Reconsume times. |  | int |
| **CamelRockerMQPreparedTransactionOffset** (consumer) Constant: [`PREPARED_TRANSACTION_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-rocketmq/latest/org/apache/camel/component/rocketmq/RocketMQConstants.html#PREPARED_TRANSACTION_OFFSET) | Prepard transaction offset. |  | long |

## Usage

### InOut Pattern

InOut Pattern based on Message Key. When the producer sends the message, a messageKey will be generated and append to the message’s key.

After the message sent, a consumer will listen to the topic configured by the parameter `ReplyToTopic`.

When a message from `ReplyToTpic` contains the key, it means that the reply received and continue routing.

If `requestTimeoutMillis` elapsed and no reply received, an exception will be thrown.

```java
from("rocketmq:START_TOPIC?producerGroup=p1&consumerGroup=c1")

.to(ExchangePattern.InOut, "rocketmq:INTERMEDIATE_TOPIC" +
        "?producerGroup=intermediaProducer" +
        "&consumerGroup=intermediateConsumer" +
        "&replyToTopic=REPLY_TO_TOPIC" +
        "&replyToConsumerGroup=replyToConsumerGroup" +
        "&requestTimeoutMillis=30000")

.to("log:InOutRoute?showAll=true")
```

## Examples

Receive messages from a topic named `from_topic`, route to `to_topic`.

```java
from("rocketmq:FROM_TOPIC?namesrvAddr=localhost:9876&consumerGroup=consumer")
    .to("rocketmq:TO_TOPIC?namesrvAddr=localhost:9876&producerGroup=producer");
```

Setting specific headers can change routing behaviour. For example, if header `RocketMQConstants.OVERRIDE_TOPIC_NAME` was set, the message will be sent to `ACTUAL_TARGET` instead of `ORIGIN_TARGET`.

```java
from("rocketmq:FROM?consumerGroup=consumer")
        .process(exchange -> {
            exchange.getMessage().setHeader(RocketMQConstants.OVERRIDE_TOPIC_NAME, "ACTUAL_TARGET");
            exchange.getMessage().setHeader(RocketMQConstants.OVERRIDE_TAG, "OVERRIDE_TAG");
            exchange.getMessage().setHeader(RocketMQConstants.OVERRIDE_MESSAGE_KEY, "OVERRIDE_MESSAGE_KEY");
        }
)
.to("rocketmq:ORIGIN_TARGET?producerGroup=producer")
.to("log:RocketRoute?showAll=true")
```