# PQC Algorithms

**Since Camel 4.12**

**Only producer is supported**

The PQC component supports signing and verifying payload using Post Quantum Cryptography algorithms, as well as key lifecycle management for Post-Quantum cryptographic keys.

## Features

-   **Digital Signatures** - Sign and verify data using NIST-standardized and experimental PQC signature algorithms
    
-   **Key Encapsulation** - Generate and extract shared secrets using Key Encapsulation Mechanisms (KEM)
    
-   **Key Lifecycle Management** - Generate, rotate, expire, revoke, and manage PQC keys
    
-   **Multiple Implementations** - File-based and in-memory key storage options
    
-   **Key Export/Import** - Convert keys between PEM, DER, PKCS8, and X.509 formats
    

Prerequisites

## URI Format

pqc://label\[?options\]

You can append query options to the URI in the following format:

`?options=value&option2=value&…​`

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The PQC Algorithms component supports 26 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | PQCConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   sign
    
-   verify
    
-   hybridSign
    
-   hybridVerify
    
-   generateSecretKeyEncapsulation
    
-   extractSecretKeyEncapsulation
    
-   extractSecretKeyFromEncapsulation
    
-   hybridGenerateSecretKeyEncapsulation
    
-   hybridExtractSecretKeyEncapsulation
    
-   hybridExtractSecretKeyFromEncapsulation
    
-   getRemainingSignatures
    
-   getKeyState
    
-   deleteKeyState
    
-   generateKeyPair
    
-   exportKey
    
-   importKey
    
-   rotateKey
    
-   getKeyMetadata
    
-   listKeys
    
-   expireKey
    
-   revokeKey
    





 |  | PQCOperations |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **classicalKEMAlgorithm** (advanced) | 

The classical key agreement algorithm to use in hybrid KEM operations.

Enum values:

-   ECDH\_P256
    
-   ECDH\_P384
    
-   ECDH\_P521
    
-   X25519
    
-   X448
    





 |  | String |
| **classicalKeyAgreement** (advanced) | **Autowired** The classical KeyAgreement instance to be used in hybrid KEM operations. |  | KeyAgreement |
| **classicalKeyPair** (advanced) | **Autowired** The classical KeyPair to be used in hybrid operations. |  | KeyPair |
| **classicalSignatureAlgorithm** (advanced) | 

The classical signature algorithm to use in hybrid operations.

Enum values:

-   ECDSA\_P256
    
-   ECDSA\_P384
    
-   ECDSA\_P521
    
-   ED25519
    
-   ED448
    
-   RSA\_2048
    
-   RSA\_3072
    
-   RSA\_4096
    





 |  | String |
| **classicalSigner** (advanced) | **Autowired** The classical Signature instance to be used in hybrid signature operations. |  | Signature |
| **hybridKdfAlgorithm** (advanced) | 

The KDF algorithm to use for combining secrets in hybrid KEM operations.

Enum values:

-   HKDF-SHA256
    
-   HKDF-SHA384
    
-   HKDF-SHA512
    





 | HKDF-SHA256 | String |
| **keyEncapsulationAlgorithm** (advanced) | 

In case there is no keyGenerator, we specify an algorithm to build the KeyGenerator.

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
    





 |  | String |
| **keyGenerator** (advanced) | **Autowired** The Key Generator to be used in encapsulation and extraction. |  | KeyGenerator |
| **keyLifecycleManager** (advanced) | **Autowired** The KeyLifecycleManager to use for key lifecycle operations such as generation, rotation, import/export, expiration, and revocation. |  | KeyLifecycleManager |
| **keyPair** (advanced) | **Autowired** The KeyPair to be used. |  | KeyPair |
| **keyPairAlias** (advanced) | A KeyPair alias to use in combination with KeyStore parameter. |  | String |
| **keyStore** (advanced) | **Autowired** A KeyStore where we could get Cryptographic material. |  | KeyStore |
| **keyStorePassword** (advanced) | The KeyStore password to use in combination with KeyStore Parameter. |  | String |
| **signatureAlgorithm** (advanced) | 

In case there is no signer, we specify an algorithm to build the KeyPair or the Signer.

Enum values:

-   MLDSA
    
-   SLHDSA
    
-   LMS
    
-   HSS
    
-   XMSS
    
-   XMSSMT
    
-   DILITHIUM
    
-   FALCON
    
-   PICNIC
    
-   SNOVA
    
-   MAYO
    
-   SPHINCSPLUS
    





 |  | String |
| **signer** (advanced) | **Autowired** The Signer to be used. |  | Signature |
| **statefulKeyWarningThreshold** (advanced) | The warning threshold for stateful key exhaustion as a fraction of total signatures (0.0 to 1.0). When the remaining signatures for a stateful key (XMSS, XMSSMT, LMS/HSS) drop below this fraction of the total capacity, a WARN log is emitted. When remaining signatures reach zero, an exception is thrown to prevent key reuse. Set to 0 to disable warnings. | 0.1 | double |
| **storeExtractedSecretKeyAsHeader** (advanced) | In the context of extractSecretKeyFromEncapsulation operation, this option define if we want to have the key set as header. | false | boolean |
| **strictKeyLifecycle** (advanced) | Whether to enforce key status checks before cryptographic operations. When enabled, REVOKED keys are rejected for all operations, EXPIRED keys are rejected for signing/encapsulation but allowed for verification/extraction, and DEPRECATED keys produce a warning but still function. Requires a KeyLifecycleManager and a CamelPQCKeyId header to be set. | true | boolean |
| **symmetricKeyAlgorithm** (advanced) | 

In case we are using KEM operations, we need a Symmetric algorithm to be defined for the flow to work.

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
    





 |  | String |
| **symmetricKeyLength** (advanced) | The required length of the symmetric key used. | 128 | int |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The PQC Algorithms endpoint is configured using URI syntax:

pqc:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (22 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   sign
    
-   verify
    
-   hybridSign
    
-   hybridVerify
    
-   generateSecretKeyEncapsulation
    
-   extractSecretKeyEncapsulation
    
-   extractSecretKeyFromEncapsulation
    
-   hybridGenerateSecretKeyEncapsulation
    
-   hybridExtractSecretKeyEncapsulation
    
-   hybridExtractSecretKeyFromEncapsulation
    
-   getRemainingSignatures
    
-   getKeyState
    
-   deleteKeyState
    
-   generateKeyPair
    
-   exportKey
    
-   importKey
    
-   rotateKey
    
-   getKeyMetadata
    
-   listKeys
    
-   expireKey
    
-   revokeKey
    





 |  | PQCOperations |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **classicalKEMAlgorithm** (advanced) | 

The classical key agreement algorithm to use in hybrid KEM operations.

Enum values:

-   ECDH\_P256
    
-   ECDH\_P384
    
-   ECDH\_P521
    
-   X25519
    
-   X448
    





 |  | String |
| **classicalKeyAgreement** (advanced) | **Autowired** The classical KeyAgreement instance to be used in hybrid KEM operations. |  | KeyAgreement |
| **classicalKeyPair** (advanced) | **Autowired** The classical KeyPair to be used in hybrid operations. |  | KeyPair |
| **classicalSignatureAlgorithm** (advanced) | 

The classical signature algorithm to use in hybrid operations.

Enum values:

-   ECDSA\_P256
    
-   ECDSA\_P384
    
-   ECDSA\_P521
    
-   ED25519
    
-   ED448
    
-   RSA\_2048
    
-   RSA\_3072
    
-   RSA\_4096
    





 |  | String |
| **classicalSigner** (advanced) | **Autowired** The classical Signature instance to be used in hybrid signature operations. |  | Signature |
| **hybridKdfAlgorithm** (advanced) | 

The KDF algorithm to use for combining secrets in hybrid KEM operations.

Enum values:

-   HKDF-SHA256
    
-   HKDF-SHA384
    
-   HKDF-SHA512
    





 | HKDF-SHA256 | String |
| **keyEncapsulationAlgorithm** (advanced) | 

In case there is no keyGenerator, we specify an algorithm to build the KeyGenerator.

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
    





 |  | String |
| **keyGenerator** (advanced) | **Autowired** The Key Generator to be used in encapsulation and extraction. |  | KeyGenerator |
| **keyLifecycleManager** (advanced) | **Autowired** The KeyLifecycleManager to use for key lifecycle operations such as generation, rotation, import/export, expiration, and revocation. |  | KeyLifecycleManager |
| **keyPair** (advanced) | **Autowired** The KeyPair to be used. |  | KeyPair |
| **keyPairAlias** (advanced) | A KeyPair alias to use in combination with KeyStore parameter. |  | String |
| **keyStore** (advanced) | **Autowired** A KeyStore where we could get Cryptographic material. |  | KeyStore |
| **keyStorePassword** (advanced) | The KeyStore password to use in combination with KeyStore Parameter. |  | String |
| **signatureAlgorithm** (advanced) | 

In case there is no signer, we specify an algorithm to build the KeyPair or the Signer.

Enum values:

-   MLDSA
    
-   SLHDSA
    
-   LMS
    
-   HSS
    
-   XMSS
    
-   XMSSMT
    
-   DILITHIUM
    
-   FALCON
    
-   PICNIC
    
-   SNOVA
    
-   MAYO
    
-   SPHINCSPLUS
    





 |  | String |
| **signer** (advanced) | **Autowired** The Signer to be used. |  | Signature |
| **statefulKeyWarningThreshold** (advanced) | The warning threshold for stateful key exhaustion as a fraction of total signatures (0.0 to 1.0). When the remaining signatures for a stateful key (XMSS, XMSSMT, LMS/HSS) drop below this fraction of the total capacity, a WARN log is emitted. When remaining signatures reach zero, an exception is thrown to prevent key reuse. Set to 0 to disable warnings. | 0.1 | double |
| **storeExtractedSecretKeyAsHeader** (advanced) | In the context of extractSecretKeyFromEncapsulation operation, this option define if we want to have the key set as header. | false | boolean |
| **strictKeyLifecycle** (advanced) | Whether to enforce key status checks before cryptographic operations. When enabled, REVOKED keys are rejected for all operations, EXPIRED keys are rejected for signing/encapsulation but allowed for verification/extraction, and DEPRECATED keys produce a warning but still function. Requires a KeyLifecycleManager and a CamelPQCKeyId header to be set. | true | boolean |
| **symmetricKeyAlgorithm** (advanced) | 

In case we are using KEM operations, we need a Symmetric algorithm to be defined for the flow to work.

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
    





 |  | String |
| **symmetricKeyLength** (advanced) | The required length of the symmetric key used. | 128 | int |

## Message Headers

The PQC Algorithms component supports 23 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelPQCOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelPQCSignature** (producer) Constant: [`SIGNATURE`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#SIGNATURE) | The signature of a body. |  | String |
| **CamelPQCVerification** (producer) Constant: [`VERIFY`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#VERIFY) | The result of verification of a Body signature. |  | Boolean |
| **CamelPQCSecretKey** (producer) Constant: [`SECRET_KEY`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#SECRET_KEY) | The extracted key in case of extractSecretKeyFromEncapsulation operation and storeExtractedSecretKeyAsHeader option enabled. |  | Boolean |
| **CamelPQCRemainingSignatures** (producer) Constant: [`REMAINING_SIGNATURES`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#REMAINING_SIGNATURES) | The remaining signatures for a stateful key. |  | Long |
| **CamelPQCKeyState** (producer) Constant: [`KEY_STATE`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#KEY_STATE) | The key state for a stateful key. |  | StatefulKeyState |
| **CamelPQCKeyId** (producer) Constant: [`KEY_ID`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#KEY_ID) | The key ID for stateful key operations. |  | String |
| **CamelPQCKeyPair** (producer) Constant: [`KEY_PAIR`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#KEY_PAIR) | The generated key pair. |  | KeyPair |
| **CamelPQCKeyFormat** (producer) Constant: [`KEY_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#KEY_FORMAT) | The key format for import/export operations. |  | String |
| **CamelPQCExportedKey** (producer) Constant: [`EXPORTED_KEY`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#EXPORTED_KEY) | The exported key data. |  | byte\[\] |
| **CamelPQCKeyMetadata** (producer) Constant: [`KEY_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#KEY_METADATA) | The key metadata. |  | KeyMetadata |
| **CamelPQCKeyList** (producer) Constant: [`KEY_LIST`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#KEY_LIST) | List of key metadata. |  | List |
| **CamelPQCAlgorithm** (producer) Constant: [`ALGORITHM`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#ALGORITHM) | The algorithm for key generation. |  | String |
| **CamelPQCIncludePrivate** (producer) Constant: [`INCLUDE_PRIVATE`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#INCLUDE_PRIVATE) | Include private key in export. |  | Boolean |
| **CamelPQCRevocationReason** (producer) Constant: [`REVOCATION_REASON`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#REVOCATION_REASON) | Revocation reason. |  | String |
| **CamelPQCHybridSignature** (producer) Constant: [`HYBRID_SIGNATURE`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#HYBRID_SIGNATURE) | The hybrid signature combining both classical and PQC signatures. |  | byte\[\] |
| **CamelPQCClassicalSignature** (producer) Constant: [`CLASSICAL_SIGNATURE`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#CLASSICAL_SIGNATURE) | The classical signature component of a hybrid signature. |  | byte\[\] |
| **CamelPQCPqcSignature** (producer) Constant: [`PQC_SIGNATURE`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#PQC_SIGNATURE) | The PQC signature component of a hybrid signature. |  | byte\[\] |
| **CamelPQCClassicalEncapsulation** (producer) Constant: [`CLASSICAL_ENCAPSULATION`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#CLASSICAL_ENCAPSULATION) | The classical encapsulation component of a hybrid KEM. |  | byte\[\] |
| **CamelPQCPqcEncapsulation** (producer) Constant: [`PQC_ENCAPSULATION`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#PQC_ENCAPSULATION) | The PQC encapsulation component of a hybrid KEM. |  | byte\[\] |
| **CamelPQCHybridSecretKey** (producer) Constant: [`HYBRID_SECRET_KEY`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#HYBRID_SECRET_KEY) | The combined secret key from hybrid KEM operation. |  | SecretKey |
| **CamelPQCHybridEncapsulation** (producer) Constant: [`HYBRID_ENCAPSULATION`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#HYBRID_ENCAPSULATION) | The hybrid encapsulation combining both classical and PQC encapsulations. |  | byte\[\] |
| **CamelPQCHybridVerification** (producer) Constant: [`HYBRID_VERIFY`](https://javadoc.io/doc/org.apache.camel/camel-pqc/latest/org/apache/camel/component/pqc/PQCConstants.html#HYBRID_VERIFY) | The verification result of hybrid signature (both must pass). |  | Boolean |

## Supported Algorithms

The component supports the following algorithms for signature and verification.

Standardized and implemented

-   ML-DSA
    
-   SLH-DSA
    
-   LMS
    
-   HSS (Hierarchical Signature System)
    
-   XMSS
    
-   XMSSMT (XMSS Multi-Tree)
    

Experimental and non-standardized

-   Dilithium
    
-   Falcon
    
-   Picnic
    
-   SNOVA
    
-   MAYO
    
-   SPHINCS+
    

## Supported Operations

The component supports the following operations:

**Signature Operations:**

-   sign - Sign data using a PQC signature algorithm
    
-   verify - Verify a signature
    

**Key Encapsulation Operations:**

-   generateSecretKeyEncapsulation - Generate a secret key and encapsulate it
    
-   extractSecretKeyEncapsulation - Extract the encapsulation
    
-   extractSecretKeyFromEncapsulation - Extract the secret key from encapsulation
    

**Hybrid Operations (classical + post-quantum):**

-   hybridSign - Create a hybrid signature combining a classical and a PQC signature
    
-   hybridVerify - Verify a hybrid signature (both components must be valid)
    
-   hybridGenerateSecretKeyEncapsulation - Generate a hybrid encapsulation and shared secret
    
-   hybridExtractSecretKeyEncapsulation - Extract the shared secret from a hybrid encapsulation
    
-   hybridExtractSecretKeyFromEncapsulation - Extract the secret key from a hybrid encapsulation
    

See [PQC Hybrid Cryptography](others/pqc-hybrid.md) for configuration details and examples.

**Key Lifecycle Operations:**

-   generateKeyPair - Generate a new PQC key pair
    
-   exportKey - Export a key to PEM, DER, PKCS8, or X.509 format
    
-   importKey - Import a key from bytes
    
-   rotateKey - Rotate a key and deprecate the old one
    
-   getKeyMetadata - Get metadata for a key
    
-   listKeys - List all keys with metadata
    
-   expireKey - Mark a key as expired
    
-   revokeKey - Revoke a compromised key
    

See [PQC Key Lifecycle Management](others/pqc-key-lifecycle.md) for full details.

## Sub-Pages

The PQC component documentation is split into focused sub-pages:

-   [Key Lifecycle Management](others/pqc-key-lifecycle.md) - Key generation, storage, rotation, expiration, revocation, and format conversion with FileBasedKeyLifecycleManager, InMemoryKeyLifecycleManager, HashiCorp Vault, and AWS Secrets Manager implementations
    
-   [Hybrid Cryptography](others/pqc-hybrid.md) - Combining classical and post-quantum algorithms for defense-in-depth, including wire format v2
    
-   [PQC DataFormat](dataformats/pqc-dataformat.md) - DataFormat for quantum-resistant encryption/decryption using KEM
    

## Signature and Verification

The component expects to find a KeyPair and a Signature Objects in to the Camel Registry.

In case the KeyPair and the Signature Objects are not in the registry, it will provide two instances of the Objects with default implementation.

This will be true for standardized algorithms and for experimental ones.

> **Tip**
> To combine a classical signature (ECDSA, Ed25519, RSA) with a PQC signature for defense-in-depth during the post-quantum transition, use the hybrid signature operations described in [Hybrid Cryptography](others/pqc-hybrid.md).

## Examples

All signature algorithms follow the same route pattern. Below is a complete example using ML-DSA, followed by a reference table for the other algorithms.

### ML-DSA (complete example)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:sign").to("pqc:sign?operation=sign").to("mock:sign").to("pqc:verify?operation=verify")
    .to("mock:verify");
```

```xml
<route>
  <from uri="direct:sign"/>
  <to uri="pqc:sign?operation=sign"/>
  <to uri="mock:sign"/>
  <to uri="pqc:verify?operation=verify"/>
  <to uri="mock:verify"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:sign
    steps:
      - to:
          uri: pqc:sign
          parameters:
            operation: sign
      - to:
          uri: mock:sign
      - to:
          uri: pqc:verify
          parameters:
            operation: verify
      - to:
          uri: mock:verify
```

With the following beans registered in the Registry

_Java-only: registering ML-DSA KeyPair and Signature beans_

```java
    @BindToRegistry("Keypair")
    public KeyPair setKeyPair() throws NoSuchAlgorithmException, NoSuchProviderException, InvalidAlgorithmParameterException {
        KeyPairGenerator kpGen = KeyPairGenerator.getInstance("ML-DSA", "BC");
        kpGen.initialize(MLDSAParameterSpec.ml_dsa_65);
        KeyPair kp = kpGen.generateKeyPair();
        return kp;
    }

    @BindToRegistry("Signer")
    public Signature getSigner() throws NoSuchAlgorithmException {
        Signature mlDsa = Signature.getInstance("ML-DSA");
        return mlDsa;
    }
```

This could be done even without the Registry beans, by specifying the `signatureAlgorithm` parameter in the following way

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:sign").to("pqc:sign?operation=sign&signatureAlgorithm=MLDSA").to("mock:sign")
    .to("pqc:verify?operation=verify&signatureAlgorithm=MLDSA")
    .to("mock:verify");
```

```xml
<route>
  <from uri="direct:sign"/>
  <to uri="pqc:sign?operation=sign&amp;signatureAlgorithm=MLDSA"/>
  <to uri="mock:sign"/>
  <to uri="pqc:verify?operation=verify&amp;signatureAlgorithm=MLDSA"/>
  <to uri="mock:verify"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:sign
    steps:
      - to:
          uri: pqc:sign
          parameters:
            operation: sign
            signatureAlgorithm: MLDSA
      - to:
          uri: mock:sign
      - to:
          uri: pqc:verify
          parameters:
            operation: verify
            signatureAlgorithm: MLDSA
      - to:
          uri: mock:verify
```

With this approach the component will use the class `org.apache.camel.component.pqc.crypto.PQCDefaultMLDSAMaterial`, which will create the Signature and KeyPair objects to be used.

The Spec used for the KeyPair will be, in this case, `ML-DSA-65`.

### Other Signature Algorithms

All other signature algorithms follow the exact same route pattern shown above for ML-DSA. The only differences are the algorithm name, the bean registration parameters, and the default material class. Use the following reference table:

     
| Algorithm | signatureAlgorithm param | JCA Algorithm Name | Provider | Default Parameter Spec | Material Class |
| --- | --- | --- | --- | --- | --- |
| SLH-DSA | `SLHDSA` | SLH-DSA | BC | SLH-DSA-SHA2-128s | `PQCDefaultSLHDSAMaterial` |
| LMS | `LMS` | LMS | BC | LMS-SHA256-N32-H5 / SHA256-N32-W1 (OTS) | `PQCDefaultLMSMaterial` |
| XMSS | `XMSS` | XMSS | BCPQC | Tree height 10, SHA-256 | `PQCDefaultXMSSMaterial` |
| XMSSMT | `XMSSMT` | XMSSMT | BCPQC | XMSSMT-SHA2-20d2-256 | `PQCDefaultXMSSMTMaterial` |
| HSS | `HSS` | HSS | BC | LMS-SHA256-N32-H5 | `PQCDefaultHSSMaterial` |
| Dilithium | `DILITHIUM` | Dilithium | BCPQC | dilithium2 | `PQCDefaultDilithiumMaterial` |
| Falcon | `FALCON` | Falcon | BCPQC | falcon\_512 | `PQCDefaultFalconMaterial` |
| SPHINCS+ | `SPHINCSPLUS` | SPHINCS+ | BCPQC | sha2\_128s | `PQCDefaultSPHINCSPlusMaterial` |
| Picnic | `PICNIC` | Picnic | BCPQC | picnicl1fs | `PQCDefaultPicknicMaterial` |

To use any algorithm, set `signatureAlgorithm` in the URI (e.g., `signatureAlgorithm=SLHDSA`). Alternatively, register a KeyPair and Signature in the registry using the JCA Algorithm Name and Provider from the table above.

## Key Encapsulation and Extraction

In Post Quantum Cryptography it has been introduced the concept of Key Encapsulation Algorithm.

In this context there are three entities to consider:

-   A key generation algorithm which generates a public key and a private key (a keypair).
    
-   An encapsulation algorithm which takes as input a public key, and outputs a shared secret value and an "encapsulation" (a ciphertext) of this secret value.
    
-   A decapsulation algorithm which takes as input the encapsulation and the private key, and outputs the shared secret value.
    

In the component we are supporting the three phases in generateSecretKeyEncapsulation, extractSecretKeyEncapsulation and extractSecretKeyFromEncapsulation

The KEM Algorithm supported are the following:

Standardized and implemented

-   ML-KEM
    

Experimental and non-standardized

-   BIKE
    
-   CMCE
    
-   HQC
    
-   FRODO
    
-   SABER
    
-   NTRU
    
-   NTRULPRime
    
-   SNTRUPrime
    
-   Kyber
    

The component expects to find a KeyGenerator and a KeyPair in to the Camel Registry.

In case the KeyPair and the KeyGenerator Objects are not in the registry, it will provide two instances of the Objects with default implementation.

This will be true for standardized algorithms and for experimental ones.

> **Tip**
> To combine a classical key agreement (X25519, ECDH) with a PQC KEM (ML-KEM) for defense-in-depth, use the hybrid KEM operations described in [Hybrid Cryptography](others/pqc-hybrid.md).

A possible flow of the operation could be the following:

### ML-KEM Example

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:encapsulate").to("pqc:keyenc?operation=generateSecretKeyEncapsulation&symmetricKeyAlgorithm=AES")
    .to("mock:encapsulate")
    .to("pqc:keyenc?operation=extractSecretKeyEncapsulation&symmetricKeyAlgorithm=AES").to("mock:extract");
```

```xml
<route>
  <from uri="direct:encapsulate"/>
  <to uri="pqc:keyenc?operation=generateSecretKeyEncapsulation&amp;symmetricKeyAlgorithm=AES"/>
  <to uri="mock:encapsulate"/>
  <to uri="pqc:keyenc?operation=extractSecretKeyEncapsulation&amp;symmetricKeyAlgorithm=AES"/>
  <to uri="mock:extract"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:encapsulate
    steps:
      - to:
          uri: pqc:keyenc
          parameters:
            operation: generateSecretKeyEncapsulation
            symmetricKeyAlgorithm: AES
      - to:
          uri: mock:encapsulate
      - to:
          uri: pqc:keyenc
          parameters:
            operation: extractSecretKeyEncapsulation
            symmetricKeyAlgorithm: AES
      - to:
          uri: mock:extract
```

With the following beans registered in the Registry

_Java-only: registering ML-KEM KeyPair and KeyGenerator beans_

```java
    @BindToRegistry("Keypair")
    public KeyPair setKeyPair() throws NoSuchAlgorithmException, NoSuchProviderException, InvalidAlgorithmParameterException {
        KeyPairGenerator kpg = KeyPairGenerator.getInstance(PQCKeyEncapsulationAlgorithms.MLKEM.getAlgorithm(),
                PQCKeyEncapsulationAlgorithms.MLKEM.getBcProvider());
        kpg.initialize(MLKEMParameterSpec.ml_kem_512, new SecureRandom());
        KeyPair kp = kpg.generateKeyPair();
        return kp;
    }

    @BindToRegistry("KeyGenerator")
    public KeyGenerator setKeyGenerator()
            throws NoSuchAlgorithmException, NoSuchProviderException, InvalidAlgorithmParameterException {
        KeyGenerator kg = KeyGenerator.getInstance(PQCKeyEncapsulationAlgorithms.MLKEM.getAlgorithm(),
                PQCKeyEncapsulationAlgorithms.MLKEM.getBcProvider());
        return kg;
    }
```

This could be done even without the Registry beans, by specifying the `symmetricKeyAlgorithm` and `keyEncapsulationAlgorithm` parameters in the following way

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:encapsulate").to(
    "pqc:keyenc?operation=generateSecretKeyEncapsulation&symmetricKeyAlgorithm=AES&keyEncapsulationAlgorithm=MLKEM")
    .to("mock:encapsulate")
    .to("pqc:keyenc?operation=extractSecretKeyEncapsulation&symmetricKeyAlgorithm=AES&keyEncapsulationAlgorithm=MLKEM")
    .to("mock:extract");
```

```xml
<route>
  <from uri="direct:encapsulate"/>
  <to uri="pqc:keyenc?operation=generateSecretKeyEncapsulation&amp;symmetricKeyAlgorithm=AES&amp;keyEncapsulationAlgorithm=MLKEM"/>
  <to uri="mock:encapsulate"/>
  <to uri="pqc:keyenc?operation=extractSecretKeyEncapsulation&amp;symmetricKeyAlgorithm=AES&amp;keyEncapsulationAlgorithm=MLKEM"/>
  <to uri="mock:extract"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:encapsulate
    steps:
      - to:
          uri: pqc:keyenc
          parameters:
            operation: generateSecretKeyEncapsulation
            symmetricKeyAlgorithm: AES
            keyEncapsulationAlgorithm: MLKEM
      - to:
          uri: mock:encapsulate
      - to:
          uri: pqc:keyenc
          parameters:
            operation: extractSecretKeyEncapsulation
            symmetricKeyAlgorithm: AES
            keyEncapsulationAlgorithm: MLKEM
      - to:
          uri: mock:extract
```

With this approach the component will use the class `org.apache.camel.component.pqc.crypto.kem.PQCDefaultMLKEMMaterial`, which will create the KeyGenerator and KeyPair objects to be used.

The Spec used for the KeyPair will be, in this case, `ML-KEM-512`.

### Extract Secret Key from Encapsulation for downstream usage

Once you have the encapsulation you’re able to decapsulate the secret key by using private key.

All of this could be done to use the secret key coming from the encapsulation in the downstream route.

As example you could use the secret key to dynamically instruct the CryptoDataFormat to use it, like in the following route.

_Java-only: extracting secret key from encapsulation for downstream CryptoDataFormat usage_

```java
CryptoDataFormat cryptoFormat = new CryptoDataFormat("AES", null);

from("direct:encapsulate")
    .to("pqc:keyenc?operation=generateSecretKeyEncapsulation&symmetricKeyAlgorithm=AES")
    .to("mock:encapsulate")
    .to("pqc:keyenc?operation=extractSecretKeyEncapsulation&symmetricKeyAlgorithm=AES")
    .to("pqc:keyenc?operation=extractSecretKeyFromEncapsulation&symmetricKeyAlgorithm=AES")
    .setHeader(CryptoDataFormat.KEY, body())
    .setBody(constant("Hello"))
    .marshal(cryptoFormat)
    .log("Encrypted ${body}")
    .to("mock:encrypted")
    .unmarshal(cryptoFormat)
    .log("Unencrypted ${body}")
    .to("mock:unencrypted");
```

This could be used to generate a secret key, protect it through Encapsulation and KEM approach and re-use it once extracted.

> **Tip**
> For a simplified approach to KEM-based encryption, consider using the [PQC DataFormat](dataformats/pqc-dataformat.md) which handles all KEM operations internally with a single marshal/unmarshal call.