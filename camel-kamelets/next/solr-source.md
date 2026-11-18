# ![solr source](_images/kamelets/solr-source.svg) Solr Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs the same query on a collection or core of Apache Solr at a regular interval, and sends the result of each query as one message.

Use it to watch a Solr collection on a schedule, for example to send the documents that match a query to another system. To add documents to Solr, use `solr-sink`.

Output: the body is JSON text, the answer of Solr: `responseHeader`, and under `response` the list of the documents found, each with its fields. The `Content-Type` header is `application/json`.

Good to know: every query returns all the matching documents again, not only the new ones; filter on a date in the query to get only new documents. Each query returns only the first documents found: as many as `size`, or 10 with the usual Solr settings when `size` is not set. It connects with plain HTTP by default; set `enableSSL` to true for a Solr that is reached with HTTPS, and give the certificate in `certificate` when Solr uses a self-signed certificate.

## Configuration Options

The following table summarizes the configuration options available for the `solr-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | Collection | **Required** The name of the Solr collection, or of the core on a Solr server that does not run in SolrCloud mode, to query. | string |  | products |
| **period** | Period between Polls | **Required** How long to wait between two queries, in milliseconds. For example, 60000 is one minute. | integer | 10000 | 60000 |
| **query** | Query | **Required** The query to run, in the Solr query syntax, as given in the `q` parameter of a Solr search, such as `**:**` for every document or `status_s:new`. | string |  | status\_s:new |
| **servers** | Servers | **Required** The address of the Solr server, as `host:port`, without `http://` and without the `/solr` path. The port of Solr is 8983 by default. | string |  | solr.example.com:8983 |
| **certificate** | Certificate | The certificate of Solr, or of the certificate authority (CA) that signed it, as a PEM or DER file encoded in base64 on one line, such as the output of `base64 -w0 solr.crt` (`base64 -i solr.crt` on macOS). Needed when Solr uses a self-signed certificate, or one that Java does not trust. When it is not set, the certificates that Java trusts are used. Only used when `enableSSL` is true. | string |  |  |
| **enableSSL** | Enable SSL | If true, it connects with HTTPS. Leave it false for a Solr that is reached with plain HTTP. | boolean | false |  |
| **password** | Password | The password of the Solr user in `username`. | string |  |  |
| **size** | Maximum Documents | The most documents each query returns, as the `rows` parameter of a Solr search. When it is not set, Solr decides, which is 10 with the usual Solr settings. | integer |  | 100 |
| **username** | Username | The Solr user to log in as, with Basic authentication. Leave it out for a Solr without login. | string |  |  |

## Dependencies

At runtime, the `solr-source` Kamelet relies upon the presence of the following dependencies:

-   camel:solr
    
-   camel:timer
    
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

### Connection and authentication

This Kamelet connects to Solr over plain HTTP by default. For a Solr that is reached with HTTPS, set `enableSSL` to true. When Solr uses a self-signed certificate, or one that Java does not trust, give the certificate of Solr, or of the certificate authority that signed it, in `certificate`, encoded in base64 on one line, for example with `base64 -w0 solr.crt`.

For a Solr with Basic authentication, set the `username` and `password` properties; leave them out for a Solr without login.

### Output format

The Kamelet runs the configured query at every `period`, and produces one message per query: the answer of Solr as JSON text, with the documents found under `response`. Every query returns all the matching documents again, not only the new ones, but at most `size` of them, or 10 with the usual Solr settings when `size` is not set.

### Configuration

The Kamelet requires the following properties:

-   `servers`: the Solr server, as `host:port`
    
-   `collection`: the collection, or the core, to query
    
-   `query`: the query, in the Solr query syntax, such as `status_s:new`
    
-   `period`: the time between two queries, in milliseconds
    

Optional properties include `size` (the most documents each query returns), `enableSSL` and `certificate` (HTTPS), and `username` and `password` (Basic authentication).

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