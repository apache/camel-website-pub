# camel-databricks-sink-kafka-connector sink configuration

Connector Description: Send data to a Databricks Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters. For Unity Catalog workspaces, specify catalog and schema parameters.

When using camel-databricks-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-databricks-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.databrickssink.CamelDatabrickssinkSinkConnector
```

The camel-databricks-sink sink connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.databricks-sink.serverHostname** | **Required** The Databricks server hostname. Example: adb-1234567890123456.7.azuredatabricks.net. |  | HIGH |
| **camel.kamelet.databricks-sink.serverPort** | The server port for the Databricks data source. | "443" | MEDIUM |
| **camel.kamelet.databricks-sink.httpPath** | **Required** The HTTP path to the Databricks SQL Warehouse or cluster. Example: /sql/1.0/warehouses/abc123def456. |  | HIGH |
| **camel.kamelet.databricks-sink.accessToken** | **Required** The personal access token to access Databricks. |  | HIGH |
| **camel.kamelet.databricks-sink.query** | **Required** The query to execute against the Databricks Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.databricks-sink.extraOptions** | Additional JDBC connection options (e.g., ConnCatalog=main;ConnSchema=default). | "" | MEDIUM |

The camel-databricks-sink sink connector has no converters out of the box.

The camel-databricks-sink sink connector has no transforms out of the box.

The camel-databricks-sink sink connector has no aggregation strategies out of the box.