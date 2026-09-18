# camel-ssh-sink-kafka-connector sink configuration

Connector Description: Send command through SSH session.

When using camel-ssh-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ssh-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.sshsink.CamelSshsinkSinkConnector
```

The camel-ssh-sink sink connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ssh-sink.connectionHost** | **Required** The SSH Host. |  | HIGH |
| **camel.kamelet.ssh-sink.connectionPort** | **Required** The SSH Port. | "22" | HIGH |
| **camel.kamelet.ssh-sink.username** | **Required** The SSH username to use. |  | HIGH |
| **camel.kamelet.ssh-sink.password** | **Required** The SSH password to use. |  | HIGH |

The camel-ssh-sink sink connector has no converters out of the box.

The camel-ssh-sink sink connector has no transforms out of the box.

The camel-ssh-sink sink connector has no aggregation strategies out of the box.