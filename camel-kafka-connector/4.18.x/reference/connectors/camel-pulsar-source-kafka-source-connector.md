# camel-pulsar-source-kafka-connector source configuration

Connector Description: Receive data from Pulsar topics.

When using camel-pulsar-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-pulsar-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.pulsarsource.CamelPulsarsourceSourceConnector
```

The camel-pulsar-source source connector supports 21 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.pulsar-source.topic** | **Required** The topic name or regexp. |  | HIGH |
| **camel.kamelet.pulsar-source.tenant** | **Required** The Tenant Name. |  | HIGH |
| **camel.kamelet.pulsar-source.topicType** | **Required** The topic type. |  | HIGH |
| **camel.kamelet.pulsar-source.namespaceName** | **Required** The Pulsar Namespace Name. |  | HIGH |
| **camel.kamelet.pulsar-source.serviceUrl** | **Required** The Pulsar Service URL to point while creating the client from URI. |  | HIGH |
| **camel.kamelet.pulsar-source.authenticationClass** | The Authentication FQCN to be used while creating the client from URI. |  | MEDIUM |
| **camel.kamelet.pulsar-source.authenticationParams** | The Authentication Parameters to be used while creating the client from URI. |  | MEDIUM |
| **camel.kamelet.pulsar-source.consumerNamePrefix** | Prefix to add to consumer names when a SHARED or FAILOVER subscription is used. | "cons" | MEDIUM |
| **camel.kamelet.pulsar-source.consumerQueueSize** | Size of the consumer queue. | 10 | MEDIUM |
| **camel.kamelet.pulsar-source.deadLetterTopic** | Name of the topic where the messages which fail `maxRedeliverCount` times are sent. Note: if not set, default topic name is topicName-subscriptionName-DLQ. |  | MEDIUM |
| **camel.kamelet.pulsar-source.maxRedeliverCount** | Maximum number of times that a message is redelivered before being sent to the dead letter queue. If this value is not set, no Dead Letter Policy is created. |  | MEDIUM |
| **camel.kamelet.pulsar-source.negativeAckRedeliveryDelayMicros** | Set the negative acknowledgement delay. | 60000000 | MEDIUM |
| **camel.kamelet.pulsar-source.messageListener** | Whether to use the messageListener interface, or to receive messages using a separate thread pool. | true | MEDIUM |
| **camel.kamelet.pulsar-source.numberOfConsumers** | Number of consumers. | 1 | MEDIUM |
| **camel.kamelet.pulsar-source.numberOfConsumerThreads** | Number of threads to receive and handle messages when using a separate thread pool. | 1 | MEDIUM |
| **camel.kamelet.pulsar-source.readCompacted** | Enable compacted topic reading. | false | MEDIUM |
| **camel.kamelet.pulsar-source.subscriptionInitialPosition** | Control the initial position in the topic of a newly created subscription. Default is latest message. | "LATEST" | MEDIUM |
| **camel.kamelet.pulsar-source.subscriptionName** | Name of the subscription to use. | "subs" | MEDIUM |
| **camel.kamelet.pulsar-source.subscriptionTopicsMode** | Determines to which topics this consumer should be subscribed to - Persistent, Non-Persistent, or both. Only used with pattern subscriptions. | "PersistentOnly" | MEDIUM |
| **camel.kamelet.pulsar-source.subscriptionType** | Type of the subscription. | "EXCLUSIVE" | MEDIUM |
| **camel.kamelet.pulsar-source.topicsPattern** | Whether the topic is a pattern (regular expression) that allows the consumer to subscribe to all matching topics in the namespace. | false | MEDIUM |

The camel-pulsar-source source connector has no converters out of the box.

The camel-pulsar-source source connector has no transforms out of the box.

The camel-pulsar-source source connector has no aggregation strategies out of the box.