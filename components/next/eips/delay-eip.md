# Delay

The Delay EIP is used for delaying messages during routing.

## Options

The Delay eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **expression** | **Required** The expression that determines the delay duration in milliseconds. |  | ExpressionDefinition |
| **asyncDelayed** | Enables asynchronous delay which means the thread will not block while delaying. | true | Boolean |
| **callerRunsWhenRejected** | Whether or not the caller should run the task when it was rejected by the thread pool. | true | Boolean |
| **executorService** | To use a custom thread pool if asyncDelay has been enabled. |  | ExecutorService |

## Exchange properties

The Delay eip has no exchange properties.

## Example

The example below will delay all messages received on **seda:b** 1 second before sending them to **mock:result**.

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:b")
  .delay(1000)
  .to("mock:result");
```

```xml
<route>
    <from uri="seda:b"/>
    <delay>
        <constant>1000</constant>
    </delay>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:b
      steps:
        - delay:
            expression:
              constant: "1000"
        - to:
            uri: mock:result
```

Note that delay creates its own block, so some DSLs (including Java) require the delay block be closed:

_Java-only: closing the delay block with end() in Java DSL_

```java
.from("direct:delayBlockExample")
    .to("direct:getJobState")
    .loopDoWhile(simple("${body.state} = 'NOT_DONE'"))
        .log(LoggingLevel.DEBUG, "Pausing")
        .delay(10000)
            .syncDelayed()
        .end() // we must end the delay or else the log statement will be executed in each loop iteration
        .to("direct:getJobState")
    .end()
    .log("and we're done");
```

The delayed value can be a dynamic [Expression](../../../manual/expression.md).

For example, to delay a random between 1 and 5 seconds, we can use the [Simple](../languages/simple-language.md) language:

-   Java
    
-   XML
    
-   YAML
    

```java
from("seda:b")
  .delay(simple("${random(1000,5000)}"))
  .to("mock:result");
```

```xml
<route>
    <from uri="seda:b"/>
    <delay>
        <simple>${random(1000,5000)}</simple>
    </delay>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: seda:b
      steps:
        - delay:
            expression:
              simple:
                expression: "${random(1000,5000)}"
        - to:
            uri: mock:result
```

You can also call a [Bean Method](../languages/bean-language.md) to compute the delayed value from Java code:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:foo")
  .delay().method("someBean", "computeDelay")
  .to("activemq:bar");
```

```xml
<route>
    <from uri="activemq:foo"/>
    <delay>
        <method ref="someBean" method="computeDelay"/>
    </delay>
    <to uri="activemq:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq
      parameters:
        destinationName: foo
      steps:
        - delay:
            expression:
              method:
                ref: someBean
                method: computeDelay
        - to:
            uri: activemq
            parameters:
              destinationName: bar
```

Then the bean would look something like this:

_Java-only: bean class to compute the delay value_

```java
public class SomeBean {
  public long computeDelay() {
     long delay = 0;
     // use java code to compute a delay value in millis
     return delay;
 }
}
```

## Asynchronous delaying

You can let the Delayer use non-blocking asynchronous delaying, which means Camel will use scheduled thread pool (`ScheduledExecutorService`) to schedule a task to be executed in the future. This allows the caller thread to not block and be able to service other messages.

You use the `asyncDelayed()` to enable the async behavior.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:queue:foo")
  .delay(1000).asyncDelayed()
  .to("activemq:aDelayedQueue");
```

```xml
<route>
   <from uri="activemq:queue:foo"/>
   <delay asyncDelayed="true">
       <constant>1000</constant>
   </delay>
   <to uri="activemq:aDelayedQueue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:queue:foo
      steps:
        - delay:
            expression:
              constant: "1000"
            asyncDelayed: true
        - to:
            uri: activemq:aDelayedQueue
```