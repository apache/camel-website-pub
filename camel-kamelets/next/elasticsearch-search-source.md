# ![elasticsearch search source](_images/kamelets/elasticsearch-search-source.svg) ElasticSearch Search Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs the same search on an index of Elasticsearch at a regular interval, and sends the result of each search as one message.

Use it to watch an index on a schedule, for example to send the error log entries or the orders that match a query to another system. To store documents in Elasticsearch, use `elasticsearch-index-sink`; for OpenSearch, use `opensearch-search-source`.

Output: the body is JSON text with the total number of matches (`total`) and a `hits` list, with the index, the id and the score of each document found. The fields of each document are under `source`, but in an unusual nested form, in which each value is wrapped in a `_value` object under `_children`. The `Content-Type` header is `application/json`.

Good to know: every search returns all the matching documents again, not only the new ones; to get only new documents, filter on a date in the query. By default a search runs every second. A search on an index that does not exist fails, and is tried again at the next interval. It connects with TLS by default (`enableSSL`).

## Configuration Options

The following table summarizes the configuration options available for the `elasticsearch-search-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | ElasticSearch Cluster Name | **Required** The name of the Elasticsearch cluster. Required, but not checked against the cluster. | string |  | quickstart |
| **hostAddresses** | Host Addresses | **Required** The address of the Elasticsearch HTTP API, as `host:port`, or several nodes separated by commas. The port is 9200 by default. | string |  | quickstart-es-http:9200 |
| **indexName** | Index in ElasticSearch | **Required** The name of the index to search. | string |  | orders |
| **query** | Query | **Required** The search to run, as a JSON search request of Elasticsearch, the same as the body of a `_search` request. It can also set `size`, the number of documents returned, which is 10 when not set. | string |  | {"query": {"match": {"status": "shipped"}}} |
| **certificate** | Certificate | The certificate of the certificate authority (CA) that signed the certificate of the cluster, such as the `http_ca.crt` file of Elasticsearch, as PEM text encoded in base64. Needed when the cluster uses a self-signed certificate. | string |  |  |
| **enableSSL** | Enable SSL | If true, it connects with HTTPS. Set it to false for a cluster that is reached with plain HTTP. | boolean | true |  |
| **password** | Password | The password of the Elasticsearch user in `user`. | string |  |  |
| **period** | Period | How long to wait between two searches, in milliseconds. For example, 60000 is one minute. | integer | 1000 | 60000 |
| **user** | Username | The Elasticsearch user to log in as, such as `elastic`. Leave it out for a cluster without security. | string |  |  |

## Dependencies

At runtime, the `elasticsearch-search-source` Kamelet relies upon the presence of the following dependencies:

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
    
-   **Trusted certificate**: Provide the base64-encoded certificate of the certificate authority of the cluster via the `certificate` parameter, for a cluster with a self-signed certificate
    

### Output format

The Kamelet outputs the search results as JSON text: the total number of matches and the list of hits, with the index, id and score of each document. Every search returns all the matching documents again, not only the new ones.

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
    
-   Providing the certificate of the certificate authority of the cluster when it uses a self-signed certificate
    

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

Search on a cluster with a self-signed certificate:

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
        certificate: "LS0tLS1CRUdJTi... (base64 encoded CA certificate)"
        period: 10000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/elasticsearch-search-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/elasticsearch-search-source.kamelet.yaml)