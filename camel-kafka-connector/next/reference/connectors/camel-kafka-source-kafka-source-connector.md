# camel-kafka-source-kafka-connector source configuration

Connector Description: Receive data from Kafka topics.

When using camel-kafka-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkasource.CamelKafkasourceSourceConnector
```

The camel-kafka-source source connector supports 21 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-source.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-source.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-source.saslAuthType** | Authentication type to use. Use NONE for no authentication, PLAIN or SCRAM\_SHA\_256/SCRAM\_SHA\_512 for username/password, SSL for certificate-based, OAUTH for OAuth 2.0, AWS\_MSK\_IAM for MSK, or KERBEROS for Kerberos. | "NONE" | MEDIUM |
| **camel.kamelet.kafka-source.saslUsername** | Username for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. |  | MEDIUM |
| **camel.kamelet.kafka-source.saslPassword** | Password for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. |  | MEDIUM |
| **camel.kamelet.kafka-source.oauthClientId** | OAuth client ID. Required when saslAuthType is OAUTH. |  | MEDIUM |
| **camel.kamelet.kafka-source.oauthClientSecret** | OAuth client secret. Required when saslAuthType is OAUTH. |  | MEDIUM |
| **camel.kamelet.kafka-source.oauthTokenEndpointUri** | OAuth token endpoint URI. Required when saslAuthType is OAUTH. |  | MEDIUM |
| **camel.kamelet.kafka-source.oauthScope** | OAuth scope. Optional when saslAuthType is OAUTH. |  | MEDIUM |
| **camel.kamelet.kafka-source.sslTruststoreLocation** | The location of the trust store file. |  | MEDIUM |
| **camel.kamelet.kafka-source.sslTruststorePassword** | The password for the trust store file. |  | MEDIUM |
| **camel.kamelet.kafka-source.sslKeystoreLocation** | The location of the key store file. Used for mTLS authentication. |  | MEDIUM |
| **camel.kamelet.kafka-source.sslKeystorePassword** | The password for the key store file. |  | MEDIUM |
| **camel.kamelet.kafka-source.sslKeyPassword** | The password of the private key in the key store file. |  | MEDIUM |
| **camel.kamelet.kafka-source.autoCommitEnable** | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | true | MEDIUM |
| **camel.kamelet.kafka-source.allowManualCommit** | Whether to allow doing manual commits. | false | MEDIUM |
| **camel.kamelet.kafka-source.pollOnError** | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of DISCARD, ERROR\_HANDLER, RECONNECT, RETRY, STOP. | "ERROR\_HANDLER" | MEDIUM |
| **camel.kamelet.kafka-source.autoOffsetReset** | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | "latest" | MEDIUM |
| **camel.kamelet.kafka-source.consumerGroup** | A string that uniquely identifies the group of consumers to which this source belongs Example: my-group-id. |  | MEDIUM |
| **camel.kamelet.kafka-source.deserializeHeaders** | When enabled the Kamelet source will deserialize all message headers to String representation. | true | MEDIUM |
| **camel.kamelet.kafka-source.topicIsPattern** | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | false | MEDIUM |

The camel-kafka-source source connector has no converters out of the box.

The camel-kafka-source source connector has no transforms out of the box.

The camel-kafka-source source connector has no aggregation strategies out of the box.