# IBM Cloud Object Storage

**Since Camel 4.16**

**Both producer and consumer are supported**

The IBM COS component supports storing and retrieving objects from/to [IBM Cloud Object Storage](https://www.ibm.com/cloud/object-storage).

Prerequisites

You must have a valid IBM Cloud account, and be signed up to use IBM Cloud Object Storage. More information is available at [IBM Cloud Object Storage](https://www.ibm.com/cloud/object-storage).

## URI Format

ibm-cos://bucketName\[?options\]

The bucket will be created if it doesn’t already exist.

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

The IBM Cloud Object Storage component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateBucket** (common) | Automatically create the bucket if it doesn’t exist. | false | boolean |
| **configuration** (common) | The component configuration. |  | IBMCOSConfiguration |
| **delimiter** (common) | The delimiter to use for listing objects. |  | String |
| **endpointUrl** (common) | IBM COS Endpoint URL (e.g., [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)) Note that some operations requires to use a regional endpoint URL instead of a cross-region one. |  | String |
| **location** (common) | IBM COS Location/Region (e.g., us-south, eu-gb). |  | String |
| **prefix** (common) | The prefix to use for listing objects. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **deleteAfterRead** (consumer) | Delete the object from IBM COS after it has been retrieved. | true | boolean |
| **destinationBucket** (consumer) | The destination bucket to move objects to. |  | String |
| **destinationBucketPrefix** (consumer) | The prefix to add to objects in the destination bucket. |  | String |
| **destinationBucketSuffix** (consumer) | The suffix to add to objects in the destination bucket. |  | String |
| **fileName** (consumer) | To get the object from the bucket with the given file name. |  | String |
| **includeBody** (consumer) | Include the object body in the exchange. | true | boolean |
| **includeFolders** (consumer) | Include folders/directories when listing objects. | true | boolean |
| **moveAfterRead** (consumer) | Move the object to a different bucket after it has been retrieved. | false | boolean |
| **autocloseBody** (consumer (advanced)) | Whether to automatically close the object input stream after processing. | true | boolean |
| **deleteAfterWrite** (producer) | Delete the object from the local filesystem after uploading. | false | boolean |
| **keyName** (producer) | The key name for the object. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **multiPartUpload** (producer) | Use multi-part upload for large files. | false | boolean |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteObjects
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   getObjectRange
    
-   headBucket
    
-   createBucket
    
-   putObject
    





 |  | IBMCOSOperations |
| **partSize** (producer) | Part size for multi-part uploads (default 25MB). | 26214400 | long |
| **storageClass** (producer) | The storage class to use when storing objects (e.g., STANDARD, VAULT, COLD, FLEX). |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **cosClient** (advanced) | **Autowired** Reference to an IBM COS Client instance in the registry. |  | AmazonS3 |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **apiKey** (security) | IBM Cloud API Key for authentication. |  | String |
| **serviceInstanceId** (security) | IBM COS Service Instance ID (CRN). |  | String |

## Endpoint Options

The IBM Cloud Object Storage endpoint is configured using URI syntax:

ibm-cos:bucketName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bucketName** (common) | **Required** Bucket name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateBucket** (common) | Automatically create the bucket if it doesn’t exist. | false | boolean |
| **delimiter** (common) | The delimiter to use for listing objects. |  | String |
| **endpointUrl** (common) | IBM COS Endpoint URL (e.g., [https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)) Note that some operations requires to use a regional endpoint URL instead of a cross-region one. |  | String |
| **location** (common) | IBM COS Location/Region (e.g., us-south, eu-gb). |  | String |
| **prefix** (common) | The prefix to use for listing objects. |  | String |
| **deleteAfterRead** (consumer) | Delete the object from IBM COS after it has been retrieved. | true | boolean |
| **destinationBucket** (consumer) | The destination bucket to move objects to. |  | String |
| **destinationBucketPrefix** (consumer) | The prefix to add to objects in the destination bucket. |  | String |
| **destinationBucketSuffix** (consumer) | The suffix to add to objects in the destination bucket. |  | String |
| **fileName** (consumer) | To get the object from the bucket with the given file name. |  | String |
| **includeBody** (consumer) | Include the object body in the exchange. | true | boolean |
| **includeFolders** (consumer) | Include folders/directories when listing objects. | true | boolean |
| **maxMessagesPerPoll** (consumer) | Gets the maximum number of messages as a limit to poll at each polling. | 10 | int |
| **moveAfterRead** (consumer) | Move the object to a different bucket after it has been retrieved. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **autocloseBody** (consumer (advanced)) | Whether to automatically close the object input stream after processing. | true | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **inProgressRepository** (consumer (advanced)) | A pluggable in-progress repository to track objects being consumed. |  | IdempotentRepository |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **deleteAfterWrite** (producer) | Delete the object from the local filesystem after uploading. | false | boolean |
| **keyName** (producer) | The key name for the object. |  | String |
| **multiPartUpload** (producer) | Use multi-part upload for large files. | false | boolean |
| **operation** (producer) | 

The operation to perform.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteObjects
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   getObjectRange
    
-   headBucket
    
-   createBucket
    
-   putObject
    





 |  | IBMCOSOperations |
| **partSize** (producer) | Part size for multi-part uploads (default 25MB). | 26214400 | long |
| **storageClass** (producer) | The storage class to use when storing objects (e.g., STANDARD, VAULT, COLD, FLEX). |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **cosClient** (advanced) | **Autowired** Reference to an IBM COS Client instance in the registry. |  | AmazonS3 |
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
| **apiKey** (security) | IBM Cloud API Key for authentication. |  | String |
| **serviceInstanceId** (security) | IBM COS Service Instance ID (CRN). |  | String |

## Message Headers

The IBM Cloud Object Storage component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIBMCOSBucketName** (common) Constant: [`BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#BUCKET_NAME) | The bucket Name which this object will be stored or which will be used for the current operation. |  | String |
| **CamelIBMCOSBucketDestinationName** (producer) Constant: [`BUCKET_DESTINATION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#BUCKET_DESTINATION_NAME) | The bucket Destination Name which will be used for the current operation. |  | String |
| **CamelIBMCOSContentControl** (common) Constant: [`CACHE_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#CACHE_CONTROL) | The optional Cache-Control HTTP header which allows the user to specify caching behavior. |  | String |
| **CamelIBMCOSContentDisposition** (common) Constant: [`CONTENT_DISPOSITION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#CONTENT_DISPOSITION) | The optional Content-Disposition HTTP header, which specifies presentational information such as the recommended filename. |  | String |
| **CamelIBMCOSContentEncoding** (common) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#CONTENT_ENCODING) | The optional Content-Encoding HTTP header specifying what content encodings have been applied to the object. |  | String |
| **CamelIBMCOSContentLength** (common) Constant: [`CONTENT_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#CONTENT_LENGTH) | The Content-Length HTTP header indicating the size of the associated object in bytes. |  | Long |
| **CamelIBMCOSContentMD5** (common) Constant: [`CONTENT_MD5`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#CONTENT_MD5) | The base64 encoded 128-bit MD5 digest of the associated object. |  | String |
| **CamelIBMCOSContentType** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#CONTENT_TYPE) | The Content-Type HTTP header, which indicates the type of content stored in the associated object. |  | String |
| **CamelIBMCOSETag** (common) Constant: [`E_TAG`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#E_TAG) | The ETag value for the object. |  | String |
| **CamelIBMCOSKey** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#KEY) | The key under which this object is stored or will be stored. |  | String |
| **CamelIBMCOSDestinationKey** (producer) Constant: [`DESTINATION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#DESTINATION_KEY) | The Destination key which will be used for the current operation. |  | String |
| **CamelIBMCOSLastModified** (common) Constant: [`LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#LAST_MODIFIED) | The value of the Last-Modified header, indicating the date and time at which IBM COS last recorded a modification to the object. |  | Date |
| **CamelIBMCOSVersionId** (common) Constant: [`VERSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#VERSION_ID) | The version ID of the associated IBM COS object if available. |  | String |
| **CamelIBMCOSOperation** (common) Constant: [`COS_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#COS_OPERATION) | The operation to perform. |  | String |
| **CamelIBMCOSPrefix** (common) Constant: [`PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#PREFIX) | The prefix which is used to filter objects. |  | String |
| **CamelIBMCOSDelimiter** (common) Constant: [`DELIMITER`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#DELIMITER) | The delimiter which is used to filter objects. |  | String |
| **CamelIBMCOSKeysToDelete** (producer) Constant: [`KEYS_TO_DELETE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#KEYS_TO_DELETE) | A list of keys to delete when using deleteObjects operation. |  | List |
| **CamelIBMCOSMetadata** (common) Constant: [`METADATA`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#METADATA) | A map of metadata to be stored with the object in IBM COS. |  | Map |
| **CamelIBMCOSRangeStart** (producer) Constant: [`RANGE_START`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#RANGE_START) | The range start position for partial object retrieval. |  | Long |
| **CamelIBMCOSRangeEnd** (producer) Constant: [`RANGE_END`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#RANGE_END) | The range end position for partial object retrieval. |  | Long |
| **CamelIBMCOSBucketExists** (producer) Constant: [`BUCKET_EXISTS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-cos/latest/org/apache/camel/component/ibm/cos/IBMCOSConstants.html#BUCKET_EXISTS) | Whether the bucket exists or not. |  | Boolean |

Required IBM COS component options

You have to provide the `apiKey` and `serviceInstanceId` to access IBM Cloud Object Storage, along with the `endpointUrl` for your region.

## Usage

### Batch Consumer

This component implements the Batch Consumer.

This allows you, for instance, to know how many messages exist in this batch and for instance, let the Aggregator aggregate this number of messages.

### IBM COS Producer operations

The IBM COS component provides the following operation on the producer side:

-   copyObject
    
-   createBucket
    
-   deleteBucket
    
-   deleteObject
    
-   deleteObjects
    
-   getObject (this will return an InputStream)
    
-   getObjectRange (this will return an InputStream with partial content)
    
-   headBucket
    
-   listBuckets
    
-   listObjects
    
-   putObject
    

If you don’t specify an operation explicitly, the producer will do:

-   a single file upload
    
-   a multipart upload if multiPartUpload option is enabled
    

## Examples

For example, to read file `hello.txt` from bucket `helloBucket`, use the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("ibm-cos://helloBucket?apiKey=yourApiKey&serviceInstanceId=yourServiceInstanceId&endpointUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud&prefix=hello.txt")
  .to("file:/var/downloaded");
```

```xml
<route>
  <from uri="ibm-cos://helloBucket?apiKey=yourApiKey&amp;serviceInstanceId=yourServiceInstanceId&amp;endpointUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud&amp;prefix=hello.txt"/>
  <to uri="file:/var/downloaded"/>
</route>
```

```yaml
- route:
    from:
      uri: ibm-cos://helloBucket
      parameters:
        apiKey: yourApiKey
        serviceInstanceId: yourServiceInstanceId
        endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
        prefix: hello.txt
      steps:
        - to:
            uri: file:/var/downloaded
```

### Advanced IBM COS Client configuration

If your Camel Application is running behind a firewall or if you need to have more control over the `AmazonS3` client instance configuration, you can create your own instance and refer to it in your Camel ibm-cos component configuration:

-   Java
    
-   XML
    
-   YAML
    

```java
from("ibm-cos://MyBucket?cosClient=#client&delay=5000&maxMessagesPerPoll=5")
.to("mock:result");
```

```xml
<route>
  <from uri="ibm-cos://MyBucket?cosClient=#client&amp;delay=5000&amp;maxMessagesPerPoll=5"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: ibm-cos://MyBucket
      parameters:
        cosClient: "#client"
        delay: 5000
        maxMessagesPerPoll: 5
      steps:
        - to:
            uri: mock:result
```

### IBM COS Authentication

IBM Cloud Object Storage uses IBM Cloud IAM (Identity and Access Management) for authentication. You need to provide:

-   `apiKey`: Your IBM Cloud API key
    
-   `serviceInstanceId`: Your COS service instance ID (CRN - Cloud Resource Name)
    
-   `endpointUrl`: The endpoint URL for your region (e.g., `[https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)`)
    

You can find your service instance ID and create API keys in the IBM Cloud console.

For more information about IBM COS authentication, see the [IBM COS IAM documentation](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-iam).

### IBM COS Endpoints

IBM COS provides different endpoints for different regions and access types (public, private, direct). Examples:

-   Public endpoint (US South): `[https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)`
    
-   Public endpoint (EU GB): `[https://s3.eu-gb.cloud-object-storage.appdomain.cloud](https://s3.eu-gb.cloud-object-storage.appdomain.cloud)`
    
-   Private endpoint (US South): `[https://s3.private.us-south.cloud-object-storage.appdomain.cloud](https://s3.private.us-south.cloud-object-storage.appdomain.cloud)`
    

For a complete list of endpoints, see [IBM COS Endpoints documentation](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-endpoints).

Note that several operations requires a regional endpoint, as opposed to a cross-region endpoint.

### IBM COS Producer Operation examples

-   Single Upload: This operation will upload a file to IBM COS based on the body content
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelIBMCOSKey", constant("camel.txt"))
    .setBody(constant("Camel rocks!"))
    .to("ibm-cos://mycamelbucket?apiKey=RAW(myApiKey)&serviceInstanceId=RAW(myServiceInstanceId)&endpointUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelIBMCOSKey">
    <constant>camel.txt</constant>
  </setHeader>
  <setBody>
    <constant>Camel rocks!</constant>
  </setBody>
  <to uri="ibm-cos://mycamelbucket?apiKey=RAW(myApiKey)&amp;serviceInstanceId=RAW(myServiceInstanceId)&amp;endpointUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelIBMCOSKey
            constant: camel.txt
        - setBody:
            constant: "Camel rocks!"
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              apiKey: RAW(myApiKey)
              serviceInstanceId: RAW(myServiceInstanceId)
              endpointUrl: "https://s3.us-south.cloud-object-storage.appdomain.cloud"
        - to:
            uri: mock:result
```

This operation will upload the file camel.txt with the content "Camel rocks!" in the _mycamelbucket_ bucket.

> **Note**
> Use `RAW()` wrapper for sensitive values like API keys to prevent property placeholder resolution.

-   Multipart Upload: This operation will perform a multipart upload of a file to IBM COS based on the body content
    

_Java-only: requires Java File object as body_

```java
from("direct:start")
    .setHeader("CamelIBMCOSKey", constant("largefile.zip"))
    .process(exchange -> exchange.getIn().setBody(new File("src/largefile.zip")))
    .to("ibm-cos://mycamelbucket?cosClient=#cosClient&multiPartUpload=true&partSize=5242880")
    .to("mock:result");
```

This operation will perform a multipart upload of the file largefile.zip in the _mycamelbucket_ bucket with a part size of 5MB.

-   CopyObject: this operation copies an object from one bucket to a different one
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelIBMCOSBucketDestinationName", constant("camelDestinationBucket"))
    .setHeader("CamelIBMCOSKey", constant("camelKey"))
    .setHeader("CamelIBMCOSDestinationKey", constant("camelDestinationKey"))
    .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=copyObject")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelIBMCOSBucketDestinationName">
    <constant>camelDestinationBucket</constant>
  </setHeader>
  <setHeader name="CamelIBMCOSKey">
    <constant>camelKey</constant>
  </setHeader>
  <setHeader name="CamelIBMCOSDestinationKey">
    <constant>camelDestinationKey</constant>
  </setHeader>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=copyObject"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelIBMCOSBucketDestinationName
            constant: camelDestinationBucket
        - setHeader:
            name: CamelIBMCOSKey
            constant: camelKey
        - setHeader:
            name: CamelIBMCOSDestinationKey
            constant: camelDestinationKey
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: copyObject
        - to:
            uri: mock:result
```

This operation will copy the object with the name expressed in the header camelKey to camelDestinationKey in the camelDestinationBucket bucket, from the bucket _mycamelbucket_.

-   DeleteObject: this operation deletes an object from a bucket
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelIBMCOSKey", constant("camelKey"))
    .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=deleteObject")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelIBMCOSKey">
    <constant>camelKey</constant>
  </setHeader>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=deleteObject"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelIBMCOSKey
            constant: camelKey
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: deleteObject
        - to:
            uri: mock:result
```

This operation will delete the object camelKey from the bucket _mycamelbucket_.

-   DeleteObjects: this operation deletes multiple objects from a bucket in a single request
    

_Java-only: requires Java List for keys to delete_

```java
from("direct:start")
    .process(exchange -> {
        List<String> keys = Arrays.asList("file1.txt", "file2.txt", "file3.txt");
        exchange.getIn().setHeader("CamelIBMCOSKeysToDelete", keys);
    })
    .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=deleteObjects")
    .to("mock:result");
```

This operation will delete the objects file1.txt, file2.txt, and file3.txt from the bucket _mycamelbucket_ in a single batch request.

-   ListBuckets: this operation lists the buckets for this account in this region
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=listBuckets")
  .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=listBuckets"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: listBuckets
        - to:
            uri: mock:result
```

This operation will list the buckets for this account.

-   DeleteBucket: this operation deletes the bucket specified as URI parameter or header
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=deleteBucket")
  .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=deleteBucket"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: deleteBucket
        - to:
            uri: mock:result
```

This operation will delete the bucket _mycamelbucket_.

-   CreateBucket: this operation creates a new bucket
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelIBMCOSBucketName", constant("newBucket"))
    .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=createBucket")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelIBMCOSBucketName">
    <constant>newBucket</constant>
  </setHeader>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=createBucket"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelIBMCOSBucketName
            constant: newBucket
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: createBucket
        - to:
            uri: mock:result
```

This operation will create a new bucket named _newBucket_.

-   ListObjects: this operation lists objects in a specific bucket
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=listObjects")
  .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=listObjects"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: listObjects
        - to:
            uri: mock:result
```

This operation will list the objects in the _mycamelbucket_ bucket.

-   ListObjects with prefix: this operation lists objects in a specific bucket with a prefix filter
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelIBMCOSPrefix", constant("backup/"))
    .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=listObjects")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelIBMCOSPrefix">
    <constant>backup/</constant>
  </setHeader>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=listObjects"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelIBMCOSPrefix
            constant: "backup/"
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: listObjects
        - to:
            uri: mock:result
```

This operation will list only the objects in the _mycamelbucket_ bucket that start with "backup/".

-   GetObject: this operation gets a single object in a specific bucket
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelIBMCOSKey", constant("camelKey"))
    .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=getObject")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelIBMCOSKey">
    <constant>camelKey</constant>
  </setHeader>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=getObject"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelIBMCOSKey
            constant: camelKey
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: getObject
        - to:
            uri: mock:result
```

This operation will return an InputStream with the content of the camelKey object in _mycamelbucket_ bucket.

-   GetObjectRange: this operation gets a single object range in a specific bucket
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelIBMCOSKey", constant("camelKey"))
    .setHeader("CamelIBMCOSRangeStart", constant(0L))
    .setHeader("CamelIBMCOSRangeEnd", constant(9L))
    .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=getObjectRange")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelIBMCOSKey">
    <constant>camelKey</constant>
  </setHeader>
  <setHeader name="CamelIBMCOSRangeStart">
    <constant resultType="java.lang.Long">0</constant>
  </setHeader>
  <setHeader name="CamelIBMCOSRangeEnd">
    <constant resultType="java.lang.Long">9</constant>
  </setHeader>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=getObjectRange"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelIBMCOSKey
            constant: camelKey
        - setHeader:
            name: CamelIBMCOSRangeStart
            constant: 0
        - setHeader:
            name: CamelIBMCOSRangeEnd
            constant: 9
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: getObjectRange
        - to:
            uri: mock:result
```

This operation will return an InputStream with the content of the camelKey object in _mycamelbucket_ bucket, containing bytes from 0 to 9.

-   HeadBucket: this operation checks if a bucket exists and you have permission to access it
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("ibm-cos://mycamelbucket?cosClient=#cosClient&operation=headBucket")
  .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;operation=headBucket"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: ibm-cos://mycamelbucket
            parameters:
              cosClient: "#cosClient"
              operation: headBucket
        - to:
            uri: mock:result
```

This operation will check if the bucket _mycamelbucket_ exists and is accessible. The result (true/false) will be in the message body.

### IBM COS Consumer

The IBM COS consumer will poll a bucket for new objects and process them.

-   Java
    
-   XML
    
-   YAML
    

```java
from("ibm-cos://mycamelbucket?cosClient=#cosClient&delay=5000&maxMessagesPerPoll=10&deleteAfterRead=true")
  .to("file:/var/downloaded");
```

```xml
<route>
  <from uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;delay=5000&amp;maxMessagesPerPoll=10&amp;deleteAfterRead=true"/>
  <to uri="file:/var/downloaded"/>
</route>
```

```yaml
- route:
    from:
      uri: ibm-cos://mycamelbucket
      parameters:
        cosClient: "#cosClient"
        delay: 5000
        maxMessagesPerPoll: 10
        deleteAfterRead: true
      steps:
        - to:
            uri: file:/var/downloaded
```

This route will poll the _mycamelbucket_ bucket every 5 seconds, processing up to 10 objects per poll, and deleting each object after it’s been successfully processed.

### Move After Read

Instead of deleting objects after reading, you can move them to a different bucket or prefix:

-   Java
    
-   XML
    
-   YAML
    

```java
from("ibm-cos://mycamelbucket?cosClient=#cosClient&deleteAfterRead=false&moveAfterRead=true&destinationBucket=processed-bucket&destinationBucketPrefix=done-")
  .to("direct:process");
```

```xml
<route>
  <from uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;deleteAfterRead=false&amp;moveAfterRead=true&amp;destinationBucket=processed-bucket&amp;destinationBucketPrefix=done-"/>
  <to uri="direct:process"/>
</route>
```

```yaml
- route:
    from:
      uri: ibm-cos://mycamelbucket
      parameters:
        cosClient: "#cosClient"
        deleteAfterRead: false
        moveAfterRead: true
        destinationBucket: processed-bucket
        destinationBucketPrefix: "done-"
      steps:
        - to:
            uri: direct:process
```

This route will move processed objects from _mycamelbucket_ to _processed-bucket_, prefixing each object key with "done-".

### IBM COS Consumer with prefix filter

You can filter which objects to consume by using a prefix:

-   Java
    
-   XML
    
-   YAML
    

```java
from("ibm-cos://mycamelbucket?cosClient=#cosClient&prefix=inbox/&deleteAfterRead=true")
  .to("direct:process");
```

```xml
<route>
  <from uri="ibm-cos://mycamelbucket?cosClient=#cosClient&amp;prefix=inbox/&amp;deleteAfterRead=true"/>
  <to uri="direct:process"/>
</route>
```

```yaml
- route:
    from:
      uri: ibm-cos://mycamelbucket
      parameters:
        cosClient: "#cosClient"
        prefix: "inbox/"
        deleteAfterRead: true
      steps:
        - to:
            uri: direct:process
```

This route will only consume objects whose keys start with "inbox/".

## Running Integration Tests

Integration tests require valid IBM Cloud credentials. Follow these steps to set up and run the tests.

### Creating Service Credentials

1.  Log in to the [IBM Cloud Console](https://cloud.ibm.com)
    
2.  Navigate to your Cloud Object Storage instance (or create one if you don’t have one)
    
3.  Go to **Service credentials** in the left menu
    
4.  Click **New credential**
    
5.  Give it a name (e.g., `camel-cos-test`)
    
6.  **Important**: Set the role to **Manager** (required for bucket creation operations)
    
7.  Click **Add**
    
8.  Expand the newly created credential to view the JSON
    

### Mapping Credentials to Test Properties

From the service credential JSON, extract the following values:

  
| System Property | JSON Field | Example |
| --- | --- | --- |
| `camel.ibm.cos.apiKey` | `apikey` | `Hh1u4wjecZ_jUhJScOt0sN…​` |
| `camel.ibm.cos.serviceInstanceId` | `resource_instance_id` | `crn:v1:bluemix:public:cloud-object-storage:global:a/…​` |
| `camel.ibm.cos.endpointUrl` | Not in credentials - choose based on region | `[https://s3.us-south.cloud-object-storage.appdomain.cloud](https://s3.us-south.cloud-object-storage.appdomain.cloud)` |
> **Note**
> The `endpoints` field in the credentials JSON is a control API URL, not the actual COS endpoint. You must choose a regional endpoint from the [IBM COS Endpoints documentation](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-endpoints).

### Running the Tests

```bash
mvn verify -pl components/camel-ibm/camel-ibm-cos \
  -Dcamel.ibm.cos.apiKey=YOUR_API_KEY \
  -Dcamel.ibm.cos.serviceInstanceId='YOUR_SERVICE_INSTANCE_ID' \
  -Dcamel.ibm.cos.endpointUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud
```

> **Tip**
> Use single quotes around the `serviceInstanceId` value to prevent shell interpretation of special characters in the CRN.

### Troubleshooting

-   **403 Forbidden**: Ensure your service credential has the **Manager** role. Writer role is not sufficient for bucket creation.
    

## Dependencies

Maven users will need to add the following dependency to their `pom.xml`.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ibm-cos</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

where `x.x.x` is the version number of Camel.