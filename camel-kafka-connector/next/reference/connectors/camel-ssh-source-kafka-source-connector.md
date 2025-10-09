# camel-ssh-source-kafka-connector source configuration

Connector Description: Receive data from SSH session.

When using camel-ssh-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ssh-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.sshsource.CamelSshsourceSourceConnector
```

The camel-ssh-source source connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ssh-source.connectionHost** | **Required** The SSH Host. |  | HIGH |
| **camel.kamelet.ssh-source.connectionPort** | **Required** The SSH Port. | "22" | HIGH |
| **camel.kamelet.ssh-source.username** | **Required** The SSH username to use. |  | HIGH |
| **camel.kamelet.ssh-source.password** | **Required** The SSH password to use. |  | HIGH |
| **camel.kamelet.ssh-source.delay** | The number of milliseconds before the next poll. | 500 | MEDIUM |
| **camel.kamelet.ssh-source.pollCommand** | **Required** The command to run while polling the SSH session Example: date. |  | HIGH |

The camel-ssh-source source connector has no converters out of the box.

The camel-ssh-source source connector has no transforms out of the box.

The camel-ssh-source source connector has no aggregation strategies out of the box.