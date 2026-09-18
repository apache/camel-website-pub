# camel-mongodb-source-kafka-connector source configuration

Connector Description: Consume data from MongoDB.

When using camel-mongodb-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mongodb-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mongodbsource.CamelMongodbsourceSourceConnector
```

The camel-mongodb-source source connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mongodb-source.hosts** | **Required** A comma-separated list of MongoDB host addresses in `host:port` format. |  | HIGH |
| **camel.kamelet.mongodb-source.collection** | **Required** The name of the MongoDB collection to bind to this endpoint. |  | HIGH |
| **camel.kamelet.mongodb-source.password** | The user password for accessing MongoDB. |  | MEDIUM |
| **camel.kamelet.mongodb-source.username** | The username for accessing MongoDB. The username must be present in the MongoDB’s authentication database (`authenticationDatabase`). By default, the MongoDB `authenticationDatabase` is 'admin'. |  | MEDIUM |
| **camel.kamelet.mongodb-source.ssl** | whether to enable ssl connection to mongodb. | true | MEDIUM |
| **camel.kamelet.mongodb-source.sslValidationEnabled** | IMPORTANT this should be disabled only in test environment since can pose security issues. | true | MEDIUM |
| **camel.kamelet.mongodb-source.database** | **Required** The name of the MongoDB database. |  | HIGH |
| **camel.kamelet.mongodb-source.persistentTailTracking** | Specifies to enable persistent tail tracking, which is a mechanism to keep track of the last consumed data across system restarts. The next time the system is up, the endpoint recovers the cursor from the point where it last stopped consuimg data. This option will only work on capped collections. | false | MEDIUM |
| **camel.kamelet.mongodb-source.tailTrackIncreasingField** | The correlation field in the incoming data which is of increasing nature and is used to position the tailing cursor every time it is generated. |  | MEDIUM |

The camel-mongodb-source source connector has no converters out of the box.

The camel-mongodb-source source connector has no transforms out of the box.

The camel-mongodb-source source connector has no aggregation strategies out of the box.