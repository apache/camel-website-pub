# Weighted Load Balancer

Weighted mode for [Load Balancer](loadBalance-eip.md) EIP. With this policy in case of failures, the exchange will be tried on the next endpoint.

## Options

The Weighted Load Balancer eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **distributionRatio** | **Required** The distribution ratio is a delimited String consisting on integer weights separated by delimiters for example 2,3,5. The distributionRatio must match the number of endpoints and/or processors specified in the load balancer list. |  | String |
| **distributionRatioDelimiter** | Delimiter used to specify the distribution ratio. The default value is , (comma). | , | String |
| **roundRobin** | To enable round robin mode. By default the weighted distribution mode is used. The default value is false. | false | Boolean |

## Exchange properties

The Weighted Load Balancer eip has no exchange properties.

## Examples

In this example, we want to send the most message to the first endpoint, then the second, and only a few to the last.

The distribution ratio is `7 = 4 + 2 + 1`. This means that for every seventh message then 4 goes to the first, 2 for the second, and 1 for the last.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .loadBalance().weighted("4,2,1")
        .to("seda:x")
        .to("seda:y")
        .to("seda:z")
    .end();
```

```xml
<route>
    <from uri="direct:start"/>
      <loadBalance>
        <weightedLoadBalancer distributionRatio="4 2 1"/>
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
              - weightedLoadBalancer:
                  distributionRatio: "4,2,1"
              - to:
                  uri: seda:x
              - to:
                  uri: seda:y
              - to:
                  uri: seda:z
```