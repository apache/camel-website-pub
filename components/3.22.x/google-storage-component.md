# Google Storage

**Since Camel 3.9**

**Both producer and consumer are supported**

The Google Storage component provides access to [Google Cloud Storage](https://cloud.google.com/storage/) via the [google java storage library](https://github.com/googleapis/java-storage).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-storage</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

## Authentication Configuration

Google Storage component authentication is targeted for use with the GCP Service Accounts. For more information please refer to [Google Storage Auth Guide](https://cloud.google.com/storage/docs/reference/libraries#setting_up_authentication).

When you have the **service account key** you can provide authentication credentials to your application code. Google security credentials can be set through the component endpoint:

```java
String endpoint = "google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json";
```

Or by providing the path to the GCP credentials file location:

Provide authentication credentials to your application code by setting the environment variable `GOOGLE_APPLICATION_CREDENTIALS` :

export GOOGLE\_APPLICATION\_CREDENTIALS="/home/user/Downloads/my-key.json"

## URI Format

google-storage://bucketNameOrArn?\[options\]

By default the bucket will be created if it don’t already exists.  
You can append query options to the URI in the following format, ?options=value&option2=value&…​

For example in order to read file `hello.txt` from bucket `myCamelBucket`, use the following snippet:

```java
from("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json&objectName=hello.txt")
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

The Google Storage component supports 18 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateBucket** (common) | Setting the autocreation of the bucket bucketName. | true | boolean |
| **configuration** (common) | The component configuration. |  | GoogleCloudStorageConfiguration |
| **serviceAccountKey** (common) | The Service account key that can be used as credentials for the Storage client. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **storageClass** (common) | The Cloud Storage class to use when creating the new buckets. | STANDARD | StorageClass |
| **storageClient** (common) | **Autowired** The storage client. |  | Storage |
| **storageLocation** (common) | The Cloud Storage location to use when creating the new buckets. | US-EAST1 | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **deleteAfterRead** (consumer) | Delete objects from the bucket after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieve over and over again on the polls. | true | boolean |
| **destinationBucket** (consumer) | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | String |
| **downloadFileName** (consumer) | The folder or filename to use when downloading the blob. By default, this specifies the folder name, and the name of the file is the blob name. For example, setting this to mydownload will be the same as setting mydownload/$\\{file:name}. You can use dynamic expressions for fine-grained control. For example, you can specify $\\{date:now:yyyyMMdd}/$\\{file:name} to store the blob in sub folders based on today’s day. Only $\\{file:name} and $\\{file:name.noext} is supported as dynamic tokens for the blob name. |  | String |
| **filter** (consumer) | A regular expression to include only blobs with name matching it. |  | String |
| **includeBody** (consumer) | If it is true, the Object exchange will be consumed and put into the body. If false the Object stream will be put raw into the body and the headers will be set with the object metadata. | true | boolean |
| **includeFolders** (consumer) | If it is true, the folders/directories will be consumed. If it is false, they will be ignored, and Exchanges will not be created for those. | true | boolean |
| **moveAfterRead** (consumer) | Move objects from the origin bucket to a different bucket after they have been retrieved. To accomplish the operation the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **objectName** (producer) | The Object name inside the bucket. |  | String |
| **operation** (producer) | 
Set the operation for the producer.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   createDownloadLink
    





 |  | GoogleCloudStorageOperations |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Google Storage endpoint is configured using URI syntax:

google-storage:bucketName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bucketName** (common) | **Required** Bucket name or ARN. |  | String |

### Query Parameters (34 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateBucket** (common) | Setting the autocreation of the bucket bucketName. | true | boolean |
| **serviceAccountKey** (common) | The Service account key that can be used as credentials for the Storage client. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **storageClass** (common) | The Cloud Storage class to use when creating the new buckets. | STANDARD | StorageClass |
| **storageClient** (common) | **Autowired** The storage client. |  | Storage |
| **storageLocation** (common) | The Cloud Storage location to use when creating the new buckets. | US-EAST1 | String |
| **deleteAfterRead** (consumer) | Delete objects from the bucket after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieve over and over again on the polls. | true | boolean |
| **destinationBucket** (consumer) | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | String |
| **downloadFileName** (consumer) | The folder or filename to use when downloading the blob. By default, this specifies the folder name, and the name of the file is the blob name. For example, setting this to mydownload will be the same as setting mydownload/$\\{file:name}. You can use dynamic expressions for fine-grained control. For example, you can specify $\\{date:now:yyyyMMdd}/$\\{file:name} to store the blob in sub folders based on today’s day. Only $\\{file:name} and $\\{file:name.noext} is supported as dynamic tokens for the blob name. |  | String |
| **filter** (consumer) | A regular expression to include only blobs with name matching it. |  | String |
| **includeBody** (consumer) | If it is true, the Object exchange will be consumed and put into the body. If false the Object stream will be put raw into the body and the headers will be set with the object metadata. | true | boolean |
| **includeFolders** (consumer) | If it is true, the folders/directories will be consumed. If it is false, they will be ignored, and Exchanges will not be created for those. | true | boolean |
| **moveAfterRead** (consumer) | Move objects from the origin bucket to a different bucket after they have been retrieved. To accomplish the operation the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
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
| **objectName** (producer) | The Object name inside the bucket. |  | String |
| **operation** (producer) | 

Set the operation for the producer.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   createDownloadLink
    





 |  | GoogleCloudStorageOperations |
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

## Usage

## Message Headers

The Google Storage component supports 26 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleCloudStorageOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   createDownloadLink
    





 |  | GoogleCloudStorageOperations |
| **CamelGoogleCloudStorageBucketName** (producer) Constant: [`BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#BUCKET_NAME) | The bucket Name which this object will be stored or which will be used for the current operation. |  | String |
| **CamelGoogleCloudStorageObjectName** (producer) Constant: [`OBJECT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#OBJECT_NAME) | The object Name which will be used for the current operation. |  | String |
| **CamelGoogleCloudStorageDestinationObjectName** (producer) Constant: [`DESTINATION_OBJECT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#DESTINATION_OBJECT_NAME) | The object Destination Name which will be used for the current operation. |  | String |
| **CamelGoogleCloudStorageDestinationBucketName** (producer) Constant: [`DESTINATION_BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#DESTINATION_BUCKET_NAME) | The bucket Destination Name which will be used for the current operation. |  | String |
| **CamelGoogleCloudStorageDownloadLinkExpirationTime** (producer) Constant: [`DOWNLOAD_LINK_EXPIRATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#DOWNLOAD_LINK_EXPIRATION_TIME) | The time in millisecond the download link will be valid. | 300000 | Long |
| **CamelGoogleCloudStorageContentLength** (common) Constant: [`CONTENT_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#CONTENT_LENGTH) | The content length of this object. |  | Long |
| **CamelGoogleCloudStorageContentType** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#CONTENT_TYPE) | The content type of this object. |  | String |
| **CamelGoogleCloudStorageCacheControl** (common) Constant: [`CACHE_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#CACHE_CONTROL) | The Cache-Control metadata can specify two different aspects of how data is served from Cloud Storage: whether the data can be cached and whether the data can be transformed. |  | String |
| **CamelGoogleCloudStorageContentDisposition** (common) Constant: [`CONTENT_DISPOSITION`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#CONTENT_DISPOSITION) | The content disposition of this object. |  | String |
| **CamelGoogleCloudStorageContentEncoding** (common) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#CONTENT_ENCODING) | The content encoding of this object. |  | String |
| **CamelGoogleCloudStorageContentMd5** (common) Constant: [`CONTENT_MD5`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#CONTENT_MD5) | The md5 checksum of this object. |  | String |
| **CamelFileName** (consumer) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#FILE_NAME) | The name of the blob. |  | String |
| **CamelGoogleCloudStorageComponentCount** (consumer) Constant: [`METADATA_COMPONENT_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_COMPONENT_COUNT) | The component count of this object. |  | Integer |
| **CamelGoogleCloudStorageContentLanguage** (consumer) Constant: [`METADATA_CONTENT_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_CONTENT_LANGUAGE) | The Content-Language metadata indicates the language(s) that the object is intended for. |  | String |
| **CamelGoogleCloudStorageCustomTime** (consumer) Constant: [`METADATA_CUSTOM_TIME`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_CUSTOM_TIME) | The Custom-Time metadata is a user-specified date and time represented in the RFC 3339 format YYYY-MM-DD’T’HH:MM:SS.SS’Z' or YYYY-MM-DD’T’HH:MM:SS’Z' when milliseconds are zero. This metadata is typically set in order to use the DaysSinceCustomTime condition in Object Lifecycle Management. |  | Long |
| **CamelGoogleCloudStorageCrc32cHex** (consumer) Constant: [`METADATA_CRC32C_HEX`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_CRC32C_HEX) | The CRC32c of the object. |  | String |
| **CamelGoogleCloudStorageETag** (common) Constant: [`METADATA_ETAG`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_ETAG) | The ETag for the Object. |  | String |
| **CamelGoogleCloudStorageGeneration** (consumer) Constant: [`METADATA_GENERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_GENERATION) | Is the generation number of the object for which you are retrieving information. |  | Long |
| **CamelGoogleCloudStorageBlobId** (consumer) Constant: [`METADATA_BLOB_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_BLOB_ID) | The blob id of the object. |  | BlobId |
| **CamelGoogleCloudStorageKmsKeyName** (consumer) Constant: [`METADATA_KMS_KEY_NAME`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_KMS_KEY_NAME) | The KMS key name. |  | String |
| **CamelGoogleCloudStorageMediaLink** (consumer) Constant: [`METADATA_MEDIA_LINK`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_MEDIA_LINK) | The media link. |  | String |
| **CamelGoogleCloudStorageMetageneration** (consumer) Constant: [`METADATA_METAGENERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_METAGENERATION) | The metageneration of the object. |  | Long |
| **CamelGoogleCloudStorageStorageClass** (consumer) Constant: [`METADATA_STORAGE_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_STORAGE_CLASS) | The storage class of the object. |  | StorageClass |
| **CamelGoogleCloudStorageCreateTime** (consumer) Constant: [`METADATA_CREATE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_CREATE_TIME) | The creation time of the object. |  | Long |
| **CamelGoogleCloudStorageLastUpdate** (consumer) Constant: [`METADATA_LAST_UPDATE`](https://javadoc.io/doc/org.apache.camel/camel-google-storage/latest/org/apache/camel/component/google/storage/GoogleCloudStorageConstants.html#METADATA_LAST_UPDATE) | The last update of the object. |  | Date |

### Google Storage Producer operations

Google Storage component provides the following operation on the producer side:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   createDownloadLink
    

If you don’t specify an operation explicitly the producer will a file upload.

### Advanced component configuration

If you need to have more control over the `storageClient` instance configuration, you can create your own instance and refer to it in your Camel google-storage component configuration:

```java
from("google-storage://myCamelBucket?storageClient=#client")
.to("mock:result");
```

### Google Storage Producer Operation examples

-   File Upload: This operation will upload a file to the Google Storage based on the body content
    

```java
//upload a file
byte[] payload = "Camel rocks!".getBytes();
ByteArrayInputStream bais = new ByteArrayInputStream(payload);
from("direct:start")
.process( exchange -> {
    exchange.getIn().setHeader(GoogleCloudStorageConstants.OBJECT_NAME, "camel.txt");
    exchange.getIn().setBody(bais);
})
.to("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json")
.log("uploaded file object:${header.CamelGoogleCloudStorageObjectName}, body:${body}");
```

This operation will upload the file camel.txt with the content "Camel rocks!" in the myCamelBucket bucket

-   CopyObject: this operation copy an object from one bucket to a different one
    

```java
  from("direct:start").process( exchange -> {
    exchange.getIn().setHeader(GoogleCloudStorageConstants.OPERATION, GoogleCloudStorageOperations.copyObject);
    exchange.getIn().setHeader(GoogleCloudStorageConstants.OBJECT_NAME, "camel.txt" );
    exchange.getIn().setHeader(GoogleCloudStorageConstants.DESTINATION_BUCKET_NAME, "myCamelBucket_dest");
    exchange.getIn().setHeader(GoogleCloudStorageConstants.DESTINATION_OBJECT_NAME, "camel_copy.txt");
  })
  .to("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json")
  .to("mock:result");
```

This operation will copy the object with the name expressed in the header DESTINATION\_OBJECT\_NAME to the DESTINATION\_BUCKET\_NAME bucket, from the bucket myCamelBucket.

-   DeleteObject: this operation deletes an object from a bucket
    

```java
  from("direct:start").process( exchange -> {
    exchange.getIn().setHeader(GoogleCloudStorageConstants.OPERATION, GoogleCloudStorageOperations.deleteObject);
    exchange.getIn().setHeader(GoogleCloudStorageConstants.OBJECT_NAME, "camel.txt" );
  })
  .to("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json")
  .to("mock:result");
```

This operation will delete the object from the bucket myCamelBucket.

-   ListBuckets: this operation list the buckets for this account in this region
    

```java
from("direct:start")
.to("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json&operation=listBuckets")
.to("mock:result");
```

This operation will list the buckets for this account.

-   DeleteBucket: this operation delete the bucket specified as URI parameter or header
    

```java
from("direct:start")
.to("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json&operation=deleteBucket")
.to("mock:result");
```

This operation will delete the bucket myCamelBucket.

-   ListObjects: this operation list object in a specific bucket
    

```java
from("direct:start")
.to("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json&operation=listObjects")
.to("mock:result");
```

This operation will list the objects in the myCamelBucket bucket.

-   GetObject: this operation get a single object in a specific bucket
    

```java
from("direct:start")
.process( exchange -> {
  exchange.getIn().setHeader(GoogleCloudStorageConstants.OBJECT_NAME, "camel.txt");
})
.to("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json&operation=getObject")
.to("mock:result");
```

This operation will return an Blob objct instance related to the OBJECT\_NAME object in myCamelBucket bucket.

-   CreateDownloadLink: this operation will return a download link
    

```java
from("direct:start")
.process( exchange -> {
  exchange.getIn().setHeader(GoogleCloudStorageConstants.OBJECT_NAME, "camel.txt" );
  exchange.getIn().setHeader(GoogleCloudStorageConstants.DOWNLOAD_LINK_EXPIRATION_TIME, 86400000L); //1 day
})
.to("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json&operation=createDownloadLink")
.to("mock:result");
```

This operation will return a download link url for the file OBJECT\_NAME in the bucket myCamelBucket. It’s possible to specify the expiration time for the created link through the header DOWNLOAD\_LINK\_EXPIRATION\_TIME. If not specified, by default it is 5 minutes.

## Bucket Autocreation

With the option `autoCreateBucket` users are able to avoid the autocreation of a Bucket in case it doesn’t exist. The default for this option is `true`. If set to false any operation on a not-existent bucket won’t be successful and an error will be returned.

## MoveAfterRead consumer option

In addition to deleteAfterRead it has been added another option, moveAfterRead. With this option enabled the consumed object will be moved to a target destinationBucket instead of being only deleted. This will require specifying the destinationBucket option. As example:

```java
  from("google-storage://myCamelBucket?serviceAccountKey=/home/user/Downloads/my-key.json"
    + "&autoCreateBucket=true"
    + "&destinationBucket=myCamelProcessedBucket"
    + "&moveAfterRead=true"
    + "&deleteAfterRead=true"
    + "&includeBody=true"
  )
  .to("mock:result");
```

In this case the objects consumed will be moved to myCamelProcessedBucket bucket and deleted from the original one (because of deleteAfterRead).

## Spring Boot Auto-Configuration

When using google-storage with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-storage-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 19 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-storage.auto-create-bucket** | Setting the autocreation of the bucket bucketName. | true | Boolean |
| **camel.component.google-storage.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-storage.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-storage.configuration** | The component configuration. The option is a org.apache.camel.component.google.storage.GoogleCloudStorageConfiguration type. |  | GoogleCloudStorageConfiguration |
| **camel.component.google-storage.delete-after-read** | Delete objects from the bucket after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieve over and over again on the polls. | true | Boolean |
| **camel.component.google-storage.destination-bucket** | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | String |
| **camel.component.google-storage.download-file-name** | The folder or filename to use when downloading the blob. By default, this specifies the folder name, and the name of the file is the blob name. For example, setting this to mydownload will be the same as setting mydownload/$\\{file:name}. You can use dynamic expressions for fine-grained control. For example, you can specify $\\{date:now:yyyyMMdd}/$\\{file:name} to store the blob in sub folders based on today’s day. Only $\\{file:name} and $\\{file:name.noext} is supported as dynamic tokens for the blob name. |  | String |
| **camel.component.google-storage.enabled** | Whether to enable auto configuration of the google-storage component. This is enabled by default. |  | Boolean |
| **camel.component.google-storage.filter** | A regular expression to include only blobs with name matching it. |  | String |
| **camel.component.google-storage.include-body** | If it is true, the Object exchange will be consumed and put into the body. If false the Object stream will be put raw into the body and the headers will be set with the object metadata. | true | Boolean |
| **camel.component.google-storage.include-folders** | If it is true, the folders/directories will be consumed. If it is false, they will be ignored, and Exchanges will not be created for those. | true | Boolean |
| **camel.component.google-storage.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-storage.move-after-read** | Move objects from the origin bucket to a different bucket after they have been retrieved. To accomplish the operation the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | Boolean |
| **camel.component.google-storage.object-name** | The Object name inside the bucket. |  | String |
| **camel.component.google-storage.operation** | Set the operation for the producer. |  | GoogleCloudStorageOperations |
| **camel.component.google-storage.service-account-key** | The Service account key that can be used as credentials for the Storage client. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **camel.component.google-storage.storage-class** | The Cloud Storage class to use when creating the new buckets. The option is a com.google.cloud.storage.StorageClass type. |  | StorageClass |
| **camel.component.google-storage.storage-client** | The storage client. The option is a com.google.cloud.storage.Storage type. |  | Storage |
| **camel.component.google-storage.storage-location** | The Cloud Storage location to use when creating the new buckets. | US-EAST1 | String |