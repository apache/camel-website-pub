# camel-file-watch-source-kafka-connector source configuration

Connector Description: Receive events related to a file or folder. It may require a volume mounting on Kubernetes.

When using camel-file-watch-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-file-watch-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.filewatchsource.CamelFilewatchsourceSourceConnector
```

The camel-file-watch-source source connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.file-watch-source.filePath** | **Required** Path of file or folder to watch. |  | HIGH |
| **camel.kamelet.file-watch-source.events** | **Required** The type of events to consume. | "CREATE,MODIFY,DELETE" | HIGH |

The camel-file-watch-source source connector has no converters out of the box.

The camel-file-watch-source source connector has no transforms out of the box.

The camel-file-watch-source source connector has no aggregation strategies out of the box.