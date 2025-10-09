# camel-aws-ddb-streams-source-kafka-connector source configuration

Connector Description: Receive events from Amazon DynamoDB Streams.

When using camel-aws-ddb-streams-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-ddb-streams-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awsddbstreamssource.CamelAwsddbstreamssourceSourceConnector
```

The camel-aws-ddb-streams-source source connector supports 13 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-ddb-streams-source.table** | **Required** The name of the DynamoDB table. |  | HIGH |
| **camel.kamelet.aws-ddb-streams-source.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-ddb-streams-source.streamIteratorType** | Defines where in the DynamoDB stream to start getting records. There are two enums and the value can be one of FROM\_LATEST and FROM\_START. Note that using FROM\_START can cause a significant delay before the stream has caught up to real-time. | "FROM\_LATEST" | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.useDefaultCredentialsProvider** | If `true`, the DynamoDB client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.useProfileCredentialsProvider** | Set whether the DynamoDB client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.useSessionCredentials** | Set whether the DynamoDB client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in DynamoDB. | false | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |
| **camel.kamelet.aws-ddb-streams-source.delay** | The number of milliseconds before the next poll from the database. | 500 | MEDIUM |

The camel-aws-ddb-streams-source source connector has no converters out of the box.

The camel-aws-ddb-streams-source source connector has no transforms out of the box.

The camel-aws-ddb-streams-source source connector has no aggregation strategies out of the box.