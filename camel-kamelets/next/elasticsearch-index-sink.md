# ![elasticsearch index sink](_images/kamelets/elasticsearch-index-sink.svg) ElasticSearch Index Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores each message, a JSON object, as a document in an index of Elasticsearch, so that it can be searched.

Use it to make records searchable, such as orders, log entries or products, or to feed dashboards in Kibana. For OpenSearch, use `opensearch-index-sink`.

Input: the body is the document, as JSON text, such as `{"order": 42, "status": "shipped"}`. The optional `indexId` header (or `ce-indexid`) is the id of the document: a document with the same id is replaced. Without it, Elasticsearch makes up a new id, so each message adds a new document. The optional `indexName` header (or `ce-indexname`) is the index to write to, instead of the `indexName` option.

Output: when it is used inside a route, the body afterwards is the id of the document, as text.

Good to know: a body that is not JSON fails the message, and so does a message with no index, from the option or the header. It connects with TLS by default (`enableSSL`); for a server with a self-signed certificate, give its certificate in `certificate`.

## Configuration Options

The following table summarizes the configuration options available for the `elasticsearch-index-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | ElasticSearch Cluster Name | **Required** The name of the Elasticsearch cluster. Required, but not checked against the cluster. | string |  | quickstart |
| **hostAddresses** | Host Addresses | **Required** The address of the Elasticsearch HTTP API, as `host:port`, or several nodes separated by commas. The port is 9200 by default. | string |  | quickstart-es-http:9200 |
| **certificate** | Certificate | The certificate of the certificate authority (CA) that signed the certificate of the cluster, such as the `http_ca.crt` file of Elasticsearch, as PEM text encoded in base64. Needed when the cluster uses a self-signed certificate. | string |  |  |
| **enableSSL** | Enable SSL | If true, it connects with HTTPS. Set it to false for a cluster that is reached with plain HTTP. | boolean | true |  |
| **indexName** | Index in ElasticSearch | The name of the index to store the documents in. Elasticsearch creates it when it does not exist. The `indexName` header of a message takes precedence. | string |  | orders |
| **password** | Password | The password of the Elasticsearch user in `user`. | string |  |  |
| **user** | Username | The Elasticsearch user to log in as, such as `elastic`. Leave it out for a cluster without security. | string |  |  |

## Dependencies

At runtime, the `elasticsearch-index-sink` Kamelet relies upon the presence of the following dependencies:

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