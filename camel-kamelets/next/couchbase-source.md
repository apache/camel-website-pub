# ![couchbase source](_images/kamelets/couchbase-source.svg) Couchbase Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Runs a SQL++ (N1QL) query on a Couchbase bucket again and again, and sends each document or row it finds as a message, as JSON text.

Use it to pass the documents of a Couchbase bucket on to another system, for example to copy them to a search index or a data warehouse. To store documents, use `couchbase-sink`.

Output: the body is one result row as JSON text. Without `statement`, the query reads all the documents of the default collection, and a row is `{"<bucket>":<the document>,"_id":"<document ID>"}_`_. With `collection` set, it reads that collection of `scope`, and a row is `{"<collection>":<the document>,"`_`id":"<document ID>"}`. The `CamelCouchbaseId` header holds the ID of the document.

Good to know: the query runs again every `delay` milliseconds and, unless `processedStrategy` is `delete`, nothing marks a document as read, so the same documents are sent on every run. With `delete`, each document is deleted once its message has been processed. A `statement` must name the document ID `_id_` _(`SELECT META().id AS`_ `id, …​`), or its rows are skipped. With `fullDocument` set to true, the body is an object of the Couchbase SDK instead of JSON text. The connection is not encrypted, also with `protocol` set to `https`.

## Configuration Options

The following table summarizes the configuration options available for the `couchbase-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucket** | Bucket | **Required** The name of the bucket to read the documents from. They are read from its default collection, unless `collection` is set. | string |  | orders |
| **couchbaseHostname** | Hostname | **Required** The host name or IP address of a node of the Couchbase cluster. The Kamelet connects to its data service, on port 11210. | string |  | couchbase.example.com |
| **protocol** | Protocol | **Required** The protocol part of the address of the server, `http` or `https`. It is required, but it does not choose how the Kamelet connects, and `https` does not turn on TLS. | string |  | http |
| **collection** | Collection | The collection to read from, in `scope`. Without `statement`, the query reads all its documents. With `fullDocument` true or `processedStrategy` `delete`, the documents are read or deleted in this collection, also when a `statement` reads another one. When it is not set, the default collection of the bucket is used. | string |  | orders |
| **connectionString** | Connection String | The address of the cluster for the Couchbase SDK, which starts with `couchbase://`. When it is set, it is used instead of `couchbaseHostname` to connect, for example to reach the data service on another port than 11210. | string |  | couchbase://couchbase.example.com:11210 |
| **couchbasePort** | Port | The port of the web console and REST interface of Couchbase, 8091 by default. The Kamelet does not connect to this port; to reach the data service on a port other than 11210, set `connectionString`. | integer | 8091 |  |
| **delay** | Delay | How long to wait after one poll before the next, in milliseconds. | integer | 500 |  |
| **descending** | Descending | If true, the results come in descending order. | boolean | false |  |
| **designDocumentName** | Design Document Name | The design document that holds the view to read. Only used when `useView` is true. The default, `beer`, is the one of the beer-sample bucket. | string | beer |  |
| **fullDocument** | Full Document | If true, the Kamelet reads each document found by its ID and sends it as an object of the Couchbase SDK, not as JSON text. If false, it sends the row of the query as JSON text. | boolean | false |  |
| **limit** | Limit | The most documents to send on each poll. A negative value means no limit. | integer | \-1 |  |
| **password** | Password | The password of the Couchbase user `username`. | string |  |  |
| **processedStrategy** | Processed Strategy | What to do with a document once its message has been processed: `none` leaves it, so the next poll sends it again, and `delete` deletes it from `collection`. A message that fails keeps its document, so a later poll sends it again. When it is not set, `none` is used. Enum values: \* none \* delete | string |  | delete |
| **scope** | Scope | The scope of the bucket to read from. A `statement` runs in this scope, so a collection named in it is one of this scope. When it is not set, the `_default` scope is used. | string |  | sales |
| **skip** | Skip | How many documents to skip on each poll before sending the others. A negative value skips none. | integer | \-1 |  |
| **statement** | SQL++ Statement | The SQL++ (N1QL) query to run on each poll, instead of reading all documents. It runs in `scope`, the `_default` scope of the bucket when `scope` is not set, so name a collection of that scope, such as `_default` or `orders`, not the bucket. It must return the document ID as `__id`, or its rows are skipped. Not used when `useView` is true. | string |  | SELECT META().id AS \_\_id, \* FROM \_default |
| **useView** | Use View | If true, the Kamelet reads a MapReduce view, chosen with `designDocumentName` and `viewName`, instead of running a SQL++ query. | boolean | false |  |
| **username** | Username | The Couchbase user to log in as. It needs the rights to read the documents of `bucket` and to run queries on it. | string |  |  |
| **viewName** | View Name | The view to read. Only used when `useView` is true. The default, `brewery_beers`, is a view of the beer-sample bucket. | string | brewery\_beers |  |

## Dependencies

At runtime, the `couchbase-source` Kamelet relies upon the presence of the following dependencies:

-   camel:couchbase
    
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
      uri: "kamelet:couchbase-source"
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

## Couchbase Source Kamelet Description

### Query Modes

The bucket is polled in one of two modes.

By default the N1QL statement in the `statement` property is run against the bucket on each poll. Set `useView` to true to poll a MapReduce view instead, selected with `designDocumentName` and `viewName`.

### Writing the Statement

The statement runs in the scope set by `scope`, or in the `_default` scope when it is not set, so the keyspace is a collection of that scope rather than the bucket name - use `_default` for the default collection.

It must also alias the document id as `__id`, because the consumer skips any row without that field. A query that omits it produces a source that polls without emitting anything:

SELECT META().id AS \_\_id, \* FROM \_default

### Example with a Scope and a Collection

Without `statement`, set `scope` and `collection` to read all the documents of that collection. Each row is `{"<collection>":<the document>,"__id":"<document ID>"}`. With `processedStrategy` set to `delete`, each document is deleted from the collection once its message has been processed, so it is sent only once. A message that fails keeps its document, and the next poll sends it again.

```yaml
- route:
    from:
      uri: "kamelet:couchbase-source"
      parameters:
        protocol: "http"
        couchbaseHostname: "couchbase.example.com"
        bucket: "shop"
        scope: "sales"
        collection: "inbox"
        processedStrategy: "delete"
        delay: 5000
        username: "{{couchbase.username}}"
        password: "{{couchbase.password}}"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

A `statement` runs in `scope` too, so it names the collection alone. With `fullDocument` true, or `processedStrategy` `delete`, also set `collection` to the collection the statement reads: the documents are read, or deleted, in `collection`, the default collection when it is not set.

```yaml
scope: "sales"
collection: "orders"
statement: "SELECT META().id AS __id, o.* FROM orders o WHERE o.status = 'new'"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-source.kamelet.yaml)