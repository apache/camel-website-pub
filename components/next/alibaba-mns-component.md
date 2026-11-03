# Alibaba Message Service (MNS)

**Since Camel 4.23**

**Both producer and consumer are supported**

The Alibaba Cloud Message Service (MNS) component allows you to integrate with [Alibaba Cloud MNS](https://www.alibabacloud.com/product/mns) for queue and topic messaging.

> **Note**
> Alibaba Cloud recommends RocketMQ for new messaging workloads. MNS remains supported, but evaluate [RocketMQ](https://www.alibabacloud.com/product/rocketmq) or the Camel RocketMQ component for greenfield projects.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-alibaba-mns</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

Queue endpoints:

```none
alibaba-mns:queueName[?options]
```

Topic endpoints:

```none
alibaba-mns:topic:topicName[?options]
```

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

The Alibaba Message Service (MNS) component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Alibaba Message Service (MNS) endpoint is configured using URI syntax:

alibaba-mns:queueName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **queueName** (common) | **Required** Queue name, or topic name when using the topic URI syntax. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accountEndpoint** (common) | **Required** MNS account endpoint, for example [https://123456.mns.cn-hangzhou.aliyuncs.com](https://123456.mns.cn-hangzhou.aliyuncs.com). |  | String |
| **operation** (common) | 
Operation to perform by the producer. The consumer does not use it: it receives the messages of the queue.

Enum values:

-   sendMessage
    
-   deleteMessage
    
-   publishMessage
    





 |  | String |
| **region** (common) | **Required** Alibaba Cloud region. |  | String |
| **topicName** (common) | Topic name for publishMessage operations. |  | String |
| **waitSeconds** (common) | Long polling wait time in seconds when receiving messages. | 0 | int |
| **deleteAfterRead** (consumer) | Delete message from the queue after it has been processed. | true | boolean |
| **maxMessagesPerPoll** (consumer) | Maximum number of messages to receive per poll. | 1 | int |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **mnsClient** (advanced) | **Autowired** Autowire an existing MNSClient instance. |  | MNSClient |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |
| **accessKey** (security) | Access key for the cloud user. |  | String |
| **secretKey** (security) | Secret key for the cloud user. |  | String |
| **serviceKeys** (security) | Configuration object for cloud service authentication. |  | ServiceKeys |

## Message Headers

The Alibaba Message Service (MNS) component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAlibabaMnsMessageId** (common) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#MESSAGE_ID) | The MNS message id. |  | String |
| **CamelAlibabaMnsReceiptHandle** (common) Constant: [`RECEIPT_HANDLE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#RECEIPT_HANDLE) | The MNS receipt handle. |  | String |
| **CamelAlibabaMnsMessageBodyMd5** (common) Constant: [`MESSAGE_BODY_MD5`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#MESSAGE_BODY_MD5) | The MD5 digest of the message body. |  | String |
| **CamelAlibabaMnsDelaySeconds** (producer) Constant: [`DELAY_SECONDS`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#DELAY_SECONDS) | Delay in seconds before the message becomes visible. |  | Integer |
| **CamelAlibabaMnsPriority** (producer) Constant: [`PRIORITY`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#PRIORITY) | Message priority. |  | Integer |
| **CamelAlibabaMnsMessageTag** (producer) Constant: [`MESSAGE_TAG`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#MESSAGE_TAG) | Message tag for topic publish operations. |  | String |
| **CamelAlibabaMnsDequeueCount** (consumer) Constant: [`DEQUEUE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#DEQUEUE_COUNT) | Number of times the message has been dequeued. |  | Integer |
| **CamelAlibabaMnsEnqueueTime** (consumer) Constant: [`ENQUEUE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#ENQUEUE_TIME) | Time when the message was enqueued. |  | Date |
| **CamelAlibabaMnsNextVisibleTime** (consumer) Constant: [`NEXT_VISIBLE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#NEXT_VISIBLE_TIME) | Next time the message becomes visible. |  | Date |
| **CamelAlibabaMnsFirstDequeueTime** (consumer) Constant: [`FIRST_DEQUEUE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-mns/latest/org/apache/camel/component/alibaba/mns/constants/MNSHeaders.html#FIRST_DEQUEUE_TIME) | Time when the message was first dequeued. |  | Date |

## Message Body

The message body at each side of the Alibaba Message Service (MNS) component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `text` or `bytes` | The body of the MNS message: a String when it is UTF-8 text, else a byte array, such as for the bytes of a file a producer sent, with the message id, the receipt handle and the dequeue count in headers. Binary data that is valid UTF-8 arrives as a String, so getBody(byte\[\].class) is the reliable way to get the bytes of a message. |
| **Producer input** | `text`, `bytes`, `stream` or `file` | 
The body of the message to send or publish: text is sent as it is, and bytes, a stream or a file as their bytes, so binary data is kept. A Map, a List or a POJO is sent as its toString(), so marshal it first, and no body fails. deleteMessage does not use the body: it takes the receipt handle from the CamelAlibabaMnsReceiptHandle header.

-   With `operation=deleteMessage`: `any`
    





 |
| **Producer output** | `unchanged` | Unchanged: the message id and the MD5 of the body are set in headers (and also as exchange properties, as before), and the request id as an exchange property. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Operations

The producer supports the following operations:

-   `sendMessage` - send a message to a queue
    
-   `deleteMessage` - delete a message from a queue using its receipt handle
    
-   `publishMessage` - publish a message to a topic
    

The consumer receives the messages of a queue: it does not use the `operation` option.

### Message body

The producer sends a `String` body as it is, and a `byte[]`, a stream or a file as its bytes, so binary data is kept. Any other body, such as a `Map`, a `List` or a POJO, is sent as its `toString()`: marshal it first, for example to JSON. A message without a body fails.

The consumer gives the body of a message as a `String` when it is UTF-8 text, and as a `byte[]` otherwise, such as for the bytes of a file that a producer sent. Binary data whose bytes happen to be valid UTF-8 also arrives as a `String`, so when a route needs the bytes of a message, use `getBody(byte[].class)` (or `convertBodyTo(byte[].class)`), which gives back the same bytes in both cases, as UTF-8 is the default charset of Camel.

### Queue producer example

-   Java
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("Hello MNS"))
    .to("alibaba-mns:myQueue?operation=sendMessage&region=cn-hangzhou&accountEndpoint=https://123456.mns.cn-hangzhou.aliyuncs.com&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            expression:
              constant:
                expression: Hello MNS
        - to:
            uri: alibaba-mns:myQueue
            parameters:
              operation: sendMessage
              accountEndpoint: https://123456.mns.cn-hangzhou.aliyuncs.com
              region: cn-hangzhou
              accessKey: "{{alibaba.access-key}}"
              secretKey: "{{alibaba.secret-key}}"
```

### Topic producer example

-   Java
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("Hello Topic"))
    .to("alibaba-mns:topic:myTopic?operation=publishMessage&region=cn-hangzhou&accountEndpoint=https://123456.mns.cn-hangzhou.aliyuncs.com&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            expression:
              constant:
                expression: Hello Topic
        - to:
            uri: alibaba-mns:topic:myTopic
            parameters:
              operation: publishMessage
              accountEndpoint: https://123456.mns.cn-hangzhou.aliyuncs.com
              region: cn-hangzhou
              accessKey: "{{alibaba.access-key}}"
              secretKey: "{{alibaba.secret-key}}"
```

### Queue consumer example

-   Java
    
-   YAML
    

```java
from("alibaba-mns:myQueue?region=cn-hangzhou&accountEndpoint=https://123456.mns.cn-hangzhou.aliyuncs.com&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)&deleteAfterRead=true")
    .to("bean:processMessage");
```

```yaml
- route:
    from:
      uri: alibaba-mns:myQueue
      parameters:
        region: cn-hangzhou
        accountEndpoint: https://123456.mns.cn-hangzhou.aliyuncs.com
        accessKey: "{{alibaba.access-key}}"
        secretKey: "{{alibaba.secret-key}}"
        deleteAfterRead: true
      steps:
        - to:
            uri: bean:processMessage
```

### Exchange properties evaluated by the producer

  
| Property | Type | Description |
| --- | --- | --- |
| `CamelAlibabaMnsOperation` | `String` | Operation to perform |
| `CamelAlibabaMnsQueueName` | `String` | Queue name override |
| `CamelAlibabaMnsTopicName` | `String` | Topic name for publish operations |
| `CamelAlibabaMnsReceiptHandle` | `String` | Receipt handle for delete operations |

### Headers and exchange properties set by the producer

`sendMessage` and `publishMessage` set these headers, as the consumer does:

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelAlibabaMnsMessageId` | `String` | Message id returned by MNS |
| `CamelAlibabaMnsMessageBodyMd5` | `String` | MD5 digest of the message body |

They also set these exchange properties:

  
| Property | Type | Description |
| --- | --- | --- |
| `CamelAlibabaMnsRequestId` | `String` | Request id returned by MNS |
| `CamelAlibabaMnsMessageId` | `String` | Message id returned by MNS, as the header of the same name |
| `CamelAlibabaMnsMessageBodyMd5` | `String` | MD5 digest of the message body, as the header of the same name |

In Camel 4.23 the producer set the message id and the MD5 only as exchange properties. They are still set as properties, so that routes that read them keep working, but prefer the headers.

## Examples

For more examples, see the unit tests in the `camel-alibaba-mns` module.