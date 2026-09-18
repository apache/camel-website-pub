# camel-sqlserver-sink-kafka-connector sink configuration

Connector Description: Send data to a Microsoft SQL Server Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

When using camel-sqlserver-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-sqlserver-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.sqlserversink.CamelSqlserversinkSinkConnector
```

The camel-sqlserver-sink sink connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.sqlserver-sink.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.sqlserver-sink.serverPort** | The server port for the data source. | "1433" | MEDIUM |
| **camel.kamelet.sqlserver-sink.username** | **Required** The username to access a secured SQL Server Database. |  | HIGH |
| **camel.kamelet.sqlserver-sink.password** | **Required** The password to access a secured SQL Server Database. |  | HIGH |
| **camel.kamelet.sqlserver-sink.query** | **Required** The query to execute against the SQL Server Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.sqlserver-sink.databaseName** | **Required** The name of the SQL Server Database. |  | HIGH |
| **camel.kamelet.sqlserver-sink.encrypt** | Encrypt the connection to SQL Server. | false | MEDIUM |
| **camel.kamelet.sqlserver-sink.trustServerCertificate** | Trust Server Certificate. | true | MEDIUM |

The camel-sqlserver-sink sink connector has no converters out of the box.

The camel-sqlserver-sink sink connector has no transforms out of the box.

The camel-sqlserver-sink sink connector has no aggregation strategies out of the box.