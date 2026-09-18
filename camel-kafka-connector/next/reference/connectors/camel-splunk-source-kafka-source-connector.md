# camel-splunk-source-kafka-connector source configuration

Connector Description: Retrieve data from Splunk and outputs in json format.

When using camel-splunk-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-splunk-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.splunksource.CamelSplunksourceSourceConnector
```

The camel-splunk-source source connector supports 17 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.splunk-source.serverHostname** | **Required** The address of your Splunk server. Example: my\_server\_splunk.com. |  | HIGH |
| **camel.kamelet.splunk-source.serverPort** | The address of your Splunk server. | 8089 | MEDIUM |
| **camel.kamelet.splunk-source.username** | **Required** The username to authenticate to Splunk Server. |  | HIGH |
| **camel.kamelet.splunk-source.password** | **Required** The password to authenticate to Splunk Server. |  | HIGH |
| **camel.kamelet.splunk-source.index** | Splunk index to write to. |  | MEDIUM |
| **camel.kamelet.splunk-source.protocol** | Connection Protocol to Splunk server. | "https" | MEDIUM |
| **camel.kamelet.splunk-source.source** | The source named field of the data. |  | MEDIUM |
| **camel.kamelet.splunk-source.sourceType** | The source named field of the data. |  | MEDIUM |
| **camel.kamelet.splunk-source.app** | The app name in Splunk. |  | MEDIUM |
| **camel.kamelet.splunk-source.connectionTimeout** | Timeout in milliseconds when connecting to Splunk server. |  | MEDIUM |
| **camel.kamelet.splunk-source.count** | The maximum number of entities to return. |  | MEDIUM |
| **camel.kamelet.splunk-source.repeat** | The maximum number of fires. |  | MEDIUM |
| **camel.kamelet.splunk-source.delay** | The number of milliseconds before the next poll. |  | MEDIUM |
| **camel.kamelet.splunk-source.query** | **Required** The Splunk query to run. |  | HIGH |
| **camel.kamelet.splunk-source.earliestTime** | Earliest time of the search time window. Example: 05/17/22 08:35:46:456. |  | MEDIUM |
| **camel.kamelet.splunk-source.initEarliestTime** | **Required** Initial start offset of the first search. Example: 05/17/22 08:35:46:456. |  | HIGH |
| **camel.kamelet.splunk-source.latestTime** | Latest time of the search time window. Example: 05/17/22 08:35:46:456. |  | MEDIUM |

The camel-splunk-source source connector has no converters out of the box.

The camel-splunk-source source connector has no transforms out of the box.

The camel-splunk-source source connector has no aggregation strategies out of the box.