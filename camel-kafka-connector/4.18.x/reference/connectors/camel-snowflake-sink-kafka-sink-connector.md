# camel-snowflake-sink-kafka-connector sink configuration

Connector Description: Send data to a Snowflake Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

When using camel-snowflake-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-snowflake-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.snowflakesink.CamelSnowflakesinkSinkConnector
```

The camel-snowflake-sink sink connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.snowflake-sink.instanceUrl** | **Required** The Instance url Example: instance.snowflakecomputing.com. |  | HIGH |
| **camel.kamelet.snowflake-sink.username** | **Required** The username to access a secured Snowflake Database. |  | HIGH |
| **camel.kamelet.snowflake-sink.password** | **Required** The password to access a secured Snowflake Database. |  | HIGH |
| **camel.kamelet.snowflake-sink.query** | **Required** The query to execute against the Snowflake Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.snowflake-sink.databaseName** | The name of the Snowflake Database. |  | MEDIUM |

The camel-snowflake-sink sink connector has no converters out of the box.

The camel-snowflake-sink sink connector has no transforms out of the box.

The camel-snowflake-sink sink connector has no aggregation strategies out of the box.