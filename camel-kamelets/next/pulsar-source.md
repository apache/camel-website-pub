# ![pulsar source](_images/kamelets/pulsar-source.svg) Pulsar Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message from a topic in Apache Pulsar, or from every topic whose name matches a pattern, through a named subscription.

Use it to process events or data that other applications publish to Pulsar. Several copies can share the work with a `SHARED` or `KEY_SHARED` subscription.

Output: the body is the payload, as bytes, and the `Content-Type` header is `application/octet-stream`. The other headers give the topic (`topic_name`), the key (`key`), the Pulsar properties as a Map (`properties`), the `message_id`, the `publish_time` and the `producer_name`.

Good to know: the subscription (`subscriptionName`, `subs` by default) remembers what was read, so messages sent while the source is stopped are read when it starts again. A new subscription starts at the newest message, unless `subscriptionInitialPosition` is `EARLIEST`. A message whose processing fails is delivered again after one minute, again and again, unless `maxRedeliverCount` is set with a `SHARED` or `KEY_SHARED` subscription. A message whose processing takes longer than `ackTimeoutMillis` (10 seconds when not set) is delivered again, and so processed twice. It connects with no TLS and no login, unless `serviceUrl` starts with `pulsar+ssl://` and `authenticationClass` is set. Over TLS, the certificate of Pulsar must be signed by an authority that the Java trust store of the integration trusts, or by one in the PEM file of `tlsTrustCertsFilePath`, such as a private one, and it must be issued for the host name in `serviceUrl`.

## Configuration Options

The following table summarizes the configuration options available for the `pulsar-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **namespaceName** | Namespace Name | **Required** The namespace within the tenant that holds the topic. A new Pulsar has the namespace `default` in the tenant `public`. | string |  | default |
| **serviceUrl** | Service URL | **Required** The address of the Pulsar broker, as `pulsar://host:port` (the usual port is 6650), or `pulsar+ssl://host:port` for TLS (usually 6651). | string |  | pulsar://localhost:6650 |
| **tenant** | Tenant Name | **Required** The Pulsar tenant that the namespace belongs to. A new Pulsar has the tenant `public`. | string |  | public |
| **topic** | Topic Name | **Required** The name of the topic within the namespace to receive the messages from. When `topicsPattern` is true, a regular expression for the names of the topics instead, such as `orders-.*`. | string |  | orders |
| **topicType** | Topic Type | **Required** Whether the topic is `persistent`, which stores the messages until they are read, or `non-persistent`, which stores nothing and drops the messages that no one is subscribed to. Enum values: \* persistent \* non-persistent | string |  |  |
| **ackTimeoutMillis** | Acknowledgement Timeout | How long the processing of a message may take, in milliseconds. A message that is not done by then is delivered again, and so processed twice. When it is not set, 10000 (10 seconds). 0 turns this off; a value from 1 to 999 makes the integration fail to start. | integer |  |  |
| **authenticationClass** | Authentication Class | The Java class of the Pulsar authentication plugin to log in with, such as `org.apache.pulsar.client.impl.auth.AuthenticationToken` for a token. Leave it empty for a Pulsar without login. | string |  | org.apache.pulsar.client.impl.auth.AuthenticationToken |
| **authenticationParams** | Authentication Params | The settings of the plugin in `authenticationClass`, in the form that plugin expects: for `AuthenticationToken`, `token:` followed by the token. | string |  |  |
| **consumerNamePrefix** | Consumer Name Prefix | The start of the name of each receiver of a `SHARED` or `FAILOVER` subscription; a number is added to it. | string | cons |  |
| **consumerQueueSize** | Consumer Queue Size | How many messages each receiver fetches from Pulsar ahead of time. | integer | 10 |  |
| **deadLetterTopic** | Dead Letter Topic | The topic that gets the messages that failed `maxRedeliverCount` times. A short name, such as `orders-dlq`, is a topic in `public/default`; for another namespace, give the full name, such as `persistent://my-tenant/my-namespace/orders-dlq`. When it is not set, it is the topic name followed by `-`, the subscription name and `-DLQ`, in the namespace of the topic. Only used when `maxRedeliverCount` is set. | string |  |  |
| **maxRedeliverCount** | Maximum Redelivery Count | How many times a message whose processing fails is delivered again before it goes to `deadLetterTopic`. Only works with a `SHARED` or `KEY_SHARED` `subscriptionType`: with `EXCLUSIVE` or `FAILOVER`, it is ignored. When it is not set, a failing message is delivered again forever. | integer |  |  |
| **messageListener** | Message Listener | If true, Pulsar hands each message to the source as it arrives. If false, `numberOfConsumerThreads` threads fetch the messages. | boolean | true |  |
| **negativeAckRedeliveryDelayMicros** | Redelivery Delay | How long to wait before a message whose processing failed is delivered again, in microseconds. For example, 60000000 is one minute. | integer | 60000000 |  |
| **numberOfConsumerThreads** | Number of Consumer Threads | How many threads fetch and handle the messages when `messageListener` is false. | integer | 1 |  |
| **numberOfConsumers** | Number of Consumers | How many receivers to open on the subscription. More than one only helps with a `SHARED`, `KEY_SHARED` or `FAILOVER` `subscriptionType`. | integer | 1 |  |
| **readCompacted** | Read Compacted | If true, reads the compacted topic, which keeps only the newest message for each key. Only for a persistent topic with an `EXCLUSIVE` or `FAILOVER` subscription. | boolean | false |  |
| **subscriptionInitialPosition** | Subscription Initial Position | Where a new subscription starts reading: `LATEST` reads only the messages sent from then on, `EARLIEST` also reads the messages already in the topic. An existing subscription goes on where it stopped. Enum values: \* EARLIEST \* LATEST | string | LATEST |  |
| **subscriptionName** | Subscription Name | The name of the subscription. Pulsar remembers for each subscription which messages were read, so keep the name across restarts. Two sources with different names each get every message. | string | subs |  |
| **subscriptionTopicsMode** | Subscription Topics Mode | Which topics a pattern subscription covers: persistent ones, non-persistent ones, or both. Only used when `topicsPattern` is true. Enum values: \* PersistentOnly \* NonPersistentOnly \* AllTopics | string | PersistentOnly |  |
| **subscriptionType** | Subscription Type | How the receivers of the subscription share the messages: `EXCLUSIVE` allows one receiver only, `SHARED` spreads the messages over all receivers, `FAILOVER` sends them all to one receiver and moves to another when it goes away, and `KEY_SHARED` spreads them while keeping the messages with the same key on one receiver. Enum values: \* EXCLUSIVE \* SHARED \* FAILOVER \* KEY\_SHARED | string | EXCLUSIVE |  |
| **tlsTrustCertsFilePath** | TLS Trust Certificates File | The path of a PEM file with the certificates of the authorities to trust for a `pulsar+ssl://` broker, such as a private one, instead of the Java trust store. Only used with `pulsar+ssl://`. | string |  | /etc/pulsar/ca.pem |
| **topicsPattern** | Topic Pattern | If true, `topic` is a regular expression, and the source subscribes to every topic of the namespace whose name matches it. | boolean | false |  |

## Dependencies

At runtime, the `pulsar-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:pulsar-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Pulsar Source Kamelet Description

### Authentication methods

With no `authenticationClass`, the Kamelet connects without a login. For a token, set `authenticationClass` to `org.apache.pulsar.client.impl.auth.AuthenticationToken` and `authenticationParams` to `token:` followed by the token. For TLS, use a `pulsar+ssl://` address in `serviceUrl`.

The Kamelet has no trust store option: over TLS, the certificate of Pulsar is checked against the Java trust store of the integration. For a certificate signed by a private authority, put the authority in a trust store and point the JVM at it, for example with `JAVA_TOOL_OPTIONS="-Djavax.net.ssl.trustStore=/etc/pulsar/truststore.jks -Djavax.net.ssl.trustStorePassword=changeit"`.

### Output format

The body is the Pulsar payload, as bytes; it is not turned into JSON. The headers give the topic, the key, the properties, the message ID and the publish time of the message.

### Configuration

The topic is named by `topicType` (`persistent` or `non-persistent`), `tenant`, `namespaceName` and `topic`, which make up `persistent://public/default/orders`, for example. With `topicsPattern` set to true, `topic` is a regular expression, and the Kamelet reads from every matching topic of the namespace.

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:pulsar-source"
      parameters:
        serviceUrl: "pulsar://localhost:6650"
        topicType: "persistent"
        tenant: "public"
        namespaceName: "default"
        topic: "orders"
        subscriptionName: "orders-processor"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Slow Processing and a Dead Letter Topic

A message that is not processed within `ackTimeoutMillis` (10 seconds when not set) is delivered again, and so processed twice. When the processing of a message can take longer, raise it, or set it to `0` to turn this off.

A message whose processing fails is delivered again and again. With a `SHARED` or `KEY_SHARED` subscription, `maxRedeliverCount` stops this: after that many failed deliveries, the message goes to `deadLetterTopic`. With an `EXCLUSIVE` or `FAILOVER` subscription, `maxRedeliverCount` is ignored.

```yaml
- route:
    from:
      uri: "kamelet:pulsar-source"
      parameters:
        serviceUrl: "pulsar://localhost:6650"
        topicType: "persistent"
        tenant: "public"
        namespaceName: "default"
        topic: "orders"
        subscriptionName: "orders-processor"
        subscriptionType: "SHARED"
        ackTimeoutMillis: 60000
        maxRedeliverCount: 3
        negativeAckRedeliveryDelayMicros: 5000000
        deadLetterTopic: "persistent://public/default/orders-dlq"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pulsar-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pulsar-source.kamelet.yaml)