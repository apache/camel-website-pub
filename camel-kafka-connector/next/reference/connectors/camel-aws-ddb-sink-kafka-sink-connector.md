# camel-aws-ddb-sink-kafka-connector sink configuration

Connector Description: Send data to Amazon DynamoDB. The sent data inserts, updates, or deletes an item on the specified AWS DynamoDB table.

When using camel-aws-ddb-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-ddb-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awsddbsink.CamelAwsddbsinkSinkConnector
```

The camel-aws-ddb-sink sink connector supports 12 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-ddb-sink.table** | **Required** The name of the DynamoDB table. |  | HIGH |
| **camel.kamelet.aws-ddb-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-ddb-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-ddb-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-ddb-sink.operation** | The operation to perform. Example: PutItem. | "PutItem" | MEDIUM |
| **camel.kamelet.aws-ddb-sink.useDefaultCredentialsProvider** | If true, the DynamoDB client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-ddb-sink.useProfileCredentialsProvider** | Set whether the DynamoDB client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-ddb-sink.useSessionCredentials** | Set whether the DynamoDB client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in DynamoDB. | false | MEDIUM |
| **camel.kamelet.aws-ddb-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-ddb-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-ddb-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-ddb-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-ddb-sink sink connector has no converters out of the box.

The camel-aws-ddb-sink sink connector has no transforms out of the box.

The camel-aws-ddb-sink sink connector has no aggregation strategies out of the box.