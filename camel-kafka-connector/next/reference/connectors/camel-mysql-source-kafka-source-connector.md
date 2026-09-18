# camel-mysql-source-kafka-connector source configuration

Connector Description: Query data from a MySQL Database.

When using camel-mysql-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mysql-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mysqlsource.CamelMysqlsourceSourceConnector
```

The camel-mysql-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mysql-source.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.mysql-source.serverPort** | The server port for the data source. | "3306" | MEDIUM |
| **camel.kamelet.mysql-source.username** | **Required** The username to access a secured MySQL Database. |  | HIGH |
| **camel.kamelet.mysql-source.password** | **Required** The password to access a secured MySQL Database. |  | HIGH |
| **camel.kamelet.mysql-source.query** | **Required** The query to execute against the MySQL Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.mysql-source.databaseName** | **Required** The name of the MySQL Database. |  | HIGH |
| **camel.kamelet.mysql-source.consumedQuery** | A query to run on a tuple consumed. Example: DELETE FROM accounts where user\_id = :#user\_id. |  | MEDIUM |
| **camel.kamelet.mysql-source.delay** | The number of milliseconds before the next poll. | 500 | MEDIUM |

The camel-mysql-source source connector has no converters out of the box.

The camel-mysql-source source connector has no transforms out of the box.

The camel-mysql-source source connector has no aggregation strategies out of the box.