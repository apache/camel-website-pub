# camel-kafka-sink-kafka-connector sink configuration

Connector Description: Send data to Kafka topics.

When using camel-kafka-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkasink.CamelKafkasinkSinkConnector
```

The camel-kafka-sink sink connector supports 14 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-sink.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-sink.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-sink.saslAuthType** | Authentication type to use. Use NONE for no authentication, PLAIN or SCRAM\_SHA\_256/SCRAM\_SHA\_512 for username/password, SSL for certificate-based, OAUTH for OAuth 2.0, AWS\_MSK\_IAM for MSK, or KERBEROS for Kerberos. | "NONE" | MEDIUM |
| **camel.kamelet.kafka-sink.saslUsername** | Username for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. |  | MEDIUM |
| **camel.kamelet.kafka-sink.saslPassword** | Password for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. |  | MEDIUM |
| **camel.kamelet.kafka-sink.oauthClientId** | OAuth client ID. Required when saslAuthType is OAUTH. |  | MEDIUM |
| **camel.kamelet.kafka-sink.oauthClientSecret** | OAuth client secret. Required when saslAuthType is OAUTH. |  | MEDIUM |
| **camel.kamelet.kafka-sink.oauthTokenEndpointUri** | OAuth token endpoint URI. Required when saslAuthType is OAUTH. |  | MEDIUM |
| **camel.kamelet.kafka-sink.oauthScope** | OAuth scope. Optional when saslAuthType is OAUTH. |  | MEDIUM |
| **camel.kamelet.kafka-sink.sslTruststoreLocation** | The location of the trust store file. |  | MEDIUM |
| **camel.kamelet.kafka-sink.sslTruststorePassword** | The password for the trust store file. |  | MEDIUM |
| **camel.kamelet.kafka-sink.sslKeystoreLocation** | The location of the key store file. Used for mTLS authentication. |  | MEDIUM |
| **camel.kamelet.kafka-sink.sslKeystorePassword** | The password for the key store file. |  | MEDIUM |
| **camel.kamelet.kafka-sink.sslKeyPassword** | The password of the private key in the key store file. |  | MEDIUM |

The camel-kafka-sink sink connector has no converters out of the box.

The camel-kafka-sink sink connector has no transforms out of the box.

The camel-kafka-sink sink connector has no aggregation strategies out of the box.