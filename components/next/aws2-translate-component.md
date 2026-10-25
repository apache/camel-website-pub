# AWS Translate

**Since Camel 3.1**

**Only producer is supported**

The AWS2 Translate component supports translate a text in multiple languages. [AWS Translate](https://aws.amazon.com/translate/) clusters instances.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Translate. More information is available at [Amazon Translate](https://aws.amazon.com/translate/).

## URI Format

aws2-translate://label\[?options\]

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

The AWS Translate component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autodetectSourceLanguage** (producer) | Being able to autodetect the source language. When enabled, the source language is auto, and the sourceLanguage option and the CamelAwsTranslateSourceLanguage header are not used. | false | boolean |
| **configuration** (producer) | Component configuration. |  | Translate2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   translateText
    





 | translateText | Translate2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Translate client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   eu-isoe-west-1
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   ca-west-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 |  | String |
| **sourceLanguage** (producer) | Source language to use. When not set, the CamelAwsTranslateSourceLanguage header is used. It is not used when autodetectSourceLanguage is enabled. |  | String |
| **targetLanguage** (producer) | Target language to use. When not set, the CamelAwsTranslateTargetLanguage header is used. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **translateClient** (advanced) | **Autowired** To use an existing configured AWS Translate client. |  | TranslateClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Translate client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Translate client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Translate client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Translate client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Translate client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Translate client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Translate. | false | boolean |

## Endpoint Options

The AWS Translate endpoint is configured using URI syntax:

aws2-translate:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autodetectSourceLanguage** (producer) | Being able to autodetect the source language. When enabled, the source language is auto, and the sourceLanguage option and the CamelAwsTranslateSourceLanguage header are not used. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   translateText
    





 | translateText | Translate2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Translate client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   eu-isoe-west-1
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   ca-west-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 |  | String |
| **sourceLanguage** (producer) | Source language to use. When not set, the CamelAwsTranslateSourceLanguage header is used. It is not used when autodetectSourceLanguage is enabled. |  | String |
| **targetLanguage** (producer) | Target language to use. When not set, the CamelAwsTranslateTargetLanguage header is used. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **translateClient** (advanced) | **Autowired** To use an existing configured AWS Translate client. |  | TranslateClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Translate client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Translate client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Translate client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Translate client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Translate client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Translate client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Translate. | false | boolean |

## Message Headers

The AWS Translate component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsTranslateSourceLanguage** (producer) Constant: [`SOURCE_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-translate/latest/org/apache/camel/component/aws2/translate/Translate2Constants.html#SOURCE_LANGUAGE) | The text source language. |  | String |
| **CamelAwsTranslateTargetLanguage** (producer) Constant: [`TARGET_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-translate/latest/org/apache/camel/component/aws2/translate/Translate2Constants.html#TARGET_LANGUAGE) | The text target language. |  | String |
| **CamelAwsTranslateTerminologyNames** (producer) Constant: [`TERMINOLOGY_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-translate/latest/org/apache/camel/component/aws2/translate/Translate2Constants.html#TERMINOLOGY_NAMES) | The terminologies to use. |  | Collection |
| **CamelAwsTranslateOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-translate/latest/org/apache/camel/component/aws2/translate/Translate2Constants.html#OPERATION) | The operation we want to perform. |  | String |

## Message Body

The message body at each side of the AWS Translate component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `text`, `bytes`, `stream` or `file` | The text to translate: bytes, a stream or a file are read as text, a Map or a POJO is translated as its toString(), so take the text out of it first, and no body fails. With pojoRequest=true the body is a TranslateTextRequest of the AWS SDK: another body fails. |
| **Producer output** | `text` (`java.lang.String`) | The translated text. The source language that AWS detects with autodetectSourceLanguage=true is not kept. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

Required Translate component options

You have to provide the translateClient in the Registry or your accessKey and secretKey to access the [Amazon Translate](https://aws.amazon.com/translate/) service.

## Usage

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Translate Producer operations

Camel-AWS Translate component provides the following operation on the producer side:

-   translateText
    

### Source and target language

Each language is taken from its option, or else from its header:

-   the source language from the `sourceLanguage` option, or else the `CamelAwsTranslateSourceLanguage` header;
    
-   the target language from the `targetLanguage` option, or else the `CamelAwsTranslateTargetLanguage` header.
    

So one language can be set as an option and the other as a header. With `autodetectSourceLanguage=true`, the source language is `auto`, and Amazon Translate detects it.

When the target language is missing, or the source language is missing and `autodetectSourceLanguage` is not enabled, the producer fails with an `IllegalArgumentException` that names the option and the header to set.

## Examples

### Translate Text example

-   Java
    
-   YAML
    

```java
from("direct:start")
  .setHeader(Translate2Constants.SOURCE_LANGUAGE, constant(Translate2LanguageEnum.ITALIAN))
  .setHeader(Translate2Constants.TARGET_LANGUAGE, constant(Translate2LanguageEnum.GERMAN))
  .setBody(constant("Ciao"))
  .to("aws2-translate://test?translateClient=#amazonTranslateClient&operation=translateText");
```

In YAML, the headers are the language codes, `it` and `de`:

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAwsTranslateSourceLanguage
            expression:
              constant:
                expression: it
        - setHeader:
            name: CamelAwsTranslateTargetLanguage
            expression:
              constant:
                expression: de
        - setBody:
            expression:
              constant:
                expression: Ciao
        - to:
            uri: aws2-translate:test
            parameters:
              translateClient: "#amazonTranslateClient"
              operation: translateText
```

As a result, you’ll get an exchange containing the translated text.

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as the body. In AWS Translate, the only operation available is TranslateText, so you can do something like:

_Java-only: uses AWS SDK POJO request builder as message body_

```java
from("direct:start")
  .setBody(constant(TranslateTextRequest.builder().sourceLanguageCode(Translate2LanguageEnum.ITALIAN.toString())
                    .targetLanguageCode(Translate2LanguageEnum.GERMAN.toString()).text("Ciao").build()))
  .to("aws2-translate://test?translateClient=#amazonTranslateClient&operation=translateText&pojoRequest=true");
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-translate</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.