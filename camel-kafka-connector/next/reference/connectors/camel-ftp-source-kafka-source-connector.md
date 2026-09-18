# camel-ftp-source-kafka-connector source configuration

Connector Description: Receive data from an FTP server.

When using camel-ftp-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ftp-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.ftpsource.CamelFtpsourceSourceConnector
```

The camel-ftp-source source connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ftp-source.connectionHost** | **Required** The hostname of the FTP server. |  | HIGH |
| **camel.kamelet.ftp-source.connectionPort** | **Required** The port of the FTP server. | "21" | HIGH |
| **camel.kamelet.ftp-source.username** | **Required** The username to access the FTP server. |  | HIGH |
| **camel.kamelet.ftp-source.password** | **Required** The password to access the FTP server. |  | HIGH |
| **camel.kamelet.ftp-source.directoryName** | **Required** The starting directory. |  | HIGH |
| **camel.kamelet.ftp-source.passiveMode** | Specifes to use passive mode connection. | false | MEDIUM |
| **camel.kamelet.ftp-source.recursive** | If a directory, look for files in all the sub-directories as well. | false | MEDIUM |
| **camel.kamelet.ftp-source.idempotent** | Skip already-processed files. | true | MEDIUM |
| **camel.kamelet.ftp-source.binary** | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | false | MEDIUM |
| **camel.kamelet.ftp-source.autoCreate** | Automatically create starting directory. | true | MEDIUM |
| **camel.kamelet.ftp-source.delete** | If true, the file is deleted after it is processed successfully. | false | MEDIUM |

The camel-ftp-source source connector has no converters out of the box.

The camel-ftp-source source connector has no transforms out of the box.

The camel-ftp-source source connector has no aggregation strategies out of the box.