# ![pqc kem action](_images/kamelets/pqc-kem-action.svg) PQC Key Encapsulation/Decapsulation Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Encapsulate or Decapsulate a secret Key with a Post-Quantum Cryptography Key Encapsulation Mechanism (PQC KEM) algorithm.

## Configuration Options

The following table summarizes the configuration options available for the `pqc-kem-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **keyEncapsulationAlgorithm** | PQC Key Encapsulation Algorithm | **Required** The PQC Key Encapsulation Algorithm to be used. Enum values: \* MLKEM \* BIKE \* HQC \* CMCE \* SABER \* FRODO \* NTRU \* NTRULPRime | string |  |  |
| **operation** | PQC KEM Operation | **Required** The PQC KEM Operation to be performed. Enum values: \* generateSecretKeyEncapsulation \* extractSecretKeyEncapsulation \* extractSecretKeyFromEncapsulation | string |  |  |
| **symmetricKeyAlgorithm** | Symmetric Key Algorithm | **Required** The Symmetric Key Algorithm to be used in KEM operations. Enum values: \* AES \* RC2 \* RC5 \* ARIA \* CAMELLIA \* CAST5 \* CAST6 \* CHACHA7539 \* DSTU7624 \* GOST28147 \* GOST3412\_2015 \* GRAIN128 \* HC128 \* HC256 \* SALSA20 \* SEED \* SM4 \* DESEDE | string |  |  |

## Dependencies

At runtime, the `pqc-kem-action` Kamelet relies upon the presence of the following dependencies:

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