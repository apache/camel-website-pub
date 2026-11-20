# ![pulsar sink](_images/kamelets/pulsar-sink.svg) Pulsar Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a topic in Apache Pulsar, named by its tenant, namespace and topic name.

Use it to publish events or data for other applications to read from Pulsar, such as orders or sensor readings. Use `pulsar-source` to read them.

Input: the body is the payload, as text or bytes. It is turned into bytes, and the `Content-Type` header is set to `application/octet-stream`, before it is sent. A Map fails: turn it into JSON text first, for example with `json-serialize-action`. The headers of the message are not sent as Pulsar properties; to set properties, put a Map in the `CamelPulsarProducerMessageProperties` header. The optional `key` header becomes the key of the message, as the `key` header that `pulsar-source` sets; the `CamelPulsarProducerMessageKey` header takes precedence over it.

Output: the body is the payload, as bytes, and the `Content-Type` header is `application/octet-stream`. The other headers are kept, and the `CamelPulsarProducerMessageId` header is added with the ID that Pulsar gave the message.

Good to know: it connects with no TLS and no login, unless `serviceUrl` starts with `pulsar+ssl://` and `authenticationClass` is set. Over TLS, the certificate of Pulsar must be signed by an authority that the Java trust store of the integration trusts, or by one in the PEM file of `tlsTrustCertsFilePath`, such as a private one, and it must be issued for the host name in `serviceUrl`. It connects when the integration starts, and the integration fails to start when Pulsar cannot be reached, unless `lazyStart` is true. Headers that start with `CamelPulsar`, except `CamelPulsarProducerMessageKey` and `CamelPulsarProducerMessageProperties`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `pulsar-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **namespaceName** | Namespace Name | **Required** The namespace within the tenant that holds the topic. A new Pulsar has the namespace `default` in the tenant `public`. | string |  | default |
| **serviceUrl** | Service URL | **Required** The address of the Pulsar broker, as `pulsar://host:port` (the usual port is 6650), or `pulsar+ssl://host:port` for TLS (usually 6651). | string |  | pulsar://localhost:6650 |
| **tenant** | Tenant Name | **Required** The Pulsar tenant that the namespace belongs to. A new Pulsar has the tenant `public`. | string |  | public |
| **topic** | Topic Name | **Required** The name of the topic within the namespace to send the messages to. | string |  | orders |
| **topicType** | Topic Type | **Required** Whether the topic is `persistent`, which stores the messages until they are read, or `non-persistent`, which stores nothing and drops the messages that no one is subscribed to. Enum values: \* persistent \* non-persistent | string |  |  |
| **authenticationClass** | Authentication Class | The Java class of the Pulsar authentication plugin to log in with, such as `org.apache.pulsar.client.impl.auth.AuthenticationToken` for a token. Leave it empty for a Pulsar without login. | string |  | org.apache.pulsar.client.impl.auth.AuthenticationToken |
| **authenticationParams** | Authentication Params | The settings of the plugin in `authenticationClass`, in the form that plugin expects: for `AuthenticationToken`, `token:` followed by the token. | string |  |  |
| **batchingEnabled** | Enable Batching | If true, messages sent close together are grouped and sent to Pulsar in one batch. A batch goes to one receiver of a `KEY_SHARED` subscription as a whole, whatever the keys of its messages; set it to false to have the keys spread over the receivers. | boolean | true |  |
| **batchingMaxMessages** | Batching Maximum Messages | The most messages in one batch. Only used when `batchingEnabled` is true. | integer | 1000 |  |
| **batchingMaxPublishDelayMicros** | Batch Publish Delay | How long to wait for more messages to fill a batch before sending it, in microseconds. For example, 1000 is one millisecond. Only used when `batchingEnabled` is true. | integer | 1000 |  |
| **blockIfQueueFull** | Block If Queue Full | What happens when `maxPendingMessages` messages are already waiting for Pulsar to confirm them: if true, sending waits until there is room; if false, the message fails. | boolean | false |  |
| **compressionType** | Compression Type | How to compress the messages on the way to Pulsar. The readers decompress them by themselves. Enum values: \* NONE \* LZ4 \* ZLIB \* ZSTD \* SNAPPY | string | NONE |  |
| **initialSequenceId** | Initial Sequence ID | The sequence ID to count from: the first message gets this number plus one. With the default, -1, the first message gets 0. Pulsar uses sequence IDs to drop duplicates when deduplication is on. | integer | \-1 |  |
| **lazyStart** | Lazy Start | If true, the connection to Pulsar is made when the first message is sent, not when the integration starts. The integration then starts even when Pulsar cannot be reached, and the first message takes longer. | boolean | false |  |
| **maxPendingMessages** | Maximum Pending Messages | The most messages that can wait at the same time for Pulsar to confirm them. See `blockIfQueueFull` for what happens to more. | integer | 1000 |  |
| **messageRoutingMode** | Message Routing Mode | How messages are spread over the partitions of a partitioned topic: `RoundRobinPartition` spreads them in turn, `SinglePartition` sends them all to one partition, and in both a message with a key always goes to the partition of its key. `CustomPartition` needs a custom router, which this Kamelet cannot set. Enum values: \* SinglePartition \* RoundRobinPartition \* CustomPartition | string | RoundRobinPartition |  |
| **producerName** | Producer Name | The name of this sender in Pulsar, shown in the topic statistics and set on each message. When it is not set, Pulsar picks a unique name. | string |  |  |
| **sendTimeoutMs** | Send Timeout | How long Pulsar may take to confirm a message before the message fails, in milliseconds. For example, 30000 is 30 seconds. | integer | 30000 |  |
| **tlsTrustCertsFilePath** | TLS Trust Certificates File | The path of a PEM file with the certificates of the authorities to trust for a `pulsar+ssl://` broker, such as a private one, instead of the Java trust store. Only used with `pulsar+ssl://`. | string |  | /etc/pulsar/ca.pem |

## Dependencies

At runtime, the `pulsar-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:pulsar
    
-   camel:kamelet
    

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

Pulsar includes built-in schema registry support for schema evolution and validation. This Kamelet does not use it: it sends the body as bytes, so turn structured data into JSON text first.

### Cloud-Native Architecture

Designed for cloud-native deployments with:

-   Horizontal scaling capabilities
    
-   Kubernetes integration
    
-   Multi-cloud support
    
-   Serverless computing integration
    

### Message Key

The optional `key` header becomes the key of the message. Pulsar keeps the messages with the same key in order on one partition, and a `KEY_SHARED` subscription hands them to the same receiver. `pulsar-source` sets the `key` header, so the key is kept when one Kamelet feeds the other. The `CamelPulsarProducerMessageKey` header takes precedence over `key`.

A batch of messages goes to one receiver of a `KEY_SHARED` subscription as a whole, whatever the keys in it. Set `batchingEnabled` to `false` to have the keys spread over the receivers.

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "order placed"
      steps:
        - setHeader:
            name: key
            constant: "customer-7"
        - to:
            uri: "kamelet:pulsar-sink"
            parameters:
              serviceUrl: "pulsar://localhost:6650"
              topicType: "persistent"
              tenant: "public"
              namespaceName: "default"
              topic: "orders"
              batchingEnabled: false
```

For TLS, use a `pulsar+ssl://` address in `serviceUrl`. The Kamelet has no trust store option: the certificate of Pulsar is checked against the Java trust store of the integration, which `javax.net.ssl.trustStore` can point at.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pulsar-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pulsar-sink.kamelet.yaml)