# camel-elasticsearch-index-sink-kafka-connector sink configuration

Connector Description: Stores JSON-formatted data into ElasticSearch.

When using camel-elasticsearch-index-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-elasticsearch-index-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.elasticsearchindexsink.CamelElasticsearchindexsinkSinkConnector
```

The camel-elasticsearch-index-sink sink connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.elasticsearch-index-sink.user** | The username to connect to ElasticSearch. |  | MEDIUM |
| **camel.kamelet.elasticsearch-index-sink.password** | The password to connect to ElasticSearch. |  | MEDIUM |
| **camel.kamelet.elasticsearch-index-sink.enableSSL** | Specifies to connect by using SSL. | true | MEDIUM |
| **camel.kamelet.elasticsearch-index-sink.hostAddresses** | **Required** A comma-separated list of remote transport addresses in `ip:port format`. Example: quickstart-es-http:9200. |  | HIGH |
| **camel.kamelet.elasticsearch-index-sink.clusterName** | **Required** The name of the ElasticSearch cluster. Example: quickstart. |  | HIGH |
| **camel.kamelet.elasticsearch-index-sink.indexName** | The name of the ElasticSearch index. Example: data. |  | MEDIUM |
| **camel.kamelet.elasticsearch-index-sink.certificate** | The Certificate for accessing the Elasticsearch cluster. You must encode this value in base64. |  | MEDIUM |

The camel-elasticsearch-index-sink sink connector has no converters out of the box.

The camel-elasticsearch-index-sink sink connector has no transforms out of the box.

The camel-elasticsearch-index-sink sink connector has no aggregation strategies out of the box.