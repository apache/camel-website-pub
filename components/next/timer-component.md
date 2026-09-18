# Timer

**Since Camel 1.0**

**Only consumer is supported**

The Timer component is used to generate message exchanges when a timer fires. You can only consume events from this endpoint.

## URI format

timer:name\[?options\]

Where `name` is the name of the `Timer` object, which is created and shared across endpoints. So if you use the same name for all your timer endpoints, only one `Timer` object and thread will be used.

> **Note**
> The _IN_ body of the generated exchange is `null`. Therefore, calling `exchange.getIn().getBody()` returns `null`.

> **Tip**
> **Advanced Scheduler**
>
> See also the [Quartz](quartz-component.md) component that supports much more advanced scheduling.

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

The Timer component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **includeMetadata** (consumer) | Whether to include metadata in the exchange such as fired time, timer name, timer count etc. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Timer endpoint is configured using URI syntax:

timer:timerName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **timerName** (consumer) | **Required** The name of the timer. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **delay** (consumer) | The number of milliseconds to wait before the first event is generated. Should not be used in conjunction with the time option. The default value is 1000. | 1000 | long |
| **fixedRate** (consumer) | Events take place at approximately regular intervals, separated by the specified period. | false | boolean |
| **includeMetadata** (consumer) | Whether to include metadata in the exchange such as fired time, timer name, timer count etc. | false | boolean |
| **period** (consumer) | Generate periodic events every period. Must be zero or positive value. The default value is 1000. | 1000 | long |
| **repeatCount** (consumer) | Specifies a maximum limit for the number of fires. Therefore, if you set it to 1, the timer will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. |  | long |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **daemon** (advanced) | Specifies whether the thread associated with the timer endpoint runs as a daemon. The default value is true. | true | boolean |
| **pattern** (advanced) | Allows you to specify a custom Date pattern to use for setting the time option using URI syntax. |  | String |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **time** (advanced) | A java.util.Date the first event should be generated. If using the URI, the pattern expected is: yyyy-MM-dd HH:mm:ss or yyyy-MM-dd’T’HH:mm:ss. |  | Date |
| **timer** (advanced) | To use a custom Timer. |  | Timer |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |

## Message Headers

The Timer component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelTimerFiredTime** (consumer) Constant: [`HEADER_FIRED_TIME`](https://javadoc.io/doc/org.apache.camel/camel-timer/latest/org/apache/camel/component/timer/TimerConstants.html#HEADER_FIRED_TIME) | The fired time. |  | Date |
| **CamelMessageTimestamp** (consumer) Constant: [`HEADER_MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-timer/latest/org/apache/camel/component/timer/TimerConstants.html#HEADER_MESSAGE_TIMESTAMP) | The timestamp of the message. |  | long |

## Usage

### Exchange Properties

When the timer is fired, it adds the following information as properties to the `Exchange`:

  
| Name | Type | Description |
| --- | --- | --- |
| `Exchange.TIMER_NAME` | `String` | The value of the `name` option. |
| `Exchange.TIMER_TIME` | `Date` | The value of the `time` option. |
| `Exchange.TIMER_PERIOD` | `long` | The value of the `period` option. |
| `Exchange.TIMER_FIRED_TIME` | `Date` | The time when the consumer fired. |
| `Exchange.TIMER_COUNTER` | `Long` | The current fire counter. Starts from 1. |

## Example

To set up a route that generates an event every 60 seconds:

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer://foo?fixedRate=true&period=60000").to("bean:myBean?method=someMethodName");
```

```xml
<route>
  <from uri="timer://foo?fixedRate=true&amp;period=60000"/>
  <to uri="bean:myBean?method=someMethodName"/>
</route>
```

```yaml
- route:
    from:
      uri: timer:foo
      parameters:
        fixedRate: true
        period: 60000
      steps:
        - to:
            uri: bean:myBean
            parameters:
              method: someMethodName
```

The above route will generate an event and then invoke the `someMethodName` method on the bean called `myBean` in the Registry.

### Firing as soon as possible

You may want to fire messages in a Camel route as soon as possible, you can use a negative delay:

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer://foo?delay=-1").to("bean:myBean?method=someMethodName");
```

```xml
<route>
  <from uri="timer://foo?delay=-1"/>
  <to uri="bean:myBean?method=someMethodName"/>
</route>
```

```yaml
- route:
    from:
      uri: timer:foo
      parameters:
        delay: -1
      steps:
        - to:
            uri: bean:myBean
            parameters:
              method: someMethodName
```

In this way, the timer will fire messages immediately.

You can also specify a `repeatCount` parameter in conjunction with a negative delay to stop firing messages after a fixed number has been reached.

If you don’t specify a `repeatCount` then the timer will continue firing messages until the route will be stopped.

### Firing only once

You may want to fire a message in a Camel route only once, such as when starting the route. To do that, you use the `repeatCount` option as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer://foo?repeatCount=1").to("bean:myBean?method=someMethodName");
```

```xml
<route>
  <from uri="timer://foo?repeatCount=1"/>
  <to uri="bean:myBean?method=someMethodName"/>
</route>
```

```yaml
- route:
    from:
      uri: timer:foo
      parameters:
        repeatCount: 1
      steps:
        - to:
            uri: bean:myBean
            parameters:
              method: someMethodName
```