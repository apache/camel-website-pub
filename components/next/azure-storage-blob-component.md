# Azure Storage Blob Service

**Since Camel 3.3**

**Both producer and consumer are supported**

The Azure Storage Blob component is used for storing and retrieving blobs from [Azure Storage Blob](https://azure.microsoft.com/services/storage/blobs/) Service using **Azure APIs v12**. However, in the case of versions above v12, we will see if this component can adopt these changes depending on how much breaking changes can result.

Prerequisites

You must have a valid Windows Azure Storage account. More information is available at [Azure Documentation Portal](https://docs.microsoft.com/azure/).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-storage-blob</artifactId>
    <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

```text
azure-storage-blob://accountName[/containerName][?options]
```

In the case of a consumer, `accountName`, `containerName` are required.

In the case of a producer, it depends on the operation that is being requested, for example, if operation is on a container level, e.b: createContainer, accountName and containerName are only required, but in case of operation being requested in blob level, e.g: getBlob, accountName, containerName and blobName are required.

The blob will be created if it does not already exist. You can append query options to the URI in the following format, `?options=value&option2=value&…​`

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

The Azure Storage Blob Service component supports 51 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **blobName** (common) | The blob name, to consume specific blob from a container. However, on producer it is only required for the operations on the blob level. |  | String |
| **blobOffset** (common) | Set the blob offset for the upload or download operations, default is 0. | 0 | long |
| **blobType** (common) | 
The blob type in order to initiate the appropriate settings for each blob type.

Enum values:

-   blockblob
    
-   appendblob
    
-   pageblob
    





 | blockblob | BlobType |
| **closeStreamAfterRead** (common) | Close the stream after read or keep it open, default is true. | true | boolean |
| **configuration** (common) | The component configurations. |  | BlobConfiguration |
| **credentials** (common) | **Autowired** StorageSharedKeyCredential can be injected to create the azure client, this holds the important authentication information. |  | StorageSharedKeyCredential |
| **credentialType** (common) | 

Determines the credential strategy to adopt.

Enum values:

-   SHARED\_ACCOUNT\_KEY
    
-   SHARED\_KEY\_CREDENTIAL
    
-   AZURE\_IDENTITY
    
-   AZURE\_SAS
    





 | AZURE\_IDENTITY | CredentialType |
| **dataCount** (common) | How many bytes to include in the range. Must be greater than or equal to 0 if specified. |  | Long |
| **fileDir** (common) | The file directory where the downloaded blobs will be saved to, this can be used in both, producer and consumer. |  | String |
| **leaseBlob** (common) | Sets whether a lease should be acquired when accessing the blob. When set to true, the component will acquire a lease before performing blob operations that require exclusive access. | false | boolean |
| **leaseDurationInSeconds** (common) | Sets the lease duration in seconds. Use -1 for infinite or a value between 15 and 60 for fixed leases. | 60 | Integer |
| **maxResultsPerPage** (common) | Specifies the maximum number of blobs to return, including all BlobPrefix elements. If the request does not specify maxResultsPerPage or specifies a value greater than 5,000, the server will return up to 5,000 items. |  | Integer |
| **maxRetryRequests** (common) | Specifies the maximum number of additional HTTP Get requests that will be made while reading the data from a response body. | 0 | int |
| **prefix** (common) | Filters the results to return only blobs whose names begin with the specified prefix. May be null to return all blobs. |  | String |
| **regex** (common) | Filters the results to return only blobs whose names match the specified regular expression. May be null to return all if both prefix and regex are set, regex takes the priority and prefix is ignored. |  | String |
| **sasToken** (common) | In case of usage of Shared Access Signature we’ll need to set a SAS Token. |  | String |
| **serviceClient** (common) | **Autowired** Client to a storage account. This client does not hold any state about a particular storage account but is instead a convenient way of sending off appropriate requests to the resource on the service. It may also be used to construct URLs to blobs and containers. This client contains operations on a service account. Operations on a container are available on BlobContainerClient through BlobServiceClient#getBlobContainerClient(String), and operations on a blob are available on BlobClient through BlobContainerClient#getBlobClient(String). |  | BlobServiceClient |
| **snapshotId** (common) | The snapshot identifier used to target a specific blob snapshot on read operations (getBlob, downloadBlobToFile, downloadLink). When set, the read targets the snapshot scoped client instead of the live blob. Can also be provided per-exchange via the CamelAzureStorageBlobSnapshotId header. |  | String |
| **timeout** (common) | An optional timeout value beyond which a RuntimeException will be raised. |  | Duration |
| **versionId** (common) | The blob version identifier used to target a specific blob version on read operations (getBlob, downloadBlobToFile, downloadLink). Requires blob versioning to be enabled on the storage account. When set, the read targets the version scoped client instead of the live blob. Can also be provided per-exchange via the CamelAzureStorageBlobVersionId header. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **deleteAfterRead** (consumer) | Delete blobs from Azure after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the blob is not deleted. If this option is false, then the same blobs will be retrieved over and over again in the polls. Therefore, you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the BlobConstants#BLOB\_NAME header, or only the blob name. | false | boolean |
| **destinationBlobPrefix** (consumer) | Define the destination blob prefix to use when a blob must be moved, and moveAfterRead is set to true. |  | String |
| **destinationBlobSuffix** (consumer) | Define the destination blob suffix to use when a blob must be moved, and moveAfterRead is set to true. |  | String |
| **destinationContainer** (consumer) | Define the destination container where a blob must be moved when moveAfterRead is set to true. |  | String |
| **moveAfterRead** (consumer) | Move blobs from the container to a different container after they have been retrieved. To accomplish the operation, the destinationContainer option must be set. The copy blob operation is only performed if the Exchange is committed. If a rollback occurs, the blob is not moved. | false | boolean |
| **removePrefixOnMove** (consumer) | Remove the contents of the prefix configuration string from the new blob name before moving. For example, if prefix is set to 'notify/' and the destinationBlobPrefix is set to 'archive/', a blob with a name of 'notify/example.txt' will be moved to 'archive/example.txt', rather than the default behavior where the new name is 'archive/notify/example.txt'. Only applicable when moveAfterRead is true. | false | boolean |
| **blobSequenceNumber** (producer) | A user-controlled value that you can use to track requests. The value of the sequence number must be between 0 and 263 - 1.The default value is 0. | 0 | Long |
| **blockListType** (producer) | 

Specifies which type of blocks to return.

Enum values:

-   committed
    
-   uncommitted
    
-   all
    





 | COMMITTED | BlockListType |
| **blockSize** (producer) | The block size in bytes to use for chunked uploads with uploadBlockBlobChunked operation. Default is 4MB (4194304). Maximum is 4000MB. Must be greater than 0. |  | Long |
| **changeFeedContext** (producer) | When using getChangeFeed producer operation, this gives additional context that is passed through the Http pipeline during the service call. |  | Context |
| **changeFeedEndTime** (producer) | When using getChangeFeed producer operation, this filters the results to return events approximately before the end time. Note: A few events belonging to the next hour can also be returned. A few events belonging to this hour can be missing; to ensure all events from the hour are returned, round the end time up by an hour. |  | OffsetDateTime |
| **changeFeedStartTime** (producer) | When using getChangeFeed producer operation, this filters the results to return events approximately after the start time. Note: A few events belonging to the previous hour can also be returned. A few events belonging to this hour can be missing; to ensure all events from the hour are returned, round the start time down by an hour. |  | OffsetDateTime |
| **closeStreamAfterWrite** (producer) | Close the stream after write or keep it open, default is true. | true | boolean |
| **commitBlockListLater** (producer) | When is set to true, the staged blocks will not be committed directly. | true | boolean |
| **createAppendBlob** (producer) | When is set to true, the append blocks will be created when committing append blocks. | true | boolean |
| **createPageBlob** (producer) | When is set to true, the page blob will be created when uploading page blob. | true | boolean |
| **downloadLinkExpiration** (producer) | Override the default expiration (millis) of URL download link. |  | Long |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxConcurrency** (producer) | The maximum number of parallel requests to use during upload with uploadBlockBlobChunked operation. Default is determined by the Azure SDK based on available processors. |  | Integer |
| **maxSingleUploadSize** (producer) | The maximum size in bytes for a single upload request with uploadBlockBlobChunked operation. Files smaller than this will be uploaded in a single request. Files larger will use chunked upload with blocks of size blockSize. Default is 256MB. |  | Long |
| **operation** (producer) | 

The blob operation that can be used with this component on the producer.

Enum values:

-   listBlobContainers
    
-   findBlobsByTags
    
-   createBlobContainer
    
-   deleteBlobContainer
    
-   listBlobs
    
-   getBlob
    
-   deleteBlob
    
-   downloadBlobToFile
    
-   downloadLink
    
-   uploadBlockBlob
    
-   uploadBlockBlobChunked
    
-   stageBlockBlobList
    
-   commitBlobBlockList
    
-   getBlobBlockList
    
-   createAppendBlob
    
-   commitAppendBlob
    
-   createPageBlob
    
-   uploadPageBlob
    
-   resizePageBlob
    
-   clearPageBlob
    
-   getPageBlobRanges
    
-   getChangeFeed
    
-   copyBlob
    
-   createBlobSnapshot
    
-   setBlobTags
    
-   getBlobTags
    
-   undeleteBlob
    
-   setBlobTier
    





 | listBlobContainers | BlobOperationsDefinition |
| **pageBlobSize** (producer) | Specifies the maximum size for the page blob, up to 8 TB. The page blob size must be aligned to a 512-byte boundary. | 512 | Long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **accessKey** (security) | Access key for the associated azure account name to be used for authentication with azure blob services. |  | String |
| **azureClientId** (security) | Azure Client ID for authentication with Azure Identity. |  | String |
| **azureClientSecret** (security) | Azure Client Secret for authentication with Azure Identity. |  | String |
| **azureTenantId** (security) | Azure Tenant ID for authentication with Azure Identity. |  | String |
| **sourceBlobAccessKey** (security) | Source Blob Access Key: for copyblob operation, sadly, we need to have an accessKey for the source blob we want to copy Passing an accessKey as header, it’s unsafe so we could set as key. |  | String |

## Endpoint Options

The Azure Storage Blob Service endpoint is configured using URI syntax:

azure-storage-blob:accountName/containerName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accountName** (common) | Azure account name to be used for authentication with azure blob services. |  | String |
| **containerName** (common) | The blob container name. |  | String |

### Query Parameters (66 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **blobName** (common) | The blob name, to consume specific blob from a container. However, on producer it is only required for the operations on the blob level. |  | String |
| **blobOffset** (common) | Set the blob offset for the upload or download operations, default is 0. | 0 | long |
| **blobServiceClient** (common) | Client to a storage account. This client does not hold any state about a particular storage account but is instead a convenient way of sending off appropriate requests to the resource on the service. It may also be used to construct URLs to blobs and containers. This client contains operations on a service account. Operations on a container are available on BlobContainerClient through getBlobContainerClient(String), and operations on a blob are available on BlobClient through getBlobContainerClient(String).getBlobClient(String). |  | BlobServiceClient |
| **blobType** (common) | 
The blob type in order to initiate the appropriate settings for each blob type.

Enum values:

-   blockblob
    
-   appendblob
    
-   pageblob
    





 | blockblob | BlobType |
| **closeStreamAfterRead** (common) | Close the stream after read or keep it open, default is true. | true | boolean |
| **credentials** (common) | **Autowired** StorageSharedKeyCredential can be injected to create the azure client, this holds the important authentication information. |  | StorageSharedKeyCredential |
| **credentialType** (common) | 

Determines the credential strategy to adopt.

Enum values:

-   SHARED\_ACCOUNT\_KEY
    
-   SHARED\_KEY\_CREDENTIAL
    
-   AZURE\_IDENTITY
    
-   AZURE\_SAS
    





 | AZURE\_IDENTITY | CredentialType |
| **dataCount** (common) | How many bytes to include in the range. Must be greater than or equal to 0 if specified. |  | Long |
| **fileDir** (common) | The file directory where the downloaded blobs will be saved to, this can be used in both, producer and consumer. |  | String |
| **leaseBlob** (common) | Sets whether a lease should be acquired when accessing the blob. When set to true, the component will acquire a lease before performing blob operations that require exclusive access. | false | boolean |
| **leaseDurationInSeconds** (common) | Sets the lease duration in seconds. Use -1 for infinite or a value between 15 and 60 for fixed leases. | 60 | Integer |
| **maxResultsPerPage** (common) | Specifies the maximum number of blobs to return, including all BlobPrefix elements. If the request does not specify maxResultsPerPage or specifies a value greater than 5,000, the server will return up to 5,000 items. |  | Integer |
| **maxRetryRequests** (common) | Specifies the maximum number of additional HTTP Get requests that will be made while reading the data from a response body. | 0 | int |
| **prefix** (common) | Filters the results to return only blobs whose names begin with the specified prefix. May be null to return all blobs. |  | String |
| **regex** (common) | Filters the results to return only blobs whose names match the specified regular expression. May be null to return all if both prefix and regex are set, regex takes the priority and prefix is ignored. |  | String |
| **sasToken** (common) | In case of usage of Shared Access Signature we’ll need to set a SAS Token. |  | String |
| **serviceClient** (common) | **Autowired** Client to a storage account. This client does not hold any state about a particular storage account but is instead a convenient way of sending off appropriate requests to the resource on the service. It may also be used to construct URLs to blobs and containers. This client contains operations on a service account. Operations on a container are available on BlobContainerClient through BlobServiceClient#getBlobContainerClient(String), and operations on a blob are available on BlobClient through BlobContainerClient#getBlobClient(String). |  | BlobServiceClient |
| **snapshotId** (common) | The snapshot identifier used to target a specific blob snapshot on read operations (getBlob, downloadBlobToFile, downloadLink). When set, the read targets the snapshot scoped client instead of the live blob. Can also be provided per-exchange via the CamelAzureStorageBlobSnapshotId header. |  | String |
| **timeout** (common) | An optional timeout value beyond which a RuntimeException will be raised. |  | Duration |
| **versionId** (common) | The blob version identifier used to target a specific blob version on read operations (getBlob, downloadBlobToFile, downloadLink). Requires blob versioning to be enabled on the storage account. When set, the read targets the version scoped client instead of the live blob. Can also be provided per-exchange via the CamelAzureStorageBlobVersionId header. |  | String |
| **deleteAfterRead** (consumer) | Delete blobs from Azure after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the blob is not deleted. If this option is false, then the same blobs will be retrieved over and over again in the polls. Therefore, you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the BlobConstants#BLOB\_NAME header, or only the blob name. | false | boolean |
| **destinationBlobPrefix** (consumer) | Define the destination blob prefix to use when a blob must be moved, and moveAfterRead is set to true. |  | String |
| **destinationBlobSuffix** (consumer) | Define the destination blob suffix to use when a blob must be moved, and moveAfterRead is set to true. |  | String |
| **destinationContainer** (consumer) | Define the destination container where a blob must be moved when moveAfterRead is set to true. |  | String |
| **moveAfterRead** (consumer) | Move blobs from the container to a different container after they have been retrieved. To accomplish the operation, the destinationContainer option must be set. The copy blob operation is only performed if the Exchange is committed. If a rollback occurs, the blob is not moved. | false | boolean |
| **removePrefixOnMove** (consumer) | Remove the contents of the prefix configuration string from the new blob name before moving. For example, if prefix is set to 'notify/' and the destinationBlobPrefix is set to 'archive/', a blob with a name of 'notify/example.txt' will be moved to 'archive/example.txt', rather than the default behavior where the new name is 'archive/notify/example.txt'. Only applicable when moveAfterRead is true. | false | boolean |
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
| **blobSequenceNumber** (producer) | A user-controlled value that you can use to track requests. The value of the sequence number must be between 0 and 263 - 1.The default value is 0. | 0 | Long |
| **blockListType** (producer) | 

Specifies which type of blocks to return.

Enum values:

-   committed
    
-   uncommitted
    
-   all
    





 | COMMITTED | BlockListType |
| **blockSize** (producer) | The block size in bytes to use for chunked uploads with uploadBlockBlobChunked operation. Default is 4MB (4194304). Maximum is 4000MB. Must be greater than 0. |  | Long |
| **changeFeedContext** (producer) | When using getChangeFeed producer operation, this gives additional context that is passed through the Http pipeline during the service call. |  | Context |
| **changeFeedEndTime** (producer) | When using getChangeFeed producer operation, this filters the results to return events approximately before the end time. Note: A few events belonging to the next hour can also be returned. A few events belonging to this hour can be missing; to ensure all events from the hour are returned, round the end time up by an hour. |  | OffsetDateTime |
| **changeFeedStartTime** (producer) | When using getChangeFeed producer operation, this filters the results to return events approximately after the start time. Note: A few events belonging to the previous hour can also be returned. A few events belonging to this hour can be missing; to ensure all events from the hour are returned, round the start time down by an hour. |  | OffsetDateTime |
| **closeStreamAfterWrite** (producer) | Close the stream after write or keep it open, default is true. | true | boolean |
| **commitBlockListLater** (producer) | When is set to true, the staged blocks will not be committed directly. | true | boolean |
| **createAppendBlob** (producer) | When is set to true, the append blocks will be created when committing append blocks. | true | boolean |
| **createPageBlob** (producer) | When is set to true, the page blob will be created when uploading page blob. | true | boolean |
| **downloadLinkExpiration** (producer) | Override the default expiration (millis) of URL download link. |  | Long |
| **maxConcurrency** (producer) | The maximum number of parallel requests to use during upload with uploadBlockBlobChunked operation. Default is determined by the Azure SDK based on available processors. |  | Integer |
| **maxSingleUploadSize** (producer) | The maximum size in bytes for a single upload request with uploadBlockBlobChunked operation. Files smaller than this will be uploaded in a single request. Files larger will use chunked upload with blocks of size blockSize. Default is 256MB. |  | Long |
| **operation** (producer) | 

The blob operation that can be used with this component on the producer.

Enum values:

-   listBlobContainers
    
-   findBlobsByTags
    
-   createBlobContainer
    
-   deleteBlobContainer
    
-   listBlobs
    
-   getBlob
    
-   deleteBlob
    
-   downloadBlobToFile
    
-   downloadLink
    
-   uploadBlockBlob
    
-   uploadBlockBlobChunked
    
-   stageBlockBlobList
    
-   commitBlobBlockList
    
-   getBlobBlockList
    
-   createAppendBlob
    
-   commitAppendBlob
    
-   createPageBlob
    
-   uploadPageBlob
    
-   resizePageBlob
    
-   clearPageBlob
    
-   getPageBlobRanges
    
-   getChangeFeed
    
-   copyBlob
    
-   createBlobSnapshot
    
-   setBlobTags
    
-   getBlobTags
    
-   undeleteBlob
    
-   setBlobTier
    





 | listBlobContainers | BlobOperationsDefinition |
| **pageBlobSize** (producer) | Specifies the maximum size for the page blob, up to 8 TB. The page blob size must be aligned to a 512-byte boundary. | 512 | Long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
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
| **accessKey** (security) | Access key for the associated azure account name to be used for authentication with azure blob services. |  | String |
| **azureClientId** (security) | Azure Client ID for authentication with Azure Identity. |  | String |
| **azureClientSecret** (security) | Azure Client Secret for authentication with Azure Identity. |  | String |
| **azureTenantId** (security) | Azure Tenant ID for authentication with Azure Identity. |  | String |
| **sourceBlobAccessKey** (security) | Source Blob Access Key: for copyblob operation, sadly, we need to have an accessKey for the source blob we want to copy Passing an accessKey as header, it’s unsafe so we could set as key. |  | String |

## Message Headers

The Azure Storage Blob Service component supports 79 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureStorageBlobOperation** (producer) Constant: [`BLOB_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_OPERATION) | 
(All) Specify the producer operation to execute, please see the doc on this page related to producer operation.

Enum values:

-   listBlobContainers
    
-   findBlobsByTags
    
-   createBlobContainer
    
-   deleteBlobContainer
    
-   listBlobs
    
-   listBlobVersions
    
-   getBlob
    
-   deleteBlob
    
-   downloadBlobToFile
    
-   downloadLink
    
-   uploadBlockBlob
    
-   uploadBlockBlobChunked
    
-   stageBlockBlobList
    
-   commitBlobBlockList
    
-   getBlobBlockList
    
-   createAppendBlob
    
-   commitAppendBlob
    
-   createPageBlob
    
-   uploadPageBlob
    
-   resizePageBlob
    
-   clearPageBlob
    
-   getPageBlobRanges
    
-   getChangeFeed
    
-   copyBlob
    
-   createBlobSnapshot
    
-   setBlobTags
    
-   getBlobTags
    
-   setBlobLegalHold
    
-   setBlobImmutabilityPolicy
    
-   undeleteBlob
    
-   setBlobTier
    





 |  | BlobOperationsDefinition |
| **CamelAzureStorageBlobHttpHeaders** (producer) Constant: [`BLOB_HTTP_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_HTTP_HEADERS) | (uploadBlockBlob, commitBlobBlockList, createAppendBlob, createPageBlob) Additional parameters for a set of operations. |  | BlobHttpHeaders |
| **CamelAzureStorageBlobETag** (consumer) Constant: [`E_TAG`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#E_TAG) | The E Tag of the blob. |  | String |
| **CamelAzureStorageBlobCreationTime** (consumer) Constant: [`CREATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CREATION_TIME) | Creation time of the blob. |  | OffsetDateTime |
| **CamelAzureStorageBlobLastModified** (consumer) Constant: [`LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#LAST_MODIFIED) | Datetime when the blob was last modified. |  | OffsetDateTime |
| **CamelAzureStorageBlobContentType** (consumer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CONTENT_TYPE) | Content type specified for the blob. |  | String |
| **CamelAzureStorageBlobContentMD5** (common) Constant: [`CONTENT_MD5`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CONTENT_MD5) | (producer) (Most operations related to upload blob) Most operations related to upload blobAn MD5 hash of the block content. This hash is used to verify the integrity of the block during transport. When this header is specified, the storage service compares the hash of the content that has arrived with this header value. Note that this MD5 hash is not stored with the blob. If the two hashes do not match, the operation will fail. (consumer) Content MD5 specified for the blob. |  | byte\[\] |
| **CamelAzureStorageBlobContentEncoding** (consumer) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CONTENT_ENCODING) | Content encoding specified for the blob. |  | String |
| **CamelAzureStorageBlobContentDisposition** (consumer) Constant: [`CONTENT_DISPOSITION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CONTENT_DISPOSITION) | Content disposition specified for the blob. |  | String |
| **CamelAzureStorageBlobContentLanguage** (consumer) Constant: [`CONTENT_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CONTENT_LANGUAGE) | Content language specified for the blob. |  | String |
| **CamelAzureStorageBlobCacheControl** (consumer) Constant: [`CACHE_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CACHE_CONTROL) | Cache control specified for the blob. |  | String |
| **CamelAzureStorageBlobBlobSize** (consumer) Constant: [`BLOB_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_SIZE) | The size of the blob. |  | long |
| **CamelAzureStorageBlobBlobUploadSize** (producer) Constant: [`BLOB_UPLOAD_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_UPLOAD_SIZE) | When uploading a blob with the uploadBlockBlob-operation this can be used to tell the client what the length of an InputStream is. |  | long |
| **CamelAzureStorageBlobSequenceNumber** (common) Constant: [`BLOB_SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_SEQUENCE_NUMBER) | (producer) (createPageBlob) A user-controlled value that you can use to track requests. The value of the sequence number must be between 0 and 263 - 1. The default value is 0. (consumer) The current sequence number for a page blob. |  | Long |
| **CamelAzureStorageBlobBlobType** (consumer) Constant: [`BLOB_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_TYPE) | 

The type of the blob.

Enum values:

-   blockblob
    
-   appendblob
    
-   pageblob
    





 |  | BlobType |
| **CamelAzureStorageBlobLeaseBlob** (common) Constant: [`LEASE_BLOB`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#LEASE_BLOB) | Specifies whether blob leasing is enabled for the operation. When set to true, the component will acquire an exclusive lease on the target blob to prevent concurrent processing by multiple routes or applications. |  | boolean |
| **CamelAzureStorageBlobLeaseDurationInSeconds** (common) Constant: [`LEASE_DURATION_IN_SECONDS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#LEASE_DURATION_IN_SECONDS) | Specifies the lease duration in seconds. Valid values are between 15 and 60 for fixed duration, or -1 for infinite duration. |  | Integer |
| **CamelAzureStorageBlobLeaseStatus** (consumer) Constant: [`LEASE_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#LEASE_STATUS) | 

Status of the lease on the blob.

Enum values:

-   locked
    
-   unlocked
    





 |  | LeaseStatusType |
| **CamelAzureStorageBlobLeaseState** (consumer) Constant: [`LEASE_STATE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#LEASE_STATE) | 

State of the lease on the blob.

Enum values:

-   available
    
-   leased
    
-   expired
    
-   breaking
    
-   broken
    





 |  | LeaseStateType |
| **CamelAzureStorageBlobLeaseDuration** (consumer) Constant: [`LEASE_DURATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#LEASE_DURATION) | 

Type of lease on the blob.

Enum values:

-   infinite
    
-   fixed
    





 |  | LeaseDurationType |
| **CamelAzureStorageBlobCopyId** (consumer) Constant: [`COPY_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#COPY_ID) | Identifier of the last copy operation performed on the blob. |  | String |
| **CamelAzureStorageBlobCopyStatus** (consumer) Constant: [`COPY_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#COPY_STATUS) | 

Status of the last copy operation performed on the blob.

Enum values:

-   pending
    
-   success
    
-   aborted
    
-   failed
    





 |  | CopyStatusType |
| **CamelAzureStorageBlobCopySource** (consumer) Constant: [`COPY_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#COPY_SOURCE) | Source of the last copy operation performed on the blob. |  | String |
| **CamelAzureStorageBlobCopyProgress** (consumer) Constant: [`COPY_PROGRESS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#COPY_PROGRESS) | Progress of the last copy operation performed on the blob. |  | String |
| **CamelAzureStorageBlobCopyCompletionTime** (consumer) Constant: [`COPY_COMPILATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#COPY_COMPILATION_TIME) | Datetime when the last copy operation on the blob completed. |  | OffsetDateTime |
| **CamelAzureStorageBlobCopyStatusDescription** (consumer) Constant: [`COPY_STATUS_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#COPY_STATUS_DESCRIPTION) | Description of the last copy operation on the blob. |  | String |
| **CamelAzureStorageBlobCopyDestinationSnapshot** (consumer) Constant: [`COPY_DESTINATION_SNAPSHOT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#COPY_DESTINATION_SNAPSHOT) | Snapshot identifier of the last incremental copy snapshot for the blob. |  | String |
| **CamelAzureStorageBlobIsServerEncrypted** (consumer) Constant: [`IS_SERVER_ENCRYPTED`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#IS_SERVER_ENCRYPTED) | Flag indicating if the blob’s content is encrypted on the server. |  | boolean |
| **CamelAzureStorageBlobIsIncrementalCopy** (consumer) Constant: [`IS_INCREMENTAL_COPY`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#IS_INCREMENTAL_COPY) | Flag indicating if the blob was incrementally copied. |  | boolean |
| **CamelAzureStorageBlobAccessTier** (common) Constant: [`ACCESS_TIER`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#ACCESS_TIER) | (producer) (uploadBlockBlob, commitBlobBlockList) Defines values for AccessTier. (consumer) Access tier of the blob. |  | AccessTier |
| **CamelAzureStorageBlobIsAccessTierInferred** (consumer) Constant: [`IS_ACCESS_TIER_INFRRRED`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#IS_ACCESS_TIER_INFRRRED) | Flag indicating if the access tier of the blob was inferred from properties of the blob. |  | boolean |
| **CamelAzureStorageBlobArchiveStatus** (consumer) Constant: [`ARCHIVE_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#ARCHIVE_STATUS) | Archive status of the blob. |  | ArchiveStatus |
| **CamelAzureStorageBlobaccessTierChangeTime** (consumer) Constant: [`ACCESS_TIER_CHANGE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#ACCESS_TIER_CHANGE_TIME) | Datetime when the access tier of the blob last changed. |  | OffsetDateTime |
| **CamelAzureStorageBlobMetadata** (common) Constant: [`METADATA`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#METADATA) | (producer) (Operations related to container and blob) Operations related to container and blob Metadata to associate with the container or blob. (consumer) Additional metadata associated with the blob. |  | Map |
| **CamelAzureStorageBlobCommittedBlockCount** (consumer) Constant: [`COMMITTED_BLOCK_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#COMMITTED_BLOCK_COUNT) | Number of blocks committed to an append blob. |  | Integer |
| **CamelAzureStorageBlobAppendOffset** (consumer) Constant: [`APPEND_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#APPEND_OFFSET) | The offset at which the block was committed to the block blob. |  | String |
| **CamelAzureStorageBlobRawHttpHeaders** (consumer) Constant: [`RAW_HTTP_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#RAW_HTTP_HEADERS) | Returns non-parsed httpHeaders that can be used by the user. |  | HttpHeaders |
| **CamelAzureStorageBlobFileName** (consumer) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#FILE_NAME) | The downloaded filename from the operation downloadBlobToFile. |  | String |
| **CamelAzureStorageBlobDownloadLink** (consumer) Constant: [`DOWNLOAD_LINK`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#DOWNLOAD_LINK) | The download link generated by downloadLink operation. |  | String |
| **CamelAzureStorageBlobListBlobOptions** (producer) Constant: [`LIST_BLOB_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#LIST_BLOB_OPTIONS) | (listBlobs) Defines options available to configure the behavior of a call to listBlobsFlatSegment on a BlobContainerClient object. |  | ListBlobsOptions |
| **CamelAzureStorageBlobListDetails** (producer) Constant: [`BLOB_LIST_DETAILS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_LIST_DETAILS) | (listBlobs) The details for listing specific blobs. |  | BlobListDetails |
| **CamelAzureStorageBlobPrefix** (producer) Constant: [`PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#PREFIX) | (listBlobs,getBlob) Filters the results to return only blobs whose names begin with the specified prefix. May be null to return all blobs. |  | String |
| **CamelAzureStorageBlobRegex** (producer) Constant: [`REGEX`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#REGEX) | (listBlobs,getBlob) Filters the results to return only blobs whose names match the specified regular expression. May be null to return all. If both prefix and regex are set, regex takes the priority and prefix is ignored. |  | String |
| **CamelAzureStorageBlobMaxResultsPerPage** (producer) Constant: [`MAX_RESULTS_PER_PAGE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#MAX_RESULTS_PER_PAGE) | (listBlobs) Specifies the maximum number of blobs to return, including all BlobPrefix elements. If the request does not specify maxResultsPerPage or specifies a value greater than 5,000, the server will return up to 5,000 items. |  | Integer |
| **CamelAzureStorageBlobTimeout** (producer) Constant: [`TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#TIMEOUT) | (All) An optional timeout value beyond which a RuntimeException will be raised. |  | Duration |
| **CamelAzureStorageBlobPublicAccessType** (producer) Constant: [`PUBLIC_ACCESS_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#PUBLIC_ACCESS_TYPE) | (createContainer) Specifies how the data in this container is available to the public. Pass null for no public access. |  | PublicAccessType |
| **CamelAzureStorageBlobRequestCondition** (producer) Constant: [`BLOB_REQUEST_CONDITION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_REQUEST_CONDITION) | (Operations related to container and blob) This contains values which will restrict the successful operation of a variety of requests to the conditions present. These conditions are entirely optional. |  | BlobRequestConditions |
| **CamelAzureStorageBlobBlobContainerName** (producer) Constant: [`BLOB_CONTAINER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_CONTAINER_NAME) | (Operations related to container and blob) Override/set the container name on the exchange headers. |  | String |
| **CamelAzureStorageBlobBlobName** (producer) Constant: [`BLOB_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_NAME) | (Operations related to blob) Override/set the blob name on the exchange headers. |  | String |
| **CamelAzureStorageBlobFileDir** (producer) Constant: [`FILE_DIR`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#FILE_DIR) | (downloadBlobToFile) The file directory where the downloaded blobs will be saved to. |  | String |
| **CamelAzureStorageBlobPageBlobRange** (producer) Constant: [`PAGE_BLOB_RANGE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#PAGE_BLOB_RANGE) | (Operations related to page blob) A PageRange object. Given that pages must be aligned with 512-byte boundaries, the start offset must be a modulus of 512 and the end offset must be a modulus of 512 - 1. Examples of valid byte ranges are 0-511, 512-1023, etc. |  | PageRange |
| **CamelAzureStorageBlobPageBlobSize** (producer) Constant: [`PAGE_BLOB_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#PAGE_BLOB_SIZE) | (createPageBlob, resizePageBlob) Specifies the maximum size for the page blob, up to 8 TB. The page blob size must be aligned to a 512-byte boundary. |  | Long |
| **CamelAzureStorageBlobCommitBlobBlockListLater** (producer) Constant: [`COMMIT_BLOCK_LIST_LATER`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#COMMIT_BLOCK_LIST_LATER) | (stageBlockBlobList) When is set to true, the staged blocks will not be committed directly. |  | boolean |
| **CamelAzureStorageBlobBlockListType** (producer) Constant: [`BLOCK_LIST_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOCK_LIST_TYPE) | 

(getBlobBlockList) Specifies which type of blocks to return.

Enum values:

-   committed
    
-   uncommitted
    
-   all
    





 |  | BlockListType |
| **CamelAzureStorageBlobCreateAppendBlob** (producer) Constant: [`CREATE_APPEND_BLOB`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CREATE_APPEND_BLOB) | (commitAppendBlob) When is set to true, the append blocks will be created when committing append blocks. |  | boolean |
| **CamelAzureStorageBlobCreatePageBlob** (producer) Constant: [`CREATE_PAGE_BLOB`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CREATE_PAGE_BLOB) | (uploadPageBlob) When is set to true, the page blob will be created when uploading page blob. |  | boolean |
| **CamelAzureStorageBlobDeleteSnapshotsOptionType** (producer) Constant: [`DELETE_SNAPSHOT_OPTION_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#DELETE_SNAPSHOT_OPTION_TYPE) | 

(deleteBlob) Specifies the behavior for deleting the snapshots on this blob. Include will delete the base blob and all snapshots. Only will delete only the snapshots. If a snapshot is being deleted, you must pass null.

Enum values:

-   include
    
-   only
    





 |  | DeleteSnapshotsOptionType |
| **CamelAzureStorageBlobListBlobContainersOptions** (producer) Constant: [`LIST_BLOB_CONTAINERS_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#LIST_BLOB_CONTAINERS_OPTIONS) | (listBlobContainers) A ListBlobContainersOptions which specifies what data should be returned by the service. |  | ListBlobContainersOptions |
| **CamelAzureStorageBlobParallelTransferOptions** (producer) Constant: [`PARALLEL_TRANSFER_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#PARALLEL_TRANSFER_OPTIONS) | (downloadBlobToFile, uploadBlockBlobChunked) ParallelTransferOptions to use to download to file or upload from file. Number of parallel transfers parameter is ignored for downloads. |  | ParallelTransferOptions |
| **CamelAzureStorageBlobFilePath** (producer) Constant: [`FILE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#FILE_PATH) | (uploadBlockBlobChunked) The local file path to upload. Can be provided as a File, Path, or String in the message body, or via this header. |  | String |
| **CamelAzureStorageBlobBlockSize** (producer) Constant: [`BLOCK_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOCK_SIZE) | (uploadBlockBlobChunked) The block size in bytes to use for chunked uploads. Default is 4MB (4194304). Maximum is 4000MB. Must be greater than 0. |  | Long |
| **CamelAzureStorageBlobMaxConcurrency** (producer) Constant: [`MAX_CONCURRENCY`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#MAX_CONCURRENCY) | (uploadBlockBlobChunked) The maximum number of parallel requests to use during upload. Default is determined by the Azure SDK based on available processors. |  | Integer |
| **CamelAzureStorageBlobMaxSingleUploadSize** (producer) Constant: [`MAX_SINGLE_UPLOAD_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#MAX_SINGLE_UPLOAD_SIZE) | (uploadBlockBlobChunked) The maximum size in bytes for a single upload request. Files smaller than this will be uploaded in a single request. Files larger will use chunked upload with blocks of size blockSize. Default is 256MB. |  | Long |
| **CamelAzureStorageBlobDownloadLinkExpiration** (producer) Constant: [`DOWNLOAD_LINK_EXPIRATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#DOWNLOAD_LINK_EXPIRATION) | (downloadLink) Override the default expiration (millis) of URL download link. |  | Long |
| **CamelAzureStorageBlobSourceBlobAccountName** (producer) Constant: [`SOURCE_BLOB_ACCOUNT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#SOURCE_BLOB_ACCOUNT_NAME) | (copyBlob) The source blob account name to be used as source account name in a copy blob operation. |  | String |
| **CamelAzureStorageBlobSourceBlobContainerName** (producer) Constant: [`SOURCE_BLOB_CONTAINER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#SOURCE_BLOB_CONTAINER_NAME) | (copyBlob) The source blob container name to be used as source container name in a copy blob operation. |  | String |
| **CamelAzureStorageBlobChangeFeedStartTime** (producer) Constant: [`CHANGE_FEED_START_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CHANGE_FEED_START_TIME) | (getChangeFeed) It filters the results to return events approximately after the start time. Note: A few events belonging to the previous hour can also be returned. A few events belonging to this hour can be missing; to ensure all events from the hour are returned, round the start time down by an hour. |  | OffsetDateTime |
| **CamelAzureStorageBlobChangeFeedEndTime** (producer) Constant: [`CHANGE_FEED_END_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CHANGE_FEED_END_TIME) | (getChangeFeed) It filters the results to return events approximately before the end time. Note: A few events belonging to the next hour can also be returned. A few events belonging to this hour can be missing; to ensure all events from the hour are returned, round the end time up by an hour. |  | OffsetDateTime |
| **CamelAzureStorageBlobContext** (producer) Constant: [`CHANGE_FEED_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#CHANGE_FEED_CONTEXT) | (getChangeFeed) This gives additional context that is passed through the Http pipeline during the service call. |  | Context |
| **CamelAzureStorageBlobSnapshotId** (common) Constant: [`BLOB_SNAPSHOT_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_SNAPSHOT_ID) | The snapshot identifier. On createBlobSnapshot it is set on the exchange as the id of the newly created snapshot. On read operations (getBlob, downloadBlobToFile, downloadLink) it can be provided as input to target a specific blob snapshot. |  | String |
| **CamelAzureStorageBlobVersionId** (common) Constant: [`BLOB_VERSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_VERSION_ID) | The blob version identifier. On read operations (getBlob, downloadBlobToFile, downloadLink) it can be provided as input to target a specific blob version when versioning is enabled on the storage account. On the consumer side it is populated from the blob properties when available. |  | String |
| **CamelAzureStorageBlobIsCurrentVersion** (consumer) Constant: [`BLOB_IS_CURRENT_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_IS_CURRENT_VERSION) | Flag indicating whether this is the current version of the blob. |  | Boolean |
| **CamelAzureStorageBlobTags** (common) Constant: [`BLOB_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_TAGS) | (producer) (setBlobTags) The tags to set on the blob as key-value pairs. (consumer) The tags retrieved from the blob. |  | Map |
| **CamelAzureStorageBlobTagFilter** (producer) Constant: [`BLOB_TAG_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_TAG_FILTER) | (findBlobsByTags) A SQL-like expression that filters blobs across the storage account based on their index tags, for example Environment = 'Production' AND Status = 'Active'. |  | String |
| **CamelAzureStorageBlobLegalHold** (common) Constant: [`BLOB_LEGAL_HOLD`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_LEGAL_HOLD) | (producer) (setBlobLegalHold) The legal hold status to set on the blob. When set to true the blob is protected from modification and deletion until the hold is cleared by setting the value to false. (consumer) The legal hold status returned by the setBlobLegalHold operation. |  | Boolean |
| **CamelAzureStorageBlobImmutabilityPolicy** (producer) Constant: [`BLOB_IMMUTABILITY_POLICY`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_IMMUTABILITY_POLICY) | (setBlobImmutabilityPolicy) A pre-built BlobImmutabilityPolicy object that overrides the policy expiry time and mode headers when present. |  | BlobImmutabilityPolicy |
| **CamelAzureStorageBlobImmutabilityPolicyExpiryTime** (producer) Constant: [`BLOB_IMMUTABILITY_POLICY_EXPIRY_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_IMMUTABILITY_POLICY_EXPIRY_TIME) | (setBlobImmutabilityPolicy) The expiry time of the time-based retention policy. Required unless a pre-built BlobImmutabilityPolicy is provided via the body or the CamelAzureStorageBlobImmutabilityPolicy header. |  | OffsetDateTime |
| **CamelAzureStorageBlobImmutabilityPolicyMode** (producer) Constant: [`BLOB_IMMUTABILITY_POLICY_MODE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#BLOB_IMMUTABILITY_POLICY_MODE) | 

(setBlobImmutabilityPolicy) The mode of the immutability policy: UNLOCKED (default, can be modified or deleted), LOCKED (cannot be modified or shortened, only extended), or MUTABLE.

Enum values:

-   Mutable
    
-   Unlocked
    
-   Locked
    





 |  | BlobImmutabilityPolicyMode |
| **CamelAzureStorageBlobRehydratePriority** (producer) Constant: [`REHYDRATE_PRIORITY`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-blob/latest/org/apache/camel/component/azure/storage/blob/BlobConstants.html#REHYDRATE_PRIORITY) | (setBlobTier) The rehydrate priority used when rehydrating a blob from the archive tier: Standard or High. Ignored when changing tier between non-archive tiers. |  | RehydratePriority |

**Required information options:**

To use this component, you have multiple options to provide the required Azure authentication information:

-   By providing your own [BlobServiceClient](https://azuresdkdocs.blob.core.windows.net/$web/java/azure-storage-blob/12.0.0/com/azure/storage/blob/BlobServiceClient.md) instance which can be injected into `blobServiceClient`. Note: You don’t need to create a specific client, e.g.: BlockBlobClient, the BlobServiceClient represents the upper level which can be used to retrieve lower level clients.
    
-   Via Azure Identity, when specifying `credentialType=AZURE_IDENTITY` and providing required [environment variables](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/identity/azure-identity#environment-variables). This enables service principal (e.g. app registration) authentication with secret/certificate as well as username password. Note that this is the default authentication strategy.
    
-   Via shared storage account key, when specifying `credentialType=SHARED_ACCOUNT_KEY` and providing `accountName` and `accessKey` for your Azure account, this is the simplest way to get started. The accessKey can be generated through your Azure portal.
    
-   Via shared storage account key, when specifying `credentialType=SHARED_KEY_CREDENTIAL` and providing a [StorageSharedKeyCredential](https://azuresdkartifacts.blob.core.windows.net/azure-sdk-for-java/staging/apidocs/com/azure/storage/common/StorageSharedKeyCredential.md) instance which can be injected into `credentials` option.
    
-   Via Azure SAS, when specifying `credentialType=AZURE_SAS` and providing a SAS Token parameter through the `sasToken` parameter.
    

## Usage

For example, to download a blob content from the block blob `hello.txt` located on the `container1` in the `camelazure` storage account, use the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-storage-blob://camelazure/container1?blobName=hello.txt&credentialType=SHARED_ACCOUNT_KEY&accessKey=RAW(yourAccessKey)")
    .to("file://blobdirectory");
```

```xml
<route>
    <from uri="azure-storage-blob://camelazure/container1?blobName=hello.txt&amp;credentialType=SHARED_ACCOUNT_KEY&amp;accessKey=RAW(yourAccessKey)"/>
    <to uri="file://blobdirectory"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-storage-blob://camelazure/container1
      parameters:
        blobName: hello.txt
        credentialType: SHARED_ACCOUNT_KEY
        accessKey: RAW(yourAccessKey)
    steps:
      - to:
          uri: file://blobdirectory
```

### Advanced Azure Storage Blob configuration

If your Camel Application is running behind a firewall or if you need to have more control over the `BlobServiceClient` instance configuration, you can create your own instance:

_Java-only: programmatic BlobServiceClient setup_

```java
StorageSharedKeyCredential credential = new StorageSharedKeyCredential("yourAccountName", "yourAccessKey");
String uri = String.format("https://%s.blob.core.windows.net", "yourAccountName");

BlobServiceClient client = new BlobServiceClientBuilder()
                          .endpoint(uri)
                          .credential(credential)
                          .buildClient();
// This is camel context
context.getRegistry().bind("client", client);
```

Then refer to this instance in your Camel `azure-storage-blob` component configuration:

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-storage-blob://cameldev/container1?blobName=myblob&serviceClient=#client")
    .to("mock:result");
```

```xml
<route>
    <from uri="azure-storage-blob://cameldev/container1?blobName=myblob&amp;serviceClient=#client"/>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-storage-blob://cameldev/container1
      parameters:
        blobName: myblob
        serviceClient: "#client"
    steps:
      - to:
          uri: mock:result
```

### Automatic detection of BlobServiceClient client in registry

The component is capable of detecting the presence of an BlobServiceClient bean into the registry. If it’s the only instance of that type, it will be used as the client, and you won’t have to define it as uri parameter, like the example above. This may be really useful for smarter configuration of the endpoint.

### Azure Storage Blob Producer operations

Camel Azure Storage Blob component provides a wide range of operations on the producer side:

**Operations on the service level**

For these operations, `accountName` is **required**.

 
| Operation | Description |
| --- | --- |
| `listBlobContainers` | Get the content of the blob. You can restrict the output of this operation to a blob range. |
| `getChangeFeed` | Returns transaction logs of all the changes that occur to the blobs and the blob metadata in your storage account. The change feed provides ordered, guaranteed, durable, immutable, read-only log of these changes. |
| `findBlobsByTags` | Returns a list of blobs across the storage account whose index tags match the SQL-like filter expression provided via the `CamelAzureStorageBlobTagFilter` header or the message body. Optionally honours `CamelAzureStorageBlobMaxResultsPerPage` and `CamelAzureStorageBlobTimeout`. The result body is a `List<TaggedBlobItem>`. |

**Operations on the container level**

For these operations, `accountName` and `containerName` are **required**.

 
| Operation | Description |
| --- | --- |
| `createBlobContainer` | Create a new container within a storage account. If a container with the same name already exists, the producer will ignore it. |
| `deleteBlobContainer` | Delete the specified container in the storage account. If the container doesn’t exist, the operation fails. |
| `listBlobs` | Returns a list of blobs in this container, with folder structures flattened. |
| `listBlobVersions` | Returns a list of blobs and their versions in this container. Each `BlobItem` in the result carries its own `versionId` and `isCurrentVersion` flag, allowing the full version history of every blob to be inspected. Requires versioning to be enabled on the storage account. Honours the same `prefix`, `regex` and `maxResultsPerPage` filters as `listBlobs`. |

**Operations on the blob level**

For these operations, `accountName`, `containerName` and `blobName` are **required**.

  
| Operation | Blob Type | Description |
| --- | --- | --- |
| `getBlob` | Common | Get the content of the blob. You can restrict the output of this operation to a blob range. |
| `deleteBlob` | Common | Delete a blob. |
| `downloadBlobToFile` | Common | Download the entire blob into a file specified by the path. The file will be created and must not exist, if the file already exists a `FileAlreadyExistsException` will be thrown. |
| `downloadLink` | Common | Generate the download link for the specified blob using shared access signatures (SAS). This by default only limits to 1hour of allowed access. However, you can override the default expiration duration through the headers. |
| `uploadBlockBlob` | BlockBlob | Creates a new block blob, or updates the content of an existing block blob. Updating an existing block blob overwrites any existing metadata on the blob. Partial updates are not supported with PutBlob; the content of the existing blob is overwritten with the new content. Note: For larger files, use `uploadBlockBlobChunked`. |
| `uploadBlockBlobChunked` | BlockBlob | Creates or updates a block blob with support for large files (up to several GB). Uses chunked parallel uploads for memory efficiency. Accepts File, Path, WrappedFile, or InputStream as body. Configure `blockSize` (default: 4MB) and `maxConcurrency` (default: auto) for performance tuning. Recommended for files larger than 256MB. |
| `stageBlockBlobList` | `BlockBlob` | Uploads the specified block to the block blob’s "staging area" to be later committed by a call to commitBlobBlockList. However, in case header `CamelAzureStorageBlobCommitBlobBlockListLater` or config `commitBlockListLater` is set to false, this will commit the blocks immediately after staging the blocks. |
| `commitBlobBlockList` | `BlockBlob` | Write a blob by specifying the list of block IDs that are to make up the blob. To be written as part of a blob, a block must have been successfully written to the server in a prior `stageBlockBlobList` operation. You can call `commitBlobBlockList` to update a blob by uploading only those blocks that have changed, then committing the new and existing blocks together. Any blocks not specified in the block list and permanently deleted. |
| `getBlobBlockList` | `BlockBlob` | Returns the list of blocks that have been uploaded as part of a block blob using the specified blocklist filter. |
| `createAppendBlob` | `AppendBlob` | Creates a 0-length append blob. Call commitAppendBlo\`b operation to append data to an append blob. |
| `commitAppendBlob` | `AppendBlob` | Commits a new block of data to the end of the existing append blob. In case of header `CamelAzureStorageBlobCreateAppendBlob` or config `createAppendBlob` is set to true, it will attempt to create the appendBlob through internal call to `createAppendBlob` operation first before committing. |
| `createPageBlob` | `PageBlob` | Creates a page blob of the specified length. Call `uploadPageBlob` operation to upload data to a page blob. |
| `uploadPageBlob` | `PageBlob` | Write one or more pages to the page blob. The size must be a multiple of 512. In case of header `CamelAzureStorageBlobCreatePageBlob` or config `createPageBlob` is set to true, it will attempt to create the appendBlob through internal call to `createPageBlob` operation first before uploading. |
| `resizePageBlob` | `PageBlob` | Resizes the page blob to the specified size, which must be a multiple of 512. |
| `clearPageBlob` | `PageBlob` | Free the specified pages from the page blob. The size of the range must be a multiple of 512. |
| `getPageBlobRanges` | `PageBlob` | Returns the list of valid page ranges for a page blob or snapshot of a page blob. |
| `copyBlob` | `Common` | Copy a blob from one container to another one, even from different accounts. |
| `createBlobSnapshot` | `Common` | Creates a read-only snapshot of a blob. The snapshot ID is returned in the `CamelAzureStorageBlobSnapshotId` header. |
| `setBlobTags` | `Common` | Sets user-defined index tags on a blob. Tags are key-value pairs that can be used to filter and query blobs across containers. Tags can be provided via the `CamelAzureStorageBlobTags` header or as the message body (`Map<String, String>`). |
| `getBlobTags` | `Common` | Retrieves user-defined index tags from a blob. The tags are returned as the message body (`Map<String, String>`) and also set in the `CamelAzureStorageBlobTags` header. |
| `setBlobLegalHold` | `Common` | Sets a legal hold on a blob. The legal hold flag (`Boolean`) is provided via the `CamelAzureStorageBlobLegalHold` header or the message body. While a legal hold is set, the blob cannot be modified or deleted until the hold is explicitly cleared by calling the operation again with `false`. |
| `setBlobImmutabilityPolicy` | `Common` | Sets a time-based immutability policy on a blob. The policy expiry time (`OffsetDateTime`) is read from the `CamelAzureStorageBlobImmutabilityPolicyExpiryTime` header and the policy mode (`BlobImmutabilityPolicyMode`, defaults to `UNLOCKED`) from `CamelAzureStorageBlobImmutabilityPolicyMode`. A pre-built `BlobImmutabilityPolicy` may also be supplied via the message body or `CamelAzureStorageBlobImmutabilityPolicy` header. |
| `undeleteBlob` | `Common` | Restores the contents and metadata of a soft-deleted blob and any associated soft-deleted snapshots. Soft delete must be enabled on the storage account for this operation to succeed. |
| `setBlobTier` | `Common` | Sets the access tier of an existing blob. The target tier (`AccessTier` such as `HOT`, `COOL`, `COLD`, or `ARCHIVE`) is read from the `CamelAzureStorageBlobAccessTier` header or the message body. When rehydrating a blob from `ARCHIVE`, the optional `CamelAzureStorageBlobRehydratePriority` header (`RehydratePriority`, `STANDARD` or `HIGH`) controls the rehydration priority. |

Refer to the example section in this page to learn how to use these operations into your camel application.

## Sub-Pages

For more details on specific features, see:

-   [Producer Operations](others/azure-storage-blob-operations.md) - All producer operation examples, blob snapshots/versions, and SAS token generation
    
-   [Consumer Examples](others/azure-storage-blob-consumer.md) - Consumer patterns including delete after read and move after read
    

## Important Development Notes

All integration tests use [Testcontainers](https://www.testcontainers.org/) and run by default. Obtaining of Azure accessKey and accountName is needed to be able to run all integration tests using Azure services. In addition to the mocked unit tests, you **will need to run the integration tests with every change you make or even client upgrade as the Azure client can break things even on minor versions upgrade.** To run the integration tests, on this component directory, run the following maven command:

```bash
mvn verify -DaccountName=myacc -DaccessKey=mykey -DcredentialType=SHARED_ACCOUNT_KEY
```

Whereby `accountName` is your Azure account name and `accessKey` is the access key being generated from Azure portal.