# ![mongodb sink](_images/kamelets/mongodb-sink.svg) MongoDB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Inserts each message as a new document into a collection of a MongoDB database.

Use it to store events, orders or other records as documents in MongoDB, for example each message that arrives on a Kafka topic. To read documents, use `mongodb-source` or `mongodb-changes-stream-source`.

Input: the body is one document, as a JSON object in text, such as `{"item":"book","qty":2}`. When it has no `_id` field, MongoDB gives the document a new ObjectId. A JSON array, or text that is not JSON, fails.

Output: the body afterwards is the document that was stored, as a Map with its `_id`, and the `CamelMongoOid` header holds that `_id`.

Good to know: a document whose `_id` is already in the collection fails: the Kamelet only inserts, and the `db-upsert` and `ce-dbupsert` headers do not change that. With `createCollection` false, the default, the Kamelet fails to start when the collection does not exist yet. It connects with TLS by default; set `ssl` to false for a MongoDB without TLS, such as a local one.

## Configuration Options

The following table summarizes the configuration options available for the `mongodb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | MongoDB Collection | **Required** The name of the collection to insert the documents into. | string |  | orders |
| **database** | MongoDB Database | **Required** The name of the database that holds the collection. | string |  | shop |
| **hosts** | MongoDB Hosts | **Required** The address of one or more MongoDB servers, as `host:port`, separated by commas. MongoDB uses port 27017 unless it was set up otherwise. For a replica set, list its members. | string |  | mongo1.example.com:27017,mongo2.example.com:27017 |
| **createCollection** | Create Collection | If true, the collection is created when the Kamelet starts, if it does not exist. If false, the Kamelet fails to start when the collection does not exist. | boolean | false |  |
| **password** | MongoDB Password | The password of the MongoDB user `username`. | string |  |  |
| **ssl** | Use TLS | Whether to connect with TLS (SSL). Set it to false for a MongoDB that does not offer TLS. | boolean | true |  |
| **sslValidationEnabled** | Check TLS Certificate | Whether to check the certificate and the host name of the server when `ssl` is true. Set it to false only for tests, as the connection can then be intercepted. | boolean | true |  |
| **username** | MongoDB Username | The MongoDB user to log in as, defined in the `admin` database. Leave it empty for a MongoDB that does not ask for a login. | string |  |  |
| **writeConcern** | Write Concern | How many MongoDB servers must confirm an insert before it counts as done, such as `MAJORITY` for most members of a replica set. When it is not set, MongoDB acknowledges each insert (`ACKNOWLEDGED`). Enum values: \* ACKNOWLEDGED \* W1 \* W2 \* W3 \* UNACKNOWLEDGED \* JOURNALED \* MAJORITY | string |  |  |

## Dependencies

At runtime, the `mongodb-sink` Kamelet relies upon the presence of the following dependencies:

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

Optional username and password authentication is supported for secured MongoDB instances. The Kamelet uses SSL-aware MongoDB client connections for secure data transmission.

### Write Operations

The Kamelet performs insert operations into the specified collection. A document whose `_id` is already in the collection fails; the `db-upsert` and `ce-dbupsert` headers do not change that.

### Write Concerns

Configurable write concern levels ensure data durability and consistency based on application requirements. Options include acknowledged, journaled, majority, and various numbered write concerns.

### Collection Management

The Kamelet can optionally create collections during initialization if they don’t exist (`createCollection`). When `createCollection` is false, the default, the Kamelet fails to start if the collection does not exist.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-sink.kamelet.yaml)