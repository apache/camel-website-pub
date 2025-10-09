# camel-salesforce-composite-upsert-sink-kafka-connector sink configuration

Connector Description: Upsert Composite List of sObjects in Salesforce.

When using camel-salesforce-composite-upsert-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-salesforce-composite-upsert-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.salesforcecompositeupsertsink.CamelSalesforcecompositeupsertsinkSinkConnector
```

The camel-salesforce-composite-upsert-sink sink connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.salesforce-composite-upsert-sink.sObjectName** | **Required** The type of the Salesforce object. Required if using a key-value pair. Example: Contact. |  | HIGH |
| **camel.kamelet.salesforce-composite-upsert-sink.sObjectIdName** | **Required** The Field Name of the External ID of the Salesforce object. Required if using a key-value pair. |  | HIGH |
| **camel.kamelet.salesforce-composite-upsert-sink.loginUrl** | The Salesforce instance login URL. | "https://login.salesforce.com" | MEDIUM |
| **camel.kamelet.salesforce-composite-upsert-sink.clientId** | **Required** The Salesforce application consumer key. |  | HIGH |
| **camel.kamelet.salesforce-composite-upsert-sink.clientSecret** | **Required** The Salesforce application consumer secret. |  | HIGH |
| **camel.kamelet.salesforce-composite-upsert-sink.userName** | **Required** The Salesforce username. |  | HIGH |
| **camel.kamelet.salesforce-composite-upsert-sink.password** | **Required** The Salesforce user password. |  | HIGH |

The camel-salesforce-composite-upsert-sink sink connector has no converters out of the box.

The camel-salesforce-composite-upsert-sink sink connector has no transforms out of the box.

The camel-salesforce-composite-upsert-sink sink connector has no aggregation strategies out of the box.