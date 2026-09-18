# camel-google-bigquery-sink-kafka-connector sink configuration

Connector Description: Send data to a Google Big Query table.

When using camel-google-bigquery-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-bigquery-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlebigquerysink.CamelGooglebigquerysinkSinkConnector
```

The camel-google-bigquery-sink sink connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-bigquery-sink.projectId** | **Required** The Google Cloud Project ID. |  | HIGH |
| **camel.kamelet.google-bigquery-sink.dataset** | **Required** The Big Query Dataset ID. |  | HIGH |
| **camel.kamelet.google-bigquery-sink.table** | **Required** The Big Query Table ID. |  | HIGH |
| **camel.kamelet.google-bigquery-sink.serviceAccountKey** | **Required** The service account key to use as credentials for the BigQuery Service. You must encode this value in base64. |  | HIGH |

The camel-google-bigquery-sink sink connector has no converters out of the box.

The camel-google-bigquery-sink sink connector has no transforms out of the box.

The camel-google-bigquery-sink sink connector has no aggregation strategies out of the box.