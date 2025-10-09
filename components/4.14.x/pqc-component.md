# PQC Algorithms

**Since Camel 4.12**

**Only producer is supported**

The PQC component supports signing and verifying payload using Post Quantum Cryptography algorithms.

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

The PQC Algorithms component supports 17 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | PQCConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   sign
    
-   verify
    
-   generateSecretKeyEncapsulation
    
-   extractSecretKeyEncapsulation
    
-   extractSecretKeyFromEncapsulation
    





 |  | PQCOperations |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
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
    





 |  | String |
| **keyGenerator** (advanced) | **Autowired** The Key Generator to be used in encapsulation and extraction. |  | KeyGenerator |
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
    
-   XMSS
    
-   FALCON
    
-   PICNIC
    
-   RAINBOW
    
-   SNOVA
    
-   MAYO
    
-   DILITHIUM
    
-   SPHINCSPLUS
    





 |  | String |
| **signer** (advanced) | **Autowired** The Signer to be used. |  | Signature |
| **storeExtractedSecretKeyAsHeader** (advanced) | In the context of extractSecretKeyFromEncapsulation operation, this option define if we want to have the key set as header. | false | boolean |
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

### Query Parameters (13 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   sign
    
-   verify
    
-   generateSecretKeyEncapsulation
    
-   extractSecretKeyEncapsulation
    
-   extractSecretKeyFromEncapsulation
    





 |  | PQCOperations |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
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
    





 |  | String |
| **keyGenerator** (advanced) | **Autowired** The Key Generator to be used in encapsulation and extraction. |  | KeyGenerator |
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
    
-   XMSS
    
-   FALCON
    
-   PICNIC
    
-   RAINBOW
    
-   SNOVA
    
-   MAYO
    
-   DILITHIUM
    
-   SPHINCSPLUS
    





 |  | String |
| **signer** (advanced) | **Autowired** The Signer to be used. |  | Signature |
| **storeExtractedSecretKeyAsHeader** (advanced) | In the context of extractSecretKeyFromEncapsulation operation, this option define if we want to have the key set as header. | false | boolean |
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

## Supported Algorithms

The component supports the following algorithms for signature and verification.

Standardized and implemented

-   ML-DSA
    
-   SLH-DSA
    
-   LMS
    
-   XMSS
    

Experimental and non-standardized

-   Falcon
    
-   Picnic
    
-   Rainbow
    

## Supported operations

The component supports five operations

-   sign
    
-   verify
    
-   generateSecretKeyEncapsulation
    
-   extractSecretKeyEncapsulation
    
-   extractSecretKeyFromEncapsulation
    

## Signature and Verification

The component expects to find a KeyPair and a Signature Objects in to the Camel Registry.

In case the KeyPair and the Signature Objects are not in the registry, it will provide two instances of the Objects with default implementation.

This will be true for standardized algorithms and for experimental ones.

## Examples

-   ML-DSA
    

```java
    from("direct:sign").to("pqc:sign?operation=sign").to("mock:sign").to("pqc:verify?operation=verify")
      .to("mock:verify");
```

With the following beans registered in the Registry

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

```java
  from("direct:sign").to("pqc:sign?operation=sign&signatureAlgorithm=MLDSA").to("mock:sign")
    .to("pqc:verify?operation=verify&signatureAlgorithm=MLDSA")
    .to("mock:verify");
```

With this approach the component will use the class `org.apache.camel.component.pqc.crypto.PQCDefaultMLDSAMaterial`, which will create the Signature and KeyPair objects to be used.

The Spec used for the KeyPair will be, in this case, `ML-DSA-65`.

-   SLH-DSA
    

```java
    from("direct:sign").to("pqc:sign?operation=sign").to("mock:sign").to("pqc:verify?operation=verify")
      .to("mock:verify");
```

With the following beans registered in the Registry

```java
    @BindToRegistry("Keypair")
    public KeyPair setKeyPair() throws NoSuchAlgorithmException, NoSuchProviderException, InvalidAlgorithmParameterException {
        KeyPairGenerator kpGen = KeyPairGenerator.getInstance("SLH-DSA", "BC");
        kpGen.initialize(SLHDSAParameterSpec.slh_dsa_sha2_128s);
        KeyPair kp = kpGen.generateKeyPair();
        return kp;
    }

    @BindToRegistry("Signer")
    public Signature getSigner() throws NoSuchAlgorithmException {
        Signature slhDsa = Signature.getInstance("SLH-DSA");
        return slhDsa;
    }
```

This could be done even without the Registry beans, by specifying the `signatureAlgorithm` parameter in the following way

```java
  from("direct:sign").to("pqc:sign?operation=sign&signatureAlgorithm=SLHDSA").to("mock:sign")
    .to("pqc:verify?operation=verify&signatureAlgorithm=SLHDSA")
    .to("mock:verify");
```

With this approach the component will use the class `org.apache.camel.component.pqc.crypto.PQCDefaultSLHDSAMaterial`, which will create the Signature and KeyPair objects to be used.

The Spec used for the KeyPair will be, in this case, `SLH-DSA-SHA2-128s`.

-   LMS
    

```java
    from("direct:sign").to("pqc:sign?operation=sign").to("mock:sign").to("pqc:verify?operation=verify")
      .to("mock:verify");
```

With the following beans registered in the Registry

```java
    @BindToRegistry("Keypair")
    public KeyPair setKeyPair() throws NoSuchAlgorithmException, NoSuchProviderException, InvalidAlgorithmParameterException {
        KeyPairGenerator kpGen = KeyPairGenerator.getInstance("LMS", "BC");
        kpGen.initialize(new LMSKeyGenParameterSpec(LMSigParameters.lms_sha256_n32_h5, LMOtsParameters.sha256_n32_w1));
        KeyPair kp = kpGen.generateKeyPair();
        return kp;
    }

    @BindToRegistry("Signer")
    public Signature getSigner() throws NoSuchAlgorithmException {
        Signature lms = Signature.getInstance("LMS");
        return lms;
    }
```

This could be done even without the Registry beans, by specifying the `signatureAlgorithm` parameter in the following way

```java
  from("direct:sign").to("pqc:sign?operation=sign&signatureAlgorithm=LMS").to("mock:sign")
    .to("pqc:verify?operation=verify&signatureAlgorithm=LMS")
    .to("mock:verify");
```

With this approach the component will use the class `org.apache.camel.component.pqc.crypto.PQCDefaultLMSMaterial`, which will create the Signature and KeyPair objects to be used.

The Parameters used will be `LMS-SHA256-N32-H5` for the signature and `SHA256-n32-w1` for the one-time signature.

-   XMSS
    

```java
    from("direct:sign").to("pqc:sign?operation=sign").to("mock:sign").to("pqc:verify?operation=verify")
      .to("mock:verify");
```

With the following beans registered in the Registry

```java
    @BindToRegistry("Keypair")
    public KeyPair setKeyPair() throws NoSuchAlgorithmException, NoSuchProviderException, InvalidAlgorithmParameterException {
        KeyPairGenerator kpGen = KeyPairGenerator.getInstance("XMSS", "BCPQC");
        kpGen.initialize(new XMSSParameterSpec(10, XMSSParameterSpec.SHA256), new SecureRandom());
        KeyPair kp = kpGen.generateKeyPair();
        return kp;
    }

    @BindToRegistry("Signer")
    public Signature getSigner() throws NoSuchAlgorithmException {
        Signature xmss = Signature.getInstance("XMSS");
        return xmss;
    }
```

This could be done even without the Registry beans, by specifying the `signatureAlgorithm` parameter in the following way

```java
  from("direct:sign").to("pqc:sign?operation=sign&signatureAlgorithm=XMSS").to("mock:sign")
    .to("pqc:verify?operation=verify&signatureAlgorithm=XMSS")
    .to("mock:verify");
```

With this approach the component will use the class `org.apache.camel.component.pqc.crypto.PQCDefaultXMSSMaterial`, which will create the Signature and KeyPair objects to be used.

The Parameters used will be `10` as tree height and `SHA-256` for the tree digest.

## Key Encapsulation and Extraction

In Post Quantum Cryptography it has been introduced the concept of Key Encapsulation Algorithm.

In this context there are three entities to consider:

-   A key generation algorithm which generates a public key and a private key (a keypair).
    
-   An encapsulation algorithm which takes as input a public key, and outputs a shared secret value and an “encapsulation” (a ciphertext) of this secret value.
    
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
    

The component expects to find a KeyGenerator and a KeyPair in to the Camel Registry.

In case the KeyPair and the KeyGenerator Objects are not in the registry, it will provide two instances of the Objects with default implementation.

This will be true for standardized algorithms and for experimental ones.

A possible flow of the operation could be the following:

-   ML-KEM
    

```java
from("direct:encapsulate").to("pqc:keyenc?operation=generateSecretKeyEncapsulation&symmetricKeyAlgorithm=AES")
  .to("mock:encapsulate")
  .to("pqc:keyenc?operation=extractSecretKeyEncapsulation&symmetricKeyAlgorithm=AES").to("mock:extract");
```

With the following beans registered in the Registry

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

```java
   from("direct:encapsulate").to(
     "pqc:keyenc?operation=generateSecretKeyEncapsulation&symmetricKeyAlgorithm=AES&keyEncapsulationAlgorithm=MLKEM")
     .to("mock:encapsulate")
     .to("pqc:keyenc?operation=extractSecretKeyEncapsulation&symmetricKeyAlgorithm=AES&keyEncapsulationAlgorithm=MLKEM")
     .to("mock:extract");
```

With this approach the component will use the class `org.apache.camel.component.pqc.crypto.kem.PQCDefaultMLKEMMaterial`, which will create the KeyGenerator and KeyPair objects to be used.

The Spec used for the KeyPair will be, in this case, `ML-KEM-512`.

## Extract Secret Key from Encapsulation for downstream usage

Once you have the encapsulation you’re able to decapsulate the secret key by using private key.

All of this could be done to use the secret key coming from the encapsulation in the downstream route.

As example you could use the secret key to dynamically instruct the CryptoDataFormat to use it, like in the following route.

```java
        CryptoDataFormat cryptoFormat = new CryptoDataFormat("AES", null);
        return new RouteBuilder() {
            @Override
            public void configure() {
                from("direct:encapsulate").to("pqc:keyenc?operation=generateSecretKeyEncapsulation&symmetricKeyAlgorithm=AES")
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
                ;
            }
```

This could be used to generate a secret key, protect it through Encapsulation and KEM approach and re-use it once extracted.

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

The component supports 18 options, which are listed below.

   
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