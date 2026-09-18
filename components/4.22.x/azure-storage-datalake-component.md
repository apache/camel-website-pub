# Azure Storage Data Lake Service

**Since Camel 3.8**

**Both producer and consumer are supported**

The Azure storage datalake component is used for storing and retrieving file from Azure Storage Data Lake Service using the **Azure APIs v12**.

Prerequisites

You need to have a valid Azure account with Azure storage set up. More information can be found at [Azure Documentation Portal](https://docs.microsoft.com/azure/).

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-storage-datalake</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your camel core version -->
</dependency>
```

## Uri Format

```text
azure-storage-datalake:accountName[/fileSystemName][?options]
```

In the case of the consumer, both `accountName` and `fileSystemName` are required. In the case of the producer, it depends on the operation being requested.

You can append query options to the URI in the following format: `?option1=value&option2=value&…​`

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

The Azure Storage Data Lake Service component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | client id for azure account. |  | String |
| **close** (common) | Whether or not a file changed event raised indicates completion (true) or modification (false). | false | Boolean |
| **closeStreamAfterRead** (common) | check for closing stream after read. | false | Boolean |
| **configuration** (common) | configuration object for data lake. |  | DataLakeConfiguration |
| **credentialType** (common) | 
Determines the credential strategy to adopt.

Enum values:

-   CLIENT\_SECRET
    
-   SHARED\_KEY\_CREDENTIAL
    
-   AZURE\_IDENTITY
    
-   AZURE\_SAS
    
-   SERVICE\_CLIENT\_INSTANCE
    





 | CLIENT\_SECRET | CredentialType |
| **dataCount** (common) | count number of bytes to download. |  | Long |
| **directoryName** (common) | directory of the file to be handled in component. |  | String |
| **downloadLinkExpiration** (common) | download link expiration time. |  | Long |
| **expression** (common) | expression for queryInputStream. |  | String |
| **fileDir** (common) | directory of file to do operations in the local system. |  | String |
| **fileName** (common) | name of file to be handled in component. |  | String |
| **fileOffset** (common) | offset position in file for different operations. |  | Long |
| **maxResults** (common) | maximum number of results to show at a time. |  | Integer |
| **maxRetryRequests** (common) | no of retries to a given request. |  | int |
| **openOptions** (common) | set open options for creating file. |  | Set |
| **path** (common) | path in azure data lake for operations. |  | String |
| **permission** (common) | permission string for the file. |  | String |
| **position** (common) | This parameter allows the caller to upload data in parallel and control the order in which it is appended to the file. |  | Long |
| **recursive** (common) | recursively include all paths. | false | Boolean |
| **regex** (common) | regular expression for matching file names. |  | String |
| **retainUncommitedData** (common) | Whether or not uncommitted data is to be retained after the operation. | false | Boolean |
| **serviceClient** (common) | **Autowired** data lake service client for azure storage data lake. |  | DataLakeServiceClient |
| **sharedKeyCredential** (common) | **Autowired** shared key credential for azure data lake gen2. |  | StorageSharedKeyCredential |
| **tenantId** (common) | tenant id for azure account. |  | String |
| **timeout** (common) | Timeout for operation. |  | Duration |
| **umask** (common) | umask permission for file. |  | String |
| **userPrincipalNameReturned** (common) | whether or not to use upn. | false | Boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 

operation to be performed.

Enum values:

-   listFileSystem
    
-   listFiles
    





 | listFileSystem | DataLakeOperationsDefinition |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **accountKey** (security) | account key for authentication. |  | String |
| **clientSecret** (security) | client secret for azure account. |  | String |
| **clientSecretCredential** (security) | **Autowired** client secret credential for authentication. |  | ClientSecretCredential |
| **sasCredential** (security) | **Autowired** SAS token credential. |  | AzureSasCredential |
| **sasSignature** (security) | SAS token signature. |  | String |

## Endpoint Options

The Azure Storage Data Lake Service endpoint is configured using URI syntax:

azure-storage-datalake:accountName/fileSystemName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **accountName** (common) | name of the azure account. |  | String |
| **fileSystemName** (common) | name of filesystem to be used. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | client id for azure account. |  | String |
| **close** (common) | Whether or not a file changed event raised indicates completion (true) or modification (false). | false | Boolean |
| **closeStreamAfterRead** (common) | check for closing stream after read. | false | Boolean |
| **credentialType** (common) | 
Determines the credential strategy to adopt.

Enum values:

-   CLIENT\_SECRET
    
-   SHARED\_KEY\_CREDENTIAL
    
-   AZURE\_IDENTITY
    
-   AZURE\_SAS
    
-   SERVICE\_CLIENT\_INSTANCE
    





 | CLIENT\_SECRET | CredentialType |
| **dataCount** (common) | count number of bytes to download. |  | Long |
| **dataLakeServiceClient** (common) | service client of data lake. |  | DataLakeServiceClient |
| **directoryName** (common) | directory of the file to be handled in component. |  | String |
| **downloadLinkExpiration** (common) | download link expiration time. |  | Long |
| **expression** (common) | expression for queryInputStream. |  | String |
| **fileDir** (common) | directory of file to do operations in the local system. |  | String |
| **fileName** (common) | name of file to be handled in component. |  | String |
| **fileOffset** (common) | offset position in file for different operations. |  | Long |
| **maxResults** (common) | maximum number of results to show at a time. |  | Integer |
| **maxRetryRequests** (common) | no of retries to a given request. |  | int |
| **openOptions** (common) | set open options for creating file. |  | Set |
| **path** (common) | path in azure data lake for operations. |  | String |
| **permission** (common) | permission string for the file. |  | String |
| **position** (common) | This parameter allows the caller to upload data in parallel and control the order in which it is appended to the file. |  | Long |
| **recursive** (common) | recursively include all paths. | false | Boolean |
| **regex** (common) | regular expression for matching file names. |  | String |
| **retainUncommitedData** (common) | Whether or not uncommitted data is to be retained after the operation. | false | Boolean |
| **serviceClient** (common) | **Autowired** data lake service client for azure storage data lake. |  | DataLakeServiceClient |
| **sharedKeyCredential** (common) | **Autowired** shared key credential for azure data lake gen2. |  | StorageSharedKeyCredential |
| **tenantId** (common) | tenant id for azure account. |  | String |
| **timeout** (common) | Timeout for operation. |  | Duration |
| **umask** (common) | umask permission for file. |  | String |
| **userPrincipalNameReturned** (common) | whether or not to use upn. | false | Boolean |
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
| **operation** (producer) | 

operation to be performed.

Enum values:

-   listFileSystem
    
-   listFiles
    





 | listFileSystem | DataLakeOperationsDefinition |
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
| **accountKey** (security) | account key for authentication. |  | String |
| **clientSecret** (security) | client secret for azure account. |  | String |
| **clientSecretCredential** (security) | **Autowired** client secret credential for authentication. |  | ClientSecretCredential |
| **sasCredential** (security) | **Autowired** SAS token credential. |  | AzureSasCredential |
| **sasSignature** (security) | SAS token signature. |  | String |

## Message Headers

The Azure Storage Data Lake Service component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureStorageDataLakeListFileSystemsOptions** (producer) Constant: [`LIST_FILESYSTEMS_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#LIST_FILESYSTEMS_OPTIONS) | Defines options available to configure the behavior of a call to listFileSystemsSegment on a DataLakeServiceAsyncClient object. Null may be passed. |  | ListFileSystemsOptions |
| **CamelAzureStorageDataLakeTimeout** (producer) Constant: [`TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#TIMEOUT) | An optional timeout value beyond which a RuntimeException will be raised. |  | Duration |
| **CamelAzureStorageDataLakeOperation** (producer) Constant: [`DATALAKE_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#DATALAKE_OPERATION) | 
Specify the producer operation to execute. Different operations allowed are shown below.

Enum values:

-   listFileSystem
    
-   createFileSystem
    
-   deleteFileSystem
    
-   listPaths
    
-   getFile
    
-   downloadToFile
    
-   downloadLink
    
-   deleteFile
    
-   appendToFile
    
-   flushToFile
    
-   uploadFromFile
    
-   upload
    
-   openQueryInputStream
    
-   createFile
    
-   deleteDirectory
    





 |  | DataLakeOperationsDefinition |
| **CamelAzureStorageDataLakeFileSystemName** (producer) Constant: [`FILESYSTEM_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#FILESYSTEM_NAME) | Name of the file system in azure data lake on which operation is to be performed. Please make sure that filesystem name is all lowercase. |  | String |
| **CamelAzureStorageDataLakeDirectoryName** (producer) Constant: [`DIRECTORY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#DIRECTORY_NAME) | Name of the directory in azure data lake on which operation is to be performed. |  | String |
| **CamelAzureStorageDataLakeFileName** (producer) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#FILE_NAME) | Name of the file in azure data lake on which operation is to be performed. |  | String |
| **CamelAzureStorageDataLakeMetadata** (from both) Constant: [`METADATA`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#METADATA) | The metadata to associate with the file. |  | Map |
| **CamelAzureStorageDataLakePublicAccessType** (producer) Constant: [`PUBLIC_ACCESS_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#PUBLIC_ACCESS_TYPE) | Defines options available to configure the behavior of a call to listFileSystemsSegment on a DataLakeServiceAsyncClient object. |  | PublicAccessType |
| **CamelAzureStorageDataLakeRawHttpHeaders** (consumer) Constant: [`RAW_HTTP_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#RAW_HTTP_HEADERS) | Non parsed http headers that can be used by the user. |  | HttpHeaders |
| **CamelAzureStorageDataLakeRequestCondition** (producer) Constant: [`DATALAKE_REQUEST_CONDITION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#DATALAKE_REQUEST_CONDITION) | This contains values which will restrict the successful operation of a variety of requests to the conditions present. These conditions are entirely optional. |  | DataLakeRequestConditions |
| **CamelAzureStorageDataLakeListPathOptions** (producer) Constant: [`LIST_PATH_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#LIST_PATH_OPTIONS) | Defines options available to configure the behavior of a call to listContainersSegment on a DataLakeFileSystemClient object. Null may be passed. |  | ListPathOptions |
| **CamelAzureStorageDataLakePath** (producer) Constant: [`PATH`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#PATH) | Path of the file to be used for upload operations. |  | String |
| **CamelAzureStorageDataLakeRecursive** (producer) Constant: [`RECURSIVE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#RECURSIVE) | Specifies if the call to listContainersSegment should recursively include all paths. |  | Boolean |
| **CamelAzureStorageDataLakeMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#MAX_RESULTS) | Specifies the maximum number of blobs to return, including all BlobPrefix elements. |  | Integer |
| **CamelAzureStorageDataLakeUserPrincipalNameReturned** (producer) Constant: [`USER_PRINCIPAL_NAME_RETURNED`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#USER_PRINCIPAL_NAME_RETURNED) | Specifies if the name of the user principal should be returned. |  | Boolean |
| **CamelAzureStorageDataLakeRegex** (producer) Constant: [`REGEX`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#REGEX) | Filter the results to return only those files with match the specified regular expression. |  | String |
| **CamelAzureStorageDataLakeFileDir** (producer) Constant: [`FILE_DIR`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#FILE_DIR) | Directory in which the file is to be downloaded. |  | String |
| **CamelAzureStorageDataLakeAccessTier** (consumer) Constant: [`ACCESS_TIER`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#ACCESS_TIER) | Access tier of file. |  | AccessTier |
| **CamelAzureStorageDataLakeContentMD5** (producer) Constant: [`CONTENT_MD5`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#CONTENT_MD5) | An MD5 hash of the content. The hash is used to verify the integrity of the file during transport. |  | byte\[\] |
| **CamelAzureStorageDataLakeFileRange** (producer) Constant: [`FILE_RANGE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#FILE_RANGE) | This is a representation of a range of bytes on a file, typically used during a download operation. Passing null as a FileRange value will default to the entire range of the file. |  | FileRange |
| **CamelAzureStorageDataLakeParallelTransferOptions** (producer) Constant: [`PARALLEL_TRANSFER_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#PARALLEL_TRANSFER_OPTIONS) | The configuration used to parallelize data transfer operations. |  | ParallelTransferOptions |
| **CamelAzureStorageDataLakeOpenOptions** (producer) Constant: [`OPEN_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#OPEN_OPTIONS) | Set of OpenOption used to configure how to open or create a file. |  | Set |
| **CamelAzureStorageDataLakeAccessTierChangeTime** (consumer) Constant: [`ACCESS_TIER_CHANGE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#ACCESS_TIER_CHANGE_TIME) | Datetime when the access tier of the blob last changed. |  | OffsetDateTime |
| **CamelAzureStorageDataLakeArchiveStatus** (consumer) Constant: [`ARCHIVE_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#ARCHIVE_STATUS) | Archive status of file. |  | ArchiveStatus |
| **CamelAzureStorageDataLakeCacheControl** (consumer) Constant: [`CACHE_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#CACHE_CONTROL) | Cache control specified for the file. |  | String |
| **CamelAzureStorageDataLakeContentDisposition** (consumer) Constant: [`CONTENT_DISPOSITION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#CONTENT_DISPOSITION) | Content disposition specified for the file. |  | String |
| **CamelAzureStorageDataLakeContentEncoding** (consumer) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#CONTENT_ENCODING) | Content encoding specified for the file. |  | String |
| **CamelAzureStorageDataLakeContentLanguage** (consumer) Constant: [`CONTENT_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#CONTENT_LANGUAGE) | Content language specified for the file. |  | String |
| **CamelAzureStorageDataLakeContentType** (consumer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#CONTENT_TYPE) | Content type specified for the file. |  | String |
| **CamelAzureStorageDataLakeCopyCompletionTime** (consumer) Constant: [`COPY_COMPLETION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#COPY_COMPLETION_TIME) | Conclusion time of the last attempted Copy Blob operation where this file was the destination file. |  | OffsetDateTime |
| **CamelAzureStorageDataLakeCopyId** (consumer) Constant: [`COPY_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#COPY_ID) | String identifier for this copy operation. |  | String |
| **CamelAzureStorageDataLakeCopyProgress** (consumer) Constant: [`COPY_PROGRESS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#COPY_PROGRESS) | Contains the number of bytes copied and the total bytes in the source in the last attempted Copy Blob operation where this file was the destination file. |  | String |
| **CamelAzureStorageDataLakeCopySource** (consumer) Constant: [`COPY_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#COPY_SOURCE) | URL up to 2 KB in length that specifies the source file or file used in the last attempted Copy Blob operation where this file was the destination file. |  | String |
| **CamelAzureStorageDataLakeCopyStatus** (consumer) Constant: [`COPY_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#COPY_STATUS) | 

Status of the last copy operation performed on the file.

Enum values:

-   pending
    
-   success
    
-   aborted
    
-   failed
    





 |  | CopyStatusType |
| **CamelAzureStorageDataLakeCopyStatusDescription** (consumer) Constant: [`COPY_STATUS_DESCRIPTION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#COPY_STATUS_DESCRIPTION) | The description of the copy’s status. |  | String |
| **CamelAzureStorageDataLakeCreationTime** (consumer) Constant: [`CREATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#CREATION_TIME) | Creation time of the file. |  | OffsetDateTime |
| **CamelAzureStorageDataLakeEncryptionKeySha256** (consumer) Constant: [`ENCRYPTION_KEY_SHA_256`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#ENCRYPTION_KEY_SHA_256) | The SHA-256 hash of the encryption key used to encrypt the file. |  | String |
| **CamelAzureStorageDataLakeETag** (consumer) Constant: [`E_TAG`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#E_TAG) | The E Tag of the file. |  | String |
| **CamelAzureStorageDataLakeFileSize** (consumer) Constant: [`FILE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#FILE_SIZE) | Size of the file. |  | Long |
| **CamelAzureStorageDataLakeLastModified** (consumer) Constant: [`LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#LAST_MODIFIED) | Datetime when the file was last modified. |  | OffsetDateTime |
| **CamelAzureStorageDataLakeLeaseDuration** (consumer) Constant: [`LEASE_DURATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#LEASE_DURATION) | 

Type of lease on the file.

Enum values:

-   infinite
    
-   fixed
    





 |  | LeaseDurationType |
| **CamelAzureStorageDataLakeLeaseState** (consumer) Constant: [`LEASE_STATE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#LEASE_STATE) | 

State of the lease on the file.

Enum values:

-   available
    
-   leased
    
-   expired
    
-   breaking
    
-   broken
    





 |  | LeaseStateType |
| **CamelAzureStorageDataLakeLeaseStatus** (consumer) Constant: [`LEASE_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#LEASE_STATUS) | 

Status of the lease on the file.

Enum values:

-   locked
    
-   unlocked
    





 |  | LeaseStatusType |
| **CamelAzureStorageDataLakeIncrementalCopy** (producer) Constant: [`INCREMENTAL_COPY`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#INCREMENTAL_COPY) | Flag indicating if the file was incrementally copied. |  | Boolean |
| **CamelAzureStorageDataLakeServerEncrypted** (consumer) Constant: [`SERVER_ENCRYPTED`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#SERVER_ENCRYPTED) | Flag indicating if the file’s content is encrypted on the server. |  | Boolean |
| **CamelAzureStorageDataLakeDownloadLinkExpiration** (producer) Constant: [`DOWNLOAD_LINK_EXPIRATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#DOWNLOAD_LINK_EXPIRATION) | Set the Expiration time of the download link. |  | Long |
| **CamelAzureStorageDataLakeDownloadLink** (consumer) Constant: [`DOWNLOAD_LINK`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#DOWNLOAD_LINK) | The link that can be used to download the file from data lake. |  | String |
| **CamelAzureStorageDataLakeFileOffset** (producer) Constant: [`FILE_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#FILE_OFFSET) | The position where the data is to be appended. |  | Long |
| **CamelAzureStorageDataLakeLeaseId** (producer) Constant: [`LEASE_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#LEASE_ID) | By setting lease id, requests will fail if the provided lease does not match the active lease on the file. |  | String |
| **CamelAzureStorageDataLakePathHttpHeaders** (producer) Constant: [`PATH_HTTP_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#PATH_HTTP_HEADERS) | Additional parameters for a set of operations. |  | PathHttpHeaders |
| **CamelAzureStorageDataLakeRetainCommitedData** (producer) Constant: [`RETAIN_UNCOMMITED_DATA`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#RETAIN_UNCOMMITED_DATA) | Determines Whether or not uncommitted data is to be retained after the operation. |  | Boolean |
| **CamelAzureStorageDataLakeClose** (producer) Constant: [`CLOSE`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#CLOSE) | Whether or not a file changed event raised indicates completion (true) or modification (false). |  | Boolean |
| **CamelAzureStorageDataLakePosition** (producer) Constant: [`POSITION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#POSITION) | The length of the file after all data has been written. |  | Long |
| **CamelAzureStorageDataLakeExpression** (producer) Constant: [`EXPRESSION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#EXPRESSION) | The query expression on the file. |  | String |
| **CamelAzureStorageDataLakeInputSerialization** (producer) Constant: [`INPUT_SERIALIZATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#INPUT_SERIALIZATION) | Defines the input serialization for a file query request. either FileQueryJsonSerialization or FileQueryDelimitedSerialization. |  | FileQuerySerialization |
| **CamelAzureStorageDataLakeOutputSerialization** (producer) Constant: [`OUTPUT_SERIALIZATION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#OUTPUT_SERIALIZATION) | Defines the output serialization for a file query request. either FileQueryJsonSerialization or FileQueryDelimitedSerialization. |  | FileQuerySerialization |
| **CamelAzureStorageDataLakeErrorConsumer** (producer) Constant: [`ERROR_CONSUMER`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#ERROR_CONSUMER) | Sets error consumer for file query. |  | Consumer |
| **CamelAzureStorageDataLakeProgressConsumer** (producer) Constant: [`PROGRESS_CONSUMER`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#PROGRESS_CONSUMER) | Sets progress consumer for file query. |  | Consumer |
| **CamelAzureStorageDataLakeQueryOptions** (producer) Constant: [`QUERY_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#QUERY_OPTIONS) | Optional parameters for File Query. |  | FileQueryOptions |
| **CamelAzureStorageDataLakePermission** (producer) Constant: [`PERMISSION`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#PERMISSION) | Sets the permission for file. |  | String |
| **CamelAzureStorageDataLakeUmask** (producer) Constant: [`UMASK`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#UMASK) | Sets the umask for file. |  | String |
| **CamelAzureStorageDataLakeFileClient** (producer) Constant: [`FILE_CLIENT`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#FILE_CLIENT) | Sets the file client to use. |  | DataLakeFileClient |
| **CamelAzureStorageDataLakeFlush** (producer) Constant: [`FLUSH`](https://javadoc.io/doc/org.apache.camel/camel-azure-storage-datalake/latest/org/apache/camel/component/azure/storage/datalake/DataLakeConstants.html#FLUSH) | Sets whether to flush on append. |  | Boolean |

### Methods of authentication

To use this component, you will have to provide at least one of the specific credentialType parameters:

-   `SHARED_KEY_CREDENTIAL`: Provide `accountName` and `accessKey` for your azure account or provide StorageSharedKeyCredential instance which can be provided into `sharedKeyCredential` option.
    
-   `CLIENT_SECRET`: Provide ClientSecretCredential instance which can be provided into `clientSecretCredential` option or provide `accountName`, `clientId`, `clientSecret` and `tenantId` for authentication with Azure Active Directory.
    
-   `SERVICE_CLIENT_INSTANCE`: Provide a DataLakeServiceClient instance which can be provided into `serviceClient` option.
    
-   `AZURE_IDENTITY`: Use the Default Azure Credential Provider Chain
    
-   `AZURE_SAS`: Provide `sasSignature` or `sasCredential` parameters to use SAS mechanism
    

The default is `CLIENT_SECRET`.

## Usage

For example, to download content from file `test.txt` located on the `filesystem` in `camelTesting` storage account, use the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-storage-datalake:camelTesting/filesystem?fileName=test.txt&accountKey=key")
    .to("file://fileDirectory");
```

```xml
<route>
    <from uri="azure-storage-datalake:camelTesting/filesystem?fileName=test.txt&amp;accountKey=key"/>
    <to uri="file://fileDirectory"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-storage-datalake:camelTesting/filesystem
      parameters:
        fileName: test.txt
        accountKey: key
    steps:
      - to:
          uri: file://fileDirectory
```

### Automatic detection of a service client

The component is capable of automatically detecting the presence of a DataLakeServiceClient bean in the registry. Hence, if your registry has only one instance of type DataLakeServiceClient, it will be automatically used as the default client. You won’t have to explicitly define it as an uri parameter.

### Azure Storage DataLake Producer Operations

The various operations supported by Azure Storage DataLake are as given below:

**Operations on Service level**

For these operations, `accountName` option is required

 
| Operation | Description |
| --- | --- |
| `listFileSystem` | List all the file systems that are present in the given azure account. |

**Operations on File system level**

For these operations, `accountName` and `fileSystemName` options are required

 
| Operation | Description |
| --- | --- |
| `createFileSystem` | Create a new file System with the storage account |
| `deleteFileSystem` | Delete the specified file system within the storage account |
| `listPaths` | Returns list of all the files within the given path in the given file system, with folder structure flattened |

**Operations on Directory level**

For these operations, `accountName`, `fileSystemName` and `directoryName` options are required

 
| Operation | Description |
| --- | --- |
| `createFile` | Create a new file in the specified directory within the fileSystem |
| `deleteDirectory` | Delete the specified directory within the file system |

**Operations on file level**

For these operations, `accountName`, `fileSystemName` and `fileName` options are required

 
| Operation | Description |
| --- | --- |
| `getFile` | Get the contents of a file |
| `downloadToFile` | Download the entire file from the file system into a path specified by fileDir. |
| `downloadLink` | Generate a download link for the specified file using Shared Access Signature (SAS). The expiration time to be set for the link can be specified otherwise 1 hour is taken as default. |
| `deleteFile` | Delete the specified file. |
| `appendToFile` | Appends the data passed to the specified file in the file System. Flush command is required after append. |
| `flushToFile` | Flushes the data already appended to the specified file. |
| `openQueryInputStream` | Opens an `InputStream` based on the query passed to the endpoint. For this operation, you must first register the query acceleration feature with your subscription. |

Refer to the examples section below for more details on how to use these operations

## Examples

### Consumer Examples

To consume a file from the storage datalake into a file using the file component, this can be done like this:

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-storage-datalake:cameltesting/filesystem?fileName=test.txt&accountKey=yourAccountKey")
    .to("file:/filelocation");
```

```xml
<route>
  <from uri="azure-storage-datalake:cameltesting/filesystem?fileName=test.txt&amp;accountKey=yourAccountKey"/>
  <to uri="file:/filelocation"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-storage-datalake:cameltesting/filesystem
      parameters:
        fileName: test.txt
        accountKey: yourAccountKey
      steps:
        - to:
            uri: file:/filelocation
```

You can also directly write to a file without using the file component. For this, you will need to specify the path in `fileDir` option, to save it to your machine.

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-storage-datalake:cameltesting/filesystem?fileName=test.txt&accountKey=yourAccountKey&fileDir=/test/directory")
    .to("mock:results");
```

```xml
<route>
  <from uri="azure-storage-datalake:cameltesting/filesystem?fileName=test.txt&amp;accountKey=yourAccountKey&amp;fileDir=/test/directory"/>
  <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-storage-datalake:cameltesting/filesystem
      parameters:
        fileName: test.txt
        accountKey: yourAccountKey
        fileDir: /test/directory
      steps:
        - to:
            uri: mock:results
```

This component also supports batch consumer. So, you can consume multiple files from a file system by specifying the path from where you want to consume the files.

-   Java
    
-   XML
    
-   YAML
    

```java
from("azure-storage-datalake:cameltesting/filesystem?accountKey=yourAccountKey&fileDir=/test/directory&path=abc/test")
    .to("mock:results");
```

```xml
<route>
  <from uri="azure-storage-datalake:cameltesting/filesystem?accountKey=yourAccountKey&amp;fileDir=/test/directory&amp;path=abc/test"/>
  <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: azure-storage-datalake:cameltesting/filesystem
      parameters:
        accountKey: yourAccountKey
        fileDir: /test/directory
        path: abc/test
      steps:
        - to:
            uri: mock:results
```

### Producer Examples

-   `listFileSystem`
    

_Java-only: uses `ListFileSystemsOptions` SDK type_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader(DataLakeConstants.LIST_FILESYSTEMS_OPTIONS,
                new ListFileSystemsOptions().setMaxResultsPerPage(10));
    })
    .to("azure-storage-datalake:cameltesting?operation=listFileSystem&serviceClient=#serviceClient")
    .to("mock:results");
```

-   `createFileSystem`
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageDataLakeFileSystemName", constant("test1"))
    .to("azure-storage-datalake:cameltesting?operation=createFileSystem&serviceClient=#serviceClient")
    .to("mock:results");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageDataLakeFileSystemName">
    <constant>test1</constant>
  </setHeader>
  <to uri="azure-storage-datalake:cameltesting?operation=createFileSystem&amp;serviceClient=#serviceClient"/>
  <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageDataLakeFileSystemName
            constant: test1
        - to:
            uri: azure-storage-datalake:cameltesting
            parameters:
              operation: createFileSystem
              serviceClient: "#serviceClient"
        - to:
            uri: mock:results
```

-   `deleteFileSystem`
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageDataLakeFileSystemName", constant("test1"))
    .to("azure-storage-datalake:cameltesting?operation=deleteFileSystem&serviceClient=#serviceClient")
    .to("mock:results");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageDataLakeFileSystemName">
    <constant>test1</constant>
  </setHeader>
  <to uri="azure-storage-datalake:cameltesting?operation=deleteFileSystem&amp;serviceClient=#serviceClient"/>
  <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageDataLakeFileSystemName
            constant: test1
        - to:
            uri: azure-storage-datalake:cameltesting
            parameters:
              operation: deleteFileSystem
              serviceClient: "#serviceClient"
        - to:
            uri: mock:results
```

-   `listPaths`
    

_Java-only: uses `ListPathsOptions` SDK type_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader(DataLakeConstants.LIST_PATH_OPTIONS,
                new ListPathsOptions().setPath("/main"));
    })
    .to("azure-storage-datalake:cameltesting/filesystem?operation=listPaths&serviceClient=#serviceClient")
    .to("mock:results");
```

-   `getFile`
    

This can be done in two ways. We can either set an `OutputStream` in the exchange body:

_Java-only: sets an `OutputStream` for the file content to be written to_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setBody(outputStream);
    })
    .to("azure-storage-datalake:cameltesting/filesystem?operation=getFile&fileName=test.txt&serviceClient=#serviceClient")
    .to("mock:results");
```

Or if the body is not set, the operation will give an `InputStream`, given that you have already registered for query acceleration in azure portal.

_Java-only: reads the file content as an \`InputStream\`_

```java
from("direct:start")
    .to("azure-storage-datalake:cameltesting/filesystem?operation=getFile&fileName=test.txt&serviceClient=#serviceClient")
    .process(exchange -> {
        InputStream inputStream = exchange.getMessage().getBody(InputStream.class);
        System.out.println(IOUtils.toString(inputStream, StandardCharsets.UTF_8.name()));
    })
    .to("mock:results");
```

-   `deleteFile`
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("azure-storage-datalake:cameltesting/filesystem?operation=deleteFile&fileName=test.txt&serviceClient=#serviceClient")
    .to("mock:results");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="azure-storage-datalake:cameltesting/filesystem?operation=deleteFile&amp;fileName=test.txt&amp;serviceClient=#serviceClient"/>
    <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
    steps:
      - to:
          uri: azure-storage-datalake:cameltesting/filesystem
          parameters:
            operation: deleteFile
            fileName: test.txt
            serviceClient: "#serviceClient"
      - to:
          uri: mock:results
```

-   `downloadToFile`
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("azure-storage-datalake:cameltesting/filesystem?operation=downloadToFile&fileName=test.txt&fileDir=/test/mydir&serviceClient=#serviceClient")
    .to("mock:results");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="azure-storage-datalake:cameltesting/filesystem?operation=downloadToFile&amp;fileName=test.txt&amp;fileDir=/test/mydir&amp;serviceClient=#serviceClient"/>
    <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
    steps:
      - to:
          uri: azure-storage-datalake:cameltesting/filesystem
          parameters:
            operation: downloadToFile
            fileName: test.txt
            fileDir: /test/mydir
            serviceClient: "#serviceClient"
      - to:
          uri: mock:results
```

-   `downloadLink`
    

_Java-only: processes the generated download link from the response body_

```java
from("direct:start")
    .to("azure-storage-datalake:cameltesting/filesystem?operation=downloadLink&fileName=test.txt&serviceClient=#serviceClient")
    .process(exchange -> {
        String link = exchange.getMessage().getBody(String.class);
        System.out.println(link);
    })
    .to("mock:results");
```

-   `appendToFile`
    

_Java-only: creates an `InputStream` body for the data to append_

```java
from("direct:start")
    .process(exchange -> {
        final String data = "test data";
        final InputStream inputStream = new ByteArrayInputStream(data.getBytes(StandardCharsets.UTF_8));
        exchange.getIn().setBody(inputStream);
    })
    .to("azure-storage-datalake:cameltesting/filesystem?operation=appendToFile&fileName=test.txt&serviceClient=#serviceClient")
    .to("mock:results");
```

-   `flushToFile`
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageDataLakePosition", constant(0))
    .to("azure-storage-datalake:cameltesting/filesystem?operation=flushToFile&fileName=test.txt&serviceClient=#serviceClient")
    .to("mock:results");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageDataLakePosition">
    <constant>0</constant>
  </setHeader>
  <to uri="azure-storage-datalake:cameltesting/filesystem?operation=flushToFile&amp;fileName=test.txt&amp;serviceClient=#serviceClient"/>
  <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageDataLakePosition
            constant: 0
        - to:
            uri: azure-storage-datalake:cameltesting/filesystem
            parameters:
              operation: flushToFile
              fileName: test.txt
              serviceClient: "#serviceClient"
        - to:
            uri: mock:results
```

-   `openQueryInputStream`
    

For this operation, you should have already registered for query acceleration on the azure portal.

_Java-only: uses `FileQueryOptions` SDK type_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader(DataLakeConstants.QUERY_OPTIONS,
                new FileQueryOptions("SELECT * from BlobStorage"));
    })
    .to("azure-storage-datalake:cameltesting/filesystem?operation=openQueryInputStream&fileName=test.txt&serviceClient=#serviceClient")
    .to("mock:results");
```

-   `upload`
    

_Java-only: creates an `InputStream` body for the data to upload_

```java
from("direct:start")
    .process(exchange -> {
        final String data = "test data";
        final InputStream inputStream = new ByteArrayInputStream(data.getBytes(StandardCharsets.UTF_8));
        exchange.getIn().setBody(inputStream);
    })
    .to("azure-storage-datalake:cameltesting/filesystem?operation=upload&fileName=test.txt&serviceClient=#serviceClient")
    .to("mock:results");
```

-   `uploadFromFile`
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageDataLakePath", constant("test/file.txt"))
    .to("azure-storage-datalake:cameltesting/filesystem?operation=uploadFromFile&fileName=test.txt&serviceClient=#serviceClient")
    .to("mock:results");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageDataLakePath">
    <constant>test/file.txt</constant>
  </setHeader>
  <to uri="azure-storage-datalake:cameltesting/filesystem?operation=uploadFromFile&amp;fileName=test.txt&amp;serviceClient=#serviceClient"/>
  <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageDataLakePath
            constant: test/file.txt
        - to:
            uri: azure-storage-datalake:cameltesting/filesystem
            parameters:
              operation: uploadFromFile
              fileName: test.txt
              serviceClient: "#serviceClient"
        - to:
            uri: mock:results
```

-   `createFile`
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageDataLakeDirectoryName", constant("test/file/"))
    .to("azure-storage-datalake:cameltesting/filesystem?operation=createFile&fileName=test.txt&serviceClient=#serviceClient")
    .to("mock:results");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageDataLakeDirectoryName">
    <constant>test/file/</constant>
  </setHeader>
  <to uri="azure-storage-datalake:cameltesting/filesystem?operation=createFile&amp;fileName=test.txt&amp;serviceClient=#serviceClient"/>
  <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageDataLakeDirectoryName
            constant: "test/file/"
        - to:
            uri: azure-storage-datalake:cameltesting/filesystem
            parameters:
              operation: createFile
              fileName: test.txt
              serviceClient: "#serviceClient"
        - to:
            uri: mock:results
```

-   `deleteDirectory`
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelAzureStorageDataLakeDirectoryName", constant("test/file/"))
    .to("azure-storage-datalake:cameltesting/filesystem?operation=deleteDirectory&serviceClient=#serviceClient")
    .to("mock:results");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelAzureStorageDataLakeDirectoryName">
    <constant>test/file/</constant>
  </setHeader>
  <to uri="azure-storage-datalake:cameltesting/filesystem?operation=deleteDirectory&amp;serviceClient=#serviceClient"/>
  <to uri="mock:results"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelAzureStorageDataLakeDirectoryName
            constant: "test/file/"
        - to:
            uri: azure-storage-datalake:cameltesting/filesystem
            parameters:
              operation: deleteDirectory
              serviceClient: "#serviceClient"
        - to:
            uri: mock:results
```

### Testing

Please run all the unit tests and integration tests while making changes to the component as changes or version upgrades can break things. For running all the tests in the component, you will need to obtain azure `accountName` and `accessKey`. After obtaining the same, you can run the full test on this component directory by running the following maven command

```bash
mvn verify -Dazure.storage.account.name=<accountName> -Dazure.storage.account.key=<accessKey>
```

You can also skip the integration test and run only basic unit test by using the command

```bash
mvn test
```