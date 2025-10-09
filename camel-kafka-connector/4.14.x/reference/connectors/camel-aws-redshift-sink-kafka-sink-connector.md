# camel-aws-redshift-sink-kafka-connector sink configuration

Connector Description: Send data to an AWS Redshift Database. This Kamelet expects a JSON-formatted body. Use key:value pairs to map the JSON fields and parameters.

When using camel-aws-redshift-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-redshift-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awsredshiftsink.CamelAwsredshiftsinkSinkConnector
```

The camel-aws-redshift-sink sink connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-redshift-sink.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.aws-redshift-sink.serverPort** | The server port for the AWS RedShi data source. | "5439" | MEDIUM |
| **camel.kamelet.aws-redshift-sink.username** | **Required** The username to access a secured AWS Redshift Database. |  | HIGH |
| **camel.kamelet.aws-redshift-sink.password** | **Required** The password to access a secured AWS Redshift Database. |  | HIGH |
| **camel.kamelet.aws-redshift-sink.query** | **Required** The query to execute against the AWS Redshift Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.aws-redshift-sink.databaseName** | **Required** The name of the AWS RedShift Database. |  | HIGH |

The camel-aws-redshift-sink sink connector has no converters out of the box.

The camel-aws-redshift-sink sink connector has no transforms out of the box.

The camel-aws-redshift-sink sink connector has no aggregation strategies out of the box.