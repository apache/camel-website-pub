# camel-google-storage-sink-kafka-connector sink configuration

Connector Description: Upload objects to Google Cloud Storage.

When using camel-google-storage-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-storage-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlestoragesink.CamelGooglestoragesinkSinkConnector
```

The camel-google-storage-sink sink connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-storage-sink.bucketNameOrArn** | **Required** The Google Cloud Storage bucket name or Bucket Amazon Resource Name (ARN). |  | HIGH |
| **camel.kamelet.google-storage-sink.serviceAccountKey** | The service account key to use as credentials for Google Cloud Storage access. You must encode this value in base64. |  | MEDIUM |
| **camel.kamelet.google-storage-sink.autoCreateBucket** | Specifies to automatically create the Google Cloud Storage bucket. | false | MEDIUM |

The camel-google-storage-sink sink connector has no converters out of the box.

The camel-google-storage-sink sink connector has no transforms out of the box.

The camel-google-storage-sink sink connector has no aggregation strategies out of the box.