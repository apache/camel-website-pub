# Sample

A sampling throttler allows you to extract a sample of the exchanges from the traffic through a route.

![image](_images/eip/WireTap.gif)

The Sample EIP works similar to a wire tap, but instead of tapping every message, the sampling will select a single message in a given time period. This selected message is allowed to pass through, and all other messages are stopped.

## Options

The Sample eip supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **samplePeriod** | Sets the sample period during which only a single Exchange will pass through. | 1000 | String |
| **messageFrequency** | Sets the sample message count which only a single Exchange will pass through after this many received. |  | Long |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Using Sample EIP

In the example below we sample one message per second (default time period):

```java
from("direct:sample")
    .sample()
    .to("direct:sampled");
```

And in XML

```xml
<route>
    <from uri="direct:sample"/>
    <sample>
        <to uri="direct:sampled"/>
    </sample>
</route>
```

### Sampling using time period

The default time period is 1 second, but this can easily be configured. For example to sample 1 message per 5 seconds you can do:

```java
from("direct:sample")
    .sample(5, TimeUnit.SECONDS)
    .to("direct:sampled");
```

And in XML

```xml
<route>
    <from uri="direct:sample"/>
    <sample samplePeriod="5000">
        <to uri="direct:sampled"/>
    </sample>
</route>
```

### Sampling using message frequency

The Sample EIP can also be configured to sample based on frequency instead of time period.

For example to sample every 10th message you can do:

```java
from("direct:sample")
    .sample(10)
    .to("direct:sampled");
```

And in XML

```xml
<route>
    <from uri="direct:sample"/>
    <sample messageFrequency="10">
        <to uri="direct:sampled"/>
    </sample>
</route>
```