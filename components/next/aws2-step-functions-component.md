# AWS StepFunctions

**Since Camel 4.0**

**Only producer is supported**

The AWS2 Step Functions component supports the following operations on [AWS Step Functions](https://aws.amazon.com/step-functions/):

-   Create, delete, update, describe, list state machines.
    
-   Create, delete, describe, list activities.
    
-   Start, start sync, stop, list, describe executions.
    
-   Get activities task.
    
-   Get execution history
    

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Step Functions. More information is available at [AWS Step Functions](https://aws.amazon.com/step-functions/).

## URI Format

aws2-step-functions://label\[?options\]

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

The AWS StepFunctions component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | StepFunctions2Configuration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
**Required** The operation to perform. It can be listFunctions, getFunction, createFunction, deleteFunction or invokeFunction.

Enum values:

-   createStateMachine
    
-   deleteStateMachine
    
-   updateStateMachine
    
-   describeStateMachine
    
-   listStateMachines
    
-   createActivity
    
-   deleteActivity
    
-   describeActivity
    
-   getActivityTask
    
-   listActivities
    
-   startExecution
    
-   startSyncExecution
    
-   stopExecution
    
-   describeExecution
    
-   listExecutions
    
-   getExecutionHistory
    





 |  | StepFunctions2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which StepFunctions client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useDefaultCredentialsProvider** (producer) | Set whether the StepFunctions client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the StepFunctions client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **awsSfnClient** (advanced) | **Autowired** To use an existing configured AwsStepFunctionsClient client. |  | SfnClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the StepFunctions client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the StepFunctions client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the StepFunctions client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **useSessionCredentials** (security) | Set whether the Step Functions client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Step Functions. | false | boolean |

## Endpoint Options

The AWS StepFunctions endpoint is configured using URI syntax:

aws2-step-functions:label

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

-   createStateMachine
    
-   deleteStateMachine
    
-   updateStateMachine
    
-   describeStateMachine
    
-   listStateMachines
    
-   createActivity
    
-   deleteActivity
    
-   describeActivity
    
-   getActivityTask
    
-   listActivities
    
-   startExecution
    
-   startSyncExecution
    
-   stopExecution
    
-   describeExecution
    
-   listExecutions
    
-   getExecutionHistory
    





 |  | StepFunctions2Operations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **region** (producer) | 

The region in which StepFunctions client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **useDefaultCredentialsProvider** (producer) | Set whether the StepFunctions client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the StepFunctions client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **awsSfnClient** (advanced) | **Autowired** To use an existing configured AwsStepFunctionsClient client. |  | SfnClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the StepFunctions client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the StepFunctions client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the StepFunctions client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **useSessionCredentials** (security) | Set whether the Step Functions client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Step Functions. | false | boolean |

## Message Headers

The AWS StepFunctions component supports 18 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsStepFunctionsOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsStepFunctionsStateMachineName** (producer) Constant: [`STATE_MACHINE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#STATE_MACHINE_NAME) | The name of the state machine. |  | String |
| **CamelAwsStepFunctionsStateMachineDefinition** (producer) Constant: [`STATE_MACHINE_DEFINITION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#STATE_MACHINE_DEFINITION) | The Amazon States Language definition of the state machine. |  | String |
| **CamelAwsStepFunctionsStateMachineType** (producer) Constant: [`STATE_MACHINE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#STATE_MACHINE_TYPE) | Determines whether a Standard or Express state machine is created. |  | String |
| **CamelAwsStepFunctionsStateMachineRoleArn** (producer) Constant: [`STATE_MACHINE_ROLE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#STATE_MACHINE_ROLE_ARN) | The Amazon Resource Name (ARN) of the IAM role to use for this state machine. |  | String |
| **CamelAwsStepFunctionsStateMachineArn** (producer) Constant: [`STATE_MACHINE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#STATE_MACHINE_ARN) | The Amazon Resource Name (ARN) of state machine. |  | String |
| **CamelAwsStepFunctionsStateMachinesMaxResults** (producer) Constant: [`STATE_MACHINES_MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#STATE_MACHINES_MAX_RESULTS) | The limit number of results while listing state machines. |  | Integer |
| **CamelAwsStepFunctionsActivityName** (producer) Constant: [`ACTIVITY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#ACTIVITY_NAME) | The name of the state machine activity. |  | String |
| **CamelAwsStepFunctionsActivityArn** (producer) Constant: [`ACTIVITY_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#ACTIVITY_ARN) | The ARN of the state machine activity. |  | String |
| **CamelAwsStepFunctionsActivitiesMaxResults** (producer) Constant: [`ACTIVITIES_MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#ACTIVITIES_MAX_RESULTS) | The limit number of results while listing state machines. |  | Integer |
| **CamelAwsStepFunctionsExecutionArn** (producer) Constant: [`EXECUTION_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#EXECUTION_ARN) | The Amazon Resource Name (ARN) of the execution. |  | String |
| **CamelAwsStepFunctionsExecutionName** (producer) Constant: [`EXECUTION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#EXECUTION_NAME) | Optional name of the execution. |  | String |
| **CamelAwsStepFunctionsExecutionInput** (producer) Constant: [`EXECUTION_INPUT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#EXECUTION_INPUT) | The string that contains the JSON input data for the execution. |  | String |
| **CamelAwsStepFunctionsExecutionTraceHeader** (producer) Constant: [`EXECUTION_TRACE_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#EXECUTION_TRACE_HEADER) | Passes the X-Ray trace header. |  | String |
| **CamelAwsStepFunctionsExecutionHistoryMaxResults** (producer) Constant: [`EXECUTION_HISTORY_MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#EXECUTION_HISTORY_MAX_RESULTS) | The limit number of results while listing execution history. |  | Integer |
| **CamelAwsStepFunctionsExecutionHistoryIncludeExecutionData** (producer) Constant: [`EXECUTION_HISTORY_INCLUDE_EXECUTION_DATA`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#EXECUTION_HISTORY_INCLUDE_EXECUTION_DATA) | You can select whether execution data (input or output of a history event) is returned. |  | Boolean |
| **CamelAwsStepFunctionsExecutionHistoryReverseOrder** (producer) Constant: [`EXECUTION_HISTORY_REVERSE_ORDER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#EXECUTION_HISTORY_REVERSE_ORDER) | Lists events in descending order of their timeStamp. |  | Boolean |
| **CamelAwsStepFunctionsExecutionMaxResults** (producer) Constant: [`EXECUTIONS_MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-step-functions/latest/org/apache/camel/component/aws2/stepfunctions/StepFunctions2Constants.html#EXECUTIONS_MAX_RESULTS) | The limit number of results while listing executions. |  | Integer |

Required Step Functions component options

You have to provide the awsSfnClient in the Registry or your accessKey and secretKey to access the [AWS Step Functions](https://aws.amazon.com/step-functions/) service.

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

### Step Functions Producer operations

Camel-AWS Step Functions component provides the following operation on the producer side:

-   createStateMachine
    
-   deleteStateMachine
    
-   updateStateMachine
    
-   describeStateMachine
    
-   listStateMachines
    
-   createActivity
    
-   deleteActivity
    
-   describeActivity
    
-   getActivityTask
    
-   listActivities
    
-   startExecution
    
-   startSyncExecution
    
-   stopExecution
    
-   describeExecution
    
-   listExecutions
    
-   getExecutionHistory
    

## Examples

### Producer Examples

-   createStateMachine: this operation will create a state machine
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:createStateMachine")
    .to("aws2-step-functions://test?awsSfnClient=#awsSfnClient&operation=createMachine");
```

```xml
<route>
  <from uri="direct:createStateMachine"/>
  <to uri="aws2-step-functions://test?awsSfnClient=#awsSfnClient&amp;operation=createMachine"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:createStateMachine
      steps:
        - to:
            uri: aws2-step-functions://test
            parameters:
              awsSfnClient: "#awsSfnClient"
              operation: createMachine
```

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as the body. In AWS Step Functions, there are multiple operations you can submit, as an example for Create state machine request, you can do something like:

_Java-only: using a POJO request body with the AWS SDK builder_

```java
from("direct:start")
  .setBody(CreateStateMachineRequest.builder().name("state-machine").build())
  .to("aws2-step-functions://test?awsSfnClient=#awsSfnClient&operation=createStateMachine&pojoRequest=true")
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-step-functions</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.