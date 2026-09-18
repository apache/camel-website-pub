# ![crypto encrypt action](_images/kamelets/crypto-encrypt-action.svg) Crypto Encrypt Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Encrypt the payload using the Java Cryptographic Extension (JCE) and a fixed key.

## Configuration Options

The following table summarizes the configuration options available for the `crypto-encrypt-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **algorithm** | Algorithm | **Required** The JCE algorithm name indicating the cryptographic algorithm that will be used. | string |  | AES |
| **key** | Secret Key | **Required** The secret key to use to encrypt the payload. The length must match the requirements of the selected algorithm (for example 16, 24 or 32 bytes for AES). | string |  |  |

## Dependencies

At runtime, the `crypto-encrypt-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    
-   camel:crypto
    

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
            uri: "kamelet:crypto-encrypt-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/crypto-encrypt-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/crypto-encrypt-action.kamelet.yaml)