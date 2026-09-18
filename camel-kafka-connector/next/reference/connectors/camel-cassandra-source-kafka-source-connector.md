# camel-cassandra-source-kafka-connector source configuration

Connector Description: Send a query to an Apache Cassandra cluster table.

When using camel-cassandra-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-cassandra-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.cassandrasource.CamelCassandrasourceSourceConnector
```

The camel-cassandra-source source connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.cassandra-source.connectionHost** | **Required** The hostname(s) for the Cassandra server(s). Use a comma to separate multiple hostnames. Example: localhost. |  | HIGH |
| **camel.kamelet.cassandra-source.connectionPort** | **Required** The port number(s) of the cassandra server(s). Use a comma to separate multiple port numbers. Example: 9042. |  | HIGH |
| **camel.kamelet.cassandra-source.keyspace** | **Required** The keyspace to use. Example: customers. |  | HIGH |
| **camel.kamelet.cassandra-source.username** | The username for accessing a secured Cassandra cluster. |  | MEDIUM |
| **camel.kamelet.cassandra-source.password** | The password for accessing a secured Cassandra cluster. |  | MEDIUM |
| **camel.kamelet.cassandra-source.resultStrategy** | The strategy to convert the result set of the query. | "ALL" | MEDIUM |
| **camel.kamelet.cassandra-source.consistencyLevel** | The consistency level to use. | "QUORUM" | MEDIUM |
| **camel.kamelet.cassandra-source.query** | **Required** The query to execute against the Cassandra cluster table. |  | HIGH |
| **camel.kamelet.cassandra-source.extraTypeCodecs** | To use a specific comma separated list of Extra Type codecs. |  | MEDIUM |

The camel-cassandra-source source connector has no converters out of the box.

The camel-cassandra-source source connector has no transforms out of the box.

The camel-cassandra-source source connector has no aggregation strategies out of the box.