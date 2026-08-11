# Transform

Camel supports the [Message Translator](http://www.enterpriseintegrationpatterns.com/MessageTranslator.md) from the [EIP patterns](enterprise-integration-patterns.md).

How can systems using different data formats communicate with each other using messaging?

![image](_images/eip/MessageTranslator.gif)

Use a special filter, a Message Translator, between other filters or applications to translate one data format into another.

The [Message Translator](message-translator.md) can be done in different ways in Camel:

-   Using [Transform](#) or [Set Body](setBody-eip.md) in the DSL
    
-   Calling a [Processor](../../../manual/processor.md) or [bean](../../../manual/bean-integration.md) to perform the transformation
    
-   Using template-based [Components](../index.md), with the template being the source for how the message is translated
    
-   Messages can also be transformed using [Data Format](../../../manual/data-format.md) to marshal and unmarshal messages in different encodings.
    
-   Using data type based transformation using [Transform DataType](transformDataType-eip.md)
    

This page is documenting the first approach by using Transform EIP.

## Options

The Transform eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **expression** | **Required** Expression to return the transformed message body (the new message body to use). |  | ExpressionDefinition |

## Exchange properties

The Transform eip has no exchange properties.

## Using Transform EIP

You can use a [Transform](#) which uses an [Expression](../../../manual/expression.md) to do the transformation:

In the example below, we prepend Hello to the message body using the [Simple](../../4.22.x/languages/simple-language.md) language:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:cheese")
    .transform(simple("Hello ${body}"))
    .to("log:hello");
```

```xml
<route>
    <from uri="direct:cheese"/>
    <transform>
        <simple>Hello ${body}</simple>
    </transform>
    <to uri="log:hello"/>
</route>
```

```yaml
- from:
    uri: direct:cheese
    steps:
      - transform:
          expression:
            simple: Hello ${body}
      - to:
          uri: log:hello
```

## What is the difference between Transform and Set Body?

The Transform EIP always sets the result on the OUT message body.

Set Body sets the result accordingly to the [Exchange Pattern](../../../manual/exchange-pattern.md) on the `Exchange`.