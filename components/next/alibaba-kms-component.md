# Alibaba Key Management Service (KMS)

**Since Camel 4.23**

**Only producer is supported**

The Alibaba Cloud KMS component allows you to encrypt, decrypt and generate data keys using Alibaba Cloud KMS.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-alibaba-kms</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

```none
alibaba-kms:operation[?options]
```

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

The Alibaba Key Management Service (KMS) component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Alibaba Key Management Service (KMS) endpoint is configured using URI syntax:

alibaba-kms:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation that the producer performs. The CamelAlibabaKmsOperation header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option.

Enum values:

-   encrypt
    
-   decrypt
    
-   generateDataKey
    





 |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpoint** (producer) | The endpoint of KMS, which is a host name without http:// or https://. The producer sends requests to it over HTTPS. If not set, the region option determines the endpoint, and one of the two is required. Not used when the kmsClient option is set or autowired. |  | String |
| **keyId** (producer) | The ID, alias or ARN of the KMS key for encrypt and generateDataKey. The CamelAlibabaKmsKeyId header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. One of the three is required for encrypt and generateDataKey. |  | String |
| **keySpec** (producer) | The key spec of the data key for generateDataKey. The value must be AES\_256 or AES\_128. KMS does not use it when the number of bytes is set as well. The CamelAlibabaKmsKeySpec header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no key spec to the request. |  | String |
| **numberOfBytes** (producer) | The number of bytes of the data key for generateDataKey. The value must be from 1 to 1024. The CamelAlibabaKmsNumberOfBytes header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer adds no number of bytes to the request. |  | Integer |
| **region** (producer) | The region ID of KMS, for example cn-hangzhou. Only used when the endpoint option is not set, to build the endpoint of KMS. One of the two is required, unless the kmsClient option is set or autowired, which uses neither. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **kmsClient** (advanced) | **Autowired** To use a custom com.aliyun.kms20160120.Client. The producer sends its requests with this client, and the region, endpoint, accessKey, secretKey and serviceKeys options are not used. If no client is set or autowired, the Camel endpoint creates a client from these options. It creates this client when the producer processes its first message. |  | Client |
| **accessKey** (security) | The AccessKey ID of the AccessKey pair for the requests that the producer sends to KMS. If not set, the accessKey of the serviceKeys option is used, and one of the two is required. Not used when the kmsClient option is set or autowired. |  | String |
| **ciphertextBlob** (security) | The ciphertext blob for decrypt, for example from the response to encrypt or generateDataKey. The CamelAlibabaKmsCiphertextBlob header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer takes the ciphertext blob from the message body as text. |  | String |
| **plaintext** (security) | The plaintext for encrypt. The producer encodes it in UTF-8 and sends it to KMS in Base64. The CamelAlibabaKmsPlaintext header replaces this option for a request that the producer sends. If that header is not set, an exchange property of the same name replaces this option. If none of the three is set, the producer takes the plaintext from the message body. |  | String |
| **secretKey** (security) | The AccessKey secret of the AccessKey pair for the requests that the producer sends to KMS. If not set, the secretKey of the serviceKeys option is used, and one of the two is required. Not used when the kmsClient option is set or autowired. |  | String |
| **serviceKeys** (security) | The AccessKey pair as an org.apache.camel.component.alibaba.common.models.ServiceKeys. Its accessKey is the AccessKey ID and its secretKey is the AccessKey secret. Each of the two is used when the option of the same name is not set. Not used when the kmsClient option is set or autowired. |  | ServiceKeys |

## Message Headers

The Alibaba Key Management Service (KMS) component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAlibabaKmsOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-kms/latest/org/apache/camel/component/alibaba/kms/constants/KMSHeaders.html#OPERATION) | The operation that the producer performs, which replaces the operation of the endpoint. If this header is not set, an exchange property of the same name replaces it. |  | String |
| **CamelAlibabaKmsKeyId** (producer) Constant: [`KEY_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-kms/latest/org/apache/camel/component/alibaba/kms/constants/KMSHeaders.html#KEY_ID) | The ID, alias or ARN of the KMS key for encrypt and generateDataKey. This header replaces the keyId option. If this header is not set, an exchange property of the same name replaces the keyId option. |  | String |
| **CamelAlibabaKmsPlaintext** (producer) Constant: [`PLAINTEXT`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-kms/latest/org/apache/camel/component/alibaba/kms/constants/KMSHeaders.html#PLAINTEXT) | The plaintext for encrypt. The producer encodes it in UTF-8 and sends it to KMS in Base64. This header replaces the plaintext option. If this header is not set, an exchange property of the same name replaces the plaintext option. A Map or a POJO fails, as it does in the message body, since Camel reads it only as its toString(). |  | String |
| **CamelAlibabaKmsCiphertextBlob** (producer) Constant: [`CIPHERTEXT_BLOB`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-kms/latest/org/apache/camel/component/alibaba/kms/constants/KMSHeaders.html#CIPHERTEXT_BLOB) | The ciphertext blob for decrypt, for example from the response to encrypt or generateDataKey. This header replaces the ciphertextBlob option. If this header is not set, an exchange property of the same name replaces the ciphertextBlob option. |  | String |
| **CamelAlibabaKmsKeySpec** (producer) Constant: [`KEY_SPEC`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-kms/latest/org/apache/camel/component/alibaba/kms/constants/KMSHeaders.html#KEY_SPEC) | The key spec of the data key for generateDataKey. The value must be AES\_256 or AES\_128. KMS does not use it when the number of bytes is set as well. This header replaces the keySpec option. If this header is not set, an exchange property of the same name replaces the keySpec option. |  | String |
| **CamelAlibabaKmsNumberOfBytes** (producer) Constant: [`NUMBER_OF_BYTES`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-kms/latest/org/apache/camel/component/alibaba/kms/constants/KMSHeaders.html#NUMBER_OF_BYTES) | The number of bytes of the data key for generateDataKey. The value must be from 1 to 1024. This header replaces the numberOfBytes option. If this header is not set, an exchange property of the same name replaces the numberOfBytes option. Only generateDataKey reads it, and a value that is not a number fails that operation alone. |  | Integer |
| **CamelAlibabaKmsRequestId** (producer) Constant: [`REQUEST_ID`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-kms/latest/org/apache/camel/component/alibaba/kms/constants/KMSHeaders.html#REQUEST_ID) | The request ID that KMS returns in the response to the operation. The producer sets it, unless the exchange fails. |  | String |

## Message Body

The message body at each side of the Alibaba Key Management Service (KMS) component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | 
encrypt encrypts the body unless the plaintext option or header is set: text in UTF-8, bytes as they are, and a stream or a file as its bytes, so binary data is kept. A Map or a POJO fails, as it does not convert to bytes, so marshal it first. decrypt takes the ciphertext blob as text, unless the ciphertextBlob option or header is set. No body fails both; generateDataKey does not use the body.

-   With `operation=encrypt`: `text`, `bytes`, `stream` or `file`
    
-   With `operation=decrypt`: `text`
    





 |
| **Producer output** | `map` (`java.util.Map`) | A Map with the statusCode and the fields of the response: the ciphertextBlob and keyId of encrypt, the plaintext of decrypt, which is Base64 when this component encrypted it, and the plaintext and ciphertextBlob of generateDataKey. The request id is in the CamelAlibabaKmsRequestId header too. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

### Operations

The component supports the following operations:

-   `encrypt` - encrypt plaintext using a KMS key (producer)
    
-   `decrypt` - decrypt a ciphertext blob (producer)
    
-   `generateDataKey` - generate a data key (producer)
    

### Plaintext of encrypt

`encrypt` encrypts the `plaintext` option or the `CamelAlibabaKmsPlaintext` header when one is set, else the message body. A `String` is encrypted in UTF-8, and a `byte[]`, an `InputStream` or a file as its bytes, so binary data is kept. The component sends these bytes to KMS in Base64, so the `plaintext` that `decrypt` returns for them is Base64: decode it to get the original bytes back. A `Map` or a POJO fails instead of being encrypted as its `toString()`: in the body with an `InvalidPayloadException`, and in the header or in the exchange property of the same name with an `IllegalArgumentException`. Marshal such a value first, for example with `marshal().json()`. A value whose text is its `toString()`, such as a `UUID`, a `URI` or a `java.time` value, is encrypted as that text. A message without a body fails with an `IllegalArgumentException`.

### Producer example

-   Java
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("secret-value"))
    .to("alibaba-kms:encrypt?keyId=alias/my-key&region=cn-hangzhou&accessKey=RAW(accessKey)&secretKey=RAW(secretKey)");
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            expression:
              constant:
                expression: secret-value
        - to:
            uri: alibaba-kms:encrypt
            parameters:
              keyId: alias/my-key
              region: cn-hangzhou
              accessKey: "{{alibaba.access-key}}"
              secretKey: "{{alibaba.secret-key}}"
```

## Examples

For more examples, see the unit tests in the `camel-alibaba-kms` module.