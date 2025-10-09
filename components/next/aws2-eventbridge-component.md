# AWS Eventbridge

**Since Camel 3.6**

**Both producer and consumer are supported**

The AWS2 Eventbridge component supports assumeRole operation. [AWS Eventbridge](https://aws.amazon.com/eventbridge/).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Eventbridge. More information is available at [Amazon Eventbridge](https://aws.amazon.com/eventbridge/).

> **Note**
> To create a rule that triggers on an action by an AWS service that does not emit events, you can base the rule on API calls made by that service. The API calls are recorded by AWS CloudTrail, so you’ll need to have CloudTrail enabled. For more information, check [Services Supported by CloudTrail Event History](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.md).

## URI Format

aws2-eventbridge://label\[?options\]

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

The AWS Eventbridge component supports 31 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | Component configuration. |  | EventbridgeConfiguration |
| **eventPatternFile** (common) | EventPattern File. |  | String |
| **operation** (common) | 
**Required** The operation to perform.

Enum values:

-   putRule
    
-   putTargets
    
-   removeTargets
    
-   deleteRule
    
-   enableRule
    
-   disableRule
    
-   describeRule
    
-   listRules
    
-   listTargetsByRule
    
-   listRuleNamesByTarget
    
-   putEvent
    





 | putRule | EventbridgeOperations |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (common) | 

The region in which the Eventbridge client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autoCreateQueue** (consumer) | Whether to auto-create an SQS queue and wire it as an EventBridge rule target. | true | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **deleteQueueOnShutdown** (consumer) | Whether to delete the auto-created SQS queue and remove the EventBridge target on shutdown. | true | boolean |
| **maxMessagesPerPoll** (consumer) | The maximum number of messages to receive per poll from SQS. | 10 | int |
| **queueUrl** (consumer) | The URL of an existing SQS queue to use as EventBridge target. If not specified, a queue is auto-created when autoCreateQueue is true. |  | String |
| **ruleName** (consumer) | The EventBridge rule name to consume events from. Required for consumer. |  | String |
| **visibilityTimeout** (consumer) | The duration (in seconds) that received SQS messages are hidden from subsequent receive requests. | 30 | int |
| **waitTimeSeconds** (consumer) | The duration (in seconds) for which the SQS receive call waits for messages (long polling). | 20 | int |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **eventbridgeClient** (advanced) | **Autowired** To use an existing configured AWS Eventbridge client. |  | EventBridgeClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Eventbridge client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Eventbridge client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Eventbridge client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Eventbridge client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Eventbridge client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Eventbridge client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Eventbridge. | false | boolean |

## Endpoint Options

The AWS Eventbridge endpoint is configured using URI syntax:

aws2-eventbridge://eventbusNameOrArn

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **eventbusNameOrArn** (common) | **Required** Event bus name or ARN. |  | String |

### Query Parameters (45 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **eventPatternFile** (common) | EventPattern File. |  | String |
| **operation** (common) | 
**Required** The operation to perform.

Enum values:

-   putRule
    
-   putTargets
    
-   removeTargets
    
-   deleteRule
    
-   enableRule
    
-   disableRule
    
-   describeRule
    
-   listRules
    
-   listTargetsByRule
    
-   listRuleNamesByTarget
    
-   putEvent
    





 | putRule | EventbridgeOperations |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **region** (common) | 

The region in which the Eventbridge client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autoCreateQueue** (consumer) | Whether to auto-create an SQS queue and wire it as an EventBridge rule target. | true | boolean |
| **deleteQueueOnShutdown** (consumer) | Whether to delete the auto-created SQS queue and remove the EventBridge target on shutdown. | true | boolean |
| **maxMessagesPerPoll** (consumer) | The maximum number of messages to receive per poll from SQS. | 10 | int |
| **queueUrl** (consumer) | The URL of an existing SQS queue to use as EventBridge target. If not specified, a queue is auto-created when autoCreateQueue is true. |  | String |
| **ruleName** (consumer) | The EventBridge rule name to consume events from. Required for consumer. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **visibilityTimeout** (consumer) | The duration (in seconds) that received SQS messages are hidden from subsequent receive requests. | 30 | int |
| **waitTimeSeconds** (consumer) | The duration (in seconds) for which the SQS receive call waits for messages (long polling). | 20 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **eventbridgeClient** (advanced) | **Autowired** To use an existing configured AWS Eventbridge client. |  | EventBridgeClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Eventbridge client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Eventbridge client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Eventbridge client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Eventbridge client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Eventbridge client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Eventbridge client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Eventbridge. | false | boolean |

## Message Headers

The AWS Eventbridge component supports 17 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsEventbridgeOperation** (common) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsEventbridgeRuleName** (common) Constant: [`RULE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#RULE_NAME) | The name of the rule. |  | String |
| **CamelAwsEventbridgeRuleNamePrefix** (common) Constant: [`RULE_NAME_PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#RULE_NAME_PREFIX) | The prefix matching the rule name. |  | String |
| **CamelAwsEventbridgeEventPattern** (common) Constant: [`EVENT_PATTERN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#EVENT_PATTERN) | The event pattern. |  | String |
| **CamelAwsEventbridgeTargets** (common) Constant: [`TARGETS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#TARGETS) | The targets to update or add to the rule. |  | Collection |
| **CamelAwsEventbridgeTargetsIds** (common) Constant: [`TARGETS_IDS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#TARGETS_IDS) | The IDs of the targets to remove from the rule. |  | Collection |
| **CamelAwsEventbridgeTargetArn** (common) Constant: [`TARGET_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#TARGET_ARN) | The Amazon Resource Name (ARN) of the target resource. |  | String |
| **CamelAwsEventbridgeResourcesArn** (common) Constant: [`EVENT_RESOURCES_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#EVENT_RESOURCES_ARN) | Comma separated list of Amazon Resource Names (ARN) of the resources related to Event. |  | String |
| **CamelAwsEventbridgeSource** (common) Constant: [`EVENT_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#EVENT_SOURCE) | The source related to Event. |  | String |
| **CamelAwsEventbridgeDetailType** (common) Constant: [`EVENT_DETAIL_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#EVENT_DETAIL_TYPE) | The detail type related to Event. |  | String |
| **CamelAwsEventbridgeNextToken** (listRules listTargetsByRule listRuleNamesByTarget) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#NEXT_TOKEN) | The token for the next set of results. |  | String |
| **CamelAwsEventbridgeLimit** (listRules listTargetsByRule listRuleNamesByTarget) Constant: [`LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#LIMIT) | The maximum number of results to return. |  | Integer |
| **CamelAwsEventbridgeIsTruncated** (listRules listTargetsByRule listRuleNamesByTarget) Constant: [`IS_TRUNCATED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#IS_TRUNCATED) | Whether the response has more results (is truncated). |  | Boolean |
| **CamelAwsEventbridgeRuleArn** (putRule describeRule) Constant: [`RULE_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#RULE_ARN) | The Amazon Resource Name (ARN) of the rule. |  | String |
| **CamelAwsEventbridgeFailedEntryCount** (putEvent putTargets removeTargets) Constant: [`FAILED_ENTRY_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#FAILED_ENTRY_COUNT) | The number of failed entries in the response. |  | Integer |
| **CamelAwsEventbridgeMessageId** (consumer) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#MESSAGE_ID) | The SQS message ID. |  | String |
| **CamelAwsEventbridgeReceiptHandle** (consumer) Constant: [`RECEIPT_HANDLE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-eventbridge/latest/org/apache/camel/component/aws2/eventbridge/EventbridgeConstants.html#RECEIPT_HANDLE) | The SQS receipt handle for message deletion. |  | String |

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

### AWS2-Eventbridge Producer operations

Camel-AWS2-Eventbridge component provides the following operation on the producer side:

-   putRule
    
-   putTargets
    
-   removeTargets
    
-   deleteRule
    
-   enableRule
    
-   disableRule
    
-   listRules
    
-   describeRule
    
-   listTargetsByRule
    
-   listRuleNamesByTarget
    
-   putEvent
    
-   PutRule: this operation creates a rule related to an eventbus
    

```java
  from("direct:putRule").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=putRule&eventPatternFile=file:src/test/resources/eventpattern.json")
  .to("mock:result");
```

This operation will create a rule named _firstrule_, and it will use a json file for defining the EventPattern.

-   PutTargets: this operation will add a target to the rule
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
          Target target = Target.builder().id("sqs-queue").arn("arn:aws:sqs:eu-west-1:780410022472:camel-connector-test")
                .build();
          List<Target> targets = new ArrayList<Target>();
          targets.add(target);
          exchange.getIn().setHeader(EventbridgeConstants.TARGETS, targets);
      }
  })
  .to("aws2-eventbridge://test?operation=putTargets")
  .to("mock:result");
```

This operation will add the target sqs-queue with the arn reported to the targets of the _firstrule_ rule.

-   RemoveTargets: this operation will remove a collection of targets from the rule
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
          List<String> ids = new ArrayList<String>();
          targets.add("sqs-queue");
          exchange.getIn().setHeader(EventbridgeConstants.TARGETS_IDS, targets);
      }
  })
  .to("aws2-eventbridge://test?operation=removeTargets")
  .to("mock:result");
```

This operation will remove the target sqs-queue from the _firstrule_ rule.

-   DeleteRule: this operation will delete a rule related to an eventbus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=deleteRule")
  .to("mock:result");
```

This operation will remove the _firstrule_ rule from the test eventbus.

-   EnableRule: this operation will enable a rule related to an eventbus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=enableRule")
  .to("mock:result");
```

This operation will enable the _firstrule_ rule from the test eventbus.

-   DisableRule: this operation will disable a rule related to an eventbus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=disableRule")
  .to("mock:result");
```

This operation will disable the _firstrule_ rule from the test eventbus.

-   ListRules: this operation will list all the rules related to an eventbus with prefix first
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME_PREFIX, "first");
      }
  })
  .to("aws2-eventbridge://test?operation=listRules")
  .to("mock:result");
```

This operation will list all the rules with prefix first from the test eventbus.

-   DescribeRule: this operation will describe a specified rule related to an eventbus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=describeRule")
  .to("mock:result");
```

This operation will describe the _firstrule_ rule from the test eventbus.

-   ListTargetsByRule: this operation will return a list of targets associated with a rule
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.RULE_NAME, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=listTargetsByRule")
  .to("mock:result");
```

this operation will return a list of targets associated with the _firstrule_ rule.

-   ListRuleNamesByTarget: this operation will return a list of rules associated with a target
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(EventbridgeConstants.TARGET_ARN, "firstrule");
      }
  })
  .to("aws2-eventbridge://test?operation=listRuleNamesByTarget")
  .to("mock:result");
```

this operation will return a list of rules associated with a target.

-   PutEvent: this operation will send an event to the Servicebus
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
                exchange.getIn().setHeader(EventbridgeConstants.EVENT_RESOURCES_ARN, "arn:aws:sqs:eu-west-1:780410022472:camel-connector-test");
                exchange.getIn().setHeader(EventbridgeConstants.EVENT_SOURCE, "com.pippo");
                exchange.getIn().setHeader(EventbridgeConstants.EVENT_DETAIL_TYPE, "peppe");
                exchange.getIn().setBody("Test Event");
      }
  })
  .to("aws2-eventbridge://test?operation=putEvent")
  .to("mock:result");
```

this operation will return a list of entries with related ID sent to servicebus.

### Updating the rule

To update a rule, you’ll need to perform the putRule operation again. There is no explicit update rule operation in the Java SDK.

## Consuming Events from EventBridge

Since Camel 4.19, the component supports consuming events from EventBridge rules using an SQS-backed polling pattern.

AWS EventBridge is an event router, not a message queue — it does not provide a pull-based API. The consumer works by wiring an SQS queue as a target of the specified EventBridge rule and then polling that queue for events. This is the standard AWS pattern for programmatically consuming EventBridge events.

### How It Works

1.  On startup the consumer creates an SQS queue (unless you provide one via `queueUrl`).
    
2.  It sets an SQS queue policy that allows EventBridge to send messages.
    
3.  It adds the queue as a target of the EventBridge rule specified by `ruleName`.
    
4.  It polls the SQS queue on schedule, delivering each event into the Camel route.
    
5.  Successfully processed messages are deleted from the queue; failed messages remain for retry.
    
6.  On shutdown the target is removed and the auto-created queue is deleted (configurable).
    

### Consumer Configuration Options

   
| Option | Default | Type | Description |
| --- | --- | --- | --- |
| `ruleName` |  | String | **Required.** The EventBridge rule name to consume events from. |
| `queueUrl` |  | String | URL of an existing SQS queue to use. If omitted, a queue is auto-created. |
| `autoCreateQueue` | `true` | boolean | Whether to auto-create an SQS queue and wire it as the rule target. |
| `deleteQueueOnShutdown` | `true` | boolean | Whether to delete the auto-created queue and remove the EventBridge target on shutdown. |
| `maxMessagesPerPoll` | `10` | int | Maximum number of SQS messages to receive per poll cycle. |
| `waitTimeSeconds` | `20` | int | SQS long-polling wait time in seconds. |
| `visibilityTimeout` | `30` | int | Seconds that received messages are hidden from subsequent polls. |

Standard `ScheduledPollConsumer` options (`delay`, `initialDelay`, `greedy`, etc.) are also available.

### Consumer Example — Auto-Created Queue

```java
from("aws2-eventbridge://default?ruleName=my-rule&delay=5000")
    .log("Received EventBridge event: ${body}")
    .to("direct:process");
```

The consumer auto-creates an SQS queue, wires it to the `my-rule` EventBridge rule, and polls every 5 seconds.

### Consumer Example — User-Provided Queue

```java
from("aws2-eventbridge://default?ruleName=my-rule"
     + "&autoCreateQueue=false"
     + "&queueUrl=https://sqs.us-east-1.amazonaws.com/123456789012/my-queue")
    .log("Received: ${body}")
    .to("direct:process");
```

Use this when you manage the SQS queue and its policy yourself.

### Consumer Example — Combined Producer and Consumer

```java
// First create the rule
from("direct:setup")
    .to("aws2-eventbridge://default?operation=putRule"
        + "&eventPatternFile=file:eventpattern.json");

// Consume events matching the rule
from("aws2-eventbridge://default?ruleName=my-rule&delay=2000")
    .log("Event: ${body}")
    .to("mock:events");
```

### IAM Permissions

The consumer’s IAM principal needs the following permissions:

-   `events:PutTargets` and `events:RemoveTargets` on the EventBridge rule
    
-   `sqs:CreateQueue`, `sqs:DeleteQueue`, `sqs:SetQueueAttributes`, `sqs:GetQueueAttributes` (if auto-creating)
    
-   `sqs:ReceiveMessage`, `sqs:DeleteMessage` on the SQS queue
    

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-eventbridge</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-eventbridge with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-eventbridge-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 32 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-eventbridge.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-eventbridge.auto-create-queue** | Whether to auto-create an SQS queue and wire it as an EventBridge rule target. | true | Boolean |
| **camel.component.aws2-eventbridge.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-eventbridge.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws2-eventbridge.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.eventbridge.EventbridgeConfiguration type. |  | EventbridgeConfiguration |
| **camel.component.aws2-eventbridge.delete-queue-on-shutdown** | Whether to delete the auto-created SQS queue and remove the EventBridge target on shutdown. | true | Boolean |
| **camel.component.aws2-eventbridge.enabled** | Whether to enable auto configuration of the aws2-eventbridge component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-eventbridge.event-pattern-file** | EventPattern File. |  | String |
| **camel.component.aws2-eventbridge.eventbridge-client** | To use an existing configured AWS Eventbridge client. The option is a software.amazon.awssdk.services.eventbridge.EventBridgeClient type. |  | EventBridgeClient |
| **camel.component.aws2-eventbridge.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws2-eventbridge.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws2-eventbridge.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-eventbridge.max-messages-per-poll** | The maximum number of messages to receive per poll from SQS. | 10 | Integer |
| **camel.component.aws2-eventbridge.operation** | The operation to perform. | putrule | EventbridgeOperations |
| **camel.component.aws2-eventbridge.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-eventbridge.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-eventbridge.profile-credentials-name** | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **camel.component.aws2-eventbridge.proxy-host** | To define a proxy host when instantiating the Eventbridge client. |  | String |
| **camel.component.aws2-eventbridge.proxy-port** | To define a proxy port when instantiating the Eventbridge client. |  | Integer |
| **camel.component.aws2-eventbridge.proxy-protocol** | To define a proxy protocol when instantiating the Eventbridge client. | https | Protocol |
| **camel.component.aws2-eventbridge.queue-url** | The URL of an existing SQS queue to use as EventBridge target. If not specified, a queue is auto-created when autoCreateQueue is true. |  | String |
| **camel.component.aws2-eventbridge.region** | The region in which the Eventbridge client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-eventbridge.rule-name** | The EventBridge rule name to consume events from. Required for consumer. |  | String |
| **camel.component.aws2-eventbridge.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-eventbridge.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws2-eventbridge.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-eventbridge.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-eventbridge.use-default-credentials-provider** | Set whether the Eventbridge client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-eventbridge.use-profile-credentials-provider** | Set whether the Eventbridge client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-eventbridge.use-session-credentials** | Set whether the Eventbridge client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Eventbridge. | false | Boolean |
| **camel.component.aws2-eventbridge.visibility-timeout** | The duration (in seconds) that received SQS messages are hidden from subsequent receive requests. | 30 | Integer |
| **camel.component.aws2-eventbridge.wait-time-seconds** | The duration (in seconds) for which the SQS receive call waits for messages (long polling). | 20 | Integer |