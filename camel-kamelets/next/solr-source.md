# ![solr source](_images/kamelets/solr-source.svg) Solr Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs the same query on a collection or core of Apache Solr at a regular interval, and sends the result of each query as one message.

Use it to watch a Solr collection on a schedule, for example to send the documents that match a query to another system. To add documents to Solr, use `solr-sink`.

Output: the body is JSON text, the answer of Solr: `responseHeader`, and under `response` the list of the documents found, each with its fields. The `Content-Type` header is `application/json`.

Good to know: every query returns all the matching documents again, not only the new ones; filter on a date in the query to get only new documents. Each query returns only the first documents found, 10 with the usual Solr settings. It connects with plain HTTP.

## Configuration Options

The following table summarizes the configuration options available for the `solr-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | Collection | **Required** The name of the Solr collection, or of the core on a Solr server that does not run in SolrCloud mode, to query. | string |  | products |
| **period** | Period between Polls | **Required** How long to wait between two queries, in milliseconds. For example, 60000 is one minute. | integer | 10000 | 60000 |
| **query** | Query | **Required** The query to run, in the Solr query syntax, as given in the `q` parameter of a Solr search, such as `**:**` for every document or `status_s:new`. | string |  | status\_s:new |
| **servers** | Servers | **Required** The address of the Solr server, as `host:port`, without `http://` and without the `/solr` path. The port of Solr is 8983 by default. | string |  | solr.example.com:8983 |
| **password** | Password | The password of the Solr user in `username`. | string |  |  |
| **username** | Username | The Solr user to log in as, with Basic authentication. Leave it out for a Solr without login. | string |  |  |

## Dependencies

At runtime, the `solr-source` Kamelet relies upon the presence of the following dependencies:

-   camel:solr
    
-   camel:timer
    
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
      uri: "kamelet:solr-source"
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

## Solr Source Kamelet Description

### Authentication methods

This Kamelet connects to Solr over plain HTTP. For a Solr with Basic authentication, set the `username` and `password` properties; leave them out for a Solr without login.

### Output format

The Kamelet runs the configured query at every `period`, and produces one message per query: the answer of Solr as JSON text, with the documents found under `response`. Every query returns all the matching documents again, not only the new ones.

### Configuration

The Kamelet requires the following properties:

-   `servers`: the Solr server, as `host:port`
    
-   `collection`: the collection, or the core, to query
    
-   `query`: the query, in the Solr query syntax, such as `status_s:new`
    
-   `period`: the time between two queries, in milliseconds
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:solr-source"
      parameters:
        servers: "solr.example.com:8983"
        collection: "products"
        query: "status_s:new"
        period: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/solr-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/solr-source.kamelet.yaml)