# Event

**Since Camel 4.19**

**Only consumer is supported**

The Event component allows you to subscribe to Camel internal events such as route lifecycle events and exchange events. The component leverages Camel’s existing `EventNotifier` mechanism to receive events and dispatch them as exchanges into a route.

## URI format

event:eventTypes\[?options\]

Where `eventTypes` is a comma-separated list of event types to subscribe to. Event types correspond to `CamelEvent.Type` enum values (case-insensitive).

Wildcard patterns are supported using a `*` suffix:

event:Route\*                          <-- all route events
event:Exchange\*                       <-- all exchange events
event:CamelContext\*                   <-- all context events
event:Step\*                           <-- all step events
event:Service\*                        <-- all service events
event:\*                               <-- all events
event:RouteStarted,RouteStopped       <-- specific events
event:Route\*,Exchange\*                <-- combine wildcards

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

The Event component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Event endpoint is configured using URI syntax:

event:events

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **events** (consumer) | **Required** Comma-separated list of event types to subscribe to. Event types correspond to CamelEvent.Type enum values (case-insensitive), for example: RouteStarted, RouteStopped, ExchangeCompleted, ExchangeFailed. Wildcard patterns are supported using a suffix, for example: Route matches all route events, Exchange matches all exchange events, and matches all events. |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **async** (consumer) | Whether to process events asynchronously using a thread pool. When enabled, the event notifier thread is not blocked while the event exchange is processed. Use asyncPoolSize to control the maximum number of concurrent event processing threads. | false | boolean |
| **asyncPoolSize** (consumer) | The maximum number of threads in the pool for async event processing. Only used when the async option is enabled. | 10 | int |
| **asyncQueueSize** (consumer) | The capacity of the bounded event queue used when async is enabled. When the queue is full, the backpressure policy determines the behavior. Only used when the async option is enabled. | 1000 | int |
| **backpressurePolicy** (consumer) | 
The backpressure policy when the async event queue is full. Supported values: Block (block the event notifier thread until space is available), Drop (silently discard the event), Fail (throw an exception).

Enum values:

-   Block
    
-   Drop
    
-   Fail
    





 | Block | BackpressurePolicy |
| **batchSize** (consumer) | Enables event batching. When set to a value greater than 1, events are collected into a java.util.List and dispatched as a single exchange when the batch is full or the batchTimeout expires. The exchange body will be a List. | 0 | int |
| **batchTimeout** (consumer) | The maximum time in milliseconds to wait for a batch to fill before dispatching a partial batch. Only used when batchSize is greater than 1. | 1000 | long |
| **customEventClass** (consumer) | Fully qualified class name of a custom event class to filter on. When set, only events that are instances of the specified class will be accepted. This is useful for subscribing to custom user-defined events. |  | String |
| **exclude** (consumer) | Comma-separated list of route IDs to exclude. For route events, this excludes by route ID. For exchange events, this excludes by the route ID of the exchange. Events matching any of the specified route IDs will be rejected. This option can be used together with the include option. |  | String |
| **include** (consumer) | Comma-separated list of route IDs to include. For route events, this matches the route ID. For exchange events, this matches the route ID of the exchange. Only events matching one of the specified route IDs will be accepted. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Message Headers

The Event component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelEventType** (consumer) Constant: [`HEADER_EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_TYPE) | The event type name (e.g., RouteStarted, ExchangeCompleted). |  | String |
| **CamelEventTimestamp** (consumer) Constant: [`HEADER_EVENT_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_TIMESTAMP) | The event timestamp in milliseconds since epoch (if available). |  | Long |
| **CamelEventRouteId** (consumer) Constant: [`HEADER_EVENT_ROUTE_ID`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_ROUTE_ID) | The route ID. For route events, the route that triggered the event. For exchange events, the route the exchange originated from. |  | String |
| **CamelEventExchangeId** (consumer) Constant: [`HEADER_EVENT_EXCHANGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_EXCHANGE_ID) | The exchange ID (for exchange events). |  | String |
| **CamelEventEndpointUri** (consumer) Constant: [`HEADER_EVENT_ENDPOINT_URI`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_ENDPOINT_URI) | The endpoint URI. For ExchangeSent/ExchangeSending events, the target endpoint. For other exchange events, the from endpoint of the exchange. |  | String |
| **CamelEventException** (consumer) Constant: [`HEADER_EVENT_EXCEPTION`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_EXCEPTION) | The exception message from FailureEvent.getCause() (for failure events such as ExchangeFailed, RouteRestartingFailure, ServiceStartupFailure, etc.). |  | String |
| **CamelEventDuration** (consumer) Constant: [`HEADER_EVENT_DURATION`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_DURATION) | The time taken in milliseconds for ExchangeSent events. |  | Long |
| **CamelEventStepId** (consumer) Constant: [`HEADER_EVENT_STEP_ID`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_STEP_ID) | The step ID (for step events such as StepStarted, StepCompleted, StepFailed). |  | String |
| **CamelEventRedeliveryAttempt** (consumer) Constant: [`HEADER_EVENT_REDELIVERY_ATTEMPT`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_REDELIVERY_ATTEMPT) | The redelivery attempt number (for ExchangeRedelivery events). |  | Integer |
| **CamelEventBatchSize** (consumer) Constant: [`HEADER_EVENT_BATCH_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-event/latest/org/apache/camel/component/camelevent/CamelEventConstants.html#HEADER_EVENT_BATCH_SIZE) | The number of events in a batch (only set when batchSize is configured). |  | Integer |

## Event Types

The following event types are available (corresponding to `org.apache.camel.spi.CamelEvent.Type`):

### CamelContext Events

-   `CamelContextInitializing`
    
-   `CamelContextInitialized`
    
-   `CamelContextStarting`
    
-   `CamelContextStarted`
    
-   `CamelContextStopping`
    
-   `CamelContextStopped`
    
-   `CamelContextResuming`
    
-   `CamelContextResumed`
    
-   `CamelContextSuspending`
    
-   `CamelContextSuspended`
    
-   `CamelContextReloading`
    
-   `CamelContextReloaded`
    
-   `CamelContextStartupFailure`
    
-   `CamelContextStopFailure`
    
-   `CamelContextResumeFailure`
    
-   `CamelContextReloadFailure`
    

### Route Events

-   `RouteAdded`
    
-   `RouteRemoved`
    
-   `RouteStarting`
    
-   `RouteStarted`
    
-   `RouteStopping`
    
-   `RouteStopped`
    
-   `RouteReloaded`
    
-   `RouteRestarting`
    
-   `RouteRestartingFailure`
    
-   `RoutesStarting`
    
-   `RoutesStarted`
    
-   `RoutesStopping`
    
-   `RoutesStopped`
    

### Exchange Events

-   `ExchangeCreated`
    
-   `ExchangeCompleted`
    
-   `ExchangeFailed`
    
-   `ExchangeFailureHandling`
    
-   `ExchangeFailureHandled`
    
-   `ExchangeRedelivery`
    
-   `ExchangeSending`
    
-   `ExchangeSent`
    

### Step Events

-   `StepStarted`
    
-   `StepCompleted`
    
-   `StepFailed`
    

### Service Events

-   `ServiceStartupFailure`
    
-   `ServiceStopFailure`
    

## Wildcard Subscriptions

Instead of listing each event type individually, you can use wildcard patterns with a `*` suffix to match all event types that start with a given prefix.

```java
// Subscribe to all route events (RouteStarted, RouteStopped, RouteAdded, etc.)
from("event:Route*")
    .log("Route event: ${header.CamelEventType}");

// Subscribe to all exchange events
from("event:Exchange*")
    .log("Exchange event: ${header.CamelEventType}");

// Subscribe to all events
from("event:*")
    .log("Event: ${header.CamelEventType}");

// Mix wildcards with specific types
from("event:Route*,ExchangeFailed")
    .log("Event: ${header.CamelEventType}");
```

## Filtering

You can filter events using the `include` option. For route events, this matches the route ID. For exchange events, this matches the route ID of the exchange (from route).

For example, to only receive events for routes `myRoute1` and `myRoute2`:

event:RouteStarted,RouteStopped?include=myRoute1,myRoute2

### Exclusion Filter

The `exclude` option allows you to exclude events from specific routes. This can be used on its own or combined with the `include` option.

event:ExchangeCompleted?exclude=internalRoute
event:Route\*?include=myRoute1,myRoute2&exclude=myRoute2

### Custom Event Class Filter

The `customEventClass` option allows filtering by a specific custom event class. When subscribing to `Custom` events, this restricts delivery to only events that are instances of the specified class.

event:Custom?customEventClass=com.example.MyCustomEvent

## Message Headers

The following headers are set on exchanges created by this component. Header constants are defined in `org.apache.camel.component.camelevent.CamelEventConstants`.

### Common Headers

  
| Header | Type | Description |
| --- | --- | --- |
| CamelEventType | String | The event type name (e.g., `RouteStarted`, `ExchangeCompleted`) |
| CamelEventTimestamp | Long | The event timestamp in milliseconds since epoch (if available) |

### Route Event Headers

  
| Header | Type | Description |
| --- | --- | --- |
| CamelEventRouteId | String | The route ID |

### Exchange Event Headers

  
| Header | Type | Description |
| --- | --- | --- |
| CamelEventExchangeId | String | The exchange ID |
| CamelEventRouteId | String | The route ID of the exchange (from route) |
| CamelEventEndpointUri | String | The from endpoint URI of the exchange |

### Failure Event Headers

Set on any failure event (`ExchangeFailed`, `RouteRestartingFailure`, `ServiceStartupFailure`, etc.):

  
| Header | Type | Description |
| --- | --- | --- |
| CamelEventException | String | The exception message from `FailureEvent.getCause()` |

### ExchangeSent Event Headers

In addition to the common exchange event headers, `ExchangeSent` events include:

  
| Header | Type | Description |
| --- | --- | --- |
| CamelEventEndpointUri | String | The endpoint URI the exchange was sent to (overrides the from endpoint URI) |
| CamelEventDuration | Long | The time taken in milliseconds |

### ExchangeSending Event Headers

In addition to the common exchange event headers, `ExchangeSending` events include:

  
| Header | Type | Description |
| --- | --- | --- |
| CamelEventEndpointUri | String | The endpoint URI the exchange is being sent to (overrides the from endpoint URI) |

### ExchangeRedelivery Event Headers

  
| Header | Type | Description |
| --- | --- | --- |
| CamelEventRedeliveryAttempt | Integer | The redelivery attempt number |

### Step Event Headers

  
| Header | Type | Description |
| --- | --- | --- |
| CamelEventStepId | String | The step ID |

## Message Body

The message body contains the `CamelEvent` object, which can be cast to the specific event sub-interface for additional details.

## Examples

Subscribe to route started and stopped events:

```java
from("event:RouteStarted,RouteStopped")
    .log("Route ${header.CamelEventRouteId} event: ${header.CamelEventType}");
```

Subscribe to all route events using a wildcard:

```java
from("event:Route*")
    .log("Route ${header.CamelEventRouteId} event: ${header.CamelEventType}");
```

Subscribe to exchange completed events for a specific route:

```java
from("event:ExchangeCompleted?include=myRoute")
    .log("Exchange completed on route myRoute");
```

Monitor exchange failures with error details:

```java
from("event:ExchangeFailed")
    .log("Exchange ${header.CamelEventExchangeId} failed on route ${header.CamelEventRouteId}: ${header.CamelEventException}");
```

Monitor exchange latency using ExchangeSent events:

```java
from("event:ExchangeSent")
    .log("Exchange sent to ${header.CamelEventEndpointUri} took ${header.CamelEventDuration}ms");
```

Exclude internal routes from monitoring:

```java
from("event:ExchangeCompleted?exclude=internalRoute1,internalRoute2")
    .log("Exchange completed on route ${header.CamelEventRouteId}");
```

Subscribe to specific custom events:

```java
from("event:Custom?customEventClass=com.example.MyCustomEvent")
    .log("Custom event received: ${body}");
```

## Async Processing

By default, events are processed synchronously on the event notifier thread. This means the event notifier is blocked until the route has finished processing the event.

To process events asynchronously, set the `async` option to `true`. This dispatches event processing to a thread pool, freeing the event notifier thread immediately.

Use the `asyncPoolSize` option to control the maximum number of concurrent event processing threads (default: 10).

```java
// Process events asynchronously with default pool size (10)
from("event:ExchangeCompleted?async=true")
    .log("Exchange completed: ${header.CamelEventExchangeId}");

// Process events asynchronously with a custom pool size
from("event:Exchange*?async=true&asyncPoolSize=5")
    .log("Exchange event: ${header.CamelEventType}");
```

### Backpressure

When async processing is enabled, events are placed into a bounded blocking queue (default capacity: 1000, configurable via `asyncQueueSize`). When the queue is full, the `backpressurePolicy` option controls the behavior:

-   `Block` (default) — blocks the event notifier thread until space is available.
    
-   `Drop` — silently discards the event.
    
-   `Fail` — throws an exception.
    

```java
// Async with a small queue and Drop policy (discard events when overloaded)
from("event:ExchangeCompleted?async=true&asyncQueueSize=100&backpressurePolicy=Drop")
    .log("Exchange completed: ${header.CamelEventExchangeId}");

// Async with Fail policy (fail fast if queue is full)
from("event:Exchange*?async=true&asyncQueueSize=500&backpressurePolicy=Fail")
    .log("Exchange event: ${header.CamelEventType}");
```

## Event Batching

For high-throughput scenarios, events can be collected into batches and dispatched as a single exchange containing a `java.util.List<CamelEvent>` body. This reduces the overhead of creating individual exchanges for each event.

Set `batchSize` to the number of events per batch. The `batchTimeout` option (default: 1000ms) controls the maximum time to wait for a full batch before flushing a partial batch.

When batching is enabled, the `CamelEventBatchSize` header is set with the number of events in the batch.

```java
// Collect events in batches of 50, flush every 2 seconds
from("event:ExchangeCompleted?batchSize=50&batchTimeout=2000")
    .log("Received batch of ${header.CamelEventBatchSize} events");

// Combine async processing with batching
from("event:Exchange*?async=true&batchSize=100&batchTimeout=5000")
    .log("Batch of ${header.CamelEventBatchSize} exchange events");
```

## JBang Quick Start

You can quickly try the Event component using [Camel JBang](../../manual/camel-jbang.md).

Create a file called `event-monitor.yaml`:

```yaml
- route:
    from:
      uri: "event:Route*"
      steps:
        - log: "Route event: ${header.CamelEventType} - route ${header.CamelEventRouteId}"

- route:
    from:
      uri: "event:ExchangeCompleted,ExchangeFailed"
      steps:
        - log: "Exchange ${header.CamelEventExchangeId} on route ${header.CamelEventRouteId}: ${header.CamelEventType}"

- route:
    id: myRoute
    from:
      uri: "timer:tick"
      parameters:
        period: "5000"
      steps:
        - setBody:
            constant: "Hello from myRoute!"
        - log: "${body}"
```

Then run it:

```bash
camel run event-monitor.yaml
```

## Distributed Events

The Event component captures events within a single CamelContext (JVM). To propagate events across multiple Camel instances, use standard Camel routes to forward events to a messaging system:

```java
// Producer side: capture local events and publish to Kafka
from("event:RouteStarted,RouteStopped,ExchangeFailed")
    .setBody(simple("${header.CamelEventType}: ${header.CamelEventRouteId} at ${header.CamelEventTimestamp}"))
    .to("kafka:camel-events");

// Consumer side (same or different JVM): process distributed events
from("kafka:camel-events")
    .to("log:distributed-events");
```

This approach is transport-agnostic — you can use Kafka, JMS, AMQP, NATS, or any other Camel messaging component. It gives you full control over event serialization, filtering, and routing logic.