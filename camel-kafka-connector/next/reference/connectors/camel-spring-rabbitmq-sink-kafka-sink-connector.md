# camel-spring-rabbitmq-sink-kafka-connector sink configuration

Connector Description: Send data to a RabbitMQ Broker.

When using camel-spring-rabbitmq-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-spring-rabbitmq-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.springrabbitmqsink.CamelSpringrabbitmqsinkSinkConnector
```

The camel-spring-rabbitmq-sink sink connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.spring-rabbitmq-sink.host** | **Required** RabbitMQ broker address Example: localhost. |  | HIGH |
| **camel.kamelet.spring-rabbitmq-sink.port** | **Required** RabbitMQ broker port Example: 5672. |  | HIGH |
| **camel.kamelet.spring-rabbitmq-sink.routingKey** | The routing key to use when binding a consumer queue to the exchange. |  | MEDIUM |
| **camel.kamelet.spring-rabbitmq-sink.username** | The username to access the RabbitMQ server. |  | MEDIUM |
| **camel.kamelet.spring-rabbitmq-sink.password** | The password to access the RabbitMQ server. |  | MEDIUM |
| **camel.kamelet.spring-rabbitmq-sink.exchangeName** | **Required** The exchange name determines the exchange the queue is bound to. |  | HIGH |
| **camel.kamelet.spring-rabbitmq-sink.queues** | The queue to receive messages from. |  | MEDIUM |
| **camel.kamelet.spring-rabbitmq-sink.autoDeclareProducer** | Specifies whether the producer should auto declare binding between exchange, queue and routing key when starting. | false | MEDIUM |
| **camel.kamelet.spring-rabbitmq-sink.vhost** | The virtual host. | "/" | MEDIUM |
| **camel.kamelet.spring-rabbitmq-sink.protocol** | The AMQP protocol to use. | "amqp" | MEDIUM |

The camel-spring-rabbitmq-sink sink connector has no converters out of the box.

The camel-spring-rabbitmq-sink sink connector has no transforms out of the box.

The camel-spring-rabbitmq-sink sink connector has no aggregation strategies out of the box.