# AWS Simple Queue Service (SQS)

**Since Camel 3.1**

**Both producer and consumer are supported**

The AWS2 SQS component supports sending and receiving messages to [Amazon’s SQS](https://aws.amazon.com/sqs) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon SQS. More information is available at [Amazon SQS](https://aws.amazon.com/sqs).

## URI Format

aws2-sqs://queueNameOrArn\[?options\]

The queue will be created if they don’t already exist.

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

The AWS Simple Queue Service (SQS) component supports 52 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonAWSHost** (common) | The hostname of the Amazon AWS cloud. | amazonaws.com | String |
| **autoCreateQueue** (common) | Setting the auto-creation of the queue. | false | boolean |
| **configuration** (common) | The AWS SQS default configuration. |  | Sqs2Configuration |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **protocol** (common) | The underlying protocol used to communicate with SQS. | https | String |
| **queueOwnerAWSAccountId** (common) | Specify the queue owner aws account id when you need to connect the queue with a different account owner. |  | String |
| **region** (common) | 
The region in which SQS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **attributeNames** (consumer) | A list of attribute names to receive when consuming. Multiple names can be separated by comma. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **concurrentConsumers** (consumer) | Allows you to use multiple threads to poll the sqs queue to increase throughput. | 1 | int |
| **concurrentRequestLimit** (consumer) | The maximum number of concurrent receive request send to AWS in single consumer polling. | 50 | int |
| **defaultVisibilityTimeout** (consumer) | The default visibility timeout (in seconds). |  | Integer |
| **deleteAfterRead** (consumer) | Delete message from SQS after it has been read. | true | boolean |
| **deleteIfFiltered** (consumer) | Whether to send the DeleteMessage to the SQS queue if the exchange has property with key Sqs2Constants#SQS\_DELETE\_FILTERED (CamelAwsSqsDeleteFiltered) set to true. | true | boolean |
| **extendMessageVisibility** (consumer) | If enabled, then a scheduled background task will keep extending the message visibility on SQS. This is needed if it takes a long time to process the message. If set to true defaultVisibilityTimeout must be set. See details at Amazon docs. | false | boolean |
| **kmsDataKeyReusePeriodSeconds** (consumer) | The length of time, in seconds, for which Amazon SQS can reuse a data key to encrypt or decrypt messages before calling AWS KMS again. An integer representing seconds, between 60 seconds (1 minute) and 86,400 seconds (24 hours). Default: 300 (5 minutes). |  | Integer |
| **kmsMasterKeyId** (consumer) | The ID of an AWS-managed customer master key (CMK) for Amazon SQS or a custom CMK. |  | String |
| **messageAttributeNames** (consumer) | A list of message attribute names to receive when consuming. Multiple names can be separated by comma. |  | String |
| **serverSideEncryptionEnabled** (consumer) | Define if Server Side Encryption is enabled or not on the queue. | false | boolean |
| **sortAttributeName** (consumer) | The name of the message attribute used for sorting the messages. When specified, the messages polled by the consumer will be sorted by this attribute. This configuration may be of importance when you configure maxMessagesPerPoll parameter exceeding 10. In such cases, the messages will be fetched concurrently so the ordering is not guaranteed. |  | String |
| **visibilityTimeout** (consumer) | The duration (in seconds) that the received messages are hidden from subsequent retrieve requests after being retrieved by a ReceiveMessage request to set in the com.amazonaws.services.sqs.model.SetQueueAttributesRequest. This only makes sense if it’s different from defaultVisibilityTimeout. It changes the queue visibility timeout attribute permanently. |  | Integer |
| **waitTimeSeconds** (consumer) | Duration in seconds (0 to 20) that the ReceiveMessage action call will wait until a message is in the queue to include in the response. |  | Integer |
| **batchSeparator** (producer) | Set the separator when passing a String to send batch message operation. | , | String |
| **delaySeconds** (producer) | Delay sending messages for a number of seconds. |  | Integer |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **messageDeduplicationIdStrategy** (producer) | 

Only for FIFO queues. Strategy for setting the messageDeduplicationId on the message. It can be one of the following options: useExchangeId, useContentBasedDeduplication. For the useContentBasedDeduplication option, no messageDeduplicationId will be set on the message.

Enum values:

-   useExchangeId
    
-   useContentBasedDeduplication
    





 | useExchangeId | String |
| **messageGroupIdStrategy** (producer) | 

Only for FIFO queues. Strategy for setting the messageGroupId on the message. It can be one of the following options: useConstant, useExchangeId, usePropertyValue. For the usePropertyValue option, the value of property CamelAwsMessageGroupId will be used.

Enum values:

-   useConstant
    
-   useExchangeId
    
-   usePropertyValue
    





 |  | String |
| **messageHeaderExceededLimit** (producer) | 

What to do if sending to AWS SQS has more messages than AWS allows (currently only maximum 10 message headers are allowed). WARN will log a WARN about the limit is for each additional header, so the message can be sent to AWS. WARN\_ONCE will only log one time a WARN about the limit is hit, and drop additional headers, so the message can be sent to AWS. IGNORE will ignore (no logging) and drop additional headers, so the message can be sent to AWS. FAIL will cause an exception to be thrown and the message is not sent to AWS.

Enum values:

-   WARN
    
-   WARN\_ONCE
    
-   IGNORE
    
-   FAIL
    





 | WARN | String |
| **operation** (producer) | 

The operation to do in case the user don’t want to send only a message.

Enum values:

-   sendBatchMessage
    
-   deleteMessage
    
-   listQueues
    
-   purgeQueue
    
-   deleteQueue
    





 |  | Sqs2Operations |
| **amazonSQSClient** (advanced) | **Autowired** To use the AmazonSQS client. |  | SqsClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **delayQueue** (advanced) | Define if you want to apply delaySeconds option to the queue or on single messages. | false | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SQS client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the SQS client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the SQS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **maximumMessageSize** (queue) | The maximumMessageSize (in bytes) an SQS message can contain for this queue. |  | Integer |
| **messageRetentionPeriod** (queue) | The messageRetentionPeriod (in seconds) a message will be retained by SQS for this queue. |  | Integer |
| **policy** (queue) | The policy for this queue. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **queueUrl** (queue) | To define the queueUrl explicitly. All other parameters, which would influence the queueUrl, are ignored. This parameter is intended to be used to connect to a mock implementation of SQS, for testing purposes. |  | String |
| **receiveMessageWaitTimeSeconds** (queue) | If you do not specify WaitTimeSeconds in the request, the queue attribute ReceiveMessageWaitTimeSeconds is used to determine how long to wait. |  | Integer |
| **redrivePolicy** (queue) | Specify the policy that send message to DeadLetter queue. See detail at Amazon docs. |  | String |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the SQS client should expect to load credentials on an AWS infra instance or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the SQS client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the SQS client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in SQS. | false | boolean |

## Endpoint Options

The AWS Simple Queue Service (SQS) endpoint is configured using URI syntax:

aws2-sqs:queueNameOrArn

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **queueNameOrArn** (common) | **Required** Queue name or ARN. |  | String |

### Query Parameters (68 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonAWSHost** (common) | The hostname of the Amazon AWS cloud. | amazonaws.com | String |
| **autoCreateQueue** (common) | Setting the auto-creation of the queue. | false | boolean |
| **headerFilterStrategy** (common) | To use a custom HeaderFilterStrategy to map headers to/from Camel. |  | HeaderFilterStrategy |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **protocol** (common) | The underlying protocol used to communicate with SQS. | https | String |
| **queueOwnerAWSAccountId** (common) | Specify the queue owner aws account id when you need to connect the queue with a different account owner. |  | String |
| **region** (common) | 
The region in which SQS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **attributeNames** (consumer) | A list of attribute names to receive when consuming. Multiple names can be separated by comma. |  | String |
| **concurrentConsumers** (consumer) | Allows you to use multiple threads to poll the sqs queue to increase throughput. | 1 | int |
| **concurrentRequestLimit** (consumer) | The maximum number of concurrent receive request send to AWS in single consumer polling. | 50 | int |
| **defaultVisibilityTimeout** (consumer) | The default visibility timeout (in seconds). |  | Integer |
| **deleteAfterRead** (consumer) | Delete message from SQS after it has been read. | true | boolean |
| **deleteIfFiltered** (consumer) | Whether to send the DeleteMessage to the SQS queue if the exchange has property with key Sqs2Constants#SQS\_DELETE\_FILTERED (CamelAwsSqsDeleteFiltered) set to true. | true | boolean |
| **extendMessageVisibility** (consumer) | If enabled, then a scheduled background task will keep extending the message visibility on SQS. This is needed if it takes a long time to process the message. If set to true defaultVisibilityTimeout must be set. See details at Amazon docs. | false | boolean |
| **kmsDataKeyReusePeriodSeconds** (consumer) | The length of time, in seconds, for which Amazon SQS can reuse a data key to encrypt or decrypt messages before calling AWS KMS again. An integer representing seconds, between 60 seconds (1 minute) and 86,400 seconds (24 hours). Default: 300 (5 minutes). |  | Integer |
| **kmsMasterKeyId** (consumer) | The ID of an AWS-managed customer master key (CMK) for Amazon SQS or a custom CMK. |  | String |
| **maxMessagesPerPoll** (consumer) | Gets the maximum number of messages as a limit to poll at each polling. Is default unlimited, but use 0 or negative number to disable it as unlimited. |  | int |
| **messageAttributeNames** (consumer) | A list of message attribute names to receive when consuming. Multiple names can be separated by comma. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **serverSideEncryptionEnabled** (consumer) | Define if Server Side Encryption is enabled or not on the queue. | false | boolean |
| **sortAttributeName** (consumer) | The name of the message attribute used for sorting the messages. When specified, the messages polled by the consumer will be sorted by this attribute. This configuration may be of importance when you configure maxMessagesPerPoll parameter exceeding 10. In such cases, the messages will be fetched concurrently so the ordering is not guaranteed. |  | String |
| **visibilityTimeout** (consumer) | The duration (in seconds) that the received messages are hidden from subsequent retrieve requests after being retrieved by a ReceiveMessage request to set in the com.amazonaws.services.sqs.model.SetQueueAttributesRequest. This only makes sense if it’s different from defaultVisibilityTimeout. It changes the queue visibility timeout attribute permanently. |  | Integer |
| **waitTimeSeconds** (consumer) | Duration in seconds (0 to 20) that the ReceiveMessage action call will wait until a message is in the queue to include in the response. |  | Integer |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **batchSeparator** (producer) | Set the separator when passing a String to send batch message operation. | , | String |
| **delaySeconds** (producer) | Delay sending messages for a number of seconds. |  | Integer |
| **messageDeduplicationIdStrategy** (producer) | 

Only for FIFO queues. Strategy for setting the messageDeduplicationId on the message. It can be one of the following options: useExchangeId, useContentBasedDeduplication. For the useContentBasedDeduplication option, no messageDeduplicationId will be set on the message.

Enum values:

-   useExchangeId
    
-   useContentBasedDeduplication
    





 | useExchangeId | String |
| **messageGroupIdStrategy** (producer) | 

Only for FIFO queues. Strategy for setting the messageGroupId on the message. It can be one of the following options: useConstant, useExchangeId, usePropertyValue. For the usePropertyValue option, the value of property CamelAwsMessageGroupId will be used.

Enum values:

-   useConstant
    
-   useExchangeId
    
-   usePropertyValue
    





 |  | String |
| **messageHeaderExceededLimit** (producer) | 

What to do if sending to AWS SQS has more messages than AWS allows (currently only maximum 10 message headers are allowed). WARN will log a WARN about the limit is for each additional header, so the message can be sent to AWS. WARN\_ONCE will only log one time a WARN about the limit is hit, and drop additional headers, so the message can be sent to AWS. IGNORE will ignore (no logging) and drop additional headers, so the message can be sent to AWS. FAIL will cause an exception to be thrown and the message is not sent to AWS.

Enum values:

-   WARN
    
-   WARN\_ONCE
    
-   IGNORE
    
-   FAIL
    





 | WARN | String |
| **operation** (producer) | 

The operation to do in case the user don’t want to send only a message.

Enum values:

-   sendBatchMessage
    
-   deleteMessage
    
-   listQueues
    
-   purgeQueue
    
-   deleteQueue
    





 |  | Sqs2Operations |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **amazonSQSClient** (advanced) | **Autowired** To use the AmazonSQS client. |  | SqsClient |
| **delayQueue** (advanced) | Define if you want to apply delaySeconds option to the queue or on single messages. | false | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SQS client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the SQS client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the SQS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **maximumMessageSize** (queue) | The maximumMessageSize (in bytes) an SQS message can contain for this queue. |  | Integer |
| **messageRetentionPeriod** (queue) | The messageRetentionPeriod (in seconds) a message will be retained by SQS for this queue. |  | Integer |
| **policy** (queue) | The policy for this queue. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **queueUrl** (queue) | To define the queueUrl explicitly. All other parameters, which would influence the queueUrl, are ignored. This parameter is intended to be used to connect to a mock implementation of SQS, for testing purposes. |  | String |
| **receiveMessageWaitTimeSeconds** (queue) | If you do not specify WaitTimeSeconds in the request, the queue attribute ReceiveMessageWaitTimeSeconds is used to determine how long to wait. |  | Integer |
| **redrivePolicy** (queue) | Specify the policy that send message to DeadLetter queue. See detail at Amazon docs. |  | String |
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
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the SQS client should expect to load credentials on an AWS infra instance or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the SQS client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the SQS client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in SQS. | false | boolean |

## Message Headers

The AWS Simple Queue Service (SQS) component supports 14 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsSqsAttributes** (consumer) Constant: [`ATTRIBUTES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#ATTRIBUTES) | A map of the attributes requested in ReceiveMessage to their respective values. |  | Map |
| **CamelAwsSqsMessageAttributes** (consumer) Constant: [`MESSAGE_ATTRIBUTES`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#MESSAGE_ATTRIBUTES) | The Amazon SQS message attributes. |  | Map |
| **CamelAwsSqsMD5OfBody** (common) Constant: [`MD5_OF_BODY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#MD5_OF_BODY) | The MD5 checksum of the Amazon SQS message. |  | String |
| **CamelAwsSqsMessageId** (common) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#MESSAGE_ID) | The Amazon SQS message ID. |  | String |
| **CamelAwsSqsReceiptHandle** (common) Constant: [`RECEIPT_HANDLE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#RECEIPT_HANDLE) | The Amazon SQS message receipt handle. |  | String |
| **CamelAwsSqsDelaySeconds** (producer) Constant: [`DELAY_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#DELAY_HEADER) | The delay seconds that the Amazon SQS message can be see by others. |  | Integer |
| **CamelAwsSqsPrefix** (common) Constant: [`SQS_QUEUE_PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#SQS_QUEUE_PREFIX) | A string to use for filtering the list results. |  | String |
| **CamelAwsSqsOperation** (common) Constant: [`SQS_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#SQS_OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsSqsNextToken** (listQueues) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#NEXT_TOKEN) | The token for the next set of results. |  | String |
| **CamelAwsSqsMaxResults** (listQueues) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#MAX_RESULTS) | The maximum number of results to return. |  | Integer |
| **CamelAwsSqsIsTruncated** (listQueues) Constant: [`IS_TRUNCATED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#IS_TRUNCATED) | Whether the response has more results (is truncated). |  | Boolean |
| **CamelAwsSqsSequenceNumber** (producer) Constant: [`SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#SEQUENCE_NUMBER) | The sequence number for FIFO queues. |  | String |
| **CamelAwsSqsFailedMessageCount** (sendBatchMessage) Constant: [`FAILED_MESSAGE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#FAILED_MESSAGE_COUNT) | The number of failed messages in a batch send operation. |  | Integer |
| **CamelAwsSqsSuccessfulMessageCount** (sendBatchMessage) Constant: [`SUCCESSFUL_MESSAGE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sqs/latest/org/apache/camel/component/aws2/sqs/Sqs2Constants.html#SUCCESSFUL_MESSAGE_COUNT) | The number of successful messages in a batch send operation. |  | Integer |

Required SQS component options

You have to provide the amazonSQSClient in the Registry or your accessKey and secretKey to access the [Amazon’s SQS](https://aws.amazon.com/sqs).

## Usage

### Batch Consumer

This component implements the Batch Consumer.

This allows you, for instance, to know how many messages exist in this batch and for instance, let the Aggregator aggregate this number of messages.

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

## Examples

### Advanced AmazonSQS configuration

If your Camel Application is running behind a firewall or if you need to have more control over the SqsClient instance configuration, you can create your own instance, and configure Camel to use your instance by the bean id.

In the example below, we use _myClient_ as the bean id:

_Java-only: programmatic `SqsClient` creation and registry binding_

```java
// create my own instance of SqsClient
SqsClient sqs = ...

// register the client into Camel registry
camelContext.getRegistry().bind("myClient", sqs);

// refer to the custom client via myClient as the bean id
from("aws2-sqs://MyQueue?amazonSQSClient=#myClient&delay=5000&maxMessagesPerPoll=5")
.to("mock:result");
```

### DelayQueue VS Delay for Single message

When the option delayQueue is set to true, the SQS Queue will be a DelayQueue with the DelaySeconds option as delay. For more information about DelayQueue you can read the [AWS SQS documentation](https://docs.aws.amazon.com/en_us/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-delay-queues.md). One important information to take into account is the following:

-   For standard queues, the per-queue delay setting is not retroactively—changing the setting doesn’t affect the delay of messages already in the queue.
    
-   For FIFO queues, the per-queue delay setting is retroactively—changing the setting affects the delay of messages already in the queue.
    

as stated in the official documentation. If you want to specify a delay on single messages, you can ignore the delayQueue option, while you can set this option to true if you need to add a fixed delay to all messages enqueued.

### Server Side Encryption

There is a set of Server Side Encryption attributes for a queue. The related option are: `serverSideEncryptionEnabled`, `keyMasterKeyId` and `kmsDataKeyReusePeriod`. The SSE is disabled by default. You need to explicitly set the option to true and set the related parameters as queue attributes.

### JMS-style Selectors

SQS does not allow selectors, but you can effectively achieve this by using the Camel Filter EIP and setting an appropriate `visibilityTimeout`. When SQS dispatches a message, it will wait up to the visibility timeout before it tries to dispatch the message to a different consumer unless a DeleteMessage is received. By default, Camel will always send the DeleteMessage at the end of the route, unless the route ended in failure. To achieve appropriate filtering and not send the DeleteMessage even on successful completion of the route, use a Filter:

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws2-sqs://MyQueue?amazonSQSClient=#client&defaultVisibilityTimeout=5000&deleteIfFiltered=false&deleteAfterRead=false")
.filter("${header.login} == true")
  .setProperty("CamelAwsSqsDeleteFiltered", constant(true))
  .to("mock:filter");
```

```xml
<route>
  <from uri="aws2-sqs://MyQueue?amazonSQSClient=#client&amp;defaultVisibilityTimeout=5000&amp;deleteIfFiltered=false&amp;deleteAfterRead=false"/>
  <filter>
    <simple>${header.login} == true</simple>
    <setProperty name="CamelAwsSqsDeleteFiltered">
      <constant>true</constant>
    </setProperty>
    <to uri="mock:filter"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: aws2-sqs://MyQueue
      parameters:
        amazonSQSClient: "#client"
        defaultVisibilityTimeout: 5000
        deleteIfFiltered: false
        deleteAfterRead: false
      steps:
        - filter:
            simple: "${header.login} == true"
            steps:
              - setProperty:
                  name: CamelAwsSqsDeleteFiltered
                  constant: true
              - to:
                  uri: mock:filter
```

> **Tip**
> In Java code, you can use the constant `Sqs2Constants.SQS_DELETE_FILTERED` for the property name.

In the above code, if an exchange doesn’t have an appropriate header, it will not make it through the filter AND also not be deleted from the SQS queue. After 5000 milliseconds, the message will become visible to other consumers.

Note we must set the property `CamelAwsSqsDeleteFiltered` to `true` to instruct Camel to send the DeleteMessage, if being filtered.

### Available Producer Operations

-   single message (default)
    
-   sendBatchMessage
    
-   deleteMessage
    
-   listQueues
    

### Send Message

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("Camel rocks!"))
    .to("aws2-sqs://camel-1?accessKey=RAW(xxx)&secretKey=RAW(xxx)&region=eu-west-1");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <constant>Camel rocks!</constant>
  </setBody>
  <to uri="aws2-sqs://camel-1?accessKey=RAW(xxx)&amp;secretKey=RAW(xxx)&amp;region=eu-west-1"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            constant: "Camel rocks!"
        - to:
            uri: aws2-sqs://camel-1
            parameters:
              accessKey: RAW(xxx)
              secretKey: RAW(xxx)
              region: eu-west-1
```

### Send Batch Message

You can set a `SendMessageBatchRequest` or an `Iterable`

_Java-only: requires constructing a `List` body programmatically for batch messages_

```java
from("direct:start")
  .setHeader("CamelAwsSqsOperation", constant("sendBatchMessage"))
  .process(exchange -> {
      List<String> c = new ArrayList<>();
      c.add("team1");
      c.add("team2");
      c.add("team3");
      c.add("team4");
      exchange.getIn().setBody(c);
  })
  .to("aws2-sqs://camel-1?accessKey=RAW(xxx)&secretKey=RAW(xxx)&region=eu-west-1");
```

As result, you’ll get an exchange containing a `SendMessageBatchResponse` instance, that you can examine to check what messages were successful and what not. The id set on each message of the batch will be a Random UUID.

### Delete single Message

Use deleteMessage operation to delete a single message. You’ll need to set a receipt handle header for the message you want to delete.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAwsSqsOperation", constant("deleteMessage"))
    .setHeader("CamelAwsSqsReceiptHandle", constant("123456"))
    .to("aws2-sqs://camel-1?accessKey=RAW(xxx)&secretKey=RAW(xxx)&region=eu-west-1");
```

```xml
<route>
    <from uri="direct:start"/>
    <setHeader name="CamelAwsSqsOperation">
        <constant>deleteMessage</constant>
    </setHeader>
    <setHeader name="CamelAwsSqsReceiptHandle">
        <constant>123456</constant>
    </setHeader>
    <to uri="aws2-sqs://camel-1?accessKey=RAW(xxx)&amp;secretKey=RAW(xxx)&amp;region=eu-west-1"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
    steps:
      - setHeader:
          name: CamelAwsSqsOperation
          constant: deleteMessage
      - setHeader:
          name: CamelAwsSqsReceiptHandle
          constant: "123456"
      - to:
          uri: aws2-sqs://camel-1
          parameters:
            accessKey: RAW(xxx)
            secretKey: RAW(xxx)
            region: eu-west-1
```

As result, you’ll get an exchange containing a `DeleteMessageResponse` instance, that you can use to check if the message was deleted or not.

### List Queues

Use listQueues operation to list queues.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAwsSqsOperation", constant("listQueues"))
    .to("aws2-sqs://camel-1?accessKey=RAW(xxx)&secretKey=RAW(xxx)&region=eu-west-1");
```

```xml
<route>
    <from uri="direct:start"/>
    <setHeader name="CamelAwsSqsOperation">
        <constant>listQueues</constant>
    </setHeader>
    <to uri="aws2-sqs://camel-1?accessKey=RAW(xxx)&amp;secretKey=RAW(xxx)&amp;region=eu-west-1"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
    steps:
      - setHeader:
          name: CamelAwsSqsOperation
          constant: listQueues
      - to:
          uri: aws2-sqs://camel-1
          parameters:
            accessKey: RAW(xxx)
            secretKey: RAW(xxx)
            region: eu-west-1
```

As result, you’ll get an exchange containing a `ListQueuesResponse` instance, that you can examine to check the actual queues.

### Purge Queue

Use purgeQueue operation to purge queue.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAwsSqsOperation", constant("purgeQueue"))
    .to("aws2-sqs://camel-1?accessKey=RAW(xxx)&secretKey=RAW(xxx)&region=eu-west-1");
```

```xml
<route>
    <from uri="direct:start"/>
    <setHeader name="CamelAwsSqsOperation">
        <constant>purgeQueue</constant>
    </setHeader>
    <to uri="aws2-sqs://camel-1?accessKey=RAW(xxx)&amp;secretKey=RAW(xxx)&amp;region=eu-west-1"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
    steps:
      - setHeader:
          name: CamelAwsSqsOperation
          constant: purgeQueue
      - to:
          uri: aws2-sqs://camel-1
          parameters:
            accessKey: RAW(xxx)
            secretKey: RAW(xxx)
            region: eu-west-1
```

As result you’ll get an exchange containing a `PurgeQueueResponse` instance.

### Queue Auto-creation

With the option `autoCreateQueue` users are able to avoid the autocreation of an SQS Queue in case it doesn’t exist. The default for this option is `false`. If set to _false_, any operation on a non-existent queue in AWS won’t be successful and an error will be returned.

### Send Batch Message and Message Deduplication Strategy

In case you’re using a SendBatchMessage Operation, you can set two different kinds of Message Deduplication Strategy: - useExchangeId - useContentBasedDeduplication

The first one will use a ExchangeIdMessageDeduplicationIdStrategy, that will use the Exchange ID as parameter The other one will use a NullMessageDeduplicationIdStrategy, that will use the body as a deduplication element.

In case of send batch message operation, you’ll need to use the `useContentBasedDeduplication` and on the Queue you’re pointing you’ll need to enable the `content based deduplication` option.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-sqs</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.