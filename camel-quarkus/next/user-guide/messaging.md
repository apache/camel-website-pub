# Messaging Support

Camel Quarkus provides support for various messaging platforms, brokers and protocols via a diverse range of component extensions.

 
| Platform / Broker / Protocol | Extension(s) |
| --- | --- |
| AMQP | [`camel-quarkus-amqp`](../reference/extensions/amqp.md) |
| Apache ActiveMQ Classic | [`camel-quarkus-activemq`](../reference/extensions/activemq.md) or [`camel-quarkus-activemq6`](../reference/extensions/activemq6.md) |
| Apache ActiveMQ Artemis | [`quarkus-artemis`](https://quarkus.io/guides/jms#artemis-jms) in conjunction with either [`camel-quarkus-jms`](../reference/extensions/jms.md) or [`camel-quarkus-sjms2`](../reference/extensions/sjms2.md) |
| Apache Kafka | [`camel-quarkus-kafka`](../reference/extensions/kafka.md) |
| Apache Pulsar | [`camel-quarkus-pulsar`](../reference/extensions/pulsar.md) (JVM mode only) |
| AWS Kinesis | [`camel-quarkus-aws2-kinesis`](../reference/extensions/aws2-kinesis.md) |
| AWS Simple Notification Service (SNS) | [`camel-quarkus-aws2-sns`](../reference/extensions/aws2-sns.md) |
| AWS Simple Queue Service (SQS) | [`camel-quarkus-aws2-sqs`](../reference/extensions/aws2-sqs.md) |
| Azure Event Hubs | [`camel-quarkus-azure-eventhubs`](../reference/extensions/azure-eventhubs.md) |
| Azure Service Bus | [`camel-quarkus-azure-servicebus`](../reference/extensions/azure-servicebus.md) |
| Azure Storage Queue | [`camel-quarkus-azure-storage-queue`](../reference/extensions/azure-storage-queue.md) |
| Google PubSub | [`camel-quarkus-google-pubsub`](../reference/extensions/google-pubsub.md) |
| Ignite | [`camel-quarkus-ignite`](../reference/extensions/ignite.md) (JVM mode only) |
| JT400 | [`camel-quarkus-jt400`](../reference/extensions/jt400.md) |
| MQTT 5 | [`camel-quarkus-paho-mqtt5`](../reference/extensions/paho-mqtt5.md) |
| NATS | [`camel-quarkus-nats`](../reference/extensions/nats.md) |
| RabbitMQ | [`camel-quarkus-spring-rabbitmq`](../reference/extensions/spring-rabbitmq.md) |
> **Note**
> For JMS brokers not listed in the table above, use `camel-quarkus-jms`, `camel-quarkus-sjms` or `camel-quarkus-sjms2`. Then add your preferred JMS client libraries to the project dependencies. Not all third party client libraries are guaranteed to work out of the box in native mode.