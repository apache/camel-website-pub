# ![solr sink](_images/kamelets/solr-sink.svg) Solr Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send documents to Solr Collection.

## Configuration Options

The following table summarizes the configuration options available for the `solr-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | Collection | **Required** Solr Collection name. | string |  |  |
| **servers** | Servers | **Required** Comma separated list of Solr Servers and ports. | string |  |  |
| **autocommit** | Autocommit | If autocommit should be enabled or not. | boolean | false |  |
| **password** | Password | Password to connect to Solr. | string |  |  |
| **username** | Username | Username to connect to Solr. | string |  |  |

## Dependencies

At runtime, the `solr-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:solr
    
-   camel:core
    
-   camel:jackson
    
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