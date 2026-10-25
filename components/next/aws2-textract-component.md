# AWS Textract

**Since Camel 4.15**

**Only producer is supported**

The AWS2 Textract component supports extracting text and data from documents [AWS Textract](https://aws.amazon.com/textract/)

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Textract. More information is available at [Amazon Textract](https://aws.amazon.com/textract/).

## URI Format

aws2-textract://label\[?options\]

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

The AWS Textract component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | Textract2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   detectDocumentText
    
-   analyzeDocument
    
-   analyzeExpense
    
-   startDocumentTextDetection
    
-   startDocumentAnalysis
    
-   startExpenseAnalysis
    
-   getDocumentTextDetection
    
-   getDocumentAnalysis
    
-   getExpenseAnalysis
    





 | detectDocumentText | Textract2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which Textract client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **s3Bucket** (producer) | The S3 bucket name for document location. |  | String |
| **s3Object** (producer) | The S3 object name for document location. |  | String |
| **s3ObjectVersion** (producer) | The S3 object version for document location. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **textractClient** (advanced) | **Autowired** To use an existing configured AWS Textract client. |  | TextractClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Textract client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Textract client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Textract client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Textract client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Textract client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Textract client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Textract. | false | boolean |

## Endpoint Options

The AWS Textract endpoint is configured using URI syntax:

aws2-textract:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   detectDocumentText
    
-   analyzeDocument
    
-   analyzeExpense
    
-   startDocumentTextDetection
    
-   startDocumentAnalysis
    
-   startExpenseAnalysis
    
-   getDocumentTextDetection
    
-   getDocumentAnalysis
    
-   getExpenseAnalysis
    





 | detectDocumentText | Textract2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which Textract client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **s3Bucket** (producer) | The S3 bucket name for document location. |  | String |
| **s3Object** (producer) | The S3 object name for document location. |  | String |
| **s3ObjectVersion** (producer) | The S3 object version for document location. |  | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **textractClient** (advanced) | **Autowired** To use an existing configured AWS Textract client. |  | TextractClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Textract client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Textract client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Textract client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Textract client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Textract client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Textract client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Textract. | false | boolean |

## Message Headers

The AWS Textract component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsTextractOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-textract/latest/org/apache/camel/component/aws2/textract/Textract2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsTextractS3Bucket** (producer) Constant: [`S3_BUCKET`](https://javadoc.io/doc/org.apache.camel/camel-aws2-textract/latest/org/apache/camel/component/aws2/textract/Textract2Constants.html#S3_BUCKET) | The S3 bucket name containing the document to process. |  | String |
| **CamelAwsTextractS3Object** (producer) Constant: [`S3_OBJECT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-textract/latest/org/apache/camel/component/aws2/textract/Textract2Constants.html#S3_OBJECT) | The S3 object name (key) of the document to process. |  | String |
| **CamelAwsTextractS3ObjectVersion** (producer) Constant: [`S3_OBJECT_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-textract/latest/org/apache/camel/component/aws2/textract/Textract2Constants.html#S3_OBJECT_VERSION) | The S3 object version of the document to process. |  | String |
| **CamelAwsTextractJobId** (producer) Constant: [`JOB_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-textract/latest/org/apache/camel/component/aws2/textract/Textract2Constants.html#JOB_ID) | The job ID of an async operation. It is set from the response of the startDocumentTextDetection, startDocumentAnalysis and startExpenseAnalysis operations, and it is the job ID of the getDocumentTextDetection, getDocumentAnalysis and getExpenseAnalysis operations (else the body is used as the job ID). |  | String |
| **CamelAwsTextractMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-textract/latest/org/apache/camel/component/aws2/textract/Textract2Constants.html#MAX_RESULTS) | The maximum number of results to return in paginated operations. |  | Integer |
| **CamelAwsTextractNextToken** (producer) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-textract/latest/org/apache/camel/component/aws2/textract/Textract2Constants.html#NEXT_TOKEN) | The next token for pagination in operations that return multiple pages. |  | String |
| **CamelAwsTextractFeatureTypes** (producer) Constant: [`FEATURE_TYPES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-textract/latest/org/apache/camel/component/aws2/textract/Textract2Constants.html#FEATURE_TYPES) | The feature types of the analyzeDocument and startDocumentAnalysis operations (TABLES, FORMS, QUERIES, SIGNATURES, LAYOUT): a list of FeatureType or String values, or a String with comma separated values. The String values are case-insensitive. Without this header TABLES and FORMS are used. |  | List |

## Message Body

The message body at each side of the AWS Textract component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | 
The document of detectDocumentText, the default, analyzeDocument and analyzeExpense when no S3 object is named: an image or a PDF as bytes, a stream or a file; a Map, a List, a POJO or no body fails. The s3Bucket and s3Object options, or else the CamelAwsTextractS3Bucket and CamelAwsTextractS3Object headers, name an S3 object instead, and the start operations read only that. The get operations take the job id from the CamelAwsTextractJobId header, or else the body as text. With pojoRequest=true the request of the AWS SDK for the operation, such as a DetectDocumentTextRequest: another body fails.

-   With `pojoRequest=true`: `pojo`
    





 |
| **Producer output** | `pojo` | The response of the AWS SDK for the operation, such as the DetectDocumentTextResponse of detectDocumentText, the default, whose blocks hold the lines and the words found. The start operations give the response with the job id, and set the CamelAwsTextractJobId header to it for the get operations. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

Required Textract component options

You have to provide the textractClient in the Registry or your accessKey and secretKey to access the [Amazon Textract](https://aws.amazon.com/textract/) service.

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

### The document

The synchronous operations (`detectDocumentText`, `analyzeDocument` and `analyzeExpense`) read the document from S3 or from the message body; the asynchronous `start` operations read it from S3 only:

-   The bucket is the `s3Bucket` option, or else the `CamelAwsTextractS3Bucket` header.
    
-   The object is the `s3Object` option, or else the `CamelAwsTextractS3Object` header.
    
-   The version is the `s3ObjectVersion` option, or else the `CamelAwsTextractS3ObjectVersion` header.
    

The options are used first: a header is read only when its option is not set. When both the bucket and the object are known, the document is that S3 object. Otherwise a synchronous operation uses the message body (as bytes) as the document, and an asynchronous operation fails.

### Feature types

The `analyzeDocument` and `startDocumentAnalysis` operations analyze the feature types of the `CamelAwsTextractFeatureTypes` header, or else `TABLES` and `FORMS`. The header can be a list (or array) of `FeatureType` or `String` values, or one `String` with comma separated values, such as `TABLES,SIGNATURES`. The `String` values are case-insensitive, and an unknown value fails with an `IllegalArgumentException`.

### Asynchronous operations

The `startDocumentTextDetection`, `startDocumentAnalysis` and `startExpenseAnalysis` operations return the start response as the body, and set the `CamelAwsTextractJobId` header to the job ID of the response. The `getDocumentTextDetection`, `getDocumentAnalysis` and `getExpenseAnalysis` operations read the job ID from the `CamelAwsTextractJobId` header, or else from the message body, so a `get` step can follow a `start` step (the job must have finished, see the `JobStatus` of the `get` response):

```yaml
- route:
    from:
      uri: direct:analyze
      steps:
        - setHeader:
            name: CamelAwsTextractFeatureTypes
            constant:
              expression: "TABLES,SIGNATURES"
        - to:
            uri: aws2-textract:textract
            parameters:
              operation: startDocumentAnalysis
              s3Bucket: my-documents
              s3Object: contracts/contract-1.pdf
        - delay:
            constant:
              expression: "10000"
        - to:
            uri: aws2-textract:textract
            parameters:
              operation: getDocumentAnalysis
        - log:
            message: "${body.jobStatus}"
```

### Example

The following route detects the text of an image in S3. Without `s3Bucket` and `s3Object`, the document is the message body:

```yaml
- route:
    from:
      uri: direct:detect
      steps:
        - to:
            uri: aws2-textract:textract
            parameters:
              operation: detectDocumentText
              s3Bucket: my-documents
              s3Object: invoices/invoice-1.png
              region: eu-west-1
              accessKey: "{{aws.access-key}}"
              secretKey: "{{aws.secret-key}}"
        - log:
            message: "${body}"
```

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-textract</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.