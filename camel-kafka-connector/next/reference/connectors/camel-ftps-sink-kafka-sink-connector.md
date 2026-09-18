# camel-ftps-sink-kafka-connector sink configuration

Connector Description: Send data to an FTPS server.

When using camel-ftps-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ftps-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.ftpssink.CamelFtpssinkSinkConnector
```

The camel-ftps-sink sink connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ftps-sink.connectionHost** | **Required** The hostname of the FTP server. |  | HIGH |
| **camel.kamelet.ftps-sink.connectionPort** | **Required** The port of the FTP server. | "21" | HIGH |
| **camel.kamelet.ftps-sink.username** | **Required** The username to access the FTP server. |  | HIGH |
| **camel.kamelet.ftps-sink.password** | **Required** The password to access the FTP server. |  | HIGH |
| **camel.kamelet.ftps-sink.directoryName** | **Required** The starting directory. |  | HIGH |
| **camel.kamelet.ftps-sink.passiveMode** | Set the passive mode connection. | false | MEDIUM |
| **camel.kamelet.ftps-sink.fileExist** | Specifies how the Kamelet behaves if the file already exists. | "Override" | MEDIUM |
| **camel.kamelet.ftps-sink.binary** | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | false | MEDIUM |
| **camel.kamelet.ftps-sink.autoCreate** | Automatically create the directory the files should be written to. | true | MEDIUM |

The camel-ftps-sink sink connector has no converters out of the box.

The camel-ftps-sink sink connector has no transforms out of the box.

The camel-ftps-sink sink connector has no aggregation strategies out of the box.