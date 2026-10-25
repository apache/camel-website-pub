# Resumable

The Resumable EIP allows consuming data from the last known offset after a restart, using a resume strategy to track and restore the position.

This is useful when consuming large data sources where you want to avoid reprocessing data that has already been consumed. The resume strategy points the consumer to the exact offset to resume operations.

## EIP options

The Resumable eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **resumeStrategy** | **Required** The resume strategy to use for resuming processing from the last known offset. |  | ResumeStrategy |
| **loggingLevel** | 
The logging level to use in case of failures.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | ERROR | LoggingLevel |
| **intermittent** | Whether the offsets will be intermittently present or whether they must be present in every exchange. | false | Boolean |

## Message Body

The message body at each side of the Resumable EIP: _EIP input_ is the body it needs, _EIP output_ the body after it, and _Steps_ the body its own steps start with.

  
| Side | Body | Description |
| --- | --- | --- |
| **EIP output** | `unchanged` | Records where the consumer is: the body stays as it was. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Example

-   Java
    
-   XML
    
-   YAML
    

```java
KafkaResumeStrategyConfigurationBuilder kafkaConfigurationBuilder =
    KafkaResumeStrategyConfigurationBuilder.newBuilder()
        .withBootstrapServers("kafka-address:9092")
        .withTopic("offset")
        .withResumeCache(new MyChoiceOfResumeCache<>(100));

from("some:component")
    .resumable().configuration(kafkaConfigurationBuilder)
    .process(this::process);
```

```xml
<route>
    <from uri="some:component"/>
    <resumable resumeStrategy="kafkaResumeStrategy"/>
    <process ref="myProcessor"/>
</route>
```

```yaml
- route:
    from:
      uri: some:component
      steps:
        - resumable:
            resumeStrategy: kafkaResumeStrategy
        - process:
            ref: myProcessor
```

> **Note**
> The configuration builder is only available in the Java DSL. In XML and YAML, the `resumeStrategy` option refers to a resume strategy bean by its name. In this example, `kafkaResumeStrategy` is a `SingleNodeKafkaResumeStrategy` bean set up with the same configuration.

### Intermittent Mode

Enable intermittent mode to avoid updating the offset for every exchange:

-   Java
    
-   XML
    
-   YAML
    

```java
from("some:component")
    .resumable().resumeStrategy(new MyTestResumeStrategy()).intermittent(true)
    .process(this::process);
```

```xml
<route>
    <from uri="some:component"/>
    <resumable resumeStrategy="testResumeStrategy" intermittent="true"/>
    <process ref="myProcessor"/>
</route>
```

```yaml
- route:
    from:
      uri: some:component
      steps:
        - resumable:
            resumeStrategy: testResumeStrategy
            intermittent: true
        - process:
            ref: myProcessor
- beans:
    - name: testResumeStrategy
      type: com.foo.MyTestResumeStrategy
```

## See Also

-   [Resume Strategies](resume-strategies.md)
    
-   [Pausable EIP](pausable-eip.md)