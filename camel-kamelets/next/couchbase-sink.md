# ![couchbase sink](_images/kamelets/couchbase-sink.svg) Couchbase Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores each message as a document in a Couchbase bucket, or deletes a document, under a document ID that the Kamelet counts up or that a header gives.

Use it to save events, orders or other records as JSON documents in Couchbase, for example each message that arrives on a Kafka topic, or to delete the documents that messages name. To read documents, use `couchbase-source`.

Input: the body is the document. JSON text is stored as a JSON document; other text is stored as a JSON string. With `autoStartId` true, the default, the documents get the IDs `1`, `2`, `3` and so on, counted from `startingId`, and the `CamelCouchbaseId` header is ignored. With `autoStartId` false, the `CamelCouchbaseId` header is the ID; a message without it uses `key`, and fails when `key` is not set either. With `operation` `CCB_DEL`, the body is not used.

Output: the body afterwards is `true`. After a delete, it is the result of Couchbase as text, such as `MutationResult{cas=0x18e92f09b4bf0000, …​}`.

Good to know: a document that already has the ID is replaced. The count starts again at `startingId` each time the integration starts, so with `autoStartId` true a restart overwrites the documents stored before. Set `autoStartId` to false and give each message its own ID to avoid that. The documents go to the default collection of the bucket unless `collection` is set, in `scope`; a collection that does not exist makes each message wait and fail with `AmbiguousTimeoutException` (10 seconds by default, see `retryAttempts`). The connection is not encrypted, also with `protocol` set to `https`. Headers that start with `CamelCouchbase`, except `CamelCouchbaseId`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `couchbase-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bucket** | Bucket | **Required** The name of the bucket to store the documents in. They go to its default collection, unless `collection` is set. | string |  | orders |
| **couchbaseHostname** | Hostname | **Required** The host name or IP address of a node of the Couchbase cluster. The Kamelet connects to its data service, on port 11210. | string |  | couchbase.example.com |
| **protocol** | Protocol | **Required** The protocol part of the address of the server, `http` or `https`. It is required, but it does not choose how the Kamelet connects, and `https` does not turn on TLS. | string |  | http |
| **autoStartId** | Automatic IDs | If true, the documents get the IDs `startingId`, `startingId` + 1, and so on, and the `CamelCouchbaseId` header and `key` are ignored. If false, each message must carry its document ID in the `CamelCouchbaseId` header, or `key` must be set. | boolean | true |  |
| **collection** | Collection | The collection to store the documents in, or delete them from, in `scope`. The collection must exist; if it does not, each message waits and then fails with `AmbiguousTimeoutException`. When it is not set, the default collection of the bucket is used, and `scope` is ignored. | string |  | orders |
| **connectTimeout** | Connect Timeout | How long one attempt to connect to a node of the cluster may take, in milliseconds, before the Kamelet tries again. A message that waits for the connection still fails after the time that `retryAttempts`, `retryPause` and `operationTimeout` give. When it is not set, 30000 (30 seconds) is used. | integer |  | 10000 |
| **connectionString** | Connection String | The address of the cluster for the Couchbase SDK, which starts with `couchbase://`. When it is set, it is used instead of `couchbaseHostname` to connect, for example to reach the data service on another port than 11210. | string |  | couchbase://couchbase.example.com:11210 |
| **couchbasePort** | Port | The port of the web console and REST interface of Couchbase, 8091 by default. The Kamelet does not connect to this port; to reach the data service on a port other than 11210, set `connectionString`. | integer | 8091 |  |
| **key** | Document ID | The document ID to use for a message without the `CamelCouchbaseId` header, when `autoStartId` is false. Every such message then writes, or deletes, the same document. When it is not set, a message without the header fails with `No document id`. | string |  | latest-status |
| **operation** | Operation | What to do with each message: `CCB_PUT` stores the body as the document, replacing a document with the same ID, and `CCB_DEL` deletes the document with the ID. Deleting a document that does not exist fails the message with `Document with the given id not found`. To delete, also set `autoStartId` to false, or the Kamelet deletes the documents `startingId`, `startingId` + 1, and so on. When it is not set, `CCB_PUT` is used. Enum values: \* CCB\_PUT \* CCB\_DEL | string |  | CCB\_DEL |
| **operationTimeout** | Operation Timeout | How long a write or delete may take, in milliseconds, when it is longer than `retryAttempts` × `retryPause`. When it is not set, 2500 is used, so the time from `retryAttempts` and `retryPause`, 10 seconds by default, applies. | integer |  | 30000 |
| **password** | Password | The password of the Couchbase user `username`. | string |  |  |
| **persistTo** | Persist To | On how many nodes a stored document must be saved to disk before the message is done: 0 (not waited for), 1 (the active node), or 2, 3 or 4 (the active node and replicas). A number higher than the bucket can give, such as 2 for a bucket without replicas, fails every message with `Not enough replicas configured on the bucket`, but only after the document has been stored. Not used with `operation` `CCB_DEL`. When it is not set, 0 is used. Enum values: \* 0 \* 1 \* 2 \* 3 \* 4 | integer |  |  |
| **replicateTo** | Replicate To | To how many replicas a stored document must be copied before the message is done, from 0 to 3. The bucket must be set up with that many replicas, on as many other nodes. Otherwise every message fails, such as with `Not enough replicas configured on the bucket`, but only after the document has been stored. Not used with `operation` `CCB_DEL`. When it is not set, 0 is used. Enum values: \* 0 \* 1 \* 2 \* 3 | integer |  |  |
| **retryAttempts** | Retry Attempts | Together with `retryPause`, how long a write or delete may take: it fails after `retryAttempts` × `retryPause` milliseconds, or after `operationTimeout` if that is longer. Within that time, a write or delete that fails for a reason that can pass, such as a collection that is not known yet or a bucket that is still opening, is tried again every `retryPause` milliseconds. When it is not set, 2 is used, which with the default `retryPause` gives 10 seconds. | integer |  | 3 |
| **retryPause** | Retry Pause | How long to wait before trying a write or delete again, in milliseconds. It also sets how long a write or delete may take; see `retryAttempts`. When it is not set, 5000 (5 seconds) is used. | integer |  | 1000 |
| **scope** | Scope | The scope of the bucket that holds `collection`. It is only used together with `collection`. When it is not set, the `_default` scope is used. | string |  | sales |
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

Optional settings include: - Port (defaults to 8091) - Starting ID for document inserts (defaults to 1) - Auto start ID flag (defaults to true) - Scope and collection to store the documents in - A fixed document ID (`key`) for messages without the `CamelCouchbaseId` header - The operation, `CCB_PUT` to store or `CCB_DEL` to delete - Durability (`persistTo`, `replicateTo`) and timeouts (`connectTimeout`, `retryAttempts`, `retryPause`, `operationTimeout`)

### Document Storage

Documents are stored in the specified Couchbase bucket. The Kamelet can automatically generate document IDs starting from a configurable starting point. The count starts again at the starting ID each time the integration starts, and a document that already has an ID is replaced, so a restart overwrites the documents stored before. To choose the IDs yourself, set `autoStartId` to false and give each message its ID in the `CamelCouchbaseId` header. A message without the header then uses `key`, and fails with `No document id` when `key` is not set either.

### Example with a Scope and a Collection

Without `collection`, the documents go to the default collection of the bucket, and `scope` is not used. Set both to store them in a collection of your own. The collection must exist: if it does not, each message waits and fails with `AmbiguousTimeoutException`. Here each order is stored in the `orders` collection of the `sales` scope, under the order number the message carries in its `CamelCouchbaseId` header:

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "orders"
        bootstrapServers: "kafka.example.com:9092"
        saslAuthType: "NONE"
      steps:
        - setHeader:
            name: CamelCouchbaseId
            jq: ".orderId"
        - to:
            uri: "kamelet:couchbase-sink"
            parameters:
              protocol: "http"
              couchbaseHostname: "couchbase.example.com"
              bucket: "shop"
              scope: "sales"
              collection: "orders"
              autoStartId: false
              username: "{{couchbase.username}}"
              password: "{{couchbase.password}}"
```

### Example Deleting Documents

With `operation` set to `CCB_DEL`, each message deletes the document whose ID it carries in the `CamelCouchbaseId` header, and the body is not used. Also set `autoStartId` to false, or the Kamelet deletes the documents `1`, `2`, `3` and so on. Deleting a document that does not exist fails the message with `Document with the given id not found`.

```yaml
- to:
    uri: "kamelet:couchbase-sink"
    parameters:
      protocol: "http"
      couchbaseHostname: "couchbase.example.com"
      bucket: "shop"
      scope: "sales"
      collection: "orders"
      autoStartId: false
      operation: "CCB_DEL"
      username: "{{couchbase.username}}"
      password: "{{couchbase.password}}"
```

### Durability and Timeouts

`persistTo` and `replicateTo` make each write wait until the document is saved to disk, or copied to replicas, on that many nodes. The bucket must have the replicas: if it does not, the document is still stored, but the message fails with `Not enough replicas configured on the bucket`. They do not apply to `CCB_DEL`.

A write or delete fails after `retryAttempts` × `retryPause` milliseconds, 2 × 5000 = 10 seconds by default, or after `operationTimeout` when that is longer. For example, `retryAttempts: 1`, `retryPause: 1000` and `operationTimeout: 4000` make a write that cannot be done fail after 4 seconds, trying again every second. `connectTimeout` is how long one attempt to connect to a node may take, 30 seconds by default.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/couchbase-sink.kamelet.yaml)