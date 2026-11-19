# ![infinispan sink](_images/kamelets/infinispan-sink.svg) Infinispan Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores the body of each message under a key in a cache of a remote Infinispan server, or in Red Hat Data Grid, or removes the entry of the key.

Use it to share data between applications through an Infinispan cache, for example the latest status of each order or a lookup table that other services read, or to keep an entry only for a while, such as a session. To react to the changes in a cache, use `infinispan-source`.

Input: the body is the value to store, as text. The `key` header (or `ce-key`) is the key; without one, a new unique id is used as the key, so each message adds a new entry. What is done depends on `operation`. By default (`PUT`), a value that is already under the key is replaced. `PUTIFABSENT` keeps a value that is already there, and `REPLACE` stores the body only under a key that has a value. `REMOVE` deletes the entry of the key: with an empty body always, and with a body only when the value stored is equal to the body.

Output: when it is used inside a route, the message has no body afterwards. With `REMOVE` and a body, the body afterwards is `true` when the entry was deleted and `false` when it was not.

Good to know: the cache must already exist on the server. A body that the Infinispan client cannot store, such as a Map, fails the message; turn it into JSON text first, for example with `json-serialize-action`. With `lifespan` or `maxIdle`, the entries are removed after that time. Recent Infinispan servers do not accept the default `saslMechanism` of `DIGEST-MD5`: set it to `SCRAM-SHA-512`. The connection has TLS only when `sslTruststoreLocation` is set, together with `sslSniHostName`. Headers that start with `CamelInfinispan` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `infinispan-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **cacheName** | Cache Name | **Required** The name of the cache to store the values in. It must exist on the server. | string |  | orders |
| **hosts** | Hosts | **Required** The address of the Infinispan server, as `host:port`. The Hot Rod port of Infinispan is 11222 by default. | string |  | infinispan.example.com:11222 |
| **password** | Password | **Required** The password of the Infinispan user in `username`. | string |  |  |
| **username** | Username | **Required** The Infinispan user to log in as. | string |  |  |
| **lifespan** | Lifespan | How long an entry stays in the cache after it is stored, in the unit of `lifespanTimeUnit`. The entry is then removed. When it is not set, the entry does not expire, unless the cache on the server sets a lifespan. Not used with `REMOVE`. | integer |  | 60 |
| **lifespanTimeUnit** | Lifespan Time Unit | The unit of `lifespan`. Only used when `lifespan` is set. Enum values: \* MILLISECONDS \* SECONDS \* MINUTES \* HOURS \* DAYS | string | SECONDS |  |
| **maxIdle** | Max Idle Time | How long an entry stays in the cache when it is not read or written, in the unit of `maxIdleTimeUnit`. The entry is then removed. It works with or without `lifespan`. When it is not set, an entry is not removed for being idle, unless the cache on the server sets it. Not used with `REMOVE`. | integer |  | 300 |
| **maxIdleTimeUnit** | Max Idle Time Unit | The unit of `maxIdle`. Only used when `maxIdle` is set. Enum values: \* MILLISECONDS \* SECONDS \* MINUTES \* HOURS \* DAYS | string | SECONDS |  |
| **operation** | Operation | What to do with each message. `PUT` stores the body under the key, and replaces a value that is already there. `PUTIFABSENT` stores it only when the key has no value yet. `REPLACE` stores it only when the key already has a value. `REMOVE` deletes the entry of the key; with a body, it deletes it only when the value stored is equal to the body. When it is not set, `PUT` is used. Enum values: \* PUT \* PUTIFABSENT \* REPLACE \* REMOVE | string |  | REMOVE |
| **saslMechanism** | SASL Mechanism | How the user and password are checked by the server. Recent Infinispan servers accept `SCRAM-SHA-512`, `SCRAM-SHA-256` or `DIGEST-SHA-512`, but not the default `DIGEST-MD5`. | string | DIGEST-MD5 | SCRAM-SHA-512 |
| **secure** | Secure | If true, it logs in with `username` and `password`. Set it to false only for a server that needs no login. It does not turn on TLS; `sslTruststoreLocation` does. | boolean | true |  |
| **securityRealm** | Security Realm | The security realm of the server that holds the user. Keep the default unless your Infinispan administrator set up another realm. | string | default |  |
| **securityServerName** | Security Server Name | The name of the server, used when logging in. Keep the default unless your Infinispan administrator changed it. | string | infinispan |  |
| **sslSniHostName** | TLS Server Name | The host name of the server as its certificate names it, such as `infinispan.example.com`. Required with `sslTruststoreLocation`. It is sent to the server when the connection starts (SNI), and the certificate of the server must be for this name, or the connection fails. Setting it without `sslTruststoreLocation` fails at start. | string |  | infinispan.example.com |
| **sslTruststoreLocation** | Trust Store Location | The path of a file with the certificate of the server, or of the authority that signed it, to connect with TLS. It is a trust store in PKCS12 or JKS format, which needs `sslTruststorePassword`, or a PEM file with the certificates, such as `ca.crt`, which needs no password. Setting it turns on TLS, and `sslSniHostName` is then required. The Infinispan client does not use the certificates that Java trusts by default, so a server with a certificate from a public authority needs this file too. When it is not set, the connection has no TLS. | string |  | /etc/infinispan/truststore.p12 |
| **sslTruststorePassword** | Trust Store Password | The password of the trust store file in `sslTruststoreLocation`. Not needed for a PEM file. | string |  |  |

## Dependencies

At runtime, the `infinispan-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:infinispan
    

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
            uri: "kamelet:infinispan-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Infinispan Sink Kamelet Description

### Authentication

This Kamelet uses username and password authentication to connect to Infinispan cache instances.

### Security Configuration

-   **Authentication**: Enabled by default (secure: true). It is a login with username and password, not TLS.
    
-   **TLS**: Off by default. It is on when **sslTruststoreLocation** is set, and **sslSniHostName** is then required. See [Example with TLS and Expiration](#infinispan-sink-tls).
    
-   **SASL Mechanism**: DIGEST-MD5 (default). Recent Infinispan servers do not accept it: set `saslMechanism` to `SCRAM-SHA-512`.
    
-   **Security Realm**: "default" realm
    
-   **Security Server Name**: "infinispan" (default)
    

### Required Configuration

-   **Cache Name**: The name of the Infinispan cache to use
    
-   **Hosts**: Host address of the Infinispan instance
    
-   **Username and Password**: Credentials for authentication
    

### Cache Operations

The body of each message is stored as the value in the specified cache, which must already exist on the server. The key comes from a header, or is a new unique id.

The **operation** option sets what is done with each message:

 
| Operation | What it does |
| --- | --- |
| `PUT` (when not set) | Stores the body under the key, and replaces a value that is already there. |
| `PUTIFABSENT` | Stores the body only when the key has no value yet. |
| `REPLACE` | Stores the body only when the key already has a value. |
| `REMOVE` | Deletes the entry of the key. With an empty body, it is always deleted. With a body, it is deleted only when the value stored is equal to the body, and the body afterwards is `true` or `false`. |

### Expiration

With **lifespan**, an entry is removed that long after it is stored. With **maxIdle**, an entry is removed when it has not been read or written for that long. Both are in seconds unless **lifespanTimeUnit** or **maxIdleTimeUnit** says otherwise, and they can be used together. They apply to `PUT`, `PUTIFABSENT` and `REPLACE`.

### Example with TLS and Expiration

The Infinispan client checks the certificate of the server against the file in **sslTruststoreLocation** only: it does not use the certificates that Java trusts by default. The file is a PKCS12 or JKS trust store with its password, or a PEM file such as the `ca.crt` of the server, without a password. **sslSniHostName** is the host name the certificate of the server is for.

```yaml
- route:
    from:
      uri: "kafka:sessions"
      steps:
        - setHeader:
            name: key
            simple: "$\{header.kafka.KEY}"
        - to:
            uri: "kamelet:infinispan-sink"
            parameters:
              cacheName: "sessions"
              hosts: "infinispan.example.com:11222"
              username: "camel"
              password: "secret"
              saslMechanism: "SCRAM-SHA-512"
              sslTruststoreLocation: "/etc/infinispan/ca.crt"
              sslSniHostName: "infinispan.example.com"
              lifespan: 30
              lifespanTimeUnit: "MINUTES"
```

Each record is stored under its Kafka key, over TLS, and removed from the cache 30 minutes later.

To delete entries instead, set `operation: "REMOVE"` and send messages with an empty body and the `key` header.

### Optional Headers

-   `key` / `ce-key`: Specify the cache key for the object
    

If no key is provided in headers, the Kamelet uses a new unique id (the id of the message) as the cache key, so each such message adds a new entry.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/infinispan-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/infinispan-sink.kamelet.yaml)