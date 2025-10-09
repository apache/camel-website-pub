# Random Load Balancer

Random mode for the [Load Balancer](loadBalance-eip.md) EIP.

The destination endpoints are selected randomly. This is a well-known and classic policy, which spreads the load randomly.

The Random Load Balancer eip has no options.

## Exchange properties

The Random Load Balancer eip has no exchange properties.

## Example

We want to load balance between three endpoints in random mode.

This is done as follows:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .loadBalance().random()
        .to("seda:x")
        .to("seda:y")
        .to("seda:z")
    .end();
```

```xml
<route>
    <from uri="direct:start"/>
    <loadBalance>
       <randomLoadBalancer/>
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
              - randomLoadBalancer: {}
              - to:
                  uri: seda:x
              - to:
                  uri: seda:y
              - to:
                  uri: seda:z
```