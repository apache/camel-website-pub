# ![kafka batch source](_images/kamelets/kafka-batch-source.svg) Kafka Batch Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from Kafka topics in batch and commit them manually through KafkaManualCommit. This provides complete control over when messages are committed, allowing for custom processing logic before acknowledgment.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-batch-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **allowManualCommit** | Allow Manual Commit | Whether to allow doing manual commits. | boolean | false |  |
| **autoCommitEnable** | Auto Commit Enable | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | string | latest |  |
| **batchSize** | Batch Dimension | The maximum number of records returned in a single call to poll(). | integer | 500 |  |
| **batchingIntervalMs** | Batching Interval | In consumer batching mode, then this option is specifying a time in millis, to trigger batch completion eager when the current batch size has not reached the maximum size defined by maxPollRecords. Notice the trigger is not exact at the given interval, as this can only happen between kafka polls (see pollTimeoutMs option). | integer |  |  |
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers to which this source belongs. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | When enabled the Kamelet source will deserialize all message headers to String representation. | boolean | true |  |
| **maxPollIntervalMs** | Max Poll Interval | The maximum delay between invocations of poll() when using consumer group management. | integer |  |  |
| **oauthClientId** | OAuth Client ID | OAuth client ID. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthClientSecret** | OAuth Client Secret | OAuth client secret. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthScope** | OAuth Scope | OAuth scope. Optional when saslAuthType is OAUTH. | string |  |  |
| **oauthTokenEndpointUri** | OAuth Token Endpoint | OAuth token endpoint URI. Required when saslAuthType is OAUTH. | string |  |  |
| **pollOnError** | Poll On Error Behavior | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of DISCARD, ERROR\_HANDLER, RECONNECT, RETRY, STOP. | string | ERROR\_HANDLER |  |
| **pollTimeout** | Poll Timeout Interval | The timeout used when polling the KafkaConsumer. | integer | 5000 |  |
| **saslAuthType** | Authentication Type | Authentication type to use. Use NONE for no authentication, PLAIN or SCRAM\_SHA\_256/SCRAM\_SHA\_512 for username/password, SSL for certificate-based, OAUTH for OAuth 2.0, AWS\_MSK\_IAM for MSK, or KERBEROS for Kerberos. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string | NONE |  |
| **saslPassword** | Password | Password for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **saslUsername** | Username | Username for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **sslKeyPassword** | SSL Key Password | The password of the private key in the key store file. | string |  |  |
| **sslKeystoreLocation** | SSL Keystore Location | The location of the key store file. Used for mTLS authentication. | string |  |  |
| **sslKeystorePassword** | SSL Keystore Password | The password for the key store file. | string |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | The location of the trust store file. | string |  |  |
| **sslTruststorePassword** | SSL Truststore Password | The password for the trust store file. | string |  |  |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |

## Dependencies

At runtime, the `kafka-batch-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:kafka-batch-source"
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

## Kafka-batch-source Kamelet Description

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
  name: kafka-batch-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kafka-batch-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-source.kamelet.yaml)