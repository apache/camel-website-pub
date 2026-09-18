# camel-ibm-cos-source-kafka-connector source configuration

Connector Description: Receive data from an IBM Cloud Object Storage Bucket.

When using camel-ibm-cos-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ibm-cos-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.ibmcossource.CamelIbmcossourceSourceConnector
```

The camel-ibm-cos-source source connector supports 17 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ibm-cos-source.bucketName** | **Required** The IBM COS Bucket name. |  | HIGH |
| **camel.kamelet.ibm-cos-source.apiKey** | **Required** IBM Cloud API Key for authentication. |  | HIGH |
| **camel.kamelet.ibm-cos-source.serviceInstanceId** | **Required** IBM COS Service Instance ID (CRN). |  | HIGH |
| **camel.kamelet.ibm-cos-source.endpointUrl** | **Required** IBM COS Endpoint URL (e.g., [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)). Example: [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud). |  | HIGH |
| **camel.kamelet.ibm-cos-source.location** | IBM COS Location/Region (e.g., us-south, eu-gb). Example: us-south. |  | MEDIUM |
| **camel.kamelet.ibm-cos-source.deleteAfterRead** | Specifies to delete objects after consuming them. | true | MEDIUM |
| **camel.kamelet.ibm-cos-source.moveAfterRead** | Move objects from IBM COS bucket to a different bucket after they have been retrieved. | false | MEDIUM |
| **camel.kamelet.ibm-cos-source.destinationBucket** | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | MEDIUM |
| **camel.kamelet.ibm-cos-source.destinationBucketPrefix** | Define the destination bucket prefix to use when an object must be moved, and moveAfterRead is set to true. |  | MEDIUM |
| **camel.kamelet.ibm-cos-source.destinationBucketSuffix** | Define the destination bucket suffix to use when an object must be moved, and moveAfterRead is set to true. |  | MEDIUM |
| **camel.kamelet.ibm-cos-source.autoCreateBucket** | Specifies to automatically create the IBM COS bucket. | false | MEDIUM |
| **camel.kamelet.ibm-cos-source.prefix** | The IBM COS bucket prefix to consider while searching. Example: folder/. |  | MEDIUM |
| **camel.kamelet.ibm-cos-source.delimiter** | The delimiter to use for listing objects. |  | MEDIUM |
| **camel.kamelet.ibm-cos-source.includeBody** | If true, the object body is included in the exchange. If false, only headers are set. | true | MEDIUM |
| **camel.kamelet.ibm-cos-source.includeFolders** | Include folders/directories when listing objects. | true | MEDIUM |
| **camel.kamelet.ibm-cos-source.delay** | The number of milliseconds before the next poll of the selected bucket. | 500 | MEDIUM |
| **camel.kamelet.ibm-cos-source.maxMessagesPerPoll** | Gets the maximum number of messages as a limit to poll at each polling. The default value is 10. Use 0 or a negative number to set it as unlimited. | 10 | MEDIUM |

The camel-ibm-cos-source source connector has no converters out of the box.

The camel-ibm-cos-source source connector has no transforms out of the box.

The camel-ibm-cos-source source connector has no aggregation strategies out of the box.