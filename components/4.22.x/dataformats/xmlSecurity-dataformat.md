# XML Security

**Since Camel 2.0**

The XMLSecurity Data Format facilitates encryption and decryption of XML payloads at the Document, Element, and Element Content levels (including simultaneous multi-node encryption/decryption using XPath). To sign messages using the XML Signature specification, please see the Camel XML Security component.

The encryption capability is based on formats supported using the Apache XML Security (Santuario) project. Symmetric encryption/decryption is currently supported using Triple-DES and AES (128, 192, and 256) encryption formats. Additional formats can be easily added later as needed. This capability allows Camel users to encrypt/decrypt payloads while being dispatched or received along a route.

**Since Camel 2.9**  
The XMLSecurity Data Format supports asymmetric key encryption. In this encryption model, a symmetric key is generated and used to perform XML content encryption or decryption. This "content encryption key" is then itself encrypted using an asymmetric encryption algorithm that leverages the recipient’s public key as the "key encryption key". Use of an asymmetric key encryption algorithm ensures that only the holder of the recipient’s private key can access the generated symmetric encryption key. Thus, only the private key holder can decode the message. The XMLSecurity Data Format handles all the logic required to encrypt and decrypt the message content and encryption key(s) using asymmetric key encryption.

The XMLSecurity Data Format also has improved support for namespaces when processing the XPath queries that select content for encryption. A namespace definition mapping can be included as part of the data format configuration. This enables true namespace matching, even if the prefix values in the XPath query and the target XML document are not equivalent strings.

## XMLSecurity Options

The XML Security dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **xmlCipherAlgorithm** (common) | `AES-256-GCM` | `Enum` | 
The cipher algorithm to be used for encryption/decryption of the XML message content.

Enum values:

-   TRIPLEDES
    
-   AES\_128
    
-   AES\_128\_GCM
    
-   AES\_192
    
-   AES\_192\_GCM
    
-   AES\_256
    
-   AES\_256\_GCM
    
-   SEED\_128
    
-   CAMELLIA\_128
    
-   CAMELLIA\_192
    
-   CAMELLIA\_256
    





 |
| **passPhrase** (common) |  | `String` | A String used as passPhrase to encrypt/decrypt content. |
| **passPhraseByte** (advanced) |  | `String` | A byte used as passPhrase to encrypt/decrypt content. |
| **secureTag** (common) |  | `String` | The XPath reference to the XML Element selected for encryption/decryption. If no tag is specified, the entire payload is encrypted/decrypted. |
| **secureTagContents** (common) | `false` | `Boolean` | A boolean value to specify whether the XML Element is to be encrypted or the contents of the XML Element. false = Element Level, true = Element Content Level. |
| **keyCipherAlgorithm** (common) | `RSA_OAEP` | `Enum` | 

The cipher algorithm to be used for encryption/decryption of the asymmetric key.

Enum values:

-   RSA\_v1dot5
    
-   RSA\_OAEP
    
-   RSA\_OAEP\_11
    





 |
| **recipientKeyAlias** (common) |  | `String` | The key alias to be used when retrieving the recipient’s public or private key from a KeyStore when performing asymmetric key encryption or decryption. |
| **keyOrTrustStoreParameters** (common) |  | `Object` | Refers to a KeyStore instance to lookup in the registry, which is used for configuration options for creating and loading a KeyStore instance that represents the sender’s trustStore or recipient’s keyStore. |
| **keyPassword** (common) |  | `String` | The password to be used for retrieving the private key from the KeyStore. This key is used for asymmetric decryption. |
| **digestAlgorithm** (common) | `SHA1` | `Enum` | 

The digest algorithm to use with the RSA OAEP algorithm.

Enum values:

-   SHA1
    
-   SHA256
    
-   SHA512
    





 |
| **mgfAlgorithm** (common) | `MGF1_SHA1` | `Enum` | 

The MGF Algorithm to use with the RSA OAEP algorithm.

Enum values:

-   MGF1\_SHA1
    
-   MGF1\_SHA256
    
-   MGF1\_SHA512
    





 |
| **addKeyValueForEncryptedKey** (common) | `true` | `Boolean` | Whether to add the public key used to encrypt the session key as a KeyValue in the EncryptedKey structure or not. |
| **namespace** (common) |  | `Object` | Refers to a Map of XML Namespaces of prefix to uri mappings. |

### Key Cipher Algorithm

The default Key Cipher Algorithm is now `XMLCipher.RSA_OAEP` instead of `XMLCipher.RSA_v1dot5`. Usage of `XMLCipher.RSA_v1dot5` is discouraged due to various attacks. Requests that use RSA v1.5 as the key cipher algorithm will be rejected unless it has been explicitly configured as the key cipher algorithm.

### Data Cipher Algorithm

The default data (payload) Cipher Algorithm is `XMLCipher.AES_256_GCM`. Usage of `XMLCipher.TRIPLEDES` (3DES) is discouraged as it is a legacy cipher; prefer an AES-GCM algorithm such as `XMLCipher.AES_256_GCM` (the default) or `XMLCipher.AES_128_GCM`.

## Marshal

To encrypt the payload, the `marshal` processor needs to be applied on the route followed by the **`xmlSecurity()`** tag.

## Unmarshal

To decrypt the payload, the `unmarshal` processor needs to be applied on the route followed by the **`xmlSecurity()`** tag.

## Examples

Given below are several examples of how marshalling could be performed at the Document, Element, and Content levels.

### Full Payload encryption/decryption

_Java-only: full payload encryption using generated AES key_

```java
KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
keyGenerator.init(256);
Key key = keyGenerator.generateKey();

from("direct:start")
    .marshal().xmlSecurity(key.getEncoded())
    .unmarshal().xmlSecurity(key.getEncoded()
    .to("direct:end");
```

### Partial Payload Content Only encryption/decryption with choice of passPhrase(password)

_Java-only: partial payload encryption with passPhrase_

```java
String tagXPATH = "//cheesesites/italy/cheese";
boolean secureTagContent = true;
...
String passPhrase = "Just another 32 Byte key for AES";
from("direct:start")
    .marshal().xmlSecurity(tagXPATH, secureTagContent, passPhrase)
    .unmarshal().xmlSecurity(tagXPATH, secureTagContent, passPhrase)
    .to("direct:end");
```

### Partial Payload Content Only encryption/decryption with passPhrase(password) and Algorithm

_Java-only: partial payload encryption with passPhrase and algorithm_

```java
import org.apache.xml.security.encryption.XMLCipher;
....
String tagXPATH = "//cheesesites/italy/cheese";
boolean secureTagContent = true;
String passPhrase = "Just another 32 Byte key for AES";
String algorithm = XMLCipher.AES_256_GCM;
from("direct:start")
    .marshal().xmlSecurity(tagXPATH, secureTagContent, passPhrase, algorithm)
    .unmarshal().xmlSecurity(tagXPATH, secureTagContent, passPhrase, algorithm)
    .to("direct:end");
```

### Partial Payload Content with Namespace support

Java DSL

_Java-only: namespace-aware encryption with asymmetric key and KeyStore_

```java
final Map<String, String> namespaces = new HashMap<String, String>();
namespaces.put("cust", "http://cheese.xmlsecurity.camel.apache.org/");

final KeyStoreParameters tsParameters = new KeyStoreParameters();
tsParameters.setPassword("password");
tsParameters.setResource("sender.truststore");

from("direct:start")
    .marshal().xmlSecurity("//cust:cheesesites/italy", namespaces, true, "recipient",
                            testCypherAlgorithm, XMLCipher.RSA_v1dot5, tsParameters)
    .to("mock:encrypted");
```

Spring XML

A namespace prefix defined as part of the `camelContext` definition can be re-used in context within the data format `secureTag` attribute of the `xmlSecurity` element.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .marshal().xmlSecurity("//cheese:cheesesites/italy", true)
    .to("...");
```

```xml
<camelContext id="springXmlSecurityDataFormatTestCamelContext"
              xmlns="http://camel.apache.org/schema/spring"
              xmlns:cheese="http://cheese.xmlsecurity.camel.apache.org/">
    <route>
        <from uri="direct://start"/>
            <marshal>
                <xmlSecurity secureTag="//cheese:cheesesites/italy"
                           secureTagContents="true"/>
            </marshal>
            ...
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            xmlSecurity:
              secureTag: "//cheese:cheesesites/italy"
              secureTagContents: true
```

### Asymmetric Key Encryption

Spring XML Sender

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .marshal().xmlSecurity("//cheese:cheesesites/italy", namespaces, true,
            "recipient", XMLCipher.AES_128_CBC, XMLCipher.RSA_v1dot5, trustStoreParams)
    .to("...");
```

```xml
<!--  trust store configuration -->
<camel:keyStoreParameters id="trustStoreParams" resource="./sender.truststore" password="password"/>

<camelContext id="springXmlSecurityDataFormatTestCamelContext"
              xmlns="http://camel.apache.org/schema/spring"
              xmlns:cheese="http://cheese.xmlsecurity.camel.apache.org/">
    <route>
        <from uri="direct://start"/>
            <marshal>
                <xmlSecurity secureTag="//cheese:cheesesites/italy"
                           secureTagContents="true"
                           xmlCipherAlgorithm="http://www.w3.org/2001/04/xmlenc#aes128-cbc"
                           keyCipherAlgorithm="http://www.w3.org/2001/04/xmlenc#rsa-1_5"
                           recipientKeyAlias="recipient"
                           keyOrTrustStoreParametersRef="trustStoreParams"/>
            </marshal>
            ...
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            xmlSecurity:
              secureTag: "//cheese:cheesesites/italy"
              secureTagContents: true
              xmlCipherAlgorithm: "http://www.w3.org/2001/04/xmlenc#aes128-cbc"
              keyCipherAlgorithm: "http://www.w3.org/2001/04/xmlenc#rsa-1_5"
              recipientKeyAlias: recipient
              keyOrTrustStoreParametersRef: "#trustStoreParams"
```

Spring XML Recipient

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:encrypted")
    .unmarshal().xmlSecurity("//cheese:cheesesites/italy", namespaces, true,
            "recipient", XMLCipher.AES_128_CBC, XMLCipher.RSA_v1dot5, keyStoreParams)
    .to("...");
```

```xml
<!--  key store configuration -->
<camel:keyStoreParameters id="keyStoreParams" resource="./recipient.keystore" password="password" />

<camelContext id="springXmlSecurityDataFormatTestCamelContext"
              xmlns="http://camel.apache.org/schema/spring"
              xmlns:cheese="http://cheese.xmlsecurity.camel.apache.org/">
    <route>
        <from uri="direct://encrypted"/>
            <unmarshal>
                <xmlSecurity secureTag="//cheese:cheesesites/italy"
                           secureTagContents="true"
                           xmlCipherAlgorithm="http://www.w3.org/2001/04/xmlenc#aes128-cbc"
                           keyCipherAlgorithm="http://www.w3.org/2001/04/xmlenc#rsa-1_5"
                           recipientKeyAlias="recipient"
                           keyOrTrustStoreParametersRef="keyStoreParams"
                           keyPassword="privateKeyPassword" />
            </unmarshal>
            ...
```

```yaml
- route:
    from:
      uri: direct:encrypted
      steps:
        - unmarshal:
            xmlSecurity:
              secureTag: "//cheese:cheesesites/italy"
              secureTagContents: true
              xmlCipherAlgorithm: "http://www.w3.org/2001/04/xmlenc#aes128-cbc"
              keyCipherAlgorithm: "http://www.w3.org/2001/04/xmlenc#rsa-1_5"
              recipientKeyAlias: recipient
              keyOrTrustStoreParametersRef: "#keyStoreParams"
              keyPassword: privateKeyPassword
```

## Dependencies

This data format is provided within the **camel-xmlsecurity** component.