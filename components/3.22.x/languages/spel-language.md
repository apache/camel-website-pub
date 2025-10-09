# SpEL

**Since Camel 2.7**

Camel allows [Spring Expression Language (SpEL)](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#expressions) to be used as an Expression or Predicate in the DSL or XML Configuration.

> **Note**
> It is recommended to use SpEL in Spring runtimes. However, you can use SpEL in other runtimes (there are some functionality which SpEL can only do in a Spring runtime)

## SpEL Options

The SpEL language supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** |  | `String` | Sets the class of the result type (type from output). |
| **trim** | `true` | `Boolean` | Whether to trim the value to remove leading and trailing whitespaces and line breaks. |

## Variables

The following Camel related variables are made available:

  
| Variable | Type | Description |
| --- | --- | --- |
| **this** | Exchange | the Exchange is the root object |
| context | CamelContext | the CamelContext |
| exchange | Exchange | the Exchange |
| exchangeId | String | the exchange id |
| exception | Throwable | the Exchange exception (if any) |
| request | Message | the message |
| message | Message | the message |
| headers | Map | the message headers |
| header(name) | Object | the message header by the given name |
| header(name, type) | Type | the message header by the given name as the given type |
| properties | Map | the exchange properties |
| property(name) | Object | the exchange property by the given name |
| property(name, type) | Type | the exchange property by the given name as the given type |

## Example

You can use SpEL as an expression for [Recipient List](../eips/recipientList-eip.md) or as a predicate inside a [Message Filter](../eips/filter-eip.md):

```xml
<route>
  <from uri="direct:foo"/>
  <filter>
    <spel>#{request.headers.foo == 'bar'}</spel>
    <to uri="direct:bar"/>
  </filter>
</route>
```

And the equivalent in Java DSL:

```java
from("direct:foo")
    .filter().spel("#{request.headers.foo == 'bar'}")
    .to("direct:bar");
```

### Expression templating

SpEL expressions need to be surrounded by `#{` `}` delimiters since expression templating is enabled. This allows you to combine SpEL expressions with regular text and use this as extremely lightweight template language.

For example if you construct the following route:

```java
from("direct:example")
    .setBody(spel("Hello #{request.body}! What a beautiful #{request.headers['dayOrNight']}"))
    .to("mock:result");
```

In the route above, notice `spel` is a static method which we need to import from `org.apache.camel.language.spel.SpelExpression.spel`, as we use `spel` as an Expression passed in as a parameter to the `setBody` method. Though if we use the fluent API we can do this instead:

```java
from("direct:example")
    .setBody().spel("Hello #{request.body}! What a beautiful #{request.headers['dayOrNight']}")
    .to("mock:result");
```

Notice we now use the `spel` method from the `setBody()` method. And this does not require us to static import the `spel` method.

Then we send a message with the string "World" in the body, and a header "dayOrNight" with value "day":

```java
template.sendBodyAndHeader("direct:example", "World", "dayOrNight", "day");
```

The output on `mock:result` will be _"Hello World! What a beautiful day"_

### Bean integration

You can reference beans defined in the [Registry](../../../manual/registry.md) in your SpEL expressions. For example if you have a bean named "foo" registered in the Spring `ApplicationContext`. You can then invoke the "bar" method on this bean like this:

```text
#{@foo.bar == 'xyz'}
```

## Loading script from external resource

You can externalize the script and have Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g. to refer to a file on the classpath you can do:

```java
.setHeader("myHeader").spel("resource:classpath:myspel.txt")
```

## Spring Boot Auto-Configuration

When using spel with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-spring-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.spring-event.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.spring-event.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.spring-event.enabled** | Whether to enable auto configuration of the spring-event component. This is enabled by default. |  | Boolean |
| **camel.component.spring-event.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.language.spel.enabled** | Whether to enable auto configuration of the spel language. This is enabled by default. |  | Boolean |
| **camel.language.spel.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |