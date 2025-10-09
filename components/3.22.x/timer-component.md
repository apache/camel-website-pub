# Timer

**Since Camel 1.0**

**Only consumer is supported**

The Timer component is used to generate message exchanges when a timer fires. You can only consume events from this endpoint.

## URI format

timer:name\[?options\]

Where `name` is the name of the `Timer` object, which is created and shared across endpoints. So if you use the same name for all your timer endpoints, only one `Timer` object and thread will be used.

**Note:** The IN body of the generated exchange is `null`. So `exchange.getIn().getBody()` returns `null`.

> **Tip**
> **Advanced Scheduler**
>
> See also the [Quartz](quartz-component.md) component that supports much more advanced scheduling.

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

The Timer component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Timer endpoint is configured using URI syntax:

timer:timerName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **timerName** (consumer) | **Required** The name of the timer. |  | String |

### Query Parameters (13 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **delay** (consumer) | Delay before first event is triggered. | 1000 | long |
| **fixedRate** (consumer) | Events take place at approximately regular intervals, separated by the specified period. | false | boolean |
| **includeMetadata** (consumer) | Whether to include metadata in the exchange such as fired time, timer name, timer count etc. This information is default included. | true | boolean |
| **period** (consumer) | If greater than 0, generate periodic events every period. | 1000 | long |
| **repeatCount** (consumer) | Specifies a maximum limit of number of fires. So if you set it to 1, the timer will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. |  | long |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **daemon** (advanced) | Specifies whether or not the thread associated with the timer endpoint runs as a daemon. The default value is true. | true | boolean |
| **pattern** (advanced) | Allows you to specify a custom Date pattern to use for setting the time option using URI syntax. |  | String |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **time** (advanced) | A java.util.Date the first event should be generated. If using the URI, the pattern expected is: yyyy-MM-dd HH:mm:ss or yyyy-MM-dd’T’HH:mm:ss. |  | Date |
| **timer** (advanced) | To use a custom Timer. |  | Timer |

## Message Headers

The Timer component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **firedTime** (consumer) Constant: [`HEADER_FIRED_TIME`](https://javadoc.io/doc/org.apache.camel/camel-timer/latest/org/apache/camel/component/timer/TimerConstants.html#HEADER_FIRED_TIME) | The fired time. |  | Date |
| **CamelMessageTimestamp** (consumer) Constant: [`HEADER_MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-timer/latest/org/apache/camel/component/timer/TimerConstants.html#HEADER_MESSAGE_TIMESTAMP) | The timestamp of the message. |  | long |

## Exchange Properties

When the timer is fired, it adds the following information as properties to the `Exchange`:

  
| Name | Type | Description |
| --- | --- | --- |
| `Exchange.TIMER_NAME` | `String` | The value of the `name` option. |
| `Exchange.TIMER_TIME` | `Date` | The value of the `time` option. |
| `Exchange.TIMER_PERIOD` | `long` | The value of the `period` option. |
| `Exchange.TIMER_FIRED_TIME` | `Date` | The time when the consumer fired. |
| `Exchange.TIMER_COUNTER` | `Long` | The current fire counter. Starts from 1. |

## Sample

To set up a route that generates an event every 60 seconds:

```java
from("timer://foo?fixedRate=true&period=60000").to("bean:myBean?method=someMethodName");
```

The above route will generate an event and then invoke the `someMethodName` method on the bean called `myBean` in the Registry.

And the route in Spring DSL:

```xml
<route>
  <from uri="timer://foo?fixedRate=true&amp;period=60000"/>
  <to uri="bean:myBean?method=someMethodName"/>
</route>
```

## Firing as soon as possible

**Since Camel 2.17**

You may want to fire messages in a Camel route as soon as possible you can use a negative delay:

```xml
<route>
  <from uri="timer://foo?delay=-1"/>
  <to uri="bean:myBean?method=someMethodName"/>
</route>
```

In this way the timer will fire messages immediately.

You can also specify a `repeatCount` parameter in conjunction with a negative delay to stop firing messages after a fixed number has been reached.

If you don’t specify a `repeatCount` then the timer will continue firing messages until the route will be stopped.

## Firing only once

You may want to fire a message in a Camel route only once, such as when starting the route. To do that you use the `repeatCount` option as shown:

```xml
<route>
  <from uri="timer://foo?repeatCount=1"/>
  <to uri="bean:myBean?method=someMethodName"/>
</route>
```

## Spring Boot Auto-Configuration

When using timer with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-timer-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.timer.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.timer.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.timer.enabled** | Whether to enable auto configuration of the timer component. This is enabled by default. |  | Boolean |