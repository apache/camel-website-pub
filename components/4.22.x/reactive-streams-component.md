# Reactive Streams

**Since Camel 2.19**

**Both producer and consumer are supported**

The Reactive Streams component allows you to exchange messages with reactive stream processing libraries compatible with the [reactive streams](http://www.reactive-streams.org/) standard.

The component supports backpressure and has been tested using the [reactive streams technology compatibility kit (TCK)](https://github.com/reactive-streams/reactive-streams-jvm/tree/master/tck).

The Camel module provides a **reactive-streams** component that allows users to define incoming and outgoing streams within Camel routes, and a direct client API that allows using Camel endpoints directly into any external reactive framework.

Camel uses an internal implementation of the reactive streams _Publisher_ and _Subscriber_, so it’s not tied to any specific framework. The following reactive frameworks have been used in the integration tests: [Reactor Core 3](https://github.com/reactor/reactor-core), [RxJava 2](https://github.com/ReactiveX/RxJava).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-reactive-streams</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

reactive-streams://stream?\[options\]

Where **stream** is a logical stream name used to bind Camel routes to the external stream processing systems.

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

The Reactive Streams component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **threadPoolMaxSize** (common) | The maximum number of threads used by the reactive streams internal engine. | 10 | int |
| **threadPoolMinSize** (common) | The minimum number of threads used by the reactive streams internal engine. |  | int |
| **threadPoolName** (common) | The name of the thread pool used by the reactive streams internal engine. | CamelReactiveStreamsWorker | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **backpressureStrategy** (producer) | 
The backpressure strategy to use when pushing events to a slow subscriber.

Enum values:

-   BUFFER
    
-   OLDEST
    
-   LATEST
    





 | BUFFER | ReactiveStreamsBackpressureStrategy |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **reactiveStreamsEngineConfiguration** (advanced) | To use an existing reactive stream engine configuration. |  | ReactiveStreamsEngineConfiguration |
| **serviceType** (advanced) | Set the type of the underlying reactive streams implementation to use. The implementation is looked up from the registry or using a ServiceLoader, the default implementation is DefaultCamelReactiveStreamsService. |  | String |

## Endpoint Options

The Reactive Streams endpoint is configured using URI syntax:

reactive-streams:stream

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **stream** (common) | Name of the stream channel used by the endpoint to exchange messages. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **concurrentConsumers** (consumer) | Number of threads used to process exchanges in the Camel route. | 1 | int |
| **exchangesRefillLowWatermark** (consumer) | Set the low watermark of requested exchanges to the active subscription as percentage of the maxInflightExchanges. When the number of pending items from the upstream source is lower than the watermark, new items can be requested to the subscription. If set to 0, the subscriber will request items in batches of maxInflightExchanges, only after all items of the previous batch have been processed. If set to 1, the subscriber can request a new item each time an exchange is processed (chatty). Any intermediate value can be used. | 0.25 | double |
| **forwardOnComplete** (consumer) | Determines if onComplete events should be pushed to the Camel route. | false | boolean |
| **forwardOnError** (consumer) | Determines if onError events should be pushed to the Camel route. Exceptions will be set as message body. | false | boolean |
| **maxInflightExchanges** (consumer) | Maximum number of exchanges concurrently being processed by Camel. This parameter controls backpressure on the stream. Setting a non-positive value will disable backpressure. | 128 | Integer |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **backpressureStrategy** (producer) | 

The backpressure strategy to use when pushing events to a slow subscriber.

Enum values:

-   BUFFER
    
-   OLDEST
    
-   LATEST
    





 |  | ReactiveStreamsBackpressureStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Reactive Streams component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelReactiveStreamsEventType** (consumer) Constant: [`REACTIVE_STREAMS_EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-reactive-streams/latest/org/apache/camel/component/reactive/streams/ReactiveStreamsConstants.html#REACTIVE_STREAMS_EVENT_TYPE) | Every exchange consumed by Camel has this header set to indicate if the exchange contains an item (value=onNext), an error (value=onError) or a completion event (value=onComplete). Errors and completion notification are not forwarded by default. |  | String |
| **CamelReactiveStreamsCallback** (common) Constant: [`REACTIVE_STREAMS_CALLBACK`](https://javadoc.io/doc/org.apache.camel/camel-reactive-streams/latest/org/apache/camel/component/reactive/streams/ReactiveStreamsConstants.html#REACTIVE_STREAMS_CALLBACK) | The callback. |  | DispatchCallback |

## Usage

The library is aimed to support all the communication modes needed by an application to interact with Camel data:

-   **Get** data from Camel routes (In-Only from Camel)
    
-   **Send** data to Camel routes (In-Only towards Camel)
    
-   **Request** a transformation to a Camel route (In-Out towards Camel)
    
-   **Process** data flowing from a Camel route using a reactive processing step (In-Out from Camel)
    

### Getting data from Camel

To subscribe to data flowing from a Camel route, exchanges should be redirected to a named stream, like in the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer:clock")
    .setBody().header(Exchange.TIMER_COUNTER)
    .to("reactive-streams:numbers");
```

```xml
<route>
  <from uri="timer:clock"/>
  <setBody>
    <header>CamelTimerCounter</header>
  </setBody>
  <to uri="reactive-streams:numbers"/>
</route>
```

```yaml
- route:
    from:
      uri: timer:clock
      steps:
        - setBody:
            header: CamelTimerCounter
        - to:
            uri: reactive-streams:numbers
```

In the example, an unbounded stream of numbers is associated to the name `numbers`. The stream can be accessed using the `CamelReactiveStreams` utility class.

_Java-only: `CamelReactiveStreamsService` API to obtain a Publisher from a named stream_

```java
CamelReactiveStreamsService camel = CamelReactiveStreams.get(context);

// Getting a stream of exchanges
Publisher<Exchange> exchanges = camel.fromStream("numbers");

// Getting a stream of Integers (using Camel standard conversion system)
Publisher<Integer> numbers = camel.fromStream("numbers", Integer.class);
```

The stream can be used easily with any reactive streams compatible library. Here is an example of how to use it with [RxJava 2](https://github.com/ReactiveX/RxJava) (although any reactive framework can be used to process events).

_Java-only: RxJava `Flowable` consuming Camel stream_

```java
Flowable.fromPublisher(numbers)
    .doOnNext(System.out::println)
    .subscribe();
```

The example prints all numbers generated by Camel into `System.out`.

#### Getting data from Camel using the direct API

For short Camel routes and for users that prefer defining the whole processing flow using functional constructs of the reactive framework (without using the Camel DSL at all), streams can also be defined using Camel URIs.

_Java-only: direct API to create a reactive Publisher from a Camel endpoint URI_

```java
CamelReactiveStreamsService camel = CamelReactiveStreams.get(context);

// Get a stream from all the files in a directory
Publisher<String> files = camel.from("file:folder", String.class);

// Use the stream in RxJava
Flowable.fromPublisher(files)
    .doOnNext(System.out::println)
    .subscribe();
```

### Sending data to Camel

When an external library needs to push events into a Camel route, the Reactive Streams endpoint must be set as consumer.

-   Java
    
-   XML
    
-   YAML
    

```java
from("reactive-streams:elements")
  .to("log:INFO");
```

```xml
<route>
  <from uri="reactive-streams:elements"/>
  <to uri="log:INFO"/>
</route>
```

```yaml
- route:
    from:
      uri: reactive-streams:elements
      steps:
        - to:
            uri: log:INFO
```

A handle to the `elements` stream can be obtained from the `CamelReactiveStreams` utility class.

_Java-only: obtaining a reactive `Subscriber` handle to push events into a Camel route_

```java
CamelReactiveStreamsService camel = CamelReactiveStreams.get(context);

Subscriber<String> elements = camel.streamSubscriber("elements", String.class);
```

The subscriber can be used to push events to the Camel route that consumes from the `elements` stream.

Here is an example of how to use it with [RxJava 2](https://github.com/ReactiveX/RxJava) (although any reactive framework can be used to publish events).

_Java-only: RxJava `Flowable` publishing events into a Camel subscriber_

```java
Flowable.interval(1, TimeUnit.SECONDS)
    .map(i -> "Item " + i)
    .subscribe(elements);
```

String items are generated every second by RxJava in the example, and they are pushed into the Camel route defined above.

#### Sending data to Camel using the direct API

Also in this case, the direct API can be used to obtain a Camel subscriber from an endpoint URI.

_Java-only: direct API to push data into a Camel endpoint using RxJava_

```java
CamelReactiveStreamsService camel = CamelReactiveStreams.get(context);

// Send two strings to the "seda:queue" endpoint
Flowable.just("hello", "world")
    .subscribe(camel.subscriber("seda:queue", String.class));
```

### Request a transformation to Camel

Routes defined in some Camel DSL can be used within a reactive stream framework to perform a specific transformation. The same mechanism can be also used to e.g., send data to an _http_ endpoint and continue.

The following snippet shows how RxJava functional code can request the task of loading and marshalling files to Camel.

_Java-only: RxJava requesting a transformation from a Camel reactive stream_

```java
CamelReactiveStreamsService camel = CamelReactiveStreams.get(context);

// Process files starting from their names
Flowable.just(new File("file1.txt"), new File("file2.txt"))
    .flatMap(file -> camel.toStream("readAndMarshal", String.class))
    // Camel output will be converted to String
    // other steps
    .subscribe();
```

In order this to work, a route like the following should be defined in the Camel context:

-   Java
    
-   XML
    
-   YAML
    

```java
from("reactive-streams:readAndMarshal")
    .marshal() // ... other details
```

```xml
<route>
  <from uri="reactive-streams:readAndMarshal"/>
  <marshal>
    <!-- ... other details -->
  </marshal>
</route>
```

```yaml
- route:
    from:
      uri: reactive-streams:readAndMarshal
      steps:
        - marshal: {}
```

#### Request a transformation to Camel using the direct API

An alternative approach consists of using the URI endpoints directly in the reactive flow:

_Java-only: direct API using `to()` to invoke a Camel endpoint from RxJava_

```java
CamelReactiveStreamsService camel = CamelReactiveStreams.get(context);

// Process files starting from their names
Flowable.just(new File("file1.txt"), new File("file2.txt"))
    .flatMap(file -> camel.to("direct:process", String.class))
    // Camel output will be converted to String
    // other steps
    .subscribe();
```

When using the `to()` method instead of the `toStream`, there is no need to define the route using `reactive-streams:` endpoints (although they are used under the hood).

In this case, the Camel transformation can be just:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:process")
    .marshal() // ... other details
```

```xml
<route>
  <from uri="direct:process"/>
  <marshal>
    <!-- ... other details -->
  </marshal>
</route>
```

```yaml
- route:
    from:
      uri: direct:process
      steps:
        - marshal: {}
```

### Process Camel data into the reactive framework

While a reactive streams _Publisher_ allows exchanging data in a unidirectional way, Camel routes often use an in-out exchange pattern (e.g., to define REST endpoints and, in general, where a reply is needed for each request).

In these circumstances, users can add a reactive processing step to the flow, to enhance a Camel route or to define the entire transformation using the reactive framework.

For example, given the following route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer:clock")
    .setBody().header(Exchange.TIMER_COUNTER)
    .to("direct:reactive")
    .log("Continue with Camel route... n=${body}");
```

```xml
<route>
  <from uri="timer:clock"/>
  <setBody>
    <header>CamelTimerCounter</header>
  </setBody>
  <to uri="direct:reactive"/>
  <log message="Continue with Camel route... n=${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: timer:clock
      steps:
        - setBody:
            header: CamelTimerCounter
        - to:
            uri: direct:reactive
        - log:
            message: "Continue with Camel route... n=${body}"
```

A reactive processing step can be associated with the "direct:reactive" endpoint:

_Java-only: reactive processing step using \`CamelReactiveStreamsService.process()\`_

```java
CamelReactiveStreamsService camel = CamelReactiveStreams.get(context);

camel.process("direct:reactive", Integer.class, items ->
    Flowable.fromPublisher(items) // RxJava
        .map(n -> -n)); // make every number negative
```

Data flowing in the Camel route will be processed by the external reactive framework then continue the processing flow inside Camel.

This mechanism can also be used to define a In-Out exchange in a completely reactive way.

_Java-only: defining a REST endpoint entirely via reactive processing_

```java
CamelReactiveStreamsService camel = CamelReactiveStreams.get(context);

// requires a rest-capable Camel component
camel.process("rest:get:orders", exchange ->
        Flowable.fromPublisher(exchange)
                .flatMap(ex -> allOrders())); // retrieve orders asynchronously
```

See Camel examples (**camel-example-reactive-streams**) for details.

### Advanced Topics

#### Controlling Backpressure (producer side)

When routing Camel exchanges to an external subscriber, backpressure is handled by an internal buffer that caches exchanges before delivering them. If the subscriber is slower than the exchange rate, the buffer may become too big. In many circumstances, this must be avoided.

Considering the following route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms:queue")
    .to("reactive-streams:flow");
```

```xml
<route>
  <from uri="jms:queue"/>
  <to uri="reactive-streams:flow"/>
</route>
```

```yaml
- route:
    from:
      uri: jms:queue
      steps:
        - to:
            uri: reactive-streams:flow
```

If the JMS queue contains a high number of messages and the Subscriber associated with the `flow` stream is too slow, messages are dequeued from JMS and appended to the buffer, possibly causing an _"out of memory"_ error. To avoid such problems, a `ThrottlingInflightRoutePolicy` can be set in the route.

_Java-only: programmatic `ThrottlingInflightRoutePolicy` to limit in-flight exchanges_

```java
ThrottlingInflightRoutePolicy policy = new ThrottlingInflightRoutePolicy();
policy.setMaxInflightExchanges(10);

from("jms:queue")
    .routePolicy(policy)
    .to("reactive-streams:flow");
```

The policy limits the maximum number of active exchanges (and so the maximum size of the buffer), keeping it lower than the threshold (`10` in the example). When more than `10` messages are in flight, the route is suspended, waiting for the subscriber to process them.

With this mechanism, the subscriber controls the route suspension/resume automatically, through backpressure. When multiple subscribers are consuming items from the same stream, the slowest one controls the route status automatically.

In other circumstances, e.g., when using a `http` consumer, the route suspension makes the http service unavailable, so using the default configuration (no policy, unbounded buffer) should be preferable. Users should try to avoid memory issues by limiting the number of requests to the http service (e.g., scaling out).

In contexts where a certain amount of data loss is acceptable, setting a backpressure strategy other than `BUFFER` can be a solution for dealing with fast sources.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:thermostat")
    .to("reactive-streams:flow?backpressureStrategy=LATEST");
```

```xml
<route>
  <from uri="direct:thermostat"/>
  <to uri="reactive-streams:flow?backpressureStrategy=LATEST"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:thermostat
      steps:
        - to:
            uri: reactive-streams:flow
            parameters:
              backpressureStrategy: LATEST
```

When the `LATEST` backpressure strategy is used, the publisher keeps only the last exchange received from the route, while older data is discarded (other options are available).

#### Controlling Backpressure (consumer side)

When Camel consumes items from a reactive-streams publisher, the maximum number of in-flight exchanges can be set as an endpoint option.

The subscriber associated with the consumer interacts with the publisher to keep the number of messages in the route lower than the threshold.

An example of backpressure-aware route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("reactive-streams:numbers?maxInflightExchanges=10")
    .to("direct:endpoint");
```

```xml
<route>
  <from uri="reactive-streams:numbers?maxInflightExchanges=10"/>
  <to uri="direct:endpoint"/>
</route>
```

```yaml
- route:
    from:
      uri: reactive-streams:numbers
      parameters:
        maxInflightExchanges: 10
      steps:
        - to:
            uri: direct:endpoint
```

The number of items that Camel requests to the source publisher (through the reactive streams backpressure mechanism) is always lower than `10`. Messages are processed by a single thread in the Camel side.

The number of concurrent consumers (threads) can also be set as endpoint option (`concurrentConsumers`). When using 1 consumer (the default), the order of items in the source stream is maintained. When this value is increased, items will be processed concurrently by multiple threads (so not preserving the order).