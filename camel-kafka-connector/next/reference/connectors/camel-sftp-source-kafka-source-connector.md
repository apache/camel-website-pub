# camel-sftp-source-kafka-connector source configuration

Connector Description: Receive data from an SFTP server.

When using camel-sftp-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-sftp-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.sftpsource.CamelSftpsourceSourceConnector
```

The camel-sftp-source source connector supports 17 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.sftp-source.connectionHost** | **Required** The hostname of the SFTP server. |  | HIGH |
| **camel.kamelet.sftp-source.connectionPort** | **Required** The port of the FTP server. | "22" | HIGH |
| **camel.kamelet.sftp-source.username** | The username to access the SFTP server. |  | MEDIUM |
| **camel.kamelet.sftp-source.password** | The password to access the SFTP server. |  | MEDIUM |
| **camel.kamelet.sftp-source.directoryName** | **Required** The starting directory. |  | HIGH |
| **camel.kamelet.sftp-source.passiveMode** | Sets the passive mode connection. | false | MEDIUM |
| **camel.kamelet.sftp-source.recursive** | If a directory, look for files in all sub-directories as well. | false | MEDIUM |
| **camel.kamelet.sftp-source.idempotent** | Skip already-processed files. | true | MEDIUM |
| **camel.kamelet.sftp-source.ignoreFileNotFoundOrPermissionError** | Whether to ignore when (trying to list files in directories or when downloading a file), which does not exist or due to permission error. By default when a directory or file does not exists or insufficient permission, then an exception is thrown. Setting this option to true allows to ignore that instead. | false | MEDIUM |
| **camel.kamelet.sftp-source.binary** | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | false | MEDIUM |
| **camel.kamelet.sftp-source.privateKeyFile** | Set the private key file so that the SFTP endpoint can do private key verification. |  | MEDIUM |
| **camel.kamelet.sftp-source.privateKeyPassphrase** | Set the private key file passphrase so that the SFTP endpoint can do private key verification. |  | MEDIUM |
| **camel.kamelet.sftp-source.privateKeyUri** | Set the private key file (loaded from classpath by default) so that the SFTP endpoint can do private key verification. |  | MEDIUM |
| **camel.kamelet.sftp-source.strictHostKeyChecking** | Sets whether to use strict host key checking. | "false" | MEDIUM |
| **camel.kamelet.sftp-source.useUserKnownHostsFile** | If knownHostFile has not been explicit configured then use the host file from System.getProperty(user.home)/.ssh/known\_hosts. | true | MEDIUM |
| **camel.kamelet.sftp-source.autoCreate** | Automatically create starting directory. | true | MEDIUM |
| **camel.kamelet.sftp-source.delete** | If true, the file is deleted after it is processed successfully. | false | MEDIUM |

The camel-sftp-source source connector has no converters out of the box.

The camel-sftp-source source connector has no transforms out of the box.

The camel-sftp-source source connector has no aggregation strategies out of the box.