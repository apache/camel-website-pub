# ![mongodb changes stream source](_images/kamelets/mongodb-changes-stream-source.svg) MongoDB Changes Stream Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends a message for each change to a collection of a MongoDB database, such as a document inserted, updated or deleted, as it happens.

Use it to react to changes in MongoDB, for example to copy new orders to another system or to keep a cache or a search index up to date. To read the documents of a capped collection from the start, use `mongodb-source`. To write documents, use `mongodb-sink`.

Output: the body is JSON text. For an insert or a replace, it is the whole new document; for an update, the text `null`; for a delete, an object with only the `_id` of the deleted document. The `CamelMongoDbStreamOperationType` header says what happened (`insert`, `update`, `replace` or `delete`), and the `_id` header holds the `_id` of the document.

Good to know: only changes made after the Kamelet starts are sent. MongoDB offers change streams only on a replica set or a sharded cluster, not on a single standalone server. Set either `hosts` or `connectionString`. With `hosts`, it connects with TLS by default; set `ssl` to false for a MongoDB without TLS, such as a local one. With `connectionString`, such as the `mongodb+srv://` string of MongoDB Atlas, it connects only as that string says, and `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used. For a user defined in a database other than `admin`, use `connectionString` with `authSource`.

## Configuration Options

The following table summarizes the configuration options available for the `mongodb-changes-stream-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | MongoDB Collection | **Required** The name of the collection to watch for changes. | string |  | orders |
| **database** | MongoDB Database | **Required** The name of the database that holds the collection. | string |  | shop |
| **connectionString** | Connection String | The MongoDB connection string, which starts with `mongodb://` or `mongodb+srv://`, such as the one MongoDB Atlas shows under Connect. Use it instead of `hosts` for MongoDB Atlas, for a user defined in a database other than `admin` (add `authSource`, such as `?authSource=shop`), or for settings such as `replicaSet` or `tls`. When it is set, `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used. TLS is used as the string says: always with `mongodb+srv://`, and with `mongodb://` only when it has `tls=true`. Write `@`, `/`, `:` and `%` in the user name or the password as `%40`, `%2F`, `%3A` and `%25`. | string |  | mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority |
| **hosts** | MongoDB Hosts | The address of one or more members of the MongoDB replica set or sharded cluster, as `host:port`, separated by commas. MongoDB uses port 27017 unless it was set up otherwise. Set either `hosts` or `connectionString`. When neither is set, the Kamelet fails to start with the error `The connection string contains an empty host`. | string |  | mongo1.example.com:27017,mongo2.example.com:27017 |
| **password** | MongoDB Password | The password of the MongoDB user `username`. Write `@`, `/`, `:` and `%` in it as `%40`, `%2F`, `%3A` and `%25`. | string |  |  |
| **ssl** | Use TLS | Whether to connect with TLS (SSL). Set it to false for a MongoDB that does not offer TLS. Not used with `connectionString`. | boolean | true |  |
| **sslValidationEnabled** | Check TLS Certificate | Whether to check the certificate and the host name of the server when `ssl` is true. Set it to false only for tests, as the connection can then be intercepted. Not used with `connectionString`. | boolean | true |  |
| **streamFilter** | Stream Filter | A `$match` stage of a MongoDB aggregation, as JSON text, that chooses which changes to send. Match on `operationType` (such as `insert`) or on fields of the new document under `fullDocument`. When it is not set, all changes are sent. | string |  | { '$match':{'$or':\[{'fullDocument.stringValue': 'specificValue'}\]} } |
| **username** | MongoDB Username | The MongoDB user to log in as, defined in the `admin` database. For a user defined in another database, use `connectionString` with `authSource` instead. Leave it empty for a MongoDB that does not ask for a login. | string |  |  |

## Dependencies

At runtime, the `mongodb-changes-stream-source` Kamelet relies upon the presence of the following dependencies:

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

-   `hosts`, with username and password authentication (optional) for a user defined in the `admin` database, and TLS on by default (`ssl`); set `ssl` to false for a MongoDB without TLS
    
-   or a MongoDB connection string (`connectionString`), such as the `mongodb+srv://` string of MongoDB Atlas; see below
    

### Output format

The Kamelet watches a collection with a MongoDB change stream, and sends one message for each change made after it starts, as JSON text: the new document for an insert or a replace, `null` for an update, and an object with the `_id` for a delete. The `CamelMongoDbStreamOperationType` header says which kind of change it is.

Change streams need a replica set or a sharded cluster.

### Configuration

The Kamelet requires database connection parameters:

-   `hosts` (the members of the replica set, as `host:port`) or `connectionString`
    
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

### Connecting with a connection string

Set either `hosts` or `connectionString`. Use `connectionString` to connect to MongoDB Atlas with its `mongodb+srv://` string, to log in as a user defined in a database other than `admin` (with `authSource`), or to give other settings of the MongoDB connection string, such as `replicaSet` or `tls`. When it is set, `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used, and TLS is used as the string says: always with `mongodb+srv://`, and with `mongodb://` only when it has `tls=true`.

Write `@`, `/`, `:` and `%` in the user name or the password as `%40`, `%2F`, `%3A` and `%25`. The connection string holds the password, so keep it in a secret, like the `password` option.

With MongoDB Atlas, copy the string from the Connect dialog of the cluster:

```yaml
- route:
    from:
      uri: "kamelet:mongodb-changes-stream-source"
      parameters:
        connectionString: "mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority"
        database: "shop"
        collection: "orders"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

For a user defined in the `shop` database, on a MongoDB without TLS:

```yaml
connectionString: "mongodb://shopuser:shoppass@mongo1.example.com:27017,mongo2.example.com:27017/?authSource=shop&replicaSet=rs0"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-changes-stream-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-changes-stream-source.kamelet.yaml)