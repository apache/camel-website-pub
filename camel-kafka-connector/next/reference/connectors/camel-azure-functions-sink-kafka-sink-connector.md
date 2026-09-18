# camel-azure-functions-sink-kafka-connector sink configuration

Connector Description: Forward data to an Azure Function.

When using camel-azure-functions-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-functions-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurefunctionssink.CamelAzurefunctionssinkSinkConnector
```

The camel-azure-functions-sink sink connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-functions-sink.url** | **Required** The Azure Functions URL you want to send the data to. Example: [https://azure-function-demo-12234.azurewebsites.net/api/httpexample](https://azure-function-demo-12234.azurewebsites.net/api/httpexample). |  | HIGH |
| **camel.kamelet.azure-functions-sink.method** | The HTTP method to use. | "POST" | MEDIUM |
| **camel.kamelet.azure-functions-sink.key** | A function-specific API key is required, if the authLevel of the function is FUNCTION or master key if the authLevel is ADMIN. |  | MEDIUM |

The camel-azure-functions-sink sink connector has no converters out of the box.

The camel-azure-functions-sink sink connector has no transforms out of the box.

The camel-azure-functions-sink sink connector has no aggregation strategies out of the box.