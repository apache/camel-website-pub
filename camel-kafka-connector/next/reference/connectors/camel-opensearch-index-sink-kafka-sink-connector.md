# camel-opensearch-index-sink-kafka-connector sink configuration

Connector Description: Stores JSON-formatted data into Opensearch.

When using camel-opensearch-index-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-opensearch-index-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.opensearchindexsink.CamelOpensearchindexsinkSinkConnector
```

The camel-opensearch-index-sink sink connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.opensearch-index-sink.user** | The username to connect to OpenSearch. |  | MEDIUM |
| **camel.kamelet.opensearch-index-sink.password** | The password to connect to OpenSearch. |  | MEDIUM |
| **camel.kamelet.opensearch-index-sink.enableSSL** | Specifies to connect by using SSL. | false | MEDIUM |
| **camel.kamelet.opensearch-index-sink.hostAddresses** | **Required** A comma-separated list of remote transport addresses in `ip:port format`. Example: quickstart-es-http:9200. |  | HIGH |
| **camel.kamelet.opensearch-index-sink.clusterName** | **Required** The name of the OpenSearch cluster. Example: quickstart. |  | HIGH |
| **camel.kamelet.opensearch-index-sink.indexName** | The name of the OpenSearch index. Example: data. |  | MEDIUM |
| **camel.kamelet.opensearch-index-sink.certificate** | The Certificate for accessing the OpenSearch cluster. You must encode this value in base64. |  | MEDIUM |

The camel-opensearch-index-sink sink connector has no converters out of the box.

The camel-opensearch-index-sink sink connector has no transforms out of the box.

The camel-opensearch-index-sink sink connector has no aggregation strategies out of the box.