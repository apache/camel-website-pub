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

Required Lambda component options

You have to provide the awsLambdaClient in the Registry or your accessKey and secretKey to access the [Amazon Lambda](https://aws.amazon.com/lambda/) service.

## Message Headers

The AWS Lambda component supports 30 message header(s), which is/are listed below:

   
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