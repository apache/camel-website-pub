# Pausable

The Pausable EIP provides pause and resume features for supported consumers. With this EIP, it is possible to implement logic that controls the behavior of the consumer based on conditions that are external to the component. For instance, it makes it possible to pause the consumer if an external system becomes unavailable.

## EIP options

The Pausable eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **consumerListener** | **Required** The consumer listener to use for pausing and resuming the consumer. |  | ConsumerListener |
| **untilCheck** | **Required** Predicate to evaluate whether the processing can resume. Returns true if consumption can resume, or false otherwise. |  | Predicate |

## Example

To use the Pausable EIP, you need an instance of a consumer listener along with a predicate that tests whether consumption should continue.

-   Java
    

```java
from("kafka:topic")
    .pausable(new KafkaConsumerListener(), o -> canContinue())
    .process(exchange -> LOG.info("Received: {}", exchange.getMessage().getBody()))
    .to("direct:destination");
```

You can also integrate the Pausable EIP with the [Circuit Breaker EIP](circuitBreaker-eip.md) to pause consumption based on downstream system availability:

```java
from("kafka:topic")
    .pausable(new KafkaConsumerListener(), o -> canContinue())
    .circuitBreaker()
        .resilience4jConfiguration().circuitBreaker("pausableCircuit").end()
        .to("direct:downstream")
    .end();
```

## See Also

-   [Resume Strategies](resume-strategies.md)
    
-   [Resumable EIP](resumable-eip.md)