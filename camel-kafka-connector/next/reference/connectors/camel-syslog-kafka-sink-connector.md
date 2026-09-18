# camel-syslog-kafka-connector sink configuration

When using camel-syslog-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-syslog-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

The camel-syslog sink connector supports is based on camel-netty sink connector and supports all its options (see: [Netty Sink Docs](camel-netty-kafka-sink-connector.md)); however has been already preconfigured and should be sufficient to provide the following properties:

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.sink.path.protocol** | The protocol to use which can be tcp or udp. One of: \[tcp\] \[udp\] | null | HIGH |
| **camel.sink.path.host** | The hostname. For the consumer the hostname is localhost or 0.0.0.0. For the producer the hostname is the remote host to connect to | null | HIGH |
| **camel.sink.path.port** | The host port number | null | HIGH |