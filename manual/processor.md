# Processor

The [Processor](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Processor.md) interface is used to implement consumers of message exchanges, or to implement a [Message Translator](../components/4.18.x/eips/message-translator.md), and other use-cases.

The `Processor` is a central API both internally and externally with Camel. The `Processor` has a single method `processor` (see below) that for example every [EIPs](../components/4.18.x/eips/enterprise-integration-patterns.md) implements.

## Using a processor in a route

Once you have written a class which implements processor like this:

```java
public class MyProcessor implements Processor {

    public void process(Exchange exchange) throws Exception {
        // do something...
    }

}
```

Then you can easily call this processor from Camel routes:

-   Java
    
-   XML
    
-   YAML
    

Notice that the processor is referred to by the class type `MyProcessor.class` in the route. Camel will during startup automatic create one new instance of the processor using [Injector](injector.md) to be used during routing messages.

```java
from("activemq:myQueue").process(MyProcessor.class);
```

```xml
<route>
  <from uri="activemq:myQueue"/>
  <process ref="myProcessor"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:myQueue
      steps:
        - process:
            ref: myProcessor
```

### Referring to beans using #class syntax

In all the Camel DSL you can also refer to the processor by its class name using `#class:` as prefix as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:myQueue")
  .process("#class:com.acme.MyProcessor");
```

However, in Java DSL you would often use the type safe way and create the Processor directly:

```java
from("activemq:myQueue").process(new MyProcessor());
```

```xml
<route>
  <from uri="activemq:myQueue"/>
  <process ref="#class:com.acme.MyProcessor"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:myQueue
      steps:
        - process:
            ref: "#class:com.acme.MyProcessor"
```

> **Note**
> For more details about the `#class:` prefix (and others) then see [Property Binding](property-binding.md).

## Why use process when you can use to instead?

The process can be used in routes as an anonymous inner class such:

```java
    from("activemq:myQueue").process(new Processor() {
        public void process(Exchange exchange) throws Exception {
            String payload = exchange.getIn().getBody(String.class);
            // do something with the payload and/or exchange here
           exchange.getIn().setBody("Changed body");
       }
    }).to("activemq:myOtherQueue");
```

This is usable for quickly whirling up some code. If the code in the inner class gets a bit more complicated it is of course advised to refactor it into a separate class. This approach is better if you do not want to use this processor again. From reusability perspective, it is not recommended to use this approach with anonymous inner classes.