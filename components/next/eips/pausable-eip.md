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

## Message Body

The message body at each side of the Pausable EIP: _EIP input_ is the body it needs, _EIP output_ the body after it, and _Steps_ the body its own steps start with.

  
| Side | Body | Description |
| --- | --- | --- |
| **EIP output** | `unchanged` | Pauses the consumer while the condition holds: the body stays as it was. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Example

To use the Pausable EIP, you need an instance of a consumer listener along with a predicate that tests whether consumption should continue.

-   Java
    
-   XML
    
-   YAML
    

```java
from("kafka:topic")
    .pausable(new KafkaConsumerListener(), o -> canContinue())
    .process(exchange -> LOG.info("Received: {}", exchange.getMessage().getBody()))
    .to("direct:destination");
```

```xml
<route>
    <from uri="kafka:topic"/>
    <pausable consumerListener="kafkaConsumerListener" untilCheck="canContinue"/>
    <log message="Received: ${body}"/>
    <to uri="direct:destination"/>
</route>
```

```yaml
- route:
    from:
      uri: kafka:topic
      steps:
        - pausable:
            consumerListener: kafkaConsumerListener
            untilCheck: canContinue
        - log:
            message: "Received: ${body}"
        - to:
            uri: direct:destination
- beans:
    - name: kafkaConsumerListener
      type: org.apache.camel.component.kafka.consumer.errorhandler.KafkaConsumerListener
    - name: canContinue
      type: com.foo.CanContinuePredicate
```

You can also integrate the Pausable EIP with the [Circuit Breaker EIP](circuitBreaker-eip.md) to pause consumption based on downstream system availability:

-   Java
    
-   XML
    
-   YAML
    

```java
from("kafka:topic")
    .pausable(new KafkaConsumerListener(), o -> canContinue())
    .circuitBreaker()
        .resilience4jConfiguration().circuitBreaker("pausableCircuit").end()
        .to("direct:downstream")
    .end();
```

```xml
<route>
    <from uri="kafka:topic"/>
    <pausable consumerListener="kafkaConsumerListener" untilCheck="canContinue"/>
    <circuitBreaker>
        <resilience4jConfiguration circuitBreaker="pausableCircuit"/>
        <to uri="direct:downstream"/>
    </circuitBreaker>
</route>
```

```yaml
- route:
    from:
      uri: kafka:topic
      steps:
        - pausable:
            consumerListener: kafkaConsumerListener
            untilCheck: canContinue
        - circuitBreaker:
            resilience4jConfiguration:
              circuitBreaker: pausableCircuit
            steps:
              - to:
                  uri: direct:downstream
```

## See Also

-   [Resume Strategies](resume-strategies.md)
    
-   [Resumable EIP](resumable-eip.md)