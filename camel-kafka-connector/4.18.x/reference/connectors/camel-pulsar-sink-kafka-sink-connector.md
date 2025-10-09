# camel-pulsar-sink-kafka-connector sink configuration

Connector Description: Send documents to Pulsar.

When using camel-pulsar-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-pulsar-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.pulsarsink.CamelPulsarsinkSinkConnector
```

The camel-pulsar-sink sink connector supports 19 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.pulsar-sink.topic** | **Required** The topic name or regexp. |  | HIGH |
| **camel.kamelet.pulsar-sink.tenant** | **Required** The Tenant Name. |  | HIGH |
| **camel.kamelet.pulsar-sink.topicType** | **Required** The topic type. |  | HIGH |
| **camel.kamelet.pulsar-sink.namespaceName** | **Required** The Pulsar Namespace Name. |  | HIGH |
| **camel.kamelet.pulsar-sink.serviceUrl** | **Required** The Pulsar Service URL to point while creating the client from URI. |  | HIGH |
| **camel.kamelet.pulsar-sink.authenticationClass** | The Authentication FQCN to be used while creating the client from URI. |  | MEDIUM |
| **camel.kamelet.pulsar-sink.authenticationParams** | The Authentication Parameters to be used while creating the client from URI. |  | MEDIUM |
| **camel.kamelet.pulsar-sink.batchingEnabled** | Control whether automatic batching of messages is enabled for the producer. | true | MEDIUM |
| **camel.kamelet.pulsar-sink.batchingMaxMessages** | The maximum size to batch messages. | 1000 | MEDIUM |
| **camel.kamelet.pulsar-sink.batchingMaxPublishDelayMicros** | Used if `batchingEnabled` is `true`. Sets the maximum time period within which the messages sent are batched. | 1000 | MEDIUM |
| **camel.kamelet.pulsar-sink.blockIfQueueFull** | Whether to block the producing thread if pending messages queue is full or to throw a ProducerQueueIsFullError. | false | MEDIUM |
| **camel.kamelet.pulsar-sink.compressionType** | Compression type to use. | "NONE" | MEDIUM |
| **camel.kamelet.pulsar-sink.initialSequenceId** | The first message published will have a sequence Id of initialSequenceId 1. | \-1 | MEDIUM |
| **camel.kamelet.pulsar-sink.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.kamelet.pulsar-sink.maxPendingMessages** | Size of the pending massages queue. When the queue is full, by default, any further sends will fail unless blockIfQueueFull=true. | 1000 | MEDIUM |
| **camel.kamelet.pulsar-sink.maxPendingMessagesAcrossPartitions** | The maximum number of pending messages for partitioned topics. The `maxPendingMessages` value is reduced if (number of partitions `maxPendingMessages`) exceeds this value. Partitioned topics have a pending message queue for each partition. | 50000 | MEDIUM |
| **camel.kamelet.pulsar-sink.messageRoutingMode** | Message Routing Mode to use. | "RoundRobinPartition" | MEDIUM |
| **camel.kamelet.pulsar-sink.producerName** | Name of the producer. If unset, lets Pulsar select a unique identifier. |  | MEDIUM |
| **camel.kamelet.pulsar-sink.sendTimeoutMs** | Send timeout in milliseconds. | 30000 | MEDIUM |

The camel-pulsar-sink sink connector has no converters out of the box.

The camel-pulsar-sink sink connector has no transforms out of the box.

The camel-pulsar-sink sink connector has no aggregation strategies out of the box.