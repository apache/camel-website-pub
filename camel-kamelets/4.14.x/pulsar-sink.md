# ![pulsar sink](_images/kamelets/pulsar-sink.svg) Pulsar Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send documents to Pulsar.

## Configuration Options

The following table summarizes the configuration options available for the `pulsar-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **namespaceName** | Pulsar Namespace Name | **Required** The Pulsar Namespace Name. | string |  |  |
| **serviceUrl** | Service URL | **Required** The Pulsar Service URL to point while creating the client from URI. | string |  |  |
| **tenant** | Tenant Name | **Required** The Tenant Name. | string |  |  |
| **topic** | Topic Name | **Required** The topic name or regexp. | string |  |  |
| **topicType** | Topic Type | **Required** The topic type. Enum values: \* persistent \* non-persistent | string |  |  |
| **authenticationClass** | Authentication Class | The Authentication FQCN to be used while creating the client from URI. | string |  |  |
| **authenticationParams** | Authentication Params | The Authentication Parameters to be used while creating the client from URI. | string |  |  |
| **batchingEnabled** | Enable Batching | Control whether automatic batching of messages is enabled for the producer. | boolean | true |  |
| **batchingMaxMessages** | Batching Maximum Messages | The maximum size to batch messages. | integer | 1000 |  |
| **batchingMaxPublishDelayMicros** | Batching Maximum Publish Delay in Microsecond | Used if `batchingEnabled` is `true`. Sets the maximum time period within which the messages sent are batched. | integer | 1000 |  |
| **blockIfQueueFull** | Block If Queue Full | Whether to block the producing thread if pending messages queue is full or to throw a ProducerQueueIsFullError. | boolean | false |  |
| **compressionType** | Compression Type | Compression type to use. Enum values: \* NONE \* LZ4 \* ZLIB \* ZSTD \* SNAPPY | string | NONE |  |
| **initialSequenceId** | Initial SequenceId | The first message published will have a sequence Id of initialSequenceId 1. | integer | \-1 |  |
| **lazyStartProducer** | Number Of Consumer Threads | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | boolean | false |  |
| **maxPendingMessages** | Maximum Pending Messages | Size of the pending massages queue. When the queue is full, by default, any further sends will fail unless blockIfQueueFull=true. | integer | 1000 |  |
| **maxPendingMessagesAcrossPartitions** | Maximum Pending Messages Across Partitions | The maximum number of pending messages for partitioned topics. The `maxPendingMessages` value is reduced if (number of partitions `maxPendingMessages`) exceeds this value. Partitioned topics have a pending message queue for each partition. | integer | 50000 |  |
| **messageRoutingMode** | Message Routing Mode | Message Routing Mode to use. Enum values: \* SinglePartition \* RoundRobinPartition \* CustomPartition | string | RoundRobinPartition |  |
| **producerName** | Producer Name | Name of the producer. If unset, lets Pulsar select a unique identifier. | string |  |  |
| **sendTimeoutMs** | Send Timeout in Milliseconds | Send timeout in milliseconds. | integer | 30000 |  |

## Dependencies

At runtime, the `pulsar-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:pulsar
    
-   camel:kamelet
    
-   camel:core
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:pulsar-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Pulsar Sink Kamelet Description

### Apache Pulsar Integration

This Kamelet integrates with Apache Pulsar, a distributed messaging and streaming platform built for the cloud. Pulsar provides unified messaging and streaming with high scalability and low latency.

### Multi-Tenancy

Pulsar supports native multi-tenancy with namespaces and topics organized within tenants, providing isolation and resource management for different applications and teams.

### Geo-Replication

Built-in geo-replication capabilities enable data replication across multiple data centers for disaster recovery and global data distribution scenarios.

### Persistent and Non-Persistent Messaging

Supports both persistent messaging (with data durability) and non-persistent messaging (for low-latency scenarios) based on application requirements.

### Schema Registry Integration

Pulsar includes built-in schema registry support for schema evolution and validation, ensuring data compatibility across producers and consumers.

### Cloud-Native Architecture

Designed for cloud-native deployments with:

-   Horizontal scaling capabilities
    
-   Kubernetes integration
    
-   Multi-cloud support
    
-   Serverless computing integration
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pulsar-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pulsar-sink.kamelet.yaml)