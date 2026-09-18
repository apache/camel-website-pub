# camel-ftps-source-kafka-connector source configuration

Connector Description: Receive data from an FTPS server.

When using camel-ftps-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ftps-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.ftpssource.CamelFtpssourceSourceConnector
```

The camel-ftps-source source connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ftps-source.connectionHost** | **Required** The hostname of the FTPS server. |  | HIGH |
| **camel.kamelet.ftps-source.connectionPort** | **Required** The port of the FTPS server. | "21" | HIGH |
| **camel.kamelet.ftps-source.username** | **Required** The username to access the FTPS server. |  | HIGH |
| **camel.kamelet.ftps-source.password** | **Required** The password to access the FTPS server. |  | HIGH |
| **camel.kamelet.ftps-source.directoryName** | **Required** The starting directory. |  | HIGH |
| **camel.kamelet.ftps-source.passiveMode** | Specifies to use passive mode connection. | false | MEDIUM |
| **camel.kamelet.ftps-source.recursive** | If a directory, look for files in all sub-directories as well. | false | MEDIUM |
| **camel.kamelet.ftps-source.idempotent** | Skip already-processed files. | true | MEDIUM |
| **camel.kamelet.ftps-source.binary** | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | false | MEDIUM |
| **camel.kamelet.ftps-source.autoCreate** | Automatically create starting directory. | true | MEDIUM |
| **camel.kamelet.ftps-source.delete** | If true, the file is deleted after it is processed successfully. | false | MEDIUM |

The camel-ftps-source source connector has no converters out of the box.

The camel-ftps-source source connector has no transforms out of the box.

The camel-ftps-source source connector has no aggregation strategies out of the box.