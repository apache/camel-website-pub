# camel-minio-sink-kafka-connector sink configuration

Connector Description: Upload data to MinIO.

When using camel-minio-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-minio-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.miniosink.CamelMiniosinkSinkConnector
```

The camel-minio-sink sink connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.minio-sink.bucketName** | **Required** The Minio Bucket name. |  | HIGH |
| **camel.kamelet.minio-sink.accessKey** | **Required** The access key obtained from MinIO. |  | HIGH |
| **camel.kamelet.minio-sink.secretKey** | **Required** The secret key obtained from MinIO. |  | HIGH |
| **camel.kamelet.minio-sink.endpoint** | **Required** The MinIO Endpoint. You can specify an URL, domain name, IPv4 address, or IPv6 address. Example: [http://localhost:9000](http://localhost:9000). |  | HIGH |
| **camel.kamelet.minio-sink.autoCreateBucket** | Specify to automatically create the MinIO bucket. | false | MEDIUM |
| **camel.kamelet.minio-sink.keyName** | The key name for saving an element in the bucket. |  | MEDIUM |

The camel-minio-sink sink connector has no converters out of the box.

The camel-minio-sink sink connector has no transforms out of the box.

The camel-minio-sink sink connector has no aggregation strategies out of the box.