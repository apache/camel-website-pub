# ![opensearch index sink](_images/kamelets/opensearch-index-sink.svg) OpenSearch Index Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores each message, a JSON object, as a document in an index of OpenSearch, so that it can be searched.

Use it to make records searchable, such as orders, log entries or products, or to feed dashboards in OpenSearch Dashboards. For Elasticsearch, use `elasticsearch-index-sink`.

Input: the body is the document, as JSON text, such as `{"order": 42, "status": "shipped"}`. The optional `indexId` header (or `ce-indexid`) is the id of the document: a document with the same id is replaced. Without it, OpenSearch makes up a new id, so each message adds a new document. The optional `indexName` header (or `ce-indexname`) is the index to write to, instead of the `indexName` option.

Output: when it is used inside a route, the body afterwards is the id of the document, as text. The `Content-Type` header is set to `application/json`.

Good to know: a body that is not JSON fails the message, and so does a message with no index, from the option or the header. It connects with TLS by default (`enableSSL`). For a cluster whose certificate is self-signed, or signed by a private certificate authority (CA), give the certificate of that CA in `certificate`; without it, the message fails with `PKIX path building failed`. When OpenSearch does not answer, the message fails after 30 seconds; `connectionTimeout` and `socketTimeout` change that. Headers that start with `CamelOpensearch` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `opensearch-index-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | OpenSearch Cluster Name | **Required** The name of the OpenSearch cluster. Required, but not checked against the cluster. | string |  | quickstart |
| **hostAddresses** | Host Addresses | **Required** The address of the OpenSearch HTTP API, as `host:port`, or several nodes separated by commas. The port is 9200 by default. | string |  | quickstart-es-http:9200 |
| **certificate** | Certificate | The certificate of the certificate authority (CA) that signed the certificate of the cluster, such as the `root-ca.pem` file of the OpenSearch demo configuration, as a PEM or DER file encoded in base64 on one line, such as the output of `base64 -w0 root-ca.pem` (`base64 -i root-ca.pem` on macOS). Needed when the cluster uses a self-signed certificate, or one signed by a private CA. When it is set, only this CA is trusted; when it is not set, the certificates that Java trusts are used. | string |  |  |
| **connectionTimeout** | Connection Timeout | How long to wait for the connection to OpenSearch, in milliseconds. When it is not set, it is 30000, which is 30 seconds. | integer |  | 5000 |
| **enableSSL** | Enable SSL | If true, it connects with HTTPS. Set it to false for a cluster that is reached with plain HTTP. | boolean | true |  |
| **indexName** | Index in OpenSearch | The name of the index to store the documents in. OpenSearch creates it when it does not exist. The `indexName` header of a message takes precedence. | string |  | orders |
| **password** | Password | The password of the OpenSearch user in `user`. | string |  |  |
| **socketTimeout** | Socket Timeout | How long to wait for data from OpenSearch, in milliseconds. When OpenSearch sends nothing for this long, for example while it stores a document, the message fails. When it is not set, it is 30000, which is 30 seconds. | integer |  | 10000 |
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

### Trusting a Private Certificate Authority

The Kamelet connects with HTTPS by default (`enableSSL`). The certificate of the cluster is checked against the certificate authorities (CA) that Java trusts, so a cluster whose certificate is self-signed, or signed by a private CA, fails with `PKIX path building failed`.

Give the certificate of that CA in `certificate`, as a PEM or DER file encoded in base64 on one line. The demo configuration of OpenSearch uses such a CA, in `config/root-ca.pem`. Encode it with `base64 -w0 root-ca.pem` (`base64 -i root-ca.pem` on macOS). Only this CA is trusted then.

### Timeouts

When OpenSearch does not answer, the message fails after 30 seconds. `connectionTimeout` is how long to wait for the connection, and `socketTimeout` how long to wait for data from OpenSearch, both in milliseconds.

### Example

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: '{"order": 42, "status": "shipped"}'
        contentType: application/json
      steps:
        - to:
            uri: "kamelet:opensearch-index-sink"
            parameters:
              hostAddresses: "opensearch.example.com:9200"
              clusterName: "opensearch-cluster"
              indexName: "orders"
              user: "admin"
              password: "{{search.password}}"
              certificate: "{{search.ca}}"
              connectionTimeout: 5000
              socketTimeout: 10000
```

Here `search.ca` is an application property that holds the certificate of the CA, encoded in base64.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-index-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-index-sink.kamelet.yaml)