# camel-kafka-batch-ssl-source-kafka-connector source configuration

Connector Description: Receive data from Kafka topics in batch with SSL/TLS support and commit them manually through KafkaManualCommit or automatically.

When using camel-kafka-batch-ssl-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-batch-ssl-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkabatchsslsource.CamelKafkabatchsslsourceSourceConnector
```

The camel-kafka-batch-ssl-source source connector supports 23 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-batch-ssl-source.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-batch-ssl-source.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-batch-ssl-source.securityProtocol** | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | "SSL" | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.saslMechanism** | The Simple Authentication and Security Layer (SASL) Mechanism used. | "GSSAPI" | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.autoCommitEnable** | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | true | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.allowManualCommit** | Whether to allow doing manual commits. | false | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.pollOnError** | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | "ERROR\_HANDLER" | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.autoOffsetReset** | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | "latest" | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.consumerGroup** | A string that uniquely identifies the group of consumers to which this source belongs Example: my-group-id. |  | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.deserializeHeaders** | When enabled the Kamelet source will deserialize all message headers to String representation. | true | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.sslKeyPassword** | **Required** The password of the private key in the key store file. |  | HIGH |
| **camel.kamelet.kafka-batch-ssl-source.sslKeystorePassword** | The store password for the key store file.This is optional for client and only needed if ssl.keystore.location is configured. |  | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.sslEndpointAlgorithm** | The endpoint identification algorithm to validate server hostname using server certificate. Use none or false to disable server hostname verification. | "https" | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.sslProtocol** | The SSL protocol used to generate the SSLContext. Default setting is TLS, which is fine for most cases. Allowed values in recent JVMs are TLS, TLSv1.1 and TLSv1.2. SSL, SSLv2 and SSLv3 may be supported in older JVMs, but their usage is discouraged due to known security vulnerabilities. | "TLSv1.2" | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.sslKeystoreLocation** | The location of the key store file. This is optional for client and can be used for two-way authentication for client. |  | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.sslTruststoreLocation** | **Required** The location of the trust store file. |  | HIGH |
| **camel.kamelet.kafka-batch-ssl-source.sslEnabledProtocols** | The list of protocols enabled for SSL connections. TLSv1.2, TLSv1.1 and TLSv1 are enabled by default. | "TLSv1.2,TLSv1.1,TLSv1" | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.saslJaasConfig** | Java Authentication and Authorization Service (JAAS) for Simple Authentication and Security Layer (SASL) configuration. |  | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.batchSize** | The maximum number of records returned in a single call to poll(). | 500 | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.pollTimeout** | The timeout used when polling the KafkaConsumer. | 5000 | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.maxPollIntervalMs** | The maximum delay between invocations of poll() when using consumer group management. |  | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.batchingIntervalMs** | In consumer batching mode, then this option is specifying a time in millis, to trigger batch completion eager when the current batch size has not reached the maximum size defined by maxPollRecords. Notice the trigger is not exact at the given interval, as this can only happen between kafka polls (see pollTimeoutMs option). |  | MEDIUM |
| **camel.kamelet.kafka-batch-ssl-source.topicIsPattern** | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | false | MEDIUM |

The camel-kafka-batch-ssl-source source connector has no converters out of the box.

The camel-kafka-batch-ssl-source source connector has no transforms out of the box.

The camel-kafka-batch-ssl-source source connector has no aggregation strategies out of the box.