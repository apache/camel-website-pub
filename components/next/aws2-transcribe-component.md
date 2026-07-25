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

The AWS Transcribe component supports the following options which are listed below.

   
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

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters

   
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

The AWS Transcribe component supports the following message header(s), which is/are listed below:

   
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
| **CamelAwsTranscribeMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#MAX_RESULTS) | The maximum number of results to return in a list operation. |  | Integer |
| **CamelAwsTranscribeNextToken** (producer) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#NEXT_TOKEN) | The token to retrieve the next page of a list operation. |  | String |
| **CamelAwsTranscribeVocabularyFileUri** (producer) Constant: [`VOCABULARY_FILE_URI`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#VOCABULARY_FILE_URI) | The S3 location of the vocabulary or vocabulary filter file. |  | String |
| **CamelAwsTranscribeBaseModelName** (producer) Constant: [`BASE_MODEL_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#BASE_MODEL_NAME) | The base model used when creating a custom language model. |  | String |
| **CamelAwsTranscribeInputDataS3Uri** (producer) Constant: [`INPUT_DATA_S3_URI`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#INPUT_DATA_S3_URI) | The S3 location of the training data for a custom language model. |  | String |
| **CamelAwsTranscribeDataAccessRoleArn** (producer) Constant: [`DATA_ACCESS_ROLE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#DATA_ACCESS_ROLE_ARN) | The ARN of the IAM role granting access to the training data or vocabulary file. |  | String |
| **CamelAwsTranscribeOutputBucketName** (producer) Constant: [`OUTPUT_BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#OUTPUT_BUCKET_NAME) | The S3 bucket where the transcription output is stored. |  | String |
| **CamelAwsTranscribeSpecialty** (producer) Constant: [`SPECIALTY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#SPECIALTY) | The medical specialty of a medical transcription job. |  | String |
| **CamelAwsTranscribeType** (producer) Constant: [`TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-transcribe/latest/org/apache/camel/component/aws2/transcribe/Transcribe2Constants.html#TYPE) | The audio type of a medical transcription job. |  | String |

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