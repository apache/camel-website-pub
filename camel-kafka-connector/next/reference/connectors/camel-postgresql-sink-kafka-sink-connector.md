# camel-postgresql-sink-kafka-connector sink configuration

Connector Description: Send data to a PostgreSQL Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

When using camel-postgresql-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-postgresql-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.postgresqlsink.CamelPostgresqlsinkSinkConnector
```

The camel-postgresql-sink sink connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.postgresql-sink.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.postgresql-sink.serverPort** | The server port for the data source. | "5432" | MEDIUM |
| **camel.kamelet.postgresql-sink.username** | **Required** The username to access a secured PostgreSQL Database. |  | HIGH |
| **camel.kamelet.postgresql-sink.password** | **Required** The password to access a secured PostgreSQL Database. |  | HIGH |
| **camel.kamelet.postgresql-sink.query** | **Required** The query to execute against the PostgreSQL Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.postgresql-sink.databaseName** | **Required** The name of the PostgreSQL Database. |  | HIGH |

The camel-postgresql-sink sink connector has no converters out of the box.

The camel-postgresql-sink sink connector has no transforms out of the box.

The camel-postgresql-sink sink connector has no aggregation strategies out of the box.