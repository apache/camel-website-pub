# OpenTelemetry Metrics

**Since Camel 4.17**

**Only producer is supported**

The OpenTelemetry Metrics component allows the collection of various metrics directly from Camel routes. Supported metric types are [counter](#OpenTelemetryComponent-counter), [summary](#OpenTelemetryComponent-summary), and [timer](#OpenTelemetryComponent-timer).

To get started, Maven users need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-opentelemetry-metrics</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

opentelemetry-metrics:\[ counter | summary | timer \]:metricname\[?options\]

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

The OpenTelemetry Metrics component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **meter** (advanced) | To use a custom configured Meter. |  | Meter |

## Endpoint Options

The OpenTelemetry Metrics endpoint is configured using URI syntax:

opentelemetry-metrics:metricType:metricName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **metricType** (producer) | 
**Required** Type of metrics.

Enum values:

-   counter
    
-   summary
    
-   timer
    





 |  | InstrumentType |
| **metricName** (producer) | **Required** Name of metric. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
Action expression when using timer type.

Enum values:

-   start
    
-   stop
    





 |  | String |
| **attributes** (producer) | metric attributes. This is a multi-value option with prefix: attributes. |  | Map |
| **decrement** (producer) | Decrement value expression when using counter type. |  | String |
| **increment** (producer) | Increment value expression when using counter type. |  | String |
| **metricsDescription** (producer) | Description of metrics. |  | String |
| **unit** (producer) | 

The time unit when using the timer type.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **value** (producer) | Value expression when using histogram type. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The OpenTelemetry Metrics component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMetricsTimerAction** (producer) Constant: [`HEADER_TIMER_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-opentelemetry-metrics/latest/org/apache/camel/opentelemetry/metrics/OpenTelemetryConstants.html#HEADER_TIMER_ACTION) | 
Override timer action in URI.

Enum values:

-   START
    
-   STOP
    





 |  | OpenTelemetryTimerAction |
| **CamelMetricsHistogramValue** (producer) Constant: [`HEADER_HISTOGRAM_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-opentelemetry-metrics/latest/org/apache/camel/opentelemetry/metrics/OpenTelemetryConstants.html#HEADER_HISTOGRAM_VALUE) | Override histogram value in URI. |  | long |
| **CamelMetricsCounterDecrement** (producer) Constant: [`HEADER_COUNTER_DECREMENT`](https://javadoc.io/doc/org.apache.camel/camel-opentelemetry-metrics/latest/org/apache/camel/opentelemetry/metrics/OpenTelemetryConstants.html#HEADER_COUNTER_DECREMENT) | Override decrement value in URI. |  | Double |
| **CamelMetricsCounterIncrement** (producer) Constant: [`HEADER_COUNTER_INCREMENT`](https://javadoc.io/doc/org.apache.camel/camel-opentelemetry-metrics/latest/org/apache/camel/opentelemetry/metrics/OpenTelemetryConstants.html#HEADER_COUNTER_INCREMENT) | Override increment value in URI. |  | Double |
| **CamelMetricsName** (producer) Constant: [`HEADER_METRIC_NAME`](https://javadoc.io/doc/org.apache.camel/camel-opentelemetry-metrics/latest/org/apache/camel/opentelemetry/metrics/OpenTelemetryConstants.html#HEADER_METRIC_NAME) | Override name value in URI. |  | String |
| **CamelMetricsDescription** (producer) Constant: [`HEADER_METRIC_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-opentelemetry-metrics/latest/org/apache/camel/opentelemetry/metrics/OpenTelemetryConstants.html#HEADER_METRIC_DESCRIPTION) | Override description value in URI. |  | String |
| **CamelMetricsAttributes** (producer) Constant: [`HEADER_METRIC_ATTRIBUTES`](https://javadoc.io/doc/org.apache.camel/camel-opentelemetry-metrics/latest/org/apache/camel/opentelemetry/metrics/OpenTelemetryConstants.html#HEADER_METRIC_ATTRIBUTES) | To augment meter attributes defined as URI parameters. |  | Attributes |

## Usage

### Opetntelemetry Meter

OpenTelemetry meter configuration involves setting up a `MeterProvider` that is responsible for creating `Meter` instances. These `Meters` are then used to create instruments like counters, gauges or histograms.

#### How it works

OpenTelemetry metrics are collected by instrumented applications that record measurements using instruments like counters and gauges. These measurements are then processed by an OpenTelemetry SDK, which aggregates and batches them before exporting them, either directly or through the OpenTelemetry Collector. See [SdkMeterProvider documentation](https://opentelemetry.io/docs/languages/java/sdk/#sdkmeterprovider) for details on how to configure this.

### Usage of producers

Each meter has a type and name. Supported types are [counter](#OpenTelemetryComponent-counter), [distribution summary](#OpenTelemetryComponent-summary), and [timer](#OpenTelemetryComponent-timer). If no type is provided, then a [counter](#OpenTelemetryComponent-counter), is used by default.

The meter name is a string that is evaluated as a `Simple` expression and can also be overridden using the [`CamelMetricsName`](#OpenTelemetryComponent-headers) header allowing the selection of the meter that depends on the exchange data.

The optional `attributes` URI parameter is a comma-separated string consisting of `key=value` expressions. Both `key` and `value` are strings that are evaluated as `Simple` expressions.

For example, the URI parameter `attributes.X=${header.Y}` would assign the current value of header `Y` to the key `X`.

#### Headers

The meter name defined in the URI can be overridden by populating a header with name `CamelMetricsName`. The meter attributes defined as URI parameters can be augmented by populating a header with name `CamelMetricsAttributes`.

For example

_Java-only: requires OpenTelemetry Attributes API_

```java
from("direct:in")
    .setHeader("CamelMetricsName", constant("new.name"))
    .setHeader("CamelMetricsAttributes", constant(Attributes.of(AttributeKey.stringKey("dynamic-key"), "dynamic-value")))
    .to("opentelemetry-metrics:counter:name.not.used?attributes.key=value")
    .to("direct:out");
```

will update a counter with name `new.name` (instead of `name.not.used`) using the attribute `dynamic-key` with value `dynamic-value` in addition to the attribute `key` with value `value`.

All Metrics specific headers are removed from the message once the OpenTelemetry endpoint finishes processing the exchange. While processing the exchange the OpenTelemetry endpoint will catch all exceptions and write log entry using level `warn`.

### Counter

opentelemetry-metrics:counter:name\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| increment | \- | Long value to add to the counter |
| decrement | \- | Long value to subtract from the counter |

If neither `increment` or `decrement` is defined then value of the counter will be incremented by one. If `increment` and `decrement` are both defined only the increment operation is called.

-   Java
    
-   XML
    
-   YAML
    

```java
// update counter 'simple.counter' by 7
from("direct:in")
    .to("opentelemetry-metrics:counter:simple.counter?increment=7")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="opentelemetry-metrics:counter:simple.counter?increment=7"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: opentelemetry-metrics:counter:simple.counter
            parameters:
              increment: 7
        - to:
            uri: direct:out
```

-   Java
    
-   XML
    
-   YAML
    

```java
// increment counter 'simple.counter' by 1
from("direct:in")
    .to("opentelemetry-metrics:counter:simple.counter")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="opentelemetry-metrics:counter:simple.counter"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: opentelemetry-metrics:counter:simple.counter
        - to:
            uri: direct:out
```

Both `increment` and `decrement` values are evaluated as `Simple` expressions with a Long result. For instance, if header `X` contains a value that evaluates to `3`, the counter with name `simple.counter` is decremented by 3:

-   Java
    
-   XML
    
-   YAML
    

```java
// decrement counter 'simple.counter' by 3
from("direct:in")
    .to("opentelemetry-metrics:counter:simple.counter?decrement=${header.X}")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="opentelemetry-metrics:counter:simple.counter?decrement=${header.X}"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: opentelemetry-metrics:counter:simple.counter
            parameters:
              decrement: "${header.X}"
        - to:
            uri: direct:out
```

#### Headers

Message headers can be used to override `increment` and `decrement` values specified in the OpenTelemetry endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsCounterIncrement | Override increment value in URI | Long |
| CamelMetricsCounterDecrement | Override decrement value in URI | Long |

-   Java
    
-   XML
    
-   YAML
    

```java
// update counter 'simple.counter' by 417
from("direct:in")
    .setHeader("CamelMetricsCounterIncrement", constant(417L))
    .to("opentelemetry-metrics:counter:simple.counter?increment=7")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsCounterIncrement">
    <constant resultType="java.lang.Long">417</constant>
  </setHeader>
  <to uri="opentelemetry-metrics:counter:simple.counter?increment=7"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelMetricsCounterIncrement
            constant: 417
        - to:
            uri: opentelemetry-metrics:counter:simple.counter
            parameters:
              increment: 7
        - to:
            uri: direct:out
```

-   Java
    
-   XML
    
-   YAML
    

```java
// updates counter using simple language to evaluate 'body.length'
from("direct:in")
    .setHeader("CamelMetricsCounterIncrement", simple("${body.length}"))
    .to("opentelemetry-metrics:counter:body.len")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsCounterIncrement">
    <simple>${body.length}</simple>
  </setHeader>
  <to uri="opentelemetry-metrics:counter:body.len"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelMetricsCounterIncrement
            simple: "${body.length}"
        - to:
            uri: opentelemetry-metrics:counter:body.len
        - to:
            uri: direct:out
```

### Distribution Summary

opentelemetry-metrics:summary:metricname\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| value | \- | Value to use in histogram |

If `value` is not set then nothing is added to histogram and warning is logged.

-   Java
    
-   XML
    
-   YAML
    

```java
// adds value 9923 to 'simple.histogram'
from("direct:in")
    .to("opentelemetry-metrics:summary:simple.histogram?value=9923")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="opentelemetry-metrics:summary:simple.histogram?value=9923"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: opentelemetry-metrics:summary:simple.histogram
            parameters:
              value: 9923
        - to:
            uri: direct:out
```

-   Java
    
-   XML
    
-   YAML
    

```java
// nothing is added to 'simple.histogram', and a warning is logged
from("direct:in")
    .to("opentelemetry-metrics:summary:simple.histogram")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="opentelemetry-metrics:summary:simple.histogram"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: opentelemetry-metrics:summary:simple.histogram
        - to:
            uri: direct:out
```

The histogram `value` is evaluated as a `Simple` expressions with a Long result. For example, if header `X` contains a value that evaluates to `3`, and this value is registered with the `simple.histogram`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .to("opentelemetry-metrics:summary:simple.histogram?value=${header.X}")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="opentelemetry-metrics:summary:simple.histogram?value=${header.X}"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: opentelemetry-metrics:summary:simple.histogram
            parameters:
              value: "${header.X}"
        - to:
            uri: direct:out
```

#### Headers

A specific Message header can be used to override the value specified in the OpenTelemetry endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsHistogramValue | Override histogram value in URI | Long |

-   Java
    
-   XML
    
-   YAML
    

```java
// adds value 992 to 'simple.histogram'
from("direct:in")
    .setHeader("CamelMetricsHistogramValue", constant(992L))
    .to("opentelemetry-metrics:summary:simple.histogram?value=700")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsHistogramValue">
    <constant resultType="java.lang.Long">992</constant>
  </setHeader>
  <to uri="opentelemetry-metrics:summary:simple.histogram?value=700"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelMetricsHistogramValue
            constant: 992
        - to:
            uri: opentelemetry-metrics:summary:simple.histogram
            parameters:
              value: 700
        - to:
            uri: direct:out
```

### Timer

opentelemetry-metrics:timer:metricname\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| action | \- | start or stop |

If no `action` or an invalid value is provided then a warning is logged without any timer update.

-   Java
    
-   XML
    
-   YAML
    

```java
// measure time spent in route "direct:calculate"
from("direct:in")
    .to("opentelemetry-metrics:timer:simple.timer?action=start")
    .to("direct:calculate")
    .to("opentelemetry-metrics:timer:simple.timer?action=stop");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="opentelemetry-metrics:timer:simple.timer?action=start"/>
  <to uri="direct:calculate"/>
  <to uri="opentelemetry-metrics:timer:simple.timer?action=stop"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: opentelemetry-metrics:timer:simple.timer
            parameters:
              action: start
        - to:
            uri: direct:calculate
        - to:
            uri: opentelemetry-metrics:timer:simple.timer
            parameters:
              action: stop
```

The timer `action` is evaluated as a `Simple` expression returning a result of type `OpenTelemetryTimerAction`. `TimerTask` objects are stored as Exchange properties between different Metrics component calls.

#### Headers

A specific Message header can be used to override action value specified in the OpenTelemetry endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsTimerAction | Override timer action in URI | `org.apache.camel.component.opentelemetry.OpenTelemetryTimerAction` |

_Java-only: requires OpenTelemetryTimerAction enum_

```java
// sets timer action using header
from("direct:in")
    .setHeader("CamelMetricsTimerAction", constant("start"))
    .to("opentelemetry-metrics:timer:simple.timer")
    .to("direct:out");
```

### OpenTelemetry Event Notification

There are event notifiers available for OpenTelemetry to capture Camel route and exchange events. The [Route Event Notifier](#OpenTelemetryComponent-route-event-notifier) counts the number of added and running routes, while the [Exchange Event Notifier](#OpenTelemetryComponent-exchange-event-notifier) times exchanges from their creation to their completion.

#### Camel Route Event Notifier

A Route event notifier can be added to the CamelContext as follows:

_Java-only: programmatic CamelContext API_

```java
camelContext.getManagementStrategy().addEventNotifier(new OpenTelemetryRouteEventNotifier());
```

Camel specific metrics that are available:

  
| Default Name | Type | Description |
| --- | --- | --- |
| camel.routes.added | LongUpDownCounter | Number of routes in total |
| camel.routes.reloaded | LongCounter | Number of routes that have been reloaded |
| camel.routes.running | LongUpDownCounter | Number of routes currently running |

The following options are supported:

  
| Name | Default | Description |
| --- | --- | --- |
| namingStrategy | OpenTelemetryRouteEventNotifierNamingStrategy.DEFAULT | The strategy to use for overriding default metric names. |

#### Camel Exchange Event Notifier

An Exchange event notifier can be added to the CamelContext as follows:

_Java-only: programmatic CamelContext API_

```java
camelContext.getManagementStrategy().addEventNotifier(new OpenTelemetryExchangeEventNotifier());
```

Camel specific metrics that are available via the `OpenTelemetryExchangeEventNotifier`:

  
| Default Name | Type | Description |
| --- | --- | --- |
| camel.exchange.sent | LongHistogram | Time taken to send a message to the endpoint; Default time unit is milliseconds |
| camel.exchange.elapsed | LongHistogram | Time taken to complete exchange; Default time unit is milliseconds |
| camel.exchanges.last.time | ObservableLongGauge | Last exchange processed time since the Unix epoch; ; Default time unit is milliseconds |
| camel.exchanges.inflight | ObservableLongGauge | Number of in flight messages per route |

The following options are supported:

  
| Name | Default | Description |
| --- | --- | --- |
| ignoreExchanges | false | A predicate allowing certain exchanges to be ignored from metrics capture. |
| namingStrategy | OpenTelemetryExchangeEventNotifierNamingStrategy.DEFAULT | The strategy to use for overriding default metric names. |
| timeUnit | TimeUnit.MILLISECONDS | The time unit to use for exchange 'sent' and 'elapsed' metrics. |
| lastExchangeTimeUnit | TimeUnit.MILLISECONDS | The time unit to use for 'last time' metric. |
| baseEndpointURI | true | Whether to use static or dynamic values for Endpoint Name attributes in captured metrics. By default, static values are used. When using dynamic attributes a dynamic to (toD) can compute many different endpoint URIs leading to high cardinality in metrics. |

### OpenTelemetry Route Policy

Route policy metrics can be enabled by adding the `OpenTelemetryRoutePolicyFactory` to the `CamelContext`:

_Java-only: programmatic CamelContext API_

```java
context.addRoutePolicyFactory(new OpenTelemetryRoutePolicyFactory());
```

> **Note**
> You can define a dedicated `OpenTelemetryRoutePolicy` per route you want to instrument in case you only want to instrument a few selected routes.

Camel specific metrics that are available via the `OpenTelemetryRoutePolicy`:

  
| Default Name | Type | Description |
| --- | --- | --- |
| camel.route.policy | LongHistogram | Time taken to complete processing of exchanges for a route |
| camel.exchanges.succeeded | LongCounter | Number of successfully completed exchanges |
| camel.exchanges.failed | LongCounter | Number of failed exchanges |
| camel.exchanges.total | LongCounter | Total number of exchanges processed |
| camel.exchanges.external.redeliveries | LongCounter | Number of externally initiated redeliveries |
| camel.exchanges.failures.handled | LongCounter | Number of failures handled |
| camel.route.policy.tasks.active | ObservableLongUpDownCounter | Number of tasks currently active |
| camel.route.policy.tasks.duration | ObservableLongUpDownCounter | Total duration of all active tasks |

The following options are supported:

  
| Name | Default | Description |
| --- | --- | --- |
| namingStrategy | OpenTelemetryRoutePolicyNamingStrategy.DEFAULT | The strategy to use for overriding default metric names. |
| policyConfiguration | \- | Enables individual metrics to be enabled or disabled. |
| timeUnit | TimeUnit.MILLISECONDS | The time unit for measuring the route policy timer. |
| longTaskTimeUnit | TimeUnit.MILLISECONDS | The time unit for the 'long task' timer that measures total duration of all active tasks. |

### OpenTelemetry Message History Factory

`OpenTelemetryMessageHistoryFactory` allows the capture of Message History performance statistics while routing messages. It works by using an OpenTelemetry Timer to record the time taken to process each node in all routes.

The `OpenTelemetryMessageHistoryFactory` can be added to the `CamelContext`:

_Java-only: programmatic CamelContext API_

```java
context.setMessageHistoryFactory(new OpenTelemetryMessageHistoryFactory());
```

`OpenTelemetryMessageHistory` provides the following Camel specific metric:

  
| Default Name | Type | Description |
| --- | --- | --- |
| camel.message.history | LongHistogram | Time taken for a node to process the message |

The following options are supported on the `OpenTelemetryMessageHistoryFactory`:

  
| Name | Default | Description |
| --- | --- | --- |
| namingStrategy | OpenTelemetryHistoryNamingStrategy.DEFAULT | The strategy to use for overriding the default metric name. |
| nodePattern |  | A pattern to filter which nodes to capture metrics for. By default, all nodes are included |
| timeUnit | TimeUnit.MILLISECONDS | The time unit for recording the processing time. |

## OpenTelemetry Configuration

### Java Agent

Your application will require a Java agent in order to get the metrics generated by the Camel application.

Download the [latest version](https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/).

This package includes the instrumentation agent as well as instrumentation for all supported libraries and all available data exporters. The package provides a completely automatic, out-of-the-box experience. Enable the instrumentation agent using the `-javaagent` flag to the JVM.

```bash
java -javaagent:path/to/opentelemetry-javaagent.jar \
     -Dotel. ... \
     -jar myapp.jar
```

By default, the OpenTelemetry Java agent uses [OTLP exporter](https://github.com/open-telemetry/opentelemetry-java/tree/main/exporters/otlp) configured to send data to [OpenTelemetry collector](https://github.com/open-telemetry/opentelemetry-collector/blob/main/receiver/otlpreceiver/README.md) at `[http://localhost:4318](http://localhost:4318)`.

Configuration parameters are passed as Java system properties (`-D` flags) or as environment variables. See [the configuration documentation](https://opentelemetry.io/docs/zero-code/java/agent/configuration/) for the full list of configuration items. For example:

```bash
java -javaagent:path/to/opentelemetry-javaagent.jar \
     -Dotel.service.name=your-service-name \
     -Dotel.metrics.exporter=otlp \
     -jar myapp.jar
```

### Using Camel OpenTelemetry Metrics with Spring Boot

When you use `camel-opentelemetry-metrics-starter` with Spring Boot, then Spring Boot autoconfiguration will automatically enable metrics capture if a `io.opentelemetry.api.metrics.Meter` is available.

See the following table for options to specify what metrics to capture, or to turn it off.

## Spring Boot Auto-Configuration

When using opentelemetry-metrics with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-opentelemetry-metrics-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.opentelemetry-metrics.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.opentelemetry-metrics.enabled** | Whether to enable auto configuration of the opentelemetry-metrics component. This is enabled by default. |  | Boolean |
| **camel.component.opentelemetry-metrics.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.opentelemetry-metrics.meter** | To use a custom configured Meter. The option is a io.opentelemetry.api.metrics.Meter type. |  | Meter |
| **camel.opentelemetry.metrics.base-endpoint-uri-exchange-event-notifier** | Whether to use static or dynamic values for Endpoint Name tags in captured metrics. By default, static values are used. When using dynamic tags, then a dynamic to (toD) can compute many different endpoint URIs that, can lead to many tags as the URI is dynamic, so use this with care if setting this option to false. | true | Boolean |
| **camel.opentelemetry.metrics.enable-exchange-event-notifier** | Set whether to enable the MicrometerExchangeEventNotifier for capturing metrics on exchange processing times. | true | Boolean |
| **camel.opentelemetry.metrics.enable-message-history** | Set whether to enable the MicrometerMessageHistoryFactory for capturing metrics on individual route node processing times. Depending on the number of configured route nodes, there is the potential to create a large volume of metrics. Therefore, this option is disabled by default. | false | Boolean |
| **camel.opentelemetry.metrics.enable-route-event-notifier** | Set whether to enable the MicrometerRouteEventNotifier for capturing metrics on the total number of routes and total number of routes running. | true | Boolean |
| **camel.opentelemetry.metrics.enable-route-policy** | Set whether to enable the MicrometerRoutePolicyFactory for capturing metrics on route processing times. | true | Boolean |
| **camel.opentelemetry.metrics.route-policy-exclude-pattern** | Pattern to exclude routes (by id) to capture. Multiple route ids can be separated by comma. |  | String |
| **camel.opentelemetry.metrics.route-policy-level** | Sets the level of information to capture. Possible values are all,route,context. all = both context and routes. route = routes only. context = camel context only. | all | String |