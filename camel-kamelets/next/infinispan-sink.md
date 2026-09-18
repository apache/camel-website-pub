# ![infinispan sink](_images/kamelets/infinispan-sink.svg) Infinispan Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Write object to an Infinispan cache.

## Configuration Options

The following table summarizes the configuration options available for the `infinispan-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **cacheName** | Cache Name | **Required** The name of the Infinispan cache to use. | string |  |  |
| **hosts** | Hosts | **Required** Specifies the host of the cache on Infinispan instance. | string |  |  |
| **password** | Password | **Required** Password to connect to Infinispan. | string |  |  |
| **username** | Username | **Required** Username to connect to Infinispan. | string |  |  |
| **saslMechanism** | SASL Mechanism | The SASL Mechanism to use. | string | DIGEST-MD5 |  |
| **secure** | Secure | If the Infinispan instance is secured or not. | boolean | true |  |
| **securityRealm** | Security Realm | Define the security realm to access the infinispan instance. | string | default |  |
| **securityServerName** | Security Server name | Define the security server name to access the infinispan instance. | string | infinispan |  |

## Dependencies

At runtime, the `infinispan-sink` Kamelet relies upon the presence of the following dependencies:

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

-   **Secure Connection**: Enabled by default (secure: true)
    
-   **SASL Mechanism**: DIGEST-MD5 (default)
    
-   **Security Realm**: "default" realm
    
-   **Security Server Name**: "infinispan" (default)
    

### Required Configuration

-   **Cache Name**: The name of the Infinispan cache to use
    
-   **Hosts**: Host address of the Infinispan instance
    
-   **Username and Password**: Credentials for authentication
    

### Cache Operations

Objects are stored in the specified cache using keys derived from headers or exchange ID.

### Optional Headers

-   `key` / `ce-key`: Specify the cache key for the object
    

If no key is provided in headers, the Kamelet uses the exchange ID as the cache key.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/infinispan-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/infinispan-sink.kamelet.yaml)