# camel-sqlserver-source-kafka-connector source configuration

Connector Description: Query data from a Microsoft SQL Server Database.

When using camel-sqlserver-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-sqlserver-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.sqlserversource.CamelSqlserversourceSourceConnector
```

The camel-sqlserver-source source connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.sqlserver-source.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.sqlserver-source.serverPort** | The server port for the data source. | "1433" | MEDIUM |
| **camel.kamelet.sqlserver-source.username** | **Required** The username to access a secured SQL Server Database. |  | HIGH |
| **camel.kamelet.sqlserver-source.password** | **Required** The password to access a secured SQL Server Database. |  | HIGH |
| **camel.kamelet.sqlserver-source.query** | **Required** The query to execute against the SQL Server Database Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.sqlserver-source.databaseName** | **Required** The name of the Database. |  | HIGH |
| **camel.kamelet.sqlserver-source.consumedQuery** | A query to run on a tuple consumed Example: DELETE FROM accounts where user\_id = :#user\_id. |  | MEDIUM |
| **camel.kamelet.sqlserver-source.encrypt** | Encrypt the connection to SQL Server. | false | MEDIUM |
| **camel.kamelet.sqlserver-source.trustServerCertificate** | Trust Server Certificate. | true | MEDIUM |
| **camel.kamelet.sqlserver-source.delay** | The number of milliseconds before the next poll. | 500 | MEDIUM |

The camel-sqlserver-source source connector has no converters out of the box.

The camel-sqlserver-source source connector has no transforms out of the box.

The camel-sqlserver-source source connector has no aggregation strategies out of the box.