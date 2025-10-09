# camel-sftp-sink-kafka-connector sink configuration

Connector Description: Send data to an SFTP Server.

When using camel-sftp-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-sftp-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.sftpsink.CamelSftpsinkSinkConnector
```

The camel-sftp-sink sink connector supports 14 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.sftp-sink.connectionHost** | **Required** The hostname of the FTP server. |  | HIGH |
| **camel.kamelet.sftp-sink.connectionPort** | **Required** The port of the FTP server. | "22" | HIGH |
| **camel.kamelet.sftp-sink.username** | The username to access the FTP server. |  | MEDIUM |
| **camel.kamelet.sftp-sink.password** | The password to access the FTP server. |  | MEDIUM |
| **camel.kamelet.sftp-sink.directoryName** | **Required** The starting directory. |  | HIGH |
| **camel.kamelet.sftp-sink.passiveMode** | Specifies to use passive mode connection. | false | MEDIUM |
| **camel.kamelet.sftp-sink.fileExist** | How to behave in case of file already existent. | "Override" | MEDIUM |
| **camel.kamelet.sftp-sink.binary** | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | false | MEDIUM |
| **camel.kamelet.sftp-sink.privateKeyFile** | Set the private key file so that the SFTP endpoint can do private key verification. |  | MEDIUM |
| **camel.kamelet.sftp-sink.privateKeyPassphrase** | Set the private key file passphrase so that the SFTP endpoint can do private key verification. |  | MEDIUM |
| **camel.kamelet.sftp-sink.privateKeyUri** | Set the private key file (loaded from classpath by default) so that the SFTP endpoint can do private key verification. |  | MEDIUM |
| **camel.kamelet.sftp-sink.strictHostKeyChecking** | Sets whether to use strict host key checking. | "false" | MEDIUM |
| **camel.kamelet.sftp-sink.useUserKnownHostsFile** | If knownHostFile has not been explicit configured then use the host file from System.getProperty(user.home)/.ssh/known\_hosts. | true | MEDIUM |
| **camel.kamelet.sftp-sink.autoCreate** | Automatically create the directory the files should be written to. | true | MEDIUM |

The camel-sftp-sink sink connector has no converters out of the box.

The camel-sftp-sink sink connector has no transforms out of the box.

The camel-sftp-sink sink connector has no aggregation strategies out of the box.