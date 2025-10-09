# ![mongodb sink](_images/kamelets/mongodb-sink.svg) MongoDB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to MongoDB.

## Configuration Options

The following table summarizes the configuration options available for the `mongodb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | MongoDB Collection | **Required** The name of the MongoDB collection to bind to this endpoint. | string |  |  |
| **database** | MongoDB Database | **Required** The name of the MongoDB database. | string |  |  |
| **hosts** | MongoDB Hosts | **Required** A comma-separated list of MongoDB host addresses in `host:port` format. | string |  |  |
| **createCollection** | Collection | Create a collection during initialization if it doesn’t exist. | boolean | false |  |
| **password** | MongoDB Password | A user password for accessing MongoDB. | string |  |  |
| **ssl** | Enable Ssl for Mongodb Connection | whether to enable ssl connection to mongodb. | boolean | true |  |
| **sslValidationEnabled** | Enables Ssl Certificates Validation and Host name checks. | IMPORTANT this should be disabled only in test environment since can pose security issues. | boolean | true |  |
| **username** | MongoDB Username | A username for accessing MongoDB. | string |  |  |
| **writeConcern** | Write Concern | The level of acknowledgment requested from MongoDB for write operations. Enum values: \* ACKNOWLEDGED \* W1 \* W2 \* W3 \* UNACKNOWLEDGED \* JOURNALED \* MAJORITY | string |  |  |

## Dependencies

At runtime, the `mongodb-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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

The Kamelet performs insert operations into the specified collection. It supports upsert operations through header configuration (`db-upsert` or `ce-dbupsert` headers).

### Write Concerns

Configurable write concern levels ensure data durability and consistency based on application requirements. Options include acknowledged, journaled, majority, and various numbered write concerns.

### Collection Management

The Kamelet can optionally create collections during initialization if they don’t exist, providing flexibility for dynamic database structures.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-sink.kamelet.yaml)