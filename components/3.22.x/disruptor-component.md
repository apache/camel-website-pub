# Disruptor

**Since Camel 2.12**

**Both producer and consumer are supported**

The Disruptor component provides asynchronous [SEDA](https://en.wikipedia.org/wiki/Staged_event-driven_architecture) behavior much as the standard SEDA Component, but utilizes a [Disruptor](https://github.com/LMAX-Exchange/disruptor) instead of a [BlockingQueue](http://docs.oracle.com/javase/1.5.0/docs/api/java/util/concurrent/BlockingQueue.md) utilized by the standard [SEDA](seda-component.md). Alternatively, a **disruptor-vm:** endpoint is supported by this component, providing an alternative to the standard [VM](vm-component.md).

The main advantage of choosing to use the Disruptor Component over the SEDA or the VM Component is performance in use cases where there is high contention between producer(s) and/or multicasted or concurrent Consumers. In those cases, significant increases of throughput and reduction of latency has been observed. Performance in scenarios without contention is comparable to the SEDA and VM Components.

The Disruptor is implemented with the intention of mimicing the behaviour and options of the SEDA and VM Components as much as possible. The main differences with the them are the following:

-   The buffer used is always bounded in size (default 1024 exchanges).
    
-   As a the buffer is always bouded, the default behaviour for the Disruptor is to block while the buffer is full instead of throwing an exception. This default behaviour may be configured on the component (see options).
    
-   The Disruptor enpoints don’t implement the BrowsableEndpoint interface. As such, the exchanges currently in the Disruptor can’t be retrieved, only the amount of exchanges.
    
-   The Disruptor requires its consumers (multicasted or otherwise) to be statically configured. Adding or removing consumers on the fly requires complete flushing of all pending exchanges in the Disruptor.
    
-   As a result of the reconfiguration: Data sent over a Disruptor is directly processed and 'gone' if there is at least one consumer, late joiners only get new exchanges published after they’ve joined.
    
-   The **pollTimeout** option is not supported by the Disruptor Component.
    
-   When a producer blocks on a full Disruptor, it does not respond to thread interrupts.
    

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-disruptor</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

 disruptor:someName\[?options\]

Where **someName** can be any string that uniquely identifies the endpoint within the current CamelContext.

## Options

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

The Disruptor component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bufferSize** (common) | To configure the ring buffer size. | 1024 | int |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **defaultConcurrentConsumers** (consumer) | To configure the default number of concurrent consumers. | 1 | int |
| **defaultMultipleConsumers** (consumer) | To configure the default value for multiple consumers. | false | boolean |
| **defaultWaitStrategy** (consumer) | 
To configure the default value for DisruptorWaitStrategy The default value is Blocking.

Enum values:

-   Blocking
    
-   Sleeping
    
-   BusySpin
    
-   Yielding
    





 | Blocking | DisruptorWaitStrategy |
| **defaultBlockWhenFull** (producer) | To configure the default value for block when full The default value is true. | true | boolean |
| **defaultProducerType** (producer) | 

To configure the default value for DisruptorProducerType The default value is Multi.

Enum values:

-   Single
    
-   Multi
    





 | Multi | DisruptorProducerType |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Disruptor endpoint is configured using URI syntax:

disruptor:name

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Name of queue. |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **size** (common) | The maximum capacity of the Disruptors ringbuffer Will be effectively increased to the nearest power of two. Notice: Mind if you use this option, then its the first endpoint being created with the queue name, that determines the size. To make sure all endpoints use same size, then configure the size option on all of them, or the first endpoint being created. | 1024 | int |
| **concurrentConsumers** (consumer) | Number of concurrent threads processing exchanges. | 1 | int |
| **multipleConsumers** (consumer) | Specifies whether multiple consumers are allowed. If enabled, you can use Disruptor for Publish-Subscribe messaging. That is, you can send a message to the queue and have each consumer receive a copy of the message. When enabled, this option should be specified on every consumer endpoint. | false | boolean |
| **waitStrategy** (consumer) | 
Defines the strategy used by consumer threads to wait on new exchanges to be published. The options allowed are:Blocking, Sleeping, BusySpin and Yielding.

Enum values:

-   Blocking
    
-   Sleeping
    
-   BusySpin
    
-   Yielding
    





 | Blocking | DisruptorWaitStrategy |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **blockWhenFull** (producer) | Whether a thread that sends messages to a full Disruptor will block until the ringbuffer’s capacity is no longer exhausted. By default, the calling thread will block and wait until the message can be accepted. By disabling this option, an exception will be thrown stating that the queue is full. | false | boolean |
| **producerType** (producer) | 

Defines the producers allowed on the Disruptor. The options allowed are: Multi to allow multiple producers and Single to enable certain optimizations only allowed when one concurrent producer (on one thread or otherwise synchronized) is active.

Enum values:

-   Single
    
-   Multi
    





 | Multi | DisruptorProducerType |
| **timeout** (producer) | Timeout (in milliseconds) before a producer will stop waiting for an asynchronous task to complete. You can disable timeout by using 0 or a negative value. | 30000 | long |
| **waitForTaskToComplete** (producer) | 

Option to specify whether the caller should wait for the async task to complete or not before continuing. The following three options are supported: Always, Never or IfReplyExpected. The first two values are self-explanatory. The last value, IfReplyExpected, will only wait if the message is Request Reply based.

Enum values:

-   Never
    
-   IfReplyExpected
    
-   Always
    





 | IfReplyExpected | WaitForTaskToComplete |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Wait strategies

The wait strategy effects the type of waiting performed by the consumer threads that are currently waiting for the next exchange to be published. The following strategies can be chosen:

  
| Name | Description | Advice |
| --- | --- | --- |
| Blocking | Blocking strategy that uses a lock and condition variable for Consumers waiting on a barrier. | This strategy can be used when throughput and low-latency are not as important as CPU resource. |
| Sleeping | Sleeping strategy that initially spins, then uses a Thread.yield(), and eventually for the minimum number of nanos the OS and JVM will allow while the Consumers are waiting on a barrier. | This strategy is a good compromise between performance and CPU resource. Latency spikes can occur after quiet periods. |
| BusySpin | Busy Spin strategy that uses a busy spin loop for Consumers waiting on a barrier. | This strategy will use CPU resource to avoid syscalls which can introduce latency jitter. It is best used when threads can be bound to specific CPU cores. |
| Yielding | Yielding strategy that uses a Thread.yield() for Consumers waiting on a barrier after an initially spinning. | This strategy is a good compromise between performance and CPU resource without incurring significant latency spikes. |

## Use of Request Reply

The Disruptor component supports using [Request Reply](eips/requestReply-eip.md), where the caller will wait for the Async route to complete. For instance:

```java
from("mina:tcp://0.0.0.0:9876?textline=true&sync=true").to("disruptor:input");
from("disruptor:input").to("bean:processInput").to("bean:createResponse");
```

In the route above, we have a TCP listener on port 9876 that accepts incoming requests. The request is routed to the _disruptor:input_ buffer. As it is a Request Reply message, we wait for the response. When the consumer on the _disruptor:input_ buffer is complete, it copies the response to the original message response.

## Concurrent consumers

By default, the Disruptor endpoint uses a single consumer thread, but you can configure it to use concurrent consumer threads. So instead of thread pools you can use:

```java
from("disruptor:stageName?concurrentConsumers=5").process(...)
```

As for the difference between the two, note a thread pool can increase/shrink dynamically at runtime depending on load, whereas the number of concurrent consumers is always fixed and supported by the Disruptor internally so performance will be higher.

## Thread pools

Be aware that adding a thread pool to a Disruptor endpoint by doing something like:

```java
from("disruptor:stageName").thread(5).process(...)
```

Can wind up with adding a normal [BlockingQueue](http://docs.oracle.com/javase/1.5.0/docs/api/java/util/concurrent/BlockingQueue.md) to be used in conjunction with the Disruptor, effectively negating part of the performance gains achieved by using the Disruptor. Instead, it is advices to directly configure number of threads that process messages on a Disruptor endpoint using the concurrentConsumers option.

## Sample

In the route below we use the Disruptor to send the request to this async queue to be able to send a fire-and-forget message for further processing in another thread, and return a constant reply in this thread to the original caller.

```java
public void configure() {
    from("direct:start")
        // send it to the disruptor that is async
        .to("disruptor:next")
        // return a constant response
        .transform(constant("OK"));

    from("disruptor:next").to("mock:result");
}
```

Here we send a Hello World message and expects the reply to be OK.

```java
Object out = template.requestBody("direct:start", "Hello World");
assertEquals("OK", out);
```

The "Hello World" message will be consumed from the Disruptor from another thread for further processing. Since this is from a unit test, it will be sent to a mock endpoint where we can do assertions in the unit test.

## Using multipleConsumers

In this example we have defined two consumers and registered them as spring beans.

```xml
<!-- define the consumers as spring beans -->
<bean id="consumer1" class="org.apache.camel.spring.example.FooEventConsumer"/>

<bean id="consumer2" class="org.apache.camel.spring.example.AnotherFooEventConsumer"/>

<camelContext xmlns="http://camel.apache.org/schema/spring">
    <!-- define a shared endpoint which the consumers can refer to instead of using url -->
    <endpoint id="foo" uri="disruptor:foo?multipleConsumers=true"/>
</camelContext>
```

Since we have specified multipleConsumers=true on the Disruptor foo endpoint we can have those two or more consumers receive their own copy of the message as a kind of pub-sub style messaging. As the beans are part of an unit test they simply send the message to a mock endpoint, but notice how we can use @Consume to consume from the Disruptor.

```java
public class FooEventConsumer {

    @EndpointInject("mock:result")
    private ProducerTemplate destination;

    @Consume(ref = "foo")
    public void doSomething(String body) {
        destination.sendBody("foo" + body);
    }

}
```

## Extracting disruptor information

If needed, information such as buffer size, etc. can be obtained without using JMX in this fashion:

```java
DisruptorEndpoint disruptor = context.getEndpoint("disruptor:xxxx");
int size = disruptor.getBufferSize();
```

## Spring Boot Auto-Configuration

When using disruptor with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-disruptor-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 20 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.disruptor-vm.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.disruptor-vm.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.disruptor-vm.buffer-size** | To configure the ring buffer size. | 1024 | Integer |
| **camel.component.disruptor-vm.default-block-when-full** | To configure the default value for block when full The default value is true. | true | Boolean |
| **camel.component.disruptor-vm.default-concurrent-consumers** | To configure the default number of concurrent consumers. | 1 | Integer |
| **camel.component.disruptor-vm.default-multiple-consumers** | To configure the default value for multiple consumers. | false | Boolean |
| **camel.component.disruptor-vm.default-producer-type** | To configure the default value for DisruptorProducerType The default value is Multi. |  | DisruptorProducerType |
| **camel.component.disruptor-vm.default-wait-strategy** | To configure the default value for DisruptorWaitStrategy The default value is Blocking. |  | DisruptorWaitStrategy |
| **camel.component.disruptor-vm.enabled** | Whether to enable auto configuration of the disruptor-vm component. This is enabled by default. |  | Boolean |
| **camel.component.disruptor-vm.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.disruptor.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.disruptor.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.disruptor.buffer-size** | To configure the ring buffer size. | 1024 | Integer |
| **camel.component.disruptor.default-block-when-full** | To configure the default value for block when full The default value is true. | true | Boolean |
| **camel.component.disruptor.default-concurrent-consumers** | To configure the default number of concurrent consumers. | 1 | Integer |
| **camel.component.disruptor.default-multiple-consumers** | To configure the default value for multiple consumers. | false | Boolean |
| **camel.component.disruptor.default-producer-type** | To configure the default value for DisruptorProducerType The default value is Multi. |  | DisruptorProducerType |
| **camel.component.disruptor.default-wait-strategy** | To configure the default value for DisruptorWaitStrategy The default value is Blocking. |  | DisruptorWaitStrategy |
| **camel.component.disruptor.enabled** | Whether to enable auto configuration of the disruptor component. This is enabled by default. |  | Boolean |
| **camel.component.disruptor.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |