# Wire Tap

[Wire Tap](http://www.enterpriseintegrationpatterns.com/WireTap.md) from the [EIP patterns](enterprise-integration-patterns.md) allows you to route messages to a separate location while they are being forwarded to the ultimate destination.

![image](_images/eip/WireTap.gif)

## Options

The Wire Tap eip supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **copy** | Whether to use a copy of the original exchange. | true | Boolean |
| **dynamicUri** | Whether the uri is dynamic or static. If dynamic then the simple language is used to evaluate a dynamic uri to use as the wire-tap destination, for each incoming message. | true | Boolean |
| **onPrepare** | Uses a processor when preparing the exchange to be sent. This can be used to deep-clone messages, or any custom logic needed before the exchange is sent. |  | Processor |
| **executorService** | Uses a custom thread pool for sending tapped exchanges. |  | ExecutorService |
| **uri** | **Required** The uri of the endpoint to send to. The uri can be dynamic computed using the simple language. |  | String |
| **variableSend** | To use a variable as the source for the message body to send. This makes it handy to use variables for user data and to easily control what data to use for sending and receiving. |  | String |
| **variableReceive** | To use a variable to store the received message body (only body, not headers). This makes it handy to use variables for user data and to easily control what data to use for sending and receiving. |  | String |
| **cacheSize** | Sets the maximum size used by the ProducerCache which is used to cache and reuse producers when uris are reused. Use 0 for default cache size, or -1 to turn cache off. |  | Integer |
| **ignoreInvalidEndpoint** | Whether to ignore invalid endpoint URIs and skip sending the message. | false | Boolean |
| **allowOptimisedComponents** | Whether to allow components to optimise toD if they are SendDynamicAware. | true | Boolean |
| **autoStartComponents** | Whether to auto startup components when toD is starting up. | true | Boolean |

## Exchange properties

The Wire Tap eip supports 1 exchange properties, which are listed below.

The exchange properties are set on the `Exchange` by the EIP, unless otherwise specified in the description. This means those properties are available after this EIP has completed processing the `Exchange`.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelToEndpoint** | Endpoint URI where this Exchange is being sent to. |  | String |

## Wire Tap

Camel’s Wire Tap will copy the original [Exchange](../../../manual/exchange.md) and set its [Exchange Pattern](../../../manual/exchange-pattern.md) to **`InOnly`**, as we want the tapped [Exchange](../../../manual/exchange.md) to be sent in a fire and forget style. The tapped [Exchange](../../../manual/exchange.md) is then sent in a separate thread, so it can run in parallel with the original. Beware that only the `Exchange` is copied - Wire Tap won’t do a deep clone (unless you specify a custom processor via **`onPrepare`** which does that). So all copies could share objects from the original `Exchange`.

### Using Wire Tap

In the example below, the exchange is wire tapped to the direct:tap route. This route delays message 1 second before continuing. This is because it allows you to see that the tapped message is routed independently of the original route, so that you would see log:result happens before log:tap

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("log:foo")
    .wireTap("direct:tap")
    .to("log:result");

from("direct:tap")
    .delay(1000).setBody().constant("Tapped")
    .to("log:tap");
```

```xml
<routes>

  <route>
    <from uri="direct:start"/>
    <wireTap uri="direct:tap"/>
    <to uri="log:result"/>
  </route>

  <route>
    <from uri="direct:tap"/>
    <to uri="log:log"/>
  </route>

</routes>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: log:foo
        - wireTap:
            uri: direct:tap
        - to:
            uri: log:result
- route:
    from:
      uri: direct:tap
      steps:
        - delay:
            expression:
              constant:
                expression: 1000
        - setBody:
            expression:
              constant:
                expression: Tapped
        - to:
            uri: log:tap
```

### Wire tapping with dynamic URIs

For example, to wire tap to a dynamic URI, then the URI uses the [Simple](../../4.18.x/languages/simple-language.md) language that allows to construct dynamic URIs.

For example, to wire tap to a JMS queue where the header ID is part of the queue name:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .wireTap("jms:queue:backup-${header.id}")
    .to("bean:doSomething");
```

```xml
<route>
  <from uri="direct:start"/>
  <wireTap uri="jms:queue:backup-${header.id}"/>
  <to uri="bean:doSomething"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - wireTap:
            uri: "jms:queue:backup-${header.id}"
        - to:
            uri: bean:doSomething
```

## WireTap Thread Pools

The WireTap uses a thread pool to process the tapped messages. This thread pool will by default use the settings detailed in the [Threading Model](../../../manual/threading-model.md).

In particular, when the pool is exhausted (with all threads used), further wiretaps will be executed synchronously by the calling thread. To remedy this, you can configure an explicit thread pool on the Wire Tap having either a different rejection policy, a larger worker queue, or more worker threads.

## Wire tapping Streaming based messages

If you Wire Tap a stream message body, then you should consider enabling [Stream caching](../../../manual/stream-caching.md) to ensure the message body can be read at each endpoint.

See more details at [Stream caching](../../../manual/stream-caching.md).