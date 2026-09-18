# camel-graphql-sink-kafka-connector sink configuration

Connector Description: Forward data to a GraphQL endpoint.

When using camel-graphql-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-graphql-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.graphqlsink.CamelGraphqlsinkSinkConnector
```

The camel-graphql-sink sink connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.graphql-sink.url** | **Required** The URL to which you want to send data. Example: [http://example.com/graphql](http://example.com/graphql). |  | HIGH |
| **camel.kamelet.graphql-sink.accessToken** | The access Token to use to access GraphQL server. |  | MEDIUM |

The camel-graphql-sink sink connector has no converters out of the box.

The camel-graphql-sink sink connector has no transforms out of the box.

The camel-graphql-sink sink connector has no aggregation strategies out of the box.