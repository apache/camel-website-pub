# camel-minio-source-kafka-connector source configuration

Connector Description: Receive data from MinIO.

When using camel-minio-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-minio-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.miniosource.CamelMiniosourceSourceConnector
```

The camel-minio-source source connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.minio-source.bucketName** | **Required** The MinIO Bucket name. |  | HIGH |
| **camel.kamelet.minio-source.deleteAfterRead** | Delete objects after consuming them. | true | MEDIUM |
| **camel.kamelet.minio-source.accessKey** | **Required** The access key obtained from MinIO. |  | HIGH |
| **camel.kamelet.minio-source.secretKey** | **Required** The secret key obtained from MinIO. |  | HIGH |
| **camel.kamelet.minio-source.endpoint** | **Required** The MinIO Endpoint. You can specify an URL, domain name, IPv4 address, or IPv6 address. Example: [http://localhost:9000](http://localhost:9000). |  | HIGH |
| **camel.kamelet.minio-source.autoCreateBucket** | Specifies to automatically create the MinIO bucket. | false | MEDIUM |

The camel-minio-source source connector has no converters out of the box.

The camel-minio-source source connector has no transforms out of the box.

The camel-minio-source source connector has no aggregation strategies out of the box.