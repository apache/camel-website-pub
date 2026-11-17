# ![pqc signature action](_images/kamelets/pqc-signature-action.svg) PQC Signature Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Signs each message with a post-quantum digital signature algorithm, such as ML-DSA, or checks the signature of a message signed before.

Use it to try out post-quantum signatures, or to check inside one running application that a message was not changed between two steps: sign it with `operation` set to `sign`, and check it later with a second copy of this Kamelet with `operation` set to `verify` and the same algorithm.

Input: the body is the data to sign or to check, as text, bytes or a stream. To check, the `CamelPQCSignature` header must hold the signature that `sign` set.

Output: the body is unchanged. `sign` sets the `CamelPQCSignature` header to the signature, as bytes. `verify` sets the `CamelPQCVerification` header to true when the signature matches the body, and to false when it does not.

Good to know: the key pair is created when the application starts, and no option can set it, so a signature can be checked only by the same running application, and not after a restart. A `verify` without a `CamelPQCSignature` header fails the message.

## Configuration Options

The following table summarizes the configuration options available for the `pqc-signature-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **operation** | PQC Signature Operation | **Required** What to do with each message. `sign` adds a signature of the body in the `CamelPQCSignature` header; `verify` checks the body against that header and sets `CamelPQCVerification`. Enum values: \* sign \* verify | string |  |  |
| **signatureAlgorithm** | PQC Signature Algorithm | **Required** The post-quantum signature algorithm. `MLDSA` (ML-DSA, the NIST standard FIPS 204) is the usual choice; `SLHDSA` is the hash-based NIST standard. Use the same algorithm to sign and to check. Enum values: \* MLDSA \* SLHDSA \* LMS \* XMSS \* FALCON | string |  |  |

## Dependencies

At runtime, the `pqc-signature-action` Kamelet relies upon the presence of the following dependencies:

-   camel:pqc
    
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