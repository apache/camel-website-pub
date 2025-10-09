# camel-aws-s3-source-kafka-connector source configuration

Connector Description: Receive data from an Amazon S3 Bucket.

When using camel-aws-s3-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-s3-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awss3source.CamelAwss3sourceSourceConnector
```

The camel-aws-s3-source source connector supports 22 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-s3-source.bucketNameOrArn** | **Required** The S3 Bucket name or Amazon Resource Name (ARN). |  | HIGH |
| **camel.kamelet.aws-s3-source.deleteAfterRead** | Specifies to delete objects after consuming them. | true | MEDIUM |
| **camel.kamelet.aws-s3-source.moveAfterRead** | Move objects from S3 bucket to a different bucket after they have been retrieved. | false | MEDIUM |
| **camel.kamelet.aws-s3-source.destinationBucket** | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | MEDIUM |
| **camel.kamelet.aws-s3-source.destinationBucketPrefix** | Define the destination bucket prefix to use when an object must be moved, and moveAfterRead is set to true. |  | MEDIUM |
| **camel.kamelet.aws-s3-source.destinationBucketSuffix** | Define the destination bucket suffix to use when an object must be moved, and moveAfterRead is set to true. |  | MEDIUM |
| **camel.kamelet.aws-s3-source.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-s3-source.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-s3-source.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-s3-source.autoCreateBucket** | Specifies to automatically create the S3 bucket. | false | MEDIUM |
| **camel.kamelet.aws-s3-source.prefix** | The AWS S3 bucket prefix to consider while searching. Example: folder/. |  | MEDIUM |
| **camel.kamelet.aws-s3-source.ignoreBody** | If true, the S3 Object body is ignored. Setting this to true overrides any behavior defined by the `includeBody` option. If false, the S3 object is put in the body. | false | MEDIUM |
| **camel.kamelet.aws-s3-source.useDefaultCredentialsProvider** | If true, the S3 client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-s3-source.useProfileCredentialsProvider** | Set whether the S3 client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-s3-source.useSessionCredentials** | Set whether the S3 client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in S3. | false | MEDIUM |
| **camel.kamelet.aws-s3-source.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-s3-source.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-s3-source.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-s3-source.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |
| **camel.kamelet.aws-s3-source.forcePathStyle** | Forces path style when accessing AWS S3 buckets. | false | MEDIUM |
| **camel.kamelet.aws-s3-source.delay** | The number of milliseconds before the next poll of the selected bucket. | 500 | MEDIUM |
| **camel.kamelet.aws-s3-source.maxMessagesPerPoll** | Gets the maximum number of messages as a limit to poll at each polling. Gets the maximum number of messages as a limit to poll at each polling. The default value is 10. Use 0 or a negative number to set it as unlimited. | 10 | MEDIUM |

The camel-aws-s3-source source connector has no converters out of the box.

The camel-aws-s3-source source connector has no transforms out of the box.

The camel-aws-s3-source source connector has no aggregation strategies out of the box.