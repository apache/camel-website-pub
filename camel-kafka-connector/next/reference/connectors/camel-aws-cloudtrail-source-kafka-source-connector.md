# camel-aws-cloudtrail-source-kafka-connector source configuration

Connector Description: Receive data from an AWS Cloudtrail.

When using camel-aws-cloudtrail-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-cloudtrail-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awscloudtrailsource.CamelAwscloudtrailsourceSourceConnector
```

The camel-aws-cloudtrail-source source connector supports 12 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-cloudtrail-source.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-cloudtrail-source.useDefaultCredentialsProvider** | If true, the Cloudtrail client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.useProfileCredentialsProvider** | Set whether the Cloudtrail client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.useSessionCredentials** | Set whether the CloudTrail client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in CloudTrail. | false | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.maxResults** | Maximum number of records that are fetched in each poll. | 1 | MEDIUM |
| **camel.kamelet.aws-cloudtrail-source.eventSource** | Specify an event source to select events. Example: secretsmanager.amazonaws.com. |  | MEDIUM |

The camel-aws-cloudtrail-source source connector has no converters out of the box.

The camel-aws-cloudtrail-source source connector has no transforms out of the box.

The camel-aws-cloudtrail-source source connector has no aggregation strategies out of the box.