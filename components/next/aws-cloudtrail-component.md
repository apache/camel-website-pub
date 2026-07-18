# AWS CloudTrail

**Since Camel 3.19**

**Only consumer is supported**

The AWS CloudTrail component supports receiving events from Amazon CloudTrail service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon CloudTrail. More information is available at [AWS CloudTrail](https://aws.amazon.com/cloudtrail/)

## URI Format

aws-cloudtrail://label\[?options\]

The stream needs to be created prior to it being used.

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

The AWS CloudTrail component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configuration** (consumer) | Component configuration. |  | CloudtrailConfiguration |
| **eventSource** (consumer) | Specify an event source to select events. |  | String |
| **maxResults** (consumer) | Maximum number of records that will be fetched in each lookup page. Each poll drains all pages, so this controls the page size rather than the total per poll. AWS allows up to 50. | 50 | int |
| **overrideEndpoint** (consumer) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **region** (consumer) | 
The region in which Cloudtrail client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (consumer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **cloudTrailClient** (advanced) | **Autowired** Amazon Cloudtrail client to use for all requests for this endpoint. |  | CloudTrailClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Cloudtrail client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Cloudtrail client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Cloudtrail client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Cloudtrail client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Cloudtrail client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the CloudTrail client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in CloudTrail. | false | boolean |

## Endpoint Options

The AWS CloudTrail endpoint is configured using URI syntax:

aws-cloudtrail:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (consumer) | **Required** A label for indexing cloudtrail endpoints. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **eventSource** (consumer) | Specify an event source to select events. |  | String |
| **maxResults** (consumer) | Maximum number of records that will be fetched in each lookup page. Each poll drains all pages, so this controls the page size rather than the total per poll. AWS allows up to 50. | 50 | int |
| **overrideEndpoint** (consumer) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **region** (consumer) | 
The region in which Cloudtrail client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **uriEndpointOverride** (consumer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **cloudTrailClient** (advanced) | **Autowired** Amazon Cloudtrail client to use for all requests for this endpoint. |  | CloudTrailClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Cloudtrail client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Cloudtrail client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Cloudtrail client.

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
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Cloudtrail client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Cloudtrail client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the CloudTrail client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in CloudTrail. | false | boolean |

## Message Headers

The AWS CloudTrail component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsCloudTrailEventId** (consumer) Constant: [`EVENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-cloudtrail/latest/org/apache/camel/component/aws/cloudtrail/CloudtrailConstants.html#EVENT_ID) | The event ID of the cloud trail event consumed. |  | String |
| **CamelAwsCloudTrailEventName** (consumer) Constant: [`EVENT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws-cloudtrail/latest/org/apache/camel/component/aws/cloudtrail/CloudtrailConstants.html#EVENT_NAME) | The event Name of the cloud trail event consumed. |  | String |
| **CamelAwsCloudTrailEventSource** (consumer) Constant: [`EVENT_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-aws-cloudtrail/latest/org/apache/camel/component/aws/cloudtrail/CloudtrailConstants.html#EVENT_SOURCE) | The event Source of the cloud trail event consumed. |  | String |
| **CamelAwsCloudTrailEventUsername** (consumer) Constant: [`USERNAME`](https://javadoc.io/doc/org.apache.camel/camel-aws-cloudtrail/latest/org/apache/camel/component/aws/cloudtrail/CloudtrailConstants.html#USERNAME) | The associated username of the event of the cloud trail event consumed. |  | String |

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

### CloudTrail Events consumed

The CloudTrail consumer will use an API method called LookupEvents.

This method will only take into account management events like create/update/delete of resources and CloudTrail insight events where enabled.

This means you won’t consume the events registered in the CloudTrail logs stored on S3, in case of creation of a new Trail.

This is important to notice, and it must be taken into account when using this component.