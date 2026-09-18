# ![elasticsearch search source](_images/kamelets/elasticsearch-search-source.svg) ElasticSearch Search Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Search data on ElasticSearch

## Configuration Options

The following table summarizes the configuration options available for the `elasticsearch-search-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | ElasticSearch Cluster Name | **Required** The name of the cluster. | string |  |  |
| **hostAddresses** | Host Addresses | **Required** Comma separated list with ip:port formatted remote transport addresses to use. | string |  |  |
| **indexName** | Index in ElasticSearch | **Required** The name of the index to act against. | string |  |  |
| **query** | Query | **Required** The query we want to use to search on ElasticSearch. | string |  |  |
| **certificate** | Certificate | The Certificate for accessing the Elasticsearch cluster. You must encode this value in base64. | string |  |  |
| **enableSSL** | Enable SSL | Do we want to connect using SSL?. | boolean | true |  |
| **password** | Password | Password to connect to ElasticSearch. | string |  |  |
| **period** | Period | The time interval between two searches. | integer | 1000 |  |
| **user** | Username | Username to connect to ElasticSearch. | string |  |  |

## Dependencies

At runtime, the `elasticsearch-search-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kamelet
    
-   camel:timer
    
-   camel:elasticsearch
    
-   camel:gson
    

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
      uri: "kamelet:elasticsearch-search-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## ElasticSearch Search Source Kamelet Description

This Kamelet performs periodic searches on an ElasticSearch cluster using a specified query and returns the search results as JSON messages.

### Authentication methods

The Kamelet supports multiple authentication options:

-   **Basic Authentication**: Use `user` and `password` parameters
    
-   **SSL/TLS**: Enable secure connections with `enableSSL` (default: true)
    
-   **Certificate Authentication**: Provide a base64-encoded certificate via the `certificate` parameter
    

### Output format

The Kamelet outputs search results in JSON format using the Gson library. Each search operation returns the complete ElasticSearch response including hits, metadata, and aggregations.

### Configuration requirements

The Kamelet requires the following mandatory properties:

-   **query**: ElasticSearch query to execute
    
-   **clusterName**: Name of the ElasticSearch cluster
    
-   **indexName**: Index to search against
    
-   **hostAddresses**: Comma-separated list of host:port addresses
    

### Connection security

For production environments, consider:

-   Using SSL connections (`enableSSL: true`)
    
-   Providing proper authentication credentials
    
-   Using certificate-based authentication for enhanced security
    

### Usage examples

Basic ElasticSearch search with authentication:

```yaml
- route:
    from:
      uri: "kamelet:elasticsearch-search-source"
      parameters:
        query: '{"query": {"match_all": {}}}'
        clusterName: "my-cluster"
        indexName: "my-index"
        hostAddresses: "localhost:9200"
        user: "elastic"
        password: "changeme"
        period: 30000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Search with specific query and SSL:

```yaml
- route:
    from:
      uri: "kamelet:elasticsearch-search-source"
      parameters:
        query: '{"query": {"term": {"status": "active"}}, "size": 100}'
        clusterName: "production-cluster"
        indexName: "users"
        hostAddresses: "es-node1:9200,es-node2:9200"
        enableSSL: true
        user: "search-user"
        password: "secure-password"
        period: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Search with certificate authentication:

```yaml
- route:
    from:
      uri: "kamelet:elasticsearch-search-source"
      parameters:
        query: '{"query": {"range": {"timestamp": {"gte": "now-1h"}}}}'
        clusterName: "secure-cluster"
        indexName: "logs"
        hostAddresses: "es.example.com:9200"
        enableSSL: true
        certificate: "LS0tLS1CRUdJTi... (base64 encoded certificate)"
        period: 10000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/elasticsearch-search-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/elasticsearch-search-source.kamelet.yaml)