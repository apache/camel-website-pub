# MicroProfile Metrics

> **Warning**
> **Deprecated:** This microprofile-metrics is deprecated and may be removed in a future release.

**Since Camel 3.0**

**Only producer is supported**

The MircoProfile Metrics component provides the capability to expose metrics from Camel routes.

Maven users need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-microprofile-metrics</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

It is expected that the component is running in a MicroProfile environment that provides an appropriate implementation of MicroProfile Metrics 2.0. E.g [SmallRye Metrics](https://github.com/smallrye/smallrye-metrics).

## URI format

microprofile-metrics:\[ concurrent gauge | counter | gauge | histogram | meter | timer \]:metricname\[?options\]

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

The MicroProfile Metrics component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **metricRegistry** (advanced) | Use a custom MetricRegistry. |  | MetricRegistry |

## Endpoint Options

The MicroProfile Metrics endpoint is configured using URI syntax:

microprofile-metrics:metricType:metricName

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **metricType** (producer) | 
**Required** Metric type.

Enum values:

-   concurrent gauge
    
-   counter
    
-   gauge
    
-   meter
    
-   histogram
    
-   timer
    
-   simple timer
    
-   invalid
    





 |  | MetricType |
| **metricName** (producer) | **Required** Metric name. |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | Action to use when using the timer type. |  | String |
| **counterIncrement** (producer) | Increment value when using the counter type. |  | Long |
| **description** (producer) | Metric description. |  | String |
| **displayName** (producer) | Metric display name. |  | String |
| **gaugeDecrement** (producer) | Decrement metric value when using concurrent gauge type. |  | Boolean |
| **gaugeIncrement** (producer) | Increment metric value when using the concurrent gauge type. |  | Boolean |
| **gaugeValue** (producer) | Decrement metric value when using concurrent gauge type. |  | Number |
| **mark** (producer) | Mark value to set when using the meter type. |  | Long |
| **metricUnit** (producer) | Metric unit. See org.eclipse.microprofile.metrics.MetricUnits. |  | String |
| **tags** (producer) | Comma delimited list of tags associated with the metric in the format tagName=tagValue. |  | String |
| **value** (producer) | Value to set when using the histogram type. |  | Long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The MicroProfile Metrics component supports 13 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMicroProfileMetricsCounterIncrement** (producer) Constant: [`HEADER_COUNTER_INCREMENT`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_COUNTER_INCREMENT) | Override increment value in URI. |  | long |
| **CamelMicroProfileMetricsGaugeIncrement** (producer) Constant: [`HEADER_GAUGE_INCREMENT`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_GAUGE_INCREMENT) | Override gaugeIncrement value from the URI. |  | Boolean |
| **CamelMicroProfileMetricsGaugeDecrement** (producer) Constant: [`HEADER_GAUGE_DECREMENT`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_GAUGE_DECREMENT) | Override gaugeDecrement value from the URI. |  | Boolean |
| **CamelMicroProfileMetricsGaugeValue** (producer) Constant: [`HEADER_GAUGE_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_GAUGE_VALUE) | Override gaugeValue value from the URI. |  | Number |
| **CamelMicroProfileMetricsHistogramValue** (producer) Constant: [`HEADER_HISTOGRAM_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_HISTOGRAM_VALUE) | Override histogram value from the URI. |  | Long |
| **CamelMicroProfileMetricsMeterMark** (producer) Constant: [`HEADER_METER_MARK`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_METER_MARK) | Override meter mark value from the URI. |  | Long |
| **CamelMicroProfileMetricsDescription** (producer) Constant: [`HEADER_METRIC_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_METRIC_DESCRIPTION) | The description within the metric metadata. |  | String |
| **CamelMicroProfileMetricsDisplayName** (producer) Constant: [`HEADER_METRIC_DISPLAY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_METRIC_DISPLAY_NAME) | The display name within the metric metadata. |  | String |
| **CamelMicroProfileMetricsName** (producer) Constant: [`HEADER_METRIC_NAME`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_METRIC_NAME) | The name of the metric. |  | String |
| **CamelMicroProfileMetricsTags** (producer) Constant: [`HEADER_METRIC_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_METRIC_TAGS) | The tags of the metric. |  | String |
| **CamelMicroProfileMetricsType** (producer) Constant: [`HEADER_METRIC_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_METRIC_TYPE) | 
The type of the metric.

Enum values:

-   concurrent gauge
    
-   counter
    
-   gauge
    
-   meter
    
-   histogram
    
-   timer
    
-   simple timer
    
-   invalid
    





 |  | MetricType |
| **CamelMicroProfileMetricsUnits** (producer) Constant: [`HEADER_METRIC_UNIT`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_METRIC_UNIT) | The metric unit within the metric metadata. |  | String |
| **CamelMicroProfileMetricsTimerAction** (producer) Constant: [`HEADER_TIMER_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-microprofile-metrics/latest/org/apache/camel/component/microprofile/metrics/MicroProfileMetricsConstants.html#HEADER_TIMER_ACTION) | 

Override time action from the URI.

Enum values:

-   START
    
-   STOP
    





 |  | TimerAction |

## MetricRegistry Configuration

Configure a `MetricRegistry` to use either by passing it to the MicroProfileMetricsComponent.

```java
MicroProfileMetricsComponent component = new MicroProfileMetricsComponent();
component.setRegistry(myMetricRegistryImpl);
```

Or by binding it to the Camel registry using the binding name 'metricRegistry' (See `MicroProfileMetricsConstants.METRIC_REGISTRY_NAME`).

## Default Camel Metrics

Some Camel specific metrics are available out of the box.

  
| Name | Type | Description |
| --- | --- | --- |
| application\_camel\_message\_history\_processing | timer | Sample of performance of each node in the route when message history is enabled |
| application\_camel\_route\_count | gauge | Number of routes added |
| application\_camel\_route\_running\_count | gauge | Number of routes runnning |
| application\_camel\_\[route or context\]\_exchanges\_inflight\_count | gauge | Route inflight messages for a CamelContext or a route |
| application\_camel\_\[route or context\]\_exchanges\_total | counter | Total number of processed exchanges for a CamelContext or a route |
| application\_camel\_\[route or context\]\_exchanges\_completed\_total | counter | Number of successfully completed exchange for a CamelContext or a route |
| application\_camel\_\[route or context\]\_exchanges\_failed\_total | counter | Number of failed exchanges for a CamelContext or a route |
| application\_camel\_\[route or context\]\_failuresHandled\_total | counter | Number of failures handled for a CamelContext or a route |
| application\_camel\_\[route or context\]\_externalRedeliveries\_total | counter | Number of external initiated redeliveries (such as from JMS broker) for a CamelContext or a route |
| application\_camel\_context\_status | gauge | The status of the Camel Context |
| application\_camel\_context\_uptime\_seconds | gauge | The amount of time since the Camel Context was started |
| application\_camel\_\[route or exchange\]_processing_\[rate\_per\_second or one\_min\_rate\_per\_second or five\_min\_rate\_per\_second or fifteen\_min\_rate\_per\_second or min\_seconds or max\_seconds or mean\_second or stddev\_seconds\] | gauge | Exchange message or route processing with multiple options |
| application\_camel\_\[route or exchange\]\_processing\_seconds | summary | Exchange message or route processing metric |

## Counter

microprofile-metrics:counter:name\[?options\]

### Options

  
| Name | Default | Description |
| --- | --- | --- |
| counterIncrement | \- | Value to add to the counter |

If `counterIncrement` is not defined then counter value will be incremented by one.

```java
// Increment counter simple.counter by 7
from("direct:in")
    .to("microprofile-metrics:counter:simple.counter?counterIncrement=7")
    .to("direct:out");
```

```java
// Increment counter simple.counter by 1
from("direct:in")
    .to("microprofile-metrics:counter:simple.counter")
    .to("direct:out");
```

### Headers

Message headers can be used to override the `counterIncrement` values specified on the `microprofile-metrics` endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMicroProfileMetricsCounterIncrement | Override increment value from the URI | Long |

```java
// Increment counter simple.counter by 417
from("direct:in")
    .setHeader(MicroProfileMetricsConstants.HEADER_COUNTER_INCREMENT, constant(417))
    .to("microprofile-metrics:counter:simple.counter?increment=7")
    .to("direct:out");
```

## Concurrent Gauge

microprofile-metrics:concurrent gauge:name\[?options\]

### Options

  
| Name | Default | Description |
| --- | --- | --- |
| gaugeIncrement | false | Value to add to the counter |
| gaugeDecrement | false | Value to add to the counter |

If neither `gaugeIncrement` or `gaugeDecrement` are defined then no action is performed on the gauge.

```java
// Increment concurrent gauge simple.gauge by 1
from("direct:in")
    .to("microprofile-metrics:concurrent gauge:simple.gauge?gaugeIncrement=true")
    .to("direct:out");
```

```java
// Decrement concurrent gauge simple.gauge by 1
from("direct:in")
    .to("microprofile-metrics:concurrent gauge:simple.gauge?gaugeDecrement=true")
    .to("direct:out");
```

### Headers

Message headers can be used to override the `gaugeIncrement` and `gaugeDecrement` values specified on the `microprofile-metrics` endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMicroProfileMetricsGaugeIncrement | Override gaugeIncrement value from the URI | Boolean |
| CamelMicroProfileMetricsGaugeDecrement | Override gaugeDecrement value from the URI | Boolean |

```java
// Increment concurrent gauge simple.gauge by 1
from("direct:in")
    .setHeader(MicroProfileMetricsConstants.HEADER_GAUGE_INCREMENT, constant(true))
    .to("microprofile-metrics:concurrent gauge:simple.gauge")
    .to("direct:out");

// Decrement concurrent gauge simple.gauge by 1
from("direct:in")
    .setHeader(MicroProfileMetricsConstants.HEADER_GAUGE_DECREMENT, constant(true))
    .to("microprofile-metrics:concurrent gauge:simple.gauge")
    .to("direct:out");
```

## Gauge

microprofile-metrics:gauge:name\[?options\]

### Options

  
| Name | Default | Description |
| --- | --- | --- |
| gaugeValue | false | Value to set the gauge to |

If `gaugeValue` is not defined then no action is performed on the gauge.

```java
// Set gauge simple.gauge value to 10
from("direct:in")
    .to("microprofile-metrics:gauge:simple.gauge?gaugeValue=10")
    .to("direct:out");
```

### Headers

Message headers can be used to override the `gaugeValue` value specified on the `microprofile-metrics` endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMicroProfileMetricsGaugeValue | Override gaugeValue value from the URI | Number |

```java
// Set gauge simple.gauge value to 10
from("direct:in")
    .setHeader(MicroProfileMetricsConstants.HEADER_GAUGE_VALUE, constant(10))
    .to("microprofile-metrics:gauge:simple.gauge")
    .to("direct:out");
```

## Histogram

microprofile-metrics:histogram:name\[?options\]

### Options

  
| Name | Default | Description |
| --- | --- | --- |
| value | \- | Value to set on the histogram |

If `value` is not defined then histogram value will not be changed.

```java
// Set histogram simple.histogram to 7
from("direct:in")
    .to("microprofile-metrics:histogram:simple.histogram?value=7")
    .to("direct:out");
```

### Headers

Message headers can be used to override the `value` specified on the `microprofile-metrics` endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMicroProfileMetricsHistogramValue | Override histogram value from the URI | Long |

```java
// Set histogram simple.histogram to 417
from("direct:in")
    .setHeader(MicroProfileMetricsConstants.HEADER_HISTOGRAM_VALUE, constant(417))
    .to("microprofile-metrics:histogram:simple.histogram?value=7")
    .to("direct:out");
```

## Meter

microprofile-metrics:meter:name\[?options\]

### Options

  
| Name | Default | Description |
| --- | --- | --- |
| mark | \- | Mark value to set on the meter |

If `mark` is not defined then the meter will be marked with the value '1'.

```java
// Mark the meter simple.meter with 7
from("direct:in")
    .to("microprofile-metrics:meter:simple.meter?mark=7")
    .to("direct:out");
```

```java
// Mark the meter simple.meter with 1
from("direct:in")
    .to("microprofile-metrics:meter:simple.meter")
    .to("direct:out");
```

### Headers

Message headers can be used to override the `value` specified on the `microprofile-metrics` endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMicroProfileMetricsMeterMark | Override meter mark value from the URI | Long |

```java
// Mark the meter simple.meter with 417
from("direct:in")
    .setHeader(MicroProfileMetricsConstants.HEADER_METER_MARK, constant(417))
    .to("microprofile-metrics:meter:simple.meter?value=7")
    .to("direct:out");
```

## Timer

microprofile-metrics:timer:name\[?options\]

### Options

  
| Name | Default | Description |
| --- | --- | --- |
| action | \- | start or stop |

If no `action` is specified or it’s an invalid value, then no timer update occurs.

If the `start` action is called on an already running timer or `stop` is called on an unknown timer, then no timer(s) are updated.

```java
// Measure time spent in route `direct:calculate`
from("direct:in")
    .to("microprofile-metrics:timer:simple.timer?action=start")
    .to("direct:calculate")
    .to("microprofile-metrics:timer:simple.timer?action=stop");
```

### Headers

Message headers can be used to override the `action` specified on the `microprofile-metrics` endpoint URI.

  
| Name | Description | Expected type |
| --- | --- | --- |
| CamelMicroProfileMetricsTimerAction | Override time action from the URI | org.apache.camel.component.microprofile.metrics.TimerAction |

```java
// Mark the meter simple.meter with 417
from("direct:in")
    .setHeader(MicroProfileMetricsConstants.HEADER_TIMER_ACTION, TimerAction.START)
    .to("microprofile-metrics:timer:simple.timer")
    .to("direct:out");
```

## MicroProfileMetricsRoutePolicyFactory

This factory allows to add a RoutePolicy for each route and exposes route utilization statistics using MicroProfile metrics.

> **Note**
> Instead of using the MicroProfileMetricsRoutePolicyFactory you can define a MicroProfileMetricsRoutePolicy per route you want to instrument, in case you only want to instrument a few selected routes.

Add the factory to the `CamelContext` as shown below:

```java
context.addRoutePolicyFactory(new MicroProfileMetricsRoutePolicyFactory());
```

## MicroProfileMetricsMessageHistoryFactory

This factory captures message history performance statistics while routing messages.

Add the factory to the `CamelContext` as shown below:

```java
context.setMessageHistoryFactory(new MicroProfileMetricsMessageHistoryFactory());
```

## MicroProfileMetricsExchangeEventNotifier

The exchange event notifier times exchanges from creation through to completion.

EventNotifiers can be added to the `CamelContext`, e.g.:

```java
camelContext.getManagementStrategy().addEventNotifier(new MicroProfileMetricsExchangeEventNotifier())
```

## MicroProfileMetricsRouteEventNotifier

The route event notifier counts added and running routes within the `CamelContext`.

EventNotifiers can be added to the `CamelContext`, e.g.:

```java
camelContext.getManagementStrategy().addEventNotifier(new MicroProfileMetricsRouteEventNotifier())
```

## MicroProfileMetricsCamelContextEventNotifier

The Camel Context event notifier adds some basic metrics about the state of the `CamelContext`.

EventNotifiers can be added to the `CamelContext`, e.g.:

```java
camelContext.getManagementStrategy().addEventNotifier(new MicroProfileMetricsCamelContextEventNotifier())
```