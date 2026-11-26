# ![opensearch search action](_images/kamelets/opensearch-search-action.svg) OpenSearch Search Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Searches an index of OpenSearch for each message, and gives back the documents found, as a JSON array.

Use it to look something up in the middle of a flow, for example to find the customer of an order, or to enrich an event with the records that match it. To store documents in OpenSearch, use `opensearch-index-sink`; for Elasticsearch, use `elasticsearch-search-action`.

Input: the body is the search. Text that starts with `{` is a search in the Query DSL of OpenSearch, as JSON text: either a query alone, such as `{"match": {"city": "Oslo"}}`, or the body of a `_search` request with a `query`, such as `{"query": {"match_all": {}}, "sort": [{"age": "desc"}]}`. Any other text is searched for as words in all the fields of the documents: `Oslo Rome` finds the documents that contain Oslo or Rome. An empty body finds nothing. Bytes are read as text, and a Map (parsed JSON) is used as the Query DSL. With `queryDsl` set to false, every body is searched for as words, also one that starts with `{`. A vector search is a Query DSL search too: `{"query": {"knn": {"embedding": {"vector": [0.1, 0.2, 0.3], "k": 3}}}, "_source": ["name"]}` finds the documents whose vector in the `knn_vector` field `embedding` is closest, best first, and gives only their `name`; the index needs the setting `index.knn`, and `k` is counted for each part (segment) of the index, so more than `k` documents can match.

Output: the body is a JSON array, as text, with the documents found (their `_source`, with the id of the document added as `_id`), best match first unless the search has a `sort`, such as `[{"name": "Alice Smith", "city": "Oslo", "_id": "1"}]`; an empty array `[]` when nothing matches. The `CamelOpensearchTotalHits` header is the number of documents that match, which can be more than the documents in the body. The `Content-Type` header is `application/json`.

Good to know: the body holds at most `size` documents; a `size` in the search is ignored. OpenSearch stops counting the matches at 10000, so a larger number is given as 10000. A search with `"_source": false` gives an empty array. A search that is not valid JSON, an index that does not exist, or a query that OpenSearch rejects, fails the message. Headers that start with `CamelOpensearch` are removed from the message first, so they cannot change the index, the operation or the size. Whoever writes the body can read every document of the index, and the Query DSL can also look up values in other indices, such as a `terms` query that reads its terms from a document of another index: log in as a user, or with an API key, that can read only the index to search. When the body comes from untrusted input or from an AI agent, such as through `ai-tool-source`, set `queryDsl` to false, so that the body can only be words to search for. It connects with TLS by default (`enableSSL`); for a self-signed certificate, give the certificate of its certificate authority (CA) in `certificate`, and for a client certificate (mutual TLS), a trust store or a TLS version, an `SSLContextParameters` object in `sslContextParameters`.

## Configuration Options

The following table summarizes the configuration options available for the `opensearch-search-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **clusterName** | OpenSearch Cluster Name | **Required** The name of the OpenSearch cluster. Required, but not checked against the cluster. | string |  | quickstart |
| **hostAddresses** | Host Addresses | **Required** The address of the OpenSearch HTTP API, as `host:port`, or several nodes separated by commas. The port is 9200 by default. | string |  | opensearch-cluster-master:9200 |
| **indexName** | Index in OpenSearch | **Required** The name of the index to search. | string |  | customers |
| **apiKey** | API Key | An API key to log in with, instead of `user` and `password`. It is the token, which starts with `os_`, that OpenSearch gives when the API token is created (OpenSearch 3.7 or later). It is sent in the `Authorization` header, only to the nodes of the cluster. Set either `apiKey` or `user`, not both. | string |  | os\_my-token |
| **certificate** | Certificate | The certificate of the certificate authority (CA) that signed the certificate of the cluster, such as the `root-ca.pem` file of the OpenSearch demo configuration, as a PEM or DER file encoded in base64 on one line, such as the output of `base64 -w0 root-ca.pem` (`base64 -i root-ca.pem` on macOS). Needed when the cluster uses a self-signed certificate, or one signed by a private CA. When it is set, only this CA is trusted; when it is not set, the certificates that Java trusts are used. | string |  |  |
| **connectionTimeout** | Connection Timeout | How long to wait for the connection to OpenSearch, in milliseconds. When it is not set, it is 30000, which is 30 seconds. | integer |  | 5000 |
| **enableSSL** | Enable SSL | If true, it connects with HTTPS. Set it to false for a cluster that is reached with plain HTTP. | boolean | true |  |
| **password** | Password | The password of the OpenSearch user in `user`. | string |  |  |
| **queryDsl** | Query DSL | Whether a body that starts with `\{`, or a Map, is a search in the Query DSL. When it is false, every body is searched for as words in all the fields, so that whoever writes the body cannot run other queries; set it to false when the body comes from untrusted input or from an AI agent. | boolean | true |  |
| **size** | Size | The largest number of documents to give back in the body, for each message. It takes precedence over a `size` in the search. | integer | 10 |  |
| **socketTimeout** | Socket Timeout | How long to wait for data from OpenSearch, in milliseconds. When OpenSearch sends nothing for this long, the message fails. When it is not set, it is 30000, which is 30 seconds. | integer |  | 10000 |
| **sslContextParameters** | SSL Context Parameters | For TLS settings that `certificate` cannot give, such as a client certificate (mutual TLS), a trust store, or a TLS version, an `SSLContextParameters` object defined in the application, as `#bean:` followed by its name. It takes precedence over `certificate`; set one or the other. | string |  | #bean:mySslContext |
| **user** | Username | The OpenSearch user to log in as, such as `admin`. Leave it out for a cluster without security. | string |  |  |

## Dependencies

At runtime, the `opensearch-search-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:opensearch
    

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
            uri: "kamelet:opensearch-search-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-search-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/opensearch-search-action.kamelet.yaml)