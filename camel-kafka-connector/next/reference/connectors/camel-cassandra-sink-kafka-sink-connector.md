# camel-cassandra-sink-kafka-connector sink configuration

Connector Description: Send data to an Apache Cassandra cluster.

When using camel-cassandra-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-cassandra-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.cassandrasink.CamelCassandrasinkSinkConnector
```

The camel-cassandra-sink sink connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.cassandra-sink.connectionHost** | **Required** The hostname(s) for the Cassandra server(s). Use a comma to separate multiple hostnames. Example: localhost. |  | HIGH |
| **camel.kamelet.cassandra-sink.connectionPort** | **Required** The port number(s) of the cassandra server(s). Use a comma to separate multiple port numbers. Example: 9042. |  | HIGH |
| **camel.kamelet.cassandra-sink.keyspace** | **Required** The keyspace to use. Example: customers. |  | HIGH |
| **camel.kamelet.cassandra-sink.username** | The username for accessing a secured Cassandra cluster. |  | MEDIUM |
| **camel.kamelet.cassandra-sink.password** | The password for accessing a secured Cassandra cluster. |  | MEDIUM |
| **camel.kamelet.cassandra-sink.consistencyLevel** | The consistency level to use. | "ANY" | MEDIUM |
| **camel.kamelet.cassandra-sink.prepareStatements** | If true, specifies to use PreparedStatements as the query. If false, specifies to use regular Statements as the query. | true | MEDIUM |
| **camel.kamelet.cassandra-sink.query** | **Required** The query to execute against the Cassandra cluster table. |  | HIGH |
| **camel.kamelet.cassandra-sink.extraTypeCodecs** | To use a specific comma separated list of Extra Type codecs. |  | MEDIUM |
| **camel.kamelet.cassandra-sink.jsonPayload** | If we want to transform the payload in json or not. | true | MEDIUM |

The camel-cassandra-sink sink connector has no converters out of the box.

The camel-cassandra-sink sink connector has no transforms out of the box.

The camel-cassandra-sink sink connector has no aggregation strategies out of the box.