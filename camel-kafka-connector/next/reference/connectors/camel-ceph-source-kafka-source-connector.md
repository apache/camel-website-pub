# camel-ceph-source-kafka-connector source configuration

Connector Description: Receive data from an Ceph Bucket, managed by a Object Storage Gateway.

When using camel-ceph-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ceph-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.cephsource.CamelCephsourceSourceConnector
```

The camel-ceph-source source connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ceph-source.bucketName** | **Required** The Ceph Bucket name. |  | HIGH |
| **camel.kamelet.ceph-source.deleteAfterRead** | Specifies to delete objects after consuming them. | true | MEDIUM |
| **camel.kamelet.ceph-source.accessKey** | **Required** The access key. |  | HIGH |
| **camel.kamelet.ceph-source.secretKey** | **Required** The secret key. |  | HIGH |
| **camel.kamelet.ceph-source.zoneGroup** | **Required** The bucket zone group. |  | HIGH |
| **camel.kamelet.ceph-source.autoCreateBucket** | Specifies to automatically create the bucket. | false | MEDIUM |
| **camel.kamelet.ceph-source.includeBody** | If true, the exchange is consumed and put into the body and closed. If false, the Object stream is put raw into the body and the headers are set with the object metadata. | true | MEDIUM |
| **camel.kamelet.ceph-source.prefix** | The bucket prefix to consider while searching. Example: folder/. |  | MEDIUM |
| **camel.kamelet.ceph-source.ignoreBody** | If true, the Object body is ignored. Setting this to true overrides any behavior defined by the `includeBody` option. If false, the object is put in the body. | false | MEDIUM |
| **camel.kamelet.ceph-source.cephUrl** | **Required** Set the Ceph Object Storage Address Url. Example: [http://ceph-storage-address.com](http://ceph-storage-address.com). |  | HIGH |
| **camel.kamelet.ceph-source.delay** | The number of milliseconds before the next poll of the selected bucket. | 500 | MEDIUM |

The camel-ceph-source source connector has no converters out of the box.

The camel-ceph-source source connector has no transforms out of the box.

The camel-ceph-source source connector has no aggregation strategies out of the box.