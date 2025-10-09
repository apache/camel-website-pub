# ![pqc signature action](_images/kamelets/pqc-signature-action.svg) PQC Signature Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sign or verify a payload with a Post-Quantum Cryptography (PQC) algorithm.

## Configuration Options

The following table summarizes the configuration options available for the `pqc-signature-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **operation** | PQC Signature Operation | **Required** The PQC Signature Operation to be performed. Enum values: \* sign \* verify | string |  |  |
| **signatureAlgorithm** | PQC Signature Algorithm | **Required** The PQC Signature Algorithm to be used. Enum values: \* MLDSA" \* SLHDSA \* LMS \* XMSS \* FALCON \* PICNIC | string |  |  |

## Dependencies

At runtime, the `pqc-signature-action` Kamelet relies upon the presence of the following dependencies:

-   camel:http
    
-   camel:kamelet
    
-   camel:core
    

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
            uri: "kamelet:pqc-signature-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pqc-signature-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pqc-signature-action.kamelet.yaml)