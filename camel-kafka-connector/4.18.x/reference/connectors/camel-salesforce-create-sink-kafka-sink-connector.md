# camel-salesforce-create-sink-kafka-connector sink configuration

Connector Description: Create an object in Salesforce.

When using camel-salesforce-create-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-salesforce-create-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.salesforcecreatesink.CamelSalesforcecreatesinkSinkConnector
```

The camel-salesforce-create-sink sink connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.salesforce-create-sink.sObjectName** | The type of the object. Example: Contact. |  | MEDIUM |
| **camel.kamelet.salesforce-create-sink.loginUrl** | The Salesforce instance login URL. | "https://login.salesforce.com" | MEDIUM |
| **camel.kamelet.salesforce-create-sink.clientId** | **Required** The Salesforce application consumer key. |  | HIGH |
| **camel.kamelet.salesforce-create-sink.clientSecret** | **Required** The Salesforce application consumer secret. |  | HIGH |
| **camel.kamelet.salesforce-create-sink.userName** | **Required** The Salesforce username. |  | HIGH |
| **camel.kamelet.salesforce-create-sink.password** | **Required** The Salesforce user password. |  | HIGH |

The camel-salesforce-create-sink sink connector has no converters out of the box.

The camel-salesforce-create-sink sink connector has no transforms out of the box.

The camel-salesforce-create-sink sink connector has no aggregation strategies out of the box.