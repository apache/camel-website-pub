# Once

**Since Camel 4.17**

**Only consumer is supported**

The Once component is used to generate a message only once. For example to trigger a message after Camel has been started, or for development and testing purposes.

This component is designed to be very basic and only a few options.

You can find more features when using the [Timer](timer-component.md) component, which also can be configured to only trigger once with `repeatCount=1`.

## URI format

once:name\[?options\]

Where `name` is a logical name.

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

The Once component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **delay** (advanced) | The number of milliseconds to wait before triggering. Use 0 or negative to fire as soon as possible. The default value is 1000. | 1000 | long |
| **languages** (advanced) | Whether Camel languages are supported such as simple,groovy. | true | boolean |

## Endpoint Options

The Once endpoint is configured using URI syntax:

once:name

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (consumer) | **Required** The logical name. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **body** (consumer) | The data to use as message body. You can externalize the data by using file: or classpath: as prefix and specify the location of the file. |  | String |
| **headers** (consumer) | The data to use as message headers as key=value pairs. You can externalize the data by using file: or classpath: as prefix and specify the location of the file. This is a multi-value option with prefix: header. |  | Map |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **delay** (advanced) | The number of milliseconds to wait before triggering. The default value is 1000. | 1000 | long |
| **exchangeProperties** (advanced) | The data to use as exchange properties as key=value pairs. You can externalize the data by using file: or classpath: as prefix and specify the location of the file. This is a multi-value option with prefix: exchangeProperty. |  | Map |
| **variables** (advanced) | The data to use as exchange variables as key=value pairs. You can externalize the data by using file: or classpath: as prefix and specify the location of the file. This is a multi-value option with prefix: variable. |  | Map |

## Usage

## Example

To set up a route that generates an event every 60 seconds:

-   Java
    
-   XML
    
-   YAML
    

```java
from("once:foo?body=file:data.json").to("bean:myBean?method=someMethodName");
```

```xml
<route>
  <from uri="once:foo?body=file:data.json"/>
  <to uri="bean:myBean?method=someMethodName"/>
</route>
```

```yaml
- route:
    from:
      uri: once:foo
      parameters:
        body: "file:data.json"
      steps:
        - to:
            uri: bean:myBean
            parameters:
              method: someMethodName
```

The above route will trigger once and load the `data.json` from file system and use as message body. And then route to call the bean.

### Using headers and variables

You can also specify headers and variables using _multivalue_, where each header is prefixed with `header.<key>`. In the sample below we set 2 headers as follows: `foo=abc` and `bar=123`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("once:tick?body=world&header.foo=abc&header.bar=123")
    .to("bean:myBean");
```

```xml
<route>
  <from uri="once:tick?body=world&amp;header.foo=abc&amp;header.bar=123"/>
  <to uri="bean:myBean"/>
</route>
```

```yaml
- route:
    from:
      uri: once:tick
      parameters:
        body: world
        header.foo: abc
        header.bar: "123"
      steps:
        - to:
            uri: bean:myBean
```

You can do the same for variables with `variable.<key>`.

And in YAML DSL you can use YAML map’s directly as shown below:

```yaml
- route:
    from:
      uri: once
      parameters:
        name: hello
        body: Hello World
        headers:
          foo: foolish
          bar: 456
      steps:
        - to: mock:result
```

> **Important**
> This requires that the `uri` does not have any configuration so it must be `uri: once` and not `uri: once:hello`.

### Using custom languages

You can use the Camel languages such as simple, or groovy when specifying body, headers, exchange properties, and variables.

The once component will set the data in the following order:

-   variables
    
-   exchangeProperties
    
-   headers
    
-   body
    

This makes it possible to use groovy or simple language for setting the message body, based on data from the variables and headers.

For example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("once:tick?body=language:groovy:file:src/test/resources/calc.groovy&variable.amount=123")
        .to("mock:result");
```

```xml
<route>
  <from uri="once:tick?body=language:groovy:file:src/test/resources/calc.groovy&amp;variable.amount=123"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: once:tick
      parameters:
        body: "language:groovy:file:src/test/resources/calc.groovy"
        variable.amount: "123"
      steps:
        - to:
            uri: mock:result
```

You must use `language:groovy:` as prefix when using languages. And you can combine this with loading from file. The `calc.groovy` file is as follows:

```groovy
variable.amount * 3
```

As you can see this just tells groovy to multiply the amount variable with 3.

### Automatic type conversion

The body, header, and variables will automatically be converted to the best suitable type for boolean and integers:

-   boolean
    
-   int
    
-   long
    

And for any other its `String` or the output from executing a language.

### Firing as soon as possible

By default, the component is fired after 1 seconds when Camel has been fully started. If you want to fire messages in a Camel route as soon as possible, you can use a negative delay:

-   Java
    
-   XML
    
-   YAML
    

```java
from("once:foo?body=file.data.json&delay=-1").to("bean:myBean?method=someMethodName");
```

```xml
<route>
  <from uri="once:foo?body=file.data.json&amp;delay=-1"/>
  <to uri="bean:myBean?method=someMethodName"/>
</route>
```

```yaml
- route:
    from:
      uri: once:foo
      parameters:
        body: file.data.json
        delay: -1
      steps:
        - to:
            uri: bean:myBean
            parameters:
              method: someMethodName
```

In this way, the timer will fire messages immediately.

## Spring Boot Auto-Configuration

When using once with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-once-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.once.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.once.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.once.delay** | The number of milliseconds to wait before triggering. Use 0 or negative to fire as soon as possible. The default value is 1000. | 1000 | Long |
| **camel.component.once.enabled** | Whether to enable auto configuration of the once component. This is enabled by default. |  | Boolean |
| **camel.component.once.languages** | Whether Camel languages are supported such as simple,groovy. | true | Boolean |