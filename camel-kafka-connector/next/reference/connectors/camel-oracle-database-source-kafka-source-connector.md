# camel-oracle-database-source-kafka-connector source configuration

Connector Description: Query data from an Oracle Database.

When using camel-oracle-database-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-oracle-database-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.oracledatabasesource.CamelOracledatabasesourceSourceConnector
```

The camel-oracle-database-source source connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.oracle-database-source.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.oracle-database-source.serverPort** | The server port for the data source. | "1521" | MEDIUM |
| **camel.kamelet.oracle-database-source.username** | **Required** The username to access a secured Oracle Database. |  | HIGH |
| **camel.kamelet.oracle-database-source.password** | **Required** The password to access a secured Oracle Database. |  | HIGH |
| **camel.kamelet.oracle-database-source.query** | **Required** The query to execute against the Oracle Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.oracle-database-source.databaseName** | **Required** The name of the Oracle Database. |  | HIGH |
| **camel.kamelet.oracle-database-source.consumedQuery** | A query to run on a tuple consumed. Example: DELETE FROM accounts where user\_id = :#user\_id. |  | MEDIUM |

The camel-oracle-database-source source connector has no converters out of the box.

The camel-oracle-database-source source connector has no transforms out of the box.

The camel-oracle-database-source source connector has no aggregation strategies out of the box.