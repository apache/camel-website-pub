# camel-scp-sink-kafka-connector sink configuration

Connector Description: Send file to an FTP Server through Secure Copy Protocol

When using camel-scp-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-scp-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.scpsink.CamelScpsinkSinkConnector
```

The camel-scp-sink sink connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.scp-sink.serverName** | **Required** The hostname of the FTP server. |  | HIGH |
| **camel.kamelet.scp-sink.serverPort** | **Required** The port of the FTP server. |  | HIGH |
| **camel.kamelet.scp-sink.username** | Username for accessing FTP Server. |  | MEDIUM |
| **camel.kamelet.scp-sink.password** | Password for accessing FTP Server. |  | MEDIUM |
| **camel.kamelet.scp-sink.privateKeyFile** | Set the private key file so that the SFTP endpoint can do private key verification. |  | MEDIUM |
| **camel.kamelet.scp-sink.privateKeyPassphrase** | Set the private key file passphrase so that the SFTP endpoint can do private key verification. |  | MEDIUM |
| **camel.kamelet.scp-sink.strictHostKeyChecking** | Sets whether to use strict host key checking. | "false" | MEDIUM |
| **camel.kamelet.scp-sink.useUserKnownHostsFile** | If knownHostFile has not been explicit configured then use the host file from System.getProperty(user.home)/.ssh/known\_hosts. | true | MEDIUM |

The camel-scp-sink sink connector has no converters out of the box.

The camel-scp-sink sink connector has no transforms out of the box.

The camel-scp-sink sink connector has no aggregation strategies out of the box.