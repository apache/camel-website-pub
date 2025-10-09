# VM

> **Warning**
> **Deprecated:** This vm is deprecated and may be removed in a future release.

**Since Camel 1.1**

**Both producer and consumer are supported**

The VM component provides asynchronous [SEDA](https://en.wikipedia.org/wiki/Staged_event-driven_architecture) behavior, exchanging messages on a [BlockingQueue](http://java.sun.com/j2se/1.5.0/docs/api/java/util/concurrent/BlockingQueue.md) and invoking consumers in a separate thread pool.

This component differs from the [Seda](seda-component.md) component in that VM supports communication across CamelContext instances - so you can use this mechanism to communicate across web applications (provided that `camel-core.jar` is on the `system/boot` classpath).

VM is an extension to the [Seda](seda-component.md) component.

## URI format

vm:queueName\[?options\]

Where **`queueName`** can be any string to uniquely identify the endpoint within the JVM (or at least within the classloader that loaded camel-core.jar)

It is sufficient to list all the options for a consumer endpoint only.

```java
from("direct:foo").to("vm:bar");

from("vm:bar?concurrentConsumers=5").to("file://output");
```

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The VM component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **concurrentConsumers** (consumer) | Sets the default number of concurrent threads processing exchanges. | 1 | int |
| **defaultPollTimeout** (consumer (advanced)) | The timeout (in milliseconds) used when polling. When a timeout occurs, the consumer can check whether it is allowed to continue running. Setting a lower value allows the consumer to react more quickly upon shutdown. | 1000 | int |
| **defaultBlockWhenFull** (producer) | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will instead block and wait until the message can be accepted. | false | boolean |
| **defaultDiscardWhenFull** (producer) | Whether a thread that sends messages to a full SEDA queue will be discarded. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will give up sending and continue, meaning that the message was not sent to the SEDA queue. | false | boolean |
| **defaultOfferTimeout** (producer) | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, where a configured timeout can be added to the block case. Utilizing the .offer(timeout) method of the underlining java queue. |  | long |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **defaultQueueFactory** (advanced) | Sets the default queue factory. |  | BlockingQueueFactory |
| **queueSize** (advanced) | Sets the default maximum capacity of the SEDA queue (i.e., the number of messages it can hold). | 1000 | int |

## Endpoint Options

The VM endpoint is configured using URI syntax:

vm:name

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Name of queue. |  | String |

### Query Parameters (18 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **size** (common) | The maximum capacity of the SEDA queue (i.e., the number of messages it can hold). Will by default use the defaultSize set on the SEDA component. | 1000 | int |
| **concurrentConsumers** (consumer) | Number of concurrent threads processing exchanges. | 1 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **limitConcurrentConsumers** (consumer (advanced)) | Whether to limit the number of concurrentConsumers to the maximum of 500. By default, an exception will be thrown if an endpoint is configured with a greater number. You can disable that check by turning this option off. | true | boolean |
| **multipleConsumers** (consumer (advanced)) | Specifies whether multiple consumers are allowed. If enabled, you can use SEDA for Publish-Subscribe messaging. That is, you can send a message to the SEDA queue and have each consumer receive a copy of the message. When enabled, this option should be specified on every consumer endpoint. | false | boolean |
| **pollTimeout** (consumer (advanced)) | The timeout (in milliseconds) used when polling. When a timeout occurs, the consumer can check whether it is allowed to continue running. Setting a lower value allows the consumer to react more quickly upon shutdown. | 1000 | int |
| **purgeWhenStopping** (consumer (advanced)) | Whether to purge the task queue when stopping the consumer/route. This allows to stop faster, as any pending messages on the queue is discarded. | false | boolean |
| **blockWhenFull** (producer) | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will instead block and wait until the message can be accepted. | false | boolean |
| **discardIfNoConsumers** (producer) | Whether the producer should discard the message (do not add the message to the queue), when sending to a queue with no active consumers. Only one of the options discardIfNoConsumers and failIfNoConsumers can be enabled at the same time. | false | boolean |
| **discardWhenFull** (producer) | Whether a thread that sends messages to a full SEDA queue will be discarded. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will give up sending and continue, meaning that the message was not sent to the SEDA queue. | false | boolean |
| **failIfNoConsumers** (producer) | Whether the producer should fail by throwing an exception, when sending to a queue with no active consumers. Only one of the options discardIfNoConsumers and failIfNoConsumers can be enabled at the same time. | false | boolean |
| **offerTimeout** (producer) | Offer timeout (in milliseconds) can be added to the block case when queue is full. You can disable timeout by using 0 or a negative value. |  | long |
| **timeout** (producer) | Timeout (in milliseconds) before a SEDA producer will stop waiting for an asynchronous task to complete. You can disable timeout by using 0 or a negative value. | 30000 | long |
| **waitForTaskToComplete** (producer) | 

Option to specify whether the caller should wait for the async task to complete or not before continuing. The following three options are supported: Always, Never or IfReplyExpected. The first two values are self-explanatory. The last value, IfReplyExpected, will only wait if the message is Request Reply based. The default option is IfReplyExpected.

Enum values:

-   Never
    
-   IfReplyExpected
    
-   Always
    





 | IfReplyExpected | WaitForTaskToComplete |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **queue** (advanced) | Define the queue instance which will be used by the endpoint. |  | BlockingQueue |

See the [Seda](seda-component.md) component for options and other important usage details as the same rules apply to the [Vm](#) component.

## Samples

In the route below we send exchanges across CamelContext instances to a VM queue named `order.email`:

```java
from("direct:in").bean(MyOrderBean.class).to("vm:order.email");
```

And then we receive exchanges in some other Camel context (such as deployed in another `.war` application):

```java
from("vm:order.email").bean(MyOrderEmailSender.class);
```

## Spring Boot Auto-Configuration

When using vm with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-vm-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.vm.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.vm.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.vm.concurrent-consumers** | Sets the default number of concurrent threads processing exchanges. | 1 | Integer |
| **camel.component.vm.default-block-when-full** | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will instead block and wait until the message can be accepted. | false | Boolean |
| **camel.component.vm.default-discard-when-full** | Whether a thread that sends messages to a full SEDA queue will be discarded. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will give up sending and continue, meaning that the message was not sent to the SEDA queue. | false | Boolean |
| **camel.component.vm.default-offer-timeout** | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, where a configured timeout can be added to the block case. Utilizing the .offer(timeout) method of the underlining java queue. |  | Long |
| **camel.component.vm.default-poll-timeout** | The timeout (in milliseconds) used when polling. When a timeout occurs, the consumer can check whether it is allowed to continue running. Setting a lower value allows the consumer to react more quickly upon shutdown. | 1000 | Integer |
| **camel.component.vm.default-queue-factory** | Sets the default queue factory. The option is a org.apache.camel.component.seda.BlockingQueueFactory<org.apache.camel.Exchange> type. |  | BlockingQueueFactory |
| **camel.component.vm.enabled** | Whether to enable auto configuration of the vm component. This is enabled by default. |  | Boolean |
| **camel.component.vm.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.vm.queue-size** | Sets the default maximum capacity of the SEDA queue (i.e., the number of messages it can hold). | 1000 | Integer |