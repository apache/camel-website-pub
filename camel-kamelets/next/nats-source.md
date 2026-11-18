# ![nats source](_images/kamelets/nats-source.svg) NATS Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message published to a subject on a NATS server, or stored in a JetStream stream.

Use it to react to events or commands that services publish on NATS. Use `nats-sink` to publish them.

Output: the body is the payload, as bytes, unchanged. The `CamelNatsSubject` header is the subject, and the NATS headers of the message become headers too.

Good to know: without JetStream, it receives only the messages published while it is connected. With `jetstreamEnabled`, it creates the stream `jetstreamName` for the subject when it does not exist, and each time it starts it reads the stream from the beginning, so messages already read are received again. When several copies of the integration run, each copy receives every message, unless they share a `queueName`: then each message goes to only one of them. This works only without JetStream. It connects with TLS when `secure` is true. The certificate of the server is checked against the certificate authorities that Java trusts. To trust a private one with Camel JBang or Camel Main, set the application properties `camel.ssl.enabled=true`, `camel.ssl.trustStore`, `camel.ssl.trustStorePassword` and `camel.component.nats.useGlobalSslContextParameters=true`: that trust store then replaces the one of Java for every NATS connection of the application that has `secure` set. The integration fails to start when no server can be reached, or when the server refuses the login.

## Configuration Options

The following table summarizes the configuration options available for the `nats-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **servers** | Servers | **Required** The addresses of one or more NATS servers, as `host:port` or `nats://host:port`, separated by commas. The usual NATS port is 4222. For a server that needs a login, put the user and password in the address, as `nats://user:password@host:4222`, or a token, as `nats://token@host:4222`. To log in with a NATS credentials file instead, use `credentialsFilePath`. | string |  | nats://localhost:4222 |
| **topic** | Subject | **Required** The NATS subject to receive the messages from. | string |  | orders.created |
| **credentialsFilePath** | Credentials File | A NATS credentials file (`.creds`) to log in with, which holds a user JWT and the NKey seed of the user. Servers with decentralized authentication, such as Synadia Cloud, use it. Start it with `file:` followed by the path of the file, or with `classpath:`, `http:` or `https:`. The `nsc generate creds` command makes one. A file that does not exist makes the integration fail to start, and a user that the server does not know is refused with `Authorization Violation`. | string |  | file:/etc/nats/user.creds |
| **jetstreamAsync** | JetStream Async | If true, JetStream calls are made without blocking a thread while waiting for the server to answer. Only used when `jetstreamEnabled` is true. | boolean | true |  |
| **jetstreamEnabled** | JetStream Enabled | If true, the messages are read from the JetStream stream `jetstreamName`, which keeps them, instead of from plain NATS. The stream is created for the subject in `topic` when it does not exist. | boolean | false |  |
| **jetstreamName** | JetStream Stream Name | The name of the JetStream stream that stores the messages. Only used when `jetstreamEnabled` is true. | string |  | ORDERS |
| **queueName** | Queue Group | The name of a NATS queue group to join. The subscribers of `topic` that use the same queue group share its messages: each message goes to only one of them. Set the same name on every copy of the integration when you run several of them, so that each message is processed once; without it, each copy receives every message. Only used without JetStream: with `jetstreamEnabled`, each copy still receives every message of the stream. | string |  | order-workers |
| **secure** | Secure (TLS) | If true, it connects with TLS, which a server with TLS in its configuration requires; without it, such a server refuses the connection with `SSL required by server`. The certificate of the server is checked against the certificate authorities that Java trusts, or against the trust store set in the `camel.ssl` application properties when `camel.component.nats.useGlobalSslContextParameters` is true. An address that starts with `tls://` also connects with TLS, but uses that trust store only when `secure` is true. When not set, it connects with TLS only to a `tls://` address. | boolean |  |  |

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

### Login

For a server that needs a user and password, put them in the address in `servers`, as `nats://user:password@host:4222`, or put a token there, as `nats://token@host:4222`.

For a server with decentralized authentication, such as Synadia Cloud, log in with a NATS credentials file (`.creds`), which holds a user JWT and the NKey seed of the user. Set its location in `credentialsFilePath`, as `file:` followed by the path of the file. The `nsc generate creds` command makes one.

### TLS with a Private Certificate Authority

With `secure: true` the Kamelet connects with TLS, which a server with TLS in its configuration requires, and checks the certificate of the server against the certificate authorities that Java trusts. When the server has a certificate from a private or self-signed authority, put the certificate of that authority in a trust store file (JKS or PKCS12), and set it in the application properties, as the global TLS settings of Camel. With Camel JBang or Camel Main, in `application.properties`:

```properties
camel.ssl.enabled=true
camel.ssl.trustStore=file:/etc/nats/truststore.p12
camel.ssl.trustStorePassword=changeit
camel.component.nats.useGlobalSslContextParameters=true
```

That trust store then replaces the one of Java for every NATS connection of the application that has `secure` set. An address that starts with `tls://` also connects with TLS, but it uses that trust store only when `secure` is true.

### Running several copies: queue groups

Each copy of the integration receives every message of the subject. To share the messages instead, so that each message is processed by only one copy, give every copy the same `queueName`. NATS then delivers each message to one member of the queue group. This works only without JetStream: with `jetstreamEnabled`, each copy still receives every message of the stream.

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

### Example with TLS, a Credentials File and a Queue Group

```yaml
- route:
    from:
      uri: "kamelet:nats-source"
      parameters:
        servers: "tls://nats.example.com:4222"
        topic: "orders.created"
        secure: true
        credentialsFilePath: "file:/etc/nats/app-user.creds"
        queueName: "order-workers"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/nats-source.kamelet.yaml)