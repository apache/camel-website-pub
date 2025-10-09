# camel-aws-s3-event-based-source-kafka-connector source configuration

Connector Description: Receive data from AWS SQS subscribed to Eventbridge Bus reporting events related to an S3 bucket or multiple buckets.

When using camel-aws-s3-event-based-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-s3-event-based-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awss3eventbasedsource.CamelAwss3eventbasedsourceSourceConnector
```

The camel-aws-s3-event-based-source source connector supports 14 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-s3-event-based-source.queueNameOrArn** | **Required** The SQS Queue Name or ARN. |  | HIGH |
| **camel.kamelet.aws-s3-event-based-source.deleteAfterRead** | Delete messages after consuming them. | true | MEDIUM |
| **camel.kamelet.aws-s3-event-based-source.accessKey** | **Required** The access key obtained from AWS. |  | HIGH |
| **camel.kamelet.aws-s3-event-based-source.secretKey** | **Required** The secret key obtained from AWS. |  | HIGH |
| **camel.kamelet.aws-s3-event-based-source.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-s3-event-based-source.autoCreateQueue** | Setting the autocreation of the SQS queue. | false | MEDIUM |
| **camel.kamelet.aws-s3-event-based-source.amazonAWSHost** | The hostname of the Amazon AWS cloud. | "amazonaws.com" | MEDIUM |
| **camel.kamelet.aws-s3-event-based-source.protocol** | The underlying protocol used to communicate with SQS Example: http or https. | "https" | MEDIUM |
| **camel.kamelet.aws-s3-event-based-source.queueURL** | The full SQS Queue URL (required if using KEDA). |  | MEDIUM |
| **camel.kamelet.aws-s3-event-based-source.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-s3-event-based-source.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |
| **camel.kamelet.aws-s3-event-based-source.delay** | The number of milliseconds before the next poll of the selected stream. | 500 | MEDIUM |
| **camel.kamelet.aws-s3-event-based-source.greedy** | If greedy is enabled, then the polling will happen immediately again, if the previous run polled 1 or more messages. | false | MEDIUM |
| **camel.kamelet.aws-s3-event-based-source.getObject** | If `getObject` is enabled, then the file created in the bucket is retrieved and returned as body. If not, only the event will returned as body. | false | MEDIUM |

The camel-aws-s3-event-based-source source connector has no converters out of the box.

The camel-aws-s3-event-based-source source connector has no transforms out of the box.

The camel-aws-s3-event-based-source source connector has no aggregation strategies out of the box.