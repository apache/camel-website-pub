# ![kafka not secured sink](_images/kamelets/kafka-not-secured-sink.svg) Kafka Not Secured Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Kafka topics on an insecure broker.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-not-secured-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |

## Dependencies

At runtime, the `kafka-not-secured-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kafka
    
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
            uri: "kamelet:kafka-not-secured-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka Not Secured Sink Kamelet Description

### Basic Kafka Integration

This Kamelet provides a simple integration with Kafka topics using an unsecured connection. It’s designed for development environments or internal networks where security is not a primary concern.

### Message Headers

The Kamelet supports both standard and CloudEvents headers for message routing:

-   Message key headers: `key` or `ce-key`
    
-   Partition key headers: `partition-key` or `ce-partitionkey`
    

### Minimal Configuration

Only requires the essential configuration parameters: topic names and bootstrap servers. No authentication or encryption is configured.

### Use Cases

Suitable for: - Development and testing environments - Internal network communications - Proof-of-concept implementations

### Security Warning

This Kamelet does not provide any security mechanisms. Do not use in production environments where data protection is required.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-not-secured-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-not-secured-sink.kamelet.yaml)