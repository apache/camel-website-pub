# ![infinispan sink](_images/kamelets/infinispan-sink.svg) Infinispan Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores the body of each message under a key in a cache of a remote Infinispan server, or in Red Hat Data Grid.

Use it to share data between applications through an Infinispan cache, for example the latest status of each order or a lookup table that other services read. To react to the changes in a cache, use `infinispan-source`.

Input: the body is the value to store, as text. The `key` header (or `ce-key`) is the key; without one, a new unique id is used as the key, so each message adds a new entry. A value that is already under the key is replaced.

Output: when it is used inside a route, the message has no body afterwards.

Good to know: the cache must already exist on the server. A body that the Infinispan client cannot store, such as a Map, fails the message; turn it into JSON text first, for example with `json-serialize-action`. Recent Infinispan servers do not accept the default `saslMechanism` of `DIGEST-MD5`: set it to `SCRAM-SHA-512`. The connection has no TLS.

## Configuration Options

The following table summarizes the configuration options available for the `infinispan-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **cacheName** | Cache Name | **Required** The name of the cache to store the values in. It must exist on the server. | string |  | orders |
| **hosts** | Hosts | **Required** The address of the Infinispan server, as `host:port`. The Hot Rod port of Infinispan is 11222 by default. | string |  | infinispan.example.com:11222 |
| **password** | Password | **Required** The password of the Infinispan user in `username`. | string |  |  |
| **username** | Username | **Required** The Infinispan user to log in as. | string |  |  |
| **saslMechanism** | SASL Mechanism | How the user and password are checked by the server. Recent Infinispan servers accept `SCRAM-SHA-512`, `SCRAM-SHA-256` or `DIGEST-SHA-512`, but not the default `DIGEST-MD5`. | string | DIGEST-MD5 | SCRAM-SHA-512 |
| **secure** | Secure | If true, it logs in with `username` and `password`. Set it to false only for a server that needs no login. It does not turn on TLS. | boolean | true |  |
| **securityRealm** | Security Realm | The security realm of the server that holds the user. Keep the default unless your Infinispan administrator set up another realm. | string | default |  |
| **securityServerName** | Security Server Name | The name of the server, used when logging in. Keep the default unless your Infinispan administrator changed it. | string | infinispan |  |

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

-   **Authentication**: Enabled by default (secure: true). It is a login with username and password, not TLS: the connection has no TLS.
    
-   **SASL Mechanism**: DIGEST-MD5 (default). Recent Infinispan servers do not accept it: set `saslMechanism` to `SCRAM-SHA-512`.
    
-   **Security Realm**: "default" realm
    
-   **Security Server Name**: "infinispan" (default)
    

### Required Configuration

-   **Cache Name**: The name of the Infinispan cache to use
    
-   **Hosts**: Host address of the Infinispan instance
    
-   **Username and Password**: Credentials for authentication
    

### Cache Operations

The body of each message is stored as the value in the specified cache, which must already exist on the server. The key comes from a header, or is a new unique id.

### Optional Headers

-   `key` / `ce-key`: Specify the cache key for the object
    

If no key is provided in headers, the Kamelet uses a new unique id (the id of the message) as the cache key, so each such message adds a new entry.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/infinispan-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/infinispan-sink.kamelet.yaml)