# ![nats sink](_images/kamelets/nats-sink.svg) NATS Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to NATS topics.

## Configuration Options

The following table summarizes the configuration options available for the `nats-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **servers** | Servers | **Required** Comma separated list of NATS Servers. | string |  |  |
| **topic** | Topic | **Required** NATS Topic name. | string |  |  |
| **jetstreamAsync** | Jetstream Async Enabled | Sets whether to operate JetStream requests asynchronously. | boolean | true |  |
| **jetstreamEnabled** | Jetstream Enabled | Sets whether to enable JetStream support for this endpoint. | boolean | false |  |
| **jetstreamName** | Jetstream Stream Name | Sets the name of the JetStream stream to use. | string |  |  |

## Dependencies

At runtime, the `nats-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:nats
    
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
            uri: "kamelet:nats-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## NATS Sink Kamelet Description

### NATS Messaging System

This Kamelet integrates with NATS, a high-performance messaging system designed for cloud-native applications, IoT messaging, and microservices architectures.

### High Performance

NATS provides extremely high throughput and low latency messaging, making it suitable for real-time applications and high-frequency trading systems.

### Subject-Based Messaging

Uses NATS subject-based messaging where messages are published to subjects (similar to topics) for efficient message routing and delivery.

### Cloud-Native Design

NATS is designed for cloud-native environments with features like:

-   Horizontal scaling capabilities
    
-   Fault tolerance and high availability
    
-   Multi-tenancy support
    
-   Service mesh integration
    

### Authentication and Security

Supports various authentication mechanisms and secure connections for enterprise deployments and sensitive data scenarios.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-sink.kamelet.yaml)