# ![opensearch index sink](_images/kamelets/opensearch-index-sink.svg) OpenSearch Index Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores JSON-formatted data into Opensearch.

## Configuration Options

The following table summarizes the configuration options available for the `opensearch-index-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | OpenSearch Cluster Name | **Required** The name of the OpenSearch cluster. | string |  | quickstart |
| **hostAddresses** | Host Addresses | **Required** A comma-separated list of remote transport addresses in `ip:port format`. | string |  | quickstart-es-http:9200 |
| **certificate** | Certificate | The Certificate for accessing the OpenSearch cluster. You must encode this value in base64. | string |  |  |
| **enableSSL** | Enable SSL | Specifies to connect by using SSL. | boolean | true |  |
| **indexName** | Index in OpenSearch | The name of the OpenSearch index. | string |  | data |
| **password** | Password | The password to connect to OpenSearch. | string |  |  |
| **user** | Username | The username to connect to OpenSearch. | string |  |  |

## Dependencies

At runtime, the `opensearch-index-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:jackson
    
-   camel:kamelet
    
-   camel:opensearch
    
-   camel:gson
    
-   camel:bean
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:opensearch-index-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## OpenSearch Index Sink Kamelet Description

### OpenSearch Integration

This Kamelet integrates with OpenSearch, an open-source search and analytics engine derived from Elasticsearch. OpenSearch provides powerful full-text search and analytics capabilities.

### Index Operations

Performs indexing operations to store documents in OpenSearch indices, enabling efficient search and analytics on the indexed data.

### Document Indexing

Processes incoming data and indexes it as documents in OpenSearch, making the data searchable and available for analytics queries.

### Distributed Search Engine

OpenSearch is designed as a distributed search engine that can:

-   Scale horizontally across multiple nodes
    
-   Provide real-time search capabilities
    
-   Support complex analytics and aggregations
    
-   Handle large volumes of data
    

### Open Source Alternative

OpenSearch serves as an open-source alternative to Elasticsearch, maintaining compatibility while providing community-driven development and governance.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-index-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-index-sink.kamelet.yaml)