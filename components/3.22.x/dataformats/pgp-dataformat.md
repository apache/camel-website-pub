# PGP

**Since Camel 2.9**

The PGP Data Format integrates the Java Cryptographic Extension into Camel, allowing simple and flexible encryption and decryption of messages using Camel’s familiar marshal and unmarshal formatting mechanism. It assumes marshalling to mean encryption to ciphertext and unmarshalling to mean decryption back to the original plaintext. This data format implements only symmetric (shared-key) encryption and decryption.

## PGPDataFormat Options

The PGP dataformat supports 14 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **keyUserid** |  | `String` | The user ID of the key in the PGP keyring used during encryption. Can also be only a part of a user ID. For example, if the user ID is Test User then you can use the part Test User or to address the user ID. |
| **signatureKeyUserid** |  | `String` | User ID of the key in the PGP keyring used for signing (during encryption) or signature verification (during decryption). During the signature verification process the specified User ID restricts the public keys from the public keyring which can be used for the verification. If no User ID is specified for the signature verficiation then any public key in the public keyring can be used for the verification. Can also be only a part of a user ID. For example, if the user ID is Test User then you can use the part Test User or to address the User ID. |
| **password** |  | `String` | Password used when opening the private key (not used for encryption). |
| **signaturePassword** |  | `String` | Password used when opening the private key used for signing (during encryption). |
| **keyFileName** |  | `String` | Filename of the keyring; must be accessible as a classpath resource (but you can specify a location in the file system by using the file: prefix). |
| **signatureKeyFileName** |  | `String` | Filename of the keyring to use for signing (during encryption) or for signature verification (during decryption); must be accessible as a classpath resource (but you can specify a location in the file system by using the file: prefix). |
| **signatureKeyRing** |  | `String` | Keyring used for signing/verifying as byte array. You can not set the signatureKeyFileName and signatureKeyRing at the same time. |
| **armored** | `false` | `Boolean` | This option will cause PGP to base64 encode the encrypted text, making it available for copy/paste, etc. |
| **integrity** | `true` | `Boolean` | Adds an integrity check/sign into the encryption file. The default value is true. |
| **provider** |  | `String` | Java Cryptography Extension (JCE) provider, default is Bouncy Castle (BC). Alternatively you can use, for example, the IAIK JCE provider; in this case the provider must be registered beforehand and the Bouncy Castle provider must not be registered beforehand. The Sun JCE provider does not work. |
| **algorithm** |  | `Integer` | Symmetric key encryption algorithm; possible values are defined in org.bouncycastle.bcpg.SymmetricKeyAlgorithmTags; for example 2 (= TRIPLE DES), 3 (= CAST5), 4 (= BLOWFISH), 6 (= DES), 7 (= AES\_128). Only relevant for encrypting. |
| **compressionAlgorithm** |  | `Integer` | Compression algorithm; possible values are defined in org.bouncycastle.bcpg.CompressionAlgorithmTags; for example 0 (= UNCOMPRESSED), 1 (= ZIP), 2 (= ZLIB), 3 (= BZIP2). Only relevant for encrypting. |
| **hashAlgorithm** |  | `Integer` | Signature hash algorithm; possible values are defined in org.bouncycastle.bcpg.HashAlgorithmTags; for example 2 (= SHA1), 8 (= SHA256), 9 (= SHA384), 10 (= SHA512), 11 (=SHA224). Only relevant for signing. |
| **signatureVerificationOption** |  | `String` | Controls the behavior for verifying the signature during unmarshaling. There are 4 values possible: optional: The PGP message may or may not contain signatures; if it does contain signatures, then a signature verification is executed. required: The PGP message must contain at least one signature; if this is not the case an exception (PGPException) is thrown. A signature verification is executed. ignore: Contained signatures in the PGP message are ignored; no signature verification is executed. no\_signature\_allowed: The PGP message must not contain a signature; otherwise an exception (PGPException) is thrown. |

## PGPDataFormat Message Headers

You can override the PGPDataFormat options by applying the below headers into messages dynamically.

  
| Name | Type | Description |
| --- | --- | --- |
| `CamelPGPDataFormatKeyFileName` | `String` | filename of the keyring; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatEncryptionKeyRing` | `byte[]` | the encryption keyring; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatKeyUserid` | `String` | the User ID of the key in the PGP keyring; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatKeyUserids` | `List<String>` | the User IDs of the key in the PGP keyring; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatKeyPassword` | `String` | password used when opening the private key; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatSignatureKeyFileName` | `String` | filename of the signature keyring; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatSignatureKeyRing` | `byte[]` | the signature keyring; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatSignatureKeyUserid` | `String` | the User ID of the signature key in the PGP keyring; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatSignatureKeyUserids` | `List<String>` | the User IDs of the signature keys in the PGP keyring; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatSignatureKeyPassword` | `String` | password used when opening the signature private key; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatEncryptionAlgorithm` | `int` | symmetric key encryption algorithm; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatSignatureHashAlgorithm` | `int` | signature hash algorithm; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatCompressionAlgorithm` | `int` | compression algorithm; will override existing setting directly on the PGPDataFormat. |
| `CamelPGPDataFormatNumberOfEncryptionKeys` | `Integer` | number of public keys used for encrypting the symmectric key, set by PGPDataFormat during encryptiion process |
| `CamelPGPDataFormatNumberOfSigningKeys` | `Integer` | number of private keys used for creating signatures, set by PGPDataFormat during signing process |

## Encrypting with PGPDataFormat

The following sample uses the popular PGP format for encrypting/decrypting files using the [Bouncy Castle Java libraries](http://www.bouncycastle.org/java.md):

The following sample performs signing + encryption, and then signature verification + decryption. It uses the same keyring for both signing and encryption, but you can obviously use different keys:

```java
from("direct:pgp-encrypt")
    .marshal().pgp("file:pubring.gpg", "alice@example.com")
    .unmarshal().pgp("file:secring.gpg", "alice@example.com", "letmein");
```

Or using Spring:

```xml
<route>
  <from uri="direct:encrypt"/>
  <marshal><pgp keyFileName="file:pubring.gpg" keyUserid="alice@example.com"/></marshal>
  <unmarshal><pgp keyFileName="file:secring.gpg" keyUserid="alice@example.com" password="letmein"/></unmarshal>
</route>
```

### To work with the previous example you need the following

-   A public keyring file which contains the public keys used to encrypt the data
    
-   A private keyring file which contains the keys used to decrypt the data
    
-   The keyring password
    

### Managing your keyring

To manage the keyring, I use the command line tools, I find this to be the simplest approach in managing the keys. There are also Java libraries available from [http://www.bouncycastle.org/java.html](http://www.bouncycastle.org/java.md) if you would prefer to do it that way.

Install the command line utilities on linux

```bash
apt-get install gnupg
```

Create your keyring, entering a secure password

```bash
gpg --gen-key
```

If you need to import someone elses public key so that you can encrypt a file for them.

```bash
gpg --import <filename.key
```

If you are using GnuPG versions prior to 2.1, the key formats are stored in different files that can be used for the example. You can check if the required files exist by running the following command:

```bash
ls -l ~/.gnupg/pubring.gpg ~/.gnupg/secring.gpg
```

However, starting from GnuPG 2.1, the key formats were changed to improve efficiency and flexibility. Unfortunately, these new formats cannot be directly used with the Bouncy Castle libraries, which are used to implement the PGP data format. For more details about the changes to the key formats, you can refer to the [GnuPG FAQ](https://gnupg.org/faq/whats-new-in-2.1.md).

In the newer GnuPG versions, the `pubring.gpg` file is replaced with a keybox file named `pubring.kbx`. Additionally, the `secring.gpg` file is replaced with several files with a `.key` extension located in the `~/.gnupg/private-keys-v1.d` directory.

To export the keys to the older format that can be used with PGP data format, you can execute the following commands:

```bash
gpg --export > pubring.gpg
gpg --export-secret-keys > secring.gpg
```

## PGP Decrypting/Verifying of Messages Encrypted/Signed by Different Private/Public Keys

A PGP Data Formatter can decrypt/verify messages which have been encrypted by different public keys or signed by different private keys. Just provide the corresponding private keys in the secret keyring, the corresponding public keys in the public keyring, and the passphrases in the passphrase accessor.

```java
Map<String, String> userId2Passphrase = new HashMap<String, String>(2);
// add passphrases of several private keys whose corresponding public keys have been used to encrypt the messages
userId2Passphrase.put("UserIdOfKey1","passphrase1"); // you must specify the exact User ID!
userId2Passphrase.put("UserIdOfKey2","passphrase2");
PGPPassphraseAccessor passphraseAccessor = new PGPPassphraseAccessorDefault(userId2Passphrase);

PGPDataFormat pgpVerifyAndDecrypt = new PGPDataFormat();
pgpVerifyAndDecrypt.setPassphraseAccessor(passphraseAccessor);
// the method getSecKeyRing() provides the secret keyring as byte array containing the private keys
pgpVerifyAndDecrypt.setEncryptionKeyRing(getSecKeyRing()); // alternatively you can use setKeyFileName(keyfileName)
// the method getPublicKeyRing() provides the public keyring as byte array containing the public keys
pgpVerifyAndDecrypt.setSignatureKeyRing((getPublicKeyRing());  // alternatively you can use setSignatureKeyFileName(signatgureKeyfileName)
// it is not necessary to specify the encryption or signer  User Id

from("direct:start")
         ...
        .unmarshal(pgpVerifyAndDecrypt) // can decrypt/verify messages encrypted/signed by different private/public keys
        ...
```

-   The functionality is especially useful to support the key exchange. If you want to exchange the private key for decrypting you can accept for a period of time messages which are either encrypted with the old or new corresponding public key. Or if the sender wants to exchange his signer private key, you can accept for a period of time, the old or new signer key.
    
-   Technical background: The PGP encrypted data contains a Key ID of the public key which was used to encrypt the data. This Key ID can be used to locate the private key in the secret keyring to decrypt the data. The same mechanism is also used to locate the public key for verifying a signature. Therefore you no longer must specify User IDs for the unmarshaling.
    

## Restricting the Signer Identities during PGP Signature Verification

If you verify a signature you not only want to verify the correctness of the signature but you also want check that the signature comes from a certain identity or a specific set of identities. Therefore it is possible to restrict the number of public keys from the public keyring which can be used for the verification of a signature.

**Signature User IDs**

```java
// specify the User IDs of the expected signer identities
 List<String> expectedSigUserIds = new ArrayList<String>();
 expectedSigUserIds.add("Trusted company1");
 expectedSigUserIds.add("Trusted company2");

 PGPDataFormat pgpVerifyWithSpecificKeysAndDecrypt = new PGPDataFormat();
 pgpVerifyWithSpecificKeysAndDecrypt.setPassword("my password"); // for decrypting with private key
 pgpVerifyWithSpecificKeysAndDecrypt.setKeyFileName(keyfileName);
 pgpVerifyWithSpecificKeysAndDecrypt.setSignatureKeyFileName(signatgureKeyfileName);
 pgpVerifyWithSpecificKeysAndDecrypt.setSignatureKeyUserids(expectedSigUserIds); // if you have only one signer identity then you can also use setSignatureKeyUserid("expected Signer")

from("direct:start")
         ...
        .unmarshal(pgpVerifyWithSpecificKeysAndDecrypt)
        ...
```

-   If the PGP content has several signatures the verification is successful as soon as one signature can be verified.
    
-   If you do not want to restrict the signer identities for verification then do not specify the signature key User IDs. In this case all public keys in the public keyring are taken into account.
    

## Several Signatures in One PGP Data Format

The PGP specification allows that one PGP data format can contain several signatures from different keys. Since Camel 2.13.3 it is possible to create such kind of PGP content via specifying signature User IDs which relate to several private keys in the secret keyring.

**Several Signatures**

```java
 PGPDataFormat pgpSignAndEncryptSeveralSignerKeys = new PGPDataFormat();
 pgpSignAndEncryptSeveralSignerKeys.setKeyUserid(keyUserid); // for encrypting, you can also use setKeyUserids if you want to encrypt with several keys
 pgpSignAndEncryptSeveralSignerKeys.setKeyFileName(keyfileName);
 pgpSignAndEncryptSeveralSignerKeys.setSignatureKeyFileName(signatgureKeyfileName);
 pgpSignAndEncryptSeveralSignerKeys.setSignaturePassword("sdude"); // here we assume that all private keys have the same password, if this is not the case then you can use setPassphraseAccessor

 List<String> signerUserIds = new ArrayList<String>();
 signerUserIds.add("company old key");
 signerUserIds.add("company new key");
 pgpSignAndEncryptSeveralSignerKeys.setSignatureKeyUserids(signerUserIds);

from("direct:start")
         ...
        .marshal(pgpSignAndEncryptSeveralSignerKeys)
        ...
```

## Support of Sub-Keys and Key Flags in PGP Data Format Marshaler

An [OpenPGP V4 key](https://tools.ietf.org/html/rfc4880#section-12.1) can have a primary key and sub-keys. The usage of the keys is indicated by the so called [Key Flags](https://tools.ietf.org/html/rfc4880#section-5.2.3.21). For example, you can have a primary key with two sub-keys; the primary key shall only be used for certifying other keys (Key Flag 0x01), the first sub-key shall only be used for signing (Key Flag 0x02), and the second sub-key shall only be used for encryption (Key Flag 0x04 or 0x08). The PGP Data Format marshaler takes into account these Key Flags of the primary key and sub-keys in order to determine the right key for signing and encryption. This is necessary because the primary key and its sub-keys have the same User IDs.

## Support of Custom Key Accessors

You can implement custom key accessors for encryption/signing. The above PGPDataFormat class selects in a certain predefined way the keys which should be used for signing/encryption or verifying/decryption. If you have special requirements how your keys should be selected you should use the [PGPKeyAccessDataFormat](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/PGPKeyAccessDataFormat.java) class instead and implement the interfaces [PGPPublicKeyAccessor](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/PGPPublicKeyAccessor.java) and [PGPSecretKeyAccessor](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/PGPSecretKeyAccessor.java) as beans. There are default implementations [DefaultPGPPublicKeyAccessor](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/DefaultPGPPublicKeyAccessor.java) and [DefaultPGPSecretKeyAccessor](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/DefaultPGPSecretKeyAccessor.java) which cache the keys, so that not every time the keyring is parsed when the processor is called.

PGPKeyAccessDataFormat has the same options as PGPDataFormat except password, keyFileName, encryptionKeyRing, signaturePassword, signatureKeyFileName, and signatureKeyRing.

## Dependencies

To use the PGP dataformat in your camel routes you need to add the following dependency to your pom.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-crypto</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using pgp with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-crypto-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 47 options, which are listed below.

   
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
| **camel.dataformat.crypto.algorithm-parameter-ref** | A JCE AlgorithmParameterSpec used to initialize the Cipher. Will lookup the type using the given name as a java.security.spec.AlgorithmParameterSpec type. |  | String |
| **camel.dataformat.crypto.buffer-size** | The size of the buffer used in the signature process. | 4096 | Integer |
| **camel.dataformat.crypto.crypto-provider** | The name of the JCE Security Provider that should be used. |  | String |
| **camel.dataformat.crypto.enabled** | Whether to enable auto configuration of the crypto data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.crypto.init-vector-ref** | Refers to a byte array containing the Initialization Vector that will be used to initialize the Cipher. |  | String |
| **camel.dataformat.crypto.inline** | Flag indicating that the configured IV should be inlined into the encrypted data stream. Is by default false. | false | Boolean |
| **camel.dataformat.crypto.key-ref** | Refers to the secret key to lookup from the register to use. |  | String |
| **camel.dataformat.crypto.mac-algorithm** | The JCE algorithm name indicating the Message Authentication algorithm. | HmacSHA1 | String |
| **camel.dataformat.crypto.should-append-h-m-a-c** | Flag indicating that a Message Authentication Code should be calculated and appended to the encrypted data. | true | Boolean |
| **camel.dataformat.pgp.algorithm** | Symmetric key encryption algorithm; possible values are defined in org.bouncycastle.bcpg.SymmetricKeyAlgorithmTags; for example 2 (= TRIPLE DES), 3 (= CAST5), 4 (= BLOWFISH), 6 (= DES), 7 (= AES\_128). Only relevant for encrypting. |  | Integer |
| **camel.dataformat.pgp.armored** | This option will cause PGP to base64 encode the encrypted text, making it available for copy/paste, etc. | false | Boolean |
| **camel.dataformat.pgp.compression-algorithm** | Compression algorithm; possible values are defined in org.bouncycastle.bcpg.CompressionAlgorithmTags; for example 0 (= UNCOMPRESSED), 1 (= ZIP), 2 (= ZLIB), 3 (= BZIP2). Only relevant for encrypting. |  | Integer |
| **camel.dataformat.pgp.enabled** | Whether to enable auto configuration of the pgp data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.pgp.hash-algorithm** | Signature hash algorithm; possible values are defined in org.bouncycastle.bcpg.HashAlgorithmTags; for example 2 (= SHA1), 8 (= SHA256), 9 (= SHA384), 10 (= SHA512), 11 (=SHA224). Only relevant for signing. |  | Integer |
| **camel.dataformat.pgp.integrity** | Adds an integrity check/sign into the encryption file. The default value is true. | true | Boolean |
| **camel.dataformat.pgp.key-file-name** | Filename of the keyring; must be accessible as a classpath resource (but you can specify a location in the file system by using the file: prefix). |  | String |
| **camel.dataformat.pgp.key-userid** | The user ID of the key in the PGP keyring used during encryption. Can also be only a part of a user ID. For example, if the user ID is Test User then you can use the part Test User or to address the user ID. |  | String |
| **camel.dataformat.pgp.password** | Password used when opening the private key (not used for encryption). |  | String |
| **camel.dataformat.pgp.provider** | Java Cryptography Extension (JCE) provider, default is Bouncy Castle (BC). Alternatively you can use, for example, the IAIK JCE provider; in this case the provider must be registered beforehand and the Bouncy Castle provider must not be registered beforehand. The Sun JCE provider does not work. |  | String |
| **camel.dataformat.pgp.signature-key-file-name** | Filename of the keyring to use for signing (during encryption) or for signature verification (during decryption); must be accessible as a classpath resource (but you can specify a location in the file system by using the file: prefix). |  | String |
| **camel.dataformat.pgp.signature-key-ring** | Keyring used for signing/verifying as byte array. You can not set the signatureKeyFileName and signatureKeyRing at the same time. |  | String |
| **camel.dataformat.pgp.signature-key-userid** | User ID of the key in the PGP keyring used for signing (during encryption) or signature verification (during decryption). During the signature verification process the specified User ID restricts the public keys from the public keyring which can be used for the verification. If no User ID is specified for the signature verficiation then any public key in the public keyring can be used for the verification. Can also be only a part of a user ID. For example, if the user ID is Test User then you can use the part Test User or to address the User ID. |  | String |
| **camel.dataformat.pgp.signature-password** | Password used when opening the private key used for signing (during encryption). |  | String |
| **camel.dataformat.pgp.signature-verification-option** | Controls the behavior for verifying the signature during unmarshaling. There are 4 values possible: optional: The PGP message may or may not contain signatures; if it does contain signatures, then a signature verification is executed. required: The PGP message must contain at least one signature; if this is not the case an exception (PGPException) is thrown. A signature verification is executed. ignore: Contained signatures in the PGP message are ignored; no signature verification is executed. no\_signature\_allowed: The PGP message must not contain a signature; otherwise an exception (PGPException) is thrown. |  | String |