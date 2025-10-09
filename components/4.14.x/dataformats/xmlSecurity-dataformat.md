# XML Security

**Since Camel 2.0**

The XMLSecurity Data Format facilitates encryption and decryption of XML payloads at the Document, Element, and Element Content levels (including simultaneous multi-node encryption/decryption using XPath). To sign messages using the XML Signature specification, please see the Camel XML Security component.

The encryption capability is based on formats supported using the Apache XML Security (Santuario) project. Symmetric encryption/decryption is currently supported using Triple-DES and AES (128, 192, and 256) encryption formats. Additional formats can be easily added later as needed. This capability allows Camel users to encrypt/decrypt payloads while being dispatched or received along a route.

**Since Camel 2.9**  
The XMLSecurity Data Format supports asymmetric key encryption. In this encryption model, a symmetric key is generated and used to perform XML content encryption or decryption. This "content encryption key" is then itself encrypted using an asymmetric encryption algorithm that leverages the recipient’s public key as the "key encryption key". Use of an asymmetric key encryption algorithm ensures that only the holder of the recipient’s private key can access the generated symmetric encryption key. Thus, only the private key holder can decode the message. The XMLSecurity Data Format handles all the logic required to encrypt and decrypt the message content and encryption key(s) using asymmetric key encryption.

The XMLSecurity Data Format also has improved support for namespaces when processing the XPath queries that select content for encryption. A namespace definition mapping can be included as part of the data format configuration. This enables true namespace matching, even if the prefix values in the XPath query and the target XML document are not equivalent strings.

## XMLSecurity Options

The XML Security dataformat supports 12 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **xmlCipherAlgorithm** (common) | `AES-256-GCM` | `Enum` | 
The cipher algorithm to be used for encryption/decryption of the XML message content. The available choices are: XMLCipher.TRIPLEDES XMLCipher.AES\_128 XMLCipher.AES\_128\_GCM XMLCipher.AES\_192 XMLCipher.AES\_192\_GCM XMLCipher.AES\_256 XMLCipher.AES\_256\_GCM XMLCipher.SEED\_128 XMLCipher.CAMELLIA\_128 XMLCipher.CAMELLIA\_192 XMLCipher.CAMELLIA\_256 The default value is XMLCipher.AES\_256\_GCM.

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
| **passPhrase** (common) |  | `String` | A String used as passPhrase to encrypt/decrypt content. The passPhrase has to be provided. The passPhrase needs to be put together in conjunction with the appropriate encryption algorithm. For example using TRIPLEDES the passPhase can be a Only another 24 Byte key. |
| **passPhraseByte** (advanced) |  | `String` | A byte used as passPhrase to encrypt/decrypt content. The passPhrase has to be provided. The passPhrase needs to be put together in conjunction with the appropriate encryption algorithm. For example using TRIPLEDES the passPhase can be a Only another 24 Byte key. |
| **secureTag** (common) |  | `String` | The XPath reference to the XML Element selected for encryption/decryption. If no tag is specified, the entire payload is encrypted/decrypted. |
| **secureTagContents** (common) | `false` | `Boolean` | A boolean value to specify whether the XML Element is to be encrypted or the contents of the XML Element. false = Element Level. true = Element Content Level. |
| **keyCipherAlgorithm** (common) | `RSA_OAEP` | `Enum` | 

The cipher algorithm to be used for encryption/decryption of the asymmetric key. The available choices are: XMLCipher.RSA\_v1dot5 XMLCipher.RSA\_OAEP XMLCipher.RSA\_OAEP\_11 The default value is XMLCipher.RSA\_OAEP.

Enum values:

-   RSA\_v1dot5
    
-   RSA\_OAEP
    
-   RSA\_OAEP\_11
    





 |
| **recipientKeyAlias** (common) |  | `String` | The key alias to be used when retrieving the recipient’s public or private key from a KeyStore when performing asymmetric key encryption or decryption. |
| **keyOrTrustStoreParametersRef** (common) |  | `String` | Refers to a KeyStore instance to lookup in the registry, which is used for configuration options for creating and loading a KeyStore instance that represents the sender’s trustStore or recipient’s keyStore. |
| **keyPassword** (common) |  | `String` | The password to be used for retrieving the private key from the KeyStore. This key is used for asymmetric decryption. |
| **digestAlgorithm** (common) | `SHA1` | `Enum` | 

The digest algorithm to use with the RSA OAEP algorithm. The available choices are: XMLCipher.SHA1 XMLCipher.SHA256 XMLCipher.SHA512 The default value is XMLCipher.SHA1.

Enum values:

-   SHA1
    
-   SHA256
    
-   SHA512
    





 |
| **mgfAlgorithm** (common) | `MGF1_SHA1` | `Enum` | 

The MGF Algorithm to use with the RSA OAEP algorithm. The available choices are: EncryptionConstants.MGF1\_SHA1 EncryptionConstants.MGF1\_SHA256 EncryptionConstants.MGF1\_SHA512 The default value is EncryptionConstants.MGF1\_SHA1.

Enum values:

-   MGF1\_SHA1
    
-   MGF1\_SHA256
    
-   MGF1\_SHA512
    





 |
| **addKeyValueForEncryptedKey** (common) | `true` | `Boolean` | Whether to add the public key used to encrypt the session key as a KeyValue in the EncryptedKey structure or not. |

### Key Cipher Algorithm

The default Key Cipher Algorithm is now `XMLCipher.RSA_OAEP` instead of `XMLCipher.RSA_v1dot5`. Usage of `XMLCipher.RSA_v1dot5` is discouraged due to various attacks. Requests that use RSA v1.5 as the key cipher algorithm will be rejected unless it has been explicitly configured as the key cipher algorithm.

## Marshal

To encrypt the payload, the `marshal` processor needs to be applied on the route followed by the **`xmlSecurity()`** tag.

## Unmarshal

To decrypt the payload, the `unmarshal` processor needs to be applied on the route followed by the **`xmlSecurity()`** tag.

## Examples

Given below are several examples of how marshalling could be performed at the Document, Element, and Content levels.

### Full Payload encryption/decryption

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

```java
String tagXPATH = "//cheesesites/italy/cheese";
boolean secureTagContent = true;
...
String passPhrase = "Just another 24 Byte key";
from("direct:start")
    .marshal().xmlSecurity(tagXPATH, secureTagContent, passPhrase)
    .unmarshal().xmlSecurity(tagXPATH, secureTagContent, passPhrase)
    .to("direct:end");
```

### Partial Payload Content Only encryption/decryption with passPhrase(password) and Algorithm

```java
import org.apache.xml.security.encryption.XMLCipher;
....
String tagXPATH = "//cheesesites/italy/cheese";
boolean secureTagContent = true;
String passPhrase = "Just another 24 Byte key";
String algorithm= XMLCipher.TRIPLEDES;
from("direct:start")
    .marshal().xmlSecurity(tagXPATH, secureTagContent, passPhrase, algorithm)
    .unmarshal().xmlSecurity(tagXPATH, secureTagContent, passPhrase, algorithm)
    .to("direct:end");
```

### Partial Payload Content with Namespace support

Java DSL

```java
final Map<String, String> namespaces = new HashMap<String, String>();
namespaces.put("cust", "http://cheese.xmlsecurity.camel.apache.org/");

final KeyStoreParameters tsParameters = new KeyStoreParameters();
tsParameters.setPassword("password");
tsParameters.setResource("sender.truststore");

context.addRoutes(new RouteBuilder() {
    public void configure() {
        from("direct:start")
           .marshal().xmlSecurity("//cust:cheesesites/italy", namespaces, true, "recipient",
                                testCypherAlgorithm, XMLCipher.RSA_v1dot5, tsParameters)
           .to("mock:encrypted");
    }
}
```

Spring XML

A namespace prefix defined as part of the `camelContext` definition can be re-used in context within the data format `secureTag` attribute of the `xmlSecurity` element.

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

### Asymmetric Key Encryption

Spring XML Sender

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

Spring XML Recipient

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

## Dependencies

This data format is provided within the **camel-xmlsecurity** component.

## Spring Boot Auto-Configuration

When using xmlSecurity with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-xmlsecurity-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 62 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.xmlsecurity-sign.add-key-info-reference** | In order to protect the KeyInfo element from tampering you can add a reference to the signed info element so that it is protected via the signature value. The default value is true. Only relevant when a KeyInfo is returned by KeyAccessor. and KeyInfo#getId() is not null. | true | Boolean |
| **camel.component.xmlsecurity-sign.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.xmlsecurity-sign.base-uri** | You can set a base URI which is used in the URI dereferencing. Relative URIs are then concatenated with the base URI. |  | String |
| **camel.component.xmlsecurity-sign.canonicalization-method** | Canonicalization method used to canonicalize the SignedInfo element before the digest is calculated. You can use the helper methods XmlSignatureHelper.getCanonicalizationMethod(String algorithm) or getCanonicalizationMethod(String algorithm, List inclusiveNamespacePrefixes) to create a canonicalization method. The option is a javax.xml.crypto.AlgorithmMethod type. |  | AlgorithmMethod |
| **camel.component.xmlsecurity-sign.clear-headers** | Determines if the XML signature specific headers be cleared after signing and verification. Defaults to true. | true | Boolean |
| **camel.component.xmlsecurity-sign.content-object-id** | Sets the content object Id attribute value. By default a UUID is generated. If you set the null value, then a new UUID will be generated. Only used in the enveloping case. |  | String |
| **camel.component.xmlsecurity-sign.content-reference-type** | Type of the content reference. The default value is null. This value can be overwritten by the header XmlSignatureConstants#HEADER\_CONTENT\_REFERENCE\_TYPE. |  | String |
| **camel.component.xmlsecurity-sign.content-reference-uri** | Reference URI for the content to be signed. Only used in the enveloped case. If the reference URI contains an ID attribute value, then the resource schema URI ( setSchemaResourceUri(String)) must also be set because the schema validator will then find out which attributes are ID attributes. Will be ignored in the enveloping or detached case. |  | String |
| **camel.component.xmlsecurity-sign.crypto-context-properties** | Sets the crypto context properties. See \\{link XMLCryptoContext#setProperty(String, Object)}. Possible properties are defined in XMLSignContext an XMLValidateContext (see Supported Properties). The following properties are set by default to the value Boolean#TRUE for the XML validation. If you want to switch these features off you must set the property value to Boolean#FALSE. org.jcp.xml.dsig.validateManifests javax.xml.crypto.dsig.cacheReference. |  | Map |
| **camel.component.xmlsecurity-sign.digest-algorithm** | Digest algorithm URI. Optional parameter. This digest algorithm is used for calculating the digest of the input message. If this digest algorithm is not specified then the digest algorithm is calculated from the signature algorithm. Example: [http://www.w3.org/2001/04/xmlenc#sha256](http://www.w3.org/2001/04/xmlenc#sha256). |  | String |
| **camel.component.xmlsecurity-sign.disallow-doctype-decl** | Disallows that the incoming XML document contains DTD DOCTYPE declaration. The default value is Boolean#TRUE. | true | Boolean |
| **camel.component.xmlsecurity-sign.enabled** | Whether to enable auto configuration of the xmlsecurity-sign component. This is enabled by default. |  | Boolean |
| **camel.component.xmlsecurity-sign.key-accessor** | For the signing process, a private key is necessary. You specify a key accessor bean which provides this private key. The key accessor bean must implement the KeyAccessor interface. The package org.apache.camel.component.xmlsecurity.api contains the default implementation class DefaultKeyAccessor which reads the private key from a Java keystore. The option is a org.apache.camel.component.xmlsecurity.api.KeyAccessor type. |  | KeyAccessor |
| **camel.component.xmlsecurity-sign.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.xmlsecurity-sign.omit-xml-declaration** | Indicator whether the XML declaration in the outgoing message body should be omitted. Default value is false. Can be overwritten by the header XmlSignatureConstants#HEADER\_OMIT\_XML\_DECLARATION. | false | Boolean |
| **camel.component.xmlsecurity-sign.output-xml-encoding** | The character encoding of the resulting signed XML document. If null then the encoding of the original XML document is used. |  | String |
| **camel.component.xmlsecurity-sign.parent-local-name** | Local name of the parent element to which the XML signature element will be added. Only relevant for enveloped XML signature. Alternatively you can also use setParentXpath(XPathFilterParameterSpec). Default value is null. The value must be null for enveloping and detached XML signature. This parameter or the parameter setParentXpath(XPathFilterParameterSpec) for enveloped signature and the parameter setXpathsToIdAttributes(List) for detached signature must not be set in the same configuration. If the parameters parentXpath and parentLocalName are specified in the same configuration then an exception is thrown. |  | String |
| **camel.component.xmlsecurity-sign.parent-namespace** | Namespace of the parent element to which the XML signature element will be added. |  | String |
| **camel.component.xmlsecurity-sign.parent-xpath** | Sets the XPath to find the parent node in the enveloped case. Either you specify the parent node via this method or the local name and namespace of the parent with the methods setParentLocalName(String) and setParentNamespace(String). Default value is null. The value must be null for enveloping and detached XML signature. If the parameters parentXpath and parentLocalName are specified in the same configuration then an exception is thrown. The option is a javax.xml.crypto.dsig.spec.XPathFilterParameterSpec type. |  | XPathFilterParameterSpec |
| **camel.component.xmlsecurity-sign.plain-text** | Indicator whether the message body contains plain text. The default value is false, indicating that the message body contains XML. The value can be overwritten by the header XmlSignatureConstants#HEADER\_MESSAGE\_IS\_PLAIN\_TEXT. | false | Boolean |
| **camel.component.xmlsecurity-sign.plain-text-encoding** | Encoding of the plain text. Only relevant if the message body is plain text (see parameter plainText. Default value is UTF-8. | UTF-8 | String |
| **camel.component.xmlsecurity-sign.prefix-for-xml-signature-namespace** | Namespace prefix for the XML signature namespace [http://www.w3.org/2000/09/xmldsig#](http://www.w3.org/2000/09/xmldsig#). Default value is ds. If null or an empty value is set then no prefix is used for the XML signature namespace. See best practice [http://www.w3.org/TR/xmldsig-bestpractices/#signing-xml-](http://www.w3.org/TR/xmldsig-bestpractices/#signing-xml-) without-namespaces. | ds | String |
| **camel.component.xmlsecurity-sign.properties** | For adding additional References and Objects to the XML signature which contain additional properties, you can provide a bean which implements the XmlSignatureProperties interface. The option is a org.apache.camel.component.xmlsecurity.api.XmlSignatureProperties type. |  | XmlSignatureProperties |
| **camel.component.xmlsecurity-sign.schema-resource-uri** | Classpath to the XML Schema. Must be specified in the detached XML Signature case for determining the ID attributes, might be set in the enveloped and enveloping case. If set, then the XML document is validated with the specified XML schema. The schema resource URI can be overwritten by the header XmlSignatureConstants#HEADER\_SCHEMA\_RESOURCE\_URI. |  | String |
| **camel.component.xmlsecurity-sign.signature-algorithm** | Signature algorithm. Default value is [http://www.w3.org/2000/09/xmldsig#rsa-sha1](http://www.w3.org/2000/09/xmldsig#rsa-sha1). | [http://www.w3.org/2001/04/xmldsig-more#rsa-sha256](http://www.w3.org/2001/04/xmldsig-more#rsa-sha256) | String |
| **camel.component.xmlsecurity-sign.signature-id** | Sets the signature Id. If this parameter is not set (null value) then a unique ID is generated for the signature ID (default). If this parameter is set to (empty string) then no Id attribute is created in the signature element. |  | String |
| **camel.component.xmlsecurity-sign.signer-configuration** | To use a shared XmlSignerConfiguration configuration to use as base for configuring endpoints. The option is a org.apache.camel.component.xmlsecurity.processor.XmlSignerConfiguration type. |  | XmlSignerConfiguration |
| **camel.component.xmlsecurity-sign.transform-methods** | Transforms which are executed on the message body before the digest is calculated. By default, C14n is added and in the case of enveloped signature (see option parentLocalName) also [http://www.w3.org/2000/09/xmldsig#enveloped-signature](http://www.w3.org/2000/09/xmldsig#enveloped-signature) is added at position 0 of the list. Use methods in XmlSignatureHelper to create the transform methods. |  | List |
| **camel.component.xmlsecurity-sign.uri-dereferencer** | If you want to restrict the remote access via reference URIs, you can set an own dereferencer. Optional parameter. If not set the provider default dereferencer is used which can resolve URI fragments, HTTP, file and XPpointer URIs. Attention: The implementation is provider dependent!. The option is a javax.xml.crypto.URIDereferencer type. |  | URIDereferencer |
| **camel.component.xmlsecurity-sign.xpaths-to-id-attributes** | Define the elements which are signed in the detached case via XPATH expressions to ID attributes (attributes of type ID). For each element found via the XPATH expression a detached signature is created whose reference URI contains the corresponding attribute value (preceded by '#'). The signature becomes the last sibling of the signed element. Elements with deeper hierarchy level are signed first. You can also set the XPATH list dynamically via the header XmlSignatureConstants#HEADER\_XPATHS\_TO\_ID\_ATTRIBUTES. The parameter setParentLocalName(String) or setParentXpath(XPathFilterParameterSpec) for enveloped signature and this parameter for detached signature must not be set in the same configuration. |  | List |
| **camel.component.xmlsecurity-verify.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.xmlsecurity-verify.base-uri** | You can set a base URI which is used in the URI dereferencing. Relative URIs are then concatenated with the base URI. |  | String |
| **camel.component.xmlsecurity-verify.clear-headers** | Determines if the XML signature specific headers be cleared after signing and verification. Defaults to true. | true | Boolean |
| **camel.component.xmlsecurity-verify.crypto-context-properties** | Sets the crypto context properties. See \\{link XMLCryptoContext#setProperty(String, Object)}. Possible properties are defined in XMLSignContext an XMLValidateContext (see Supported Properties). The following properties are set by default to the value Boolean#TRUE for the XML validation. If you want to switch these features off you must set the property value to Boolean#FALSE. org.jcp.xml.dsig.validateManifests javax.xml.crypto.dsig.cacheReference. |  | Map |
| **camel.component.xmlsecurity-verify.disallow-doctype-decl** | Disallows that the incoming XML document contains DTD DOCTYPE declaration. The default value is Boolean#TRUE. | true | Boolean |
| **camel.component.xmlsecurity-verify.enabled** | Whether to enable auto configuration of the xmlsecurity-verify component. This is enabled by default. |  | Boolean |
| **camel.component.xmlsecurity-verify.key-selector** | Provides the key for validating the XML signature. The option is a javax.xml.crypto.KeySelector type. |  | KeySelector |
| **camel.component.xmlsecurity-verify.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.xmlsecurity-verify.omit-xml-declaration** | Indicator whether the XML declaration in the outgoing message body should be omitted. Default value is false. Can be overwritten by the header XmlSignatureConstants#HEADER\_OMIT\_XML\_DECLARATION. | false | Boolean |
| **camel.component.xmlsecurity-verify.output-node-search-type** | Determines the search type for determining the output node which is serialized into the output message bodyF. See setOutputNodeSearch(Object). The supported default search types you can find in DefaultXmlSignature2Message. | Default | String |
| **camel.component.xmlsecurity-verify.output-xml-encoding** | The character encoding of the resulting signed XML document. If null then the encoding of the original XML document is used. |  | String |
| **camel.component.xmlsecurity-verify.remove-signature-elements** | Indicator whether the XML signature elements (elements with local name Signature and namespace [http://www.w3.org/2000/09/xmldsig#](http://www.w3.org/2000/09/xmldsig#)) shall be removed from the document set to the output message. Normally, this is only necessary, if the XML signature is enveloped. The default value is Boolean#FALSE. This parameter is forwarded to XmlSignature2Message. This indicator has no effect if the output node search is of type DefaultXmlSignature2Message#OUTPUT\_NODE\_SEARCH\_TYPE\_DEFAULT.F. | false | Boolean |
| **camel.component.xmlsecurity-verify.schema-resource-uri** | Classpath to the XML Schema. Must be specified in the detached XML Signature case for determining the ID attributes, might be set in the enveloped and enveloping case. If set, then the XML document is validated with the specified XML schema. The schema resource URI can be overwritten by the header XmlSignatureConstants#HEADER\_SCHEMA\_RESOURCE\_URI. |  | String |
| **camel.component.xmlsecurity-verify.secure-validation** | Enables secure validation. If true then secure validation is enabled. | true | Boolean |
| **camel.component.xmlsecurity-verify.uri-dereferencer** | If you want to restrict the remote access via reference URIs, you can set an own dereferencer. Optional parameter. If not set the provider default dereferencer is used which can resolve URI fragments, HTTP, file and XPpointer URIs. Attention: The implementation is provider dependent!. The option is a javax.xml.crypto.URIDereferencer type. |  | URIDereferencer |
| **camel.component.xmlsecurity-verify.validation-failed-handler** | Handles the different validation failed situations. The default implementation throws specific exceptions for the different situations (All exceptions have the package name org.apache.camel.component.xmlsecurity.api and are a sub-class of XmlSignatureInvalidException. If the signature value validation fails, a XmlSignatureInvalidValueException is thrown. If a reference validation fails, a XmlSignatureInvalidContentHashException is thrown. For more detailed information, see the JavaDoc. The option is a org.apache.camel.component.xmlsecurity.api.ValidationFailedHandler type. |  | ValidationFailedHandler |
| **camel.component.xmlsecurity-verify.verifier-configuration** | To use a shared XmlVerifierConfiguration configuration to use as base for configuring endpoints. The option is a org.apache.camel.component.xmlsecurity.processor.XmlVerifierConfiguration type. |  | XmlVerifierConfiguration |
| **camel.component.xmlsecurity-verify.xml-signature-checker** | This interface allows the application to check the XML signature before the validation is executed. This step is recommended in [http://www.w3.org/TR/xmldsig-bestpractices/#check-what-is-signed](http://www.w3.org/TR/xmldsig-bestpractices/#check-what-is-signed). The option is a org.apache.camel.component.xmlsecurity.api.XmlSignatureChecker type. |  | XmlSignatureChecker |
| **camel.component.xmlsecurity-verify.xml-signature2-message** | Bean which maps the XML signature to the output-message after the validation. How this mapping should be done can be configured by the options outputNodeSearchType, outputNodeSearch, and removeSignatureElements. The default implementation offers three possibilities which are related to the three output node search types Default, ElementName, and XPath. The default implementation determines a node which is then serialized and set to the body of the output message If the search type is ElementName then the output node (which must be in this case an element) is determined by the local name and namespace defined in the search value (see option outputNodeSearch). If the search type is XPath then the output node is determined by the XPath specified in the search value (in this case the output node can be of type Element, TextNode or Document). If the output node search type is Default then the following rules apply: In the enveloped XML signature case (there is a reference with URI= and transform [http://www.w3.org/2000/09/xmldsig#enveloped-signature](http://www.w3.org/2000/09/xmldsig#enveloped-signature)), the incoming XML document without the Signature element is set to the output message body. In the non-enveloped XML signature case, the message body is determined from a referenced Object; this is explained in more detail in chapter Output Node Determination in Enveloping XML Signature Case. The option is a org.apache.camel.component.xmlsecurity.api.XmlSignature2Message type. |  | XmlSignature2Message |
| **camel.dataformat.xml-security.add-key-value-for-encrypted-key** | Whether to add the public key used to encrypt the session key as a KeyValue in the EncryptedKey structure or not. | true | Boolean |
| **camel.dataformat.xml-security.digest-algorithm** | The digest algorithm to use with the RSA OAEP algorithm. The available choices are: XMLCipher.SHA1 XMLCipher.SHA256 XMLCipher.SHA512 The default value is XMLCipher.SHA1. | SHA1 | String |
| **camel.dataformat.xml-security.enabled** | Whether to enable auto configuration of the xmlSecurity data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.xml-security.key-cipher-algorithm** | The cipher algorithm to be used for encryption/decryption of the asymmetric key. The available choices are: XMLCipher.RSA\_v1dot5 XMLCipher.RSA\_OAEP XMLCipher.RSA\_OAEP\_11 The default value is XMLCipher.RSA\_OAEP. | RSA\_OAEP | String |
| **camel.dataformat.xml-security.key-or-trust-store-parameters-ref** | Refers to a KeyStore instance to lookup in the registry, which is used for configuration options for creating and loading a KeyStore instance that represents the sender’s trustStore or recipient’s keyStore. |  | String |
| **camel.dataformat.xml-security.key-password** | The password to be used for retrieving the private key from the KeyStore. This key is used for asymmetric decryption. |  | String |
| **camel.dataformat.xml-security.mgf-algorithm** | The MGF Algorithm to use with the RSA OAEP algorithm. The available choices are: EncryptionConstants.MGF1\_SHA1 EncryptionConstants.MGF1\_SHA256 EncryptionConstants.MGF1\_SHA512 The default value is EncryptionConstants.MGF1\_SHA1. | MGF1\_SHA1 | String |
| **camel.dataformat.xml-security.pass-phrase** | A String used as passPhrase to encrypt/decrypt content. The passPhrase has to be provided. The passPhrase needs to be put together in conjunction with the appropriate encryption algorithm. For example using TRIPLEDES the passPhase can be a Only another 24 Byte key. |  | String |
| **camel.dataformat.xml-security.pass-phrase-byte** | A byte used as passPhrase to encrypt/decrypt content. The passPhrase has to be provided. The passPhrase needs to be put together in conjunction with the appropriate encryption algorithm. For example using TRIPLEDES the passPhase can be a Only another 24 Byte key. |  | Byte\[\] |
| **camel.dataformat.xml-security.recipient-key-alias** | The key alias to be used when retrieving the recipient’s public or private key from a KeyStore when performing asymmetric key encryption or decryption. |  | String |
| **camel.dataformat.xml-security.secure-tag** | The XPath reference to the XML Element selected for encryption/decryption. If no tag is specified, the entire payload is encrypted/decrypted. |  | String |
| **camel.dataformat.xml-security.secure-tag-contents** | A boolean value to specify whether the XML Element is to be encrypted or the contents of the XML Element. false = Element Level. true = Element Content Level. | false | Boolean |
| **camel.dataformat.xml-security.xml-cipher-algorithm** | The cipher algorithm to be used for encryption/decryption of the XML message content. The available choices are: XMLCipher.TRIPLEDES XMLCipher.AES\_128 XMLCipher.AES\_128\_GCM XMLCipher.AES\_192 XMLCipher.AES\_192\_GCM XMLCipher.AES\_256 XMLCipher.AES\_256\_GCM XMLCipher.SEED\_128 XMLCipher.CAMELLIA\_128 XMLCipher.CAMELLIA\_192 XMLCipher.CAMELLIA\_256 The default value is XMLCipher.AES\_256\_GCM. | AES-256-GCM | String |