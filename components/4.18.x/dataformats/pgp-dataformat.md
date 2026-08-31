# PGP

**Since Camel 2.9**

The PGP Data Format integrates the Java Cryptographic Extension into Camel, allowing simple and flexible encryption and decryption of messages using Camel’s familiar marshal and unmarshal formatting mechanism. It assumes marshalling to mean encryption to ciphertext and unmarshalling to mean decryption back to the original plaintext. This data format implements only symmetric (shared-key) encryption and decryption.

## PGPDataFormat Options

The PGP dataformat supports 15 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **keyUserid** (common) |  | `String` | The user ID of the key in the PGP keyring used during encryption. Can also be only a part of a user ID. For example, if the user ID is Test User then you can use the part Test User or to address the user ID. |
| **signatureKeyUserid** (common) |  | `String` | User ID of the key in the PGP keyring used for signing (during encryption) or signature verification (during decryption). During the signature verification process the specified User ID restricts the public keys from the public keyring which can be used for the verification. If no User ID is specified for the signature verficiation then any public key in the public keyring can be used for the verification. Can also be only a part of a user ID. For example, if the user ID is Test User then you can use the part Test User or to address the User ID. |
| **password** (common) |  | `String` | Password used when opening the private key (not used for encryption). |
| **signaturePassword** (common) |  | `String` | Password used when opening the private key used for signing (during encryption). |
| **keyFileName** (common) |  | `String` | Filename of the keyring; must be accessible as a classpath resource (but you can specify a location in the file system by using the file: prefix). |
| **signatureKeyFileName** (common) |  | `String` | Filename of the keyring to use for signing (during encryption) or for signature verification (during decryption); must be accessible as a classpath resource (but you can specify a location in the file system by using the file: prefix). |
| **signatureKeyRing** (common) |  | `String` | Keyring used for signing/verifying as byte array. You can not set the signatureKeyFileName and signatureKeyRing at the same time. |
| **armored** (common) | `false` | `Boolean` | This option will cause PGP to base64 encode the encrypted text, making it available for copy/paste, etc. |
| **integrity** (common) | `true` | `Boolean` | Adds an integrity check/sign into the encryption file. The default value is true. |
| **provider** (common) |  | `String` | Java Cryptography Extension (JCE) provider, default is Bouncy Castle (BC). Alternatively you can use, for example, the IAIK JCE provider; in this case the provider must be registered beforehand and the Bouncy Castle provider must not be registered beforehand. The Sun JCE provider does not work. |
| **algorithm** (common) |  | `Integer` | Symmetric key encryption algorithm; possible values are defined in org.bouncycastle.bcpg.SymmetricKeyAlgorithmTags; for example 2 (= TRIPLE DES), 3 (= CAST5), 4 (= BLOWFISH), 6 (= DES), 7 (= AES\_128). Only relevant for encrypting. |
| **compressionAlgorithm** (common) |  | `Integer` | Compression algorithm; possible values are defined in org.bouncycastle.bcpg.CompressionAlgorithmTags; for example 0 (= UNCOMPRESSED), 1 (= ZIP), 2 (= ZLIB), 3 (= BZIP2). Only relevant for encrypting. |
| **hashAlgorithm** (common) |  | `Integer` | Signature hash algorithm; possible values are defined in org.bouncycastle.bcpg.HashAlgorithmTags; for example 2 (= SHA1), 8 (= SHA256), 9 (= SHA384), 10 (= SHA512), 11 (=SHA224). Only relevant for signing. |
| **signatureVerificationOption** (common) |  | `String` | Controls the behavior for verifying the signature during unmarshaling. There are 4 values possible: optional: The PGP message may or may not contain signatures; if it does contain signatures, then a signature verification is executed. required: The PGP message must contain at least one signature; if this is not the case an exception (PGPException) is thrown. A signature verification is executed. ignore: Contained signatures in the PGP message are ignored; no signature verification is executed. no\_signature\_allowed: The PGP message must not contain a signature; otherwise an exception (PGPException) is thrown. |
| **requireIntegrityProtection** (common) | `true` | `Boolean` | Whether a message must be integrity protected in order to be decrypted. The legacy symmetrically encrypted data packet carries no modification detection code, and the packet type is chosen by whoever produced the message, so accepting it lets the sender decide whether the integrity check applies. Set to false only to interoperate with a sender that still emits the legacy packet. |

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
| `CamelPGPDataFormatNumberOfEncryptionKeys` | `Integer` | number of public keys used for encrypting the symmetric key, set by PGPDataFormat during the encryption process |
| `CamelPGPDataFormatNumberOfSigningKeys` | `Integer` | number of private keys used for creating signatures, set by PGPDataFormat during the signing process |

## Encrypting with PGPDataFormat

The following sample uses the popular PGP format for encrypting/decrypting files using the [Bouncy Castle Java libraries](http://www.bouncycastle.org/java.md):

The following sample performs signing + encryption, and then signature verification + decryption. It uses the same keyring for both signing and encryption, but you can obviously use different keys:

-   Java
    
-   Spring XML
    

```java
from("direct:pgp-encrypt")
    .marshal().pgp("file:pubring.gpg", "alice@example.com")
    .unmarshal().pgp("file:secring.gpg", "alice@example.com", "letmein");
```

```xml
<route>
  <from uri="direct:encrypt"/>
  <marshal><pgp keyFileName="file:pubring.gpg" keyUserid="alice@example.com"/></marshal>
  <unmarshal><pgp keyFileName="file:secring.gpg" keyUserid="alice@example.com" password="letmein"/></unmarshal>
</route>
```

### Working with the previous example

-   A public keyring file which contains the public keys used to encrypt the data
    
-   A private keyring file which contains the keys used to decrypt the data
    
-   The keyring password
    

### Managing your keyring

To manage the keyring, I use the command line tools, I find this to be the simplest approach to managing the keys. There are also Java libraries available from [http://www.bouncycastle.org/java.html](http://www.bouncycastle.org/java.md) if you would prefer to do it that way.

Install the command line utilities on linux

```bash
apt-get install gnupg
```

Create your keyring, entering a secure password

```bash
gpg --gen-key
```

If you need to import someone else’s public key so that you can encrypt a file for them.

```bash
gpg --import <filename.key
```

If you are using GnuPG versions prior to 2.1, the key formats are stored in different files that can be used, for example. You can check if the required files exist by running the following command:

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

A PGP Data Formatter can decrypt/verify messages which have been encrypted by different public keys or signed by different private keys. Provide the corresponding private keys in the secret keyring, the corresponding public keys in the public keyring, and the passphrases in the passphrase accessor.

```java
Map<String, String> userId2Passphrase = new HashMap<String, String>(2);
// add passphrases of several private keys whose corresponding public keys have been used to encrypt the messages
userId2Passphrase.put("UserIdOfKey1","passphrase1"); // you must specify the exact User ID!
userId2Passphrase.put("UserIdOfKey2","passphrase2");
PGPPassphraseAccessor passphraseAccessor = new PGPPassphraseAccessorDefault(userId2Passphrase);

PGPDataFormat pgpVerifyAndDecrypt = new PGPDataFormat();
pgpVerifyAndDecrypt.setPassphraseAccessor(passphraseAccessor);
// the method getSecKeyRing() provides the secret keyring as a byte array containing the private keys
pgpVerifyAndDecrypt.setEncryptionKeyRing(getSecKeyRing()); // alternatively, you can use setKeyFileName(keyfileName)
// the method getPublicKeyRing() provides the public keyring as a byte array containing the public keys
pgpVerifyAndDecrypt.setSignatureKeyRing((getPublicKeyRing());  // alternatively, you can use setSignatureKeyFileName(signatgureKeyfileName)
// it is not necessary to specify the encryption or signer User Id

from("direct:start")
         ...
        .unmarshal(pgpVerifyAndDecrypt) // can decrypt/verify messages encrypted/signed by different private/public keys
        ...
```

-   The functionality is especially useful to support the key exchange. If you want to exchange the private key for decrypting, you can accept for a period of time messages which are either encrypted with the old or new corresponding public key. Or if the sender wants to exchange his signer private key, you can accept for a period of time, the old or new signer key.
    
-   Technical background: The PGP encrypted data contains a Key ID of the public key which was used to encrypt the data. This Key ID can be used to locate the private key in the secret keyring to decrypt the data. The same mechanism is also used to locate the public key for verifying a signature. Therefore, you no longer must specify User IDs for the unmarshalling.
    

## Restricting the Signer Identities during PGP Signature Verification

If you verify a signature, you not only want to verify the correctness of the signature, but you also want to check that the signature comes from a certain identity or a specific set of identities. Therefore, it is possible to restrict the number of public keys from the public keyring which can be used for the verification of a signature.

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
 pgpVerifyWithSpecificKeysAndDecrypt.setSignatureKeyUserids(expectedSigUserIds); // if you have only one signer identity, then you can also use setSignatureKeyUserid("expected Signer")

from("direct:start")
         ...
        .unmarshal(pgpVerifyWithSpecificKeysAndDecrypt)
        ...
```

-   If the PGP content has several signatures, the verification is successful as soon as one signature can be verified.
    
-   If you do not want to restrict the signer identities for verification, then do not specify the signature key User IDs. In this case, all public keys in the public keyring are taken into account.
    

## Several Signatures in One PGP Data Format

The PGP specification allows that one PGP data format can contain several signatures from different keys. Since Camel 2.13.3, it’s been possible to create such kind of PGP content via specifying signature User IDs which relate to several private keys in the secret keyring.

**Several Signatures**

```java
 PGPDataFormat pgpSignAndEncryptSeveralSignerKeys = new PGPDataFormat();
 pgpSignAndEncryptSeveralSignerKeys.setKeyUserid(keyUserid); // for encrypting, you can also use setKeyUserids if you want to encrypt with several keys
 pgpSignAndEncryptSeveralSignerKeys.setKeyFileName(keyfileName);
 pgpSignAndEncryptSeveralSignerKeys.setSignatureKeyFileName(signatgureKeyfileName);
 pgpSignAndEncryptSeveralSignerKeys.setSignaturePassword("sdude"); // here we assume that all private keys have the same password, if this is not the case, then you can use setPassphraseAccessor

 List<String> signerUserIds = new ArrayList<String>();
 signerUserIds.add("company old key");
 signerUserIds.add("company new key");
 pgpSignAndEncryptSeveralSignerKeys.setSignatureKeyUserids(signerUserIds);

from("direct:start")
         ...
        .marshal(pgpSignAndEncryptSeveralSignerKeys)
        ...
```

## Support for Sub-Keys and Key Flags in PGP Data Format Marshaller

An [OpenPGP V4 key](https://tools.ietf.org/html/rfc4880#section-12.1) can have a primary key and sub-keys. The usage of the keys is indicated by the so-called [Key Flags](https://tools.ietf.org/html/rfc4880#section-5.2.3.21). For example, you can have a primary key with two sub-keys; the primary key shall only be used for certifying other keys (Key Flag 0x01), the first sub-key shall only be used for signing (Key Flag 0x02), and the second sub-key shall only be used for encryption (Key Flag 0x04 or 0x08). The PGP Data Format marshaler takes into account these Key Flags of the primary key and sub-keys in order to determine the right key for signing and encryption. This is necessary because the primary key and its sub-keys have the same User IDs.

## Support for Custom Key Accessors

You can implement custom key accessors for encryption/signing. The above PGPDataFormat class selects in a certain predefined way the keys which should be used for signing/encryption or verifying/decryption. If you have special requirements for how your keys should be selected, you should use the [PGPKeyAccessDataFormat](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/PGPKeyAccessDataFormat.java) class instead and implement the interfaces [PGPPublicKeyAccessor](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/PGPPublicKeyAccessor.java) and [PGPSecretKeyAccessor](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/PGPSecretKeyAccessor.java) as beans. There are default implementations [DefaultPGPPublicKeyAccessor](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/DefaultPGPPublicKeyAccessor.java) and [DefaultPGPSecretKeyAccessor](https://github.com/apache/camel/blob/main/components/camel-crypto/src/main/java/org/apache/camel/converter/crypto/DefaultPGPSecretKeyAccessor.java) which cache the keys, so that not every time the keyring is parsed when the processor is called.

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
  <artifactId>camel-crypto-pgp-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 15 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
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