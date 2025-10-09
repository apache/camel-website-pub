# Sticky

Sticky mode for the [Load Balancer](loadBalance-eip.md) EIP.

A stick mode means that a correlation key (calculated as [Expression](../../../manual/expression.md)) is used to determine the destination. This allows to route all messages with the same key to the same destination.

## Options

The Sticky eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **correlationExpression** | **Required** The correlation expression to use to calculate the correlation key. |  | ExpressionSubElementDefinition |

## Examples

In this case we are using the header myKey as correlation expression:

```java
from("direct:start")
    .loadBalance().sticky(header("myKey"))
        .to("seda:x")
        .to("seda:y")
        .to("seda:z")
    .end();
```

In XML you’ll have a route like this:

```xml
<route>
<from uri="direct:start"/>
    <loadBalance>
       <sticky>
           <correlationExpression>
               <header>myKey</header>
           </correlationExpression>
       </sticky>
       <to uri="seda:x"/>
       <to uri="seda:y"/>
       <to uri="seda:z"/>
    </loadBalance>
</route>
```