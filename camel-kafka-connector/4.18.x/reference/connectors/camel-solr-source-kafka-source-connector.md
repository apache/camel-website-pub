# camel-solr-source-kafka-connector source configuration

Connector Description: Query for documents to Solr Collection.

When using camel-solr-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-solr-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.solrsource.CamelSolrsourceSourceConnector
```

The camel-solr-source source connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.solr-source.period** | **Required** The interval between fetches to the Solr collection. | 10000 | HIGH |
| **camel.kamelet.solr-source.collection** | **Required** Solr Collection name. |  | HIGH |
| **camel.kamelet.solr-source.servers** | **Required** Comma separated list of Solr Servers and ports. |  | HIGH |
| **camel.kamelet.solr-source.query** | **Required** The query to submit to Solr. |  | HIGH |
| **camel.kamelet.solr-source.username** | Username to connect to Solr. |  | MEDIUM |
| **camel.kamelet.solr-source.password** | Password to connect to Solr. |  | MEDIUM |

The camel-solr-source source connector has no converters out of the box.

The camel-solr-source source connector has no transforms out of the box.

The camel-solr-source source connector has no aggregation strategies out of the box.