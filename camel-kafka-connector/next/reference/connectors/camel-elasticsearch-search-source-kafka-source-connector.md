# camel-elasticsearch-search-source-kafka-connector source configuration

Connector Description: Search data on ElasticSearch

When using camel-elasticsearch-search-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-elasticsearch-search-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.elasticsearchsearchsource.CamelElasticsearchsearchsourceSourceConnector
```

The camel-elasticsearch-search-source source connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.elasticsearch-search-source.period** | The time interval between two searches. | 1000 | MEDIUM |
| **camel.kamelet.elasticsearch-search-source.query** | **Required** The query we want to use to search on ElasticSearch. |  | HIGH |
| **camel.kamelet.elasticsearch-search-source.user** | Username to connect to ElasticSearch. |  | MEDIUM |
| **camel.kamelet.elasticsearch-search-source.password** | Password to connect to ElasticSearch. |  | MEDIUM |
| **camel.kamelet.elasticsearch-search-source.enableSSL** | Do we want to connect using SSL?. | true | MEDIUM |
| **camel.kamelet.elasticsearch-search-source.hostAddresses** | **Required** Comma separated list with ip:port formatted remote transport addresses to use. |  | HIGH |
| **camel.kamelet.elasticsearch-search-source.indexName** | **Required** The name of the index to act against. |  | HIGH |
| **camel.kamelet.elasticsearch-search-source.clusterName** | **Required** The name of the cluster. |  | HIGH |
| **camel.kamelet.elasticsearch-search-source.certificate** | The Certificate for accessing the Elasticsearch cluster. You must encode this value in base64. |  | MEDIUM |

The camel-elasticsearch-search-source source connector has no converters out of the box.

The camel-elasticsearch-search-source source connector has no transforms out of the box.

The camel-elasticsearch-search-source source connector has no aggregation strategies out of the box.