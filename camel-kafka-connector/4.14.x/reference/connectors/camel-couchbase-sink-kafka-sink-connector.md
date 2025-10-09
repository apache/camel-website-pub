# camel-couchbase-sink-kafka-connector sink configuration

Connector Description: Send documents to Couchbase.

When using camel-couchbase-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-couchbase-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.couchbasesink.CamelCouchbasesinkSinkConnector
```

The camel-couchbase-sink sink connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.couchbase-sink.protocol** | **Required** The protocol to use. |  | HIGH |
| **camel.kamelet.couchbase-sink.couchbaseHostname** | **Required** The hostname to use. |  | HIGH |
| **camel.kamelet.couchbase-sink.couchbasePort** | The port to use. | 8091 | MEDIUM |
| **camel.kamelet.couchbase-sink.bucket** | **Required** The bucket to use. |  | HIGH |
| **camel.kamelet.couchbase-sink.username** | Username to connect to Couchbase. |  | MEDIUM |
| **camel.kamelet.couchbase-sink.password** | Password to connect to Couchbase. |  | MEDIUM |
| **camel.kamelet.couchbase-sink.startingId** | The starting id. | 1 | MEDIUM |
| **camel.kamelet.couchbase-sink.autoStartId** | Auto Start Id or not. | true | MEDIUM |

The camel-couchbase-sink sink connector has no converters out of the box.

The camel-couchbase-sink sink connector has no transforms out of the box.

The camel-couchbase-sink sink connector has no aggregation strategies out of the box.