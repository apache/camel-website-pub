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

## Example

-   Java
    

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

### Intermittent Mode

Enable intermittent mode to avoid updating the offset for every exchange:

```java
from("some:component")
    .resumable(new MyTestResumeStrategy()).intermittent(true)
    .process(this::process);
```

## See Also

-   [Resume Strategies](resume-strategies.md)
    
-   [Pausable EIP](pausable-eip.md)