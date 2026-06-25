# Sticky Load Balancer

Sticky mode for the [Load Balancer](loadBalance-eip.md) EIP.

A stick mode means that a correlation key (calculated as [Expression](../../../manual/expression.md)) is used to determine the destination. This allows routing all messages with the same key to the same destination.

## Options

The Sticky Load Balancer eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **correlationExpression** | The correlation expression to use to calculate the correlation key. |  | ExpressionSubElementDefinition |

## Exchange properties

The Sticky Load Balancer eip has no exchange properties.

## Examples

In this case, we are using the header myKey as correlation expression:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .loadBalance().sticky(header("myKey"))
        .to("seda:x")
        .to("seda:y")
        .to("seda:z")
    .end();
```

```xml
<route>
<from uri="direct:start"/>
    <loadBalance>
       <stickyLoadBalancer>
           <correlationExpression>
               <header>myKey</header>
           </correlationExpression>
       </stickyLoadBalancer>
       <to uri="seda:x"/>
       <to uri="seda:y"/>
       <to uri="seda:z"/>
    </loadBalance>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - loadBalance:
            steps:
              - stickyLoadBalancer:
                  correlationExpression:
                    header:
                      expression: myKey
              - to:
                  uri: seda:x
              - to:
                  uri: seda:y
              - to:
                  uri: seda:z
```