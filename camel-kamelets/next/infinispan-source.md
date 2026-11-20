# ![infinispan source](_images/kamelets/infinispan-source.svg) Infinispan Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives an event each time an entry of a cache on a remote Infinispan server, or Red Hat Data Grid, is created, changed, removed or expires, one message per event.

Use it to react to changes in a shared cache, for example to update a search index or notify another service when a value changes. To write to a cache, use `infinispan-sink`.

Output: the message has no body: the event is in headers. `infinispan-event-type` is the kind of event, such as `CLIENT_CACHE_ENTRY_CREATED`, `infinispan-key` the key of the entry, `infinispan-cache-name` the name of the cache and `infinispan-entry-version` the version of the entry. The same values are in `ce-infinispaneventtype`, `ce-infinispankey`, `ce-infinispancachename` and `ce-infinispanentryversion`, and in the `CamelInfinispanEventType`, `CamelInfinispanKey`, `CamelInfinispanCacheName` and `CamelInfinispanEntryVersion` headers, with `CamelInfinispanCommandRetried`. To read the value, look up the key in the cache.

Good to know: only the changes made while the integration runs are received. The cache must already exist on the server. Recent Infinispan servers do not accept the default `saslMechanism` of `DIGEST-MD5`: set it to `SCRAM-SHA-512`. The connection has TLS only when `sslTruststoreLocation` is set, together with `sslSniHostName`.

## Configuration Options

The following table summarizes the configuration options available for the `infinispan-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **cacheName** | Cache Name | **Required** The name of the cache to watch. It must exist on the server. | string |  | orders |
| **hosts** | Hosts | **Required** The address of the Infinispan server, as `host:port`. The Hot Rod port of Infinispan is 11222 by default. | string |  | infinispan.example.com:11222 |
| **password** | Password | **Required** The password of the Infinispan user in `username`. | string |  |  |
| **username** | Username | **Required** The Infinispan user to log in as. | string |  |  |
| **eventTypes** | Event Types | The kinds of events to receive, separated by commas without spaces. `CLIENT_CACHE_ENTRY_CREATED`, `CLIENT_CACHE_ENTRY_MODIFIED`, `CLIENT_CACHE_ENTRY_REMOVED` and `CLIENT_CACHE_ENTRY_EXPIRED` are changes of an entry; `CLIENT_CACHE_FAILOVER` tells that the connection moved to another server of the cluster. Enum values: \* CLIENT\_CACHE\_ENTRY\_CREATED \* CLIENT\_CACHE\_ENTRY\_MODIFIED \* CLIENT\_CACHE\_ENTRY\_REMOVED \* CLIENT\_CACHE\_ENTRY\_EXPIRED \* CLIENT\_CACHE\_FAILOVER | string | CLIENT\_CACHE\_ENTRY\_CREATED,CLIENT\_CACHE\_ENTRY\_MODIFIED,CLIENT\_CACHE\_ENTRY\_REMOVED,CLIENT\_CACHE\_ENTRY\_EXPIRED,CLIENT\_CACHE\_FAILOVER | CLIENT\_CACHE\_ENTRY\_CREATED,CLIENT\_CACHE\_ENTRY\_MODIFIED |
| **saslMechanism** | SASL Mechanism | How the user and password are checked by the server. Recent Infinispan servers accept `SCRAM-SHA-512`, `SCRAM-SHA-256` or `DIGEST-SHA-512`, but not the default `DIGEST-MD5`. | string | DIGEST-MD5 | SCRAM-SHA-512 |
| **secure** | Secure | If true, it logs in with `username` and `password`. Set it to false only for a server that needs no login. It does not turn on TLS; `sslTruststoreLocation` does. | boolean | true |  |
| **securityRealm** | Security Realm | The security realm of the server that holds the user. Keep the default unless your Infinispan administrator set up another realm. | string | default |  |
| **securityServerName** | Security Server Name | The name of the server, used when logging in. Keep the default unless your Infinispan administrator changed it. | string | infinispan |  |
| **sslSniHostName** | TLS Server Name | The host name of the server as its certificate names it, such as `infinispan.example.com`. Required with `sslTruststoreLocation`. It is sent to the server when the connection starts (SNI), and the certificate of the server must be for this name, or the connection fails. Setting it without `sslTruststoreLocation` fails at start. | string |  | infinispan.example.com |
| **sslTruststoreLocation** | Trust Store Location | The path of a file with the certificate of the server, or of the authority that signed it, to connect with TLS. It is a trust store in PKCS12 or JKS format, which needs `sslTruststorePassword`, or a PEM file with the certificates, such as `ca.crt`, which needs no password. Setting it turns on TLS, and `sslSniHostName` is then required. The Infinispan client does not use the certificates that Java trusts by default, so a server with a certificate from a public authority needs this file too. When it is not set, the connection has no TLS. | string |  | /etc/infinispan/truststore.p12 |
| **sslTruststorePassword** | Trust Store Password | The password of the trust store file in `sslTruststoreLocation`. Not needed for a PEM file. | string |  |  |

## Dependencies

At runtime, the `infinispan-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:infinispan-source"
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

## Infinispan Source Kamelet Description

### Authentication methods

This Kamelet uses username and password authentication to connect to Infinispan cache. You need to provide:

-   Username and password for Infinispan authentication
    
-   Host information for the Infinispan instance
    
-   Optionally, security settings (login enabled by default with `secure`; TLS when `sslTruststoreLocation` is set)
    

### Output format

The Kamelet receives an event for each change of an entry in the cache. The message has no body: the event type, the key, the cache name and the version of the entry are in the `infinispan-event-type`, `infinispan-key`, `infinispan-cache-name` and `infinispan-entry-version` headers.

### Configuration

The Kamelet requires the following parameters:

-   `cacheName`: The name of the Infinispan cache to use
    
-   `hosts`: Specifies the host of the cache on Infinispan instance
    
-   `username`: Username to connect to Infinispan
    
-   `password`: Password to connect to Infinispan
    

Optional parameters: - `secure`: If the Infinispan instance is secured or not (default: true) - `sslTruststoreLocation`: A trust store (PKCS12 or JKS, with `sslTruststorePassword`) or a PEM file with the certificate of the server, or of the authority that signed it. Setting it turns on TLS. - `sslSniHostName`: The host name the certificate of the server is for. Required with `sslTruststoreLocation`.

### Example with TLS

The Infinispan client checks the certificate of the server against the file in `sslTruststoreLocation` only: it does not use the certificates that Java trusts by default.

```yaml
- route:
    from:
      uri: "kamelet:infinispan-source"
      parameters:
        cacheName: "orders"
        hosts: "infinispan.example.com:11222"
        username: "camel"
        password: "secret"
        saslMechanism: "SCRAM-SHA-512"
        sslTruststoreLocation: "/etc/infinispan/truststore.p12"
        sslTruststorePassword: "changeit"
        sslSniHostName: "infinispan.example.com"
      steps:
        - to: "log:orders"
```

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: infinispan-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: infinispan-source
    properties:
      cacheName: "my-cache"
      hosts: "infinispan-server:11222"
      username: "{{username}}"
      password: "{{password}}"
      secure: true
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/infinispan-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/infinispan-source.kamelet.yaml)