# camel-http-sink-kafka-connector sink configuration

Connector Description: Forward data to a HTTP or HTTPS endpoint.

When using camel-http-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-http-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.httpsink.CamelHttpsinkSinkConnector
```

The camel-http-sink sink connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.http-sink.url** | **Required** The URL to which you want to send data. Example: [https://my-service/path](https://my-service/path). |  | HIGH |
| **camel.kamelet.http-sink.method** | The HTTP method to use. | "POST" | MEDIUM |

The camel-http-sink sink connector has no converters out of the box.

The camel-http-sink sink connector has no transforms out of the box.

The camel-http-sink sink connector has no aggregation strategies out of the box.