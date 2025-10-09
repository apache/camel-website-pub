# AWS Lambda

**Since Camel 3.2**

**Only producer is supported**

The AWS2 Lambda component supports create, get, list, delete, and invoke [AWS Lambda](https://aws.amazon.com/lambda/) functions.

**Prerequisites**

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Lambda. More information is available at [AWS Lambda](https://aws.amazon.com/lambda/).

When creating a Lambda function, you need to specify an IAM role which has at least the AWSLambdaBasicExecuteRole policy attached.

## URI Format

aws2-lambda://functionName\[?options\]

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

The AWS Lambda component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | Lambda2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform. It can be listFunctions, getFunction, createFunction, deleteFunction or invokeFunction.

Enum values:

-   listFunctions
    
-   getFunction
    
-   createAlias
    
-   deleteAlias
    
-   getAlias
    
-   listAliases
    
-   createFunction
    
-   deleteFunction
    
-   invokeFunction
    
-   updateFunction
    
-   createEventSourceMapping
    
-   deleteEventSourceMapping
    
-   listEventSourceMapping
    
-   listTags
    
-   tagResource
    
-   untagResource
    
-   publishVersion
    
-   listVersions
    
-   createFunctionUrlConfig
    
-   getFunctionUrlConfig
    
-   updateFunctionUrlConfig
    
-   deleteFunctionUrlConfig
    
-   listFunctionUrlConfigs
    
-   getFunctionConfiguration
    
-   updateFunctionConfiguration
    
-   putFunctionConcurrency
    
-   deleteFunctionConcurrency
    
-   getFunctionConcurrency
    
-   addPermission
    
-   removePermission
    
-   getPolicy
    





 | invokeFunction | Lambda2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Lambda client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **awsLambdaClient** (advanced) | **Autowired** To use an existing configured AwsLambdaClient client. |  | LambdaClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Lambda client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Lambda client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Lambda client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Lambda client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Lambda client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Lambda client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Lambda. | false | boolean |

## Endpoint Options

The AWS Lambda endpoint is configured using URI syntax:

aws2-lambda:function

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **function** (producer) | **Required** Name of the Lambda function. |  | String |

### Query Parameters (18 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
The operation to perform. It can be listFunctions, getFunction, createFunction, deleteFunction or invokeFunction.

Enum values:

-   listFunctions
    
-   getFunction
    
-   createAlias
    
-   deleteAlias
    
-   getAlias
    
-   listAliases
    
-   createFunction
    
-   deleteFunction
    
-   invokeFunction
    
-   updateFunction
    
-   createEventSourceMapping
    
-   deleteEventSourceMapping
    
-   listEventSourceMapping
    
-   listTags
    
-   tagResource
    
-   untagResource
    
-   publishVersion
    
-   listVersions
    
-   createFunctionUrlConfig
    
-   getFunctionUrlConfig
    
-   updateFunctionUrlConfig
    
-   deleteFunctionUrlConfig
    
-   listFunctionUrlConfigs
    
-   getFunctionConfiguration
    
-   updateFunctionConfiguration
    
-   putFunctionConcurrency
    
-   deleteFunctionConcurrency
    
-   getFunctionConcurrency
    
-   addPermission
    
-   removePermission
    
-   getPolicy
    





 | invokeFunction | Lambda2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (producer) | 

The region in which the Lambda client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **awsLambdaClient** (advanced) | **Autowired** To use an existing configured AwsLambdaClient client. |  | LambdaClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Lambda client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Lambda client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Lambda client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Lambda client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Lambda client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Lambda client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Lambda. | false | boolean |

## Message Headers

The AWS Lambda component supports 56 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsLambdaOperation** (all) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#OPERATION) | **Required** The operation we want to perform. Override operation passed as query parameter. |  | String |
| **CamelAwsLambdaS3Bucket** (createFunction) Constant: [`S3_BUCKET`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#S3_BUCKET) | Amazon S3 bucket name where the .zip file containing your deployment package is stored. This bucket must reside in the same AWS region where you are creating the Lambda function. |  | String |
| **CamelAwsLambdaS3Key** (createFunction) Constant: [`S3_KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#S3_KEY) | The Amazon S3 object (the deployment package) key name you want to upload. |  | String |
| **CamelAwsLambdaS3ObjectVersion** (createFunction) Constant: [`S3_OBJECT_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#S3_OBJECT_VERSION) | The Amazon S3 object (the deployment package) version you want to upload. |  | String |
| **CamelAwsLambdaZipFile** (createFunction) Constant: [`ZIP_FILE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#ZIP_FILE) | The local path of the zip file (the deployment package). Content of zip file can also be put in Message body. |  | String |
| **CamelAwsLambdaDescription** (createFunction) Constant: [`DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#DESCRIPTION) | The user-provided description. |  | String |
| **CamelAwsLambdaRole** (createFunction) Constant: [`ROLE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#ROLE) | **Required** The Amazon Resource Name (ARN) of the IAM role that Lambda assumes when it executes your function to access any other Amazon Web Services (AWS) resources. |  | String |
| **CamelAwsLambdaRuntime** (createFunction) Constant: [`RUNTIME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#RUNTIME) | **Required** The runtime environment for the Lambda function you are uploading. (nodejs, nodejs4.3, nodejs6.10, java8, python2.7, python3.6, dotnetcore1.0, odejs4.3-edge). |  | String |
| **CamelAwsLambdaHandler** (createFunction) Constant: [`HANDLER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#HANDLER) | **Required** The function within your code that Lambda calls to begin execution. For Node.js, it is the module-name.export value in your function. For Java, it can be package.class-name::handler or package.class-name. |  | String |
| **CamelAwsLambdaTargetArn** (createFunction) Constant: [`TARGET_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#TARGET_ARN) | The parent object that contains the target ARN (Amazon Resource Name) of an Amazon SQS queue or Amazon SNS topic. |  | String |
| **CamelAwsLambdaMemorySize** (createFunction) Constant: [`MEMORY_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#MEMORY_SIZE) | The memory size, in MB, you configured for the function. Must be a multiple of 64 MB. |  | Integer |
| **CamelAwsLambdaKMSKeyArn** (createFunction) Constant: [`KMS_KEY_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#KMS_KEY_ARN) | The Amazon Resource Name (ARN) of the KMS key used to encrypt your function’s environment variables. If not provided, AWS Lambda will use a default service key. |  | String |
| **CamelAwsLambdaEnvironmentVariables** (createFunction) Constant: [`ENVIRONMENT_VARIABLES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#ENVIRONMENT_VARIABLES) | The key-value pairs that represent your environment’s configuration settings. |  | Map |
| **CamelAwsLambdaPublish** (createFunction updateFunction) Constant: [`PUBLISH`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#PUBLISH) | This boolean parameter can be used to request AWS Lambda to create the Lambda function and publish a version as an atomic operation. |  | Boolean |
| **CamelAwsLambdaTimeout** (createFunction) Constant: [`TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#TIMEOUT) | The function execution time at which Lambda should terminate the function. The default is 3 seconds. |  | Integer |
| **CamelAwsLambdaTags** (createFunction) Constant: [`TAGS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#TAGS) | The list of tags (key-value pairs) assigned to the new function. |  | Map |
| **CamelAwsLambdaTracingConfig** (createFunction) Constant: [`TRACING_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#TRACING_CONFIG) | Your function’s tracing settings (Active or PassThrough). |  | String |
| **CamelAwsLambdaSecurityGroupIds** (createFunction) Constant: [`SECURITY_GROUP_IDS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#SECURITY_GROUP_IDS) | If your Lambda function accesses resources in a VPC, a list of one or more security groups IDs in your VPC. |  | List |
| **CamelAwsLambdaSubnetIds** (createFunction) Constant: [`SUBNET_IDS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#SUBNET_IDS) | If your Lambda function accesses resources in a VPC, a list of one or more subnet IDs in your VPC. |  | List |
| **CamelAwsLambdaEventSourceArn** (createEventSourceMapping) Constant: [`EVENT_SOURCE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#EVENT_SOURCE_ARN) | The Amazon Resource Name (ARN) of the event source. |  | String |
| **CamelAwsLambdaEventSourceBatchSize** (createEventSourceMapping) Constant: [`EVENT_SOURCE_BATCH_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#EVENT_SOURCE_BATCH_SIZE) | The maximum number of records in each batch that Lambda pulls from your stream or queue and sends to your function. |  | Integer |
| **CamelAwsLambdaEventSourceUuid** (deleteEventSourceMapping) Constant: [`EVENT_SOURCE_UUID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#EVENT_SOURCE_UUID) | The identifier of the event source mapping. |  | String |
| **CamelAwsLambdaResourceArn** (listTags tagResource untagResource) Constant: [`RESOURCE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#RESOURCE_ARN) | The function’s Amazon Resource Name (ARN). |  | String |
| **CamelAwsLambdaResourceTags** (tagResource) Constant: [`RESOURCE_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#RESOURCE_TAGS) | A list of tags to apply to the function. |  | Map |
| **CamelAwsLambdaResourceTagKeys** (untagResource) Constant: [`RESOURCE_TAG_KEYS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#RESOURCE_TAG_KEYS) | A list of tag keys to remove from the function. |  | List |
| **CamelAwsLambdaVersionDescription** (publishVersion) Constant: [`VERSION_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#VERSION_DESCRIPTION) | A description for the version to override the description in the function configuration. |  | String |
| **CamelAwsLambdaVersionRevisionId** (publishVersion) Constant: [`VERSION_REVISION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#VERSION_REVISION_ID) | Only update the function if the revision ID matches the ID that’s specified. |  | String |
| **CamelAwsLambdaFunctionVersion** (createAlias listAliases) Constant: [`FUNCTION_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_VERSION) | The function version to set in the alias. |  | String |
| **CamelAwsLambdaAliasFunctionName** (createAlias deleteAlias getAlias) Constant: [`FUNCTION_ALIAS_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_ALIAS_NAME) | **Required** The function name of the alias. |  | String |
| **CamelAwsLambdaAliasFunctionDescription** (createAlias) Constant: [`FUNCTION_ALIAS_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_ALIAS_DESCRIPTION) | The function description to set in the alias. |  | String |
| **CamelAwsLambdaMarker** (listFunctions listVersions listAliases listEventSourceMapping listTags) Constant: [`MARKER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#MARKER) | The marker for the next set of results. |  | String |
| **CamelAwsLambdaMaxItems** (listFunctions listVersions listAliases listEventSourceMapping) Constant: [`MAX_ITEMS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#MAX_ITEMS) | The maximum number of results to return. |  | Integer |
| **CamelAwsLambdaIsTruncated** (listFunctions listVersions listAliases listEventSourceMapping) Constant: [`IS_TRUNCATED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#IS_TRUNCATED) | Whether the response has more results (is truncated). |  | Boolean |
| **CamelAwsLambdaFunctionArn** (createFunction getFunction publishVersion createAlias getAlias) Constant: [`FUNCTION_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_ARN) | The Amazon Resource Name (ARN) of the function. |  | String |
| **CamelAwsLambdaStatusCode** (invokeFunction) Constant: [`STATUS_CODE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#STATUS_CODE) | The HTTP status code of the function invocation. |  | Integer |
| **CamelAwsLambdaFunctionError** (invokeFunction) Constant: [`FUNCTION_ERROR`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_ERROR) | If present, indicates that an error occurred during function execution. |  | String |
| **CamelAwsLambdaLogResult** (invokeFunction) Constant: [`LOG_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#LOG_RESULT) | The last 4 KB of the execution log. |  | String |
| **CamelAwsLambdaFunctionUrlAuthType** (createFunctionUrlConfig updateFunctionUrlConfig) Constant: [`FUNCTION_URL_AUTH_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_URL_AUTH_TYPE) | **Required** The type of authentication that the function URL uses. Set to AWS\_IAM to restrict access to authenticated users only. Set to NONE to bypass IAM authentication and allow any user to invoke the function. |  | String |
| **CamelAwsLambdaFunctionUrlQualifier** (createFunctionUrlConfig updateFunctionUrlConfig getFunctionUrlConfig deleteFunctionUrlConfig) Constant: [`FUNCTION_URL_QUALIFIER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_URL_QUALIFIER) | The alias name or $LATEST for the function URL. |  | String |
| **CamelAwsLambdaFunctionUrlCorsAllowCredentials** (createFunctionUrlConfig updateFunctionUrlConfig) Constant: [`FUNCTION_URL_CORS_ALLOW_CREDENTIALS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_URL_CORS_ALLOW_CREDENTIALS) | The cross-origin resource sharing (CORS) settings for the function URL. |  | String |
| **CamelAwsLambdaFunctionUrlCorsAllowOrigins** (createFunctionUrlConfig updateFunctionUrlConfig) Constant: [`FUNCTION_URL_CORS_ALLOW_ORIGINS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_URL_CORS_ALLOW_ORIGINS) | The allowed origins for CORS. |  | List |
| **CamelAwsLambdaFunctionUrlCorsAllowMethods** (createFunctionUrlConfig updateFunctionUrlConfig) Constant: [`FUNCTION_URL_CORS_ALLOW_METHODS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_URL_CORS_ALLOW_METHODS) | The allowed HTTP methods for CORS. |  | List |
| **CamelAwsLambdaFunctionUrlCorsAllowHeaders** (createFunctionUrlConfig updateFunctionUrlConfig) Constant: [`FUNCTION_URL_CORS_ALLOW_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_URL_CORS_ALLOW_HEADERS) | The allowed HTTP headers for CORS. |  | List |
| **CamelAwsLambdaFunctionUrlCorsExposeHeaders** (createFunctionUrlConfig updateFunctionUrlConfig) Constant: [`FUNCTION_URL_CORS_EXPOSE_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_URL_CORS_EXPOSE_HEADERS) | The exposed headers for CORS. |  | List |
| **CamelAwsLambdaFunctionUrlCorsMaxAge** (createFunctionUrlConfig updateFunctionUrlConfig) Constant: [`FUNCTION_URL_CORS_MAX_AGE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_URL_CORS_MAX_AGE) | The max age in seconds for CORS. |  | Integer |
| **CamelAwsLambdaFunctionUrl** (createFunctionUrlConfig getFunctionUrlConfig) Constant: [`FUNCTION_URL`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_URL) | The function URL endpoint. |  | String |
| **CamelAwsLambdaFunctionMemorySize** (updateFunctionConfiguration) Constant: [`FUNCTION_MEMORY_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_MEMORY_SIZE) | The amount of memory available to the function at runtime. Increasing the function memory also increases its CPU allocation. The default value is 128 MB. The value can be any multiple of 1 MB. |  | Integer |
| **CamelAwsLambdaFunctionTimeout** (updateFunctionConfiguration) Constant: [`FUNCTION_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_TIMEOUT) | The amount of time (in seconds) that Lambda allows a function to run before stopping it. The default is 3 seconds. The maximum allowed value is 900 seconds. |  | Integer |
| **CamelAwsLambdaFunctionRuntime** (updateFunctionConfiguration) Constant: [`FUNCTION_RUNTIME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_RUNTIME) | The new runtime environment for the function. |  | String |
| **CamelAwsLambdaFunctionHandler** (updateFunctionConfiguration) Constant: [`FUNCTION_HANDLER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#FUNCTION_HANDLER) | The new function handler. |  | String |
| **CamelAwsLambdaReservedConcurrentExecutions** (putFunctionConcurrency) Constant: [`RESERVED_CONCURRENT_EXECUTIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#RESERVED_CONCURRENT_EXECUTIONS) | **Required** The number of simultaneous executions to reserve for the function. |  | Integer |
| **CamelAwsLambdaStatementId** (addPermission) Constant: [`STATEMENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#STATEMENT_ID) | **Required** A unique statement identifier for the permission. |  | String |
| **CamelAwsLambdaAction** (addPermission) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#ACTION) | **Required** The action that the principal can use on the function. For example, lambda:InvokeFunction or lambda:GetFunction. |  | String |
| **CamelAwsLambdaPrincipal** (addPermission) Constant: [`PRINCIPAL`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#PRINCIPAL) | **Required** The Amazon Web Services service, Amazon Web Services account, IAM user, or IAM role that invokes the function. For example, s3.amazonaws.com or 123456789012. |  | String |
| **CamelAwsLambdaSourceAccount** (addPermission) Constant: [`SOURCE_ACCOUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#SOURCE_ACCOUNT) | The Amazon Web Services account ID of the principal. |  | String |
| **CamelAwsLambdaSourceArn** (addPermission) Constant: [`SOURCE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-lambda/latest/org/apache/camel/component/aws2/lambda/Lambda2Constants.html#SOURCE_ARN) | The ARN of the Amazon Web Services resource that invokes the function. For example, an Amazon S3 bucket or Amazon SNS topic. |  | String |

Required Lambda component options

You have to provide the awsLambdaClient in the Registry or your accessKey and secretKey to access the [Amazon Lambda](https://aws.amazon.com/lambda/) service.

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

## List of Available Operations

-   listFunctions
    
-   getFunction
    
-   createFunction
    
-   deleteFunction
    
-   invokeFunction
    
-   updateFunction
    
-   createEventSourceMapping
    
-   deleteEventSourceMapping
    
-   listEventSourceMapping
    
-   listTags
    
-   tagResource
    
-   untagResource
    
-   publishVersion
    
-   listVersions
    
-   createAlias
    
-   deleteAlias
    
-   getAlias
    
-   listAliases
    
-   createFunctionUrlConfig
    
-   getFunctionUrlConfig
    
-   updateFunctionUrlConfig
    
-   deleteFunctionUrlConfig
    
-   listFunctionUrlConfigs
    
-   getFunctionConfiguration
    
-   updateFunctionConfiguration
    
-   putFunctionConcurrency
    
-   deleteFunctionConcurrency
    
-   getFunctionConcurrency
    
-   addPermission
    
-   removePermission
    
-   getPolicy
    

## Examples

### Producer Example

To have a full understanding of how the component works, you may have a look at these [integration tests](https://github.com/apache/camel/tree/main/components/camel-aws/camel-aws2-lambda/src/test/java/org/apache/camel/component/aws2/lambda/integration)

### Producer Examples

-   CreateFunction: this operation will create a function for you in AWS Lambda
    

```java
  from("direct:createFunction").to("aws2-lambda://GetHelloWithName?operation=createFunction").to("mock:result");
```

and by sending

```java
        template.send("direct:createFunction", ExchangePattern.InOut, new Processor() {
            @Override
            public void process(Exchange exchange) throws Exception {
                exchange.getIn().setHeader(Lambda2Constants.RUNTIME, "nodejs6.10");
                exchange.getIn().setHeader(Lambda2Constants.HANDLER, "GetHelloWithName.handler");
                exchange.getIn().setHeader(Lambda2Constants.DESCRIPTION, "Hello with node.js on Lambda");
                exchange.getIn().setHeader(Lambda2Constants.ROLE,
                        "arn:aws:iam::643534317684:role/lambda-execution-role");

                ClassLoader classLoader = getClass().getClassLoader();
                File file = new File(
                        classLoader
                                .getResource("org/apache/camel/component/aws2/lambda/function/node/GetHelloWithName.zip")
                                .getFile());
                FileInputStream inputStream = new FileInputStream(file);
                exchange.getIn().setBody(inputStream);
            }
        });
```

### Function URL Operations

Function URLs provide a dedicated HTTP(S) endpoint for your Lambda function, enabling direct invocation via HTTP without needing API Gateway.

-   createFunctionUrlConfig: this operation will create a function URL for your Lambda function
    

```java
from("direct:createFunctionUrl")
    .setHeader(Lambda2Constants.FUNCTION_URL_AUTH_TYPE, constant("NONE"))
    .to("aws2-lambda://myFunction?operation=createFunctionUrlConfig")
    .to("mock:result");
```

The `FUNCTION_URL_AUTH_TYPE` can be either `NONE` (public access) or `AWS_IAM` (authenticated access).

-   getFunctionUrlConfig: this operation will retrieve the function URL configuration
    

```java
from("direct:getFunctionUrl")
    .to("aws2-lambda://myFunction?operation=getFunctionUrlConfig")
    .to("mock:result");
```

-   updateFunctionUrlConfig: this operation will update the function URL configuration
    

```java
from("direct:updateFunctionUrl")
    .setHeader(Lambda2Constants.FUNCTION_URL_AUTH_TYPE, constant("AWS_IAM"))
    .to("aws2-lambda://myFunction?operation=updateFunctionUrlConfig")
    .to("mock:result");
```

-   deleteFunctionUrlConfig: this operation will delete the function URL
    

```java
from("direct:deleteFunctionUrl")
    .to("aws2-lambda://myFunction?operation=deleteFunctionUrlConfig")
    .to("mock:result");
```

-   listFunctionUrlConfigs: this operation will list all function URLs for a function
    

```java
from("direct:listFunctionUrls")
    .to("aws2-lambda://myFunction?operation=listFunctionUrlConfigs")
    .to("mock:result");
```

### Function Configuration Operations

Function Configuration operations allow you to view and modify your Lambda function’s runtime settings.

-   getFunctionConfiguration: this operation will retrieve the configuration details of a function
    

```java
from("direct:getFunctionConfiguration")
    .to("aws2-lambda://myFunction?operation=getFunctionConfiguration")
    .to("mock:result");
```

-   updateFunctionConfiguration: this operation will update the configuration of a function
    

```java
from("direct:updateFunctionConfiguration")
    .process(exchange -> {
        exchange.getIn().setHeader(Lambda2Constants.FUNCTION_MEMORY_SIZE, 512);
        exchange.getIn().setHeader(Lambda2Constants.FUNCTION_TIMEOUT, 60);
        exchange.getIn().setHeader(Lambda2Constants.DESCRIPTION, "Updated function description");
    })
    .to("aws2-lambda://myFunction?operation=updateFunctionConfiguration")
    .to("mock:result");
```

### Concurrency Operations

Concurrency operations allow you to manage reserved concurrency for your Lambda functions.

-   putFunctionConcurrency: this operation will set the reserved concurrency for a function
    

```java
from("direct:putFunctionConcurrency")
    .setHeader(Lambda2Constants.RESERVED_CONCURRENT_EXECUTIONS, constant(100))
    .to("aws2-lambda://myFunction?operation=putFunctionConcurrency")
    .to("mock:result");
```

-   deleteFunctionConcurrency: this operation will remove reserved concurrency from a function
    

```java
from("direct:deleteFunctionConcurrency")
    .to("aws2-lambda://myFunction?operation=deleteFunctionConcurrency")
    .to("mock:result");
```

-   getFunctionConcurrency: this operation will retrieve the reserved concurrency for a function
    

```java
from("direct:getFunctionConcurrency")
    .to("aws2-lambda://myFunction?operation=getFunctionConcurrency")
    .to("mock:result");
```

### Permission Operations

Permission operations allow you to manage the resource-based policy for your Lambda functions.

-   addPermission: this operation will add a permission to the function’s resource-based policy
    

```java
from("direct:addPermission")
    .process(exchange -> {
        exchange.getIn().setHeader(Lambda2Constants.STATEMENT_ID, "s3-invoke");
        exchange.getIn().setHeader(Lambda2Constants.ACTION, "lambda:InvokeFunction");
        exchange.getIn().setHeader(Lambda2Constants.PRINCIPAL, "s3.amazonaws.com");
        exchange.getIn().setHeader(Lambda2Constants.SOURCE_ARN, "arn:aws:s3:::my-bucket");
    })
    .to("aws2-lambda://myFunction?operation=addPermission")
    .to("mock:result");
```

-   removePermission: this operation will remove a permission from the function’s resource-based policy
    

```java
from("direct:removePermission")
    .setHeader(Lambda2Constants.STATEMENT_ID, constant("s3-invoke"))
    .to("aws2-lambda://myFunction?operation=removePermission")
    .to("mock:result");
```

-   getPolicy: this operation will retrieve the resource-based policy for a function
    

```java
from("direct:getPolicy")
    .to("aws2-lambda://myFunction?operation=getPolicy")
    .to("mock:result");
```

You can also configure CORS settings for function URLs:

```java
from("direct:createFunctionUrlWithCors")
    .process(exchange -> {
        exchange.getIn().setHeader(Lambda2Constants.FUNCTION_URL_AUTH_TYPE, "NONE");
        exchange.getIn().setHeader(Lambda2Constants.FUNCTION_URL_CORS_ALLOW_ORIGINS,
            Arrays.asList("https://example.com"));
        exchange.getIn().setHeader(Lambda2Constants.FUNCTION_URL_CORS_ALLOW_METHODS,
            Arrays.asList("GET", "POST"));
        exchange.getIn().setHeader(Lambda2Constants.FUNCTION_URL_CORS_ALLOW_HEADERS,
            Arrays.asList("Content-Type", "Authorization"));
        exchange.getIn().setHeader(Lambda2Constants.FUNCTION_URL_CORS_MAX_AGE, 3600);
    })
    .to("aws2-lambda://myFunction?operation=createFunctionUrlConfig")
    .to("mock:result");
```

## Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as the body. In AWS Lambda there are multiple operations you can submit, as an example for Get Function request, you can do something like:

```java
from("direct:getFunction")
     .setBody(GetFunctionRequest.builder().functionName("test").build())
     .to("aws2-lambda://GetHelloWithName?awsLambdaClient=#awsLambdaClient&operation=getFunction&pojoRequest=true")
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-lambda</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-lambda with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-lambda-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-lambda.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-lambda.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-lambda.aws-lambda-client** | To use an existing configured AwsLambdaClient client. The option is a software.amazon.awssdk.services.lambda.LambdaClient type. |  | LambdaClient |
| **camel.component.aws2-lambda.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.lambda.Lambda2Configuration type. |  | Lambda2Configuration |
| **camel.component.aws2-lambda.enabled** | Whether to enable auto configuration of the aws2-lambda component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-lambda.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws2-lambda.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws2-lambda.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-lambda.operation** | The operation to perform. It can be listFunctions, getFunction, createFunction, deleteFunction or invokeFunction. | invokefunction | Lambda2Operations |
| **camel.component.aws2-lambda.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-lambda.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-lambda.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **camel.component.aws2-lambda.proxy-host** | To define a proxy host when instantiating the Lambda client. |  | String |
| **camel.component.aws2-lambda.proxy-port** | To define a proxy port when instantiating the Lambda client. |  | Integer |
| **camel.component.aws2-lambda.proxy-protocol** | To define a proxy protocol when instantiating the Lambda client. | https | Protocol |
| **camel.component.aws2-lambda.region** | The region in which the Lambda client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-lambda.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-lambda.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws2-lambda.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-lambda.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-lambda.use-default-credentials-provider** | Set whether the Lambda client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-lambda.use-profile-credentials-provider** | Set whether the Lambda client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-lambda.use-session-credentials** | Set whether the Lambda client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Lambda. | false | Boolean |