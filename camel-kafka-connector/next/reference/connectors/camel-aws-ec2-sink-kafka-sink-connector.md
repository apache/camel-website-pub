# camel-aws-ec2-sink-kafka-connector sink configuration

Connector Description: Check the status of EC2 instances

When using camel-aws-ec2-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-ec2-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awsec2sink.CamelAwsec2sinkSinkConnector
```

The camel-aws-ec2-sink sink connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-ec2-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-ec2-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-ec2-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-ec2-sink.useDefaultCredentialsProvider** | If true, the EC2 client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-ec2-sink.useProfileCredentialsProvider** | Set whether the EC2 client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-ec2-sink.useSessionCredentials** | Set whether the EC2 client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in EC2. | false | MEDIUM |
| **camel.kamelet.aws-ec2-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-ec2-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-ec2-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-ec2-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-ec2-sink sink connector has no converters out of the box.

The camel-aws-ec2-sink sink connector has no transforms out of the box.

The camel-aws-ec2-sink sink connector has no aggregation strategies out of the box.