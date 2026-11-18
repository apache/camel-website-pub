# ![opensearch index sink](_images/kamelets/opensearch-index-sink.svg) OpenSearch Index Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores each message, a JSON object, as a document in an index of OpenSearch, so that it can be searched.

Use it to make records searchable, such as orders, log entries or products, or to feed dashboards in OpenSearch Dashboards. For Elasticsearch, use `elasticsearch-index-sink`.

Input: the body is the document, as JSON text, such as `{"order": 42, "status": "shipped"}`. The optional `indexId` header (or `ce-indexid`) is the id of the document: a document with the same id is replaced. Without it, OpenSearch makes up a new id, so each message adds a new document. The optional `indexName` header (or `ce-indexname`) is the index to write to, instead of the `indexName` option.

Output: when it is used inside a route, the body afterwards is the id of the document, as text.

Good to know: a body that is not JSON fails the message, and so does a message with no index, from the option or the header. It connects with TLS by default (`enableSSL`); for a server with a self-signed certificate, give its certificate in `certificate`.

## Configuration Options

The following table summarizes the configuration options available for the `opensearch-index-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | OpenSearch Cluster Name | **Required** The name of the OpenSearch cluster. Required, but not checked against the cluster. | string |  | quickstart |
| **hostAddresses** | Host Addresses | **Required** The address of the OpenSearch HTTP API, as `host:port`, or several nodes separated by commas. The port is 9200 by default. | string |  | quickstart-es-http:9200 |
| **certificate** | Certificate | The certificate of the certificate authority (CA) that signed the certificate of the cluster, as PEM text encoded in base64. Needed when the cluster uses a self-signed certificate. | string |  |  |
| **enableSSL** | Enable SSL | If true, it connects with HTTPS. Set it to false for a cluster that is reached with plain HTTP. | boolean | true |  |
| **indexName** | Index in OpenSearch | The name of the index to store the documents in. OpenSearch creates it when it does not exist. The `indexName` header of a message takes precedence. | string |  | orders |
| **password** | Password | The password of the OpenSearch user in `user`. | string |  |  |
| **sslContextParameters** | SSL Context Parameters | For TLS settings that `certificate` cannot give, such as a client certificate (mutual TLS), a trust store, or a TLS version, an `SSLContextParameters` object defined in the application, as `#bean:` followed by its name. It takes precedence over `certificate`; set one or the other. | string |  | #bean:mySslContext |
| **user** | Username | The OpenSearch user to log in as, such as `admin`. Leave it out for a cluster without security. | string |  |  |

## Dependencies

At runtime, the `opensearch-index-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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