# Multicast

The Multicast EIP allows to route **the same** message to a number of [endpoints](../../../manual/endpoint.md) and process them in a different way.

![image](_images/eip/RecipientListIcon.gif)

The Multicast EIP has many features and is also used as baseline for the [Recipient List](recipientList-eip.md) and [Split](split-eip.md) EIPs. For example the Multicast EIP is capable of aggregating each multicasted message into a single _response_ message as the result after the Multicast EIP.

## Options

The Multicast eip supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **aggregationStrategy** | Refers to an AggregationStrategy to be used to assemble the replies from the multicasts, into a single outgoing message from the Multicast. By default Camel will use the last reply as the outgoing message. You can also use a POJO as the AggregationStrategy. |  | AggregationStrategy |
| **aggregationStrategyMethodName** | This option can be used to explicit declare the method name to use, when using POJOs as the AggregationStrategy. |  | String |
| **aggregationStrategyMethodAllowNull** | If this option is false then the aggregate method is not used if there was no data to enrich. If this option is true then null values is used as the oldExchange (when no data to enrich), when using POJOs as the AggregationStrategy. | false | Boolean |
| **parallelAggregate** | If enabled then the aggregate method on AggregationStrategy can be called concurrently. Notice that this would require the implementation of AggregationStrategy to be implemented as thread-safe. By default this is false meaning that Camel synchronizes the call to the aggregate method. Though in some use-cases this can be used to archive higher performance when the AggregationStrategy is implemented as thread-safe. | false | Boolean |
| **parallelProcessing** | If enabled then sending messages to the multicasts occurs concurrently. Note the caller thread will still wait until all messages has been fully processed, before it continues. Its only the sending and processing the replies from the multicasts which happens concurrently. When parallel processing is enabled, then the Camel routing engin will continue processing using last used thread from the parallel thread pool. However, if you want to use the original thread that called the multicast, then make sure to enable the synchronous option as well. | false | Boolean |
| **synchronous** | Sets whether synchronous processing should be strictly used. When enabled then the same thread is used to continue routing after the multicast is complete, even if parallel processing is enabled. | false | Boolean |
| **streaming** | If enabled then Camel will process replies out-of-order, eg in the order they come back. If disabled, Camel will process replies in the same order as defined by the multicast. | false | Boolean |
| **stopOnException** | Will now stop further processing if an exception or failure occurred during processing of an org.apache.camel.Exchange and the caused exception will be thrown. Will also stop if processing the exchange failed (has a fault message) or an exception was thrown and handled by the error handler (such as using onException). In all situations the multicast will stop further processing. This is the same behavior as in pipeline, which is used by the routing engine. The default behavior is to not stop but continue processing till the end. | false | Boolean |
| **timeout** | Sets a total timeout specified in millis, when using parallel processing. If the Multicast hasn’t been able to send and process all replies within the given timeframe, then the timeout triggers and the Multicast breaks out and continues. Notice if you provide a TimeoutAwareAggregationStrategy then the timeout method is invoked before breaking out. If the timeout is reached with running tasks still remaining, certain tasks for which it is difficult for Camel to shut down in a graceful manner may continue to run. So use this option with a bit of care. | 0 | String |
| **executorService** | Refers to a custom Thread Pool to be used for parallel processing. Notice if you set this option, then parallel processing is automatic implied, and you do not have to enable that option as well. |  | ExecutorService |
| **onPrepare** | Uses the Processor when preparing the org.apache.camel.Exchange to be send. This can be used to deep-clone messages that should be send, or any custom logic needed before the exchange is send. |  | Processor |
| **shareUnitOfWork** | Shares the org.apache.camel.spi.UnitOfWork with the parent and each of the sub messages. Multicast will by default not share unit of work between the parent exchange and each multicasted exchange. This means each sub exchange has its own individual unit of work. | false | Boolean |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |

## Exchange properties

The following exchange properties are set on each `Exchange` that are multicasted:

  
| Property | Type | Description |
| --- | --- | --- |
| `CamelMulticastIndex` | `` `int` `` | An index counter that increases for each Exchange being multicasted. The counter starts from 0. |
| `CamelMulticastComplete` | `` `boolean` `` | Whether this Exchange is the last. |

## Using Multicast

The following example shows how to take a request from the direct:a endpoint, then multicast these request to direct:x, direct:y, and direct:z.

```java
from("direct:a")
  .multicast()
    .to("direct:x")
    .to("direct:y")
    .to("direct:z");
```

And in XML:

```xml
<route>
    <from uri="direct:a"/>
    <multicast>
        <to uri="direct:b"/>
        <to uri="direct:c"/>
        <to uri="direct:d"/>
    </multicast>
</route>
```

By default, Multicast EIP runs in single threaded mode, which mean that the next multicasted message is processed only when the previous is finished. This means that direct:b must be done before Camel will call direct:c and so on.

### Multicasting with parallel processing

You can enable parallel processing with Multicast EIP so each multicasted message is processed by its own thread in parallel.

The example below enabled parallel mode:

```java
from("direct:a")
  .multicast().parallelProcessing()
    .to("direct:x")
    .to("direct:y")
    .to("direct:z");
```

And in XML:

```xml
<route>
    <from uri="direct:a"/>
    <multicast parallelProcessing="true">
        <to uri="direct:b"/>
        <to uri="direct:c"/>
        <to uri="direct:d"/>
    </multicast>
</route>
```

> **Important**
> When parallel processing is enabled, then the Camel routing engin will continue processing using last used thread from the parallel thread pool. However, if you want to use the original thread that called the multicast, then make sure to enable the synchronous option as well.

### Ending a Multicast block

You may want to continue routing the exchange after the Multicast EIP. In Java DSL you need to use `end()` to mark where multicast ends, and where other EIPs can be added to continue the route.

In the example above then sending to mock:result happens after the Multicast EIP has finished. In other words direct:y, direct:y, and direct:z should be completed first, before the message continues.

```java
from("direct:a")
  .multicast().parallelProcessing()
    .to("direct:x")
    .to("direct:y")
    .to("direct:z")
  .end()
  .to("mock:result");
```

And in XML its intuitive as `</multicast>` marks the end of the block:

```xml
<route>
    <from uri="direct:a"/>
    <multicast parallelProcessing="true">
        <to uri="direct:b"/>
        <to uri="direct:c"/>
        <to uri="direct:d"/>
    </multicast>
    <to uri="mock:result"/>
</route>
```

### Aggregating

The `AggregationStrategy` is used for aggregating all the multicasted exchanges together as a single response exchange, that becomes the outgoing exchange after the Multicast EIP block.

The example now aggregates with the `MyAggregationStrategy` class:

```java
from("direct:start")
  .multicast(new MyAggregationStrategy()).parallelProcessing().timeout(500)
    .to("direct:x")
    .to("direct:y")
    .to("direct:z")
  .end()
  .to("mock:result");
```

And in XML we can refer to the FQN class name with `#class:` syntax as shown below:

```xml
<route>
    <from uri="direct:a"/>
    <multicast parallelProcessing="true" timeout="5000"
               aggreationStrategy="#class:com.foo.MyAggregationStrategy">
        <to uri="direct:b"/>
        <to uri="direct:c"/>
        <to uri="direct:d"/>
    </multicast>
    <to uri="mock:result"/>
</route>
```

> **Note**
> The Multicast, Recipient List, and Splitter EIPs have special support for using `AggregationStrategy` with access to the original input exchange. You may want to use this when you aggregate messages and there has been a failure in one of the messages, which you then want to enrich on the original input message and return as response; it’s the aggregate method with 3 exchange parameters.

### Stop processing in case of exception

The Multicast EIP will by default continue to process the entire exchange even in case one of the multicasted messages will throw an exception during routing.

For example if you want to multicast to 3 destinations and the 2nd destination fails by an exception. What Camel does by default is to process the remainder destinations. You have the chance to deal with the exception when aggregating using an `AggregationStrategy`.

But sometimes you just want Camel to stop and let the exception be propagated back, and let the Camel [Error Handler](../../../manual/error-handler.md) handle it. You can do this by specifying that it should stop in case of an exception occurred. This is done by the `stopOnException` option as shown below:

```java
from("direct:start")
    .multicast()
        .stopOnException().to("direct:foo", "direct:bar", "direct:baz")
    .end()
    .to("mock:result");

    from("direct:foo").to("mock:foo");

    from("direct:bar").process(new MyProcessor()).to("mock:bar");

    from("direct:baz").to("mock:baz");
```

In the example above, then `MyProcessor` is causing a failure and throws an exception. This means the Multicast EIP will stop after this, and not the last route (direct:baz).

And using XML DSL you specify it as follows:

```xml
<routes>
    <route>
        <from uri="direct:start"/>
        <multicast stopOnException="true">
            <to uri="direct:foo"/>
            <to uri="direct:bar"/>
            <to uri="direct:baz"/>
        </multicast>
        <to uri="mock:result"/>
    </route>

    <route>
        <from uri="direct:foo"/>
        <to uri="mock:foo"/>
    </route>

    <route>
        <from uri="direct:bar"/>
        <process ref="myProcessor"/>
        <to uri="mock:bar"/>
    </route>

    <route>
        <from uri="direct:baz"/>
        <to uri="mock:baz"/>
    </route>
</routes>
```

### Preparing the message by deep copying before multicasting

The multicast EIP will copy the source exchange and multicast each copy. However, the copy is a shallow copy, so in case you have mutable message bodies, then any changes will be visible by the other copied messages. If you want to use a deep clone copy then you need to use a custom `onPrepare` which allows you to create a deep copy of the message body in the `Processor`.

Notice the `onPrepare` can be used for any kind of custom logic which you would like to execute before the [Exchange](../../../manual/exchange.md) is being multicasted.

## See Also

Because Multicast EIP is baseline for the [Recipient List](recipientList-eip.md) and [Split](split-eip.md) EIPs, then you can find more information in those EIPs about features that is also available with Multicast EIP.