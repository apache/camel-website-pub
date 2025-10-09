# camel-ftp-sink-kafka-connector sink configuration

Connector Description: Send data to an FTP server.

When using camel-ftp-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ftp-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.ftpsink.CamelFtpsinkSinkConnector
```

The camel-ftp-sink sink connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ftp-sink.connectionHost** | **Required** The hostname of the FTP server. |  | HIGH |
| **camel.kamelet.ftp-sink.connectionPort** | **Required** The port of the FTP server. | "21" | HIGH |
| **camel.kamelet.ftp-sink.username** | **Required** The username to access the FTP server. |  | HIGH |
| **camel.kamelet.ftp-sink.password** | **Required** The password to access the FTP server. |  | HIGH |
| **camel.kamelet.ftp-sink.directoryName** | **Required** The starting directory. |  | HIGH |
| **camel.kamelet.ftp-sink.passiveMode** | Specifies to use passive mode connection. | false | MEDIUM |
| **camel.kamelet.ftp-sink.fileExist** | How to behave in case of file already existent. | "Override" | MEDIUM |
| **camel.kamelet.ftp-sink.binary** | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | false | MEDIUM |
| **camel.kamelet.ftp-sink.autoCreate** | Automatically create the directory the files should be written to. | true | MEDIUM |

The camel-ftp-sink sink connector has no converters out of the box.

The camel-ftp-sink sink connector has no transforms out of the box.

The camel-ftp-sink sink connector has no aggregation strategies out of the box.