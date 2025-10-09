# Minio

**Since Camel 3.5**

**Both producer and consumer are supported**

The Minio component supports storing and retrieving objects from/to [Minio](https://min.io/) service.

## Prerequisites

You must have valid credentials for authorized access to the buckets/folders. More information is available at [Minio](https://min.io/).

## URI Format

minio://bucketName\[?options\]

The bucket will be created if it doesn’t already exist.  
You can append query options to the URI in the following format, ?options=value&option2=value&…​

For example in order to read file `hello.txt` from the bucket `helloBucket`, use the following snippet:

```java
from("minio://helloBucket?accessKey=yourAccessKey&secretKey=yourSecretKey&objectName=hello.txt")
  .to("file:/var/downloaded");
```

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Minio component supports 47 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateBucket** (common) | Setting the autocreation of the bucket if bucket name not exist. | true | boolean |
| **configuration** (common) | The component configuration. |  | MinioConfiguration |
| **customHttpClient** (common) | Set custom HTTP client for authenticated access. |  | OkHttpClient |
| **endpoint** (common) | Endpoint can be an URL, domain name, IPv4 address or IPv6 address. |  | String |
| **minioClient** (common) | **Autowired** Reference to a Minio Client object in the registry. |  | MinioClient |
| **objectLock** (common) | Set when creating new bucket. | false | boolean |
| **policy** (common) | The policy for this queue to set in the method. |  | String |
| **proxyPort** (common) | TCP/IP port number. 80 and 443 are used as defaults for HTTP and HTTPS. |  | Integer |
| **region** (common) | The region in which Minio client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1). You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **secure** (common) | Flag to indicate to use secure connection to minio service or not. | false | boolean |
| **serverSideEncryption** (common) | Server-side encryption. |  | ServerSideEncryption |
| **serverSideEncryptionCustomerKey** (common) | Server-side encryption for source object while copy/move objects. |  | ServerSideEncryptionCustomerKey |
| **autoCloseBody** (consumer) | If this option is true and includeBody is true, then the MinioObject.close() method will be called on exchange completion. This option is strongly related to includeBody option. In case of setting includeBody to true and autocloseBody to false, it will be up to the caller to close the MinioObject stream. Setting autocloseBody to true, will close the MinioObject stream automatically. | true | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **bypassGovernanceMode** (consumer) | Set this flag if you want to bypassGovernanceMode when deleting a particular object. | false | boolean |
| **deleteAfterRead** (consumer) | Delete objects from Minio after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieve over and over again on the polls. Therefore you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the MinioConstants#BUCKET\_NAME and MinioConstants#OBJECT\_NAME headers, or only the MinioConstants#OBJECT\_NAME header. | true | boolean |
| **delimiter** (consumer) | The delimiter which is used in the ListObjectsRequest to only consume objects we are interested in. |  | String |
| **destinationBucketName** (consumer) | Destination bucket name. |  | String |
| **destinationObjectName** (consumer) | Destination object name. |  | String |
| **includeBody** (consumer) | If it is true, the exchange body will be set to a stream to the contents of the file. If false, the headers will be set with the Minio object metadata, but the body will be null. This option is strongly related to autocloseBody option. In case of setting includeBody to true and autocloseBody to false, it will be up to the caller to close the MinioObject stream. Setting autocloseBody to true, will close the MinioObject stream automatically. | true | boolean |
| **includeFolders** (consumer) | The flag which is used in the ListObjectsRequest to set include folders. | false | boolean |
| **includeUserMetadata** (consumer) | The flag which is used in the ListObjectsRequest to get objects with user meta data. | false | boolean |
| **includeVersions** (consumer) | The flag which is used in the ListObjectsRequest to get objects with versioning. | false | boolean |
| **length** (consumer) | Number of bytes of object data from offset. |  | long |
| **matchETag** (consumer) | Set match ETag parameter for get object(s). |  | String |
| **maxConnections** (consumer) | Set the maxConnections parameter in the minio client configuration. | 60 | int |
| **maxMessagesPerPoll** (consumer) | Gets the maximum number of messages as a limit to poll at each polling. Gets the maximum number of messages as a limit to poll at each polling. The default value is 10. Use 0 or a negative number to set it as unlimited. | 10 | int |
| **modifiedSince** (consumer) | Set modified since parameter for get object(s). |  | ZonedDateTime |
| **moveAfterRead** (consumer) | Move objects from bucket to a different bucket after they have been retrieved. To accomplish the operation the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | boolean |
| **notMatchETag** (consumer) | Set not match ETag parameter for get object(s). |  | String |
| **objectName** (consumer) | To get the object from the bucket with the given object name. |  | String |
| **offset** (consumer) | Start byte position of object data. |  | long |
| **prefix** (consumer) | Object name starts with prefix. |  | String |
| **recursive** (consumer) | List recursively than directory structure emulation. | false | boolean |
| **startAfter** (consumer) | list objects in bucket after this object name. |  | String |
| **unModifiedSince** (consumer) | Set un modified since parameter for get object(s). |  | ZonedDateTime |
| **useVersion1** (consumer) | when true, version 1 of REST API is used. | false | boolean |
| **versionId** (consumer) | Set specific version\_ID of a object when deleting the object. |  | String |
| **deleteAfterWrite** (producer) | Delete file object after the Minio file has been uploaded. | false | boolean |
| **keyName** (producer) | Setting the key name for an element in the bucket through endpoint parameter. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to do in case the user don’t want to do only an upload.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteObjects
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   getObjectRange
    
-   createDownloadLink
    
-   createUploadLink
    





 |  | MinioOperations |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **storageClass** (producer) | The storage class to set in the request. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Secret Access Key or Minio Access Key. If not set camel will connect to service for anonymous access. |  | String |
| **secretKey** (security) | Amazon AWS Access Key Id or Minio Secret Key. If not set camel will connect to service for anonymous access. |  | String |

## Endpoint Options

The Minio endpoint is configured using URI syntax:

minio:bucketName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bucketName** (common) | **Required** Bucket name. |  | String |

### Query Parameters (63 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateBucket** (common) | Setting the autocreation of the bucket if bucket name not exist. | true | boolean |
| **customHttpClient** (common) | Set custom HTTP client for authenticated access. |  | OkHttpClient |
| **endpoint** (common) | Endpoint can be an URL, domain name, IPv4 address or IPv6 address. |  | String |
| **minioClient** (common) | **Autowired** Reference to a Minio Client object in the registry. |  | MinioClient |
| **objectLock** (common) | Set when creating new bucket. | false | boolean |
| **policy** (common) | The policy for this queue to set in the method. |  | String |
| **proxyPort** (common) | TCP/IP port number. 80 and 443 are used as defaults for HTTP and HTTPS. |  | Integer |
| **region** (common) | The region in which Minio client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1). You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **secure** (common) | Flag to indicate to use secure connection to minio service or not. | false | boolean |
| **serverSideEncryption** (common) | Server-side encryption. |  | ServerSideEncryption |
| **serverSideEncryptionCustomerKey** (common) | Server-side encryption for source object while copy/move objects. |  | ServerSideEncryptionCustomerKey |
| **autoCloseBody** (consumer) | If this option is true and includeBody is true, then the MinioObject.close() method will be called on exchange completion. This option is strongly related to includeBody option. In case of setting includeBody to true and autocloseBody to false, it will be up to the caller to close the MinioObject stream. Setting autocloseBody to true, will close the MinioObject stream automatically. | true | boolean |
| **bypassGovernanceMode** (consumer) | Set this flag if you want to bypassGovernanceMode when deleting a particular object. | false | boolean |
| **deleteAfterRead** (consumer) | Delete objects from Minio after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieve over and over again on the polls. Therefore you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the MinioConstants#BUCKET\_NAME and MinioConstants#OBJECT\_NAME headers, or only the MinioConstants#OBJECT\_NAME header. | true | boolean |
| **delimiter** (consumer) | The delimiter which is used in the ListObjectsRequest to only consume objects we are interested in. |  | String |
| **destinationBucketName** (consumer) | Destination bucket name. |  | String |
| **destinationObjectName** (consumer) | Destination object name. |  | String |
| **includeBody** (consumer) | If it is true, the exchange body will be set to a stream to the contents of the file. If false, the headers will be set with the Minio object metadata, but the body will be null. This option is strongly related to autocloseBody option. In case of setting includeBody to true and autocloseBody to false, it will be up to the caller to close the MinioObject stream. Setting autocloseBody to true, will close the MinioObject stream automatically. | true | boolean |
| **includeFolders** (consumer) | The flag which is used in the ListObjectsRequest to set include folders. | false | boolean |
| **includeUserMetadata** (consumer) | The flag which is used in the ListObjectsRequest to get objects with user meta data. | false | boolean |
| **includeVersions** (consumer) | The flag which is used in the ListObjectsRequest to get objects with versioning. | false | boolean |
| **length** (consumer) | Number of bytes of object data from offset. |  | long |
| **matchETag** (consumer) | Set match ETag parameter for get object(s). |  | String |
| **maxConnections** (consumer) | Set the maxConnections parameter in the minio client configuration. | 60 | int |
| **maxMessagesPerPoll** (consumer) | Gets the maximum number of messages as a limit to poll at each polling. Gets the maximum number of messages as a limit to poll at each polling. The default value is 10. Use 0 or a negative number to set it as unlimited. | 10 | int |
| **modifiedSince** (consumer) | Set modified since parameter for get object(s). |  | ZonedDateTime |
| **moveAfterRead** (consumer) | Move objects from bucket to a different bucket after they have been retrieved. To accomplish the operation the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | boolean |
| **notMatchETag** (consumer) | Set not match ETag parameter for get object(s). |  | String |
| **objectName** (consumer) | To get the object from the bucket with the given object name. |  | String |
| **offset** (consumer) | Start byte position of object data. |  | long |
| **prefix** (consumer) | Object name starts with prefix. |  | String |
| **recursive** (consumer) | List recursively than directory structure emulation. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **startAfter** (consumer) | list objects in bucket after this object name. |  | String |
| **unModifiedSince** (consumer) | Set un modified since parameter for get object(s). |  | ZonedDateTime |
| **useVersion1** (consumer) | when true, version 1 of REST API is used. | false | boolean |
| **versionId** (consumer) | Set specific version\_ID of a object when deleting the object. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **deleteAfterWrite** (producer) | Delete file object after the Minio file has been uploaded. | false | boolean |
| **keyName** (producer) | Setting the key name for an element in the bucket through endpoint parameter. |  | String |
| **operation** (producer) | 

The operation to do in case the user don’t want to do only an upload.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteObjects
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   getObjectRange
    
-   createDownloadLink
    
-   createUploadLink
    





 |  | MinioOperations |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **storageClass** (producer) | The storage class to set in the request. |  | String |
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
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. |  | Map |
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
| **accessKey** (security) | Amazon AWS Secret Access Key or Minio Access Key. If not set camel will connect to service for anonymous access. |  | String |
| **secretKey** (security) | Amazon AWS Access Key Id or Minio Secret Key. If not set camel will connect to service for anonymous access. |  | String |

You have to provide the minioClient in the Registry or your accessKey and secretKey to access the [Minio](https://min.io/).

## Batch Consumer

This component implements the Batch Consumer.

This allows you for instance to know how many messages exists in this batch and for instance let the Aggregator aggregate this number of messages.

## Message Headers

The Minio component supports 22 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMinioBucketName** (common) Constant: [`BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#BUCKET_NAME) | Producer: The bucket Name which this object will be stored or which will be used for the current operation. Consumer: The name of the bucket in which this object is contained. |  | String |
| **CamelMinioDestinationBucketName** (producer) Constant: [`DESTINATION_BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#DESTINATION_BUCKET_NAME) | The bucket Destination Name which will be used for the current operation. |  | String |
| **CamelMinioContentControl** (common) Constant: [`CACHE_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#CACHE_CONTROL) | Producer: The content control of this object. Consumer: The optional Cache-Control HTTP header which allows the user to specify caching behavior along the HTTP request/reply chain. |  | String |
| **CamelMinioContentDisposition** (common) Constant: [`CONTENT_DISPOSITION`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#CONTENT_DISPOSITION) | Producer: The content disposition of this object. Consumer: The optional Content-Disposition HTTP header, which specifies presentational information such as the recommended filename for the object to be saved as. |  | String |
| **CamelMinioContentEncoding** (common) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#CONTENT_ENCODING) | Producer: The content encoding of this object. Consumer: The optional Content-Encoding HTTP header specifying what content encodings have been applied to the object and what decoding mechanisms must be applied in order to obtain the media-type referenced by the Content-Type field. |  | String |
| **CamelMinioContentLength** (common) Constant: [`CONTENT_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#CONTENT_LENGTH) | Producer: The content length of this object. Consumer: The Content-Length HTTP header indicating the size of the associated object in bytes. |  | Long |
| **CamelMinioContentMD5** (common) Constant: [`CONTENT_MD5`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#CONTENT_MD5) | Producer: The md5 checksum of this object. Consumer: The base64 encoded 128-bit MD5 digest of the associated object (content - not including headers) according to RFC 1864. This data is used as a message integrity check to verify that the data received by Minio is the same data that the caller sent. |  | String |
| **CamelMinioContentType** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#CONTENT_TYPE) | Producer: The content type of this object. Consumer: The Content-Type HTTP header, which indicates the type of content stored in the associated object. The value of this header is a standard MIME type. |  | String |
| **CamelMinioETag** (common) Constant: [`E_TAG`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#E_TAG) | Producer: The ETag value for the newly uploaded object. Consumer: The hex encoded 128-bit MD5 digest of the associated object according to RFC 1864. This data is used as an integrity check to verify that the data received by the caller is the same data that was sent by Minio. |  | String |
| **CamelMinioObjectName** (common) Constant: [`OBJECT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#OBJECT_NAME) | Producer: The key under which this object will be stored or which will be used for the current operation. Consumer: The key under which this object is stored. |  | String |
| **CamelMinioDestinationObjectName** (producer) Constant: [`DESTINATION_OBJECT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#DESTINATION_OBJECT_NAME) | The Destination key which will be used for the current operation. |  | String |
| **CamelMinioLastModified** (common) Constant: [`LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#LAST_MODIFIED) | Producer: The last modified timestamp of this object. Consumer: The value of the Last-Modified header, indicating the date and time at which Minio last recorded a modification to the associated object. |  | Date |
| **CamelMinioStorageClass** (producer) Constant: [`STORAGE_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#STORAGE_CLASS) | The storage class of this object. |  | String |
| **CamelMinioVersionId** (common) Constant: [`VERSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#VERSION_ID) | Producer: The version Id of the object to be stored or returned from the current operation. Consumer: The version ID of the associated Minio object if available. Version IDs are only assigned to objects when an object is uploaded to an Minio bucket that has object versioning enabled. |  | String |
| **CamelMinioCannedAcl** (producer) Constant: [`CANNED_ACL`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#CANNED_ACL) | The canned acl that will be applied to the object. see com.amazonaws.services.s3.model.CannedAccessControlList for allowed values. |  | String |
| **CamelMinioOperation** (producer) Constant: [`MINIO_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#MINIO_OPERATION) | 
The operation to perform.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteObjects
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   getPartialObject
    
-   createDownloadLink
    
-   createUploadLink
    





 |  | MinioOperations |
| **CamelMinioServerSideEncryption** (common) Constant: [`SERVER_SIDE_ENCRYPTION`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#SERVER_SIDE_ENCRYPTION) | Producer: Sets the server-side encryption algorithm when encrypting the object using Minio-managed keys. For example use AES256. Consumer: The server-side encryption algorithm when encrypting the object using Minio-managed keys. |  | String |
| **CamelMinioExpirationTime** (common) Constant: [`EXPIRATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#EXPIRATION_TIME) | The expiration time. |  | String |
| **CamelMinioReplicationStatus** (common) Constant: [`REPLICATION_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#REPLICATION_STATUS) | The replication status. |  | String |
| **CamelMinioOffset** (producer) Constant: [`OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#OFFSET) | The offset. |  | String |
| **CamelMinioLength** (producer) Constant: [`LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#LENGTH) | The length. |  | String |
| **CamelMinioPresignedURLExpirationTime** (producer) Constant: [`PRESIGNED_URL_EXPIRATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-minio/latest/org/apache/camel/component/minio/MinioConstants.html#PRESIGNED_URL_EXPIRATION_TIME) | Expiration of minio presigned url in Seconds. |  | int |

### Minio Producer operations

Camel-Minio component provides the following operation on the producer side:

-   copyObject
    
-   deleteObject
    
-   deleteObjects
    
-   listBuckets
    
-   deleteBucket
    
-   listObjects
    
-   getObject (this will return a MinioObject instance)
    
-   getObjectRange (this will return a MinioObject instance)
    
-   createDownloadLink (this will return a Presigned download Url)
    
-   createUploadLink (this will return a Presigned upload url)
    

### Advanced Minio configuration

If your Camel Application is running behind a firewall or if you need to have more control over the `MinioClient` instance configuration, you can create your own instance and refer to it in your Camel minio component configuration:

```java
from("minio://MyBucket?minioClient=#client&delay=5000&maxMessagesPerPoll=5")
.to("mock:result");
```

### Minio Producer Operation examples

-   CopyObject: this operation copy an object from one bucket to a different one
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(MinioConstants.DESTINATION_BUCKET_NAME, "camelDestinationBucket");
          exchange.getIn().setHeader(MinioConstants.OBJECT_NAME, "camelKey");
          exchange.getIn().setHeader(MinioConstants.DESTINATION_OBJECT_NAME, "camelDestinationKey");
      }
  })
  .to("minio://mycamelbucket?minioClient=#minioClient&operation=copyObject")
  .to("mock:result");
```

This operation will copy the object with the name expressed in the header camelDestinationKey to the camelDestinationBucket bucket, from the bucket mycamelbucket.

-   DeleteObject: this operation deletes an object from a bucket
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(MinioConstants.OBJECT_NAME, "camelKey");
      }
  })
  .to("minio://mycamelbucket?minioClient=#minioClient&operation=deleteObject")
  .to("mock:result");
```

This operation will delete the object camelKey from the bucket mycamelbucket.

-   ListBuckets: this operation list the buckets for this account in this region
    

```java
  from("direct:start")
  .to("minio://mycamelbucket?minioClient=#minioClient&operation=listBuckets")
  .to("mock:result");
```

This operation will list the buckets for this account

-   DeleteBucket: this operation delete the bucket specified as URI parameter or header
    

```java
  from("direct:start")
  .to("minio://mycamelbucket?minioClient=#minioClient&operation=deleteBucket")
  .to("mock:result");
```

This operation will delete the bucket mycamelbucket

-   ListObjects: this operation list object in a specific bucket
    

```java
  from("direct:start")
  .to("minio://mycamelbucket?minioClient=#minioClient&operation=listObjects")
  .to("mock:result");
```

This operation will list the objects in the mycamelbucket bucket

-   GetObject: this operation get a single object in a specific bucket
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(MinioConstants.OBJECT_NAME, "camelKey");
      }
  })
  .to("minio://mycamelbucket?minioClient=#minioClient&operation=getObject")
  .to("mock:result");
```

This operation will return an MinioObject instance related to the camelKey object in mycamelbucket bucket.

-   GetObjectRange: this operation get a single object range in a specific bucket
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(MinioConstants.OBJECT_NAME, "camelKey");
          exchange.getIn().setHeader(MinioConstants.OFFSET, "0");
          exchange.getIn().setHeader(MinioConstants.LENGTH, "9");
      }
  })
  .to("minio://mycamelbucket?minioClient=#minioClient&operation=getObjectRange")
  .to("mock:result");
```

This operation will return an MinioObject instance related to the camelKey object in mycamelbucket bucket, containing bytes from 0 to 9.

-   createDownloadLink: this operation will return a presigned url through which a file can be downloaded using GET method
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(MinioConstants.OBJECT_NAME, "camelKey");
          exchange.getIn().setHeader(MinioConstants.PRESIGNED_URL_EXPIRATION_TIME, 60 * 60);
      }
  })
  .to("minio://mycamelbucket?minioClient=#minioClient&operation=createDownloadLink")
  .to("mock:result");
```

-   createUploadLink: this operation will return a presigned url through which a file can be uploaded using PUT method
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(MinioConstants.OBJECT_NAME, "camelKey");
          exchange.getIn().setHeader(MinioConstants.PRESIGNED_URL_EXPIRATION_TIME, 60 * 60);
      }
  })
  .to("minio://mycamelbucket?minioClient=#minioClient&operation=createUploadLink")
  .to("mock:result");
```

createDownLink and createUploadLink have a default expiry of 3600s which can be overridden by setting the header MinioConstants.PRESIGNED\_URL\_EXPIRATION\_TIME (value in seconds)

## Bucket Autocreation

With the option `autoCreateBucket` users are able to avoid the autocreation of a Minio Bucket in case it doesn’t exist. The default for this option is `true`. If set to false any operation on a not-existent bucket in Minio won’t be successful, and an error will be returned.

## Automatic detection of Minio client in registry

The component is capable of detecting the presence of a Minio bean into the registry. If it’s the only instance of that type it will be used as client, and you won’t have to define it as uri parameter, like the example above. This may be really useful for smarter configuration of the endpoint.

## Moving stuff between a bucket and another bucket

Some users like to consume stuff from a bucket and move the content in a different one without using the copyObject feature of this component. If this is case for you, don’t forget to remove the bucketName header from the incoming exchange of the consumer, otherwise the file will always be overwritten on the same original bucket.

## MoveAfterRead consumer option

In addition to deleteAfterRead it has been added another option, moveAfterRead. With this option enabled the consumed object will be moved to a target destinationBucket instead of being only deleted. This will require specifying the destinationBucket option. As example:

```java
  from("minio://mycamelbucket?minioClient=#minioClient&moveAfterRead=true&destinationBucketName=myothercamelbucket")
  .to("mock:result");
```

In this case the objects consumed will be moved to myothercamelbucket bucket and deleted from the original one (because of deleteAfterRead set to true as default).

## Using a POJO as body

Sometimes build a Minio Request can be complex, because of multiple options. We introduce the possibility to use a POJO as body. In Minio there are multiple operations you can submit, as an example for List brokers request, you can do something like:

```java
from("direct:minio")
     .setBody(ListObjectsArgs.builder()
                    .bucket(bucketName)
                    .recursive(getConfiguration().isRecursive())))
     .to("minio://test?minioClient=#minioClient&operation=listObjects&pojoRequest=true")
```

In this way you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-minio</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using minio with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-minio-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 48 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.minio.access-key** | Amazon AWS Secret Access Key or Minio Access Key. If not set camel will connect to service for anonymous access. |  | String |
| **camel.component.minio.auto-close-body** | If this option is true and includeBody is true, then the MinioObject.close() method will be called on exchange completion. This option is strongly related to includeBody option. In case of setting includeBody to true and autocloseBody to false, it will be up to the caller to close the MinioObject stream. Setting autocloseBody to true, will close the MinioObject stream automatically. | true | Boolean |
| **camel.component.minio.auto-create-bucket** | Setting the autocreation of the bucket if bucket name not exist. | true | Boolean |
| **camel.component.minio.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.minio.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.minio.bypass-governance-mode** | Set this flag if you want to bypassGovernanceMode when deleting a particular object. | false | Boolean |
| **camel.component.minio.configuration** | The component configuration. The option is a org.apache.camel.component.minio.MinioConfiguration type. |  | MinioConfiguration |
| **camel.component.minio.custom-http-client** | Set custom HTTP client for authenticated access. The option is a okhttp3.OkHttpClient type. |  | OkHttpClient |
| **camel.component.minio.delete-after-read** | Delete objects from Minio after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieve over and over again on the polls. Therefore you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the MinioConstants#BUCKET\_NAME and MinioConstants#OBJECT\_NAME headers, or only the MinioConstants#OBJECT\_NAME header. | true | Boolean |
| **camel.component.minio.delete-after-write** | Delete file object after the Minio file has been uploaded. | false | Boolean |
| **camel.component.minio.delimiter** | The delimiter which is used in the ListObjectsRequest to only consume objects we are interested in. |  | String |
| **camel.component.minio.destination-bucket-name** | Destination bucket name. |  | String |
| **camel.component.minio.destination-object-name** | Destination object name. |  | String |
| **camel.component.minio.enabled** | Whether to enable auto configuration of the minio component. This is enabled by default. |  | Boolean |
| **camel.component.minio.endpoint** | Endpoint can be an URL, domain name, IPv4 address or IPv6 address. |  | String |
| **camel.component.minio.include-body** | If it is true, the exchange body will be set to a stream to the contents of the file. If false, the headers will be set with the Minio object metadata, but the body will be null. This option is strongly related to autocloseBody option. In case of setting includeBody to true and autocloseBody to false, it will be up to the caller to close the MinioObject stream. Setting autocloseBody to true, will close the MinioObject stream automatically. | true | Boolean |
| **camel.component.minio.include-folders** | The flag which is used in the ListObjectsRequest to set include folders. | false | Boolean |
| **camel.component.minio.include-user-metadata** | The flag which is used in the ListObjectsRequest to get objects with user meta data. | false | Boolean |
| **camel.component.minio.include-versions** | The flag which is used in the ListObjectsRequest to get objects with versioning. | false | Boolean |
| **camel.component.minio.key-name** | Setting the key name for an element in the bucket through endpoint parameter. |  | String |
| **camel.component.minio.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.minio.length** | Number of bytes of object data from offset. |  | Long |
| **camel.component.minio.match-e-tag** | Set match ETag parameter for get object(s). |  | String |
| **camel.component.minio.max-connections** | Set the maxConnections parameter in the minio client configuration. | 60 | Integer |
| **camel.component.minio.max-messages-per-poll** | Gets the maximum number of messages as a limit to poll at each polling. Gets the maximum number of messages as a limit to poll at each polling. The default value is 10. Use 0 or a negative number to set it as unlimited. | 10 | Integer |
| **camel.component.minio.minio-client** | Reference to a Minio Client object in the registry. The option is a io.minio.MinioClient type. |  | MinioClient |
| **camel.component.minio.modified-since** | Set modified since parameter for get object(s). The option is a java.time.ZonedDateTime type. |  | ZonedDateTime |
| **camel.component.minio.move-after-read** | Move objects from bucket to a different bucket after they have been retrieved. To accomplish the operation the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | Boolean |
| **camel.component.minio.not-match-e-tag** | Set not match ETag parameter for get object(s). |  | String |
| **camel.component.minio.object-lock** | Set when creating new bucket. | false | Boolean |
| **camel.component.minio.object-name** | To get the object from the bucket with the given object name. |  | String |
| **camel.component.minio.offset** | Start byte position of object data. |  | Long |
| **camel.component.minio.operation** | The operation to do in case the user don’t want to do only an upload. |  | MinioOperations |
| **camel.component.minio.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.minio.policy** | The policy for this queue to set in the method. |  | String |
| **camel.component.minio.prefix** | Object name starts with prefix. |  | String |
| **camel.component.minio.proxy-port** | TCP/IP port number. 80 and 443 are used as defaults for HTTP and HTTPS. |  | Integer |
| **camel.component.minio.recursive** | List recursively than directory structure emulation. | false | Boolean |
| **camel.component.minio.region** | The region in which Minio client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1). You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.minio.secret-key** | Amazon AWS Access Key Id or Minio Secret Key. If not set camel will connect to service for anonymous access. |  | String |
| **camel.component.minio.secure** | Flag to indicate to use secure connection to minio service or not. | false | Boolean |
| **camel.component.minio.server-side-encryption** | Server-side encryption. The option is a io.minio.ServerSideEncryption type. |  | ServerSideEncryption |
| **camel.component.minio.server-side-encryption-customer-key** | Server-side encryption for source object while copy/move objects. The option is a io.minio.ServerSideEncryptionCustomerKey type. |  | ServerSideEncryptionCustomerKey |
| **camel.component.minio.start-after** | list objects in bucket after this object name. |  | String |
| **camel.component.minio.storage-class** | The storage class to set in the request. |  | String |
| **camel.component.minio.un-modified-since** | Set un modified since parameter for get object(s). The option is a java.time.ZonedDateTime type. |  | ZonedDateTime |
| **camel.component.minio.use-version1** | when true, version 1 of REST API is used. | false | Boolean |
| **camel.component.minio.version-id** | Set specific version\_ID of a object when deleting the object. |  | String |