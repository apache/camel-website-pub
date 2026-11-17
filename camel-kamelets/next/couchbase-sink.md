# ![couchbase sink](_images/kamelets/couchbase-sink.svg) Couchbase Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores each message as a document in a Couchbase bucket, under a document ID that the Kamelet counts up or that a header gives.

Use it to save events, orders or other records as JSON documents in Couchbase, for example each message that arrives on a Kafka topic. To read documents, use `couchbase-source`.

Input: the body is the document. JSON text is stored as a JSON document; other text is stored as a JSON string. With `autoStartId` true, the default, the documents get the IDs `1`, `2`, `3` and so on, counted from `startingId`, and the `CamelCouchbaseId` header is ignored. With `autoStartId` false, the `CamelCouchbaseId` header is the ID, and it is required.

Output: the body afterwards is `true`.

Good to know: a document that already has the ID is replaced. The count starts again at `startingId` each time the integration starts, so with `autoStartId` true a restart overwrites the documents stored before. Set `autoStartId` to false and give each message its own ID to avoid that. The connection is not encrypted, also with `protocol` set to `https`.

## Configuration Options

The following table summarizes the configuration options available for the `couchbase-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucket** | Bucket | **Required** The name of the bucket to store the documents in, in its default collection. | string |  | orders |
| **couchbaseHostname** | Hostname | **Required** The host name or IP address of a node of the Couchbase cluster. The Kamelet connects to its data service, on port 11210. | string |  | couchbase.example.com |
| **protocol** | Protocol | **Required** The protocol part of the address of the server, `http` or `https`. It is required, but it does not choose how the Kamelet connects, and `https` does not turn on TLS. | string |  | http |
| **autoStartId** | Automatic IDs | If true, the documents get the IDs `startingId`, `startingId` + 1, and so on, and the `CamelCouchbaseId` header is ignored. If false, each message must carry its document ID in the `CamelCouchbaseId` header. | boolean | true |  |
| **connectionString** | Connection String | The address of the cluster for the Couchbase SDK, which starts with `couchbase://`. When it is set, it is used instead of `couchbaseHostname` to connect, for example to reach the data service on another port than 11210. | string |  | couchbase://couchbase.example.com:11210 |
| **couchbasePort** | Port | The port of the web console and REST interface of Couchbase, 8091 by default. The Kamelet does not connect to this port; to reach the data service on a port other than 11210, set `connectionString`. | integer | 8091 |  |
| **password** | Password | The password of the Couchbase user `username`. | string |  |  |
| **startingId** | Starting ID | The first document ID to use when `autoStartId` is true. Each message gets the next number. | integer | 1 |  |
| **username** | Username | The Couchbase user to log in as. It needs the rights to write documents in `bucket`. | string |  |  |

## Dependencies

At runtime, the `couchbase-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:couchbase-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Couchbase Sink Kamelet Description

### Authentication

This Kamelet uses username and password authentication to connect to Couchbase.

### Configuration

This Kamelet requires configuration of: - Protocol (`http` or `https`; it does not turn on TLS) - Hostname of the Couchbase server - Bucket name to store documents - Username and password credentials

Optional settings include: - Port (defaults to 8091) - Starting ID for document inserts (defaults to 1) - Auto start ID flag (defaults to true)

### Document Storage

Documents are stored in the specified Couchbase bucket. The Kamelet can automatically generate document IDs starting from a configurable starting point. The count starts again at the starting ID each time the integration starts, and a document that already has an ID is replaced, so a restart overwrites the documents stored before. To choose the IDs yourself, set `autoStartId` to false and give each message its ID in the `CamelCouchbaseId` header.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-sink.kamelet.yaml)