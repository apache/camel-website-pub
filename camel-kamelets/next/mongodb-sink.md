# ![mongodb sink](_images/kamelets/mongodb-sink.svg) MongoDB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Writes each message to a collection of a MongoDB database: inserts it as a new document, or, with `operation`, replaces or updates a stored document.

Use it to store events, orders or other records as documents in MongoDB, for example each message that arrives on a Kafka topic, to keep a copy of records by their ID (`save`), or to change fields of a document, such as the stock of a product (`update`). To read documents, use `mongodb-source` or `mongodb-changes-stream-source`.

Input: with `insert` (the default) and `save`, the body is one document, as a JSON object in text, such as `{"item":"book","qty":2}`. When it has no `_id` field, MongoDB gives the document a new ObjectId. With `update`, the body is a JSON array in text of two objects: the filter that selects the document and the changes, such as `[{"sku":"A1"},{"$set":{"qty":3}}]`. An ObjectId is written as `{"$oid":"…​"}`. Text that is not JSON fails.

Output: with `insert`, the body afterwards is the document that was stored, as a Map with its `_id`. With `save` and `update`, it is the result that MongoDB returns. With `insert` and `save`, the `CamelMongoOid` header holds the `_id` of the document. With `update`, the `CamelMongoDbRecordsMatched` and `CamelMongoDbRecordsAffected` headers say how many documents matched the filter and how many were changed.

Good to know: with `insert`, a document whose `_id` is already in the collection fails; `save` replaces it instead. `save` replaces the whole document, so fields that are not in the body are removed. `update` changes only the first document that matches, and nothing when none matches, unless `upsert` is true. The `db-upsert` and `ce-dbupsert` headers are not used. With `createCollection` false, the default, the Kamelet fails to start when the collection does not exist yet. Set either `hosts` or `connectionString`. With `hosts`, it connects with TLS by default; set `ssl` to false for a MongoDB without TLS, such as a local one. With `connectionString`, such as the `mongodb+srv://` string of MongoDB Atlas, it connects only as that string says, and `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used. For a user defined in a database other than `admin`, use `connectionString` with `authSource`. Headers that start with `CamelMongo` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `mongodb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | MongoDB Collection | **Required** The name of the collection to write the documents to. | string |  | orders |
| **database** | MongoDB Database | **Required** The name of the database that holds the collection. | string |  | shop |
| **connectionString** | Connection String | The MongoDB connection string, which starts with `mongodb://` or `mongodb+srv://`, such as the one MongoDB Atlas shows under Connect. Use it instead of `hosts` for MongoDB Atlas, for a user defined in a database other than `admin` (add `authSource`, such as `?authSource=shop`), or for settings such as `replicaSet` or `tls`. When it is set, `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used. TLS is used as the string says: always with `mongodb+srv://`, and with `mongodb://` only when it has `tls=true`. Write `@`, `/`, `:` and `%` in the user name or the password as `%40`, `%2F`, `%3A` and `%25`. | string |  | mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority |
| **createCollection** | Create Collection | If true, the collection is created when the Kamelet starts, if it does not exist. If false, the Kamelet fails to start when the collection does not exist. | boolean | false |  |
| **hosts** | MongoDB Hosts | The address of one or more MongoDB servers, as `host:port`, separated by commas. MongoDB uses port 27017 unless it was set up otherwise. For a replica set, list its members. Set either `hosts` or `connectionString`. When neither is set, the Kamelet fails to start with the error `The connection string contains an empty host`. | string |  | mongo1.example.com:27017,mongo2.example.com:27017 |
| **operation** | Operation | What to do with each message. `insert` adds the body as a new document, and fails when its `_id` is already in the collection. `save` replaces the document that has the `_id` of the body as a whole, or adds the body when there is none or the body has no `_id`. `update` changes the first document that matches a filter: the body is the filter and the changes, such as `[\{"sku":"A1"},\{"$set":\{"qty":3}}]`, and the changes must use update operators such as `$set`, `$inc` or `$unset`. Enum values: \* insert \* save \* update | string | insert |  |
| **password** | MongoDB Password | The password of the MongoDB user `username`. Write `@`, `/`, `:` and `%` in it as `%40`, `%2F`, `%3A` and `%25`. | string |  |  |
| **ssl** | Use TLS | Whether to connect with TLS (SSL). Set it to false for a MongoDB that does not offer TLS. Not used with `connectionString`. | boolean | true |  |
| **sslValidationEnabled** | Check TLS Certificate | Whether to check the certificate and the host name of the server when `ssl` is true. Set it to false only for tests, as the connection can then be intercepted. Not used with `connectionString`. | boolean | true |  |
| **upsert** | Insert When Missing | Only used when `operation` is `update`. If true, a filter that matches no document inserts a new one, made of the fields of the filter and the changes, such as `\{"sku":"A1","qty":3}`, and the next message with the same filter updates it. If false or not set, a filter that matches no document changes nothing. | boolean |  |  |
| **username** | MongoDB Username | The MongoDB user to log in as, defined in the `admin` database. For a user defined in another database, use `connectionString` with `authSource` instead. Leave it empty for a MongoDB that does not ask for a login. | string |  |  |
| **writeConcern** | Write Concern | How many MongoDB servers must confirm a write before it counts as done, such as `MAJORITY` for most members of a replica set. When it is not set, MongoDB acknowledges each write (`ACKNOWLEDGED`). Enum values: \* ACKNOWLEDGED \* W1 \* W2 \* W3 \* UNACKNOWLEDGED \* JOURNALED \* MAJORITY | string |  |  |

## Dependencies

At runtime, the `mongodb-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:mongodb
    
-   camel:jackson3
    

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
            uri: "kamelet:mongodb-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## MongoDB Sink Kamelet Description

### NoSQL Database Integration

This Kamelet integrates with MongoDB, a popular NoSQL document database. MongoDB stores data in flexible, JSON-like documents, making it ideal for applications requiring dynamic schemas.

### SSL/TLS Security

The Kamelet supports SSL/TLS encryption for secure connections to MongoDB. SSL is enabled by default, and certificate validation can be configured based on security requirements.

### Authentication

Optional username and password authentication is supported for secured MongoDB instances, for a user defined in the `admin` database. The Kamelet uses SSL-aware MongoDB client connections for secure data transmission. For MongoDB Atlas, or a user defined in another database, use a connection string instead, as shown below.

### Write Operations

The `operation` option says what the Kamelet does with each message:

  
| `operation` | Body | What happens |
| --- | --- | --- |
| `insert` (default) | One document as a JSON object, such as `{"_id":"o-1","item":"book","qty":2}` | The document is added. A document whose `_id` is already in the collection fails. |
| `save` | One document as a JSON object, such as `{"_id":"o-1","item":"book","qty":5}` | The stored document with the same `_id` is replaced as a whole: fields that are not in the body are removed. When there is none, or the body has no `_id`, the document is added. |
| `update` | A JSON array of the filter and the changes, such as `[{"sku":"A1"},{"$set":{"qty":3}}]` | The first document that matches the filter is changed. The changes must use update operators, such as `$set`, `$inc` or `$unset`. When no document matches, nothing is written, unless `upsert` is true. |

An ObjectId is written in the body as `{"$oid":"6afd00000000000000000001"}`. With `insert` and `save`, the `CamelMongoOid` header holds the `_id` of the document. With `update`, the `CamelMongoDbRecordsMatched` and `CamelMongoDbRecordsAffected` headers say how many documents matched and how many were changed. The `db-upsert` and `ce-dbupsert` headers are not used.

### Example with Update and Upsert

With `upsert` true, the first message for a product inserts `{"sku":"A1","qty":2}`, and each later one updates it:

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "stock"
        bootstrapServers: "kafka.example.com:9092"
        saslAuthType: "NONE"
      steps:
        # each record is a JSON array such as [{"sku":"A1"},{"$set":{"qty":2}}]
        - to:
            uri: "kamelet:mongodb-sink"
            parameters:
              hosts: "mongo1.example.com:27017"
              username: "mongouser"
              password: "mongopass"
              database: "shop"
              collection: "stock"
              operation: "update"
              upsert: true
```

To keep a copy of records by their ID instead, set `operation` to `save` and send each record as a document with its `_id`.

### Write Concerns

Configurable write concern levels ensure data durability and consistency based on application requirements. Options include acknowledged, journaled, majority, and various numbered write concerns.

### Collection Management

The Kamelet can optionally create collections during initialization if they don’t exist (`createCollection`). When `createCollection` is false, the default, the Kamelet fails to start if the collection does not exist.

### Connecting with a connection string

Set either `hosts` or `connectionString`. Use `connectionString` to connect to MongoDB Atlas with its `mongodb+srv://` string, to log in as a user defined in a database other than `admin` (with `authSource`), or to give other settings of the MongoDB connection string, such as `replicaSet` or `tls`. When it is set, `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used, and TLS is used as the string says: always with `mongodb+srv://`, and with `mongodb://` only when it has `tls=true`.

Write `@`, `/`, `:` and `%` in the user name or the password as `%40`, `%2F`, `%3A` and `%25`. The connection string holds the password, so keep it in a secret, like the `password` option.

With MongoDB Atlas, copy the string from the Connect dialog of the cluster:

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "orders"
        bootstrapServers: "kafka.example.com:9092"
        saslAuthType: "NONE"
      steps:
        - to:
            uri: "kamelet:mongodb-sink"
            parameters:
              connectionString: "mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority"
              database: "shop"
              collection: "orders"
```

For a user defined in the `shop` database, on a MongoDB without TLS:

```yaml
connectionString: "mongodb://shopuser:shoppass@mongo1.example.com:27017,mongo2.example.com:27017/?authSource=shop&replicaSet=rs0"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-sink.kamelet.yaml)