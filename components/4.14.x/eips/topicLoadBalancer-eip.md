# Topic Load Balancer

Topic mode for the [Load Balancer](loadBalance-eip.md) EIP. With this policy, then all destinations are selected.

## Options

The Topic Load Balancer eip has no options.

## Exchange properties

The Topic Load Balancer eip has no exchange properties.

## Examples

In this example, we send the message to all three endpoints:

-   Java
    
-   XML
    

```java
from("direct:start")
    .loadBalance().topic()
        .to("seda:x")
        .to("seda:y")
        .to("seda:z")
    .end();
```

```xml
<route>
<from uri="direct:start"/>
    <loadBalance>
       <topicLoadBalancer/>
       <to uri="seda:x"/>
       <to uri="seda:y"/>
       <to uri="seda:z"/>
    </loadBalance>
</route>
```