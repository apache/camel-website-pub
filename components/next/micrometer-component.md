# Micrometer

**Since Camel 2.22**

**Only producer is supported**

The Micrometer component allows collecting various metrics directly from Camel routes. Supported metric types are [counter](#MicrometerComponent-counter), [summary](#MicrometerComponent-summary), and [timer](#MicrometerComponent-timer). [Micrometer](http://micrometer.io/) provides a simple way to measure the behaviour of an application. The configurable reporting backend (via Micrometer registries) enables different integration options for collecting and visualizing statistics.

The component also provides a `MicrometerRoutePolicyFactory` which allows to expose route statistics using Micrometer as well as `EventNotifier` implementations for counting routes and timing exchanges from their creation to their completion.

Maven users need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-micrometer</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

micrometer:\[ counter | summary | timer \]:metricname\[?options\]

## Options

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

The Micrometer component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **metricsRegistry** (advanced) | To use a custom configured MetricRegistry. |  | MeterRegistry |

## Endpoint Options

The Micrometer endpoint is configured using URI syntax:

micrometer:metricsType:metricsName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **metricsType** (producer) | 
**Required** Type of metrics.

Enum values:

-   counter
    
-   summary
    
-   timer
    





 |  | Type |
| **metricsName** (producer) | **Required** Name of metrics. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
Action expression when using timer type.

Enum values:

-   start
    
-   stop
    





 |  | String |
| **decrement** (producer) | Decrement value expression when using counter type. |  | String |
| **increment** (producer) | Increment value expression when using counter type. |  | String |
| **metricsDescription** (producer) | Description of metrics. |  | String |
| **tags** (producer) | Tags of metrics. This is a multi-value option with prefix: tags. |  | Map |
| **value** (producer) | Value expression when using histogram type. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Micrometer component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMetricsTimerAction** (producer) Constant: [`HEADER_TIMER_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-micrometer/latest/org/apache/camel/component/micrometer/MicrometerConstants.html#HEADER_TIMER_ACTION) | 
Override timer action in URI.

Enum values:

-   start
    
-   stop
    





 |  | MicrometerTimerAction |
| **CamelMetricsHistogramValue** (producer) Constant: [`HEADER_HISTOGRAM_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-micrometer/latest/org/apache/camel/component/micrometer/MicrometerConstants.html#HEADER_HISTOGRAM_VALUE) | Override histogram value in URI. |  | long |
| **CamelMetricsCounterDecrement** (producer) Constant: [`HEADER_COUNTER_DECREMENT`](https://javadoc.io/doc/org.apache.camel/camel-micrometer/latest/org/apache/camel/component/micrometer/MicrometerConstants.html#HEADER_COUNTER_DECREMENT) | Override decrement value in URI. |  | Double |
| **CamelMetricsCounterIncrement** (producer) Constant: [`HEADER_COUNTER_INCREMENT`](https://javadoc.io/doc/org.apache.camel/camel-micrometer/latest/org/apache/camel/component/micrometer/MicrometerConstants.html#HEADER_COUNTER_INCREMENT) | Override increment value in URI. |  | Double |
| **CamelMetricsName** (producer) Constant: [`HEADER_METRIC_NAME`](https://javadoc.io/doc/org.apache.camel/camel-micrometer/latest/org/apache/camel/component/micrometer/MicrometerConstants.html#HEADER_METRIC_NAME) | Override name value in URI. |  | String |
| **CamelMetricsDescription** (producer) Constant: [`HEADER_METRIC_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-micrometer/latest/org/apache/camel/component/micrometer/MicrometerConstants.html#HEADER_METRIC_DESCRIPTION) | Override description value in URI. |  | String |
| **CamelMetricsTags** (producer) Constant: [`HEADER_METRIC_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-micrometer/latest/org/apache/camel/component/micrometer/MicrometerConstants.html#HEADER_METRIC_TAGS) | To augment meter tags defined as URI parameters. |  | Iterable |

## Usage

### Meter Registry

By default the Camel Micrometer component creates a `SimpleMeterRegistry` instance, suitable mainly for testing. You should define a dedicated registry by providing a `MeterRegistry` bean. Micrometer registries primarily determine the backend monitoring system to be used. A `CompositeMeterRegistry` can be used to address more than one monitoring target.

### Default Camel Metrics

Some Camel specific metrics are available out of the box.

  
| Name | Type | Description |
| --- | --- | --- |
| camel.message.history | timer | Sample of performance of each node in the route when message history is enabled |
| camel.routes.added | gauge | Number of routes in total |
| camel.routes.reloaded | gauge | Number of routes that has been reloaded |
| camel.routes.running | gauge | Number of routes currently running |
| camel.exchanges.inflight | gauge | Route inflight messages |
| camel.exchanges.total | counter | Total number of processed exchanges |
| camel.exchanges.succeeded | counter | Number of successfully completed exchanges |
| camel.exchanges.failed | counter | Number of failed exchanges |
| camel.exchanges.failures.handled | counter | Number of failures handled |
| camel.exchanges.external.redeliveries | counter | Number of external initiated redeliveries (such as from JMS broker) |
| camel.exchange.event.notifier | gauge + summary | Metrics for messages created, sent, completed, and failed events |
| camel.route.policy | gauge + summary | Route performance metrics |
| camel.route.policy.long.task | gauge + summary | Route long task metric |

#### Using legacy metrics naming

In Camel 3.20 or older, then the naming of metrics is using _camelCase_ style. However, since Camel 3.21 onwards, the naming is using the Micrometer convention style (see table above).

To use the legacy naming, then you can use the `LEGACY` naming from the `xxxNamingStrategy` interfaces.

For example:

_Java-only: configuring legacy naming strategy on the route policy factory_

```java
MicrometerRoutePolicyFactory factory = new MicrometerRoutePolicyFactory();
factory.setNamingStrategy(MicrometerRoutePolicyNamingStrategy.LEGACY);
```

The naming style can be configured on:

-   `MicrometerRoutePolicyFactory`
    
-   `MicrometerExchangeEventNotifier`
    
-   `MicrometerRouteEventNotifier`
    
-   `MicrometerMessageHistoryFactory`
    

### Usage of producers

Each meter has type and name. Supported types are [counter](#MicrometerComponent-counter), [distribution summary](#MicrometerComponent-summary), and timer. If no type is provided, then a counter is used by default.

The meter name is a string that is evaluated as `Simple` expression. In addition to using the `CamelMetricsName` header (see below), this allows selecting the meter depending on exchange data.

The optional `tags` URI parameter is a comma-separated string, consisting of `key=value` expressions. Both `key` and `value` are strings that are also evaluated as `Simple` expression. E.g., the URI parameter `tags=X=${header.Y}` would assign the current value of header `Y` to the key `X`.

#### Headers

The meter name defined in URI can be overridden by populating a header with name `CamelMetricsName`. The meter tags defined as URI parameters can be augmented by populating a header with name `CamelMetricsTags`.

For example

_Java-only: requires Micrometer Tags API_

```java
from("direct:in")
    .setHeader("CamelMetricsName").constant("new.name")
    .setHeader("CamelMetricsTags", constant(Tags.of("dynamic-key", "dynamic-value")))
    .to("micrometer:counter:name.not.used?tags=key=value")
    .to("direct:out");
```

will update a counter with name `new.name` instead of `name.not.used` using the tag `dynamic-key` with value `dynamic-value` in addition to the tag `key` with value `value`.

All Metrics specific headers are removed from the message once the Micrometer endpoint finishes processing of exchange. While processing exchange Micrometer endpoint will catch all exceptions and write log entry using level `warn`.

### Counter

micrometer:counter:name\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| increment | \- | Double value to add to the counter |
| decrement | \- | Double value to subtract from the counter |

If neither `increment` or `decrement` is defined then value of the counter will be incremented by one. If `increment` and `decrement` are both defined only increment operation is called.

-   Java
    
-   XML
    
-   YAML
    

```java
// update counter simple.counter by 7
from("direct:in")
    .to("micrometer:counter:simple.counter?increment=7")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="micrometer:counter:simple.counter?increment=7"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: micrometer:counter:simple.counter
            parameters:
              increment: 7
        - to:
            uri: direct:out
```

-   Java
    
-   XML
    
-   YAML
    

```java
// increment counter simple.counter by 1
from("direct:in")
    .to("micrometer:counter:simple.counter")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="micrometer:counter:simple.counter"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: micrometer:counter:simple.counter
        - to:
            uri: direct:out
```

Both `increment` and `decrement` values are evaluated as `Simple` expressions with a Double result, e.g., if header `X` contains a value that evaluates to 3.0, the `simple.counter` counter is decremented by 3.0:

-   Java
    
-   XML
    
-   YAML
    

```java
// decrement counter simple.counter by 3
from("direct:in")
    .to("micrometer:counter:simple.counter?decrement=${header.X}")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="micrometer:counter:simple.counter?decrement=${header.X}"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: micrometer:counter:simple.counter
            parameters:
              decrement: "${header.X}"
        - to:
            uri: direct:out
```

#### Headers

Like in `camel-metrics`, specific Message headers can be used to override `increment` and `decrement` values specified in the Micrometer endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsCounterIncrement | Override increment value in URI | Double |
| CamelMetricsCounterDecrement | Override decrement value in URI | Double |

-   Java
    
-   XML
    
-   YAML
    

```java
// update counter simple.counter by 417
from("direct:in")
    .setHeader("CamelMetricsCounterIncrement").constant(417.0D)
    .to("micrometer:counter:simple.counter?increment=7")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsCounterIncrement">
    <constant resultType="java.lang.Double">417.0</constant>
  </setHeader>
  <to uri="micrometer:counter:simple.counter?increment=7"/>
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
            constant: 417.0
        - to:
            uri: micrometer:counter:simple.counter
            parameters:
              increment: 7
        - to:
            uri: direct:out
```

-   Java
    
-   XML
    
-   YAML
    

```java
// updates counter using simple language to evaluate body.length
from("direct:in")
    .setHeader("CamelMetricsCounterIncrement", simple("${body.length}"))
    .to("micrometer:counter:body.length")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsCounterIncrement">
    <simple>${body.length}</simple>
  </setHeader>
  <to uri="micrometer:counter:body.length"/>
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
            uri: micrometer:counter:body.length
        - to:
            uri: direct:out
```

### Distribution Summary

micrometer:summary:metricname\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| value | \- | Value to use in histogram |

If no `value` is not set, nothing is added to histogram and warning is logged.

-   Java
    
-   XML
    
-   YAML
    

```java
// adds value 9923 to simple.histogram
from("direct:in")
    .to("micrometer:summary:simple.histogram?value=9923")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="micrometer:summary:simple.histogram?value=9923"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: micrometer:summary:simple.histogram
            parameters:
              value: 9923
        - to:
            uri: direct:out
```

-   Java
    
-   XML
    
-   YAML
    

```java
// nothing is added to simple.histogram; warning is logged
from("direct:in")
    .to("micrometer:summary:simple.histogram")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="micrometer:summary:simple.histogram"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: micrometer:summary:simple.histogram
        - to:
            uri: direct:out
```

`value` is evaluated as `Simple` expressions with a Double result, e.g., if header `X` contains a value that evaluates to 3.0, this value is registered with the `simple.histogram`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .to("micrometer:summary:simple.histogram?value=${header.X}")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="micrometer:summary:simple.histogram?value=${header.X}"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: micrometer:summary:simple.histogram
            parameters:
              value: "${header.X}"
        - to:
            uri: direct:out
```

#### Headers

Like in `camel-metrics`, a specific Message header can be used to override the value specified in the Micrometer endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsHistogramValue | Override histogram value in URI | Long |

-   Java
    
-   XML
    
-   YAML
    

```java
// adds value 992.0 to simple.histogram
from("direct:in")
    .setHeader("CamelMetricsHistogramValue").constant(992.0D)
    .to("micrometer:summary:simple.histogram?value=700")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsHistogramValue">
    <constant resultType="java.lang.Double">992.0</constant>
  </setHeader>
  <to uri="micrometer:summary:simple.histogram?value=700"/>
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
            constant: 992.0
        - to:
            uri: micrometer:summary:simple.histogram
            parameters:
              value: 700
        - to:
            uri: direct:out
```

### Timer

micrometer:timer:metricname\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| action | \- | start or stop |

If no `action` or invalid value is provided then warning is logged without any timer update. If action `start` is called on an already running timer or `stop` is called on an unknown timer, nothing is updated and warning is logged.

-   Java
    
-   XML
    
-   YAML
    

```java
// measure time spent in route "direct:calculate"
from("direct:in")
    .to("micrometer:timer:simple.timer?action=start")
    .to("direct:calculate")
    .to("micrometer:timer:simple.timer?action=stop");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="micrometer:timer:simple.timer?action=start"/>
  <to uri="direct:calculate"/>
  <to uri="micrometer:timer:simple.timer?action=stop"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: micrometer:timer:simple.timer
            parameters:
              action: start
        - to:
            uri: direct:calculate
        - to:
            uri: micrometer:timer:simple.timer
            parameters:
              action: stop
```

`Timer.Sample` objects are stored as Exchange properties between different Metrics component calls.

`action` is evaluated as a `Simple` expression returning a result of type `MicrometerTimerAction`.

#### Headers

Like in `camel-metrics`, a specific Message header can be used to override action value specified in the Micrometer endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsTimerAction | Override timer action in URI | `org.apache.camel.component.micrometer.MicrometerTimerAction` |

-   Java
    
-   XML
    
-   YAML
    

```java
// sets timer action using header
from("direct:in")
    .setHeader("CamelMetricsTimerAction").constant("start")
    .to("micrometer:timer:simple.timer")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsTimerAction">
    <constant>start</constant>
  </setHeader>
  <to uri="micrometer:timer:simple.timer"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelMetricsTimerAction
            constant: start
        - to:
            uri: micrometer:timer:simple.timer
        - to:
            uri: direct:out
```

### Using Micrometer route policy factory

`MicrometerRoutePolicyFactory` allows to add a RoutePolicy for each route to expose route utilization statistics using Micrometer. This factory can be used in Java and XML as the examples below demonstrates.

> **Note**
> Instead of using the `MicrometerRoutePolicyFactory` you can define a dedicated `MicrometerRoutePolicy` per route you want to instrument, in case you only want to instrument a few selected routes.

From Java, you add the factory to the `CamelContext` as shown below:

_Java-only: adding MicrometerRoutePolicyFactory to the CamelContext_

```java
context.addRoutePolicyFactory(new MicrometerRoutePolicyFactory());
```

And from XML DSL you define a <bean> as follows:

```xml
  <!-- use camel-micrometer route policy to gather metrics for all routes -->
  <bean id="metricsRoutePolicyFactory" class="org.apache.camel.component.micrometer.routepolicy.MicrometerRoutePolicyFactory"/>
```

The `MicrometerRoutePolicyFactory` and `MicrometerRoutePolicy` supports the following options:

  
| Name | Default | Description |
| --- | --- | --- |
| prettyPrint | false | Whether to use pretty print when outputting statistics in json format |
| meterRegistry |  | Allow using a shared `MeterRegistry`. If none is provided, then Camel will create a shared instance used by the CamelContext. |
| durationUnit | TimeUnit.MILLISECONDS | The unit to use for duration in when dumping the statistics as json. |
| configuration | see below | MicrometerRoutePolicyConfiguration.class |

The `MicrometerRoutePolicyConfiguration` supports the following options:

  
| Name | Default | Description |
| --- | --- | --- |
| contextEnabled | true | whether to include counter for context level metrics |
| routeEnabled | true | whether to include counter for route level metrics |
| excludePattern |  | Optional pattern to exclude routes matched by route ids. Multiple ids can be separated by comma. |
| additionalCounters | true | activates all additional counters |
| exchangesSucceeded | true | activates counter for succeeded exchanges |
| exchangesFailed | true | activates counter for failed exchanges |
| exchangesTotal | true | activates counter for total count of exchanges |
| externalRedeliveries | true | activates counter for redeliveries of exchanges |
| failuresHandled | true | activates counter for handled failures |
| longTask | false | activates long task timer (current processing time for micrometer) |
| timerInitiator | null | Consumer<Timer.Builder> for custom initialize Timer |
| longTaskInitiator | null | Consumer<LongTaskTimer.Builder> for custom initialize LongTaskTimer |

If JMX is enabled in the CamelContext, the MBean is registered in the `type=services` tree with `name=MicrometerRoutePolicy`.

### Using Micrometer message history factory

`MicrometerMessageHistoryFactory` allows to use metrics to capture Message History performance statistics while routing messages. It works by using a Micrometer Timer for each node in all the routes. This factory can be used in Java and XML as the examples below demonstrates.

From Java, you set the factory to the `CamelContext` as shown below:

_Java-only: setting MicrometerMessageHistoryFactory on the CamelContext_

```java
context.setMessageHistoryFactory(new MicrometerMessageHistoryFactory());
```

And from XML DSL you define a <bean> as follows:

```xml
  <!-- use camel-micrometer message history to gather metrics for all messages being routed -->
  <bean id="metricsMessageHistoryFactory" class="org.apache.camel.component.micrometer.messagehistory.MicrometerMessageHistoryFactory"/>
```

The following options are supported on the factory:

  
| Name | Default | Description |
| --- | --- | --- |
| prettyPrint | false | Whether to use pretty print when outputting statistics in json format |
| meterRegistry |  | Allow using a shared `MeterRegistry`. If none is provided, then Camel will create a shared instance used by the CamelContext. |
| durationUnit | TimeUnit.MILLISECONDS | The unit to use for duration when dumping the statistics as json. |

At runtime the metrics can be accessed from Java API or JMX, which allows to gather the data as json output.

From Java code, you can get the service from the CamelContext as shown:

_Java-only: accessing MicrometerMessageHistoryService from the CamelContext_

```java
MicrometerMessageHistoryService service = context.hasService(MicrometerMessageHistoryService.class);
String json = service.dumpStatisticsAsJson();
```

If JMX is enabled in the CamelContext, the MBean is registered in the `type=services` tree with `name=MicrometerMessageHistory`.

### Micrometer event notification

There is a `MicrometerRouteEventNotifier` (counting added and running routes) and a `MicrometerExchangeEventNotifier` (timing exchanges from their creation to their completion).

EventNotifiers can be added to the CamelContext, e.g.:

_Java-only: adding MicrometerExchangeEventNotifier to the CamelContext_

```java
camelContext.getManagementStrategy().addEventNotifier(new MicrometerExchangeEventNotifier());
```

At runtime the metrics can be accessed from Java API or JMX, which allows to gather the data as json output.

From Java code, you can get the service from the CamelContext as shown:

_Java-only: accessing MicrometerEventNotifierService from the CamelContext_

```java
MicrometerEventNotifierService service = context.hasService(MicrometerEventNotifierService.class);
String json = service.dumpStatisticsAsJson();
```

If JMX is enabled in the CamelContext, the MBean is registered in the `type=services` tree with `name=MicrometerEventNotifier`.

The following options are supported on the factory:

  
| Name | Default | Description |
| --- | --- | --- |
| prettyPrint | false | Whether to use pretty print when outputting statistics in json format |
| meterRegistry |  | Allow using a shared `MeterRegistry`. If none is provided, then Camel will create a shared instance used by the CamelContext. |
| durationUnit | TimeUnit.MILLISECONDS | The unit to use for duration when dumping the statistics as json. |
| baseEndpointURI | true | Whether to use static or dynamic values for Endpoint Name tags in captured metrics. By default, static values are used. When using dynamic tags, then a dynamic to (toD) can compute many different endpoint URIs that, can lead to many tags as the URI is dynamic, so use this with care if setting this option to false. |

### Instrumenting Camel thread pools

`InstrumentedThreadPoolFactory` allows you to gather performance information about Camel Thread Pools by injecting a `InstrumentedThreadPoolFactory` which collects information from the inside of Camel. See more details at [Threading Model](../../manual/threading-model.md).

### Exposing Micrometer statistics in JMX

Micrometer uses `MeterRegistry` implementations to publish statistics. While in production scenarios it is advisable to select a dedicated backend like Prometheus or Graphite, it may be sufficient for test or local deployments to publish statistics to JMX.

To achieve this, add the following dependency:

```xml
    <dependency>
      <groupId>io.micrometer</groupId>
      <artifactId>micrometer-registry-jmx</artifactId>
      <version>${micrometer-version}</version>
    </dependency>
```

and add a `JmxMeterRegistry` instance:

-   Java
    
-   CDI
    

```java
    @Bean(name = "metricsRegistry")
    public MeterRegistry getMeterRegistry() {
        CompositeMeterRegistry meterRegistry = new CompositeMeterRegistry();
        meterRegistry.add(...);
        meterRegistry.add(new JmxMeterRegistry(
           CamelJmxConfig.DEFAULT,
           Clock.SYSTEM,
           HierarchicalNameMapper.DEFAULT));
        return meterRegistry;
    }
```

```java
    @Produces
    @Named("metricsRegistry"))
    public MeterRegistry getMeterRegistry() {
        CompositeMeterRegistry meterRegistry = new CompositeMeterRegistry();
        meterRegistry.add(...);
        meterRegistry.add(new JmxMeterRegistry(
           CamelJmxConfig.DEFAULT,
           Clock.SYSTEM,
           HierarchicalNameMapper.DEFAULT));
        return meterRegistry;
    }
```

The `HierarchicalNameMapper` strategy determines how meter name and tags are assembled into an MBean name.

### Using Camel Micrometer with Camel Main

When you use Camel standalone (`camel-main`), then if you need to expose metrics for Prometheus, then you can use `camel-micrometer-prometheus` JAR. And easily enable and configure this from `application.properties` as shown:

```properties
# enable HTTP management server with metrics
camel.management.enabled=true
camel.management.metricsEnabled=true

# turn on micrometer metrics
camel.metrics.enabled=true
# include more camel details
camel.metrics.enableMessageHistory=true
# include additional out-of-the-box micrometer metrics for cpu, jvm and used file descriptors
camel.metrics.binders=processor,jvm-info,file-descriptor
```

### Using Camel Micrometer with Spring Boot

When you use `camel-micrometer-starter` with Spring Boot, then Spring Boot autoconfiguration will automatically enable metrics capture if a `io.micrometer.core.instrument.MeterRegistry` is available.

For example, to capture data with Prometheus, you can add the following dependency:

```xml
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
</dependency>
```

See the following table for options to specify what metrics to capture, or to turn it off.