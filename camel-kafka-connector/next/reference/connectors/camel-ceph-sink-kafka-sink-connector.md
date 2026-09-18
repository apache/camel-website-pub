# camel-ceph-sink-kafka-connector sink configuration

Connector Description: Upload data to an Ceph Bucket managed by a Object Storage Gateway.

When using camel-ceph-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ceph-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.cephsink.CamelCephsinkSinkConnector
```

The camel-ceph-sink sink connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ceph-sink.bucketName** | **Required** The Ceph Bucket name. |  | HIGH |
| **camel.kamelet.ceph-sink.accessKey** | **Required** The access key. |  | HIGH |
| **camel.kamelet.ceph-sink.secretKey** | **Required** The secret key. |  | HIGH |
| **camel.kamelet.ceph-sink.zoneGroup** | **Required** The bucket zone group. |  | HIGH |
| **camel.kamelet.ceph-sink.autoCreateBucket** | Specifies to automatically create the bucket. | false | MEDIUM |
| **camel.kamelet.ceph-sink.cephUrl** | **Required** Set the Ceph Object Storage Address Url. Example: [http://ceph-storage-address.com](http://ceph-storage-address.com). |  | HIGH |
| **camel.kamelet.ceph-sink.keyName** | The key name for saving an element in the bucket. |  | MEDIUM |

The camel-ceph-sink sink connector has no converters out of the box.

The camel-ceph-sink sink connector has no transforms out of the box.

The camel-ceph-sink sink connector has no aggregation strategies out of the box.