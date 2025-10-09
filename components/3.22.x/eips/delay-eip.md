# Delay

The Delay EIP is used for delaying messages during routing.

## Options

The Delay eip supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **expression** | **Required** Expression to define how long time to wait (in millis). |  | ExpressionDefinition |
| **asyncDelayed** | Enables asynchronous delay which means the thread will not block while delaying. | true | Boolean |
| **callerRunsWhenRejected** | Whether or not the caller should run the task when it was rejected by the thread pool. Is by default true. | true | Boolean |
| **executorService** | To use a custom Thread Pool if asyncDelay has been enabled. |  | ExecutorService |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Example

The example below will delay all messages received on **seda:b** 1 second before sending them to **mock:result**.

```java
from("seda:b")
  .delay(1000)
  .to("mock:result");
```

And in XML:

```xml
<route>
    <from uri="seda:b"/>
    <delay>
        <constant>1000</constant>
    </delay>
    <to uri="mock:result"/>
</route>
```

Note that delay creates its own block, so some DSLs (including Java) require the delay block be closed:

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

For example to delay a random between 1 and 5 seconds, we can use the [Simple](../languages/simple-language.md) language:

```java
from("seda:b")
  .delay(simple("${random(1000,5000)}"))
  .to("mock:result");
```

And in XML DSL:

```xml
<route>
    <from uri="seda:b"/>
    <delay>
        <simple>${random(1000,5000)}</simple>
    </delay>
    <to uri="mock:result"/>
</route>
```

You can also call a [Bean Method](../languages/bean-language.md) to compute the delayed value from Java code:

```java
from("activemq:foo")
  .delay().method("someBean", "computeDelay")
  .to("activemq:bar");
```

Then the bean would look something like this:

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

```java
from("activemq:queue:foo")
  .delay(1000).asyncDelayed()
  .to("activemq:aDelayedQueue");
```

In XML DSL you use the `asyncDelayed` attribute to enable the async mode:

```xml
<route>
   <from uri="activemq:queue:foo"/>
   <delay asyncDelayed="true">
       <constant>1000</constant>
   </delay>
   <to uri="activemq:aDealyedQueue"/>
</route>
```