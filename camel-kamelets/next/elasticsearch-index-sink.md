# ![elasticsearch index sink](_images/kamelets/elasticsearch-index-sink.svg) ElasticSearch Index Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores JSON-formatted data into ElasticSearch.

## Configuration Options

The following table summarizes the configuration options available for the `elasticsearch-index-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | ElasticSearch Cluster Name | **Required** The name of the ElasticSearch cluster. | string |  | quickstart |
| **hostAddresses** | Host Addresses | **Required** A comma-separated list of remote transport addresses in `ip:port format`. | string |  | quickstart-es-http:9200 |
| **certificate** | Certificate | The Certificate for accessing the Elasticsearch cluster. You must encode this value in base64. | string |  |  |
| **enableSSL** | Enable SSL | Specifies to connect by using SSL. | boolean | true |  |
| **indexName** | Index in ElasticSearch | The name of the ElasticSearch index. | string |  | data |
| **password** | Password | The password to connect to ElasticSearch. | string |  |  |
| **user** | Username | The username to connect to ElasticSearch. | string |  |  |

## Dependencies

At runtime, the `elasticsearch-index-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:jackson
    
-   camel:kamelet
    
-   camel:elasticsearch
    
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
            uri: "kamelet:elasticsearch-index-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## ElasticSearch Index Sink Kamelet Description

### Input Format

This Kamelet expects JSON-formatted data as input and outputs plain text responses.

### Authentication

This Kamelet supports username and password authentication for connecting to ElasticSearch clusters.

### SSL Configuration

SSL connection is enabled by default. You can provide a base64-encoded certificate for secure connections to your ElasticSearch cluster.

### Index Configuration

You can specify: - Cluster name (required) - Host addresses in `ip:port` format (required) - Index name for storing documents

### Optional Headers

The Kamelet supports the following optional headers: - `indexId` / `ce-indexid`: To specify the document ID for indexing - `indexName` / `ce-indexname`: To override the configured index name

Both headers are optional and will use configured defaults if not provided.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/elasticsearch-index-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/elasticsearch-index-sink.kamelet.yaml)