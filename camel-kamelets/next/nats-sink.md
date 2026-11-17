# ![nats sink](_images/kamelets/nats-sink.svg) NATS Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Publishes each message to a subject on a NATS server, or to a JetStream stream that stores the messages.

Use it to send events or commands to services that listen on NATS, such as microservices or edge devices. Use `nats-source` to receive them.

Input: the body is the payload, as text or bytes. A Map is sent as its Java text form, such as `{a=1, b=x}`, so turn it into JSON text first, for example with `json-serialize-action`. Headers of the message, such as `Content-Type`, are sent as NATS headers.

Output: the message is unchanged.

Good to know: a plain NATS subject stores nothing: only the receivers subscribed at that moment get the message. With `jetstreamEnabled`, the message is stored in the stream `jetstreamName`, which must exist already, for example created by `nats-source`; otherwise sending fails. It connects with no TLS, and the integration fails to start when no server can be reached. It publishes the message and does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does.

## Configuration Options

The following table summarizes the configuration options available for the `nats-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **servers** | Servers | **Required** The addresses of one or more NATS servers, as `host:port` or `nats://host:port`, separated by commas. The usual NATS port is 4222. For a server that needs a login, put the user and password in the address, as `nats://user:password@host:4222`. | string |  | nats://localhost:4222 |
| **topic** | Subject | **Required** The NATS subject to publish the messages to. | string |  | orders.created |
| **jetstreamAsync** | JetStream Async | If true, JetStream calls are made without blocking a thread while waiting for the server to answer. Only used when `jetstreamEnabled` is true. | boolean | true |  |
| **jetstreamEnabled** | JetStream Enabled | If true, each message is published to the JetStream stream `jetstreamName`, which stores it, instead of to plain NATS. The stream must exist and take in the subject in `topic`. | boolean | false |  |
| **jetstreamName** | JetStream Stream Name | The name of the JetStream stream that stores the messages. Only used when `jetstreamEnabled` is true. | string |  | ORDERS |

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

NATS supports various authentication mechanisms and secure connections. This Kamelet takes a user and password in the server address, as `nats://user:password@host:4222`, and has no options for TLS or for other kinds of login.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-sink.kamelet.yaml)