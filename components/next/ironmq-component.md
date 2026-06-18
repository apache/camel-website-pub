# IronMQ

> **Warning**
> **Deprecated:** This ironmq is deprecated and may be removed in a future release.

**Since Camel 2.17**

**Both producer and consumer are supported**

The IronMQ component provides integration with [IronMQ](http://www.iron.io/products/mq) an elastic and durable hosted message queue as a service.

The component uses the [IronMQ java client](https://github.com/iron-io/iron_mq_java) library.

To run it requires an IronMQ account and a project id and token.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ironmq</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

 ironmq:queueName\[?options\]

Where `queueName` identifies the IronMQ queue you want to publish or consume messages from.

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

The IronMQ component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The IronMQ endpoint is configured using URI syntax:

ironmq:queueName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **queueName** (common) | **Required** The name of the IronMQ queue. |  | String |

### Query Parameters (31 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ironMQCloud** (common) | IronMq Cloud url. Urls for public clusters: [https://mq-aws-us-east-1-1.iron.io](https://mq-aws-us-east-1-1.iron.io) (US) and [https://mq-aws-eu-west-1-1.iron.io](https://mq-aws-eu-west-1-1.iron.io) (EU). | [https://mq-aws-us-east-1-1.iron.io](https://mq-aws-us-east-1-1.iron.io) | String |
| **preserveHeaders** (common) | Should message headers be preserved when publishing messages. This will add the Camel headers to the Iron MQ message as a json payload with a header list, and a message body. Useful when Camel is both consumer and producer. | false | boolean |
| **projectId** (common) | IronMQ projectId. |  | String |
| **batchDelete** (consumer) | Should messages be deleted in one batch. This will limit the number of api requests since messages are deleted in one request, instead of one per exchange. If enabled care should be taken that the consumer is idempotent when processing exchanges. | false | boolean |
| **concurrentConsumers** (consumer) | The number of concurrent consumers. | 1 | int |
| **maxMessagesPerPoll** (consumer) | Number of messages to poll per call. Maximum is 100. | 1 | int |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **timeout** (consumer) | After timeout (in seconds), item will be placed back onto the queue. | 60 | int |
| **wait** (consumer) | Time in seconds to wait for a message to become available. This enables long polling. Default is 0 (does not wait), maximum is 30. |  | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **visibilityDelay** (producer) | The item will not be available on the queue until this many seconds have passed. Default is 0 seconds. |  | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (advanced) | Reference to a io.iron.ironmq.Client in the Registry. |  | Client |
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
| **token** (security) | IronMQ token. |  | String |

## Message Headers

The IronMQ component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIronMQMessageId** (common) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-ironmq/latest/org/apache/camel/component/ironmq/IronMQConstants.html#MESSAGE_ID) | (producer) The id of the IronMQ message as a String when sending a single message, or a Ids object when sending a array of strings. (consumer) The id of the message. |  | Ids |
| **CamelIronMQReservationId** (consumer) Constant: [`MESSAGE_RESERVATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-ironmq/latest/org/apache/camel/component/ironmq/IronMQConstants.html#MESSAGE_RESERVATION_ID) | The reservation id of the message. |  | String |
| **CamelIronMQReservedCount** (consumer) Constant: [`MESSAGE_RESERVED_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-ironmq/latest/org/apache/camel/component/ironmq/IronMQConstants.html#MESSAGE_RESERVED_COUNT) | The number of times this message has been reserved. |  | long |
| **CamelIronMQOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ironmq/latest/org/apache/camel/component/ironmq/IronMQConstants.html#OPERATION) | If value set to 'CamelIronMQClearQueue' the queue is cleared of unconsumed messages. |  | String |

## Usage

### Message Body

It should be either a String or an array of Strings. In the latter case, the batch of strings will be sent to IronMQ as one request, creating one message per element in the array.

## Examples

### Consumer example

Consume 50 messages per poll from the queue `testqueue` on aws eu, and save the messages to files.

-   Java
    
-   XML
    
-   YAML
    

```java
from("ironmq:testqueue?ironMQCloud=https://mq-aws-eu-west-1-1.iron.io&projectId=myIronMQProjectid&token=myIronMQToken&maxMessagesPerPoll=50")
  .to("file:somefolder");
```

```xml
<route>
  <from uri="ironmq:testqueue?ironMQCloud=https://mq-aws-eu-west-1-1.iron.io&amp;projectId=myIronMQProjectid&amp;token=myIronMQToken&amp;maxMessagesPerPoll=50"/>
  <to uri="file:somefolder"/>
</route>
```

```yaml
- route:
    from:
      uri: ironmq:testqueue
      parameters:
        ironMQCloud: "https://mq-aws-eu-west-1-1.iron.io"
        projectId: myIronMQProjectid
        token: myIronMQToken
        maxMessagesPerPoll: 50
      steps:
        - to:
            uri: file:somefolder
```

### Producer example

Dequeue from activemq jms and enqueue the messages on IronMQ.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:foo")
  .to("ironmq:testqueue?projectId=myIronMQProjectid&token=myIronMQToken");
```

```xml
<route>
  <from uri="activemq:foo"/>
  <to uri="ironmq:testqueue?projectId=myIronMQProjectid&amp;token=myIronMQToken"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:foo
      steps:
        - to:
            uri: ironmq:testqueue
            parameters:
              projectId: myIronMQProjectid
              token: myIronMQToken
```

## Spring Boot Auto-Configuration

When using ironmq with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ironmq-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.ironmq.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.ironmq.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.ironmq.enabled** | Whether to enable auto configuration of the ironmq component. This is enabled by default. |  | Boolean |
| **camel.component.ironmq.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.ironmq.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.ironmq.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |