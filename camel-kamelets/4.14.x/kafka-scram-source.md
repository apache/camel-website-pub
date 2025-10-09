# ![kafka scram source](_images/kamelets/kafka-scram-source.svg) Kafka Scram Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from Kafka topics through SCRAM login module.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-scram-source` Kamelet:

     
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
| **saslMechanism** | SASL Mechanism | The Simple Authentication and Security Layer (SASL) Mechanism used. | string | SCRAM-SHA-512 |  |
| **securityProtocol** | Security Protocol | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | string | SASL\_SSL |  |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |

## Dependencies

At runtime, the `kafka-scram-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:kafka-scram-source"
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

## Kafka-scram-source Kamelet Description

### Authentication methods

This Kamelet connects to Kafka using appropriate security mechanisms based on the configuration type:

-   Security settings as indicated by the kamelet name (SSL, SCRAM, not-secured)
    
-   Schema registry integration where applicable
    
-   Bootstrap servers configuration
    

### Output format

The Kamelet consumes messages from Kafka topics and produces the message data in the configured format.

### Configuration

The Kamelet requires Kafka connection parameters:

-   `topic`: The Kafka topic to consume from
    
-   `bootstrapServers`: Comma separated list of Kafka Broker URLs
    
-   Security-specific parameters based on the authentication method
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kafka-scram-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kafka-scram-source
    properties:
      topic: "my-topic"
      bootstrapServers: "kafka-broker1:9092,kafka-broker2:9092"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-scram-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-scram-source.kamelet.yaml)