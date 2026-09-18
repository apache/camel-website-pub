# camel-mariadb-source-kafka-connector source configuration

Connector Description: Query data from a MariaDB Database.

When using camel-mariadb-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mariadb-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mariadbsource.CamelMariadbsourceSourceConnector
```

The camel-mariadb-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mariadb-source.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.mariadb-source.serverPort** | The server port for the data source. | "3306" | MEDIUM |
| **camel.kamelet.mariadb-source.username** | **Required** The username to access a secured MariaDB Database. |  | HIGH |
| **camel.kamelet.mariadb-source.password** | **Required** The password to access a secured MariaDB Database. |  | HIGH |
| **camel.kamelet.mariadb-source.query** | **Required** The query to execute against the MariaDB Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.mariadb-source.databaseName** | **Required** The name of the MariaDB Database. |  | HIGH |
| **camel.kamelet.mariadb-source.consumedQuery** | A query to run on a tuple consumed. Example: DELETE FROM accounts where user\_id = :#user\_id. |  | MEDIUM |
| **camel.kamelet.mariadb-source.delay** | The number of milliseconds before the next poll. | 500 | MEDIUM |

The camel-mariadb-source source connector has no converters out of the box.

The camel-mariadb-source source connector has no transforms out of the box.

The camel-mariadb-source source connector has no aggregation strategies out of the box.