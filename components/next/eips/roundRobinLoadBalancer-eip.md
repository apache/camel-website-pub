# Round Robin Load Balancer

Round Robin mode for the [Load Balancer](loadBalance-eip.md) EIP.

The exchanges are selected in a round-robin fashion. This is a well known and classic policy, which spreads the load evenly.

## Options

The Round Robin Load Balancer eip has no options.

## Exchange properties

The Round Robin Load Balancer eip has no exchange properties.

## Example

We want to load balance between three endpoints in round-robin mode.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .loadBalance().roundRobin()
        .to("seda:x")
        .to("seda:y")
        .to("seda:z")
    .end();
```

```xml
<route>
    <from uri="direct:start"/>
    <loadBalance>
       <roundRobinLoadBalancer/>
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
              - roundRobinLoadBalancer: {}
              - to:
                  uri: seda:x
              - to:
                  uri: seda:y
              - to:
                  uri: seda:z
```