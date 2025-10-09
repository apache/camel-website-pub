# Log

How can I log the processing of a [Message](message.md)?

Camel provides many ways to log the fact that you are processing a message. Here are just a few examples:

-   You can use the [Log](../log-component.md) component which logs the Message content.
    
-   You can use the [Tracer](../../../manual/tracer.md) which trace logs message flow.
    
-   You can also use a [Processor](../../../manual/processor.md) or [Bean](../../../manual/bean-binding.md) and log from Java code.
    
-   You can use this log EIP.
    

## Options

The Log eip supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **message** | **Required** Sets the log message (uses simple language). |  | String |
| **loggingLevel** | 
Sets the logging level. The default value is INFO.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | INFO | LoggingLevel |
| **logName** | Sets the name of the logger. |  | String |
| **marker** | To use slf4j marker. |  | String |
| **logger** | To refer to a custom logger instance to lookup from the registry. |  | Logger |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

### Difference between Log EIP and Log component

This log EIP is much lighter and meant for logging human logs such as `Starting to do …​` etc. It can only log a message based on the [Simple](../languages/simple-language.md) language.

The [log](../log-component.md) component is meant for logging the message content (body, headers, etc.). There are many options on the log component to configure what content to log.

## Example

You can use the log EIP which allows you to use [Simple](../languages/simple-language.md) language to construct a dynamic message which gets logged.

For example, you can do

```java
from("direct:start")
    .log("Processing ${id}")
    .to("bean:foo");
```

And in XML:

```xml
<route>
  <from uri="direct:start"/>
  <log message="Processing ${id}"/>
  <to uri="bean:foo"/>
</route>
```

This will be evaluated using the [Simple](../languages/simple-language.md) to construct the `String` containg the message to be logged.

### Logging message body with streaming

If the message body is stream based, then logging the message body, may cause the message body to be empty afterwards. For streamed messages you can use Stream caching to allow logging the message body and be able to read the message body afterwards again.

The log DSL have overloaded methods to set the logging level and/or name as well.

```java
from("direct:start")
    .log(LoggingLevel.DEBUG, "Processing ${id}")
    .to("bean:foo");
```

and to set a logger name

```java
from("direct:start")
    .log(LoggingLevel.DEBUG, "com.mycompany.MyCoolRoute", "Processing ${id}")
    .to("bean:foo");
```

The logger instance may be used as well:

```java
from("direct:start")
    .log(LoggingLevel.DEBUG, org.slf4j.LoggerFactory.getLogger("com.mycompany.mylogger"), "Processing ${id}")
    .to("bean:foo");
```

For example you can use this to log the file name being processed if you consume files.

```java
from("file://target/files")
    .log(LoggingLevel.DEBUG, "Processing file ${file:name}")
    .to("bean:foo");
```

In Spring DSL it is also easy to use log DSL as shown below:

```xml
<route id="foo">
    <from uri="direct:foo"/>
    <log message="Got ${body}"/>
    <to uri="mock:foo"/>
</route>
```

The log tag has attributes to set the message, loggingLevel and logName. For example:

```xml
<route id="baz">
    <from uri="direct:baz"/>
    <log message="Me Got ${body}" loggingLevel="FATAL" logName="com.mycompany.MyCoolRoute"/>
    <to uri="mock:baz"/>
</route>
```

## Using custom logger

It is possible to reference an existing logger instance. For example:

```xml
<bean id="myLogger" class="org.slf4j.LoggerFactory" factory-method="getLogger">
    <constructor-arg value="com.mycompany.mylogger" />
</bean>

<route id="moo">
    <from uri="direct:moo"/>
    <log message="Me Got ${body}" loggerRef="myLogger"/>
    <to uri="mock:baz"/>
</route>
```

### Configuring logging name

The log message will be logged at `INFO` level using the route id as the logger name. So for example if you have not assigned an id to the route, then Camel will use `route-1`, `route-2` as the logger name.

For example to use "fooRoute" as the route id, you can do:

```java
from("direct:start").routeId("fooRoute")
    .log("Processing ${id}")
    .to("bean:foo");
```

And in XML:

```xml
<route id="fooRoute">
  <from uri="direct:start"/>
  <log message="Processing ${id}"/>
  <to uri="bean:foo"/>
</route>
```

#### Using custom logger from the Registry

If the Log EIP has not been configured with a specific logger to use, then Camel will will lookup in the [Registry](../../../manual/registry.md) if there is a single instance of `org.slf4j.Logger`.

If such an instance exists then this logger is used, if not the behavior defaults to creating a new instance of logger.

### Configuring logging name globally

You can configure a global log name that is used instead of the route id, by setting the global option on the `CamelContext`.

In Java you can do:

```java
camelContext.getGlobalOptions().put(Exchange.LOG_EIP_NAME, "com.foo.myapp");
```

And in XML:

```xml
<camelContext>
  <properties>
    <property key="CamelLogEipName" value="com.foo.myapp"/>
  </properties>
</camelContext>
```

## Masking sensitive information like password

You can enable security masking for logging by setting `logMask` flag to `true`. Note that this option also affects [Log](../log-component.md) component.

To enable mask in Java DSL at CamelContext level:

```java
camelContext.setLogMask(true);
```

And in XML you set the option on `<camelContext>`:

```xml
<camelContext logMask="true">

</camelContext>
```

You can also turn it on|off at route level. To enable mask in Java DSL at route level:

```java
from("direct:start").logMask()
    .log("Processing ${id}")
    .to("bean:foo");
```

And in XML:

```xml
<route logMask="true">

</route>
```

### Using custom masking formatter

`org.apache.camel.support.processor.DefaultMaskingFormatter` is used for the masking by default. If you want to use a custom masking formatter, put it into registry with the name `CamelCustomLogMask`. Note that the masking formatter must implement `org.apache.camel.spi.MaskingFormatter`.

The know set of keywords to mask is gathered from all the different component options, that are marked as secret. The list is generated into the source code in `org.apache.camel.util.SensitiveUtils`. At this time of writing there is more than 65 different keywords.

Custom keywords can be added as shown:

```java
DefaultMaskingFormatter formatter = new DefaultMaskingFormatter();
formatter.addKeyword("mySpecialKeyword");
formatter.addKeyword("verySecret");

camelContext.getRegistry().bind(MaskingFormatter.CUSTOM_LOG_MASK_REF, formatter);
```