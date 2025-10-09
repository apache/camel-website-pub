# AWS S3 Storage Service

**Since Camel 3.2**

**Both producer and consumer are supported**

The AWS2 S3 component supports storing and retrieving objects from/to [Amazon’s S3](https://aws.amazon.com/s3) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon S3. More information is available at [Amazon S3](https://aws.amazon.com/s3).

## URI Format

aws2-s3://bucketNameOrArn\[?options\]

The bucket will be created if it don’t already exists.  
You can append query options to the URI in the following format, ?options=value&option2=value&…​

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

The AWS S3 Storage Service component supports 52 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonS3Client** (common) | **Autowired** Reference to a com.amazonaws.services.s3.AmazonS3 in the registry. |  | S3Client |
| **amazonS3Presigner** (common) | **Autowired** An S3 Presigner for Request, used mainly in createDownloadLink operation. |  | S3Presigner |
| **autoCreateBucket** (common) | Setting the autocreation of the S3 bucket bucketName. This will apply also in case of moveAfterRead option enabled and it will create the destinationBucket if it doesn’t exist already. | false | boolean |
| **configuration** (common) | The component configuration. |  | AWS2S3Configuration |
| **delimiter** (common) | The delimiter which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **forcePathStyle** (common) | Set whether the S3 client should use path-style URL instead of virtual-hosted-style. | false | boolean |
| **overrideEndpoint** (common) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **policy** (common) | The policy for this queue to set in the com.amazonaws.services.s3.AmazonS3#setBucketPolicy() method. |  | String |
| **prefix** (common) | The prefix which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **proxyHost** (common) | To define a proxy host when instantiating the SQS client. |  | String |
| **proxyPort** (common) | Specify a proxy port to be used inside the client definition. |  | Integer |
| **proxyProtocol** (common) | 
To define a proxy protocol when instantiating the S3 client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (common) | The region in which S3 client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (common) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (common) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **customerAlgorithm** (common (advanced)) | Define the customer algorithm to use in case CustomerKey is enabled. |  | String |
| **customerKeyId** (common (advanced)) | Define the id of Customer key to use in case CustomerKey is enabled. |  | String |
| **customerKeyMD5** (common (advanced)) | Define the MD5 of Customer key to use in case CustomerKey is enabled. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **deleteAfterRead** (consumer) | Delete objects from S3 after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieve over and over again on the polls. Therefore you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the AWS2S3Constants#BUCKET\_NAME and AWS2S3Constants#KEY headers, or only the AWS2S3Constants#KEY header. | true | boolean |
| **destinationBucket** (consumer) | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | String |
| **destinationBucketPrefix** (consumer) | Define the destination bucket prefix to use when an object must be moved and moveAfterRead is set to true. |  | String |
| **destinationBucketSuffix** (consumer) | Define the destination bucket suffix to use when an object must be moved and moveAfterRead is set to true. |  | String |
| **doneFileName** (consumer) | If provided, Camel will only consume files if a done file exists. |  | String |
| **fileName** (consumer) | To get the object from the bucket with the given file name. |  | String |
| **ignoreBody** (consumer) | If it is true, the S3 Object Body will be ignored completely, if it is set to false the S3 Object will be put in the body. Setting this to true, will override any behavior defined by includeBody option. | false | boolean |
| **includeBody** (consumer) | If it is true, the S3Object exchange will be consumed and put into the body and closed. If false the S3Object stream will be put raw into the body and the headers will be set with the S3 object metadata. This option is strongly related to autocloseBody option. In case of setting includeBody to true because the S3Object stream will be consumed then it will also be closed, while in case of includeBody false then it will be up to the caller to close the S3Object stream. However setting autocloseBody to true when includeBody is false it will schedule to close the S3Object stream automatically on exchange completion. | true | boolean |
| **includeFolders** (consumer) | If it is true, the folders/directories will be consumed. If it is false, they will be ignored, and Exchanges will not be created for those. | true | boolean |
| **moveAfterRead** (consumer) | Move objects from S3 bucket to a different bucket after they have been retrieved. To accomplish the operation the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | boolean |
| **autocloseBody** (consumer (advanced)) | If this option is true and includeBody is false, then the S3Object.close() method will be called on exchange completion. This option is strongly related to includeBody option. In case of setting includeBody to false and autocloseBody to false, it will be up to the caller to close the S3Object stream. Setting autocloseBody to true, will close the S3Object stream automatically. | true | boolean |
| **batchMessageNumber** (producer) | The number of messages composing a batch in streaming upload mode. | 10 | int |
| **batchSize** (producer) | The batch size (in bytes) in streaming upload mode. | 1000000 | int |
| **deleteAfterWrite** (producer) | Delete file object after the S3 file has been uploaded. | false | boolean |
| **keyName** (producer) | Setting the key name for an element in the bucket through endpoint parameter. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **multiPartUpload** (producer) | If it is true, camel will upload the file with multi part format, the part size is decided by the option of partSize. | false | boolean |
| **namingStrategy** (producer) | 

The naming strategy to use in streaming upload mode.

Enum values:

-   progressive
    
-   random
    





 | progressive | AWSS3NamingStrategyEnum |
| **operation** (producer) | 

The operation to do in case the user don’t want to do only an upload.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   getObjectRange
    
-   createDownloadLink
    





 |  | AWS2S3Operations |
| **partSize** (producer) | Setup the partSize which is used in multi part upload, the default size is 25M. | 26214400 | long |
| **restartingPolicy** (producer) | 

The restarting policy to use in streaming upload mode.

Enum values:

-   override
    
-   lastPart
    





 | override | AWSS3RestartingPolicyEnum |
| **storageClass** (producer) | The storage class to set in the com.amazonaws.services.s3.model.PutObjectRequest request. |  | String |
| **streamingUploadMode** (producer) | When stream mode is true the upload to bucket will be done in streaming. | false | boolean |
| **streamingUploadTimeout** (producer) | While streaming upload mode is true, this option set the timeout to complete upload. |  | long |
| **awsKMSKeyId** (producer (advanced)) | Define the id of KMS key to use in case KMS is enabled. |  | String |
| **useAwsKMS** (producer (advanced)) | Define if KMS must be used or not. | false | boolean |
| **useCustomerKey** (producer (advanced)) | Define if Customer Key must be used or not. | false | boolean |
| **useSSES3** (producer (advanced)) | Define if SSE S3 must be used or not. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS S3 Storage Service endpoint is configured using URI syntax:

aws2-s3://bucketNameOrArn

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bucketNameOrArn** (common) | **Required** Bucket name or ARN. |  | String |

### Query Parameters (70 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonS3Client** (common) | **Autowired** Reference to a com.amazonaws.services.s3.AmazonS3 in the registry. |  | S3Client |
| **amazonS3Presigner** (common) | **Autowired** An S3 Presigner for Request, used mainly in createDownloadLink operation. |  | S3Presigner |
| **autoCreateBucket** (common) | Setting the autocreation of the S3 bucket bucketName. This will apply also in case of moveAfterRead option enabled and it will create the destinationBucket if it doesn’t exist already. | false | boolean |
| **delimiter** (common) | The delimiter which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **forcePathStyle** (common) | Set whether the S3 client should use path-style URL instead of virtual-hosted-style. | false | boolean |
| **overrideEndpoint** (common) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **policy** (common) | The policy for this queue to set in the com.amazonaws.services.s3.AmazonS3#setBucketPolicy() method. |  | String |
| **prefix** (common) | The prefix which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **proxyHost** (common) | To define a proxy host when instantiating the SQS client. |  | String |
| **proxyPort** (common) | Specify a proxy port to be used inside the client definition. |  | Integer |
| **proxyProtocol** (common) | 
To define a proxy protocol when instantiating the S3 client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (common) | The region in which S3 client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (common) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (common) | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **customerAlgorithm** (common (advanced)) | Define the customer algorithm to use in case CustomerKey is enabled. |  | String |
| **customerKeyId** (common (advanced)) | Define the id of Customer key to use in case CustomerKey is enabled. |  | String |
| **customerKeyMD5** (common (advanced)) | Define the MD5 of Customer key to use in case CustomerKey is enabled. |  | String |
| **deleteAfterRead** (consumer) | Delete objects from S3 after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieve over and over again on the polls. Therefore you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the AWS2S3Constants#BUCKET\_NAME and AWS2S3Constants#KEY headers, or only the AWS2S3Constants#KEY header. | true | boolean |
| **destinationBucket** (consumer) | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | String |
| **destinationBucketPrefix** (consumer) | Define the destination bucket prefix to use when an object must be moved and moveAfterRead is set to true. |  | String |
| **destinationBucketSuffix** (consumer) | Define the destination bucket suffix to use when an object must be moved and moveAfterRead is set to true. |  | String |
| **doneFileName** (consumer) | If provided, Camel will only consume files if a done file exists. |  | String |
| **fileName** (consumer) | To get the object from the bucket with the given file name. |  | String |
| **ignoreBody** (consumer) | If it is true, the S3 Object Body will be ignored completely, if it is set to false the S3 Object will be put in the body. Setting this to true, will override any behavior defined by includeBody option. | false | boolean |
| **includeBody** (consumer) | If it is true, the S3Object exchange will be consumed and put into the body and closed. If false the S3Object stream will be put raw into the body and the headers will be set with the S3 object metadata. This option is strongly related to autocloseBody option. In case of setting includeBody to true because the S3Object stream will be consumed then it will also be closed, while in case of includeBody false then it will be up to the caller to close the S3Object stream. However setting autocloseBody to true when includeBody is false it will schedule to close the S3Object stream automatically on exchange completion. | true | boolean |
| **includeFolders** (consumer) | If it is true, the folders/directories will be consumed. If it is false, they will be ignored, and Exchanges will not be created for those. | true | boolean |
| **maxConnections** (consumer) | Set the maxConnections parameter in the S3 client configuration. | 60 | int |
| **maxMessagesPerPoll** (consumer) | Gets the maximum number of messages as a limit to poll at each polling. Gets the maximum number of messages as a limit to poll at each polling. The default value is 10. Use 0 or a negative number to set it as unlimited. | 10 | int |
| **moveAfterRead** (consumer) | Move objects from S3 bucket to a different bucket after they have been retrieved. To accomplish the operation the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **autocloseBody** (consumer (advanced)) | If this option is true and includeBody is false, then the S3Object.close() method will be called on exchange completion. This option is strongly related to includeBody option. In case of setting includeBody to false and autocloseBody to false, it will be up to the caller to close the S3Object stream. Setting autocloseBody to true, will close the S3Object stream automatically. | true | boolean |
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
| **batchMessageNumber** (producer) | The number of messages composing a batch in streaming upload mode. | 10 | int |
| **batchSize** (producer) | The batch size (in bytes) in streaming upload mode. | 1000000 | int |
| **deleteAfterWrite** (producer) | Delete file object after the S3 file has been uploaded. | false | boolean |
| **keyName** (producer) | Setting the key name for an element in the bucket through endpoint parameter. |  | String |
| **multiPartUpload** (producer) | If it is true, camel will upload the file with multi part format, the part size is decided by the option of partSize. | false | boolean |
| **namingStrategy** (producer) | 

The naming strategy to use in streaming upload mode.

Enum values:

-   progressive
    
-   random
    





 | progressive | AWSS3NamingStrategyEnum |
| **operation** (producer) | 

The operation to do in case the user don’t want to do only an upload.

Enum values:

-   copyObject
    
-   listObjects
    
-   deleteObject
    
-   deleteBucket
    
-   listBuckets
    
-   getObject
    
-   getObjectRange
    
-   createDownloadLink
    





 |  | AWS2S3Operations |
| **partSize** (producer) | Setup the partSize which is used in multi part upload, the default size is 25M. | 26214400 | long |
| **restartingPolicy** (producer) | 

The restarting policy to use in streaming upload mode.

Enum values:

-   override
    
-   lastPart
    





 | override | AWSS3RestartingPolicyEnum |
| **storageClass** (producer) | The storage class to set in the com.amazonaws.services.s3.model.PutObjectRequest request. |  | String |
| **streamingUploadMode** (producer) | When stream mode is true the upload to bucket will be done in streaming. | false | boolean |
| **streamingUploadTimeout** (producer) | While streaming upload mode is true, this option set the timeout to complete upload. |  | long |
| **awsKMSKeyId** (producer (advanced)) | Define the id of KMS key to use in case KMS is enabled. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **useAwsKMS** (producer (advanced)) | Define if KMS must be used or not. | false | boolean |
| **useCustomerKey** (producer (advanced)) | Define if Customer Key must be used or not. | false | boolean |
| **useSSES3** (producer (advanced)) | Define if SSE S3 must be used or not. | false | boolean |
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
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

Required S3 component options

You have to provide the amazonS3Client in the Registry or your accessKey and secretKey to access the [Amazon’s S3](https://aws.amazon.com/s3).

## Batch Consumer

This component implements the Batch Consumer.

This allows you for instance to know how many messages exists in this batch and for instance let the Aggregator aggregate this number of messages.

## Usage

For example in order to read file `hello.txt` from bucket `helloBucket`, use the following snippet:

```java
from("aws2-s3://helloBucket?accessKey=yourAccessKey&secretKey=yourSecretKey&prefix=hello.txt")
  .to("file:/var/downloaded");
```

## Message Headers

The AWS S3 Storage Service component supports 30 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsS3BucketName** (common) Constant: [`BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#BUCKET_NAME) | The bucket Name which this object will be stored or which will be used for the current operation or in which this object is contained. |  | String |
| **CamelAwsS3BucketDestinationName** (producer) Constant: [`BUCKET_DESTINATION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#BUCKET_DESTINATION_NAME) | The bucket Destination Name which will be used for the current operation. |  | String |
| **CamelAwsS3ContentControl** (common) Constant: [`CACHE_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CACHE_CONTROL) | The optional Cache-Control HTTP header which allows the user to specify caching behavior along the HTTP request/reply chain. |  | String |
| **CamelAwsS3ContentDisposition** (common) Constant: [`CONTENT_DISPOSITION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_DISPOSITION) | The optional Content-Disposition HTTP header, which specifies presentational information such as the recommended filename for the object to be saved as. |  | String |
| **CamelAwsS3ContentEncoding** (common) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_ENCODING) | The optional Content-Encoding HTTP header specifying what content encodings have been applied to the object and what decoding mechanisms must be applied in order to obtain the media-type referenced by the Content-Type field. |  | String |
| **CamelAwsS3ContentLength** (common) Constant: [`CONTENT_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_LENGTH) | The Content-Length HTTP header indicating the size of the associated object in bytes. |  | Long |
| **CamelAwsS3ContentMD5** (common) Constant: [`CONTENT_MD5`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_MD5) | The base64 encoded 128-bit MD5 digest of the associated object (content - not including headers) according to RFC 1864. This data is used as a message integrity check to verify that the data received by Amazon S3 is the same data that the caller sent. |  | String |
| **CamelAwsS3ContentType** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_TYPE) | The Content-Type HTTP header, which indicates the type of content stored in the associated object. The value of this header is a standard MIME type. |  | String |
| **CamelAwsS3ETag** (common) Constant: [`E_TAG`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#E_TAG) | (producer) The ETag value for the newly uploaded object. (consumer) The hex encoded 128-bit MD5 digest of the associated object according to RFC 1864. This data is used as an integrity check to verify that the data received by the caller is the same data that was sent by Amazon S3. |  | String |
| **CamelAwsS3Key** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#KEY) | The key under which this object is stored or will be stored or which will be used for the current operation. |  | String |
| **CamelAwsS3DestinationKey** (producer) Constant: [`DESTINATION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#DESTINATION_KEY) | The Destination key which will be used for the current operation. |  | String |
| **CamelAwsS3LastModified** (common) Constant: [`LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#LAST_MODIFIED) | The value of the Last-Modified header, indicating the date and time at which Amazon S3 last recorded a modification to the associated object. |  | Date |
| **CamelAwsS3StorageClass** (common) Constant: [`STORAGE_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#STORAGE_CLASS) | The storage class of this object. |  | String |
| **CamelAwsS3VersionId** (common) Constant: [`VERSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#VERSION_ID) | (producer) The optional version ID of the newly uploaded object. (consumer) The version ID of the associated Amazon S3 object if available. Version IDs are only assigned to objects when an object is uploaded to an Amazon S3 bucket that has object versioning enabled. |  | String |
| **CamelAwsS3CannedAcl** (producer) Constant: [`CANNED_ACL`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CANNED_ACL) | The canned acl that will be applied to the object. see software.amazon.awssdk.services.s3.model.ObjectCannedACL for allowed values. |  | String |
| **CamelAwsS3Acl** (producer) Constant: [`ACL`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#ACL) | 
A well constructed Amazon S3 Access Control List object.

Enum values:

-   private
    
-   public-read
    
-   public-read-write
    
-   authenticated-read
    
-   null
    





 |  | BucketCannedACL |
| **CamelAwsS3Operation** (common) Constant: [`S3_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#S3_OPERATION) | The operation to perform. Permitted values are copyObject, deleteObject, listBuckets, deleteBucket, listObjects. |  | String |
| **CamelAwsS3ServerSideEncryption** (common) Constant: [`SERVER_SIDE_ENCRYPTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#SERVER_SIDE_ENCRYPTION) | Sets the server-side encryption algorithm when encrypting the object using AWS-managed keys. For example use AES256. |  | String |
| **CamelAwsS3ExpirationTime** (consumer) Constant: [`EXPIRATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#EXPIRATION_TIME) | If the object expiration is configured (see PUT Bucket lifecycle), the response includes this header. |  | String |
| **CamelAwsS3ReplicationStatus** (consumer) Constant: [`REPLICATION_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#REPLICATION_STATUS) | 

Amazon S3 can return this if your request involves a bucket that is either a source or destination in a replication rule.

Enum values:

-   COMPLETE
    
-   PENDING
    
-   FAILED
    
-   REPLICA
    
-   null
    





 |  | ReplicationStatus |
| **CamelAwsS3RangeStart** (producer) Constant: [`RANGE_START`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#RANGE_START) | The position of the first byte to get. |  | String |
| **CamelAwsS3RangeEnd** (producer) Constant: [`RANGE_END`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#RANGE_END) | The position of the last byte to get. |  | String |
| **CamelAwsS3DowloadLinkExpirationTime** (producer) Constant: [`DOWNLOAD_LINK_EXPIRATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#DOWNLOAD_LINK_EXPIRATION_TIME) | The expiration time of the download link in milliseconds. |  | Long |
| **CamelAwsS3DownloadLinkBrowserCompatible** (producer) Constant: [`DOWNLOAD_LINK_BROWSER_COMPATIBLE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#DOWNLOAD_LINK_BROWSER_COMPATIBLE) | Whether the download link is browser compatible. |  | boolean |
| **CamelAwsS3DownloadLinkHttpRequestHeaders** (producer) Constant: [`DOWNLOAD_LINK_HTTP_REQUEST_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#DOWNLOAD_LINK_HTTP_REQUEST_HEADERS) | The headers that are needed by the service (not needed when BrowserCompatible is true). |  | Map |
| **CamelAwsS3DownloadLinkSignedPayload** (producer) Constant: [`DOWNLOAD_LINK_SIGNED_PAYLOAD`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#DOWNLOAD_LINK_SIGNED_PAYLOAD) | The request payload that is needed by the service (not needed when BrowserCompatible is true). |  | String |
| **CamelAwsS3Metadata** (common) Constant: [`METADATA`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#METADATA) | A map of metadata to be stored or stored with the object in S3. More details about metadata [https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMetadata.htmlhere](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMetadata.htmlhere). |  | Map |
| **CamelMessageTimestamp** (consumer) Constant: [`MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#MESSAGE_TIMESTAMP) | The timestamp of the message. |  | long |
| **CamelAwsS3Prefix** (common) Constant: [`PREFIX`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#PREFIX) | The prefix which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only list objects we are interested in. |  |  |
| **CamelAwsS3Delimiter** (common) Constant: [`DELIMITER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#DELIMITER) | The delimiter which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only list objects we are interested in. |  | String |

### S3 Producer operations

Camel-AWS2-S3 component provides the following operation on the producer side:

-   copyObject
    
-   deleteObject
    
-   listBuckets
    
-   deleteBucket
    
-   listObjects
    
-   getObject (this will return an S3Object instance)
    
-   getObjectRange (this will return an S3Object instance)
    
-   createDownloadLink
    

If you don’t specify an operation explicitly the producer will do: - a single file upload - a multipart upload if multiPartUpload option is enabled

### Advanced AmazonS3 configuration

If your Camel Application is running behind a firewall or if you need to have more control over the `S3Client` instance configuration, you can create your own instance and refer to it in your Camel aws2-s3 component configuration:

```java
from("aws2-s3://MyBucket?amazonS3Client=#client&delay=5000&maxMessagesPerPoll=5")
.to("mock:result");
```

### Use KMS with the S3 component

To use AWS KMS to encrypt/decrypt data by using AWS infrastructure you can use the options introduced in 2.21.x like in the following example

```java
from("file:tmp/test?fileName=test.txt")
     .setHeader(AWS2S3Constants.KEY, constant("testFile"))
     .to("aws2-s3://mybucket?amazonS3Client=#client&useAwsKMS=true&awsKMSKeyId=3f0637ad-296a-3dfe-a796-e60654fb128c");
```

In this way you’ll ask to S3, to use the KMS key 3f0637ad-296a-3dfe-a796-e60654fb128c, to encrypt the file test.txt. When you’ll ask to download this file, the decryption will be done directly before the download.

### Static credentials vs Default Credential Provider

You have the possibility of avoiding the usage of explicit static credentials, by specifying the useDefaultCredentialsProvider option and set it to true.

-   Java system properties - aws.accessKeyId and aws.secretKey
    
-   Environment variables - AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable AWS\_CONTAINER\_CREDENTIALS\_RELATIVE\_URI is set.
    
-   Amazon EC2 Instance profile credentials.
    

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### S3 Producer Operation examples

-   Single Upload: This operation will upload a file to S3 based on the body content
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(AWS2S3Constants.KEY, "camel.txt");
          exchange.getIn().setBody("Camel rocks!");
      }
  })
  .to("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client")
  .to("mock:result");
```

This operation will upload the file camel.txt with the content "Camel rocks!" in the mycamelbucket bucket

-   Multipart Upload: This operation will perform a multipart upload of a file to S3 based on the body content
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(AWS2S3Constants.KEY, "empty.txt");
          exchange.getIn().setBody(new File("src/empty.txt"));
      }
  })
  .to("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&multiPartUpload=true&autoCreateBucket=true&partSize=1048576")
  .to("mock:result");
```

This operation will perform a multipart upload of the file empty.txt with based on the content the file src/empty.txt in the mycamelbucket bucket

-   CopyObject: this operation copy an object from one bucket to a different one
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(AWS2S3Constants.BUCKET_DESTINATION_NAME, "camelDestinationBucket");
          exchange.getIn().setHeader(AWS2S3Constants.KEY, "camelKey");
          exchange.getIn().setHeader(AWS2S3Constants.DESTINATION_KEY, "camelDestinationKey");
      }
  })
  .to("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&operation=copyObject")
  .to("mock:result");
```

This operation will copy the object with the name expressed in the header camelDestinationKey to the camelDestinationBucket bucket, from the bucket mycamelbucket.

-   DeleteObject: this operation deletes an object from a bucket
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(AWS2S3Constants.KEY, "camelKey");
      }
  })
  .to("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&operation=deleteObject")
  .to("mock:result");
```

This operation will delete the object camelKey from the bucket mycamelbucket.

-   ListBuckets: this operation list the buckets for this account in this region
    

```java
  from("direct:start")
  .to("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&operation=listBuckets")
  .to("mock:result");
```

This operation will list the buckets for this account

-   DeleteBucket: this operation delete the bucket specified as URI parameter or header
    

```java
  from("direct:start")
  .to("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&operation=deleteBucket")
  .to("mock:result");
```

This operation will delete the bucket mycamelbucket

-   ListObjects: this operation list object in a specific bucket
    

```java
  from("direct:start")
  .to("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&operation=listObjects")
  .to("mock:result");
```

This operation will list the objects in the mycamelbucket bucket

-   GetObject: this operation get a single object in a specific bucket
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(AWS2S3Constants.KEY, "camelKey");
      }
  })
  .to("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&operation=getObject")
  .to("mock:result");
```

This operation will return an S3Object instance related to the camelKey object in mycamelbucket bucket.

-   GetObjectRange: this operation get a single object range in a specific bucket
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(AWS2S3Constants.KEY, "camelKey");
          exchange.getIn().setHeader(AWS2S3Constants.RANGE_START, "0");
          exchange.getIn().setHeader(AWS2S3Constants.RANGE_END, "9");
      }
  })
  .to("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&operation=getObjectRange")
  .to("mock:result");
```

This operation will return an S3Object instance related to the camelKey object in mycamelbucket bucket, containing a the bytes from 0 to 9.

-   CreateDownloadLink: this operation will return a download link through S3 Presigner
    

```java
  from("direct:start").process(new Processor() {

      @Override
      public void process(Exchange exchange) throws Exception {
          exchange.getIn().setHeader(AWS2S3Constants.KEY, "camelKey");
      }
  })
  .to("aws2-s3://mycamelbucket?accessKey=xxx&secretKey=yyy&region=region&operation=createDownloadLink")
  .to("mock:result");
```

This operation will return a download link url for the file camel-key in the bucket mycamelbucket and region region. Parameters (`accessKey`, `secretKey` and `region`) are mandatory for this operation, if S3 client is autowired from the registry.

> **Note**
> If checksum validations are enabled, the url will no longer be browser compatible because it adds a signed header that must be included in the HTTP request.

## Streaming Upload mode

With the stream mode enabled users will be able to upload data to S3 without knowing ahead of time the dimension of the data, by leveraging multipart upload. The upload will be completed when: the batchSize has been completed or the batchMessageNumber has been reached. There are two possible naming strategy: progressive and random. With the progressive strategy each file will have the name composed by keyName option and a progressive counter, and eventually the file extension (if any), while with the random strategy a UUID will be added after keyName and eventually the file extension will appended.

As an example:

```java
from(kafka("topic1").brokers("localhost:9092"))
        .log("Kafka Message is: ${body}")
        .to(aws2S3("camel-bucket").streamingUploadMode(true).batchMessageNumber(25).namingStrategy(AWS2S3EndpointBuilderFactory.AWSS3NamingStrategyEnum.progressive).keyName("{{kafkaTopic1}}/{{kafkaTopic1}}.txt"));

from(kafka("topic2").brokers("localhost:9092"))
         .log("Kafka Message is: ${body}")
         .to(aws2S3("camel-bucket").streamingUploadMode(true).batchMessageNumber(25).namingStrategy(AWS2S3EndpointBuilderFactory.AWSS3NamingStrategyEnum.random).keyName("{{kafkaTopic2}}/{{kafkaTopic2}}.txt"));
```

The default size for a batch is 1 Mb, but you can adjust it according to your requirements.

When you’ll stop your producer route, the producer will take care of flushing the remaining buffered messaged and complete the upload.

In Streaming upload you’ll be able restart the producer from the point where it left. It’s important to note that this feature is critical only when using the progressive naming strategy.

By setting the restartingPolicy to lastPart, you will restart uploading files and contents from the last part number the producer left.

As example: - Start the route with progressive naming strategy and keyname equals to camel.txt, with batchMessageNumber equals to 20, and restartingPolicy equals to lastPart - Send 70 messages. - Stop the route - On your S3 bucket you should now see 4 files: camel.txt, camel-1.txt, camel-2.txt and camel-3.txt, the first three will have 20 messages, while the last one only 10. - Restart the route - Send 25 messages - Stop the route - You’ll now have 2 other files in your bucket: camel-5.txt and camel-6.txt, the first with 20 messages and second with 5 messages. - Go ahead

This won’t be needed when using the random naming strategy.

On the opposite you can specify the override restartingPolicy. In that case you’ll be able to override whatever you written before (for that particular keyName) on your bucket.

> **Note**
> In Streaming upload mode the only keyName option that will be taken into account is the endpoint option. Using the header will throw an NPE and this is done by design. Setting the header means potentially change the file name on each exchange and this is against the aim of the streaming upload producer. The keyName needs to be fixed and static. The selected naming strategy will do the rest of the of the work.

Another possibility is specifying a streamingUploadTimeout with batchMessageNumber and batchSize options. With this option the user will be able to complete the upload of a file after a certain time passed. In this way the upload completion will be passed on three tiers: the timeout, the number of messages and the batch size.

As an example:

```java
from(kafka("topic1").brokers("localhost:9092"))
        .log("Kafka Message is: ${body}")
        .to(aws2S3("camel-bucket").streamingUploadMode(true).batchMessageNumber(25).streamingUploadTimeout(10000).namingStrategy(AWS2S3EndpointBuilderFactory.AWSS3NamingStrategyEnum.progressive).keyName("{{kafkaTopic1}}/{{kafkaTopic1}}.txt"));
```

In this case the upload will be completed after 10 seconds.

## Bucket Autocreation

With the option `autoCreateBucket` users are able to avoid the autocreation of an S3 Bucket in case it doesn’t exist. The default for this option is `false`. If set to false any operation on a not-existent bucket in AWS won’t be successful and an error will be returned.

## Moving stuff between a bucket and another bucket

Some users like to consume stuff from a bucket and move the content in a different one without using the copyObject feature of this component. If this is case for you, don’t forget to remove the bucketName header from the incoming exchange of the consumer, otherwise the file will be always overwritten on the same original bucket.

## MoveAfterRead consumer option

In addition to deleteAfterRead it has been added another option, moveAfterRead. With this option enabled the consumed object will be moved to a target destinationBucket instead of being only deleted. This will require specifying the destinationBucket option. As example:

```java
  from("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&moveAfterRead=true&destinationBucket=myothercamelbucket")
  .to("mock:result");
```

In this case the objects consumed will be moved to myothercamelbucket bucket and deleted from the original one (because of deleteAfterRead set to true as default).

You have also the possibility of using a key prefix/suffix while moving the file to a different bucket. The options are destinationBucketPrefix and destinationBucketSuffix.

Taking the above example, you could do something like:

```java
  from("aws2-s3://mycamelbucket?amazonS3Client=#amazonS3Client&moveAfterRead=true&destinationBucket=myothercamelbucket&destinationBucketPrefix=RAW(pre-)&destinationBucketSuffix=RAW(-suff)")
  .to("mock:result");
```

In this case the objects consumed will be moved to myothercamelbucket bucket and deleted from the original one (because of deleteAfterRead set to true as default).

So if the file name is test, in the myothercamelbucket you should see a file called pre-test-suff.

## Using customer key as encryption

We introduced also the customer key support (an alternative of using KMS). The following code shows an example.

```java
String key = UUID.randomUUID().toString();
byte[] secretKey = generateSecretKey();
String b64Key = Base64.getEncoder().encodeToString(secretKey);
String b64KeyMd5 = Md5Utils.md5AsBase64(secretKey);

String awsEndpoint = "aws2-s3://mycamel?autoCreateBucket=false&useCustomerKey=true&customerKeyId=RAW(" + b64Key + ")&customerKeyMD5=RAW(" + b64KeyMd5 + ")&customerAlgorithm=" + AES256.name();

from("direct:putObject")
    .setHeader(AWS2S3Constants.KEY, constant("test.txt"))
    .setBody(constant("Test"))
    .to(awsEndpoint);
```

## Using a POJO as body

Sometimes build an AWS Request can be complex, because of multiple options. We introduce the possibility to use a POJO as body. In AWS S3 there are multiple operations you can submit, as an example for List brokers request, you can do something like:

```java
from("direct:aws2-s3")
     .setBody(ListObjectsRequest.builder().bucket(bucketName).build())
     .to("aws2-s3://test?amazonS3Client=#amazonS3Client&operation=listObjects&pojoRequest=true")
```

In this way you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

## Create S3 client and add component to registry

Sometimes you would want to perform some advanced configuration using AWS2S3Configuration which also allows to set the S3 client. You can create and set the S3 client in the component configuration as shown in the following example

```java
String awsBucketAccessKey = "your_access_key";
String awsBucketSecretKey = "your_secret_key";

S3Client s3Client = S3Client.builder().credentialsProvider(StaticCredentialsProvider.create(AwsBasicCredentials.create(awsBucketAccessKey, awsBucketSecretKey)))
                .region(Region.US_EAST_1).build();

AWS2S3Configuration configuration = new AWS2S3Configuration();
configuration.setAmazonS3Client(s3Client);
configuration.setAutoDiscoverClient(true);
configuration.setBucketName("s3bucket2020");
configuration.setRegion("us-east-1");
```

Now you can configure the S3 component (using the configuration object created above) and add it to the registry in the configure method before initialization of routes.

```java
AWS2S3Component s3Component = new AWS2S3Component(getContext());
s3Component.setConfiguration(configuration);
s3Component.setLazyStartProducer(true);
camelContext.addComponent("aws2-s3", s3Component);
```

Now your component will be used for all the operations implemented in camel routes.

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-s3</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-s3 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-s3-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 53 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-s3.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-s3.amazon-s3-client** | Reference to a com.amazonaws.services.s3.AmazonS3 in the registry. The option is a software.amazon.awssdk.services.s3.S3Client type. |  | S3Client |
| **camel.component.aws2-s3.amazon-s3-presigner** | An S3 Presigner for Request, used mainly in createDownloadLink operation. The option is a software.amazon.awssdk.services.s3.presigner.S3Presigner type. |  | S3Presigner |
| **camel.component.aws2-s3.auto-create-bucket** | Setting the autocreation of the S3 bucket bucketName. This will apply also in case of moveAfterRead option enabled and it will create the destinationBucket if it doesn’t exist already. | false | Boolean |
| **camel.component.aws2-s3.autoclose-body** | If this option is true and includeBody is false, then the S3Object.close() method will be called on exchange completion. This option is strongly related to includeBody option. In case of setting includeBody to false and autocloseBody to false, it will be up to the caller to close the S3Object stream. Setting autocloseBody to true, will close the S3Object stream automatically. | true | Boolean |
| **camel.component.aws2-s3.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-s3.aws-k-m-s-key-id** | Define the id of KMS key to use in case KMS is enabled. |  | String |
| **camel.component.aws2-s3.batch-message-number** | The number of messages composing a batch in streaming upload mode. | 10 | Integer |
| **camel.component.aws2-s3.batch-size** | The batch size (in bytes) in streaming upload mode. | 1000000 | Integer |
| **camel.component.aws2-s3.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws2-s3.configuration** | The component configuration. The option is a org.apache.camel.component.aws2.s3.AWS2S3Configuration type. |  | AWS2S3Configuration |
| **camel.component.aws2-s3.customer-algorithm** | Define the customer algorithm to use in case CustomerKey is enabled. |  | String |
| **camel.component.aws2-s3.customer-key-id** | Define the id of Customer key to use in case CustomerKey is enabled. |  | String |
| **camel.component.aws2-s3.customer-key-m-d5** | Define the MD5 of Customer key to use in case CustomerKey is enabled. |  | String |
| **camel.component.aws2-s3.delete-after-read** | Delete objects from S3 after they have been retrieved. The delete is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieve over and over again on the polls. Therefore you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the AWS2S3Constants#BUCKET\_NAME and AWS2S3Constants#KEY headers, or only the AWS2S3Constants#KEY header. | true | Boolean |
| **camel.component.aws2-s3.delete-after-write** | Delete file object after the S3 file has been uploaded. | false | Boolean |
| **camel.component.aws2-s3.delimiter** | The delimiter which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **camel.component.aws2-s3.destination-bucket** | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | String |
| **camel.component.aws2-s3.destination-bucket-prefix** | Define the destination bucket prefix to use when an object must be moved and moveAfterRead is set to true. |  | String |
| **camel.component.aws2-s3.destination-bucket-suffix** | Define the destination bucket suffix to use when an object must be moved and moveAfterRead is set to true. |  | String |
| **camel.component.aws2-s3.done-file-name** | If provided, Camel will only consume files if a done file exists. |  | String |
| **camel.component.aws2-s3.enabled** | Whether to enable auto configuration of the aws2-s3 component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-s3.file-name** | To get the object from the bucket with the given file name. |  | String |
| **camel.component.aws2-s3.force-path-style** | Set whether the S3 client should use path-style URL instead of virtual-hosted-style. | false | Boolean |
| **camel.component.aws2-s3.ignore-body** | If it is true, the S3 Object Body will be ignored completely, if it is set to false the S3 Object will be put in the body. Setting this to true, will override any behavior defined by includeBody option. | false | Boolean |
| **camel.component.aws2-s3.include-body** | If it is true, the S3Object exchange will be consumed and put into the body and closed. If false the S3Object stream will be put raw into the body and the headers will be set with the S3 object metadata. This option is strongly related to autocloseBody option. In case of setting includeBody to true because the S3Object stream will be consumed then it will also be closed, while in case of includeBody false then it will be up to the caller to close the S3Object stream. However setting autocloseBody to true when includeBody is false it will schedule to close the S3Object stream automatically on exchange completion. | true | Boolean |
| **camel.component.aws2-s3.include-folders** | If it is true, the folders/directories will be consumed. If it is false, they will be ignored, and Exchanges will not be created for those. | true | Boolean |
| **camel.component.aws2-s3.key-name** | Setting the key name for an element in the bucket through endpoint parameter. |  | String |
| **camel.component.aws2-s3.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-s3.move-after-read** | Move objects from S3 bucket to a different bucket after they have been retrieved. To accomplish the operation the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | Boolean |
| **camel.component.aws2-s3.multi-part-upload** | If it is true, camel will upload the file with multi part format, the part size is decided by the option of partSize. | false | Boolean |
| **camel.component.aws2-s3.naming-strategy** | The naming strategy to use in streaming upload mode. |  | AWSS3NamingStrategyEnum |
| **camel.component.aws2-s3.operation** | The operation to do in case the user don’t want to do only an upload. |  | AWS2S3Operations |
| **camel.component.aws2-s3.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-s3.part-size** | Setup the partSize which is used in multi part upload, the default size is 25M. | 26214400 | Long |
| **camel.component.aws2-s3.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws2-s3.policy** | The policy for this queue to set in the com.amazonaws.services.s3.AmazonS3#setBucketPolicy() method. |  | String |
| **camel.component.aws2-s3.prefix** | The prefix which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **camel.component.aws2-s3.proxy-host** | To define a proxy host when instantiating the SQS client. |  | String |
| **camel.component.aws2-s3.proxy-port** | Specify a proxy port to be used inside the client definition. |  | Integer |
| **camel.component.aws2-s3.proxy-protocol** | To define a proxy protocol when instantiating the S3 client. |  | Protocol |
| **camel.component.aws2-s3.region** | The region in which S3 client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-s3.restarting-policy** | The restarting policy to use in streaming upload mode. |  | AWSS3RestartingPolicyEnum |
| **camel.component.aws2-s3.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-s3.storage-class** | The storage class to set in the com.amazonaws.services.s3.model.PutObjectRequest request. |  | String |
| **camel.component.aws2-s3.streaming-upload-mode** | When stream mode is true the upload to bucket will be done in streaming. | false | Boolean |
| **camel.component.aws2-s3.streaming-upload-timeout** | While streaming upload mode is true, this option set the timeout to complete upload. |  | Long |
| **camel.component.aws2-s3.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-s3.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-s3.use-aws-k-m-s** | Define if KMS must be used or not. | false | Boolean |
| **camel.component.aws2-s3.use-customer-key** | Define if Customer Key must be used or not. | false | Boolean |
| **camel.component.aws2-s3.use-default-credentials-provider** | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-s3.use-s-s-e-s3** | Define if SSE S3 must be used or not. | false | Boolean |