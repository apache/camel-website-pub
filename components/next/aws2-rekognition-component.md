# AWS Rekognition

**Since Camel 4.17**

**Only producer is supported**

The AWS2 Rekognition component supports the following operations on [AWS Rekognition](https://aws.amazon.com/rekognition/):

\- -

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Rekognition. More information is available at [AWS Rekognition](https://aws.amazon.com/rekognition/).

## URI Format

aws2-rekognition://label\[?options\]

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

The AWS Rekognition component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | Rekognition2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform. It can be listFunctions, getFunction, createFunction, deleteFunction or invokeFunction.

Enum values:

-   associateFaces
    
-   compareFaces
    
-   createCollection
    
-   createUser
    
-   deleteCollection
    
-   deleteFaces
    
-   deleteUser
    
-   describeCollection
    
-   detectFaces
    
-   detectLabels
    
-   detectModerationLabels
    
-   detectProtectiveEquipment
    
-   detectText
    
-   disassociateFaces
    
-   getCelebrityInfo
    
-   getMediaAnalysisJob
    
-   indexFaces
    
-   listCollections
    
-   listMediaAnalysisJobs
    
-   listFaces
    
-   listUsers
    
-   recognizeCelebrities
    
-   searchFaces
    
-   searchFacesByImage
    
-   searchUsers
    
-   searchUsersByImage
    
-   startMediaAnalysisJob
    





 |  | Rekognition2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which Rekognition client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Rekognition client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Rekognition client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **awsRekognitionClient** (advanced) | **Autowired** To use an existing configured AwsRekognitionClient client. |  | RekognitionClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Rekognition client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Rekognition client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Rekognition client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **useSessionCredentials** (security) | Set whether the Rekognition client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Rekognition. | false | boolean |

## Endpoint Options

The AWS Rekognition endpoint is configured using URI syntax:

aws2-rekognition:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (18 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform. It can be listFunctions, getFunction, createFunction, deleteFunction or invokeFunction.

Enum values:

-   associateFaces
    
-   compareFaces
    
-   createCollection
    
-   createUser
    
-   deleteCollection
    
-   deleteFaces
    
-   deleteUser
    
-   describeCollection
    
-   detectFaces
    
-   detectLabels
    
-   detectModerationLabels
    
-   detectProtectiveEquipment
    
-   detectText
    
-   disassociateFaces
    
-   getCelebrityInfo
    
-   getMediaAnalysisJob
    
-   indexFaces
    
-   listCollections
    
-   listMediaAnalysisJobs
    
-   listFaces
    
-   listUsers
    
-   recognizeCelebrities
    
-   searchFaces
    
-   searchFacesByImage
    
-   searchUsers
    
-   searchUsersByImage
    
-   startMediaAnalysisJob
    





 |  | Rekognition2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which Rekognition client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Rekognition client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Rekognition client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **awsRekognitionClient** (advanced) | **Autowired** To use an existing configured AwsRekognitionClient client. |  | RekognitionClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Rekognition client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Rekognition client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Rekognition client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **useSessionCredentials** (security) | Set whether the Rekognition client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Rekognition. | false | boolean |

## Message Headers

The AWS Rekognition component supports 35 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsRekognitionOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsRekognitionCollectionId** (producer) Constant: [`COLLECTION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#COLLECTION_ID) | The ID of the Collection. |  | String |
| **CamelAwsRekognitionUserId** (producer) Constant: [`USER_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#USER_ID) | The ID of the User. |  | String |
| **CamelAwsRekognitionFaceIds** (producer) Constant: [`FACE_IDS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#FACE_IDS) | Collection of the Face IDs. |  | Collection |
| **CamelAwsRekognitionUserMatchThreshold** (producer) Constant: [`USER_MATCH_THRESHOLD`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#USER_MATCH_THRESHOLD) | Minimum user match confidence required for the face to be associated with a UserID that has at least one FaceID already associated. |  | Float |
| **CamelAwsRekognitionClientRequestToken** (producer) Constant: [`CLIENT_REQUEST_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#CLIENT_REQUEST_TOKEN) | The ID of the User. |  | String |
| **CamelAwsRekognitionSourceImage** (producer) Constant: [`SOURCE_IMAGE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#SOURCE_IMAGE) | Source Input Image. |  | Image |
| **CamelAwsRekognitionTargetImage** (producer) Constant: [`TARGET_IMAGE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#TARGET_IMAGE) | Target Input Image. |  | Image |
| **CamelAwsRekognitionSimilarityThreshold** (producer) Constant: [`SIMILARITY_THRESHOLD`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#SIMILARITY_THRESHOLD) | Similarity Score Threshold. |  | Float |
| **CamelAwsRekognitionQualityFilter** (producer) Constant: [`QUALITY_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#QUALITY_FILTER) | Allows to filter out detected faces that dont meet a required quality bar. |  | String |
| **CamelAwsRekognitionImage** (producer) Constant: [`IMAGE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#IMAGE) | Input Image. |  | Image |
| **CamelAwsRekognitionFacialAttributes** (producer) Constant: [`FACIAL_ATTRIBUTES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#FACIAL_ATTRIBUTES) | Facial Attributes to be returned. |  | List |
| **CamelAwsRekognitionMaxLabels** (producer) Constant: [`MAX_LABELS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#MAX_LABELS) | Maximum Labels to detect. |  | Integer |
| **CamelAwsRekognitionMinConfidence** (producer) Constant: [`MIN_CONFIDENCE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#MIN_CONFIDENCE) | Minimum confidence level for the labels to return. |  | Float |
| **CamelAwsRekognitionFeatures** (producer) Constant: [`FEATURES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#FEATURES) | A list of the types of analysis to perform. |  | Collection |
| **CamelAwsRekognitionDetectLabelsSettings** (producer) Constant: [`DETECT_LABELS_SETTINGS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#DETECT_LABELS_SETTINGS) | A list of the filters to be applied to returned detected labels and image properties. |  | DetectLabelsSettings |
| **CamelAwsRekognitionHumanLoopConfig** (producer) Constant: [`HUMAN_LOOP_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#HUMAN_LOOP_CONFIG) | Sets up the configuration for human evaluation. |  | HumanLoopConfig |
| **CamelAwsRekognitionProjectVersion** (producer) Constant: [`PROJECT_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#PROJECT_VERSION) | Identifier for the custom adapter. |  | String |
| **CamelAwsRekognitionProtectiveEquipmentSummarizationAttributes** (producer) Constant: [`PROTECTIVE_EQUIPMENT_SUMMARIZATION_ATTRIBUTES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#PROTECTIVE_EQUIPMENT_SUMMARIZATION_ATTRIBUTES) | An array of PPE types to summarize. |  | ProtectiveEquipmentSummarizationAttributes |
| **CamelAwsRekognitionWordFilter** (producer) Constant: [`WORD_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#WORD_FILTER) | An optional filter that specifies words to include in the response. |  | DetectTextFilters |
| **CamelAwsRekognitionCelebrityId** (producer) Constant: [`CELEBRITY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#CELEBRITY_ID) | The ID of the celebrity to get information about. |  | String |
| **CamelAwsRekognitionJobId** (producer) Constant: [`JOB_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#JOB_ID) | Unique identifier for the media analysis job for which you want to retrieve results. |  | String |
| **CamelAwsRekognitionJobName** (producer) Constant: [`JOB_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#JOB_NAME) | The name of the media analysis job. |  | String |
| **CamelAwsRekognitionInput** (producer) Constant: [`INPUT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#INPUT) | Input data to be analyzed by the job. |  | MediaAnalysisInput |
| **CamelAwsRekognitionOutputConfig** (producer) Constant: [`OUTPUT_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#OUTPUT_CONFIG) | The Amazon S3 bucket location to store the results. |  | MediaAnalysisOutputConfig |
| **CamelAwsRekognitionOperationsConfig** (producer) Constant: [`OPERATIONS_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#OPERATIONS_CONFIG) | Configuration options for the media analysis job to be created. |  | MediaAnalysisOperationsConfig |
| **CamelAwsRekognitionKmsKeyId** (producer) Constant: [`KMS_KEY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#KMS_KEY_ID) | The identifier for your AWS Key Management Service key (AWS KMS key). |  | String |
| **CamelAwsRekognitionExternalImageId** (producer) Constant: [`EXTERNAL_IMAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#EXTERNAL_IMAGE_ID) | The ID used to identify a user in the collection. |  | String |
| **CamelAwsRekognitionDetectionAttributes** (producer) Constant: [`DETECTION_ATTRIBUTES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#DETECTION_ATTRIBUTES) | An array of facial attributes to return. |  | Collection |
| **CamelAwsRekognitionMaxFaces** (producer) Constant: [`MAX_FACES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#MAX_FACES) | The maximum number of faces to index. |  | Integer |
| **CamelAwsRekognitionMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#MAX_RESULTS) | Maximum number of results to return. |  | Integer |
| **CamelAwsRekognitionNextToken** (producer) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#NEXT_TOKEN) | Pagination token from the previous response. |  | String |
| **CamelAwsRekognitionFaceId** (producer) Constant: [`FACE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#FACE_ID) | ID of a face to find matches for in the collection. |  | String |
| **CamelAwsRekognitionFaceMatchThreshold** (producer) Constant: [`FACE_MATCH_THRESHOLD`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#FACE_MATCH_THRESHOLD) | Optional value specifying the minimum confidence in the face match to return. |  | Float |
| **CamelAwsRekognitionMaxUsers** (producer) Constant: [`MAX_USERS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-rekognition/latest/org/apache/camel/component/aws2/rekognition/Rekognition2Constants.html#MAX_USERS) | Maximum number of users to return in the response. |  | Integer |

Required Rekognition component options

You have to provide the `awsRekognitionClient` in the Camel Registry or your accessKey and secretKey to access the [AWS Rekognition](https://aws.amazon.com/rekognition/) service.

## Usage

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Rekognition Producer operations

Camel-AWS Rekognition component provides the following operation on the producer side:

-   associateFaces
    
-   compareFaces
    
-   createCollection
    
-   createUser
    
-   deleteCollection
    
-   deleteFaces
    
-   deleteUser
    
-   describeCollection
    
-   detectFaces
    
-   detectLabels
    
-   detectModerationLabels
    
-   detectProtectiveEquipment
    
-   detectText
    
-   disassociateFaces
    
-   getCelebrityInfo
    
-   getMediaAnalysisJob
    
-   indexFaces
    
-   listCollections
    
-   listMediaAnalysisJobs
    
-   listFaces
    
-   listUsers
    
-   recognizeCelebrities
    
-   searchFaces
    
-   searchFacesByImage
    
-   searchUsers
    
-   searchUsersByImage
    
-   startMediaAnalysisJob
    

## Examples

### Producer Examples

-   createCollection: this operation will create a collection
    

```java
from("direct:createCollection")
    .to("aws2-rekognition://test?awsRekognitionClient=#awsRekognitionClient&operation=createCollection")
```

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as the body. In AWS Rekognition, there are multiple operations you can submit, as an example for Create Collection request, you can do something like:

```java
from("direct:start")
  .setBody(CreateCollectionRequest.builder().collectionId("test-collection").build())
  .to("aws2-rekognition://test?awsRekognitionClient=#awsRekognitionClient&operation=createCollection&pojoRequest=true")
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-rekognition</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.