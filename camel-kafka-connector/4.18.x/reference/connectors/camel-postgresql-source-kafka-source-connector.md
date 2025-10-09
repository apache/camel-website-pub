# camel-postgresql-source-kafka-connector source configuration

Connector Description: Query data from a PostgreSQL Database.

When using camel-postgresql-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-postgresql-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.postgresqlsource.CamelPostgresqlsourceSourceConnector
```

The camel-postgresql-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.postgresql-source.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.postgresql-source.serverPort** | The server port for the data source. | "5432" | MEDIUM |
| **camel.kamelet.postgresql-source.username** | **Required** The username to access a secured PostgreSQL Database. |  | HIGH |
| **camel.kamelet.postgresql-source.password** | **Required** The password to access a secured PostgreSQL Database. |  | HIGH |
| **camel.kamelet.postgresql-source.query** | **Required** The query to execute against the PostgreSQL Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.postgresql-source.databaseName** | **Required** The name of the PostgreSQL Database. |  | HIGH |
| **camel.kamelet.postgresql-source.consumedQuery** | A query to run on a tuple consumed. Example: DELETE FROM accounts where user\_id = :#user\_id. |  | MEDIUM |
| **camel.kamelet.postgresql-source.delay** | The number of milliseconds before the next poll. | 500 | MEDIUM |

The camel-postgresql-source source connector has no converters out of the box.

The camel-postgresql-source source connector has no transforms out of the box.

The camel-postgresql-source source connector has no aggregation strategies out of the box.