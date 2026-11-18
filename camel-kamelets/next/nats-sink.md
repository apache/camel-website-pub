# ![nats sink](_images/kamelets/nats-sink.svg) NATS Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Publishes each message to a subject on a NATS server, or to a JetStream stream that stores the messages.

Use it to send events or commands to services that listen on NATS, such as microservices or edge devices. Use `nats-source` to receive them.

Input: the body is the payload, as text or bytes. A Map is sent as its Java text form, such as `{a=1, b=x}`, so turn it into JSON text first, for example with `json-serialize-action`. Headers of the message, such as `Content-Type`, are sent as NATS headers.

Output: the message is unchanged.

Good to know: a plain NATS subject stores nothing: only the receivers subscribed at that moment get the message. With `jetstreamEnabled`, the message is stored in the stream `jetstreamName`, which must exist already, for example created by `nats-source`; otherwise sending fails. It connects with TLS when `secure` is true. The certificate of the server is checked against the certificate authorities that Java trusts. To trust a private one with Camel JBang or Camel Main, set the application properties `camel.ssl.enabled=true`, `camel.ssl.trustStore`, `camel.ssl.trustStorePassword` and `camel.component.nats.useGlobalSslContextParameters=true`: that trust store then replaces the one of Java for every NATS connection of the application that has `secure` set. The integration fails to start when no server can be reached, or when the server refuses the login. It publishes the message and does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does.

## Configuration Options

The following table summarizes the configuration options available for the `nats-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **servers** | Servers | **Required** The addresses of one or more NATS servers, as `host:port` or `nats://host:port`, separated by commas. The usual NATS port is 4222. For a server that needs a login, put the user and password in the address, as `nats://user:password@host:4222`, or a token, as `nats://token@host:4222`. To log in with a NATS credentials file instead, use `credentialsFilePath`. | string |  | nats://localhost:4222 |
| **topic** | Subject | **Required** The NATS subject to publish the messages to. | string |  | orders.created |
| **credentialsFilePath** | Credentials File | A NATS credentials file (`.creds`) to log in with, which holds a user JWT and the NKey seed of the user. Servers with decentralized authentication, such as Synadia Cloud, use it. Start it with `file:` followed by the path of the file, or with `classpath:`, `http:` or `https:`. The `nsc generate creds` command makes one. A file that does not exist makes the integration fail to start, and a user that the server does not know is refused with `Authorization Violation`. | string |  | file:/etc/nats/user.creds |
| **jetstreamAsync** | JetStream Async | If true, JetStream calls are made without blocking a thread while waiting for the server to answer. Only used when `jetstreamEnabled` is true. | boolean | true |  |
| **jetstreamEnabled** | JetStream Enabled | If true, each message is published to the JetStream stream `jetstreamName`, which stores it, instead of to plain NATS. The stream must exist and take in the subject in `topic`. | boolean | false |  |
| **jetstreamName** | JetStream Stream Name | The name of the JetStream stream that stores the messages. Only used when `jetstreamEnabled` is true. | string |  | ORDERS |
| **secure** | Secure (TLS) | If true, it connects with TLS, which a server with TLS in its configuration requires; without it, such a server refuses the connection with `SSL required by server`. The certificate of the server is checked against the certificate authorities that Java trusts, or against the trust store set in the `camel.ssl` application properties when `camel.component.nats.useGlobalSslContextParameters` is true. An address that starts with `tls://` also connects with TLS, but uses that trust store only when `secure` is true. When not set, it connects with TLS only to a `tls://` address. | boolean |  |  |

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
    

### Login

For a server that needs a user and password, put them in the address in `servers`, as `nats://user:password@host:4222`, or put a token there, as `nats://token@host:4222`.

For a server with decentralized authentication, such as Synadia Cloud, log in with a NATS credentials file (`.creds`), which holds a user JWT and the NKey seed of the user. Set its location in `credentialsFilePath`, as `file:` followed by the path of the file. The `nsc generate creds` command makes one:

```bash
nsc generate creds --account APP --name app-user > app-user.creds
```

### TLS with a Private Certificate Authority

With `secure: true` the Kamelet connects with TLS, which a server with TLS in its configuration requires, and checks the certificate of the server against the certificate authorities that Java trusts. When the server has a certificate from a private or self-signed authority, put the certificate of that authority in a trust store file (JKS or PKCS12):

```bash
keytool -importcert -alias nats-ca -file ca.pem -keystore truststore.p12 -storetype PKCS12 -storepass changeit
```

The Kamelet has no option for the trust store. Set it in the application properties, as the global TLS settings of Camel, and tell the NATS component to use them. With Camel JBang or Camel Main, in `application.properties`:

```properties
camel.ssl.enabled=true
camel.ssl.trustStore=file:/etc/nats/truststore.p12
camel.ssl.trustStorePassword=changeit
camel.component.nats.useGlobalSslContextParameters=true
```

That trust store then replaces the one of Java for every NATS connection of the application that has `secure` set. An address that starts with `tls://` also connects with TLS, but it uses that trust store only when `secure` is true.

### Example with TLS and a Credentials File

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "hello"
        period: 5000
      steps:
        - to:
            uri: "kamelet:nats-sink"
            parameters:
              servers: "tls://nats.example.com:4222"
              topic: "orders.created"
              secure: true
              credentialsFilePath: "file:/etc/nats/app-user.creds"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-sink.kamelet.yaml)