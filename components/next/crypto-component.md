# Crypto (JCE)

**Since Camel 2.3**

**Only producer is supported**

With Camel cryptographic endpoints and Java’s Cryptographic extension, it is possible to create Digital Signatures for Exchanges. Camel provides a pair of flexible endpoints which get used in concert to create a signature for an exchange in one part of the exchange’s workflow and then verify the signature in a later part of the workflow.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-crypto</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Introduction

Digital signatures make use of Asymmetric Cryptographic techniques to sign messages. From a (very) high level, the algorithms use pairs of complimentary keys with the special property that data encrypted with one key can only be decrypted with the other. One, the private key, is closely guarded and used to 'sign' the message while the other, public key, is shared around to anyone interested in verifying the signed messages. Messages are signed by using the private key to encrypting a digest of the message. This encrypted digest is transmitted along with the message. On the other side, the verifier recalculates the message digest and uses the public key to decrypt the digest in the signature. If both digests match, the verifier knows only the holder of the private key could have created the signature.

Camel uses the Signature service from the Java Cryptographic Extension to do all the heavy cryptographic lifting required to create exchange signatures. The following are some excellent resources for explaining the mechanics of Cryptography, Message digests and Digital Signatures and how to leverage them with the JCE.

-   Bruce Schneier’s Applied Cryptography
    
-   Beginning Cryptography with Java by David Hook
    
-   The ever insightful Wikipedia [Digital\_signatures](http://en.wikipedia.org/wiki/Digital_signature)
    

## URI format

As mentioned, Camel provides a pair of crypto endpoints to create and verify signatures

crypto:sign:name\[?options\]
crypto:verify:name\[?options\]

-   `crypto:sign` creates the signature and stores it in the header `CamelDigitalSignature`.
    
-   `crypto:verify` will read in the contents of this header and do the verification calculation.
    

To correctly function, the sign and verify process needs a pair of keys to be shared, signing requiring a `PrivateKey` and verifying a `PublicKey` (or a `Certificate` containing one). Using the JCE it is very simple to generate these key pairs, but it is usually most secure to use a KeyStore to house and share your keys. The DSL is very flexible about how keys are supplied and provides a number of mechanisms.

Note a `crypto:sign` endpoint is typically defined in one route and the complimentary `crypto:verify` in another, though for simplicity in the examples they appear one after the other. It goes without saying that both signing and verifying should be configured identically.

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

The Crypto (JCE) component supports 21 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **algorithm** (producer) | Sets the JCE name of the Algorithm that should be used for the signer. | SHA256withRSA | String |
| **alias** (producer) | Sets the alias used to query the KeyStore for keys and \\{link java.security.cert.Certificate Certificates} to be used in signing and verifying exchanges. This value can be provided at runtime via the message header org.apache.camel.component.crypto.DigitalSignatureConstants#KEYSTORE\_ALIAS. |  | String |
| **certificateName** (producer) | Sets the reference name for a PrivateKey that can be found in the registry. |  | String |
| **keystore** (producer) | Sets the KeyStore that can contain keys and Certficates for use in signing and verifying exchanges. A KeyStore is typically used with an alias, either one supplied in the Route definition or dynamically via the message header CamelSignatureKeyStoreAlias. If no alias is supplied and there is only a single entry in the Keystore, then this single entry will be used. |  | KeyStore |
| **keystoreName** (producer) | Sets the reference name for a Keystore that can be found in the registry. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **privateKey** (producer) | Set the PrivateKey that should be used to sign the exchange. |  | PrivateKey |
| **privateKeyName** (producer) | Sets the reference name for a PrivateKey that can be found in the registry. |  | String |
| **provider** (producer) | Set the id of the security provider that provides the configured Signature algorithm. |  | String |
| **publicKeyName** (producer) | references that should be resolved when the context changes. |  | String |
| **secureRandomName** (producer) | Sets the reference name for a SecureRandom that can be found in the registry. |  | String |
| **signatureHeaderName** (producer) | Set the name of the message header that should be used to store the base64 encoded signature. This defaults to 'CamelDigitalSignature'. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **bufferSize** (advanced) | Set the size of the buffer used to read in the Exchange payload data. | 2048 | Integer |
| **certificate** (advanced) | Set the Certificate that should be used to verify the signature in the exchange based on its payload. |  | Certificate |
| **clearHeaders** (advanced) | Determines if the Signature specific headers be cleared after signing and verification. Defaults to true, and should only be made otherwise at your extreme peril as vital private information such as Keys and passwords may escape if unset. | true | boolean |
| **configuration** (advanced) | To use the shared DigitalSignatureConfiguration as configuration. |  | DigitalSignatureConfiguration |
| **keyStoreParameters** (advanced) | Sets the KeyStore that can contain keys and Certficates for use in signing and verifying exchanges based on the given KeyStoreParameters. A KeyStore is typically used with an alias, either one supplied in the Route definition or dynamically via the message header CamelSignatureKeyStoreAlias. If no alias is supplied and there is only a single entry in the Keystore, then this single entry will be used. |  | KeyStoreParameters |
| **publicKey** (advanced) | Set the PublicKey that should be used to verify the signature in the exchange. |  | PublicKey |
| **secureRandom** (advanced) | Set the SecureRandom used to initialize the Signature service. |  | SecureRandom |
| **password** (security) | Sets the password used to access an aliased PrivateKey in the KeyStore. |  | String |

## Endpoint Options

The Crypto (JCE) endpoint is configured using URI syntax:

crypto:cryptoOperation:name

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cryptoOperation** (producer) | 
**Required** Set the Crypto operation from that supplied after the crypto scheme in the endpoint uri e.g. crypto:sign sets sign as the operation.

Enum values:

-   sign
    
-   verify
    





 |  | CryptoOperation |
| **name** (producer) | **Required** The logical name of this operation. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **algorithm** (producer) | Sets the JCE name of the Algorithm that should be used for the signer. | SHA256withRSA | String |
| **alias** (producer) | Sets the alias used to query the KeyStore for keys and \\{link java.security.cert.Certificate Certificates} to be used in signing and verifying exchanges. This value can be provided at runtime via the message header org.apache.camel.component.crypto.DigitalSignatureConstants#KEYSTORE\_ALIAS. |  | String |
| **certificateName** (producer) | Sets the reference name for a PrivateKey that can be found in the registry. |  | String |
| **keystore** (producer) | Sets the KeyStore that can contain keys and Certficates for use in signing and verifying exchanges. A KeyStore is typically used with an alias, either one supplied in the Route definition or dynamically via the message header CamelSignatureKeyStoreAlias. If no alias is supplied and there is only a single entry in the Keystore, then this single entry will be used. |  | KeyStore |
| **keystoreName** (producer) | Sets the reference name for a Keystore that can be found in the registry. |  | String |
| **privateKey** (producer) | Set the PrivateKey that should be used to sign the exchange. |  | PrivateKey |
| **privateKeyName** (producer) | Sets the reference name for a PrivateKey that can be found in the registry. |  | String |
| **provider** (producer) | Set the id of the security provider that provides the configured Signature algorithm. |  | String |
| **publicKeyName** (producer) | references that should be resolved when the context changes. |  | String |
| **secureRandomName** (producer) | Sets the reference name for a SecureRandom that can be found in the registry. |  | String |
| **signatureHeaderName** (producer) | Set the name of the message header that should be used to store the base64 encoded signature. This defaults to 'CamelDigitalSignature'. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **bufferSize** (advanced) | Set the size of the buffer used to read in the Exchange payload data. | 2048 | Integer |
| **certificate** (advanced) | Set the Certificate that should be used to verify the signature in the exchange based on its payload. |  | Certificate |
| **clearHeaders** (advanced) | Determines if the Signature specific headers be cleared after signing and verification. Defaults to true, and should only be made otherwise at your extreme peril as vital private information such as Keys and passwords may escape if unset. | true | boolean |
| **keyStoreParameters** (advanced) | Sets the KeyStore that can contain keys and Certficates for use in signing and verifying exchanges based on the given KeyStoreParameters. A KeyStore is typically used with an alias, either one supplied in the Route definition or dynamically via the message header CamelSignatureKeyStoreAlias. If no alias is supplied and there is only a single entry in the Keystore, then this single entry will be used. |  | KeyStoreParameters |
| **publicKey** (advanced) | Set the PublicKey that should be used to verify the signature in the exchange. |  | PublicKey |
| **secureRandom** (advanced) | Set the SecureRandom used to initialize the Signature service. |  | SecureRandom |
| **password** (security) | Sets the password used to access an aliased PrivateKey in the KeyStore. |  | String |

## Message Headers

The Crypto (JCE) component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSignaturePrivateKey** (producer) Constant: [`SIGNATURE_PRIVATE_KEY`](https://javadoc.io/doc/org.apache.camel/camel-crypto/latest/org/apache/camel/component/crypto/DigitalSignatureConstants.html#SIGNATURE_PRIVATE_KEY) | The PrivateKey that should be used to sign the message. |  | PrivateKey |
| **CamelSignaturePublicKeyOrCert** (producer) Constant: [`SIGNATURE_PUBLIC_KEY_OR_CERT`](https://javadoc.io/doc/org.apache.camel/camel-crypto/latest/org/apache/camel/component/crypto/DigitalSignatureConstants.html#SIGNATURE_PUBLIC_KEY_OR_CERT) | The Certificate or PublicKey that should be used to verify the signature. |  | Certificate or PublicKey |
| **CamelSignatureKeyStoreAlias** (producer) Constant: [`KEYSTORE_ALIAS`](https://javadoc.io/doc/org.apache.camel/camel-crypto/latest/org/apache/camel/component/crypto/DigitalSignatureConstants.html#KEYSTORE_ALIAS) | The alias used to query the KeyStore for keys and Certificates to be used in signing and verifying exchanges. |  | String |
| **CamelSignatureKeyStorePassword** (producer) Constant: [`KEYSTORE_PASSWORD`](https://javadoc.io/doc/org.apache.camel/camel-crypto/latest/org/apache/camel/component/crypto/DigitalSignatureConstants.html#KEYSTORE_PASSWORD) | The password used to access an aliased PrivateKey in the KeyStore. |  | char\[\] |

## Usage

### Raw keys

The most basic way to sign and verify an exchange is with a KeyPair as follows.

_Java-only: requires Java KeyPair objects_

```java
KeyPair keyPair = KeyGenerator.getInstance("RSA").generateKeyPair();

from("direct:sign")
    .setHeader("CamelSignaturePrivateKey", constant(keyPair.getPrivate()))
    .to("crypto:sign:message")
    .to("direct:verify");

from("direct:verify")
    .setHeader("CamelSignaturePublicKeyOrCert", constant(keyPair.getPublic()))
    .to("crypto:verify:check");
```

The same can be achieved with the [Spring XML Extensions](../../manual/spring-xml-extensions.md) using references to keys

### KeyStores and Aliases.

The JCE provides a very versatile keystore concept for housing pairs of private keys and certificates, keeping them encrypted and password protected. They can be retrieved by applying an alias to the retrieval APIs. There are a number of ways to get keys and Certificates into a keystore, most often this is done with the external 'keytool' application.

The following command will create a keystore containing a key and certificate aliased by `bob`, which can be used in the following examples. The password for the keystore and the key is `letmein`.

```sh
keytool -genkey -keyalg RSA -keysize 2048 -keystore keystore.jks -storepass letmein -alias bob -dname "CN=Bob,OU=IT,O=Camel" -noprompt
```

The following route first signs an exchange using Bob’s alias from the KeyStore bound into the Camel Registry, and then verifies it using the same alias.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:sign")
    .to("crypto:sign:keystoreSign?alias=bob&keystoreName=myKeystore&password=letmein")
    .log("Signature: ${header.CamelDigitalSignature}")
    .to("crypto:verify:keystoreVerify?alias=bob&keystoreName=myKeystore&password=letmein")
    .log("Verified: ${body}");
```

```xml
<route>
  <from uri="direct:sign"/>
  <to uri="crypto:sign:keystoreSign?alias=bob&amp;keystoreName=myKeystore&amp;password=letmein"/>
  <log message="Signature: ${header.CamelDigitalSignature}"/>
  <to uri="crypto:verify:keystoreVerify?alias=bob&amp;keystoreName=myKeystore&amp;password=letmein"/>
  <log message="Verified: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:sign
      steps:
        - to:
            uri: crypto:sign:keystoreSign
            parameters:
              alias: bob
              keystoreName: myKeystore
              password: letmein
        - log:
            message: "Signature: ${header.CamelDigitalSignature}"
        - to:
            uri: crypto:verify:keystoreVerify
            parameters:
              alias: bob
              keystoreName: myKeystore
              password: letmein
        - log:
            message: "Verified: ${body}"
```

The following code shows how to load the keystore created using the above `keytool` command and bind it into the registry with the name `myKeystore` for use in the above route. The example makes use of the `@Configuration` and `@BindToRegistry` annotations introduced in Camel 3 to instantiate the KeyStore and register it with the name `myKeyStore`.

_Java-only: KeyStore bean configuration with \`@BindToRegistry\`_

```java
@Configuration
public class KeystoreConfig {

    @BindToRegistry
    public KeyStore myKeystore() throws Exception {
        KeyStore store = KeyStore.getInstance("JKS");
        try (FileInputStream fis = new FileInputStream("keystore.jks")) {
            store.load(fis, "letmein".toCharArray());
        }
        return store;
    }
}
```

Again in Spring, a ref is used to look up an actual keystore instance.

### Changing JCE Provider and Algorithm

Changing the Signature algorithm or the Security provider is a simple matter of specifying their names. You will need to also use Keys that are compatible with the algorithm you choose.

### Changing the Signature Message Header

It may be desirable to change the message header used to store the signature. A different header name can be specified in the route definition as follows

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:sign")
    .to("crypto:sign:keystoreSign?alias=bob&keystoreName=myKeystore&password=letmein&signatureHeaderName=mySignature")
    .log("Signature: ${header.mySignature}")
    .to("crypto:verify:keystoreVerify?alias=bob&keystoreName=myKeystore&password=letmein&signatureHeaderName=mySignature");
```

```xml
<route>
  <from uri="direct:sign"/>
  <to uri="crypto:sign:keystoreSign?alias=bob&amp;keystoreName=myKeystore&amp;password=letmein&amp;signatureHeaderName=mySignature"/>
  <log message="Signature: ${header.mySignature}"/>
  <to uri="crypto:verify:keystoreVerify?alias=bob&amp;keystoreName=myKeystore&amp;password=letmein&amp;signatureHeaderName=mySignature"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:sign
      steps:
        - to:
            uri: crypto:sign:keystoreSign
            parameters:
              alias: bob
              keystoreName: myKeystore
              password: letmein
              signatureHeaderName: mySignature
        - log:
            message: "Signature: ${header.mySignature}"
        - to:
            uri: crypto:verify:keystoreVerify
            parameters:
              alias: bob
              keystoreName: myKeystore
              password: letmein
              signatureHeaderName: mySignature
```

### Changing the bufferSize

In case you need to update the size of the buffer…​

### Supplying Keys dynamically.

When using a Recipient list or similar EIP, the recipient of an exchange can vary dynamically. Using the same key across all recipients may be neither feasible nor desirable. It would be useful to be able to specify signature keys dynamically on a per-exchange basis. The exchange could then be dynamically enriched with the key of its target recipient prior to signing. To facilitate this, the signature mechanisms allow for keys to be supplied dynamically via the message headers below

-   `CamelSignaturePrivateKey`
    
-   `CamelSignaturePublicKeyOrCert`
    

Even better would be to dynamically supply a keystore alias. Again, the alias can be supplied in a message header

-   `CamelSignatureKeyStoreAlias`
    

The header would be set as follows:

_Java-only: Java test API (ProducerTemplate)_

```java
Exchange unsigned = getMandatoryEndpoint("direct:alias-sign").createExchange();
unsigned.getIn().setBody(payload);
unsigned.getIn().setHeader("CamelSignatureKeyStoreAlias", "bob");
unsigned.getIn().setHeader("CamelSignatureKeyStorePassword", "letmein".toCharArray());
template.send("direct:alias-sign", unsigned);
Exchange signed = getMandatoryEndpoint("direct:alias-sign").createExchange();
signed.getIn().copyFrom(unsigned.getMessage());
signed.getIn().setHeader("CamelSignatureKeyStoreAlias", "bob");
template.send("direct:alias-verify", signed);
```

## Using Post-Quantum Cryptography (PQC) Algorithms

The Digital Signature EIP supports Post-Quantum Cryptography algorithms through the standard JCE provider mechanism. Since the `algorithm` and `provider` options accept any value supported by the underlying JCE implementation, you can use PQC signature algorithms such as ML-DSA (NIST FIPS 204) by registering a Bouncy Castle provider and supplying the corresponding keys.

This approach is useful when you want to apply PQC signatures directly using the `crypto:sign` / `crypto:verify` pair without the full `camel-pqc` component. For hybrid signatures (combining classical + PQC) or key lifecycle management, use the [PQC component](../4.18.x/pqc-component.md) instead.

### Prerequisites

Add the Bouncy Castle provider dependencies to your project:

```xml
<dependency>
    <groupId>org.bouncycastle</groupId>
    <artifactId>bcprov-jdk18on</artifactId>
    <version>${bouncycastle.version}</version>
</dependency>
<dependency>
    <groupId>org.bouncycastle</groupId>
    <artifactId>bcpkix-jdk18on</artifactId>
    <version>${bouncycastle.version}</version>
</dependency>
```

Register the Bouncy Castle provider at application startup:

_Java-only: static provider registration_

```java
import org.bouncycastle.jce.provider.BouncyCastleProvider;

Security.addProvider(new BouncyCastleProvider());
```

### ML-DSA (NIST FIPS 204)

ML-DSA (Module-Lattice Digital Signature Algorithm, formerly Dilithium) is the primary NIST-standardized post-quantum signature algorithm.

#### Java DSL

-   Raw keys
    
-   Dynamic keys via headers
    

```java
private KeyPair mlDsaKeyPair;

private KeyPair getMlDsaKeyPair() throws Exception {
    if (mlDsaKeyPair == null) {
        KeyPairGenerator kpGen = KeyPairGenerator.getInstance("ML-DSA", "BC");
        kpGen.initialize(MLDSAParameterSpec.ml_dsa_65);
        mlDsaKeyPair = kpGen.generateKeyPair();
    }
    return mlDsaKeyPair;
}

@BindToRegistry("mlDsaPrivateKey")
public PrivateKey mlDsaPrivateKey() throws Exception {
    return getMlDsaKeyPair().getPrivate();
}

@BindToRegistry("mlDsaPublicKey")
public PublicKey mlDsaPublicKey() throws Exception {
    return getMlDsaKeyPair().getPublic();
}

from("direct:sign")
    .to("crypto:sign:pqc?algorithm=ML-DSA&provider=BC&privateKeyName=#mlDsaPrivateKey")
    .to("direct:verify");

from("direct:verify")
    .to("crypto:verify:pqc?algorithm=ML-DSA&provider=BC&publicKeyName=#mlDsaPublicKey")
    .to("mock:result");
```

```java
KeyPairGenerator kpGen = KeyPairGenerator.getInstance("ML-DSA", "BC");
kpGen.initialize(MLDSAParameterSpec.ml_dsa_65);
KeyPair kp = kpGen.generateKeyPair();

from("direct:sign")
    .setHeader("CamelSignaturePrivateKey", constant(kp.getPrivate()))
    .to("crypto:sign:pqc?algorithm=ML-DSA&provider=BC")
    .to("direct:verify");

from("direct:verify")
    .setHeader("CamelSignaturePublicKeyOrCert", constant(kp.getPublic()))
    .to("crypto:verify:pqc?algorithm=ML-DSA&provider=BC")
    .to("mock:result");
```

#### YAML DSL

```yaml
- route:
    id: sign-route
    from:
      uri: direct:sign
    steps:
      - to:
          uri: crypto:sign:pqc
          parameters:
            algorithm: ML-DSA
            provider: BC
            privateKeyName: "#mlDsaPrivateKey"
      - to:
          uri: direct:verify

- route:
    id: verify-route
    from:
      uri: direct:verify
    steps:
      - to:
          uri: crypto:verify:pqc
          parameters:
            algorithm: ML-DSA
            provider: BC
            publicKeyName: "#mlDsaPublicKey"
      - to:
          uri: mock:result
```

#### ML-DSA parameter sets

The following ML-DSA parameter sets are available:

   
| Parameter Set | Security Level | Signature Size | Use Case |
| --- | --- | --- | --- |
| `ml_dsa_44` | NIST Level 2 | ~2,420 bytes | General-purpose signing |
| `ml_dsa_65` | NIST Level 3 | ~3,309 bytes | Recommended default |
| `ml_dsa_87` | NIST Level 5 | ~4,627 bytes | Highest security |

### SLH-DSA (NIST FIPS 205)

SLH-DSA (Stateless Hash-Based Digital Signature Algorithm, formerly SPHINCS+) is the secondary NIST-standardized PQC signature algorithm, based on hash functions.

_Java-only: requires Java KeyPair and registry binding_

```java
private KeyPair slhDsaKeyPair;

private KeyPair getSlhDsaKeyPair() throws Exception {
    if (slhDsaKeyPair == null) {
        KeyPairGenerator kpGen = KeyPairGenerator.getInstance("SLH-DSA", "BC");
        kpGen.initialize(SLHDSAParameterSpec.slh_dsa_sha2_128s);
        slhDsaKeyPair = kpGen.generateKeyPair();
    }
    return slhDsaKeyPair;
}

@BindToRegistry("slhDsaPrivateKey")
public PrivateKey slhDsaPrivateKey() throws Exception {
    return getSlhDsaKeyPair().getPrivate();
}

@BindToRegistry("slhDsaPublicKey")
public PublicKey slhDsaPublicKey() throws Exception {
    return getSlhDsaKeyPair().getPublic();
}

from("direct:sign")
    .to("crypto:sign:pqc?algorithm=SLH-DSA&provider=BC&privateKeyName=#slhDsaPrivateKey")
    .to("direct:verify");

from("direct:verify")
    .to("crypto:verify:pqc?algorithm=SLH-DSA&provider=BC&publicKeyName=#slhDsaPublicKey")
    .to("mock:result");
```

### Hybrid Signatures (Classical + PQC)

For hybrid signatures that combine a classical algorithm (e.g., ECDSA) with a PQC algorithm (e.g., ML-DSA) in a single route, the recommended approach is to use the [PQC component](../4.18.x/pqc-component.md) which provides built-in hybrid operations.

#### Using the PQC component (recommended)

The `camel-pqc` component has dedicated `hybridSign` and `hybridVerify` operations that produce a single combined signature:

-   Java DSL
    
-   YAML DSL
    

```java
from("direct:sign")
    .to("pqc:hybrid?operation=hybridSign"
        + "&signatureAlgorithm=MLDSA"
        + "&classicalSignatureAlgorithm=ECDSA_P256")
    .to("direct:verify");

from("direct:verify")
    .to("pqc:hybrid?operation=hybridVerify"
        + "&signatureAlgorithm=MLDSA"
        + "&classicalSignatureAlgorithm=ECDSA_P256")
    .to("mock:result");
```

```yaml
- route:
    id: hybrid-sign-route
    from:
      uri: direct:sign
    steps:
      - to:
          uri: pqc:hybrid
          parameters:
            operation: hybridSign
            signatureAlgorithm: MLDSA
            classicalSignatureAlgorithm: ECDSA_P256
      - to:
          uri: direct:verify

- route:
    id: hybrid-verify-route
    from:
      uri: direct:verify
    steps:
      - to:
          uri: pqc:hybrid
          parameters:
            operation: hybridVerify
            signatureAlgorithm: MLDSA
            classicalSignatureAlgorithm: ECDSA_P256
      - to:
          uri: mock:result
```

Other hybrid combinations include:

-   `ED25519` + `MLDSA` — Edwards curve + ML-DSA
    
-   `RSA_3072` + `MLDSA` — RSA 3072-bit + ML-DSA
    
-   `ECDSA_P384` + `SLHDSA` — ECDSA P-384 + SLH-DSA
    

See the [PQC component](../4.18.x/pqc-component.md) for the full list of supported classical algorithms and details on the hybrid wire format.

#### Chaining crypto: endpoints (manual approach)

Alternatively, you can chain two `crypto:sign` / `crypto:verify` endpoints to produce both a classical and a PQC signature, storing each in a separate header:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:sign")
    .to("crypto:sign:classical?algorithm=SHA256withECDSA&privateKeyName=#ecPrivateKey&signatureHeaderName=ClassicalSignature")
    .to("crypto:sign:pqc?algorithm=ML-DSA&provider=BC&privateKeyName=#mlDsaPrivateKey&signatureHeaderName=PQCSignature")
    .to("direct:verify");

from("direct:verify")
    .to("crypto:verify:classical?algorithm=SHA256withECDSA&publicKeyName=#ecPublicKey&signatureHeaderName=ClassicalSignature")
    .to("crypto:verify:pqc?algorithm=ML-DSA&provider=BC&publicKeyName=#mlDsaPublicKey&signatureHeaderName=PQCSignature")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:sign"/>
  <to uri="crypto:sign:classical?algorithm=SHA256withECDSA&amp;privateKeyName=#ecPrivateKey&amp;signatureHeaderName=ClassicalSignature"/>
  <to uri="crypto:sign:pqc?algorithm=ML-DSA&amp;provider=BC&amp;privateKeyName=#mlDsaPrivateKey&amp;signatureHeaderName=PQCSignature"/>
  <to uri="direct:verify"/>
</route>

<route>
  <from uri="direct:verify"/>
  <to uri="crypto:verify:classical?algorithm=SHA256withECDSA&amp;publicKeyName=#ecPublicKey&amp;signatureHeaderName=ClassicalSignature"/>
  <to uri="crypto:verify:pqc?algorithm=ML-DSA&amp;provider=BC&amp;publicKeyName=#mlDsaPublicKey&amp;signatureHeaderName=PQCSignature"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:sign
      steps:
        - to:
            uri: crypto:sign:classical
            parameters:
              algorithm: SHA256withECDSA
              privateKeyName: "#ecPrivateKey"
              signatureHeaderName: ClassicalSignature
        - to:
            uri: crypto:sign:pqc
            parameters:
              algorithm: ML-DSA
              provider: BC
              privateKeyName: "#mlDsaPrivateKey"
              signatureHeaderName: PQCSignature
        - to:
            uri: direct:verify
- route:
    from:
      uri: direct:verify
      steps:
        - to:
            uri: crypto:verify:classical
            parameters:
              algorithm: SHA256withECDSA
              publicKeyName: "#ecPublicKey"
              signatureHeaderName: ClassicalSignature
        - to:
            uri: crypto:verify:pqc
            parameters:
              algorithm: ML-DSA
              provider: BC
              publicKeyName: "#mlDsaPublicKey"
              signatureHeaderName: PQCSignature
        - to:
            uri: mock:result
```

> **Note**
> The chaining approach stores two independent signatures in separate headers, while the PQC component’s hybrid operations produce a single combined signature. For new implementations, the PQC component’s hybrid operations are recommended as they handle the wire format, key management, and verification logic in a single step.

### Choosing Between camel-crypto and camel-pqc

  
| Feature | `camel-crypto` (Digital Signature EIP) | `camel-pqc` component |
| --- | --- | --- |
| PQC-only signatures | Supported (set `algorithm` and `provider`) | Supported (built-in algorithm support) |
| Hybrid signatures | Manual chaining of two endpoints | Built-in `hybridSign` / `hybridVerify` |
| Key lifecycle management | Not included | Generate, rotate, expire, revoke keys |
| Key encapsulation (KEM) | Not supported | Built-in support |
| Additional dependencies | Only Bouncy Castle | Only Bouncy Castle |
| Best for | Adding PQC to existing crypto: routes | New PQC-focused implementations |

## Spring Boot Auto-Configuration

When using crypto with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-crypto-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 32 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.crypto.algorithm** | Sets the JCE name of the Algorithm that should be used for the signer. | SHA256withRSA | String |
| **camel.component.crypto.alias** | Sets the alias used to query the KeyStore for keys and \\{link java.security.cert.Certificate Certificates} to be used in signing and verifying exchanges. This value can be provided at runtime via the message header org.apache.camel.component.crypto.DigitalSignatureConstants#KEYSTORE\_ALIAS. |  | String |
| **camel.component.crypto.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.crypto.buffer-size** | Set the size of the buffer used to read in the Exchange payload data. | 2048 | Integer |
| **camel.component.crypto.certificate** | Set the Certificate that should be used to verify the signature in the exchange based on its payload. The option is a java.security.cert.Certificate type. |  | Certificate |
| **camel.component.crypto.certificate-name** | Sets the reference name for a PrivateKey that can be found in the registry. |  | String |
| **camel.component.crypto.clear-headers** | Determines if the Signature specific headers be cleared after signing and verification. Defaults to true, and should only be made otherwise at your extreme peril as vital private information such as Keys and passwords may escape if unset. | true | Boolean |
| **camel.component.crypto.configuration** | To use the shared DigitalSignatureConfiguration as configuration. The option is a org.apache.camel.component.crypto.DigitalSignatureConfiguration type. |  | DigitalSignatureConfiguration |
| **camel.component.crypto.enabled** | Whether to enable auto configuration of the crypto component. This is enabled by default. |  | Boolean |
| **camel.component.crypto.key-store-parameters** | Sets the KeyStore that can contain keys and Certficates for use in signing and verifying exchanges based on the given KeyStoreParameters. A KeyStore is typically used with an alias, either one supplied in the Route definition or dynamically via the message header CamelSignatureKeyStoreAlias. If no alias is supplied and there is only a single entry in the Keystore, then this single entry will be used. The option is a org.apache.camel.support.jsse.KeyStoreParameters type. |  | KeyStoreParameters |
| **camel.component.crypto.keystore** | Sets the KeyStore that can contain keys and Certficates for use in signing and verifying exchanges. A KeyStore is typically used with an alias, either one supplied in the Route definition or dynamically via the message header CamelSignatureKeyStoreAlias. If no alias is supplied and there is only a single entry in the Keystore, then this single entry will be used. The option is a java.security.KeyStore type. |  | KeyStore |
| **camel.component.crypto.keystore-name** | Sets the reference name for a Keystore that can be found in the registry. |  | String |
| **camel.component.crypto.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.crypto.password** | Sets the password used to access an aliased PrivateKey in the KeyStore. |  | String |
| **camel.component.crypto.private-key** | Set the PrivateKey that should be used to sign the exchange. The option is a java.security.PrivateKey type. |  | PrivateKey |
| **camel.component.crypto.private-key-name** | Sets the reference name for a PrivateKey that can be found in the registry. |  | String |
| **camel.component.crypto.provider** | Set the id of the security provider that provides the configured Signature algorithm. |  | String |
| **camel.component.crypto.public-key** | Set the PublicKey that should be used to verify the signature in the exchange. The option is a java.security.PublicKey type. |  | PublicKey |
| **camel.component.crypto.public-key-name** | references that should be resolved when the context changes. |  | String |
| **camel.component.crypto.secure-random** | Set the SecureRandom used to initialize the Signature service. The option is a java.security.SecureRandom type. |  | SecureRandom |
| **camel.component.crypto.secure-random-name** | Sets the reference name for a SecureRandom that can be found in the registry. |  | String |
| **camel.component.crypto.signature-header-name** | Set the name of the message header that should be used to store the base64 encoded signature. This defaults to 'CamelDigitalSignature'. |  | String |
| **camel.dataformat.crypto.algorithm** | The JCE algorithm name indicating the cryptographic algorithm that will be used. |  | String |
| **camel.dataformat.crypto.algorithm-parameter-spec** | A JCE AlgorithmParameterSpec used to initialize the Cipher. Will lookup the type using the given name as a java.security.spec.AlgorithmParameterSpec type. The option is a java.security.spec.AlgorithmParameterSpec type. |  | String |
| **camel.dataformat.crypto.buffer-size** | The size of the buffer used in the signature process. | 4096 | Integer |
| **camel.dataformat.crypto.crypto-provider** | The name of the JCE Security Provider that should be used. |  | String |
| **camel.dataformat.crypto.enabled** | Whether to enable auto configuration of the crypto data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.crypto.init-vector** | Refers to a byte array containing the Initialization Vector that will be used to initialize the Cipher. |  | Byte\[\] |
| **camel.dataformat.crypto.inline** | Flag indicating that the configured IV should be inlined into the encrypted data stream. Is by default false. | false | Boolean |
| **camel.dataformat.crypto.key** | Refers to the secret key to lookup from the register to use. The option is a java.security.Key type. |  | String |
| **camel.dataformat.crypto.mac-algorithm** | The JCE algorithm name indicating the Message Authentication algorithm. | HmacSHA1 | String |
| **camel.dataformat.crypto.should-append-h-m-a-c** | Flag indicating that a Message Authentication Code should be calculated and appended to the encrypted data. | true | Boolean |