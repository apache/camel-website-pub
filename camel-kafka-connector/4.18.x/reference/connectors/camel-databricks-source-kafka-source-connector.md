# camel-databricks-source-kafka-connector source configuration

Connector Description: Query data from a Databricks Database. For Unity Catalog workspaces, specify catalog and schema parameters.

When using camel-databricks-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-databricks-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.databrickssource.CamelDatabrickssourceSourceConnector
```

The camel-databricks-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.databricks-source.serverHostname** | **Required** The Databricks server hostname. Example: adb-1234567890123456.7.azuredatabricks.net. |  | HIGH |
| **camel.kamelet.databricks-source.serverPort** | The server port for the Databricks data source. | "443" | MEDIUM |
| **camel.kamelet.databricks-source.httpPath** | **Required** The HTTP path to the Databricks SQL Warehouse or cluster. Example: /sql/1.0/warehouses/abc123def456. |  | HIGH |
| **camel.kamelet.databricks-source.accessToken** | **Required** The personal access token to access Databricks. |  | HIGH |
| **camel.kamelet.databricks-source.query** | **Required** The query to execute against the Databricks Database. Example: SELECT \* FROM accounts. |  | HIGH |
| **camel.kamelet.databricks-source.extraOptions** | Additional JDBC connection options (e.g., ConnCatalog=main;ConnSchema=default). | "" | MEDIUM |
| **camel.kamelet.databricks-source.consumedQuery** | A query to run on a tuple consumed. Example: DELETE FROM accounts where user\_id = :#user\_id. |  | MEDIUM |
| **camel.kamelet.databricks-source.delay** | The number of milliseconds before the next poll from the Databricks database. | 500 | MEDIUM |

The camel-databricks-source source connector has no converters out of the box.

The camel-databricks-source source connector has no transforms out of the box.

The camel-databricks-source source connector has no aggregation strategies out of the box.