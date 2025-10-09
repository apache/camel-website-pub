# ![kafka sink](_images/kamelets/kafka-sink.svg) Kafka Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Kafka topics through Plain Login Module.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **password** | Password | **Required** Password to authenticate to kafka. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **user** | Username | **Required** Username to authenticate to Kafka. | string |  |  |
| **saslMechanism** | SASL Mechanism | The Simple Authentication and Security Layer (SASL) Mechanism used. | string | PLAIN |  |
| **securityProtocol** | Security Protocol | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | string | SASL\_SSL |  |

## Dependencies

At runtime, the `kafka-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:kafka-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka Sink Kamelet Description

### Headers Support

The Kamelet is able to understand the following headers to be set:

-   `key` / `ce-key`: as message key
    
-   `partition-key` / `ce-partitionkey`: as message partition key
    

Both headers are optional.

### Authentication

This Kamelet uses Plain Login Module for authentication with username and password.

### Security Protocols

Supports multiple security protocols: - SASL\_PLAINTEXT - PLAINTEXT - SASL\_SSL - SSL

Default security protocol is SASL\_SSL with PLAIN SASL mechanism.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-sink.kamelet.yaml)