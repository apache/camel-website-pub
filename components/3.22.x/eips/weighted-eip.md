# Weighted

Weighted mode for [Load Balancer](loadBalance-eip.md) EIP. With this policy in case of failures the exchange will be tried on the next endpoint.

## Options

The Weighted eip supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **distributionRatio** | **Required** The distribution ratio is a delimited String consisting on integer weights separated by delimiters for example 2,3,5. The distributionRatio must match the number of endpoints and/or processors specified in the load balancer list. |  | String |
| **distributionRatioDelimiter** | Delimiter used to specify the distribution ratio. The default value is , (comma). | , | String |
| **roundRobin** | To enable round robin mode. By default the weighted distribution mode is used. The default value is false. | false | Boolean |

## Examples

In this example we want to send the most message to the first endpoint, then the second, and only a few to the last.

The distribution ratio is 7 = 4 + 2 + 1. This means that for every 7 message then 4 goes to the 1st, 2 for the 2nd, and 1 for the last.

```java
from("direct:start")
    .loadBalance().weighted(false, "4,2,1")
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
        <weighted distributionRatio="4 2 1"/>
        <to uri="seda:x"/>
        <to uri="seda:y"/>
        <to uri="seda:z"/>
      </loadBalance>
</route>
```