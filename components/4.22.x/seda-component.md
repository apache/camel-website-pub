# SEDA

**Since Camel 1.1**

**Both producer and consumer are supported**

The SEDA component provides asynchronous [SEDA](https://en.wikipedia.org/wiki/Staged_event-driven_architecture) behavior, so that messages are exchanged on a [BlockingQueue](http://java.sun.com/j2se/1.5.0/docs/api/java/util/concurrent/BlockingQueue.md) and consumers are invoked in a separate thread from the producer.

Note that queues are only visible within the same CamelContext.

> **Note**
> This component does not implement any kind of persistence or recovery if the JVM terminates while messages are yet to be processed. If you need persistence, reliability or distributed SEDA, try using [JMS](jms-component.md).

> **Tip**
> **Synchronous**
>
> The [Direct](direct-component.md) component provides synchronous invocation (uses no threading; it directly invokes the consumer when sending) of any consumers when a producer sends a message exchange.

## URI format

seda:someId\[?options\]

Where _someId_ can be any string that uniquely identifies the endpoint within the current CamelContext.

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

The SEDA component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **concurrentConsumers** (consumer) | Sets the default number of concurrent threads processing exchanges. | 1 | int |
| **defaultPollTimeout** (consumer (advanced)) | The timeout (in milliseconds) used when polling. When a timeout occurs, the consumer can check whether it is allowed to continue running. Setting a lower value allows the consumer to react more quickly upon shutdown. | 1000 | int |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **defaultBlockWhenFull** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will instead block and wait until the message can be accepted. | false | boolean |
| **defaultDiscardWhenFull** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will be discarded. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will give up sending and continue, meaning that the message was not sent to the SEDA queue. | false | boolean |
| **defaultOfferTimeout** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, where a configured timeout can be added to the block case. Using the offer(timeout) method of the underlining java queue. |  | long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **defaultQueueFactory** (advanced) | Sets the default queue factory. |  | BlockingQueueFactory |
| **queueSize** (advanced) | Sets the default maximum capacity of the SEDA queue (i.e., the number of messages it can hold). | 1000 | int |

## Endpoint Options

The SEDA endpoint is configured using URI syntax:

seda:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Name of queue. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **size** (common) | The maximum capacity of the SEDA queue (i.e., the number of messages it can hold). Will by default use the queueSize set on the SEDA component. | 1000 | int |
| **concurrentConsumers** (consumer) | Number of concurrent threads processing exchanges. When virtualThreadPerTask is enabled, this becomes a concurrency limit (0 = unlimited) and defaults to 0 instead of 1. | 1 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **limitConcurrentConsumers** (consumer (advanced)) | Whether to limit the number of concurrentConsumers to the maximum of 500. By default, an exception will be thrown if an endpoint is configured with a greater number. You can disable that check by turning this option off. | true | boolean |
| **multipleConsumers** (consumer (advanced)) | Specifies whether multiple consumers are allowed. If enabled, you can use SEDA for Publish-Subscribe messaging. That is, you can send a message to the SEDA queue and have each consumer receive a copy of the message. When enabled, this option should be specified on every consumer endpoint. | false | boolean |
| **pollTimeout** (consumer (advanced)) | The timeout (in milliseconds) used when polling. When a timeout occurs, the consumer can check whether it is allowed to continue running. Setting a lower value allows the consumer to react more quickly upon shutdown. | 1000 | int |
| **purgeWhenStopping** (consumer (advanced)) | Whether to purge the task queue when stopping the consumer/route. This allows to stop faster, as any pending messages on the queue is discarded. | false | boolean |
| **virtualThreadPerTask** (consumer (advanced)) | If enabled, spawns a new virtual thread for each message instead of using a fixed pool of consumer threads. This model is optimized for virtual threads (JDK 21) and I/O-bound workloads where creating threads is cheap. The concurrentConsumers option becomes a limit on max concurrent tasks (0 = unlimited). Requires virtual threads to be enabled via camel.threads.virtual.enabled=true. | false | boolean |
| **timeout** (producer) | Timeout before a SEDA producer will stop waiting for an asynchronous task to complete. You can disable timeout by using 0 or a negative value. | 30000 | long |
| **waitForTaskToComplete** (producer) | 

Option to specify whether the caller should wait for the async task to complete or not before continuing. The following three options are supported: Always, Never or IfReplyExpected. The first two values are self-explanatory. The last value, IfReplyExpected, will only wait if the message is Request Reply based. The default option is IfReplyExpected.

Enum values:

-   Never
    
-   IfReplyExpected
    
-   Always
    





 | IfReplyExpected | WaitForTaskToComplete |
| **blockWhenFull** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will instead block and wait until the message can be accepted. | false | boolean |
| **discardIfNoConsumers** (producer (advanced)) | Whether the producer should discard the message (do not add the message to the queue), when sending to a queue with no active consumers. Only one of the options discardIfNoConsumers and failIfNoConsumers can be enabled at the same time. | false | boolean |
| **discardWhenFull** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will be discarded. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will give up sending and continue, meaning that the message was not sent to the SEDA queue. | false | boolean |
| **failIfNoConsumers** (producer (advanced)) | Whether the producer should fail by throwing an exception, when sending to a queue with no active consumers. Only one of the options discardIfNoConsumers and failIfNoConsumers can be enabled at the same time. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **offerTimeout** (producer (advanced)) | Offer timeout can be added to the block case when queue is full. You can disable timeout by using 0 or a negative value. |  | long |
| **browseLimit** (advanced) | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | int |
| **queue** (advanced) | Define the queue instance which will be used by the endpoint. |  | BlockingQueue |

## Usage

### Choosing BlockingQueue implementation

By default, the SEDA component always instantiates a `LinkedBlockingQueue`, but you can use different implementation, you can reference your own `BlockingQueue` implementation, in this case the size option is not used:

_XML-only: Spring bean definition for custom BlockingQueue_

```xml
<bean id="arrayQueue" class="java.util.ArrayBlockingQueue">
  <constructor-arg index="0" value="10" /><!-- size -->
  <constructor-arg index="1" value="true" /><!-- fairness -->
</bean>

<!-- ... and later -->
<from>seda:array?queue=#arrayQueue</from>
```

You can also reference a `BlockingQueueFactory` implementation. Three implementations are provided:

-   `LinkedBlockingQueueFactory`
    
-   `ArrayBlockingQueueFactory`
    
-   `PriorityBlockingQueueFactory`
    

_XML-only: Spring bean definition for custom BlockingQueueFactory_

```xml
<bean id="priorityQueueFactory" class="org.apache.camel.component.seda.PriorityBlockingQueueFactory">
  <property name="comparator">
    <bean class="org.apache.camel.demo.MyExchangeComparator" />
  </property>
</bean>

<!-- ... and later -->
<from>seda:priority?queueFactory=#priorityQueueFactory&size=100</from>
```

### Use of Request Reply

The [SEDA](#) component supports using Request Reply, where the caller will wait for the Async route to complete. For instance:

-   Java
    
-   XML
    
-   YAML
    

```java
from("mina:tcp://0.0.0.0:9876?textline=true&sync=true").to("seda:input");

from("seda:input").to("bean:processInput").to("bean:createResponse");
```

```xml
<route>
  <from uri="mina:tcp://0.0.0.0:9876?textline=true&amp;sync=true"/>
  <to uri="seda:input"/>
</route>
<route>
  <from uri="seda:input"/>
  <to uri="bean:processInput"/>
  <to uri="bean:createResponse"/>
</route>
```

```yaml
- route:
    from:
      uri: mina:tcp://0.0.0.0:9876
      parameters:
        textline: true
        sync: true
      steps:
        - to:
            uri: seda:input
- route:
    from:
      uri: seda:input
      steps:
        - to:
            uri: bean:processInput
        - to:
            uri: bean:createResponse
```

In the route above, we have a TCP listener on port 9876 that accepts incoming requests. The request is routed to the `seda:input` queue. As it is a Request Reply message, we wait for the response. When the consumer on the `seda:input` queue is complete, it copies the response to the original message response.

### Concurrent consumers

By default, the SEDA endpoint uses a single consumer thread, but you can configure it to use concurrent consumer threads. So instead of thread pools, you can use:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:stageName?concurrentConsumers=5").process(...)
```

```xml
<from uri="seda:stageName?concurrentConsumers=5"/>
```

```yaml
from:
  uri: seda:stageName
  parameters:
    concurrentConsumers: 5
```

As for the difference between the two, note a _thread pool_ can increase/shrink dynamically at runtime depending on load, whereas the number of concurrent consumers is always fixed.

### Thread pools

Be aware that adding a thread pool to a SEDA endpoint by doing something like:

_Java-only: thread pool added to SEDA endpoint_

```java
from("seda:stageName").thread(5).process(...)
```

Can wind up with two `BlockQueues`: one from the SEDA endpoint, and one from the work queue of the thread pool, which may not be what you want. Instead, you might wish to configure a [Direct](direct-component.md) endpoint with a thread pool, which can process messages both synchronously and asynchronously. For example:

_Java-only: thread pool on a Direct endpoint_

```java
from("direct:stageName").thread(5).process(...)
```

You can also directly configure number of threads that process messages on a SEDA endpoint using the `concurrentConsumers` option.

## Examples

In the route below, we use the SEDA queue to send the request to this async queue. As such, it is able to send a _fire-and-forget_ message for further processing in another thread, and return a constant reply in this thread to the original caller.

We send a _Hello World_ message and expect the reply to be _OK_.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("seda:next")
    .transform(constant("OK"));

from("seda:next").to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="seda:next"/>
  <transform>
    <constant>OK</constant>
  </transform>
</route>
<route>
  <from uri="seda:next"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: seda:next
        - transform:
            constant: "OK"
- route:
    from:
      uri: seda:next
      steps:
        - to:
            uri: mock:result
```

The _Hello World_ message will be consumed from the SEDA queue from another thread for further processing. Since this is from a unit test, it will be sent to a `mock` endpoint where we can do assertions in the unit test.

### Using multipleConsumers

In this example, we have defined two consumers.

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:foo?multipleConsumers=true").routeId("foo").to("mock:foo");
from("seda:foo?multipleConsumers=true").routeId("bar").to("mock:bar");
```

```xml
<route id="foo">
  <from uri="seda:foo?multipleConsumers=true"/>
  <to uri="mock:foo"/>
</route>
<route id="bar">
  <from uri="seda:foo?multipleConsumers=true"/>
  <to uri="mock:bar"/>
</route>
```

```yaml
- route:
    id: foo
    from:
      uri: seda:foo
      parameters:
        multipleConsumers: true
      steps:
        - to:
            uri: mock:foo
- route:
    id: bar
    from:
      uri: seda:foo
      parameters:
        multipleConsumers: true
      steps:
        - to:
            uri: mock:bar
```

Since we have specified `multipleConsumers=true` on the seda `foo` endpoint we can have those two consumers receive their own copy of the message as a kind of _publish/subscribe_ style messaging.

### Extracting queue information.

If needed, information such as queue size, etc. can be obtained without using JMX in this fashion:

_Java-only: programmatic access to `SedaEndpoint` internals_

```java
SedaEndpoint seda = context.getEndpoint("seda:xxxx");
int size = seda.getExchanges().size();
```