# camel-mongodb-sink-kafka-connector sink configuration

Connector Description: Send data to MongoDB.

When using camel-mongodb-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mongodb-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mongodbsink.CamelMongodbsinkSinkConnector
```

The camel-mongodb-sink sink connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mongodb-sink.hosts** | **Required** A comma-separated list of MongoDB host addresses in `host:port` format. |  | HIGH |
| **camel.kamelet.mongodb-sink.collection** | **Required** The name of the MongoDB collection to bind to this endpoint. |  | HIGH |
| **camel.kamelet.mongodb-sink.password** | A user password for accessing MongoDB. |  | MEDIUM |
| **camel.kamelet.mongodb-sink.username** | A username for accessing MongoDB. |  | MEDIUM |
| **camel.kamelet.mongodb-sink.ssl** | whether to enable ssl connection to mongodb. | true | MEDIUM |
| **camel.kamelet.mongodb-sink.sslValidationEnabled** | IMPORTANT this should be disabled only in test environment since can pose security issues. | true | MEDIUM |
| **camel.kamelet.mongodb-sink.database** | **Required** The name of the MongoDB database. |  | HIGH |
| **camel.kamelet.mongodb-sink.writeConcern** | The level of acknowledgment requested from MongoDB for write operations. |  | MEDIUM |
| **camel.kamelet.mongodb-sink.createCollection** | Create a collection during initialization if it doesn’t exist. | false | MEDIUM |

The camel-mongodb-sink sink connector has no converters out of the box.

The camel-mongodb-sink sink connector has no transforms out of the box.

The camel-mongodb-sink sink connector has no aggregation strategies out of the box.