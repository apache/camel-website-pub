# XQuery

**Since Camel 1.0**

**Both producer and consumer are supported**

Camel supports [XQuery](http://www.w3.org/TR/xquery/) component for message transformation

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

The XQuery component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use a custom Saxon configuration. |  | Configuration |
| **configurationProperties** (advanced) | To set custom Saxon configuration properties. |  | Map |
| **moduleURIResolver** (advanced) | To use the custom ModuleURIResolver. |  | ModuleURIResolver |

## Endpoint Options

The XQuery endpoint is configured using URI syntax:

xquery:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (common) | **Required** The name of the template to load from classpath or file system. |  | String |

### Query Parameters (32 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowStAX** (common) | Whether to allow using StAX mode. | false | boolean |
| **namespacePrefixes** (common) | Allows to control which namespace prefixes to use for a set of namespace mappings. |  | Map |
| **resultsFormat** (common) | 
What output result to use.

Enum values:

-   Bytes
    
-   BytesSource
    
-   DOM
    
-   DOMSource
    
-   List
    
-   String
    
-   StringSource
    





 | DOM | ResultFormat |
| **resultType** (common) | What output result to use defined as a class. |  | Class |
| **source** (common) | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| **stripsAllWhiteSpace** (common) | Whether to strip all whitespaces. | true | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **configuration** (advanced) | To use a custom Saxon configuration. |  | Configuration |
| **configurationProperties** (advanced) | To set custom Saxon configuration properties. |  | Map |
| **moduleURIResolver** (advanced) | To use the custom ModuleURIResolver. |  | ModuleURIResolver |
| **parameters** (advanced) | Additional parameters. |  | Map |
| **properties** (advanced) | Properties to configure the serialization parameters. |  | Properties |
| **staticQueryContext** (advanced) | To use a custom Saxon StaticQueryContext. |  | StaticQueryContext |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
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
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |

## Examples

-   Java
    
-   XML
    
-   YAML
    

```java
from("queue:foo")
  .filter().xquery("//foo")
    .to("queue:bar");
```

```xml
<route>
  <from uri="queue:foo"/>
  <filter>
    <xquery>//foo</xquery>
    <to uri="queue:bar"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: queue:foo
      steps:
        - filter:
            xquery:
              expression: //foo
            steps:
              - to:
                  uri: queue:bar
```

You can also use functions inside your query, in which case you need an explicit type conversion (otherwise you will get a `org.w3c.dom.DOMException: HIERARCHY_REQUEST_ERR`), by passing the Class as a second argument to the **xquery()** method.

_Java-only: xquery() with class literal parameter_

```java
from("direct:start")
  .recipientList().xquery("concat('mock:foo.', /person/@city)", String.class);
```

## Usage

### Variables

The IN message body will be set as the `contextItem`. Besides this, these Variables are also added as parameters:

  
| Variable | Type | Description |
| --- | --- | --- |
| `exchange` | Exchange | The current Exchange |
| `in.body` | Object | The In message’s body |
| `out.body` | Object | The OUT message’s body (if any) |
| `in.headers.*` | Object | You can access the value of exchange.in.headers with key **foo** by using the variable which name is in.headers.foo |
| `out.headers.*` | Object | You can access the value of exchange.out.headers with key **foo** by using the variable which name is out.headers.foo variable |
| `**key name**` | Object | Any exchange.properties and exchange.in.headers and any additional parameters set using `setParameters(Map)`. These parameters are added with their own key name, for instance, if there is an IN header with the key name **foo** then it is added as **foo**. |

### Using XML configuration

If you prefer to configure your routes in your Spring XML file, then you can use XPath expressions as follows

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:MyQueue")
    .filter().xquery("/foo:person[@name='James']")
        .to("mqseries:SomeOtherQueue");
```

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:foo="http://example.com/person"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">

  <camelContext id="camel" xmlns="http://activemq.apache.org/camel/schema/spring">
    <route>
      <from uri="activemq:MyQueue"/>
      <filter>
        <xquery>/foo:person[@name='James']</xquery>
        <to uri="mqseries:SomeOtherQueue"/>
      </filter>
    </route>
  </camelContext>
</beans>
```

```yaml
- route:
    from:
      uri: activemq:MyQueue
      steps:
        - filter:
            xquery:
              expression: "/foo:person[@name='James']"
            steps:
              - to:
                  uri: mqseries:SomeOtherQueue
```

Notice how we can reuse the namespace prefixes, **foo** in this case, in the XPath expression for easier namespace-based XQuery expressions!

When you use functions in your XQuery expression, you need an explicit type conversion which is done in the xml configuration via the **@type** attribute:

```xml
<xquery resultType="java.lang.String">concat('mock:foo.', /person/@city)</xquery>
```

### Using XQuery as an endpoint

Sometimes an XQuery expression can be quite large; it can essentially be used for Templating. So you may want to use an XQuery Endpoint, so you can route using XQuery templates.

The following example shows how to take a message of an ActiveMQ queue (MyQueue) and transform it using XQuery and send it to MQSeries.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:MyQueue")
    .to("xquery:com/acme/someTransform.xquery")
    .to("mqseries:SomeOtherQueue");
```

```xml
<camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
  <route>
    <from uri="activemq:MyQueue"/>
    <to uri="xquery:com/acme/someTransform.xquery"/>
    <to uri="mqseries:SomeOtherQueue"/>
  </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: activemq:MyQueue
      steps:
        - to:
            uri: xquery:com/acme/someTransform.xquery
        - to:
            uri: mqseries:SomeOtherQueue
```

### Loading script from external resource

You can externalize the script and have Apache Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g., to refer to a file on the classpath you can do:

_Java-only: setHeader with xquery() and class literal_

```java
.setHeader("myHeader").xquery("resource:classpath:myxquery.txt", String.class)
```

### Learning XQuery

XQuery is a very powerful language for querying, searching, sorting and returning XML. For help learning XQuery, try these tutorials

-   Mike Kay’s [XQuery Primer](http://www.stylusstudio.com/xquery_primer.md)
    
-   The W3Schools [XQuery Tutorial](https://www.w3schools.com/xml/xquery_intro.asp)
    

## Dependencies

To use XQuery in your Camel routes, you need to add the dependency on **camel-saxon**, which implements the XQuery language.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-saxon</artifactId>
  <version>x.x.x</version>
</dependency>
```