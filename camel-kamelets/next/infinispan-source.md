# ![infinispan source](_images/kamelets/infinispan-source.svg) Infinispan Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Get Events from an Infinispan cache

## Configuration Options

The following table summarizes the configuration options available for the `infinispan-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **cacheName** | Cache Name | **Required** The name of the Infinispan cache to use. | string |  |  |
| **hosts** | Hosts | **Required** Specifies the host of the cache on Infinispan instance. | string |  |  |
| **password** | Password | **Required** Password to connect to Infinispan. | string |  |  |
| **username** | Username | **Required** Username to connect to Infinispan. | string |  |  |
| **eventTypes** | Infinispan Cluster Name | Specifies the set of event types to register by the consumer. Multiple event can be separated by comma without spaces. Enum values: \* CLIENT\_CACHE\_ENTRY\_CREATED \* CLIENT\_CACHE\_ENTRY\_MODIFIED \* CLIENT\_CACHE\_ENTRY\_REMOVED \* CLIENT\_CACHE\_ENTRY\_EXPIRED \* CLIENT\_CACHE\_FAILOVER | string | CLIENT\_CACHE\_ENTRY\_CREATED,CLIENT\_CACHE\_ENTRY\_MODIFIED,CLIENT\_CACHE\_ENTRY\_REMOVED,CLIENT\_CACHE\_ENTRY\_EXPIRED,CLIENT\_CACHE\_FAILOVER | CLIENT\_CACHE\_ENTRY\_CREATED,CLIENT\_CACHE\_ENTRY\_MODIFIED |
| **saslMechanism** | SASL Mechanism | The SASL Mechanism to use. | string | DIGEST-MD5 |  |
| **secure** | Secure | If the Infinispan instance is secured or not. | boolean | true |  |
| **securityRealm** | Security Realm | Define the security realm to access the infinispan instance. | string | default |  |
| **securityServerName** | Security Server name | Define the security server name to access the infinispan instance. | string | infinispan |  |

## Dependencies

At runtime, the `infinispan-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
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
    
-   Optionally, security settings (secure connection enabled by default)
    

### Output format

The Kamelet gets events from an Infinispan cache and produces the event data in the configured format.

### Configuration

The Kamelet requires the following parameters:

-   `cacheName`: The name of the Infinispan cache to use
    
-   `hosts`: Specifies the host of the cache on Infinispan instance
    
-   `username`: Username to connect to Infinispan
    
-   `password`: Password to connect to Infinispan
    

Optional parameters: - `secure`: If the Infinispan instance is secured or not (default: true)

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