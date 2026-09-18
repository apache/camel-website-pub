# camel-snowflake-source-kafka-connector source configuration

Connector Description: Query data from a Snowflake Database.

When using camel-snowflake-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-snowflake-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.snowflakesource.CamelSnowflakesourceSourceConnector
```

The camel-snowflake-source source connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.snowflake-source.instanceUrl** | **Required** The Instance url Example: instance.snowflakecomputing.com. |  | HIGH |
| **camel.kamelet.snowflake-source.username** | **Required** The username to access a secured Snowflake Database. |  | HIGH |
| **camel.kamelet.snowflake-source.password** | **Required** The password to access a secured Snowflake Database. |  | HIGH |
| **camel.kamelet.snowflake-source.query** | **Required** The query to execute against the Snowflake Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.snowflake-source.databaseName** | The name of the Snowflake Database. |  | MEDIUM |
| **camel.kamelet.snowflake-source.consumedQuery** | A query to run on a tuple consumed. Example: DELETE FROM accounts where user\_id = :#user\_id. |  | MEDIUM |
| **camel.kamelet.snowflake-source.delay** | The number of milliseconds before the next poll. | 500 | MEDIUM |

The camel-snowflake-source source connector has no converters out of the box.

The camel-snowflake-source source connector has no transforms out of the box.

The camel-snowflake-source source connector has no aggregation strategies out of the box.