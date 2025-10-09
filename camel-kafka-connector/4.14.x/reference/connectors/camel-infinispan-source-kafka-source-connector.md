# camel-infinispan-source-kafka-connector source configuration

Connector Description: Get Events from an Infinispan cache

When using camel-infinispan-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-infinispan-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.infinispansource.CamelInfinispansourceSourceConnector
```

The camel-infinispan-source source connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.infinispan-source.cacheName** | **Required** The name of the Infinispan cache to use. |  | HIGH |
| **camel.kamelet.infinispan-source.hosts** | **Required** Specifies the host of the cache on Infinispan instance. |  | HIGH |
| **camel.kamelet.infinispan-source.secure** | If the Infinispan instance is secured or not. | true | MEDIUM |
| **camel.kamelet.infinispan-source.username** | **Required** Username to connect to Infinispan. |  | HIGH |
| **camel.kamelet.infinispan-source.password** | **Required** Password to connect to Infinispan. |  | HIGH |
| **camel.kamelet.infinispan-source.saslMechanism** | The SASL Mechanism to use. | "DIGEST-MD5" | MEDIUM |
| **camel.kamelet.infinispan-source.securityRealm** | Define the security realm to access the infinispan instance. | "default" | MEDIUM |
| **camel.kamelet.infinispan-source.securityServerName** | Define the security server name to access the infinispan instance. | "infinispan" | MEDIUM |
| **camel.kamelet.infinispan-source.eventTypes** | Specifies the set of event types to register by the consumer. Multiple event can be separated by comma without spaces. Example: CLIENT\_CACHE\_ENTRY\_CREATED,CLIENT\_CACHE\_ENTRY\_MODIFIED. | "CLIENT\_CACHE\_ENTRY\_CREATED,CLIENT\_CACHE\_ENTRY\_MODIFIED,CLIENT\_CACHE\_ENTRY\_REMOVED,CLIENT\_CACHE\_ENTRY\_EXPIRED,CLIENT\_CACHE\_FAILOVER" | MEDIUM |

The camel-infinispan-source source connector has no converters out of the box.

The camel-infinispan-source source connector has no transforms out of the box.

The camel-infinispan-source source connector has no aggregation strategies out of the box.