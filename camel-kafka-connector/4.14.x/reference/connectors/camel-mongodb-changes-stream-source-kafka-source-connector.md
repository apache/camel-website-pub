# camel-mongodb-changes-stream-source-kafka-connector source configuration

Connector Description: Consume Changes from MongoDB Collection in streaming mode.

When using camel-mongodb-changes-stream-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mongodb-changes-stream-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mongodbchangesstreamsource.CamelMongodbchangesstreamsourceSourceConnector
```

The camel-mongodb-changes-stream-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mongodb-changes-stream-source.hosts** | **Required** Comma separated list of MongoDB Host Addresses in host:port format. |  | HIGH |
| **camel.kamelet.mongodb-changes-stream-source.collection** | **Required** Sets the name of the MongoDB collection to bind to this endpoint. |  | HIGH |
| **camel.kamelet.mongodb-changes-stream-source.password** | User password for accessing MongoDB. |  | MEDIUM |
| **camel.kamelet.mongodb-changes-stream-source.username** | Username for accessing MongoDB. The username must be present in the MongoDB’s authentication database (authenticationDatabase). By default, the MongoDB authenticationDatabase is 'admin'. |  | MEDIUM |
| **camel.kamelet.mongodb-changes-stream-source.ssl** | whether to enable ssl connection to mongodb. | true | MEDIUM |
| **camel.kamelet.mongodb-changes-stream-source.sslValidationEnabled** | IMPORTANT this should be disabled only in test environment since can pose security issues. | true | MEDIUM |
| **camel.kamelet.mongodb-changes-stream-source.database** | **Required** Sets the name of the MongoDB database to target. |  | HIGH |
| **camel.kamelet.mongodb-changes-stream-source.streamFilter** | Filter condition for change streams consumer. Example: \\{ '$match':\\{'$or':\[\\{'fullDocument.stringValue': 'specificValue'}\]} }. |  | MEDIUM |

The camel-mongodb-changes-stream-source source connector has no converters out of the box.

The camel-mongodb-changes-stream-source source connector has no transforms out of the box.

The camel-mongodb-changes-stream-source source connector has no aggregation strategies out of the box.