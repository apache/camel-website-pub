# ![nats source](_images/kamelets/nats-source.svg) NATS Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message published to a subject on a NATS server, or stored in a JetStream stream.

Use it to react to events or commands that services publish on NATS. Use `nats-sink` to publish them.

Output: the body is the payload, as bytes, unchanged. The `CamelNatsSubject` header is the subject, and the NATS headers of the message become headers too.

Good to know: without JetStream, it receives only the messages published while it is connected. With `jetstreamEnabled`, it creates the stream `jetstreamName` for the subject when it does not exist, and each time it starts it reads the stream from the beginning, so messages already read are received again. The integration fails to start when no server can be reached.

## Configuration Options

The following table summarizes the configuration options available for the `nats-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **servers** | Servers | **Required** The addresses of one or more NATS servers, as `host:port` or `nats://host:port`, separated by commas. The usual NATS port is 4222. For a server that needs a login, put the user and password in the address, as `nats://user:password@host:4222`. | string |  | nats://localhost:4222 |
| **topic** | Subject | **Required** The NATS subject to receive the messages from. | string |  | orders.created |
| **jetstreamAsync** | JetStream Async | If true, JetStream calls are made without blocking a thread while waiting for the server to answer. Only used when `jetstreamEnabled` is true. | boolean | true |  |
| **jetstreamEnabled** | JetStream Enabled | If true, the messages are read from the JetStream stream `jetstreamName`, which keeps them, instead of from plain NATS. The stream is created for the subject in `topic` when it does not exist. | boolean | false |  |
| **jetstreamName** | JetStream Stream Name | The name of the JetStream stream that stores the messages. Only used when `jetstreamEnabled` is true. | string |  | ORDERS |

## Dependencies

At runtime, the `nats-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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
      uri: "kamelet:nats-source"
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

## NATS Source Kamelet Description

### Authentication

The Kamelet has no login options. For a server that needs a user and password, put them in the address in `servers`, as `nats://user:password@host:4222`. The Kamelet has no TLS options.

### Output format

The body is the NATS payload, unchanged, as bytes; it is not turned into JSON. The `CamelNatsSubject` header is the subject, and the NATS headers of the message become headers too.

### JetStream

With `jetstreamEnabled` set to true, the Kamelet reads from the JetStream stream `jetstreamName`, and creates it for the subject in `topic` when it does not exist. Each time it starts, it reads the stream from the beginning.

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:nats-source"
      parameters:
        servers: "nats://localhost:4222"
        topic: "orders.created"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-source.kamelet.yaml)