# camel-ibm-cos-sink-kafka-connector sink configuration

Connector Description: Upload data to an IBM Cloud Object Storage Bucket.

When using camel-ibm-cos-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ibm-cos-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.ibmcossink.CamelIbmcossinkSinkConnector
```

The camel-ibm-cos-sink sink connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ibm-cos-sink.bucketName** | **Required** The IBM COS Bucket name. |  | HIGH |
| **camel.kamelet.ibm-cos-sink.apiKey** | **Required** IBM Cloud API Key for authentication. |  | HIGH |
| **camel.kamelet.ibm-cos-sink.serviceInstanceId** | **Required** IBM COS Service Instance ID (CRN). |  | HIGH |
| **camel.kamelet.ibm-cos-sink.endpointUrl** | **Required** IBM COS Endpoint URL (e.g., [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)). Example: [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud). |  | HIGH |
| **camel.kamelet.ibm-cos-sink.location** | IBM COS Location/Region (e.g., us-south, eu-gb). Example: us-south. |  | MEDIUM |
| **camel.kamelet.ibm-cos-sink.autoCreateBucket** | Specifies to automatically create the IBM COS bucket. | false | MEDIUM |
| **camel.kamelet.ibm-cos-sink.keyName** | The key name for saving an element in the bucket. |  | MEDIUM |
| **camel.kamelet.ibm-cos-sink.multiPartUpload** | Use multi-part upload for large files. | false | MEDIUM |
| **camel.kamelet.ibm-cos-sink.partSize** | Part size for multi-part uploads (default 25MB). | 26214400 | MEDIUM |
| **camel.kamelet.ibm-cos-sink.storageClass** | The storage class to use when storing objects (e.g., STANDARD, VAULT, COLD, FLEX). |  | MEDIUM |

The camel-ibm-cos-sink sink connector has no converters out of the box.

The camel-ibm-cos-sink sink connector has no transforms out of the box.

The camel-ibm-cos-sink sink connector has no aggregation strategies out of the box.