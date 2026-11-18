# ![mongodb source](_images/kamelets/mongodb-source.svg) MongoDB Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the documents of a capped collection in a MongoDB database, first those already there and then each new one as it is added, one message per document, as JSON text.

Use it to pass on records that an application appends to a capped collection, such as log entries or events, as they arrive. For a normal collection, or to also see updates and deletes, use `mongodb-changes-stream-source`. To write documents, use `mongodb-sink`.

Output: the body is one document as JSON text. An `_id` that is an ObjectId comes out as an object with only its time (`timestamp` and `date`), not as the ID text, and the format of dates depends on the Camel version. The `CamelMongoDbDatabase` and `CamelMongoDbCollection` headers name where the document comes from.

Good to know: the collection must be capped (created with a fixed size), or the Kamelet fails to start. Each time the integration starts, it reads the whole collection again from the start, unless `persistentTailTracking` is true. Set either `hosts` or `connectionString`. With `hosts`, it connects with TLS by default; set `ssl` to false for a MongoDB without TLS, such as a local one. With `connectionString`, such as the `mongodb+srv://` string of MongoDB Atlas, it connects only as that string says, and `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used. For a user defined in a database other than `admin`, use `connectionString` with `authSource`.

## Configuration Options

The following table summarizes the configuration options available for the `mongodb-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | MongoDB Collection | **Required** The name of the capped collection to read. | string |  | events |
| **database** | MongoDB Database | **Required** The name of the database that holds the collection. | string |  | shop |
| **connectionString** | Connection String | The MongoDB connection string, which starts with `mongodb://` or `mongodb+srv://`, such as the one MongoDB Atlas shows under Connect. Use it instead of `hosts` for MongoDB Atlas, for a user defined in a database other than `admin` (add `authSource`, such as `?authSource=shop`), or for settings such as `replicaSet` or `tls`. When it is set, `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used. TLS is used as the string says: always with `mongodb+srv://`, and with `mongodb://` only when it has `tls=true`. Write `@`, `/`, `:` and `%` in the user name or the password as `%40`, `%2F`, `%3A` and `%25`. | string |  | mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority |
| **hosts** | MongoDB Hosts | The address of one or more MongoDB servers, as `host:port`, separated by commas. MongoDB uses port 27017 unless it was set up otherwise. For a replica set, list its members. Set either `hosts` or `connectionString`. When neither is set, the Kamelet fails to start with the error `The connection string contains an empty host`. | string |  | mongo1.example.com:27017,mongo2.example.com:27017 |
| **password** | MongoDB Password | The password of the MongoDB user `username`. Write `@`, `/`, `:` and `%` in it as `%40`, `%2F`, `%3A` and `%25`. | string |  |  |
| **persistentTailTracking** | Remember Last Document | If true, the Kamelet stores the `tailTrackIncreasingField` value of the last document it read in the `camelTailTracking` collection of the same database, and after a restart goes on from there instead of reading the whole collection again. Needs `tailTrackIncreasingField`. | boolean | false |  |
| **ssl** | Use TLS | Whether to connect with TLS (SSL). Set it to false for a MongoDB that does not offer TLS. Not used with `connectionString`. | boolean | true |  |
| **sslValidationEnabled** | Check TLS Certificate | Whether to check the certificate and the host name of the server when `ssl` is true. Set it to false only for tests, as the connection can then be intercepted. Not used with `connectionString`. | boolean | true |  |
| **tailTrackIncreasingField** | Increasing Field | The name of a field whose value grows with each new document, such as a sequence number or a time, used to find the place to go on reading from. Required when `persistentTailTracking` is true. | string |  | seq |
| **username** | MongoDB Username | The MongoDB user to log in as, defined in the `admin` database. For a user defined in another database, use `connectionString` with `authSource` instead. Leave it empty for a MongoDB that does not ask for a login. | string |  |  |

## Dependencies

At runtime, the `mongodb-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:mongodb-source"
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

## MongoDB Source Kamelet Description

### Authentication

This Kamelet supports MongoDB authentication using username and password credentials. The connection can be configured with or without authentication depending on your MongoDB setup.

### Configuration

The MongoDB Source Kamelet supports the following configurations:

-   **Hosts**: MongoDB server hosts and ports; set either this or the connection string
    
-   **Connection String**: a MongoDB connection string, such as the `mongodb+srv://` string of MongoDB Atlas, used instead of the hosts, username, password and SSL settings
    
-   **Collection**: MongoDB collection name to read; it must be a capped collection (required)
    
-   **Database**: MongoDB database name (required)
    
-   **Username**: Username for authentication (optional)
    
-   **Password**: Password for authentication (optional)
    
-   **SSL**: Whether to connect with TLS (default: true); set it to false for a MongoDB without TLS
    
-   **Tail Track Increasing Field**: A field whose value grows with each new document
    
-   **Persistent Tail Tracking**: Remember the last document read across restarts (needs the increasing field)
    

### Output Format

The Kamelet reads the documents of a capped collection with a tailable cursor: first the documents already there, then each new one as it is added. Each document is sent as one message, as JSON text.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:mongodb-source"
      parameters:
        hosts: "mongodb.example.com:27017"
        database: "logs"
        collection: "app_logs"
        username: "mongouser"
        password: "mongopass"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Persistent Tail Tracking

The Kamelet stores the `seq` value of the last document read in the `camelTailTracking` collection of the same database, and after a restart goes on from there.

```yaml
- route:
    from:
      uri: "kamelet:mongodb-source"
      parameters:
        hosts: "mongo1.example.com:27017,mongo2.example.com:27017,mongo3.example.com:27017"
        database: "production"
        collection: "events"
        username: "mongouser"
        password: "mongopass"
        tailTrackIncreasingField: "seq"
        persistentTailTracking: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Capped Collections

The collection must be capped, or the Kamelet fails to start. A capped collection is created with a fixed size, for example in `mongosh`:

```javascript
db.createCollection("events", { capped: true, size: 100000 })
```

### Connecting with a connection string

Set either `hosts` or `connectionString`. Use `connectionString` to connect to MongoDB Atlas with its `mongodb+srv://` string, to log in as a user defined in a database other than `admin` (with `authSource`), or to give other settings of the MongoDB connection string, such as `replicaSet` or `tls`. When it is set, `hosts`, `username`, `password`, `ssl` and `sslValidationEnabled` are not used, and TLS is used as the string says: always with `mongodb+srv://`, and with `mongodb://` only when it has `tls=true`.

Write `@`, `/`, `:` and `%` in the user name or the password as `%40`, `%2F`, `%3A` and `%25`. The connection string holds the password, so keep it in a secret, like the `password` option.

With MongoDB Atlas, copy the string from the Connect dialog of the cluster:

```yaml
- route:
    from:
      uri: "kamelet:mongodb-source"
      parameters:
        connectionString: "mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority"
        database: "logs"
        collection: "app_logs"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

For a user defined in the `shop` database, on a MongoDB without TLS:

```yaml
connectionString: "mongodb://shopuser:shoppass@mongo1.example.com:27017,mongo2.example.com:27017/?authSource=shop&replicaSet=rs0"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-source.kamelet.yaml)