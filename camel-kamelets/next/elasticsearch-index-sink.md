# ![elasticsearch index sink](_images/kamelets/elasticsearch-index-sink.svg) ElasticSearch Index Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores each message, a JSON object, as a document in an index of Elasticsearch, so that it can be searched.

Use it to make records searchable, such as orders, log entries or products, or to feed dashboards in Kibana. For OpenSearch, use `opensearch-index-sink`.

Input: the body is the document, as JSON text, such as `{"order": 42, "status": "shipped"}`. The optional `indexId` header (or `ce-indexid`) is the id of the document: a document with the same id is replaced. Without it, Elasticsearch makes up a new id, so each message adds a new document. The optional `indexName` header (or `ce-indexname`) is the index to write to, instead of the `indexName` option.

Output: when it is used inside a route, the body afterwards is the id of the document, as text. The `Content-Type` header is set to `application/json`.

Good to know: a body that is not JSON fails the message, and so does a message with no index, from the option or the header. It connects with TLS by default (`enableSSL`). For a cluster whose certificate is self-signed, or signed by a private certificate authority (CA), give the certificate of that CA in `certificate`; without it, the message fails with `PKIX path building failed`. When Elasticsearch does not answer, the message fails after 30 seconds; `connectionTimeout` and `socketTimeout` change that. Headers that start with `CamelElasticsearch` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `elasticsearch-index-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | ElasticSearch Cluster Name | **Required** The name of the Elasticsearch cluster. Required, but not checked against the cluster. | string |  | quickstart |
| **hostAddresses** | Host Addresses | **Required** The address of the Elasticsearch HTTP API, as `host:port`, or several nodes separated by commas. The port is 9200 by default. | string |  | quickstart-es-http:9200 |
| **apiKey** | API Key | An API key to log in with, instead of `user` and `password`. It is the `encoded` value that Elasticsearch gives when the key is created, or its `id` and `api_key` joined with a colon (`id:api_key`). It is sent in the `Authorization` header, only to the nodes of the cluster. Set either `apiKey` or `user`, not both. | string |  | bXktaWQ6bXkta2V5 |
| **certificate** | Certificate | The certificate of the certificate authority (CA) that signed the certificate of the cluster, such as the `http_ca.crt` file that Elasticsearch generates, as a PEM or DER file encoded in base64 on one line, such as the output of `base64 -w0 http_ca.crt` (`base64 -i http_ca.crt` on macOS). Needed when the cluster uses a self-signed certificate, or one signed by a private CA. When it is set, only this CA is trusted; when it is not set, the certificates that Java trusts are used. | string |  |  |
| **connectionTimeout** | Connection Timeout | How long to wait for the connection to Elasticsearch, in milliseconds. When it is not set, it is 30000, which is 30 seconds. | integer |  | 5000 |
| **enableSSL** | Enable SSL | If true, it connects with HTTPS. Set it to false for a cluster that is reached with plain HTTP. | boolean | true |  |
| **indexName** | Index in ElasticSearch | The name of the index to store the documents in. Elasticsearch creates it when it does not exist. The `indexName` header of a message takes precedence. | string |  | orders |
| **password** | Password | The password of the Elasticsearch user in `user`. | string |  |  |
| **socketTimeout** | Socket Timeout | How long to wait for data from Elasticsearch, in milliseconds. When Elasticsearch sends nothing for this long, during the TLS handshake or while it stores the document, the message fails with a `SocketTimeoutException`. When it is not set, it is 30000, which is 30 seconds. | integer |  | 10000 |
| **sslContextParameters** | SSL Context Parameters | For TLS settings that `certificate` cannot give, such as a client certificate (mutual TLS), a trust store, or a TLS version, an `SSLContextParameters` object defined in the application, as `#bean:` followed by its name. It takes precedence over `certificate`; set one or the other. | string |  | #bean:mySslContext |
| **user** | Username | The Elasticsearch user to log in as, such as `elastic`. Leave it out for a cluster without security. | string |  |  |

## Dependencies

At runtime, the `elasticsearch-index-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:elasticsearch
    
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

### Trusting a Private Certificate Authority

The Kamelet connects with HTTPS by default (`enableSSL`). The certificate of the cluster is checked against the certificate authorities (CA) that Java trusts, so a cluster whose certificate is self-signed, or signed by a private CA, fails with `PKIX path building failed`.

Give the certificate of that CA in `certificate`, as a PEM or DER file encoded in base64 on one line. Elasticsearch generates such a CA when it starts with security on, in `config/certs/http_ca.crt`. Encode it with `base64 -w0 http_ca.crt` (`base64 -i http_ca.crt` on macOS). Only this CA is trusted then.

### Timeouts

When Elasticsearch does not answer, the message fails after 30 seconds. `connectionTimeout` is how long to wait for the connection, and `socketTimeout` how long to wait for data from Elasticsearch, both in milliseconds.

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
            uri: "kamelet:elasticsearch-index-sink"
            parameters:
              hostAddresses: "es.example.com:9200"
              clusterName: "quickstart"
              indexName: "orders"
              user: "elastic"
              password: "{{search.password}}"
              certificate: "{{search.ca}}"
              connectionTimeout: 5000
              socketTimeout: 10000
```

Here `search.ca` is an application property that holds the certificate of the CA, encoded in base64.

### Index Configuration

You can specify: - Cluster name (required) - Host addresses in `ip:port` format (required) - Index name for storing documents

### Optional Headers

The Kamelet supports the following optional headers: - `indexId` / `ce-indexid`: To specify the document ID for indexing - `indexName` / `ce-indexname`: To override the configured index name

Both headers are optional and will use configured defaults if not provided.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/elasticsearch-index-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/elasticsearch-index-sink.kamelet.yaml)