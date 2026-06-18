# Crypto (Java Cryptographic Extension)

**Since Camel 2.3**

The Crypto Data Format integrates the Java Cryptographic Extension into Camel, allowing simple and flexible encryption and decryption of messages using Camel’s familiar marshall and unmarshal formatting mechanism. It assumes marshaling to mean encryption to cyphertext and unmarshalling to mean decryption back to the original plaintext. This data format implements only symmetric (shared-key) encryption and decyption.

## CryptoDataFormat Options

The Crypto (Java Cryptographic Extension) dataformat supports 9 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **algorithm** (common) |  | `String` | The JCE algorithm name indicating the cryptographic algorithm that will be used. |
| **key** (common) |  | `Object` | Refers to the secret key to lookup from the register to use. |
| **cryptoProvider** (advanced) |  | `String` | The name of the JCE Security Provider that should be used. |
| **initVector** (advanced) |  | `String` | Refers to a byte array containing the Initialization Vector that will be used to initialize the Cipher. |
| **algorithmParameterSpec** (advanced) |  | `Object` | A JCE AlgorithmParameterSpec used to initialize the Cipher. Will lookup the type using the given name as a java.security.spec.AlgorithmParameterSpec type. |
| **bufferSize** (common) | `4096` | `Integer` | The size of the buffer used in the signature process. |
| **macAlgorithm** (common) | `HmacSHA1` | `String` | The JCE algorithm name indicating the Message Authentication algorithm. |
| **shouldAppendHMAC** (common) | `true` | `Boolean` | Flag indicating that a Message Authentication Code should be calculated and appended to the encrypted data. |
| **inline** (advanced) | `false` | `Boolean` | Flag indicating that the configured IV should be inlined into the encrypted data stream. Is by default false. |

## Basic Usage

At its most basic, all that is required to encrypt/decrypt an exchange is a shared secret key. If one or more instances of the Crypto data format are configured with this key, the format can be used to encrypt the payload in one route (or part of one) and decrypted in another. For example, using the Java DSL as follows:

_Java-only: programmatic CryptoDataFormat configuration with KeyGenerator_

```java
KeyGenerator generator = KeyGenerator.getInstance("DES");

CryptoDataFormat cryptoFormat = new CryptoDataFormat("DES", generator.generateKey());

from("direct:basic-encryption")
    .marshal(cryptoFormat)
    .to("mock:encrypted")
    .unmarshal(cryptoFormat)
    .to("mock:unencrypted");
```

In Spring the dataformat is configured first and then used in routes

_XML-only: Spring XML data format configuration_

```xml
<camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
  <dataFormats>
    <crypto id="basic" algorithm="DES" key="desKey" />
  </dataFormats>
    ...
  <route>
    <from uri="direct:basic-encryption" />
    <marshal ref="basic" />
    <to uri="mock:encrypted" />
    <unmarshal ref="basic" />
    <to uri="mock:unencrypted" />
  </route>
</camelContext>
```

## Specifying the Encryption Algorithm

Changing the algorithm is a matter of supplying the JCE algorithm name. If you change the algorithm, you will need to use a compatible key.

_Java-only: programmatic CryptoDataFormat with custom algorithm and HMAC_

```java
KeyGenerator generator = KeyGenerator.getInstance("DES");

CryptoDataFormat cryptoFormat = new CryptoDataFormat("DES", generator.generateKey());
cryptoFormat.setShouldAppendHMAC(true);
cryptoFormat.setMacAlgorithm("HmacMD5");

from("direct:hmac-algorithm")
    .marshal(cryptoFormat)
    .to("mock:encrypted")
    .unmarshal(cryptoFormat)
    .to("mock:unencrypted");
```

A list of the available algorithms in Java 17 is available via the [Java Security Standard Algorithm Names](https://docs.oracle.com/en/java/javase/17/docs/specs/security/standard-names.md) documentation.

## Specifying an Initialization Vector

Some crypto algorithms, particularly block algorithms, require configuration with an initial block of data known as an Initialization Vector. In the JCE this is passed as an AlgorithmParameterSpec when the Cipher is initialized. To use such a vector with the CryptoDataFormat, you can configure it with a byte\[\] containing the required data, e.g.

_Java-only: programmatic CryptoDataFormat with initialization vector_

```java
KeyGenerator generator = KeyGenerator.getInstance("DES");
byte[] initializationVector = new byte[] {0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07};

CryptoDataFormat cryptoFormat = new CryptoDataFormat("DES/CBC/PKCS5Padding", generator.generateKey());
cryptoFormat.setInitializationVector(initializationVector);

from("direct:init-vector")
    .marshal(cryptoFormat)
    .to("mock:encrypted")
    .unmarshal(cryptoFormat)
    .to("mock:unencrypted");
```

or with spring, suppling a reference to a byte\[\]

```xml
<crypto id="initvector" algorithm="DES/CBC/PKCS5Padding" key="desKey" initVector="initializationVector" />
```

The same vector is required in both the encryption and decryption phases. As it is not necessary to keep the IV a secret, the DataFormat allows for it to be inlined into the encrypted data and subsequently read out in the decryption phase to initialize the Cipher. To inline the IV set the `Inline` flag.

-   Java
    
-   Spring XML
    

```java
KeyGenerator generator = KeyGenerator.getInstance("DES");
byte[] initializationVector = new byte[] {0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07};
SecretKey key = generator.generateKey();

CryptoDataFormat cryptoFormat = new CryptoDataFormat("DES/CBC/PKCS5Padding", key);
cryptoFormat.setInitializationVector(initializationVector);
cryptoFormat.setShouldInlineInitializationVector(true);
CryptoDataFormat decryptFormat = new CryptoDataFormat("DES/CBC/PKCS5Padding", key);
decryptFormat.setShouldInlineInitializationVector(true);

from("direct:inline")
    .marshal(cryptoFormat)
    .to("mock:encrypted")
    .unmarshal(decryptFormat)
    .to("mock:unencrypted");
```

```xml
<crypto id="inline" algorithm="DES/CBC/PKCS5Padding" key="desKey" initVector="initializationVector"
  inline="true" />
<crypto id="inline-decrypt" algorithm="DES/CBC/PKCS5Padding" key="desKey" inline="true" />
```

For more information about the use of Initialization Vectors, consult

-   [http://en.wikipedia.org/wiki/Initialization\_vector](http://en.wikipedia.org/wiki/Initialization_vector)
    
-   [http://www.herongyang.com/Cryptography/](http://www.herongyang.com/Cryptography/)
    
-   [http://en.wikipedia.org/wiki/Block\_cipher\_mode\_of\_operation](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation)
    

## Hashed Message Authentication Codes (HMAC)

To avoid attacks against the encrypted data while it is in transit, the CryptoDataFormat can also calculate a Message Authentication Code for the encrypted exchange contents based on a configurable MAC algorithm. The calculated HMAC is appended to the stream after encryption. It is separated from the stream in the decryption phase. The MAC is recalculated and verified against the transmitted version to ensure nothing was tampered with in transit. For more information on Message Authentication Codes see [http://en.wikipedia.org/wiki/HMAC](http://en.wikipedia.org/wiki/HMAC)

-   Java
    
-   Spring XML
    

```java
KeyGenerator generator = KeyGenerator.getInstance("DES");

CryptoDataFormat cryptoFormat = new CryptoDataFormat("DES", generator.generateKey());
cryptoFormat.setShouldAppendHMAC(true);

from("direct:hmac")
    .marshal(cryptoFormat)
    .to("mock:encrypted")
    .unmarshal(cryptoFormat)
    .to("mock:unencrypted");
```

```xml
<crypto id="hmac" algorithm="DES" key="desKey" shouldAppendHMAC="true" />
```

By default, the HMAC is calculated using the HmacSHA1 mac algorithm, though this can be easily changed by supplying a different algorithm name. See here for how to check what algorithms are available through the configured security providers

-   Java
    
-   Spring XML
    

```java
KeyGenerator generator = KeyGenerator.getInstance("DES");

CryptoDataFormat cryptoFormat = new CryptoDataFormat("DES", generator.generateKey());
cryptoFormat.setShouldAppendHMAC(true);
cryptoFormat.setMacAlgorithm("HmacMD5");

from("direct:hmac-algorithm")
    .marshal(cryptoFormat)
    .to("mock:encrypted")
    .unmarshal(cryptoFormat)
    .to("mock:unencrypted");
```

```xml
<crypto id="hmac-algorithm" algorithm="DES" key="desKey" macAlgorithm="HmacMD5" shouldAppendHMAC="true" />
```

## Supplying Keys Dynamically

When using a Recipient list or similar EIP, the recipient of an exchange can vary dynamically. Using the same key across all recipients may neither be feasible nor desirable. It would be useful to be able to specify keys dynamically on a per-exchange basis. The exchange could then be dynamically enriched with the key of its target recipient before being processed by the data format. To facilitate this, the DataFormat allows for keys to be supplied dynamically via the message headers below

-   CryptoDataFormat.KEY "CamelCryptoKey"
    

-   Java
    
-   Spring XML
    

```java
CryptoDataFormat cryptoFormat = new CryptoDataFormat("DES", null);
/**
 * Note: the header containing the key should be cleared after
 * marshaling to stop it from leaking by accident and
 * potentially being compromised. The processor version below is
 * arguably better as the key is left in the header when you use
 * the DSL leaks the fact that camel encryption was used.
 */
from("direct:key-in-header-encrypt")
    .marshal(cryptoFormat)
    .removeHeader(CryptoDataFormat.KEY)
    .to("mock:encrypted");

from("direct:key-in-header-decrypt").unmarshal(cryptoFormat).process(new Processor() {
    public void process(Exchange exchange) throws Exception {
        exchange.getIn().getHeaders().remove(CryptoDataFormat.KEY);
        exchange.getMessage().copyFrom(exchange.getIn());
    }
}).to("mock:unencrypted");
```

```xml
<crypto id="nokey" algorithm="DES" />
```

## Dependencies

To use the [Crypto](../crypto-component.md) dataformat in your camel routes, you need to add the following dependency to your pom.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-crypto</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

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