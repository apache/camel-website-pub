# ![opensearch search source](_images/kamelets/opensearch-search-source.svg) OpenSearch Search Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs the same search on an index of OpenSearch at a regular interval, and sends the result of each search as one message.

Use it to watch an index on a schedule, for example to send the error log entries or the orders that match a query to another system. To store documents in OpenSearch, use `opensearch-index-sink`; for Elasticsearch, use `elasticsearch-search-source`.

Output: the body is JSON text with the total number of matches (`total`) and a `hits` list, with the index, the id and the score of each document found. The fields of each document are under `source`, but in an unusual nested form, in which each value is wrapped in a `_value` object under `_children`. The `Content-Type` header is `application/json`.

Good to know: every search returns all the matching documents again, not only the new ones; to get only new documents, filter on a date in the query. By default a search runs every second. A search on an index that does not exist fails, and is tried again at the next interval. It connects with TLS by default (`enableSSL`).

## Configuration Options

The following table summarizes the configuration options available for the `opensearch-search-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | OpenSearch Cluster Name | **Required** The name of the OpenSearch cluster. Required, but not checked against the cluster. | string |  | quickstart |
| **hostAddresses** | Host Addresses | **Required** The address of the OpenSearch HTTP API, as `host:port`, or several nodes separated by commas. The port is 9200 by default. | string |  | quickstart-es-http:9200 |
| **indexName** | Index in OpenSearch | **Required** The name of the index to search. | string |  | orders |
| **query** | Query | **Required** The search to run, as a JSON search request of OpenSearch, the same as the body of a `_search` request. It can also set `size`, the number of documents returned, which is 10 when not set. | string |  | {"query": {"match": {"status": "shipped"}}} |
| **certificate** | Certificate | The certificate of the certificate authority (CA) that signed the certificate of the cluster, as PEM text encoded in base64. Needed when the cluster uses a self-signed certificate. | string |  |  |
| **enableSSL** | Enable SSL | If true, it connects with HTTPS. Set it to false for a cluster that is reached with plain HTTP. | boolean | true |  |
| **password** | Password | The password of the OpenSearch user in `user`. | string |  |  |
| **period** | Period | How long to wait between two searches, in milliseconds. For example, 60000 is one minute. | integer | 1000 | 60000 |
| **sslContextParameters** | SSL Context Parameters | For TLS settings that `certificate` cannot give, such as a client certificate (mutual TLS), a trust store, or a TLS version, an `SSLContextParameters` object defined in the application, as `#bean:` followed by its name. It takes precedence over `certificate`; set one or the other. | string |  | #bean:mySslContext |
| **user** | Username | The OpenSearch user to log in as, such as `admin`. Leave it out for a cluster without security. | string |  |  |

## Dependencies

At runtime, the `opensearch-search-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:timer
    
-   camel:opensearch
    
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
      uri: "kamelet:opensearch-search-source"
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

## Opensearch Search Source Kamelet Description

### Authentication methods

This Kamelet connects to OpenSearch with:

-   Basic authentication, with the `user` and `password` properties, or no login for a cluster without security
    
-   TLS, on by default (`enableSSL`), with the base64-encoded certificate of the certificate authority of the cluster in `certificate`, or an `SSLContextParameters` bean in `sslContextParameters` for other TLS settings
    

### Output format

The Kamelet runs the configured search at every `period`, and produces one message per search, with the result as JSON text: the total number of matches and the list of hits. Every search returns all the matching documents again, not only the new ones.

### Configuration

The Kamelet requires the following properties:

-   `hostAddresses`: the OpenSearch HTTP API, as `host:port`
    
-   `clusterName`: the name of the cluster
    
-   `indexName`: the index to search
    
-   `query`: the search, as a JSON search request
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:opensearch-search-source"
      parameters:
        hostAddresses: "opensearch.example.com:9200"
        clusterName: "my-cluster"
        indexName: "orders"
        query: '{"query": {"match": {"status": "shipped"}}}'
        user: "admin"
        password: "my-password"
        period: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-search-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-search-source.kamelet.yaml)