# PQC (Post-Quantum Cryptography)

**Since Camel 4.16**

The PQC data format supports encrypting and decrypting payload using Post Quantum Cryptography algorithms.

## PGC DataFormat Options

The PQC (Post-Quantum Cryptography) dataformat supports 7 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **keyEncapsulationAlgorithm** (common) | `MLKEM` | `Enum` | 
The Post-Quantum KEM algorithm to use for key encapsulation. Supported values: MLKEM, BIKE, HQC, CMCE, SABER, FRODO, NTRU, NTRULPRime, SNTRUPrime, KYBER.

Enum values:

-   MLKEM
    
-   BIKE
    
-   HQC
    
-   CMCE
    
-   SABER
    
-   FRODO
    
-   NTRU
    
-   NTRULPRime
    
-   SNTRUPrime
    
-   KYBER
    





 |
| **symmetricKeyAlgorithm** (common) | `AES` | `Enum` | 

The symmetric encryption algorithm to use with the shared secret. Supported values: AES, ARIA, RC2, RC5, CAMELLIA, CAST5, CAST6, CHACHA7539, etc.

Enum values:

-   AES
    
-   ARIA
    
-   RC2
    
-   RC5
    
-   CAMELLIA
    
-   CAST5
    
-   CAST6
    
-   CHACHA7539
    
-   DSTU7624
    
-   GOST28147
    
-   GOST3412\_2015
    
-   GRAIN128
    
-   HC128
    
-   HC256
    
-   SALSA20
    
-   SEED
    
-   SM4
    
-   DESEDE
    





 |
| **symmetricKeyLength** (common) | `128` | `Integer` | The length (in bits) of the symmetric key. |
| **keyPair** (common) |  | `Object` | Refers to the KeyPair to lookup from the register to use for KEM operations. |
| **bufferSize** (advanced) | `4096` | `Integer` | The size of the buffer used for streaming encryption/decryption. |
| **provider** (advanced) |  | `String` | The JCE security provider to use. |
| **keyGenerator** (advanced) |  | `Object` | Refers to a custom KeyGenerator to lookup from the register for KEM operations. |

## Spring Boot Auto-Configuration

When using pqc with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-pqc-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 26 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.pqc.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.pqc.configuration** | Component configuration. The option is a org.apache.camel.component.pqc.PQCConfiguration type. |  | PQCConfiguration |
| **camel.component.pqc.enabled** | Whether to enable auto configuration of the pqc component. This is enabled by default. |  | Boolean |
| **camel.component.pqc.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.pqc.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.pqc.key-encapsulation-algorithm** | In case there is no keyGenerator, we specify an algorithm to build the KeyGenerator. |  | String |
| **camel.component.pqc.key-generator** | The Key Generator to be used in encapsulation and extraction. The option is a javax.crypto.KeyGenerator type. |  | KeyGenerator |
| **camel.component.pqc.key-pair** | The KeyPair to be used. The option is a java.security.KeyPair type. |  | KeyPair |
| **camel.component.pqc.key-pair-alias** | A KeyPair alias to use in combination with KeyStore parameter. |  | String |
| **camel.component.pqc.key-store** | A KeyStore where we could get Cryptographic material. The option is a java.security.KeyStore type. |  | KeyStore |
| **camel.component.pqc.key-store-password** | The KeyStore password to use in combination with KeyStore Parameter. |  | String |
| **camel.component.pqc.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.pqc.operation** | The operation to perform. |  | PQCOperations |
| **camel.component.pqc.signature-algorithm** | In case there is no signer, we specify an algorithm to build the KeyPair or the Signer. |  | String |
| **camel.component.pqc.signer** | The Signer to be used. The option is a java.security.Signature type. |  | Signature |
| **camel.component.pqc.store-extracted-secret-key-as-header** | In the context of extractSecretKeyFromEncapsulation operation, this option define if we want to have the key set as header. | false | Boolean |
| **camel.component.pqc.symmetric-key-algorithm** | In case we are using KEM operations, we need a Symmetric algorithm to be defined for the flow to work. |  | String |
| **camel.component.pqc.symmetric-key-length** | The required length of the symmetric key used. | 128 | Integer |
| **camel.dataformat.pqc.buffer-size** | The size of the buffer used for streaming encryption/decryption. | 4096 | Integer |
| **camel.dataformat.pqc.enabled** | Whether to enable auto configuration of the pqc data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.pqc.key-encapsulation-algorithm** | The Post-Quantum KEM algorithm to use for key encapsulation. Supported values: MLKEM, BIKE, HQC, CMCE, SABER, FRODO, NTRU, NTRULPRime, SNTRUPrime, KYBER. | MLKEM | String |
| **camel.dataformat.pqc.key-generator** | Refers to a custom KeyGenerator to lookup from the register for KEM operations. The option is a javax.crypto.KeyGenerator type. |  | String |
| **camel.dataformat.pqc.key-pair** | Refers to the KeyPair to lookup from the register to use for KEM operations. The option is a java.security.KeyPair type. |  | String |
| **camel.dataformat.pqc.provider** | The JCE security provider to use. |  | String |
| **camel.dataformat.pqc.symmetric-key-algorithm** | The symmetric encryption algorithm to use with the shared secret. Supported values: AES, ARIA, RC2, RC5, CAMELLIA, CAST5, CAST6, CHACHA7539, etc. | AES | String |
| **camel.dataformat.pqc.symmetric-key-length** | The length (in bits) of the symmetric key. | 128 | Integer |