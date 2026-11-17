# ![pqc kem action](_images/kamelets/pqc-kem-action.svg) PQC Key Encapsulation/Decapsulation Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Creates a new secret key for a symmetric cipher, such as AES, together with its encapsulation by a post-quantum algorithm such as ML-KEM, or takes the secret key back out of such an encapsulation.

Use it to try out post-quantum key establishment (a KEM, key encapsulation mechanism): one step creates a secret key and its encapsulation, the protected form of the key that may be sent to the holder of the private key, and a later step takes the same secret key out of it. To encrypt the messages themselves with a fixed key, use `crypto-encrypt-action`.

Input: for `generateSecretKeyEncapsulation`, any body; it is not used. For `extractSecretKeyEncapsulation` and `extractSecretKeyFromEncapsulation`, the body must be the result of `generateSecretKeyEncapsulation`.

Output: `generateSecretKeyEncapsulation` and `extractSecretKeyEncapsulation` give a Java object that holds the secret key and its encapsulation. `extractSecretKeyFromEncapsulation` gives the secret key, as a Java object. None of them is text or bytes, so the next step must be one that works with Java key objects.

Good to know: the key pair of the post-quantum algorithm is created when the application starts, and no option can set it, so an encapsulation can be opened only by the same running application.

## Configuration Options

The following table summarizes the configuration options available for the `pqc-kem-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **keyEncapsulationAlgorithm** | PQC Key Encapsulation Algorithm | **Required** The post-quantum algorithm that encapsulates the secret key. `MLKEM` (ML-KEM, the NIST standard FIPS 203) is the usual choice. Use the same algorithm in the steps that create and that open an encapsulation. Enum values: \* MLKEM \* BIKE \* HQC \* CMCE \* SABER \* FRODO \* NTRU \* NTRULPRime | string |  |  |
| **operation** | PQC KEM Operation | **Required** What to do with each message. `generateSecretKeyEncapsulation` creates a new secret key and its encapsulation; `extractSecretKeyEncapsulation` gives the encapsulation again; `extractSecretKeyFromEncapsulation` gives the secret key taken out of the encapsulation. Enum values: \* generateSecretKeyEncapsulation \* extractSecretKeyEncapsulation \* extractSecretKeyFromEncapsulation | string |  |  |
| **symmetricKeyAlgorithm** | Symmetric Key Algorithm | **Required** The symmetric cipher the secret key is for, such as `AES`, the usual choice. The cipher must accept a key of the length the Camel PQC component creates (256 bits in recent Camel versions); with one that does not, such as `SEED` or `SM4`, the integration fails to start. Enum values: \* AES \* RC2 \* RC5 \* ARIA \* CAMELLIA \* CAST5 \* CAST6 \* CHACHA7539 \* DSTU7624 \* GOST28147 \* GOST3412\_2015 \* GRAIN128 \* HC128 \* HC256 \* SALSA20 \* SEED \* SM4 \* DESEDE | string |  |  |

## Dependencies

At runtime, the `pqc-kem-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:pqc-kem-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/pqc-kem-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/pqc-kem-action.kamelet.yaml)