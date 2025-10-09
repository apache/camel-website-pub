# camel-kafka-ssl-sink-kafka-connector sink configuration

Connector Description: Send data to Kafka topics wit TLS/SSL support.

When using camel-kafka-ssl-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-ssl-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkasslsink.CamelKafkasslsinkSinkConnector
```

The camel-kafka-ssl-sink sink connector supports 12 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-ssl-sink.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-ssl-sink.sslKeystoreLocation** | **Required** The location of the key store file. This is optional for client and can be used for two-way authentication for client. |  | HIGH |
| **camel.kamelet.kafka-ssl-sink.sslProtocol** | The SSL protocol used to generate the SSLContext. Default setting is TLS, which is fine for most cases. Allowed values in recent JVMs are TLS, TLSv1.1 and TLSv1.2. SSL, SSLv2 and SSLv3 may be supported in older JVMs, but their usage is discouraged due to known security vulnerabilities. | "TLSv1.2" | MEDIUM |
| **camel.kamelet.kafka-ssl-sink.saslMechanism** | The Simple Authentication and Security Layer (SASL) Mechanism used. | "GSSAPI" | MEDIUM |
| **camel.kamelet.kafka-ssl-sink.sslEnabledProtocols** | The list of protocols enabled for SSL connections. TLSv1.2, TLSv1.1 and TLSv1 are enabled by default. | "TLSv1.2,TLSv1.1,TLSv1" | MEDIUM |
| **camel.kamelet.kafka-ssl-sink.sslKeystorePassword** | **Required** The store password for the key store file.This is optional for client and only needed if ssl.keystore.location is configured. |  | HIGH |
| **camel.kamelet.kafka-ssl-sink.sslTruststoreLocation** | **Required** The location of the trust store file. |  | HIGH |
| **camel.kamelet.kafka-ssl-sink.sslTruststorePassword** | **Required** The store password for the trust store file. |  | HIGH |
| **camel.kamelet.kafka-ssl-sink.sslKeyPassword** | **Required** The password of the private key in the key store file. |  | HIGH |
| **camel.kamelet.kafka-ssl-sink.sslEndpointAlgorithm** | The endpoint identification algorithm to validate server hostname using server certificate. Use none or false to disable server hostname verification. | "https" | MEDIUM |
| **camel.kamelet.kafka-ssl-sink.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-ssl-sink.securityProtocol** | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | "SSL" | MEDIUM |

The camel-kafka-ssl-sink sink connector has no converters out of the box.

The camel-kafka-ssl-sink sink connector has no transforms out of the box.

The camel-kafka-ssl-sink sink connector has no aggregation strategies out of the box.