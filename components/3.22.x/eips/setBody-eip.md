# Set Body

Camel supports the [Message Translator](http://www.enterpriseintegrationpatterns.com/MessageTranslator.md) from the [EIP patterns](enterprise-integration-patterns.md).

![image](_images/eip/MessageTranslator.gif)

The [Message Translator](message-translator.md) can be done in different ways in Camel:

-   Using [Transform](transform-eip.md) or [Set Body](#) in the DSL
    
-   Calling a [Processor](../../../manual/processor.md) or [bean](../../../manual/bean-integration.md) to perform the transformation
    
-   Using template-based [Components](../index.md), with the template being the source for how the message is translated
    
-   Messages can also be transformed using [Data Format](../../../manual/data-format.md) to marshal and unmarshal messages in different encodings.
    

This page is documenting the first approach by using Set Body EIP.

## Options

The Set Body eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **expression** | **Required** Expression that returns the new body to use. |  | ExpressionDefinition |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Examples

### Using Set Body EIP

You can use a [Set Body](#) which uses an [Expression](../../../manual/expression.md) to do the transformation:

In the example below we prepend Hello to the message body using the [Simple](../../4.18.x/languages/simple-language.md) language:

```java
from("direct:cheese")
    .setBody(simple("Hello ${body}"))
    .to("log:hello");
```

And in XML DSL:

```xml
<route>
    <from uri="direct:cheese"/>
    <setBody>
        <simple>Hello ${body}</simple>
    </setBody>
    <to uri="log:hello"/>
</route>
```

### What is the difference between Transform and Set Body

The Transform EIP always sets the result on the OUT message body.

Set Body sets the result accordingly to the [Exchange Pattern](../../../manual/exchange-pattern.md) on the `Exchange`.