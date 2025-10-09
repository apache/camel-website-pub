# Topic

Topic mode for the [Load Balancer](loadBalance-eip.md) EIP. With this policy then all destination is selected.

## Options

The Topic eip has no options.

## Examples

In this example we send the message to all three endpoints:

```java
from("direct:start")
    .loadBalance().topic()
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
       <topic/>
       <to uri="seda:x"/>
       <to uri="seda:y"/>
       <to uri="seda:z"/>
    </loadBalance>
</route>
```