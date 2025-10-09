# camel-infinispan-sink-kafka-connector sink configuration

Connector Description: Write object to an Infinispan cache.

When using camel-infinispan-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-infinispan-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.infinispansink.CamelInfinispansinkSinkConnector
```

The camel-infinispan-sink sink connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.infinispan-sink.cacheName** | **Required** The name of the Infinispan cache to use. |  | HIGH |
| **camel.kamelet.infinispan-sink.hosts** | **Required** Specifies the host of the cache on Infinispan instance. |  | HIGH |
| **camel.kamelet.infinispan-sink.secure** | If the Infinispan instance is secured or not. | true | MEDIUM |
| **camel.kamelet.infinispan-sink.username** | **Required** Username to connect to Infinispan. |  | HIGH |
| **camel.kamelet.infinispan-sink.password** | **Required** Password to connect to Infinispan. |  | HIGH |
| **camel.kamelet.infinispan-sink.saslMechanism** | The SASL Mechanism to use. | "DIGEST-MD5" | MEDIUM |
| **camel.kamelet.infinispan-sink.securityRealm** | Define the security realm to access the infinispan instance. | "default" | MEDIUM |
| **camel.kamelet.infinispan-sink.securityServerName** | Define the security server name to access the infinispan instance. | "infinispan" | MEDIUM |

The camel-infinispan-sink sink connector has no converters out of the box.

The camel-infinispan-sink sink connector has no transforms out of the box.

The camel-infinispan-sink sink connector has no aggregation strategies out of the box.