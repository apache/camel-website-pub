# ![mongodb changes stream source](_images/kamelets/mongodb-changes-stream-source.svg) MongoDB Changes Stream Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends a message for each change to a collection of a MongoDB database, such as a document inserted, updated or deleted, as it happens.

Use it to react to changes in MongoDB, for example to copy new orders to another system or to keep a cache or a search index up to date. To read the documents of a capped collection from the start, use `mongodb-source`. To write documents, use `mongodb-sink`.

Output: the body is JSON text. For an insert or a replace, it is the whole new document; for an update, the text `null`; for a delete, an object with only the `_id` of the deleted document. The `CamelMongoDbStreamOperationType` header says what happened (`insert`, `update`, `replace` or `delete`), and the `_id` header holds the `_id` of the document.

Good to know: only changes made after the Kamelet starts are sent. MongoDB offers change streams only on a replica set or a sharded cluster, not on a single standalone server. It connects with TLS by default; set `ssl` to false for a MongoDB without TLS, such as a local one.

## Configuration Options

The following table summarizes the configuration options available for the `mongodb-changes-stream-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | MongoDB Collection | **Required** The name of the collection to watch for changes. | string |  | orders |
| **database** | MongoDB Database | **Required** The name of the database that holds the collection. | string |  | shop |
| **hosts** | MongoDB Hosts | **Required** The address of one or more members of the MongoDB replica set or sharded cluster, as `host:port`, separated by commas. MongoDB uses port 27017 unless it was set up otherwise. | string |  | mongo1.example.com:27017,mongo2.example.com:27017 |
| **password** | MongoDB Password | The password of the MongoDB user `username`. | string |  |  |
| **ssl** | Use TLS | Whether to connect with TLS (SSL). Set it to false for a MongoDB that does not offer TLS. | boolean | true |  |
| **sslValidationEnabled** | Check TLS Certificate | Whether to check the certificate and the host name of the server when `ssl` is true. Set it to false only for tests, as the connection can then be intercepted. | boolean | true |  |
| **streamFilter** | Stream Filter | A `$match` stage of a MongoDB aggregation, as JSON text, that chooses which changes to send. Match on `operationType` (such as `insert`) or on fields of the new document under `fullDocument`. When it is not set, all changes are sent. | string |  | { '$match':{'$or':\[{'fullDocument.stringValue': 'specificValue'}\]} } |
| **username** | MongoDB Username | The MongoDB user to log in as, defined in the `admin` database. Leave it empty for a MongoDB that does not ask for a login. | string |  |  |

## Dependencies

At runtime, the `mongodb-changes-stream-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:mongodb
    
-   camel:jackson
    

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
      uri: "kamelet:mongodb-changes-stream-source"
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

## Mongodb Changes Stream Source Kamelet Description

### Authentication methods

This Kamelet connects to MongoDB with:

-   Username and password authentication (optional), for a user defined in the `admin` database
    
-   TLS, on by default (`ssl`); set `ssl` to false for a MongoDB without TLS
    

### Output format

The Kamelet watches a collection with a MongoDB change stream, and sends one message for each change made after it starts, as JSON text: the new document for an insert or a replace, `null` for an update, and an object with the `_id` for a delete. The `CamelMongoDbStreamOperationType` header says which kind of change it is.

Change streams need a replica set or a sharded cluster.

### Configuration

The Kamelet requires database connection parameters:

-   `hosts`: the members of the replica set, as `host:port`
    
-   `database` and `collection`: the collection to watch
    
-   `streamFilter` (optional): a `$match` stage that chooses the changes to send
    

### Usage example

The route below logs each document inserted into the `orders` collection.

```yaml
- route:
    from:
      uri: "kamelet:mongodb-changes-stream-source"
      parameters:
        hosts: "mongo1.example.com:27017,mongo2.example.com:27017"
        database: "shop"
        collection: "orders"
        username: "mongouser"
        password: "mongopass"
        streamFilter: "{ '$match': { 'operationType': 'insert' } }"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-changes-stream-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-changes-stream-source.kamelet.yaml)