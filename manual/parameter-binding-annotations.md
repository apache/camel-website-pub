# Parameter Binding Annotations

The bean parameter binding annotations from Camel are as follows:

 
| Annotation | Meaning |
| --- | --- |
| `` `org.apache.camel.Body` `` | To bind to an inbound message body |
| `` `org.apache.camel.Header` `` | To bind to a message header by the given name |
| `` `org.apache.camel.Headers` `` | To bind to the Map of the message headers |
| `` `org.apache.camel.Variable` `` | To bind to a named variable the given name |
| `` `org.apache.camel.Variables` `` | To bind to the variables map |
| `` `org.apache.camel.ExchangeProperty` `` | To bind to a named property on the exchange the given name |
| `` `org.apache.camel.ExchangeProperties` `` | To bind to the exchange property map on the exchange |
| `` `org.apache.camel.ExchangeException` `` | To bind to an Exception set on the exchange |

These annotations can be used with the [Bean](../components/4.22.x/bean-component.md) component or when invoking beans in the [DSL](dsl.md)

Annotations can be used to define an [Expression](expression.md) or to extract various headers, properties or payloads from a [Message](../components/4.22.x/eips/message.md) when invoking a bean method. See [Bean Integration](bean-integration.md) for more in depth details on invoking beans.

If no annotations are used then Camel assumes that a single parameter is the body of the message. Camel will then use the [Type Converter](type-converter.md) mechanism to convert from the expression value to the actual type of the parameter.

## Using bean parameter binding annotations

In this example below we have a `@Consume` consumer (like message driven) that consumes JMS messages from the activemq queue. We use the `@Header` and `@Body` parameter binding annotations to bind from the JMSMessage to the method parameters.

```java
public class MyBean {

    @Consume("activemq:my.queue")
    public void doSomething(@Header("JMSCorrelationID") String correlationID, @Body String body) {
        // process the inbound message here
    }

}
```

In the above Camel will extract the value of `Message.getJMSCorrelationID()`, then using the [Type Converter](type-converter.md) to adapt the value to the type of the parameter if required - it will inject the parameter value for the **correlationID** parameter. Then the payload of the message will be converted to a String and injected into the **body** parameter.

> **Tip**
> You don’t necessarily need to use the `@Consume` annotation if you don’t want to as you could also make use of the Camel [DSL](dsl.md) to route to the bean’s method as well.

### Calling bean from Camel routes

Here is another example which does not use [POJO Consuming](pojo-consuming.md) annotations but instead uses the [DSL](dsl.md) to route messages to the bean method.

```java
public class MyBean {

    public void doSomething(@Header("JMSCorrelationID") String correlationID, @Body String body) {
        // process the inbound message here
    }

}
```

The routing DSL then looks like this

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:someQueue").
  to("bean:myBean");
```

```xml
<route>
    <from uri="activemq:someQueue"/>
    <to uri="bean:myBean"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:someQueue
      steps:
        - to:
            uri: bean:myBean
```

Here **myBean** would be looked up in the [Registry](registry.md) then the body of the message would be used to try figure out what method to call.

If you want to be explicit you can use:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:someQueue").
  to("bean:myBean?method=doSomething");
```

```xml
<route>
    <from uri="activemq:someQueue"/>
    <to uri="bean:myBean?method=doSomething"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:someQueue
      steps:
        - to:
            uri: bean:myBean
            parameters:
              method: doSomething
```

And here we have a nifty example for you to show some great power in Camel. You can mix and match the annotations with the normal parameters, so we can have this example with annotations and the Exchange also:

```java
public class MyBean {

    public void doSomething(@Header("user") String user, @Body String body, Exchange exchange) {
        exchange.getIn().setBody(body + "MyBean");
    }

}
```

### Annotation Based Expression Language

You can also use any of the [Languages](languages.md) supported in Camel to bind expressions to method parameters when using [Bean Integration](bean-integration.md). For example, you can use any of these annotations:

 
| Annotation | Description |
| --- | --- |
| `` `@Bean` `` | Inject a [Bean](../components/4.22.x/languages/bean-language.md) expression |
| `` `@Constant` `` | Inject a [Constant](../components/4.22.x/languages/constant-language.md) expression |
| `` `@Groovy` `` | Inject a [Groovy](../components/4.22.x/languages/groovy-language.md) expression |
| `` `@Header` `` | Inject a [Header](../components/4.22.x/languages/header-language.md) expression |
| `` `@Simple` `` | Inject an [Simple](../components/4.22.x/languages/simple-language.md) expression |
| `` `@XPath` `` | Inject an [XPath](../components/4.22.x/languages/xpath-language.md) expression |

The table above only list some of the commonly used languages. You can find a list of all supported [Languages](../components/4.22.x/languages/index.md) which each have their own annotation that can be used.

It is required to include the JAR of the language, for example `camel-groovy`, or `camel-jsonpath` to use the `@JSonPath` annotation.

Here is an example how to use `@XPath`:

```java
public class Foo {

    @Consume("activemq:my.queue")
    public void doSomething(@XPath("/foo/bar/text()") String correlationID, @Body String body) {
        // process the inbound message here
    }

}
```

#### Advanced example using @Bean

And an example of using the `@Bean` binding annotation, where you can call a [POJO](../components/4.22.x/bean-component.md) to supply the parameter value:

```java
public class MyBean {

    @Consume("activemq:my.queue")
    public void doSomething(@Bean("myCorrelationIdGenerator") String correlationID, @Body String body) {
        // process the inbound message here
    }
}
```

When a message is consumed from the activemq queue, then Camel will invoke the `doSomething` method. The parameter with `@Bean` is telling Camel to call yet another bean that computes the correlation id parameter:

```java
public class MyIdGenerator {

    private UserManager userManager;

    public String generate(@Header(name = "user") String user, @Body String payload) throws Exception {
       User user = userManager.lookupUser(user);
       String userId = user.getPrimaryId();
       return userId + generateHashCodeForPayload(payload);
   }
}
```

The [POJO](../components/4.22.x/bean-component.md) MyIdGenerator has one public method that accepts two parameters. We have also annotated this one with the `@Header` and `@Body` annotations to help Camel know what to bind here from the Exchange being processed.

Of course this could be simplified a lot if you for instance just have a simple id generator. But we wanted to demonstrate that you can use the [Bean Binding](bean-binding.md) annotations anywhere.

```java
public class MySimpleIdGenerator {

    public static int generate()  {
       // generate a unique id
       return 123;
   }
}
```

And finally we just need to remember to have our bean registered in the [Registry](registry.md):

For example in Spring XML:

```xml
<bean id="myCorrelationIdGenerator" class="com.mycompany.MySimpleIdGenerator"/>
```

#### Example using Groovy

In this example we have an Exchange that has a User object stored in the in header. This User object has methods to get some user information. We want to use [Groovy](../components/4.22.x/languages/groovy-language.md) to inject an expression that extracts and concat the names of the user into the fullName parameter.

```java
public class MyBean {

    public void doSomething(@Groovy("$request.header['user'].firstName $request.header['user'].familyName") String fullName, @Body String body) {
        // process the inbound message here
    }

}
```

Groovy supports _GStrings_ that is like a template where we can insert `$` placeholders that will be evaluated by Groovy.