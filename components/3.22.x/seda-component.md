# SEDA

**Since Camel 1.1**

**Both producer and consumer are supported**

The SEDA component provides asynchronous [SEDA](https://en.wikipedia.org/wiki/Staged_event-driven_architecture) behavior, so that messages are exchanged on a [BlockingQueue](http://java.sun.com/j2se/1.5.0/docs/api/java/util/concurrent/BlockingQueue.md) and consumers are invoked in a separate thread from the producer.

Note that queues are only visible within a _single_ CamelContext. If you want to communicate across `CamelContext` instances (for example, communicating between Web applications), see the [VM](vm-component.md) component.

This component does not implement any kind of persistence or recovery, if the VM terminates while messages are yet to be processed. If you need persistence, reliability or distributed SEDA, try using either [JMS](jms-component.md) or [ActiveMQ](jms-component.md).

> **Tip**
> **Synchronous**
>
> The [Direct](direct-component.md) component provides synchronous invocation of any consumers when a producer sends a message exchange.

## URI format

seda:someName\[?options\]

Where **someName** can be any string that uniquely identifies the endpoint within the current CamelContext.

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

The SEDA component supports 10 options, which are listed below.

   
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

The SEDA endpoint is configured using URI syntax:

seda:name

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

## Choosing BlockingQueue implementation

By default, the SEDA component always intantiates LinkedBlockingQueue, but you can use different implementation, you can reference your own BlockingQueue implementation, in this case the size option is not used

```xml
<bean id="arrayQueue" class="java.util.ArrayBlockingQueue">
  <constructor-arg index="0" value="10" ><!-- size -->
  <constructor-arg index="1" value="true" ><!-- fairness -->
</bean>

<!-- ... and later -->
<from>seda:array?queue=#arrayQueue</from>
```

Or you can reference a BlockingQueueFactory implementation, 3 implementations are provided LinkedBlockingQueueFactory, ArrayBlockingQueueFactory and PriorityBlockingQueueFactory:

```xml
<bean id="priorityQueueFactory" class="org.apache.camel.component.seda.PriorityBlockingQueueFactory">
  <property name="comparator">
    <bean class="org.apache.camel.demo.MyExchangeComparator" />
  </property>
</bean>

<!-- ... and later -->
<from>seda:priority?queueFactory=#priorityQueueFactory&size=100</from>
```

## Use of Request Reply

The [SEDA](#) component supports using Request Reply, where the caller will wait for the Async route to complete. For instance:

```java
from("mina:tcp://0.0.0.0:9876?textline=true&sync=true").to("seda:input");

from("seda:input").to("bean:processInput").to("bean:createResponse");
```

In the route above, we have a TCP listener on port 9876 that accepts incoming requests. The request is routed to the `seda:input` queue. As it is a Request Reply message, we wait for the response. When the consumer on the `seda:input` queue is complete, it copies the response to the original message response.

## Concurrent consumers

By default, the SEDA endpoint uses a single consumer thread, but you can configure it to use concurrent consumer threads. So instead of thread pools you can use:

```java
from("seda:stageName?concurrentConsumers=5").process(...)
```

As for the difference between the two, note a _thread pool_ can increase/shrink dynamically at runtime depending on load, whereas the number of concurrent consumers is always fixed.

## Thread pools

Be aware that adding a thread pool to a SEDA endpoint by doing something like:

```java
from("seda:stageName").thread(5).process(...)
```

Can wind up with two `BlockQueues`: one from the SEDA endpoint, and one from the workqueue of the thread pool, which may not be what you want. Instead, you might wish to configure a [Direct](direct-component.md) endpoint with a thread pool, which can process messages both synchronously and asynchronously. For example:

```java
from("direct:stageName").thread(5).process(...)
```

You can also directly configure number of threads that process messages on a SEDA endpoint using the `concurrentConsumers` option.

## Sample

In the route below we use the SEDA queue to send the request to this async queue to be able to send a fire-and-forget message for further processing in another thread, and return a constant reply in this thread to the original caller.

We send a Hello World message and expects the reply to be OK.

```java
    @Test
    public void testSendAsync() throws Exception {
        MockEndpoint mock = getMockEndpoint("mock:result");
        mock.expectedBodiesReceived("Hello World");

        // START SNIPPET: e2
        Object out = template.requestBody("direct:start", "Hello World");
        assertEquals("OK", out);
        // END SNIPPET: e2

        MockEndpoint.assertIsSatisfied(context);
    }

    @Override
    protected RouteBuilder createRouteBuilder() throws Exception {
        return new RouteBuilder() {
            // START SNIPPET: e1
            public void configure() throws Exception {
                from("direct:start")
                    // send it to the seda queue that is async
                    .to("seda:next")
                    // return a constant response
                    .transform(constant("OK"));

                from("seda:next").to("mock:result");
            }
            // END SNIPPET: e1
        };
    }
```

The "Hello World" message will be consumed from the SEDA queue from another thread for further processing. Since this is from a unit test, it will be sent to a `mock` endpoint where we can do assertions in the unit test.

## Using multipleConsumers

In this example we have defined two consumers.

```java
    @Test
    public void testSameOptionsProducerStillOkay() throws Exception {
        getMockEndpoint("mock:foo").expectedBodiesReceived("Hello World");
        getMockEndpoint("mock:bar").expectedBodiesReceived("Hello World");

        template.sendBody("seda:foo", "Hello World");

        MockEndpoint.assertIsSatisfied(context);
    }

    @Override
    protected RouteBuilder createRouteBuilder() throws Exception {
        return new RouteBuilder() {
            @Override
            public void configure() throws Exception {
                from("seda:foo?multipleConsumers=true").routeId("foo").to("mock:foo");
                from("seda:foo?multipleConsumers=true").routeId("bar").to("mock:bar");
            }
        };
    }
```

Since we have specified **multipleConsumers=true** on the seda foo endpoint we can have those two consumers receive their own copy of the message as a kind of pub-sub style messaging.

As the beans are part of an unit test they simply send the message to a mock endpoint.

## Extracting queue information.

If needed, information such as queue size, etc. can be obtained without using JMX in this fashion:

```java
SedaEndpoint seda = context.getEndpoint("seda:xxxx");
int size = seda.getExchanges().size();
```

## Spring Boot Auto-Configuration

When using seda with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-seda-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.seda.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.seda.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.seda.concurrent-consumers** | Sets the default number of concurrent threads processing exchanges. | 1 | Integer |
| **camel.component.seda.default-block-when-full** | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will instead block and wait until the message can be accepted. | false | Boolean |
| **camel.component.seda.default-discard-when-full** | Whether a thread that sends messages to a full SEDA queue will be discarded. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will give up sending and continue, meaning that the message was not sent to the SEDA queue. | false | Boolean |
| **camel.component.seda.default-offer-timeout** | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, where a configured timeout can be added to the block case. Utilizing the .offer(timeout) method of the underlining java queue. |  | Long |
| **camel.component.seda.default-poll-timeout** | The timeout (in milliseconds) used when polling. When a timeout occurs, the consumer can check whether it is allowed to continue running. Setting a lower value allows the consumer to react more quickly upon shutdown. | 1000 | Integer |
| **camel.component.seda.default-queue-factory** | Sets the default queue factory. The option is a org.apache.camel.component.seda.BlockingQueueFactory<org.apache.camel.Exchange> type. |  | BlockingQueueFactory |
| **camel.component.seda.enabled** | Whether to enable auto configuration of the seda component. This is enabled by default. |  | Boolean |
| **camel.component.seda.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.seda.queue-size** | Sets the default maximum capacity of the SEDA queue (i.e., the number of messages it can hold). | 1000 | Integer |