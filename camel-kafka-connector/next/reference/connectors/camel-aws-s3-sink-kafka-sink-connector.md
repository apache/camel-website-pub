# camel-aws-s3-sink-kafka-connector sink configuration

Connector Description: Upload data to an Amazon S3 Bucket.

When using camel-aws-s3-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-s3-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awss3sink.CamelAwss3sinkSinkConnector
```

The camel-aws-s3-sink sink connector supports 14 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-s3-sink.bucketNameOrArn** | **Required** The S3 Bucket name or Amazon Resource Name (ARN). |  | HIGH |
| **camel.kamelet.aws-s3-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-s3-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-s3-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-s3-sink.autoCreateBucket** | Specifies to automatically create the S3 bucket. | false | MEDIUM |
| **camel.kamelet.aws-s3-sink.useDefaultCredentialsProvider** | If true, the S3 client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-s3-sink.useProfileCredentialsProvider** | Set whether the S3 client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-s3-sink.useSessionCredentials** | Set whether the S3 client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in S3. | false | MEDIUM |
| **camel.kamelet.aws-s3-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-s3-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-s3-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-s3-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |
| **camel.kamelet.aws-s3-sink.forcePathStyle** | Forces path style when accessing AWS S3 buckets. | false | MEDIUM |
| **camel.kamelet.aws-s3-sink.keyName** | The key name for saving an element in the bucket. |  | MEDIUM |

The camel-aws-s3-sink sink connector has no converters out of the box.

The camel-aws-s3-sink sink connector has no transforms out of the box.

The camel-aws-s3-sink sink connector has no aggregation strategies out of the box.