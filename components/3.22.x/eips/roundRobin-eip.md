# Round Robin

Round Robin mode for the [Load Balancer](loadBalance-eip.md) EIP.

The exchanges are selected in a round-robin fashion. This is a well known and classic policy, which spreads the load evenly.

## Options

The Round Robin eip has no options.

## Example

We want to load balance between three endpoints in round-robin mode.

This is done as follows in Java DSL:

```java
from("direct:start")
    .loadBalance().roundRobin()
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
       <roundRobin/>
       <to uri="seda:x"/>
       <to uri="seda:y"/>
       <to uri="seda:z"/>
    </loadBalance>
</route>
```