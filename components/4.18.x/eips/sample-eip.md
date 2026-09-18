# Sample

A sampling throttler allows you to extract a sample of the exchanges from the traffic through a route.

![image](_images/eip/Sample.png)

The Sample EIP selects a single message in a given time period or every nth message. This selected message is allowed to pass through, and all other messages are stopped.

## Options

The Sample eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **samplePeriod** | Sets the sample period during which only a single Exchange will pass through. | 1000 | String |
| **messageFrequency** | Sets the sample message count which only a single Exchange will pass through after this many received. |  | Long |

## Exchange properties

The Sample eip has no exchange properties.

## Using Sample EIP

In the example below, we sample one message per second (default time period):

-   Java
    
-   XML
    

```java
from("direct:sample")
    .sample()
    .to("direct:sampled");
```

```xml
<route>
    <from uri="direct:sample"/>
    <sample/>
    <to uri="direct:sampled"/>
</route>
```

### Sampling using time period

The default time period is 1 second, but this can easily be configured. For example, to sample one message per 5 seconds, you can do:

-   Java
    
-   XML
    

```java
from("direct:sample")
    .sample(Duration.of(5, ChronoUnit.SECONDS))
    .to("direct:sampled");
```

```xml
<route>
    <from uri="direct:sample"/>
    <sample samplePeriod="5000"/>
    <to uri="direct:sampled"/>
</route>
```

### Sampling using message frequency

The Sample EIP can also be configured to sample based on frequency instead of a time period.

For example, to sample every 10th message you can do:

-   Java
    
-   XML
    

```java
from("direct:sample")
    .sample(10)
    .to("direct:sampled");
```

```xml
<route>
    <from uri="direct:sample"/>
    <sample messageFrequency="10"/>
    <to uri="direct:sampled"/>
</route>
```

### Sampling with wiretap

The sampling throttler will stop all exchanges not included in the sample. This may be undesirable if you want to perform custom processing on the sample while still allowing all 10 messages to flow to an endpoint after the sample EIP.

For this use case, you can combine the sample EIP with wiretap EIP. In the example below, we sample every 10th message and send it to direct:sampleProcessing, while all 10 messages are still sent to direct:regularProcessing.

-   Java
    
-   XML
    

```java
from("direct:start")
  .wireTap("direct:sample")
  .to("direct:regularProcessing")

from("direct:sample")
  .sample(10)
  .to("direct:sampleProcessing");
```

```xml
<route>
    <from uri="direct:start"/>
    <wireTap uri="direct:sample"/>
    <to uri="direct:regularProcessing"/>
</route>

<route>
    <from uri="direct:sample"/>
    <sample messageFrequency="10"/>
    <to uri="direct:sampleProcessing"/>
</route>
```