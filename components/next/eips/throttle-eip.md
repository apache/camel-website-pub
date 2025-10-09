# Throttle

How can I throttle messages to ensure that a specific endpoint does not get overloaded, or we don’t exceed an agreed SLA with some external service?

![image](_images/eip/MessagingAdapterIcon.gif)

Use a Throttler that controls the rate of how many or fast messages are flowing to the endpoint.

## Options

The Throttle eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **expression** | **Required** Expression to configure the maximum number of messages to throttle per request. |  | ExpressionDefinition |
| **mode** | 
Sets the throttling mode to one of the available modes enumerated in ThrottlingMode.

Enum values:

-   TotalRequests
    
-   ConcurrentRequests
    





 | TotalRequests | ThrottlingMode |
| **correlationExpression** | The expression used to calculate the correlation key to use for throttle grouping. The Exchange which has the same correlation key is throttled together. |  | ExpressionSubElementDefinition |
| **executorService** | To use a custom thread pool (ScheduledExecutorService) by the throttler. |  | ExecutorService |
| **asyncDelayed** | Enables asynchronous delay which means the thread will not block while delaying. | false | Boolean |
| **callerRunsWhenRejected** | Whether or not the caller should run the task when it was rejected by the thread pool. Is by default true. | true | Boolean |
| **rejectExecution** | Whether or not throttler throws the ThrottlerRejectedExecutionException when the exchange exceeds the request limit Is by default false. | false | Boolean |
| **timePeriodMillis** | Sets the time period during which the maximum request count is valid for. | 1000 | String |

## Exchange properties

The Throttle eip has no exchange properties.

## Using Throttle

The below example will throttle messages received on seda:a before being sent to mock:result ensuring that a maximum of 3 messages is sent during a running 10-second window slot.

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .throttle(3).timePeriodMillis(10000)
  .to("mock:result");
```

```xml
<route>
  <from uri="seda:a"/>
  <throttle timePeriodMillis="10000">
    <constant>3</constant>
  </throttle>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - throttle:
            timePeriodMillis: 10000
            expression:
              constant:
                expression: 3
        - to:
            uri: mock:result
```

To use 10-seconds window, we set the `timePeriodMillis` to ten-thousand. The default value is 1000 (i.e., 1 second), meaning that setting just `throttle(3)` has the effect of setting the maximum number of requests per second.

To throttle by 50 requests per second, it would look like this:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .throttle(50)
  .to("seda:b");
```

```xml
<route>
  <from uri="seda:a"/>
  <throttle>
    <constant>50</constant>
  </throttle>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - throttle:
            expression:
              constant:
                expression: 50
        - to:
            uri: seda:b
```

### Dynamically changing maximum requests per period

The Throttler uses an [Expression](../../../manual/expression.md) to configure the number of requests. In all the examples from above, we used a [constant](../../4.18.x/languages/constant-language.md). However, the expression can be dynamic, such as determined from a message header from the current `Exchange`.

At runtime Camel evaluates the expression and converts the result to a `java.lang.Long` type. In the example below, we use a header from the message to determine the maximum requests per period. If the header is absent, then the Throttler uses the old value. This allows you to only provide a header if the value is to be changed:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .throttle(header("throttleValue")).timePeriodMillis(500)
  .to("seda:b")
```

```xml
<route>
  <from uri="seda:a"/>
  <throttle timePeriodMillis="500">
    <!-- use a header to determine how many messages to throttle per 0.5 sec -->
    <header>throttleValue</header>
  </throttle>
  <to uri="seda:b"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - throttle:
            timePeriodMillis: 500
            expression:
              header:
                expression: throttleValue
        - to:
            uri: seda:b
```

### Asynchronous delaying

You can let the Throttler use non-blocking asynchronous delaying, which means Camel will use a scheduler to schedule a task to be executed in the future. The task will then continue routing. This allows the caller thread to not block and be able to service other messages, etc.

You enable asynchronous delaying using `asyncDelayed` as shown:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .throttle(100).asyncDelayed()
  .to("seda:b");
```

```xml
<route>
  <from uri="seda:a"/>
  <throttle asyncDelayed="true">
    <constant>100</constant>
  </throttle>
  <to uri="seda:b"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - throttle:
            asyncDelayed: "true"
            expression:
              constant:
                expression: 100
        - to:
            uri: seda:b
```

### Rejecting processing if rate limit hit

When a message is being _throttled_ due the maximum request per limit has been reached, then the Throttler will by default wait until there is _free space_ before continue routing the message.

Instead of waiting you can also configure the Throttler to reject the message by throwing `ThrottlerRejectedExecutionException` exception.

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .throttle(100).rejectExecution(true)
  .to("seda:b");
```

```xml
<route>
  <from uri="seda:a"/>
  <throttle timePeriodMillis="100" rejectExecution="true">
    <constant>100</constant>
  </throttle>
  <to uri="seda:b"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - throttle:
            rejectExecution: "true"
            expression:
              constant:
                expression: 100
        - to:
            uri: seda:b
```

### Throttling per group

The Throttler will by default throttle all messages in the same group. However, it is possible to use a _correlation expression_ to diving into multiple groups, where each group is throttled independently.

For example, you can throttle by a [message](message.md) header as shown in the following example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .throttle(100).correlationExpression(header("region"))
  .to("seda:b");
```

```xml
<route>
  <from uri="seda:a"/>
  <throttle>
    <constant>100</constant>
    <correlationExpression>
      <header>region</header>
    </correlationExpression>
  </throttle>
  <to uri="seda:b"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - throttle:
            expression:
              constant:
                expression: 100
            correlationExpression:
              header:
                expression: region
        - to:
            uri: seda:b
```

In the example above, messages are throttled by the header with name region. So suppose there are regions for US, EMEA, and ASIA. Then we have three different groups that each are throttled by 100 messages per second.

## Throttling Modes

Apache Camel comes with two distinct throttling modes to control and manage the flow of requests in their applications.

These modes address different aspects of request handling:

**Total Requests Mode**

Throttles requests based on the total number of requests made within a defined unit of time. It regulates the overall traffic flow to prevent overwhelming the system with an excessive number of requests.

**Concurrent Connections Mode**

Throttles requests by managing concurrent connections using a [leaky bucket algorithm.](https://en.wikipedia.org/wiki/Leaky_bucket) This algorithm controls the rate at which requests are processed simultaneously, preventing system overload.

### Default Mode

By default, Camel uses the **Total Requests Mode** as the default throttling mechanism.

This means that, unless specified otherwise, the framework regulates the flow of requests based on the total number of requests per unit of time.

### Choosing Throttling Mode

Users can choose their preferred throttling mode using different approaches:

**DSL Methods**

-   `totalRequestsMode()`: Sets the total requests mode.
    
-   `concurrentRequestsMode()`: Sets the concurrent connections mode.
    

**Mode DSL Method**

-   `mode(String)`: Users can specify the throttling mode by passing either `TotalRequests` or `ConcurrentRequests` as an argument.
    

For example, `mode("ConcurrentRequests")` sets the throttling mode based on concurrent connections.

These options provide users with fine-grained control over how Camel manages the flow of requests, allowing them to choose the mode that best aligns with their specific application requirements.

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:a")
  .throttle(3).concurrentRequestsMode()
  .to("mock:result");
```

```xml
<route>
    <from uri="seda:a"/>
    <throttle mode="ConcurrentRequests">
        <constant>3</constant>
    </throttle>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:a
      steps:
        - throttle:
            mode: ConcurrentRequests
            expression:
              constant:
                expression: 3
        - to:
            uri: mock:result
```