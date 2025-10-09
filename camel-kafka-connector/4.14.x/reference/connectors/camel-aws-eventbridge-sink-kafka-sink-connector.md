# camel-aws-eventbridge-sink-kafka-connector sink configuration

Connector Description: Send events to an Amazon Eventbridge Eventbus. In the headers, you can set the \`resources-arn\` / \`ce-resources-arn\` property to specify the ARN of resources related to the event. In the headers, you can set the \`detail-type\` / \`ce-detail-type\` property to specify the detail type related to the event. In the headers, you can set the \`event-source\` / \`ce-event-source\` property to specify the event source related to the event. If you do not set the property in the header, the Kamelet uses the given Kamelet properties as a default.

When using camel-aws-eventbridge-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-eventbridge-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awseventbridgesink.CamelAwseventbridgesinkSinkConnector
```

The camel-aws-eventbridge-sink sink connector supports 15 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-eventbridge-sink.eventbusNameOrArn** | **Required** The Eventbridge Eventbus name or Amazon Resource Name (ARN). |  | HIGH |
| **camel.kamelet.aws-eventbridge-sink.resourcesArn** | The ARN of resources related to the AWS event (e.g. `arn:aws:s3:eu-east-1:000000000001:test`). |  | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.eventSourcePrefix** | The event source prefix set for all events sent to the eventbus. | "" | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.eventSource** | The event source related to the AWS event (e.g. `aws.s3`). |  | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.detailType** | The event detail type related to the AWS event. |  | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-eventbridge-sink.useDefaultCredentialsProvider** | If true, the Eventbridge client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.useProfileCredentialsProvider** | Set whether the Eventbridge client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.useSessionCredentials** | Set whether the Eventbridge client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Eventbridge. | false | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-eventbridge-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-eventbridge-sink sink connector has no converters out of the box.

The camel-aws-eventbridge-sink sink connector has no transforms out of the box.

The camel-aws-eventbridge-sink sink connector has no aggregation strategies out of the box.