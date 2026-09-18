# camel-salesforce-delete-sink-kafka-connector sink configuration

Connector Description: Remove an object from Salesforce.

When using camel-salesforce-delete-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-salesforce-delete-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.salesforcedeletesink.CamelSalesforcedeletesinkSinkConnector
```

The camel-salesforce-delete-sink sink connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.salesforce-delete-sink.loginUrl** | The Salesforce instance login URL. | "https://login.salesforce.com" | MEDIUM |
| **camel.kamelet.salesforce-delete-sink.clientId** | **Required** The Salesforce application consumer key. |  | HIGH |
| **camel.kamelet.salesforce-delete-sink.clientSecret** | **Required** The Salesforce application consumer secret. |  | HIGH |
| **camel.kamelet.salesforce-delete-sink.userName** | **Required** The Salesforce username. |  | HIGH |
| **camel.kamelet.salesforce-delete-sink.password** | **Required** The Salesforce user password. |  | HIGH |

The camel-salesforce-delete-sink sink connector has no converters out of the box.

The camel-salesforce-delete-sink sink connector has no transforms out of the box.

The camel-salesforce-delete-sink sink connector has no aggregation strategies out of the box.