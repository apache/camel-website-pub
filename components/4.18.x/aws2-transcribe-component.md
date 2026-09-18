# AWS Transcribe

**Since Camel 4.15**

**Only producer is supported**

The AWS2 Transcribe component supports Automatically convert speech to text [AWS Transcribe](https://aws.amazon.com/transcribe/)

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Transcribe. More information is available at [Amazon Transcribe](https://aws.amazon.com/transcribe/).

## URI Format

aws2-transcribe://label\[?options\]

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

The AWS Transcribe component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | Transcribe2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   startTranscriptionJob
    
-   getTranscriptionJob
    
-   listTranscriptionJobs
    
-   deleteTranscriptionJob
    
-   createVocabulary
    
-   getVocabulary
    
-   listVocabularies
    
-   updateVocabulary
    
-   deleteVocabulary
    
-   createVocabularyFilter
    
-   getVocabularyFilter
    
-   listVocabularyFilters
    
-   updateVocabularyFilter
    
-   deleteVocabularyFilter
    
-   createLanguageModel
    
-   describeLanguageModel
    
-   listLanguageModels
    
-   deleteLanguageModel
    
-   createMedicalVocabulary
    
-   getMedicalVocabulary
    
-   listMedicalVocabularies
    
-   updateMedicalVocabulary
    
-   deleteMedicalVocabulary
    
-   startMedicalTranscriptionJob
    
-   getMedicalTranscriptionJob
    
-   listMedicalTranscriptionJobs
    
-   deleteMedicalTranscriptionJob
    
-   tagResource
    
-   untagResource
    
-   listTagsForResource
    





 |  | Transcribe2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **protocol** (producer) | 

To define a proxy protocol when instantiating the Transcribe client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **proxyHost** (producer) | To define a proxy host when instantiating the Transcribe client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Transcribe client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Transcribe client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which Transcribe client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **transcribeClient** (producer) | To use a existing configured AWS Transcribe as client. |  | TranscribeClient |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | true | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Transcribe client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Transcribe client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (producer) | Set whether the Transcribe client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume a IAM role for doing the operations. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **proxyPassword** (security) | To define a proxy password when instantiating the Transcribe client. |  | String |
| **proxyUsername** (security) | To define a proxy username when instantiating the Transcribe client. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |

## Endpoint Options

The AWS Transcribe endpoint is configured using URI syntax:

aws2-transcribe:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (21 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   startTranscriptionJob
    
-   getTranscriptionJob
    
-   listTranscriptionJobs
    
-   deleteTranscriptionJob
    
-   createVocabulary
    
-   getVocabulary
    
-   listVocabularies
    
-   updateVocabulary
    
-   deleteVocabulary
    
-   createVocabularyFilter
    
-   getVocabularyFilter
    
-   listVocabularyFilters
    
-   updateVocabularyFilter
    
-   deleteVocabularyFilter
    
-   createLanguageModel
    
-   describeLanguageModel
    
-   listLanguageModels
    
-   deleteLanguageModel
    
-   createMedicalVocabulary
    
-   getMedicalVocabulary
    
-   listMedicalVocabularies
    
-   updateMedicalVocabulary
    
-   deleteMedicalVocabulary
    
-   startMedicalTranscriptionJob
    
-   getMedicalTranscriptionJob
    
-   listMedicalTranscriptionJobs
    
-   deleteMedicalTranscriptionJob
    
-   tagResource
    
-   untagResource
    
-   listTagsForResource
    





 |  | Transcribe2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **protocol** (producer) | 

To define a proxy protocol when instantiating the Transcribe client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **proxyHost** (producer) | To define a proxy host when instantiating the Transcribe client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Transcribe client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Transcribe client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which Transcribe client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **transcribeClient** (producer) | To use a existing configured AWS Transcribe as client. |  | TranscribeClient |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | true | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Transcribe client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Transcribe client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (producer) | Set whether the Transcribe client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume a IAM role for doing the operations. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **proxyPassword** (security) | To define a proxy password when instantiating the Transcribe client. |  | String |
| **proxyUsername** (security) | To define a proxy username when instantiating the Transcribe client. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |

## Message Headers

The AWS Transcribe component supports 14 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsTranscribeTranscriptionJobName** (producer) Constant: [`TRANSCRIPTION_JOB_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#TRANSCRIPTION_JOB_NAME) | The name of the transcription job. |  | String |
| **CamelAwsTranscribeLanguageCode** (producer) Constant: [`LANGUAGE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#LANGUAGE_CODE) | The language code for the transcription job. |  | String |
| **CamelAwsTranscribeMediaFormat** (producer) Constant: [`MEDIA_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#MEDIA_FORMAT) | The format of the input media file. |  | String |
| **CamelAwsTranscribeMediaUri** (producer) Constant: [`MEDIA_URI`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#MEDIA_URI) | The URI of the media file to transcribe. |  | String |
| **CamelAwsTranscribeJobNameContains** (producer) Constant: [`JOB_NAME_CONTAINS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#JOB_NAME_CONTAINS) | Filter transcription jobs by name containing this string. |  | String |
| **CamelAwsTranscribeStatus** (producer) Constant: [`STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#STATUS) | The status of the transcription job. |  | String |
| **CamelAwsTranscribeVocabularyName** (producer) Constant: [`VOCABULARY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#VOCABULARY_NAME) | The name of the custom vocabulary to use. |  | String |
| **CamelAwsTranscribeVocabularyFilterName** (producer) Constant: [`VOCABULARY_FILTER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#VOCABULARY_FILTER_NAME) | The name of the vocabulary filter to use. |  | String |
| **CamelAwsTranscribeVocabularyPhrases** (producer) Constant: [`VOCABULARY_PHRASES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#VOCABULARY_PHRASES) | List of phrases for custom vocabulary. |  | List |
| **CamelAwsTranscribeLanguageModelName** (producer) Constant: [`LANGUAGE_MODEL_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#LANGUAGE_MODEL_NAME) | The name of the custom language model to use. |  | String |
| **CamelAwsTranscribeMedicalTranscriptionJobName** (producer) Constant: [`MEDICAL_TRANSCRIPTION_JOB_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#MEDICAL_TRANSCRIPTION_JOB_NAME) | The name of the medical transcription job. |  | String |
| **CamelAwsTranscribeResourceArn** (producer) Constant: [`RESOURCE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#RESOURCE_ARN) | The Amazon Resource Name (ARN) of the resource. |  | String |
| **CamelAwsTranscribeTags** (producer) Constant: [`TAGS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#TAGS) | A map of tags to assign to the resource. |  | Map |
| **CamelAwsTranscribeTagKeys** (producer) Constant: [`TAG_KEYS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#TAG_KEYS) | A list of tag keys to remove from the resource. |  | List |

Required Transcribe component options

You have to provide the amazonTranscribeClient in the Registry or your accessKey and secretKey to access the [Amazon Transcribe](https://aws.amazon.com/transcribe/) service.

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

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-transcribe</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-transcribe with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-transcribe-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 24 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-transcribe.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-transcribe.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-transcribe.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.transcribe.Transcribe2Configuration type. |  | Transcribe2Configuration |
| **camel.component.aws2-transcribe.enabled** | Whether to enable auto configuration of the aws2-transcribe component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-transcribe.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-transcribe.operation** | The operation to perform. |  | Transcribe2Operations |
| **camel.component.aws2-transcribe.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-transcribe.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-transcribe.profile-credentials-name** | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **camel.component.aws2-transcribe.protocol** | To define a proxy protocol when instantiating the Transcribe client. | https | Protocol |
| **camel.component.aws2-transcribe.proxy-host** | To define a proxy host when instantiating the Transcribe client. |  | String |
| **camel.component.aws2-transcribe.proxy-password** | To define a proxy password when instantiating the Transcribe client. |  | String |
| **camel.component.aws2-transcribe.proxy-port** | To define a proxy port when instantiating the Transcribe client. |  | Integer |
| **camel.component.aws2-transcribe.proxy-protocol** | To define a proxy protocol when instantiating the Transcribe client. | https | Protocol |
| **camel.component.aws2-transcribe.proxy-username** | To define a proxy username when instantiating the Transcribe client. |  | String |
| **camel.component.aws2-transcribe.region** | The region in which Transcribe client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-transcribe.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-transcribe.session-token** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **camel.component.aws2-transcribe.transcribe-client** | To use a existing configured AWS Transcribe as client. The option is a software.amazon.awssdk.services.transcribe.TranscribeClient type. |  | TranscribeClient |
| **camel.component.aws2-transcribe.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | true | Boolean |
| **camel.component.aws2-transcribe.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-transcribe.use-default-credentials-provider** | Set whether the Transcribe client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-transcribe.use-profile-credentials-provider** | Set whether the Transcribe client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-transcribe.use-session-credentials** | Set whether the Transcribe client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume a IAM role for doing the operations. | false | Boolean |