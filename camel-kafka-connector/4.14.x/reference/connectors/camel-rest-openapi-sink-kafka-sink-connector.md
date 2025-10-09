# camel-rest-openapi-sink-kafka-connector sink configuration

Connector Description: Load an OpenAPI specification from a URI and call an operation on a HTTP service. The request that is generated respects the rules given in the OpenAPI specification (for example, path parameters and Content-Type).

When using camel-rest-openapi-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-rest-openapi-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.restopenapisink.CamelRestopenapisinkSinkConnector
```

The camel-rest-openapi-sink sink connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.rest-openapi-sink.specification** | **Required** The URI to the OpenApi specification file. Example: [https://api.example.com/openapi.json](https://api.example.com/openapi.json). |  | HIGH |
| **camel.kamelet.rest-openapi-sink.operation** | **Required** The operation to call. |  | HIGH |

The camel-rest-openapi-sink sink connector has no converters out of the box.

The camel-rest-openapi-sink sink connector has no transforms out of the box.

The camel-rest-openapi-sink sink connector has no aggregation strategies out of the box.