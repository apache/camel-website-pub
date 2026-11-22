# ![mongodb changes stream source](_images/kamelets/mongodb-changes-stream-source.svg) MongoDB Changes Stream Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends a message for each change to a collection of a MongoDB database, such as a document inserted, updated or deleted, as it happens.

Use it to react to changes in MongoDB, for example to copy new orders to another system or to keep a cache or a search index up to date. To read the documents of a capped collection from the start, use `mongodb-source`. To write documents, use `mongodb-sink`.

Output: the body is JSON text in bytes. For an insert or a replace, it is the whole new document. For an update, it is the whole document as it is when the change is sent, read again from the collection, so it can already hold later changes, and it is the text `null` when the document was deleted meanwhile; `fullDocument` changes this. For a delete, it is an object with only the `_id` of the deleted document. The `CamelMongoDbStreamOperationType` header says what happened (`insert`, `update`, `replace` or `delete`), and the `_id` header holds the `_id` of the document.

Good to know: only changes made after the Kamelet starts are sent. It does not save where it stopped, so the changes made while it is stopped, such as during a restart, are never sent, unless `tokenRepository` is set: with a `StateRepository` bean, such as an `org.apache.camel.support.processor.state.FileStateRepository`, given as `#name`, it stores the resume token after each change and, after a restart, sends the changes made while it was stopped. The collection must exist when the Kamelet starts; otherwise it fails to start with `Collection …​ does not exist on the database`. Reading the document again costs MongoDB one more read for each update; set `fullDocument` to `default` to send `null` for an update instead. MongoDB offers change streams only on a replica set or a sharded cluster, not on a single standalone server. Set either `hosts` or `connectionString`. With `hosts`, it connects with TLS by default; set `ssl` to false for a MongoDB without TLS, such as a local one. With `connectionString`, such as the `mongodb+srv://` string of MongoDB Atlas, it connects only as that string says, and `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used. For a user defined in a database other than `admin`, use `connectionString` with `authSource`.

## Configuration Options

The following table summarizes the configuration options available for the `mongodb-changes-stream-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | MongoDB Collection | **Required** The name of the collection to watch for changes. | string |  | orders |
| **database** | MongoDB Database | **Required** The name of the database that holds the collection. | string |  | shop |
| **connectionString** | Connection String | The MongoDB connection string, which starts with `mongodb://` or `mongodb+srv://`, such as the one MongoDB Atlas shows under Connect. Use it instead of `hosts` for MongoDB Atlas, for a user defined in a database other than `admin` (add `authSource`, such as `?authSource=shop`), or for settings such as `replicaSet` or `tls`. When it is set, `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used. TLS is used as the string says: always with `mongodb+srv://`, and with `mongodb://` only when it has `tls=true`. Write `@`, `/`, `:` and `%` in the user name or the password as `%40`, `%2F`, `%3A` and `%25`. | string |  | mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority |
| **fullDocument** | Document of an Update | What the body is for an update; inserts, replaces and deletes are sent the same with any value. `updateLookup` (the default): the whole document, read again from the collection when the change is sent. It can already hold later changes, and it is the text `null` when the document was deleted meanwhile. Use it to keep a copy, a cache or a search index up to date. An update whose document and changed fields are together larger than about 16 MB cannot be sent: the Kamelet then retries it every second and sends no later change. `default`: the text `null`, with no extra read. `whenAvailable`: the document as it was right after this update, which MongoDB saves only for a collection with change stream post-images turned on (`changeStreamPreAndPostImages`); for another collection, the text `null`. `required`: as `whenAvailable`, but for a collection without post-images, the Kamelet retries the update every second and sends no later change. Enum values: \* updateLookup \* default \* whenAvailable \* required | string | updateLookup |  |
| **hosts** | MongoDB Hosts | The address of one or more members of the MongoDB replica set or sharded cluster, as `host:port`, separated by commas. MongoDB uses port 27017 unless it was set up otherwise. Set either `hosts` or `connectionString`. When neither is set, the Kamelet fails to start with the error `The connection string contains an empty host`. | string |  | mongo1.example.com:27017,mongo2.example.com:27017 |
| **password** | MongoDB Password | The password of the MongoDB user `username`. Write `@`, `/`, `:` and `%` in it as `%40`, `%2F`, `%3A` and `%25`. | string |  |  |
| **readPreference** | Read Preference | Which members of the replica set the Kamelet reads from: `PRIMARY` (the primary only), `PRIMARY_PREFERRED` (the primary, or a secondary while there is no primary), `SECONDARY` (a secondary only), `SECONDARY_PREFERRED` (a secondary, or the primary when there is no secondary) or `NEAREST` (the member with the lowest network latency). Reading from a secondary takes load off the primary, but a secondary can be a little behind it. With `SECONDARY` and no secondary available, the Kamelet cannot read. When it is not set, the Kamelet reads from the primary. Not used with `connectionString`; put `readPreference` in the connection string instead, such as `?readPreference=secondaryPreferred`. Enum values: \* PRIMARY \* PRIMARY\_PREFERRED \* SECONDARY \* SECONDARY\_PREFERRED \* NEAREST | string |  | SECONDARY\_PREFERRED |
| **ssl** | Use TLS | Whether to connect with TLS (SSL). Set it to false for a MongoDB that does not offer TLS. Not used with `connectionString`. | boolean | true |  |
| **sslValidationEnabled** | Check TLS Certificate | Whether to check the certificate and the host name of the server when `ssl` is true. Set it to false only for tests, as the connection can then be intercepted. Not used with `connectionString`. | boolean | true |  |
| **streamFilter** | Stream Filter | A `$match` stage of a MongoDB aggregation, as JSON text, that chooses which changes to send. Match on `operationType` (such as `insert`) or on fields of the document under `fullDocument`. For an update, `fullDocument` holds the document the Kamelet sends, so with the `fullDocument` option set to `default` an update never matches a field under it. When it is not set, all changes are sent. | string |  | { '$match':{'$or':\[{'fullDocument.stringValue': 'specificValue'}\]} } |
| **tokenRepository** | Resume Token Repository | A reference to a `StateRepository` bean that stores the resume token after each change, such as `#changeStreamTokens`, so that after a restart the Kamelet goes on from where it stopped. Declare the bean in the integration, for example an `org.apache.camel.support.processor.state.FileStateRepository` whose `fileStore` property is set to `#class:java.io.File('/data/change-stream-tokens.dat')`. Without it, the changes made while the Kamelet is stopped are not sent. | string |  | #changeStreamTokens |
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

The Kamelet watches a collection with a MongoDB change stream, and sends one message for each change made after it starts, as JSON text: the new document for an insert or a replace, the whole document for an update (see below), and an object with the `_id` for a delete. The `CamelMongoDbStreamOperationType` header says which kind of change it is.

Change streams need a replica set or a sharded cluster.

### Restarts

The Kamelet does not save where it stopped. Each time it starts, it sends only the changes made from then on, so the changes made while it is stopped, such as during a restart or an upgrade, are never sent. A system that must not miss a change has to catch up from the collection itself after a restart.

The collection must exist when the Kamelet starts. Otherwise the Kamelet fails to start with `Collection …​ does not exist on the database and createCollection is false`.

### The document of an update

MongoDB records an update as the fields that changed, not as the document. The `fullDocument` option says what the Kamelet sends as the body for an update:

 
| `fullDocument` | Body for an update |
| --- | --- |
| `updateLookup` (default) | The whole document, read again from the collection when the change is sent. It can already hold later changes: after three quick updates of `qty` to 2, 3 and 4, all three messages can show `qty` 4. It is `null` when the document was deleted meanwhile. This costs MongoDB one more read for each update. |
| `default` | `null`. Only the `_id` header says which document changed. |
| `whenAvailable` | The document as it was right after this update, on a collection with change stream post-images turned on (see below); `null` on another collection. |
| `required` | As `whenAvailable`, but on a collection without post-images, the Kamelet retries the update every second and sends no later change. |

Inserts, replaces and deletes are sent the same with any value. A `streamFilter` on a field under `fullDocument` matches an update only when the body of the update is a document, so never with `default`.

With `updateLookup`, an update whose document and changed fields are together larger than about 16 MB cannot be sent (MongoDB fails with `BSONObjectTooLarge`): the Kamelet retries it every second and sends no later change. Use `default` for a collection with such documents.

To send each update with the document as it was right after that update, turn on post-images for the collection, as a user allowed to run `collMod`:

```javascript
db.runCommand({ collMod: "orders", changeStreamPreAndPostImages: { enabled: true } })
```

and set `fullDocument` to `whenAvailable`:

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
        fullDocument: "whenAvailable"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

With post-images turned on, MongoDB saves a copy of the document for each update in its `config.system.preimages` collection, which takes disk space until MongoDB removes it.

### Configuration

The Kamelet requires database connection parameters:

-   `hosts` (the members of the replica set, as `host:port`) or `connectionString`
    
-   `database` and `collection`: the collection to watch
    
-   `streamFilter` (optional): a `$match` stage that chooses the changes to send
    
-   `fullDocument` (optional): what the body is for an update; by default the whole document
    

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