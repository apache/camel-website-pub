# Azure Storage Queue Service

**Since Camel 3.3**

**Both producer and consumer are supported**

The Azure Storage Queue component supports storing and retrieving the messages to/from [Azure Storage Queue](https://azure.microsoft.com/services/storage/queues/) service using **Azure APIs v12**. However, in the case of versions above v12, we will see if this component can adopt these changes depending on how much breaking changes can result.

Prerequisites

You must have a valid Windows Azure Storage account. More information is available at [Azure Documentation Portal](https://docs.microsoft.com/azure/).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-storage-queue</artifactId>
    <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

```text
azure-storage-queue://accountName[/queueName][?options]
```

In the case of consumer, `accountName` and `queueName` are required.

In the case of producer, it depends on the operation that being requested, for example, if operation is on a service level, e.b: `listQueues`, only `accountName` is required, but in the case of operation being requested on the queue level, e.g.: ``createQueue, `sendMessage``, etc., both `accountName` and `queueName` are required.

The queue will be created if it does not already exist. You can append query options to the URI in the following format: `?options=value&option2=value&…​`

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

The Azure Storage Queue Service component supports 18 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | The component configurations. |  | QueueConfiguration |
| **credentialType** (common) | 
Determines the credential strategy to adopt.

Enum values:

-   SHARED\_ACCOUNT\_KEY
    
-   SHARED\_KEY\_CREDENTIAL
    
-   AZURE\_IDENTITY
    





 | SHARED\_ACCOUNT\_KEY | CredentialType |
| **serviceClient** (common) | **Autowired** Service client to a storage account to interact with the queue service. This client does not hold any state about a particular storage account but is instead a convenient way of sending off appropriate requests to the resource on the service. This client contains all the operations for interacting with a queue account in Azure Storage. Operations allowed by the client are creating, listing, and deleting queues, retrieving and updating properties of the account, and retrieving statistics of the account. |  | QueueServiceClient |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **createQueue** (producer) | When is set to true, the queue will be automatically created when sending messages to the queue. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 

Queue service operation hint to the producer.

Enum values:

-   listQueues
    
-   createQueue
    
-   deleteQueue
    
-   clearQueue
    
-   sendMessage
    
-   deleteMessage
    
-   receiveMessages
    
-   peekMessages
    
-   updateMessage
    





 |  | QueueOperationDefinition |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **maxMessages** (queue) | Maximum number of messages to get, if there are less messages exist in the queue than requested all the messages will be returned. If left empty only 1 message will be retrieved, the allowed range is 1 to 32 messages. | 1 | Integer |
| **messageId** (queue) | The ID of the message to be deleted or updated. |  | String |
| **popReceipt** (queue) | Unique identifier that must match for the message to be deleted or updated. |  | String |
| **timeout** (queue) | An optional timeout applied to the operation. If a response is not returned before the timeout concludes a RuntimeException will be thrown. |  | Duration |
| **timeToLive** (queue) | How long the message will stay alive in the queue. If unset the value will default to 7 days, if -1 is passed the message will not expire. The time to live must be -1 or any positive number. The format should be in this form: PnDTnHnMn.nS., e.g: PT20.345S — parses as 20.345 seconds, P2D — parses as 2 days However, in case you are using EndpointDsl/ComponentDsl, you can do something like Duration.ofSeconds() since these Java APIs are typesafe. |  | Duration |
| **visibilityTimeout** (queue) | The timeout period for how long the message is invisible in the queue. The timeout must be between 1 seconds and 7 days. The format should be in this form: PnDTnHnMn.nS., e.g: PT20.345S — parses as 20.345 seconds, P2D — parses as 2 days However, in case you are using EndpointDsl/ComponentDsl, you can do something like Duration.ofSeconds() since these Java APIs are typesafe. |  | Duration |
| **accessKey** (security) | Access key for the associated azure account name to be used for authentication with azure queue services. |  | String |
| **credentials** (security) | **Autowired** StorageSharedKeyCredential can be injected to create the azure client, this holds the important authentication information. |  | StorageSharedKeyCredential |

## Endpoint Options

The Azure Storage Queue Service endpoint is configured using URI syntax:

azure-storage-queue:accountName/queueName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accountName** (common) | Azure account name to be used for authentication with azure queue services. |  | String |
| **queueName** (common) | The queue resource name. |  | String |

### Query Parameters (32 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **credentialType** (common) | 
Determines the credential strategy to adopt.

Enum values:

-   SHARED\_ACCOUNT\_KEY
    
-   SHARED\_KEY\_CREDENTIAL
    
-   AZURE\_IDENTITY
    





 | SHARED\_ACCOUNT\_KEY | CredentialType |
| **serviceClient** (common) | **Autowired** Service client to a storage account to interact with the queue service. This client does not hold any state about a particular storage account but is instead a convenient way of sending off appropriate requests to the resource on the service. This client contains all the operations for interacting with a queue account in Azure Storage. Operations allowed by the client are creating, listing, and deleting queues, retrieving and updating properties of the account, and retrieving statistics of the account. |  | QueueServiceClient |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **createQueue** (producer) | When is set to true, the queue will be automatically created when sending messages to the queue. | false | boolean |
| **operation** (producer) | 

Queue service operation hint to the producer.

Enum values:

-   listQueues
    
-   createQueue
    
-   deleteQueue
    
-   clearQueue
    
-   sendMessage
    
-   deleteMessage
    
-   receiveMessages
    
-   peekMessages
    
-   updateMessage
    





 |  | QueueOperationDefinition |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxMessages** (queue) | Maximum number of messages to get, if there are less messages exist in the queue than requested all the messages will be returned. If left empty only 1 message will be retrieved, the allowed range is 1 to 32 messages. | 1 | Integer |
| **messageId** (queue) | The ID of the message to be deleted or updated. |  | String |
| **popReceipt** (queue) | Unique identifier that must match for the message to be deleted or updated. |  | String |
| **timeout** (queue) | An optional timeout applied to the operation. If a response is not returned before the timeout concludes a RuntimeException will be thrown. |  | Duration |
| **timeToLive** (queue) | How long the message will stay alive in the queue. If unset the value will default to 7 days, if -1 is passed the message will not expire. The time to live must be -1 or any positive number. The format should be in this form: PnDTnHnMn.nS., e.g: PT20.345S — parses as 20.345 seconds, P2D — parses as 2 days However, in case you are using EndpointDsl/ComponentDsl, you can do something like Duration.ofSeconds() since these Java APIs are typesafe. |  | Duration |
| **visibilityTimeout** (queue) | The timeout period for how long the message is invisible in the queue. The timeout must be between 1 seconds and 7 days. The format should be in this form: PnDTnHnMn.nS., e.g: PT20.345S — parses as 20.345 seconds, P2D — parses as 2 days However, in case you are using EndpointDsl/ComponentDsl, you can do something like Duration.ofSeconds() since these Java APIs are typesafe. |  | Duration |
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
| **accessKey** (security) | Access key for the associated azure account name to be used for authentication with azure queue services. |  | String |
| **credentials** (security) | **Autowired** StorageSharedKeyCredential can be injected to create the azure client, this holds the important authentication information. |  | StorageSharedKeyCredential |

## Message Headers

The Azure Storage Queue Service component supports 16 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureStorageQueueRawHttpHeaders** (common) Constant: [`RAW_HTTP_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#RAW_HTTP_HEADERS) | Returns non-parsed httpHeaders that can be used by the user. |  | HttpHeaders |
| **CamelAzureStorageQueueMetadata** (producer) Constant: [`METADATA`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#METADATA) | (createQueue) Metadata to associate with the queue. |  | Map |
| **CamelAzureStorageQueueMessageId** (common) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#MESSAGE_ID) | The ID of the message. |  | String |
| **CamelAzureStorageQueueInsertionTime** (common) Constant: [`INSERTION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#INSERTION_TIME) | The time the Message was inserted into the Queue. |  | OffsetDateTime |
| **CamelAzureStorageQueueExpirationTime** (common) Constant: [`EXPIRATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#EXPIRATION_TIME) | The time that the Message will expire and be automatically deleted. |  | OffsetDateTime |
| **CamelAzureStorageQueuePopReceipt** (producer) Constant: [`POP_RECEIPT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#POP_RECEIPT) | (deleteMessage, updateMessage) Unique identifier that must match for the message to be deleted or updated. If deletion fails using this pop receipt then the message has been dequeued by another client. |  | String |
| **CamelAzureStorageQueueTimeNextVisible** (common) Constant: [`TIME_NEXT_VISIBLE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#TIME_NEXT_VISIBLE) | The time that the message will again become visible in the Queue. |  | OffsetDateTime |
| **CamelAzureStorageQueueDequeueCount** (common) Constant: [`DEQUEUE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#DEQUEUE_COUNT) | The number of times the message has been dequeued. |  | long |
| **CamelAzureStorageQueueOperation** (producer) Constant: [`QUEUE_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#QUEUE_OPERATION) | 
(All) Specify the producer operation to execute, please see the doc on this page related to producer operation.

Enum values:

-   listQueues
    
-   createQueue
    
-   deleteQueue
    
-   clearQueue
    
-   sendMessage
    
-   deleteMessage
    
-   receiveMessages
    
-   peekMessages
    
-   updateMessage
    





 |  | QueueOperationDefinition |
| **CamelAzureStorageQueueName** (producer) Constant: [`QUEUE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#QUEUE_NAME) | (All) Override the queue name. |  | String |
| **CamelAzureStorageQueueSegmentOptions** (producer) Constant: [`QUEUES_SEGMENT_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#QUEUES_SEGMENT_OPTIONS) | (listQueues) Options for listing queues. |  | QueuesSegmentOptions |
| **CamelAzureStorageQueueTimeout** (producer) Constant: [`TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#TIMEOUT) | (All) An optional timeout value beyond which a RuntimeException will be raised. |  | Duration |
| **CamelAzureStorageQueueMaxMessages** (producer) Constant: [`MAX_MESSAGES`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#MAX_MESSAGES) | (receiveMessages, peekMessages) Maximum number of messages to get, if there are less messages exist in the queue than requested all the messages will be returned. If left empty only 1 message will be retrieved, the allowed range is 1 to 32 messages. |  | Integer |
| **CamelAzureStorageQueueVisibilityTimeout** (producer) Constant: [`VISIBILITY_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#VISIBILITY_TIMEOUT) | (sendMessage, receiveMessages, updateMessage) The timeout period for how long the message is invisible in the queue. If unset the value will default to 0 and the message will be instantly visible. The timeout must be between 0 seconds and 7 days. |  | Duration |
| **CamelAzureStorageQueueTimeToLive** (producer) Constant: [`TIME_TO_LIVE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#TIME_TO_LIVE) | (sendMessage) How long the message will stay alive in the queue. If unset the value will default to 7 days, if -1 is passed the message will not expire. The time to live must be -1 or any positive number. |  | Duration |
| **CamelAzureStorageQueueCreateQueue** (producer) Constant: [`CREATE_QUEUE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-queue/latest/org/apache/camel/component/azure/storage/queue/QueueConstants.html#CREATE_QUEUE) | (sendMessage) When is set to true, the queue will be automatically created when sending messages to the queue. |  | boolean |

**Required information options:**

**Required information options:**

To use this component, you have multiple options to provide the required Azure authentication information:

-   By providing your own QueueServiceClient instance which can be injected into `serviceClient`.
    
-   Via Azure Identity, when specifying `credentialType=AZURE_IDENTITY` and providing required [environment variables](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/identity/azure-identity#environment-variables). This enables service principal (e.g. app registration) authentication with secret/certificate as well as username password.
    
-   Via shared storage account key, when specifying `credentialType=SHARED_ACCOUNT_KEY` and providing `accountName` and `accessKey` for your Azure account, this is the simplest way to get started. The accessKey can be generated through your Azure portal. Note that this is the default authentication strategy.
    
-   Via shared storage account key, when specifying `credentialType=SHARED_KEY_CREDENTIAL` and providing a [StorageSharedKeyCredential](https://azuresdkartifacts.blob.core.windows.net/azure-sdk-for-java/staging/apidocs/com/azure/storage/common/StorageSharedKeyCredential.md) instance which can be injected into `credentials` option.
    

## Usage

For example, to get a message content from the queue `messageQueue` in the `storageAccount` storage account and, use the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-storage-queue://storageAccount/messageQueue?accessKey=yourAccessKey")
    .to("file://queuedirectory");
```

```xml
<route>
    <from uri="azure-storage-queue://storageAccount/messageQueue?accessKey=yourAccessKey"/>
    <to uri="file://queuedirectory"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-storage-queue://storageAccount/messageQueue
      parameters:
        accessKey: yourAccessKey
    steps:
      - to:
          uri: file://queuedirectory
```

### Advanced Azure Storage Queue configuration

If your Camel Application is running behind a firewall or if you need to have more control over the `QueueServiceClient` instance configuration, you can create your own instance:

_Java-only: programmatic Azure SDK client configuration_

```java
StorageSharedKeyCredential credential = new StorageSharedKeyCredential("yourAccountName", "yourAccessKey");
String uri = String.format("https://%s.queue.core.windows.net", "yourAccountName");

QueueServiceClient client = new QueueServiceClientBuilder()
                          .endpoint(uri)
                          .credential(credential)
                          .buildClient();
// This is camel context
context.getRegistry().bind("client", client);
```

Then refer to this instance in your Camel `azure-storage-queue` component configuration:

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-storage-queue://cameldev/queue1?serviceClient=#client")
    .to("file://outputFolder?fileName=output.txt&fileExist=Append");
```

```xml
<route>
  <from uri="azure-storage-queue://cameldev/queue1?serviceClient=#client"/>
  <to uri="file://outputFolder?fileName=output.txt&amp;fileExist=Append"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-storage-queue://cameldev/queue1
      parameters:
        serviceClient: "#client"
      steps:
        - to:
            uri: file://outputFolder
            parameters:
              fileName: output.txt
              fileExist: Append
```

### Automatic detection of QueueServiceClient client in registry

The component is capable of detecting the presence of an QueueServiceClient bean into the registry. If it’s the only instance of that type, it will be used as the client, and you won’t have to define it as uri parameter, like the example above. This may be really useful for smarter configuration of the endpoint.

### Azure Storage Queue Producer operations

Camel Azure Storage Queue component provides a wide range of operations on the producer side:

**Operations on the service level**

For these operations, `accountName` is **required**.

 
| Operation | Description |
| --- | --- |
| `listQueues` | Lists the queues in the storage account that pass the filter starting at the specified marker. |

**Operations on the queue level**

For these operations, `accountName` and `queueName` are **required**.

 
| Operation | Description |
| --- | --- |
| `createQueue` | Creates a new queue. |
| `deleteQueue` | Permanently deletes the queue. |
| `clearQueue` | Deletes all messages in the queue.. |
| `sendMessage` | **Default Producer Operation** Sends a message with a given time-to-live and timeout period where the message is invisible in the queue. The message text is evaluated from the exchange message body. By default, if the queue doesn’t exist, it will create an empty queue first. If you want to disable this, set the config `createQueue` or header `CamelAzureStorageQueueCreateQueue` to `false`. |
| `deleteMessage` | Deletes the specified message in the queue. |
| `receiveMessages` | Retrieves up to the maximum number of messages from the queue and hides them from other operations for the timeout period. However, it will not dequeue the message from the queue due to reliability reasons. |
| `peekMessages` | Peek messages from the front of the queue up to the maximum number of messages. |
| `updateMessage` | Updates the specific message in the queue with a new message and resets the visibility timeout. The message text is evaluated from the exchange message body. |

Refer to the example section in this page to learn how to use these operations into your camel application.

## Examples

### Consumer Examples

To consume a queue into a file component with maximum five messages in one batch, this can be done like this:

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-storage-queue://cameldev/queue1?serviceClient=#client&maxMessages=5")
    .to("file://outputFolder?fileName=output.txt&fileExist=Append");
```

```xml
<route>
    <from uri="azure-storage-queue://cameldev/queue1?serviceClient=#client&amp;maxMessages=5"/>
    <to uri="file://outputFolder?fileName=output.txt&amp;fileExist=Append"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-storage-queue://cameldev/queue1
      parameters:
        serviceClient: "#client"
        maxMessages: 5
    steps:
      - to:
          uri: file://outputFolder
          parameters:
            fileName: output.txt
            fileExist: Append
```

### Producer Operations Examples

-   `listQueues`:
    

_Java-only: requires SDK QueuesSegmentOptions object_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelAzureStorageQueueSegmentOptions",
                new QueuesSegmentOptions().setPrefix("awesome"));
    })
    .to("azure-storage-queue://cameldev?serviceClient=#client&operation=listQueues")
    .log("${body}")
    .to("mock:result");
```

-   `createQueue`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageQueueName", constant("overrideName"))
    .to("azure-storage-queue://cameldev/test?serviceClient=#client&operation=createQueue");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageQueueName">
    <constant>overrideName</constant>
  </setHeader>
  <to uri="azure-storage-queue://cameldev/test?serviceClient=#client&amp;operation=createQueue"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageQueueName
            constant: overrideName
        - to:
            uri: azure-storage-queue://cameldev/test
            parameters:
              serviceClient: "#client"
              operation: createQueue
```

-   `deleteQueue`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageQueueName", constant("overrideName"))
    .to("azure-storage-queue://cameldev/test?serviceClient=#client&operation=deleteQueue");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageQueueName">
    <constant>overrideName</constant>
  </setHeader>
  <to uri="azure-storage-queue://cameldev/test?serviceClient=#client&amp;operation=deleteQueue"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageQueueName
            constant: overrideName
        - to:
            uri: azure-storage-queue://cameldev/test
            parameters:
              serviceClient: "#client"
              operation: deleteQueue
```

-   `clearQueue`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageQueueName", constant("overrideName"))
    .to("azure-storage-queue://cameldev/test?serviceClient=#client&operation=clearQueue");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageQueueName">
    <constant>overrideName</constant>
  </setHeader>
  <to uri="azure-storage-queue://cameldev/test?serviceClient=#client&amp;operation=clearQueue"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageQueueName
            constant: overrideName
        - to:
            uri: azure-storage-queue://cameldev/test
            parameters:
              serviceClient: "#client"
              operation: clearQueue
```

-   `sendMessage`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("message to send"))
    .to("azure-storage-queue://cameldev/test?serviceClient=#client");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <constant>message to send</constant>
  </setBody>
  <to uri="azure-storage-queue://cameldev/test?serviceClient=#client"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            constant: message to send
        - to:
            uri: azure-storage-queue://cameldev/test
            parameters:
              serviceClient: "#client"
```

-   `deleteMessage`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageQueueMessageId", constant("1"))
    .setHeader("CamelAzureStorageQueuePopReceipt", constant("PAAAAHEEERXXX-1"))
    .to("azure-storage-queue://cameldev/test?serviceClient=#client&operation=deleteMessage");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageQueueMessageId">
    <constant>1</constant>
  </setHeader>
  <setHeader name="CamelAzureStorageQueuePopReceipt">
    <constant>PAAAAHEEERXXX-1</constant>
  </setHeader>
  <to uri="azure-storage-queue://cameldev/test?serviceClient=#client&amp;operation=deleteMessage"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageQueueMessageId
            constant: "1"
        - setHeader:
            name: CamelAzureStorageQueuePopReceipt
            constant: PAAAAHEEERXXX-1
        - to:
            uri: azure-storage-queue://cameldev/test
            parameters:
              serviceClient: "#client"
              operation: deleteMessage
```

-   `receiveMessages`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("azure-storage-queue://cameldev/test?serviceClient=#client&operation=receiveMessages")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="azure-storage-queue://cameldev/test?serviceClient=#client&amp;operation=receiveMessages"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: azure-storage-queue://cameldev/test
            parameters:
              serviceClient: "#client"
              operation: receiveMessages
        - to:
            uri: mock:result
```

-   `peekMessages`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("azure-storage-queue://cameldev/test?serviceClient=#client&operation=peekMessages")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="azure-storage-queue://cameldev/test?serviceClient=#client&amp;operation=peekMessages"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: azure-storage-queue://cameldev/test
            parameters:
              serviceClient: "#client"
              operation: peekMessages
        - to:
            uri: mock:result
```

-   `updateMessage`:
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("new message text"))
    .setHeader("CamelAzureStorageQueueMessageId", constant("1"))
    .setHeader("CamelAzureStorageQueuePopReceipt", constant("PAAAAHEEERXXX-1"))
    .to("azure-storage-queue://cameldev/test?serviceClient=#client&operation=updateMessage");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <constant>new message text</constant>
  </setBody>
  <setHeader name="CamelAzureStorageQueueMessageId">
    <constant>1</constant>
  </setHeader>
  <setHeader name="CamelAzureStorageQueuePopReceipt">
    <constant>PAAAAHEEERXXX-1</constant>
  </setHeader>
  <to uri="azure-storage-queue://cameldev/test?serviceClient=#client&amp;operation=updateMessage"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            constant: new message text
        - setHeader:
            name: CamelAzureStorageQueueMessageId
            constant: "1"
        - setHeader:
            name: CamelAzureStorageQueuePopReceipt
            constant: PAAAAHEEERXXX-1
        - to:
            uri: azure-storage-queue://cameldev/test
            parameters:
              serviceClient: "#client"
              operation: updateMessage
```

## Important Development Notes

When developing on this component, you will need to obtain your Azure `accessKey` to run the integration tests. In addition to the mocked unit tests, you **will need to run the integration tests with every change you make or even client upgrade as the Azure client can break things even on minor versions upgrade.** To run the integration tests, on this component directory, run the following maven command:

```bash
mvn verify -DaccountName=myacc -DaccessKey=mykey
```

Whereby `accountName` is your Azure account name and `accessKey` is the access key being generated from Azure portal.