# camel-google-storage-source-kafka-connector source configuration

Connector Description: Consume objects from Google Cloud Storage.

When using camel-google-storage-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-storage-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlestoragesource.CamelGooglestoragesourceSourceConnector
```

The camel-google-storage-source source connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-storage-source.bucketNameOrArn** | **Required** The Google Cloud Storage bucket name or Bucket Amazon Resource Name (ARN). |  | HIGH |
| **camel.kamelet.google-storage-source.serviceAccountKey** | The service account key to use as credentials for Google Cloud Storage access. You must encode this value in base64. |  | MEDIUM |
| **camel.kamelet.google-storage-source.deleteAfterRead** | Specifies to delete objects after consuming them. | true | MEDIUM |
| **camel.kamelet.google-storage-source.autoCreateBucket** | Specifies to automatically create the Google Cloud Storage bucket. | false | MEDIUM |
| **camel.kamelet.google-storage-source.prefix** | The prefix which is used in the BlobListOptions to only consume objects we are interested in. |  | MEDIUM |
| **camel.kamelet.google-storage-source.filter** | A regular expression to include only blobs with name matching it. |  | MEDIUM |

The camel-google-storage-source source connector has no converters out of the box.

The camel-google-storage-source source connector has no transforms out of the box.

The camel-google-storage-source source connector has no aggregation strategies out of the box.