# camel-oracle-database-sink-kafka-connector sink configuration

Connector Description: Send data to an Oracle Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

When using camel-oracle-database-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-oracle-database-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.oracledatabasesink.CamelOracledatabasesinkSinkConnector
```

The camel-oracle-database-sink sink connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.oracle-database-sink.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.oracle-database-sink.serverPort** | The server port for the data source. | "1521" | MEDIUM |
| **camel.kamelet.oracle-database-sink.username** | **Required** The username to access a secured Oracle Database. |  | HIGH |
| **camel.kamelet.oracle-database-sink.password** | **Required** The password to access a secured Oracle Database. |  | HIGH |
| **camel.kamelet.oracle-database-sink.query** | **Required** The query to execute against the Oracle Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.oracle-database-sink.databaseName** | **Required** The name of the Oracle Database. |  | HIGH |

The camel-oracle-database-sink sink connector has no converters out of the box.

The camel-oracle-database-sink sink connector has no transforms out of the box.

The camel-oracle-database-sink sink connector has no aggregation strategies out of the box.