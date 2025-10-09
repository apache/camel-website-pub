# camel-google-functions-sink-kafka-connector sink configuration

Connector Description: Send data to Google Functions.

When using camel-google-functions-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-functions-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlefunctionssink.CamelGooglefunctionssinkSinkConnector
```

The camel-google-functions-sink sink connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-functions-sink.projectId** | **Required** The Google Cloud Functions Project ID. |  | HIGH |
| **camel.kamelet.google-functions-sink.region** | **Required** The region where Google Cloud Functions has been deployed. |  | HIGH |
| **camel.kamelet.google-functions-sink.functionName** | **Required** The Function name. |  | HIGH |
| **camel.kamelet.google-functions-sink.serviceAccountKey** | **Required** The path to the service account key file that provides credentials for the Google Cloud Functions platform. You must encode this value in base64. |  | HIGH |

The camel-google-functions-sink sink connector has no converters out of the box.

The camel-google-functions-sink sink connector has no transforms out of the box.

The camel-google-functions-sink sink connector has no aggregation strategies out of the box.