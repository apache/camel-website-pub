# camel-aws-redshift-source-kafka-connector source configuration

Connector Description: Query data from an AWS RedShift Database.

When using camel-aws-redshift-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-redshift-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awsredshiftsource.CamelAwsredshiftsourceSourceConnector
```

The camel-aws-redshift-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-redshift-source.serverName** | **Required** The server name for the data source. Example: localhost. |  | HIGH |
| **camel.kamelet.aws-redshift-source.serverPort** | The server port for the data source. | "5439" | MEDIUM |
| **camel.kamelet.aws-redshift-source.username** | **Required** The username to access a secured AWS RedShift Database. |  | HIGH |
| **camel.kamelet.aws-redshift-source.password** | **Required** The password to access a secured AWS RedShift Database. |  | HIGH |
| **camel.kamelet.aws-redshift-source.query** | **Required** The query to execute against the AWS RedShift Database. Example: INSERT INTO accounts (username,city) VALUES (:#username,:#city). |  | HIGH |
| **camel.kamelet.aws-redshift-source.databaseName** | **Required** The name of the AWS RedShift Database. |  | HIGH |
| **camel.kamelet.aws-redshift-source.consumedQuery** | A query to run on a tuple consumed. Example: DELETE FROM accounts where user\_id = :#user\_id. |  | MEDIUM |
| **camel.kamelet.aws-redshift-source.delay** | The number of milliseconds before the next poll from the AWS RedShift database. | 500 | MEDIUM |

The camel-aws-redshift-source source connector has no converters out of the box.

The camel-aws-redshift-source source connector has no transforms out of the box.

The camel-aws-redshift-source source connector has no aggregation strategies out of the box.