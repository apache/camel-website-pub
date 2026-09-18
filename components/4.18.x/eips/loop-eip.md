# Loop

The Loop EIP allows for processing a message a number of times, possibly in a different way for each iteration.

## Options

The Loop eip supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **expression** | **Required** Expression to define how many times we should loop. Notice the expression is only evaluated once, and should return a number as how many times to loop. A value of zero or negative means no looping. The loop is like a for-loop fashion, if you want a while loop, then the dynamic router may be a better choice. |  | ExpressionDefinition |
| **copy** | If the copy attribute is true, a copy of the input Exchange is used for each iteration. That means each iteration will start from a copy of the same message. By default loop will loop the same exchange all over, so each iteration may have different message content. | false | Boolean |
| **doWhile** | Enables the while loop that loops until the predicate evaluates to false or null. | false | Boolean |
| **breakOnShutdown** | If the breakOnShutdown attribute is true, then the loop will not iterate until it reaches the end when Camel is shut down. | false | Boolean |
| **onPrepare** | Uses the Processor when preparing the org.apache.camel.Exchange for each loop iteration. This can be used to deep-clone messages, or any custom logic needed before the looping executes. |  | Processor |
| **outputs** | **Required** |  | List |

## Exchange properties

The Loop eip supports 2 exchange properties, which are listed below.

The exchange properties are set on the `Exchange` by the EIP, unless otherwise specified in the description. This means those properties are available after this EIP has completed processing the `Exchange`.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLoopIndex** | Index of the current iteration (0 based). |  | int |
| **CamelLoopSize** | Total number of loops. This is not available if running the loop in while loop mode. |  | int |

## Looping modes

The Loop EIP can run in three modes: default, copy, or while mode.

In default mode the Loop EIP uses the same `Exchange` instance throughout the looping. So the result from the previous iteration will be used for the next iteration.

In the copy mode, then the Loop EIP uses a copy of the original `Exchange` in each iteration. So the result from the previous iteration will **not** be used for the next iteration.

In the while mode, then the Loop EIP will keep looping until the expression evaluates to `false` or `null`.

> **Note**
> The Loop EIP is not intended to be looping a very high number. So keep the number of loops to a reasonable number such as 10000 or less. A very high number can degrade performance.

## Example

The following example shows how to take a request from the `direct:x` endpoint, then send the message repetitively to `mock:result`.

The number of times the message is sent is either passed as an argument to `loop`, or determined at runtime by evaluating an expression.

The [Expression](../../../manual/expression.md) **must** evaluate to an `int`, otherwise a `RuntimeCamelException` is thrown.

Pass loop count as an argument:

-   Java
    
-   XML
    

```java
from("direct:a")
    .loop(8)
        .to("mock:result");
```

```xml
<route>
  <from uri="direct:a"/>
  <loop>
    <constant>8</constant>
    <to uri="mock:result"/>
  </loop>
</route>
```

Use expression to determine loop count:

-   Java
    
-   XML
    

```java
from("direct:b")
    .loop(header("loop"))
        .to("mock:result");
```

```xml
<route>
  <from uri="direct:b"/>
  <loop>
    <header>loop</header>
    <to uri="mock:result"/>
  </loop>
</route>
```

And with the [XPath](../languages/xpath-language.md) language:

```java
from("direct:c")
    .loop(xpath("/hello/@times"))
        .to("mock:result");
```

## Using copy mode

Now suppose we send a message to direct:start endpoint containing the letter A. The output of processing this route will be that, each mock:loop endpoint will receive AB as the message.

-   Java
    
-   XML
    

```java
from("direct:start")
    // instruct loop to use copy mode, which mean it will use a copy of the input exchange
    // for each loop iteration, instead of keep using the same exchange all over
    .loop(3).copy()
        .transform(body().append("B"))
        .to("mock:loop")
    .end() // end loop
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <!-- enable copy mode for loop eip -->
  <loop copy="true">
    <constant>3</constant>
    <transform>
      <simple>${body}B</simple>
    </transform>
    <to uri="mock:loop"/>
  </loop>
  <to uri="mock:result"/>
</route>
```

However, if we do **not** enable copy mode, then mock:loop will receive `_"AB"_`, `_"ABB"_`, `_"ABBB"_`, etc. messages.

## Looping using while

The loop can act like a while loop that loops until the expression evaluates to `false` or `null`.

For example, the route below loops while the length of the message body is five or fewer characters. Notice that the DSL uses `loopDoWhile`.

-   Java
    
-   XML
    

```java
from("direct:start")
    .loopDoWhile(simple("${body.length} <= 5"))
        .to("mock:loop")
        .transform(body().append("A"))
    .end() // end loop
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <loop doWhile="true">
    <simple>${body.length} &lt;= 5</simple>
    <to uri="mock:loop"/>
    <transform>
      <simple>A${body}</simple>
    </transform>
  </loop>
  <to uri="mock:result"/>
</route>
```

Notice that the while loop is turned on using the `doWhile` attribute.