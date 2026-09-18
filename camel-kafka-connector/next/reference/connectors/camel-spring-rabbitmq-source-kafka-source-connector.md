# camel-spring-rabbitmq-source-kafka-connector source configuration

Connector Description: Receive data from a RabbitMQ Broker.

When using camel-spring-rabbitmq-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-spring-rabbitmq-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.springrabbitmqsource.CamelSpringrabbitmqsourceSourceConnector
```

The camel-spring-rabbitmq-source source connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.spring-rabbitmq-source.host** | **Required** RabbitMQ broker address Example: localhost. |  | HIGH |
| **camel.kamelet.spring-rabbitmq-source.port** | **Required** RabbitMQ broker port Example: 5672. |  | HIGH |
| **camel.kamelet.spring-rabbitmq-source.routingKey** | The routing key to use when binding a consumer queue to the exchange. |  | MEDIUM |
| **camel.kamelet.spring-rabbitmq-source.username** | The username to access the RabbitMQ server. |  | MEDIUM |
| **camel.kamelet.spring-rabbitmq-source.password** | The password to access the RabbitMQ server. |  | MEDIUM |
| **camel.kamelet.spring-rabbitmq-source.exchangeName** | **Required** The exchange name determines the exchange the queue is bound to. |  | HIGH |
| **camel.kamelet.spring-rabbitmq-source.queues** | The queue to receive messages from. |  | MEDIUM |
| **camel.kamelet.spring-rabbitmq-source.autoDeclare** | The routing key to use when binding a consumer queue to the exchange. | false | MEDIUM |
| **camel.kamelet.spring-rabbitmq-source.vhost** | The virtual host. | "/" | MEDIUM |
| **camel.kamelet.spring-rabbitmq-source.protocol** | The AMQP protocol to use. | "amqp" | MEDIUM |

The camel-spring-rabbitmq-source source connector has no converters out of the box.

The camel-spring-rabbitmq-source source connector has no transforms out of the box.

The camel-spring-rabbitmq-source source connector has no aggregation strategies out of the box.