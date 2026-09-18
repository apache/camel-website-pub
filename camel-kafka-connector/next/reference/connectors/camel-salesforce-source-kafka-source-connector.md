# camel-salesforce-source-kafka-connector source configuration

Connector Description: Receive updates from Salesforce.

When using camel-salesforce-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-salesforce-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.salesforcesource.CamelSalesforcesourceSourceConnector
```

The camel-salesforce-source source connector supports 15 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.salesforce-source.query** | **Required** The query to execute on Salesforce. Example: SELECT Id, Name, Email, Phone FROM Contact. |  | HIGH |
| **camel.kamelet.salesforce-source.topicName** | **Required** The name of the topic or channel. Example: ContactTopic. |  | HIGH |
| **camel.kamelet.salesforce-source.loginUrl** | The Salesforce instance login URL. | "https://login.salesforce.com" | MEDIUM |
| **camel.kamelet.salesforce-source.notifyForFields** | Notify for fields. | "ALL" | MEDIUM |
| **camel.kamelet.salesforce-source.clientId** | **Required** The Salesforce application consumer key. |  | HIGH |
| **camel.kamelet.salesforce-source.clientSecret** | **Required** The Salesforce application consumer secret. |  | HIGH |
| **camel.kamelet.salesforce-source.userName** | **Required** The Salesforce username. |  | HIGH |
| **camel.kamelet.salesforce-source.password** | **Required** The Salesforce user password. |  | HIGH |
| **camel.kamelet.salesforce-source.notifyForOperationCreate** | Notify for create operation. | true | MEDIUM |
| **camel.kamelet.salesforce-source.notifyForOperationUpdate** | Notify for update operation. | false | MEDIUM |
| **camel.kamelet.salesforce-source.notifyForOperationDelete** | Notify for delete operation. | false | MEDIUM |
| **camel.kamelet.salesforce-source.notifyForOperationUndelete** | Notify for undelete operation. | false | MEDIUM |
| **camel.kamelet.salesforce-source.operation** | The operation to use. | "subscribe" | MEDIUM |
| **camel.kamelet.salesforce-source.rawPayload** | Use raw payload String for request and response (either JSON or XML depending on format), instead of DTOs, false by default. | false | MEDIUM |
| **camel.kamelet.salesforce-source.replayId** | The replayId value to use when subscribing to the Streaming API. |  | MEDIUM |

The camel-salesforce-source source connector has no converters out of the box.

The camel-salesforce-source source connector has no transforms out of the box.

The camel-salesforce-source source connector has no aggregation strategies out of the box.