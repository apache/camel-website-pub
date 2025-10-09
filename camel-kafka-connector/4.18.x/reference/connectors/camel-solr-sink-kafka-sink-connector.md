# camel-solr-sink-kafka-connector sink configuration

Connector Description: Send documents to Solr Collection.

When using camel-solr-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-solr-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.solrsink.CamelSolrsinkSinkConnector
```

The camel-solr-sink sink connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.solr-sink.collection** | **Required** Solr Collection name. |  | HIGH |
| **camel.kamelet.solr-sink.servers** | **Required** Comma separated list of Solr Servers and ports. |  | HIGH |
| **camel.kamelet.solr-sink.autocommit** | If autocommit should be enabled or not. | false | MEDIUM |
| **camel.kamelet.solr-sink.username** | Username to connect to Solr. |  | MEDIUM |
| **camel.kamelet.solr-sink.password** | Password to connect to Solr. |  | MEDIUM |

The camel-solr-sink sink connector has no converters out of the box.

The camel-solr-sink sink connector has no transforms out of the box.

The camel-solr-sink sink connector has no aggregation strategies out of the box.