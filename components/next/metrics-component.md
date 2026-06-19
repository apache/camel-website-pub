# Metrics

**Since Camel 2.14**

**Only producer is supported**

The Metrics component allows collecting various metrics directly from Camel routes. Supported metric types are [counter](#MetricsComponent-counter), [histogram](#MetricsComponent-histogram), [meter](#MetricsComponent-meter), [timer](#MetricsComponent-timer) and [gauge](#MetricsComponent-gauge). [Metrics](http://metrics.dropwizard.io) provides a simple way to measure the behaviour of applications. The configurable reporting backend enables different integration options for collecting and visualizing statistics. The component also provides a `MetricsRoutePolicyFactory` which allows exposing route statistics using Dropwizard Metrics, see bottom of page for details.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-metrics</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

metrics:\[ meter | counter | histogram | timer | gauge \]:metricname\[?options\]

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

The Metrics component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **metricRegistry** (advanced) | To use a custom configured MetricRegistry. |  | MetricRegistry |

## Endpoint Options

The Metrics endpoint is configured using URI syntax:

metrics:metricsType:metricsName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **metricsType** (producer) | 
**Required** Type of metrics.

Enum values:

-   gauge
    
-   counter
    
-   histogram
    
-   meter
    
-   timer
    





 |  | MetricsType |
| **metricsName** (producer) | **Required** Name of metrics. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
Action when using timer type.

Enum values:

-   start
    
-   stop
    





 |  | MetricsTimerAction |
| **decrement** (producer) | Decrement value when using counter type. |  | Long |
| **increment** (producer) | Increment value when using counter type. |  | Long |
| **mark** (producer) | Mark when using meter type. |  | Long |
| **subject** (producer) | Subject value when using gauge type. |  | Object |
| **value** (producer) | Value value when using histogram type. |  | Long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Metrics component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMetricsTimerAction** (producer) Constant: [`HEADER_TIMER_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-metrics/latest/org/apache/camel/component/metrics/MetricsConstants.html#HEADER_TIMER_ACTION) | 
Override timer action in URI.

Enum values:

-   start
    
-   stop
    





 |  | MetricsTimerAction |
| **CamelMetricsMeterMark** (producer) Constant: [`HEADER_METER_MARK`](https://javadoc.io/doc/org.apache.camel/camel-metrics/latest/org/apache/camel/component/metrics/MetricsConstants.html#HEADER_METER_MARK) | Override mark value in URI. |  | long |
| **CamelMetricsHistogramValue** (producer) Constant: [`HEADER_HISTOGRAM_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-metrics/latest/org/apache/camel/component/metrics/MetricsConstants.html#HEADER_HISTOGRAM_VALUE) | Override histogram value in URI. |  | long |
| **CamelMetricsCounterDecrement** (producer) Constant: [`HEADER_COUNTER_DECREMENT`](https://javadoc.io/doc/org.apache.camel/camel-metrics/latest/org/apache/camel/component/metrics/MetricsConstants.html#HEADER_COUNTER_DECREMENT) | Override decrement value in URI. |  | long |
| **CamelMetricsCounterIncrement** (producer) Constant: [`HEADER_COUNTER_INCREMENT`](https://javadoc.io/doc/org.apache.camel/camel-metrics/latest/org/apache/camel/component/metrics/MetricsConstants.html#HEADER_COUNTER_INCREMENT) | Override increment value in URI. |  | long |
| **CamelMetricsGaugeSubject** (producer) Constant: [`HEADER_GAUGE_SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-metrics/latest/org/apache/camel/component/metrics/MetricsConstants.html#HEADER_GAUGE_SUBJECT) | Override subject value in URI. |  | Object |
| **CamelMetricsName** (producer) Constant: [`HEADER_METRIC_NAME`](https://javadoc.io/doc/org.apache.camel/camel-metrics/latest/org/apache/camel/component/metrics/MetricsConstants.html#HEADER_METRIC_NAME) | Override name value in URI. |  | String |

## Metric Registry

Camel Metrics component uses by default a `MetricRegistry` instance with a `Slf4jReporter` that has a 60-second reporting interval. This default registry can be replaced with a custom one by providing a `MetricRegistry` bean. If multiple `MetricRegistry` beans exist in the application, the one with name `metricRegistry` is used.

## Usage

Each metric has type and name. Supported types are [counter](#MetricsComponent-counter), [histogram](#MetricsComponent-histogram), [meter](#MetricsComponent-meter), [timer](#MetricsComponent-timer) and [gauge](#MetricsComponent-gauge). Metric name is simple string. If a metric type is not provided, then type meter is used by default.

### Headers

Metric name defined in URI can be overridden by using header with name `CamelMetricsName`.

For example

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("CamelMetricsName").constant("new.name")
    .to("metrics:counter:name.not.used")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsName">
    <constant>new.name</constant>
  </setHeader>
  <to uri="metrics:counter:name.not.used"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelMetricsName
            constant: new.name
        - to:
            uri: metrics:counter:name.not.used
        - to:
            uri: direct:out
```

will update counter with name `new.name` instead of `name.not.used`.

All Metrics specific headers are removed from the message once Metrics endpoint finishes processing of exchange. While processing exchange Metrics endpoint will catch all exceptions and write log entry using level `warn`.

### Metrics type counter

metrics:counter:metricname\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| increment | \- | Long value to add to the counter |
| decrement | \- | Long value to subtract from the counter |

If neither `increment` or `decrement` is defined then the value of the counter will be incremented by one. If `increment` and `decrement` are both defined only increment operation is called.

-   Java
    
-   XML
    
-   YAML
    

```java
// update counter simple.counter by 7
from("direct:in")
    .to("metrics:counter:simple.counter?increment=7")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="metrics:counter:simple.counter?increment=7"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: metrics:counter:simple.counter
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
    .to("metrics:counter:simple.counter")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="metrics:counter:simple.counter"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: metrics:counter:simple.counter
        - to:
            uri: direct:out
```

-   Java
    
-   XML
    
-   YAML
    

```java
// decrement counter simple.counter by 3
from("direct:in")
    .to("metrics:counter:simple.counter?decrement=3")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="metrics:counter:simple.counter?decrement=3"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: metrics:counter:simple.counter
            parameters:
              decrement: 3
        - to:
            uri: direct:out
```

#### Headers

Message headers can be used to override `increment` and `decrement` values specified in Metrics component URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsCounterIncrement | Override increment value in URI | Long |
| CamelMetricsCounterDecrement | Override decrement value in URI | Long |

-   Java
    
-   XML
    
-   YAML
    

```java
// update counter simple.counter by 417
from("direct:in")
    .setHeader("CamelMetricsCounterIncrement").constant(417L)
    .to("metrics:counter:simple.counter?increment=7")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsCounterIncrement">
    <constant resultType="java.lang.Long">417</constant>
  </setHeader>
  <to uri="metrics:counter:simple.counter?increment=7"/>
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
            uri: metrics:counter:simple.counter
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
    .to("metrics:counter:body.length")
    .to("mock:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsCounterIncrement">
    <simple>${body.length}</simple>
  </setHeader>
  <to uri="metrics:counter:body.length"/>
  <to uri="mock:out"/>
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
            uri: metrics:counter:body.length
        - to:
            uri: mock:out
```

### Metric type histogram

metrics:histogram:metricname\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| value | \- | Value to use in histogram |

If `value` is not set, nothing is added to histogram and warning is logged.

-   Java
    
-   XML
    
-   YAML
    

```java
// adds value 9923 to simple.histogram
from("direct:in")
    .to("metrics:histogram:simple.histogram?value=9923")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="metrics:histogram:simple.histogram?value=9923"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: metrics:histogram:simple.histogram
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
    .to("metrics:histogram:simple.histogram")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="metrics:histogram:simple.histogram"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: metrics:histogram:simple.histogram
        - to:
            uri: direct:out
```

#### Headers

Message header can be used to override value specified in Metrics component URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsHistogramValue | Override histogram value in URI | Long |

-   Java
    
-   XML
    
-   YAML
    

```java
// adds value 992 to simple.histogram
from("direct:in")
    .setHeader("CamelMetricsHistogramValue", constant(992L))
    .to("metrics:histogram:simple.histogram?value=700")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsHistogramValue">
    <constant resultType="java.lang.Long">992</constant>
  </setHeader>
  <to uri="metrics:histogram:simple.histogram?value=700"/>
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
            uri: metrics:histogram:simple.histogram
            parameters:
              value: 700
        - to:
            uri: direct:out
```

### Metric type meter

metrics:meter:metricname\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| mark | \- | Long value to use as mark |

If `mark` is not set then `meter.mark()` is called without argument.

-   Java
    
-   XML
    
-   YAML
    

```java
// marks simple.meter without value
from("direct:in")
    .to("metrics:simple.meter")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="metrics:simple.meter"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: metrics:simple.meter
        - to:
            uri: direct:out
```

-   Java
    
-   XML
    
-   YAML
    

```java
// marks simple.meter with value 81
from("direct:in")
    .to("metrics:meter:simple.meter?mark=81")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="metrics:meter:simple.meter?mark=81"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: metrics:meter:simple.meter
            parameters:
              mark: 81
        - to:
            uri: direct:out
```

#### Headers

Message header can be used to override `mark` value specified in Metrics component URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsMeterMark | Override mark value in URI | Long |

-   Java
    
-   XML
    
-   YAML
    

```java
// updates meter simple.meter with value 345
from("direct:in")
    .setHeader("CamelMetricsMeterMark", constant(345L))
    .to("metrics:meter:simple.meter?mark=123")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsMeterMark">
    <constant resultType="java.lang.Long">345</constant>
  </setHeader>
  <to uri="metrics:meter:simple.meter?mark=123"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelMetricsMeterMark
            constant: 345
        - to:
            uri: metrics:meter:simple.meter
            parameters:
              mark: 123
        - to:
            uri: direct:out
```

### Metrics type timer

metrics:timer:metricname\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| action | \- | start or stop |

If no `action` or invalid value is provided then warning is logged without any timer update. If action `start` is called on already running timer or `stop` is called on not running timer then nothing is updated and warning is logged.

-   Java
    
-   XML
    
-   YAML
    

```java
// measure time taken by route "calculate"
from("direct:in")
    .to("metrics:timer:simple.timer?action=start")
    .to("direct:calculate")
    .to("metrics:timer:simple.timer?action=stop");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="metrics:timer:simple.timer?action=start"/>
  <to uri="direct:calculate"/>
  <to uri="metrics:timer:simple.timer?action=stop"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: metrics:timer:simple.timer
            parameters:
              action: start
        - to:
            uri: direct:calculate
        - to:
            uri: metrics:timer:simple.timer
            parameters:
              action: stop
```

`TimerContext` objects are stored as Exchange properties between different Metrics component calls.

#### Headers

Message header can be used to override action value specified in Metrics component URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsTimerAction | Override timer action in URI | `org.apache.camel.component.metrics.MetricsTimerAction` |

-   Java
    
-   XML
    
-   YAML
    

```java
// sets timer action using header
from("direct:in")
    .setHeader("CamelMetricsTimerAction").constant("start")
    .to("metrics:timer:simple.timer")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsTimerAction">
    <constant>start</constant>
  </setHeader>
  <to uri="metrics:timer:simple.timer"/>
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
            uri: metrics:timer:simple.timer
        - to:
            uri: direct:out
```

### Metric type gauge

metrics:gauge:metricname\[?options\]

#### Options

  
| Name | Default | Description |
| --- | --- | --- |
| subject | \- | Any object to be observed by the gauge |

If `subject` is not defined it’s simply ignored, i.e., the gauge is not registered.

-   Java
    
-   XML
    
-   YAML
    

```java
// update gauge "simple.gauge" by a bean "mySubjectBean"
from("direct:in")
    .to("metrics:gauge:simple.gauge?subject=#mySubjectBean")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="metrics:gauge:simple.gauge?subject=#mySubjectBean"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: metrics:gauge:simple.gauge
            parameters:
              subject: "#mySubjectBean"
        - to:
            uri: direct:out
```

#### Headers

Message headers can be used to override `subject` values specified in Metrics component URI. Note: if `CamelMetricsName` header is specified, then new gauge is registered in addition to default one specified in a URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMetricsGaugeSubject | Override subject value in URI | Object |

-   Java
    
-   XML
    
-   YAML
    

```java
// update gauge simple.gauge by a String literal "myUpdatedSubject"
from("direct:in")
    .setHeader("CamelMetricsGaugeSubject").constant("myUpdatedSubject")
    .to("metrics:counter:simple.gauge?subject=#mySubjectBean")
    .to("direct:out");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMetricsGaugeSubject">
    <constant>myUpdatedSubject</constant>
  </setHeader>
  <to uri="metrics:counter:simple.gauge?subject=#mySubjectBean"/>
  <to uri="direct:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelMetricsGaugeSubject
            constant: myUpdatedSubject
        - to:
            uri: metrics:counter:simple.gauge
            parameters:
              subject: "#mySubjectBean"
        - to:
            uri: direct:out
```

### MetricsRoutePolicyFactory

This factory allows adding a `RoutePolicy` for each route that exposes route utilization statistics using Dropwizard metrics. This factory can be used in Java and XML as the examples below demonstrates.

> **Note**
> Instead of using the `MetricsRoutePolicyFactory` you can define a MetricsRoutePolicy per route you want to instrument, in case you only want to instrument a few selected routes.

From Java, you add the factory to the `CamelContext` as shown below:

_Java-only: adding MetricsRoutePolicyFactory to CamelContext_

```java
context.addRoutePolicyFactory(new MetricsRoutePolicyFactory());
```

And from XML DSL you define a <bean> as follows:

```xml
  <!-- use camel-metrics route policy to gather metrics for all routes -->
  <bean id="metricsRoutePolicyFactory" class="org.apache.camel.component.metrics.routepolicy.MetricsRoutePolicyFactory"/>
```

The `MetricsRoutePolicyFactory` and `MetricsRoutePolicy` supports the following options:

  
| Name | Default | Description |
| --- | --- | --- |
| useJmx | false | Whether to report fine-grained statistics to JMX by using the `com.codahale.metrics.JmxReporter`.  
Notice that if JMX is enabled on CamelContext then a `MetricsRegistryService` mbean is enlisted under the services type in the JMX tree. That mbean has a single operation to output the statistics using json. Setting `useJmx` to true is only needed if you want fine-grained mbeans per statistics type. |
| jmxDomain | org.apache.camel.metrics | The JMX domain name |
| prettyPrint | false | Whether to use pretty print when outputting statistics in json format |
| metricsRegistry |  | Allow using a shared `com.codahale.metrics.MetricRegistry`. If none is provided, then Camel will create a shared instance used by the CamelContext. |
| rateUnit | TimeUnit.SECONDS | The unit to use for rate in the metrics reporter or when dumping the statistics as json. |
| durationUnit | TimeUnit.MILLISECONDS | The unit to use for duration in the metrics reporter or when dumping the statistics as json. |
| namePattern | `name.routeId.type` | **Camel 2.17:** The name pattern to use. Use dot as separators, but you can change that. The values `name`, `routeId`, and `type` will be replaced with actual value. Where `name` is the name of the CamelContext. `routeId` is the name of the route. And `type` is the value of responses. |

From Java code you can get hold of the `com.codahale.metrics.MetricRegistry` from the `org.apache.camel.component.metrics.routepolicy.MetricsRegistryService` as shown below:

_Java-only: accessing MetricRegistry from MetricsRegistryService_

```java
MetricRegistryService registryService = context.hasService(MetricsRegistryService.class);
if (registryService != null) {
  MetricsRegistry registry = registryService.getMetricsRegistry();
  ...
}
```

### MetricsMessageHistoryFactory

This factory allows using metrics to capture Message History performance statistics while routing messages. It works by using a metrics Timer for each node in all the routes. This factory can be used in Java and XML as the examples below demonstrates.

From Java, you set the factory to the `CamelContext` as shown below:

_Java-only: setting MetricsMessageHistoryFactory on CamelContext_

```java
context.setMessageHistoryFactory(new MetricsMessageHistoryFactory());
```

And from XML DSL you define a <bean> as follows:

```xml
  <!-- use camel-metrics message history to gather metrics for all messages being routed -->
  <bean id="metricsMessageHistoryFactory" class="org.apache.camel.component.metrics.messagehistory.MetricsMessageHistoryFactory"/>
```

The following options are supported on the factory:

  
| Name | Default | Description |
| --- | --- | --- |
| useJmx | false | Whether to report fine-grained statistics to JMX by using the `com.codahale.metrics.JmxReporter`.  
Notice that if JMX is enabled on CamelContext then a `MetricsRegistryService` mbean is enlisted under the services type in the JMX tree. That mbean has a single operation to output the statistics using json. Setting `useJmx` to true is only needed if you want fine-grained mbeans per statistics type. |
| jmxDomain | org.apache.camel.metrics | The JMX domain name |
| prettyPrint | false | Whether to use pretty print when outputting statistics in json format |
| metricsRegistry |  | Allow using a shared `com.codahale.metrics.MetricRegistry`. If none is provided, then Camel will create a shared instance used by the CamelContext. |
| rateUnit | TimeUnit.SECONDS | The unit to use for rate in the metrics reporter or when dumping the statistics as json. |
| durationUnit | TimeUnit.MILLISECONDS | The unit to use for duration in the metrics reporter or when dumping the statistics as json. |
| namePattern | `name.routeId.id.type` | The name pattern to use. Use dot as separators, but you can change that. The values `name`, `routeId`, `type`, and `id` will be replaced with actual value. Where `name` is the name of the CamelContext. `routeId` is the name of the route. The `id` pattern represents the node id. And `type` is the value of history. |

At runtime the metrics can be accessed from Java API or JMX, which allows to gather the data as json output.

From Java code, you can get the service from the CamelContext as shown:

_Java-only: dumping message history statistics as JSON_

```java
MetricsMessageHistoryService service = context.hasService(MetricsMessageHistoryService.class);
String json = service.dumpStatisticsAsJson();
```

And the JMX API the MBean is registered in the `type=services` tree with `name=MetricsMessageHistoryService`.

### InstrumentedThreadPoolFactory

This factory allows you to gather performance information about Camel Thread Pools by injecting a `InstrumentedThreadPoolFactory` which collects information from the inside of Camel. See more details at Advanced configuration of CamelContext using Spring