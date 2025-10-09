# ![pulsar source](_images/kamelets/pulsar-source.svg) Pulsar Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from Pulsar topics.

## Configuration Options

The following table summarizes the configuration options available for the `pulsar-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **namespaceName** | Pulsar Namespace Name | **Required** The Pulsar Namespace Name. | string |  |  |
| **serviceUrl** | Service URL | **Required** The Pulsar Service URL to point while creating the client from URI. | string |  |  |
| **tenant** | Tenant Name | **Required** The Tenant Name. | string |  |  |
| **topic** | Topic Name | **Required** The topic name or regexp. | string |  |  |
| **topicType** | Topic Type | **Required** The topic type. Enum values: \* persistent \* non-persistent | string |  |  |
| **authenticationClass** | Authentication Class | The Authentication FQCN to be used while creating the client from URI. | string |  |  |
| **authenticationParams** | Authentication Params | The Authentication Parameters to be used while creating the client from URI. | string |  |  |
| **consumerNamePrefix** | Consumer Name Prefix | Prefix to add to consumer names when a SHARED or FAILOVER subscription is used. | string | cons |  |
| **consumerQueueSize** | Consumer Queue Size | Size of the consumer queue. | integer | 10 |  |
| **deadLetterTopic** | Dead Letter Topic | Name of the topic where the messages which fail `maxRedeliverCount` times are sent. Note: if not set, default topic name is topicName-subscriptionName-DLQ. | integer |  |  |
| **maxRedeliverCount** | Maximum Redelivery Count | Maximum number of times that a message is redelivered before being sent to the dead letter queue. If this value is not set, no Dead Letter Policy is created. | integer |  |  |
| **messageListener** | Message Listener | Whether to use the messageListener interface, or to receive messages using a separate thread pool. | boolean | true |  |
| **negativeAckRedeliveryDelayMicros** | Negative Ack Redelivery Delay in Microseconds | Set the negative acknowledgement delay. | integer | 60000000 |  |
| **numberOfConsumerThreads** | Number Of Consumer Threads | Number of threads to receive and handle messages when using a separate thread pool. | integer | 1 |  |
| **numberOfConsumers** | Number Of Consumers | Number of consumers. | integer | 1 |  |
| **readCompacted** | Read Compacted | Enable compacted topic reading. | boolean | false |  |
| **subscriptionInitialPosition** | Subscription Initial Position | Control the initial position in the topic of a newly created subscription. Default is latest message. Enum values: \* EARLIEST \* LATEST | string | LATEST |  |
| **subscriptionName** | Subscription Name | Name of the subscription to use. | string | subs |  |
| **subscriptionTopicsMode** | Subscription Topics Mode | Determines to which topics this consumer should be subscribed to - Persistent, Non-Persistent, or both. Only used with pattern subscriptions. Enum values: \* PersistentOnly \* NonPersistentOnly \* AllTopics | string | PersistentOnly |  |
| **subscriptionType** | Subscription Type | Type of the subscription. Enum values: \* EXCLUSIVE \* SHARED \* FAILOVER \* KEY\_SHARED | string | EXCLUSIVE |  |
| **topicsPattern** | Topic Pattern | Whether the topic is a pattern (regular expression) that allows the consumer to subscribe to all matching topics in the namespace. | boolean | false |  |

## Dependencies

At runtime, the `pulsar-source` Kamelet relies upon the presence of the following dependencies:

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

This Kamelet connects to Pulsar using appropriate authentication mechanisms:

-   Service-specific authentication methods
    
-   API keys, tokens, or credential-based authentication
    
-   Connection configuration
    

### Output format

The Kamelet consumes data from Pulsar and produces the data in JSON format.

### Configuration

The Kamelet requires connection parameters specific to Pulsar:

-   Service connection details
    
-   Authentication credentials
    
-   Query or consumption parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: pulsar-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: pulsar-source
    properties:
      # Add service-specific properties here
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pulsar-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pulsar-source.kamelet.yaml)