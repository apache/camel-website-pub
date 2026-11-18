# ![solr sink](_images/kamelets/solr-sink.svg) Solr Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Adds each message, a JSON object or a JSON array of objects, as one or more documents to a collection or core of Apache Solr, so that they can be searched.

Use it to make records searchable in Solr, such as products, articles or orders. To run a query on a schedule, use `solr-source`.

Input: the body is JSON text: an object for one document, such as `{"id": "order-42", "status_s": "shipped"}`, or an array of objects for several. A document with the same `id` as one already stored replaces it.

Output: when it is used inside a route, the body afterwards is the answer of Solr, as a Map-like object with its `responseHeader`.

Good to know: a body that is not JSON fails the message. With `autocommit` false, the default, the documents become searchable only when Solr commits them, as set in the configuration of the collection. It connects with plain HTTP by default; set `enableSSL` to true for a Solr that is reached with HTTPS, and give the certificate in `certificate` when Solr uses a self-signed certificate.

## Configuration Options

The following table summarizes the configuration options available for the `solr-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | Collection | **Required** The name of the Solr collection, or of the core on a Solr server that does not run in SolrCloud mode, to add the documents to. | string |  | products |
| **servers** | Servers | **Required** The address of the Solr server, as `host:port`, without `http://` and without the `/solr` path. The port of Solr is 8983 by default. | string |  | solr.example.com:8983 |
| **autocommit** | Autocommit | If true, Solr commits after each message, so the documents can be searched at once. Commits are costly, so leave it false for many messages and let Solr commit on its own schedule. | boolean | false |  |
| **certificate** | Certificate | The certificate of Solr, or of the certificate authority (CA) that signed it, as a PEM or DER file encoded in base64 on one line, such as the output of `base64 -w0 solr.crt` (`base64 -i solr.crt` on macOS). Needed when Solr uses a self-signed certificate, or one that Java does not trust. When it is not set, the certificates that Java trusts are used. Only used when `enableSSL` is true. | string |  |  |
| **enableSSL** | Enable SSL | If true, it connects with HTTPS. Leave it false for a Solr that is reached with plain HTTP. | boolean | false |  |
| **password** | Password | The password of the Solr user in `username`. | string |  |  |
| **username** | Username | The Solr user to log in as, with Basic authentication. Leave it out for a Solr without login. | string |  |  |

## Dependencies

At runtime, the `solr-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:solr
    
-   camel:jackson3
    
-   camel:kamelet
    

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
            uri: "kamelet:solr-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Solr Sink Kamelet Description

### Apache Solr Integration

This Kamelet integrates with Apache Solr, a popular open-source search platform built on Apache Lucene. Solr provides powerful full-text search, faceted search, and analytics capabilities.

### Document Indexing

Indexes documents in Solr cores or collections, making data searchable and available for complex queries and analytics operations.

### Schema Management

Solr supports both schemaless and managed schema approaches, providing flexibility in defining field types, analyzers, and search configurations.

### Real-Time Search

Provides real-time or near real-time search capabilities, enabling immediate searchability of indexed documents for dynamic applications.

### Distributed Search

Supports distributed search through SolrCloud, enabling:

-   Horizontal scaling across multiple nodes
    
-   Automatic sharding and replication
    
-   High availability and fault tolerance
    
-   Load distribution for query processing
    

### Advanced Features

Solr provides advanced search features including:

-   Faceted search and filtering
    
-   Highlighting and suggestions
    
-   Spatial and geographical search
    
-   Complex query syntax and boosting
    
-   Analytics and aggregations
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/solr-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/solr-sink.kamelet.yaml)