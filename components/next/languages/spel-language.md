# SpEL

**Since Camel 2.7**

Camel allows [Spring Expression Language (SpEL)](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#expressions) to be used as an Expression or Predicate in the DSL or XML Configuration.

> **Note**
> It is recommended to use SpEL in Spring runtimes. Although you can use SpEL in other runtimes, there is some functionality that SpEL can only do in a Spring runtime.

## SpEL Options

The SpEL language supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

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

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:foo")
    .filter().spel("#{request.headers.foo == 'bar'}")
    .to("direct:bar");
```

```xml
<route>
  <from uri="direct:foo"/>
  <filter>
    <spel>#{request.headers.foo == 'bar'}</spel>
    <to uri="direct:bar"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: direct:foo
      steps:
        - filter:
            expression:
              spel:
                expression: "#{request.headers.foo == 'bar'}"
            steps:
              - to:
                  uri: direct:bar
```

### Expression templating

SpEL expressions need to be surrounded by `#{` `}` delimiters since expression templating is enabled. This allows you to combine SpEL expressions with regular text and use this as an extremely lightweight template language.

For example, if you construct the following route:

_Java-only: static method import for spel expression_

```java
from("direct:example")
    .setBody(spel("Hello #{request.body}! What a beautiful #{request.headers['dayOrNight']}"))
    .to("mock:result");
```

In the route above, notice `spel` is a static method which we need to import from `org.apache.camel.language.spel.SpelExpression.spel`, as we use `spel` as an Expression passed in as a parameter to the `setBody` method. Though if we use the fluent API, we can do this instead:

_Java-only: fluent API for spel expression_

```java
from("direct:example")
    .setBody().spel("Hello #{request.body}! What a beautiful #{request.headers['dayOrNight']}")
    .to("mock:result");
```

Notice we now use the `spel` method from the `setBody()` method. And this does not require us to statically import the `spel` method.

Then we send a message with the string "World" in the body, and a header `dayOrNight` with value `day`:

_Java-only: ProducerTemplate usage_

```java
template.sendBodyAndHeader("direct:example", "World", "dayOrNight", "day");
```

The output on `mock:result` will be _"Hello World! What a beautiful day"_

### Bean integration

You can reference beans defined in the [Registry](../../../manual/registry.md) in your SpEL expressions. For example, if you have a bean named "foo" registered in the Spring `ApplicationContext`. You can then invoke the "bar" method on this bean like this:

```text
#{@foo.bar == 'xyz'}
```

## Loading script from external resource

You can externalize the script and have Apache Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g., to refer to a file on the classpath you can do:

_Java-only: fluent API for loading SpEL from resource_

```java
.setHeader("myHeader").spel("resource:classpath:myspel.txt")
```