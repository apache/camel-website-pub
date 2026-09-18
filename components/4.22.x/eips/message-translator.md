# Message Translator

Camel supports the [Message Translator](http://www.enterpriseintegrationpatterns.com/MessageTranslator.md) from the [EIP patterns](enterprise-integration-patterns.md).

![image](_images/eip/MessageTranslator.gif)

The Message Translator can be done in different ways in Camel:

-   Using [Transform](transform-eip.md) or [Set Body](setBody-eip.md) in the DSL
    
-   Calling a [Processor](../../../manual/processor.md) or [bean](../../../manual/bean-integration.md) to perform the transformation
    
-   Using template-based [Components](../index.md), with the template being the source for how the message is translated
    
-   Messages can also be transformed using [Data Format](../../../manual/data-format.md) to marshal and unmarshal messages in different encodings.
    

## Example

Each of the approaches above is documented in the following examples:

### Message Translator with Transform EIP

You can use a [Transform](transform-eip.md) which uses an [Expression](../../../manual/expression.md) to do the transformation:

In the example below, we prepend Hello to the message body using the [Simple](../languages/simple-language.md) language:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:cheese")
    .setBody(simple("Hello ${body}"))
    .to("log:hello");
```

```xml
<route>
    <from uri="activemq:cheese"/>
    <transform>
        <simple>Hello ${body}</simple>
    </transform>
    <to uri="activemq:wine"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq
      parameters:
        destinationName: cheese
      steps:
        - transform:
            simple:
              expression: Hello ${body}
        - to:
            uri: activemq
            parameters:
              destinationName: wine
```

### Message Translator with Bean

You can transform a message using Camel’s [Bean Integration](../../../manual/bean-integration.md) to call any method on a bean that performs the message translation:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:cheese")
  .bean("myTransformerBean", "doTransform")
  .to("activemq:wine");
```

```xml
<route>
    <from uri="activemq:cheese"/>
    <bean ref="myTransformerBean" method="doTransform"/>
    <to uri="activemq:wine"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq
      parameters:
        destinationName: cheese
      steps:
        - bean:
            ref: myTransformerBean
            method: doTransform
        - to:
            uri: activemq
            parameters:
              destinationName: wine
```

### Message Translator with Processor

You can also use a [Processor](../../../manual/processor.md) to do the transformation:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:cheese")
  .process(new MyTransformerProcessor())
  .to("activemq:wine");
```

```xml
<route>
    <from uri="activemq:cheese"/>
    <process ref="myTransformerProcessor"/>
    <to uri="activemq:wine"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq
      parameters:
        destinationName: cheese
      steps:
        - process:
            ref: myTransformerProcessor
        - to:
            uri: activemq
            parameters:
              destinationName: wine
```

### Message Translator using Templating Components

You can also consume a message from one destination, transform it with something like [Velocity](../velocity-component.md) or [XQuery](../xquery-component.md), and then send it on to another destination.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:cheese")
    .to("velocity:com/acme/MyResponse.vm")
    .to("activemq:wine");
```

```xml
<route>
    <from uri="activemq:cheese"/>
    <to uri="velocity:com/acme/MyResponse.vm"/>
    <to uri="activemq:wine"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq
      parameters:
        destinationName: cheese
      steps:
        - to:
            uri: velocity
            parameters:
              resourceUri: com/acme/MyResponse.vm
        - to:
            uri: activemq
            parameters:
              destinationName: wine
```

### Message Translator using Data Format

See [Marshal](marshal-eip.md) EIP for more details and examples.