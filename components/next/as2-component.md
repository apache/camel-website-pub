# AS2

**Since Camel 2.22**

**Both producer and consumer are supported**

The AS2 component provides transport of EDI messages using the HTTP transfer protocol as specified in [RFC4130](https://tools.ietf.org/html/rfc4130).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-as2</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

as2://apiName/methodName

apiName can be one of:

-   client
    
-   server
    

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

The AS2 component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | Component configuration. |  | AS2Configuration |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The AS2 endpoint is configured using URI syntax:

as2:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   CLIENT
    
-   SERVER
    
-   RECEIPT
    





 |  | AS2ApiName |
| **methodName** (common) | **Required** What sub operation to use for the selected operation. |  | String |

### Query Parameters (48 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **as2From** (common) | The value of the AS2From header of AS2 message. |  | String |
| **as2MessageStructure** (common) | 
The structure of AS2 Message. One of: PLAIN - No encryption, no signature, SIGNED - No encryption, signature, ENCRYPTED - Encryption, no signature, ENCRYPTED\_SIGNED - Encryption, signature.

Enum values:

-   PLAIN
    
-   SIGNED
    
-   ENCRYPTED
    
-   SIGNED\_ENCRYPTED
    
-   PLAIN\_COMPRESSED
    
-   COMPRESSED\_SIGNED
    
-   SIGNED\_COMPRESSED
    
-   ENCRYPTED\_COMPRESSED
    
-   ENCRYPTED\_COMPRESSED\_SIGNED
    
-   ENCRYPTED\_SIGNED\_COMPRESSED
    





 |  | AS2MessageStructure |
| **as2To** (common) | The value of the AS2To header of AS2 message. |  | String |
| **as2Version** (common) | 

The version of the AS2 protocol.

Enum values:

-   1.0
    
-   1.1
    





 | 1.1 | String |
| **asyncMdnPortNumber** (common) | The port number of asynchronous MDN server. |  | Integer |
| **attachedFileName** (common) | The name of the attached file. |  | String |
| **clientFqdn** (common) | The Client Fully Qualified Domain Name (FQDN). Used in message ids sent by endpoint. | camel.apache.org | String |
| **compressionAlgorithm** (common) | 

The algorithm used to compress EDI message.

Enum values:

-   ZLIB
    





 |  | AS2CompressionAlgorithm |
| **dispositionNotificationTo** (common) | The value of the Disposition-Notification-To header. Assigning a value to this parameter requests a message disposition notification (MDN) for the AS2 message. |  | String |
| **ediMessageCharset** (common) | The charset of the content type of EDI message. | us-ascii | String |
| **ediMessageTransferEncoding** (common) | The transfer encoding of EDI message. |  | String |
| **ediMessageType** (common) | 

The content type of EDI message. One of application/edifact, application/edi-x12, application/edi-consent, application/xml.

Enum values:

-   application/edifact
    
-   application/edi-x12
    
-   application/edi-consent
    
-   application/xml
    





 |  | String |
| **from** (common) | The value of the From header of AS2 message. |  | String |
| **httpConnectionPoolSize** (common) | The maximum size of the connection pool for http connections (client only). | 5 | Integer |
| **httpConnectionPoolTtl** (common) | The time to live for connections in the connection pool (client only). | 15m | Duration |
| **httpConnectionTimeout** (common) | The timeout of the http connection (client only). | 5s | Duration |
| **httpSocketTimeout** (common) | The timeout of the underlying http socket (client only). | 5s | Duration |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **mdnMessageTemplate** (common) | The template used to format MDN message. |  | String |
| **receiptDeliveryOption** (common) | The return URL that the message receiver should send an asynchronous MDN to. If not present the receipt is synchronous. (Client only). |  | String |
| **requestUri** (common) | The request URI of EDI message. | / | String |
| **server** (common) | The value included in the Server message header identifying the AS2 Server. | Camel AS2 Server Endpoint | String |
| **serverFqdn** (common) | The Server Fully Qualified Domain Name (FQDN). Used in message ids sent by endpoint. | camel.apache.org | String |
| **serverPortNumber** (common) | The port number of server. |  | Integer |
| **subject** (common) | The value of Subject header of AS2 message. |  | String |
| **targetHostname** (common) | The host name (IP or DNS name) of target host. |  | String |
| **targetPortNumber** (common) | The port number of target host. -1 indicates the scheme default port. | 80 | Integer |
| **userAgent** (common) | The value included in the User-Agent message header identifying the AS2 user agent. | Camel AS2 Client Endpoint | String |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **expectContinue** (producer) | Controls whether the Expect: 100-Continue header is included in outbound AS2 messages. When enabled, the client sends the headers first and waits for a 100 Continue response from the server before sending the message body. This can improve efficiency with compatible partners but may cause 3-second delays with servers that don’t support the protocol. Default is false for backward compatibility. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessToken** (security) | The access token that is used by the client for bearer authentication. |  | String |
| **decryptingPrivateKey** (security) | The key used to encrypt the EDI message. |  | PrivateKey |
| **encryptingAlgorithm** (security) | 

The algorithm used to encrypt EDI message.

Enum values:

-   AES128\_CBC
    
-   AES192\_CBC
    
-   AES256\_CBC
    
-   AES128\_CCM
    
-   AES192\_CCM
    
-   AES256\_CCM
    
-   AES128\_GCM
    
-   AES192\_GCM
    
-   AES256\_GCM
    
-   CAMELLIA128\_CBC
    
-   CAMELLIA192\_CBC
    
-   CAMELLIA256\_CBC
    
-   CAST5\_CBC
    
-   DES\_CBC
    
-   DES\_EDE3\_CBC
    
-   GOST28147\_GCFB
    
-   IDEA\_CBC
    
-   RC2\_CBC
    
-   RC4
    
-   SEED\_CBC
    





 |  | AS2EncryptionAlgorithm |
| **encryptingCertificateChain** (security) | The chain of certificates used to encrypt EDI message. |  | Certificate\[\] |
| **hostnameVerifier** (security) | Set hostname verifier for SSL session. |  | HostnameVerifier |
| **mdnAccessToken** (security) | The access token that is used by the server when it sends an async MDN. |  | String |
| **mdnPassword** (security) | The password that is used by the server for basic authentication when it sends an async MDN. |  | String |
| **mdnUserName** (security) | The user-name that is used by the server for basic authentication when it sends an async MDN. If options for basic authentication and bearer authentication are both set then basic authentication takes precedence. |  | String |
| **password** (security) | The password that is used by the client for basic authentication. |  | String |
| **signedReceiptMicAlgorithms** (security) | The list of algorithms, in order of preference, requested to generate a message integrity check (MIC) returned in message disposition notification (MDN). Multiple algorithms can be separated by comma. |  | String |
| **signingAlgorithm** (security) | 

The algorithm used to sign EDI message.

Enum values:

-   SHA3\_224WITHRSA
    
-   SHA3\_256WITHRSA
    
-   SHA3\_384withRSA
    
-   SHA3\_512WITHRSA
    
-   MD5WITHRSA
    
-   SHA1WITHRSA
    
-   MD2WITHRSA
    
-   SHA224WITHRSA
    
-   SHA256WITHRSA
    
-   SHA384WITHRSA
    
-   SHA512WITHRSA
    
-   RIPEMD128WITHRSA
    
-   RIPEMD160WITHRSA
    
-   RIPEMD256WITHRSA
    
-   SHA224WITHDSA
    
-   SHA256WITHDSA
    
-   SHA384WITHDSA
    
-   SHA512WITHDSA
    
-   SHA3\_224WITHDSA
    
-   SHA3\_256WITHDSA
    
-   SHA3\_384WITHDSA
    
-   SHA3\_512WITHDSA
    
-   SHA1WITHDSA
    
-   SHA3\_224WITHECDSA
    
-   SHA3\_256WITHECDSA
    
-   SHA3\_384WITHECDSA
    
-   SHA3\_512WITHECDSA
    
-   SHA1WITHECDSA
    
-   SHA224WITHECDSA
    
-   SHA256WITHECDSA
    
-   SHA384WITHECDSA
    
-   SHA512WITHECDSA
    
-   SHA1WITHPLAIN\_ECDSA
    
-   SHA224WITHPLAIN\_ECDSA
    
-   SHA256WITHPLAIN\_ECDSA
    
-   SHA384WITHPLAIN\_ECDSA
    
-   SHA512WITHPLAIN\_ECDSA
    
-   RIPEMD160WITHPLAIN\_ECDSA
    
-   SHA1WITHRSAANDMGF1
    
-   SHA224WITHRSAANDMGF1
    
-   SHA256WITHRSAANDMGF1
    
-   SHA384WITHRSAANDMGF1
    
-   SHA512WITHRSAANDMGF1
    
-   SHA3\_224WITHRSAANDMGF1
    
-   SHA3\_256WITHRSAANDMGF1
    
-   SHA3\_384WITHRSAANDMGF1
    
-   SHA3\_512WITHRSAANDMGF1
    





 |  | AS2SignatureAlgorithm |
| **signingCertificateChain** (security) | The chain of certificates used to sign EDI message. |  | Certificate\[\] |
| **signingPrivateKey** (security) | The key used to sign the EDI message. |  | PrivateKey |
| **sslContext** (security) | Set SSL context for connection to remote server. |  | SSLContext |
| **userName** (security) | The user-name that is used by the client for basic authentication. If options for basic authentication and bearer authentication are both set then basic authentication takes precedence. |  | String |
| **validateSigningCertificateChain** (security) | Certificates to validate the message’s signature against. If not supplied, validation will not take place. Server: validates the received message. Client: not yet implemented, should validate the MDN. |  | Certificate\[\] |

## API Parameters (3 APIs)

The AS2 endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

as2:apiName/methodName

There are 3 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**client**](#_api_client) | Producer | Sends EDI Messages over HTTP |
| [**receipt**](#_api_receipt) | Consumer | Receives the asynchronous AS2-MDN that is requested by the sender of an AS2 message |
| [**server**](#_api_server) | Consumer | Receives EDI Messages over HTTP |

Each API is documented in the following sections to come.

### API: client

**Only producer is supported**

The client API is defined in the syntax as follows:

```none
as2:client/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**send**](#_api_client_method_send) |  | Send ediMessage to trading partner |

#### Method send

Signatures:

-   org.apache.hc.core5.http.protocol.HttpCoreContext send(Object ediMessage, String requestUri, String subject, String from, String as2From, String as2To, org.apache.camel.component.as2.api.AS2MessageStructure as2MessageStructure, String ediMessageContentType, String ediMessageCharset, String ediMessageTransferEncoding, org.apache.camel.component.as2.api.AS2SignatureAlgorithm signingAlgorithm, java.security.cert.Certificate\[\] signingCertificateChain, java.security.PrivateKey signingPrivateKey, org.apache.camel.component.as2.api.AS2CompressionAlgorithm compressionAlgorithm, String dispositionNotificationTo, String signedReceiptMicAlgorithms, org.apache.camel.component.as2.api.AS2EncryptionAlgorithm encryptingAlgorithm, java.security.cert.Certificate\[\] encryptingCertificateChain, String attachedFileName, String receiptDeliveryOption, String userName, String password, String accessToken);
    

The as2/send API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **accessToken** | The access token that is used by the client for bearer authentication | String |
| **as2From** | AS2 name of sender | String |
| **as2MessageStructure** | The structure of AS2 to send; see AS2MessageStructure | AS2MessageStructure |
| **as2To** | AS2 name of recipient | String |
| **attachedFileName** | The name of the attached file or null if user doesn’t want to specify it | String |
| **compressionAlgorithm** | The algorithm used to compress the message or null if sending EDI message uncompressed | AS2CompressionAlgorithm |
| **dispositionNotificationTo** | An RFC2822 address to request a receipt or null if no receipt requested | String |
| **ediMessage** | EDI message to transport | Object |
| **ediMessageCharset** | The charset of the EDI message | String |
| **ediMessageContentType** | The content type of EDI message | String |
| **ediMessageTransferEncoding** | The transfer encoding used to transport EDI message | String |
| **encryptingAlgorithm** | The algorithm used to encrypt the message or null if sending EDI message unencrypted | AS2EncryptionAlgorithm |
| **encryptingCertificateChain** | The chain of certificates used to encrypt the message or null if sending EDI message unencrypted | Certificate\[\] |
| **from** | RFC2822 address of sender | String |
| **password** | The password that is used by the client for basic authentication | String |
| **receiptDeliveryOption** | The return URL that the message receiver should send an asynchronous MDN to | String |
| **requestUri** | Resource location to deliver message | String |
| **signedReceiptMicAlgorithms** | The senders list of signing algorithms for signing receipt, in preferred order, or null if requesting an unsigned receipt. | String |
| **signingAlgorithm** | The algorithm used to sign the message or null if sending EDI message unsigned | AS2SignatureAlgorithm |
| **signingCertificateChain** | The chain of certificates used to sign the message or null if sending EDI message unsigned | Certificate\[\] |
| **signingPrivateKey** | The private key used to sign EDI message | PrivateKey |
| **subject** | Message subject | String |
| **userName** | The user-name that is used for basic authentication | String |

In addition to the parameters above, the as2 API can also use any of the [Query Parameters (48 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelAs2.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelAs2.myParameterNameHere` header.

### API: receipt

**Only consumer is supported**

The receipt API is defined in the syntax as follows:

```none
as2:receipt/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**receive**](#_api_receipt_method_receive) |  | 
 |

#### Method receive

Signatures:

-   void receive(String requestUriPattern, org.apache.hc.core5.http.io.HttpRequestHandler handler);
    

The as2/receive API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **requestUriPattern** | 
 | String |

In addition to the parameters above, the as2 API can also use any of the [Query Parameters (48 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelAs2.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelAs2.myParameterNameHere` header.

### API: server

**Only consumer is supported**

The server API is defined in the syntax as follows:

```none
as2:server/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**listen**](#_api_server_method_listen) |  | 
 |

#### Method listen

Signatures:

-   void listen(String requestUriPattern, org.apache.hc.core5.http.io.HttpRequestHandler handler);
    

The as2/listen API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **requestUriPattern** | 
 | String |

In addition to the parameters above, the as2 API can also use any of the [Query Parameters (48 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelAs2.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelAs2.myParameterNameHere` header.

## Spring Boot Auto-Configuration

When using as2 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-as2-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.as2.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.as2.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.as2.configuration** | Component configuration. The option is a org.apache.camel.component.as2.AS2Configuration type. |  | AS2Configuration |
| **camel.component.as2.enabled** | Whether to enable auto configuration of the as2 component. This is enabled by default. |  | Boolean |
| **camel.component.as2.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.as2.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.as2.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |