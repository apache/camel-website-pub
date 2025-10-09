# ![kafka source](_images/kamelets/kafka-source.svg) Kafka Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from Kafka topics through Plain Login Module.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **password** | Password | **Required** Password to authenticate to kafka. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **user** | Username | **Required** Username to authenticate to Kafka. | string |  |  |
| **allowManualCommit** | Allow Manual Commit | Whether to allow doing manual commits. | boolean | false |  |
| **autoCommitEnable** | Auto Commit Enable | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | string | latest |  |
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers to which this source belongs. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | When enabled the Kamelet source will deserialize all message headers to String representation. | boolean | true |  |
| **pollOnError** | Poll On Error Behavior | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | string | ERROR\_HANDLER |  |
| **saslMechanism** | SASL Mechanism | The Simple Authentication and Security Layer (SASL) Mechanism used. | string | PLAIN |  |
| **securityProtocol** | Security Protocol | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | string | SASL\_SSL |  |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |

## Dependencies

At runtime, the `kafka-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kafka
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka Source Kamelet Description

### Authentication

This Kamelet requires SASL/PLAIN authentication to connect to Kafka through a Plain Login Module. The credentials are configured through the `user` and `password` properties.

### Configuration

The Kafka Source Kamelet supports the following configurations:

-   **Topic**: Comma-separated list of Kafka topic names to consume from (required)
    
-   **Bootstrap Servers**: Comma-separated list of Kafka bootstrap servers (required)
    
-   **User**: Username for SASL/PLAIN authentication (required)
    
-   **Password**: Password for SASL/PLAIN authentication (required)
    
-   **Consumer Group**: Kafka consumer group ID for managing offsets
    
-   **Auto Offset Reset**: What to do when there is no initial offset (earliest, latest, none)
    
-   **Allow Manual Commit**: Enable manual commit for better control over message processing
    

### Output Format

The Kamelet outputs Kafka message content and includes Kafka headers and metadata such as topic, partition, offset, and timestamp.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "orders,payments"
        bootstrapServers: "kafka.example.com:9092"
        user: "kafka-user"
        password: "kafka-password"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Consumer Group

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "user-events"
        bootstrapServers: "kafka1.example.com:9092,kafka2.example.com:9092"
        user: "kafka-user"
        password: "kafka-password"
        consumerGroup: "my-consumer-group"
        autoOffsetReset: "earliest"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Security

This kamelet uses SASL/PLAIN authentication mechanism with TLS encryption enabled for secure communication with Kafka brokers.

### Error Handling

The consumer automatically handles connection failures and will attempt to reconnect to the Kafka cluster. Failed message processing can be handled through Camel’s error handling mechanisms.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-source.kamelet.yaml)