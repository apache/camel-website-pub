# camel-aws-s3-streaming-upload-sink-kafka-connector sink configuration

Connector Description: Upload data to AWS S3 in streaming upload mode.

When using camel-aws-s3-streaming-upload-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-s3-streaming-upload-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awss3streaminguploadsink.CamelAwss3streaminguploadsinkSinkConnector
```

The camel-aws-s3-streaming-upload-sink sink connector supports 19 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-s3-streaming-upload-sink.bucketNameOrArn** | **Required** The S3 Bucket name or Amazon Resource Name (ARN). |  | HIGH |
| **camel.kamelet.aws-s3-streaming-upload-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-s3-streaming-upload-sink.autoCreateBucket** | Setting the autocreation of the S3 bucket bucketName. | false | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.restartingPolicy** | The restarting policy to use in streaming upload mode. There are 2 enums and the value can be one of `override`, `lastPart`. | "lastPart" | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.batchMessageNumber** | The number of messages composing a batch in streaming upload mode. | 10 | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.batchSize** | The batch size (in bytes) in streaming upload mode. | 1000000 | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.streamingUploadTimeout** | While streaming upload mode is true, this option set the timeout to complete upload. |  | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.namingStrategy** | The naming strategy to use in streaming upload mode. There are 2 enums and the value can be one of progressive, random. | "progressive" | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.keyName** | **Required** Setting the key name for an element in the bucket through endpoint parameter. In Streaming Upload, with the default configuration, this is the base for the progressive creation of files. |  | HIGH |
| **camel.kamelet.aws-s3-streaming-upload-sink.useDefaultCredentialsProvider** | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.useProfileCredentialsProvider** | Set whether the S3 client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.useSessionCredentials** | Set whether the S3 client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in S3. | false | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |
| **camel.kamelet.aws-s3-streaming-upload-sink.forcePathStyle** | Forces path style when accessing AWS S3 buckets. | false | MEDIUM |

The camel-aws-s3-streaming-upload-sink sink connector has no converters out of the box.

The camel-aws-s3-streaming-upload-sink sink connector has no transforms out of the box.

The camel-aws-s3-streaming-upload-sink sink connector has no aggregation strategies out of the box.