# AWS S3 Storage Service

**Since Camel 3.2**

**Both producer and consumer are supported**

The AWS2 S3 component supports storing and retrieving objects from/to [Amazon’s S3](https://aws.amazon.com/s3) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon S3. More information is available at [Amazon S3](https://aws.amazon.com/s3).

## URI Format

aws2-s3://bucketNameOrArn\[?options\]

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

The AWS S3 Storage Service component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateBucket** (common) | Setting the autocreation of the S3 bucket bucketName. This will apply also in case of moveAfterRead option enabled, and it will create the destinationBucket if it doesn’t exist already. | false | boolean |
| **configuration** (common) | The component configuration. |  | AWS2S3Configuration |
| **delimiter** (common) | The delimiter which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **forcePathStyle** (common) | Set whether the S3 client should use path-style URL instead of virtual-hosted-style. | false | boolean |
| **ignoreBody** (common) | If it is true, the S3 Object Body will be ignored completely if it is set to false, the S3 Object will be put in the body. Setting this to true will override any behavior defined by includeBody option. | false | boolean |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **policy** (common) | The policy for this queue to set in the com.amazonaws.services.s3.AmazonS3#setBucketPolicy() method. |  | String |
| **prefix** (common) | The prefix which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **region** (common) | 
The region in which the S3 client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **customerAlgorithm** (common (advanced)) | Define the customer algorithm to use in case CustomerKey is enabled. |  | String |
| **customerKeyId** (common (advanced)) | Define the id of the Customer key to use in case CustomerKey is enabled. |  | String |
| **customerKeyMD5** (common (advanced)) | Define the MD5 of Customer key to use in case CustomerKey is enabled. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **deleteAfterRead** (consumer) | Delete objects from S3 after they have been retrieved. The deleting is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieved over and over again in the polls. Therefore, you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the AWS2S3Constants#BUCKET\_NAME and AWS2S3Constants#KEY headers, or only the AWS2S3Constants#KEY header. | true | boolean |
| **destinationBucket** (consumer) | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | String |
| **destinationBucketPrefix** (consumer) | Define the destination bucket prefix to use when an object must be moved, and moveAfterRead is set to true. |  | String |
| **destinationBucketSuffix** (consumer) | Define the destination bucket suffix to use when an object must be moved, and moveAfterRead is set to true. |  | String |
| **doneFileName** (consumer) | If provided, Camel will only consume files if a done file exists. |  | String |
| **fileName** (consumer) | To get the object from the bucket with the given file name. |  | String |
| **includeBody** (consumer) | If it is true, the S3Object exchange will be consumed and put into the body and closed. If false, the S3Object stream will be put raw into the body and the headers will be set with the S3 object metadata. This option is strongly related to the autocloseBody option. In case of setting includeBody to true because the S3Object stream will be consumed then it will also be closed, while in case of includeBody false then it will be up to the caller to close the S3Object stream. However, setting autocloseBody to true when includeBody is false it will schedule to close the S3Object stream automatically on exchange completion. | true | boolean |
| **includeFolders** (consumer) | If it is true, the folders/directories will be consumed. If it is false, they will be ignored, and Exchanges will not be created for those. | true | boolean |
| **moveAfterRead** (consumer) | Move objects from S3 bucket to a different bucket after they have been retrieved. To accomplish the operation, the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | boolean |
| **removePrefixOnMove** (consumer) | Remove the contents of the prefix configuration string from the new S3Object key before copying. For example, if prefix is set to 'demo/notify' and the destinationBucketPrefix is set to 'demo/archive', an S3Object with a key of 'demo/notify/example.txt' will be copied to 'demo/archive/example.txt', rather than the default behavior where the new key is 'demo/archive/demo/notify/example.txt'. Only applicable when moveAfterRead is true. | false | boolean |
| **autocloseBody** (consumer (advanced)) | If this option is true and includeBody is false, then the S3Object.close() method will be called on exchange completion. This option is strongly related to includeBody option. In case of setting includeBody to false and autocloseBody to false, it will be up to the caller to close the S3Object stream. Setting autocloseBody to true, will close the S3Object stream automatically. | true | boolean |
| **batchMessageNumber** (producer) | The number of messages composing a batch in streaming upload mode. | 10 | int |
| **batchSize** (producer) | The batch size (in bytes) in streaming upload mode. | 1000000 | int |
| **bufferSize** (producer) | The buffer size (in bytes) in streaming upload mode. | 1000000 | int |
| **deleteAfterWrite** (producer) | Delete file object after the S3 file has been uploaded. | false | boolean |
| **keyName** (producer) | Setting the key name for an element in the bucket through endpoint parameter. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **multiPartUpload** (producer) | If it is true, camel will upload the file with multipart format. The part size is decided by the partSize option. Camel will only do multipart uploads for files that are larger than the part-size thresholds. Files that are smaller will be uploaded in a single operation. | false | boolean |
| **namingStrategy** (producer) | 

The naming strategy to use in streaming upload mode.

Enum values:

-   progressive
    
-   random
    
-   timestamp
    





 | progressive | AWSS3NamingStrategyEnum |
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
    
-   headBucket
    
-   headObject
    
-   restoreObject
    
-   getObjectTagging
    
-   putObjectTagging
    
-   deleteObjectTagging
    
-   getObjectAcl
    
-   putObjectAcl
    
-   createBucket
    
-   getBucketTagging
    
-   putBucketTagging
    
-   deleteBucketTagging
    
-   getBucketVersioning
    
-   putBucketVersioning
    
-   getBucketPolicy
    
-   putBucketPolicy
    
-   deleteBucketPolicy
    





 |  | AWS2S3Operations |
| **partSize** (producer) | Set up the partSize which is used in multipart upload, the default size is 25 MB. The minimum size in AWS is 5 MB. Camel will only do multipart uploads for files that are larger than the part-size thresholds. Files that are smaller will be uploaded in a single operation. | 26214400 | long |
| **restartingPolicy** (producer) | 

The restarting policy to use in streaming upload mode.

Enum values:

-   override
    
-   lastPart
    





 | override | AWSS3RestartingPolicyEnum |
| **storageClass** (producer) | The storage class to set in the com.amazonaws.services.s3.model.PutObjectRequest request. |  | String |
| **streamingUploadMode** (producer) | When stream mode is true, the upload to bucket will be done in streaming. | false | boolean |
| **streamingUploadTimeout** (producer) | While streaming upload mode is true, this option set the timeout to complete upload. |  | long |
| **timestampGroupingEnabled** (producer) | Enable timestamp-based grouping of messages into time windows for file creation. When enabled, messages are grouped by their timestamp header into time windows. | false | boolean |
| **timestampHeaderName** (producer) | The name of the message header containing the timestamp for grouping. Default is CamelMessageTimestamp. | CamelMessageTimestamp | String |
| **timestampWindowSizeMillis** (producer) | The size of the time window in milliseconds for timestamp-based grouping. Messages within the same time window will be written to the same file. Default is 300000 (5 minutes). | 300000 | long |
| **awsKMSKeyId** (producer (advanced)) | Define the id of KMS key to use in case KMS is enabled. |  | String |
| **conditionalWritesEnabled** (producer (advanced)) | Uploads the object only if the object key name does not already exist in the bucket specified. | false | boolean |
| **useAwsKMS** (producer (advanced)) | Define if KMS must be used or not. | false | boolean |
| **useCustomerKey** (producer (advanced)) | Define if Customer Key must be used or not. | false | boolean |
| **useSSES3** (producer (advanced)) | Define if SSE S3 must be used or not. | false | boolean |
| **amazonS3Client** (advanced) | **Autowired** Reference to a com.amazonaws.services.s3.AmazonS3 in the registry. |  | S3Client |
| **amazonS3Presigner** (advanced) | **Autowired** An S3 Presigner for Request, used mainly in createDownloadLink operation. |  | S3Presigner |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SQS client. |  | String |
| **proxyPort** (proxy) | Specify a proxy port to be used inside the client definition. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the S3 client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the S3 client should expect to load credentials through a default credentials provider. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the S3 client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the S3 client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in S3. | false | boolean |

## Endpoint Options

The AWS S3 Storage Service endpoint is configured using URI syntax:

aws2-s3://bucketNameOrArn

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bucketNameOrArn** (common) | **Required** Bucket name or ARN. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateBucket** (common) | Setting the autocreation of the S3 bucket bucketName. This will apply also in case of moveAfterRead option enabled, and it will create the destinationBucket if it doesn’t exist already. | false | boolean |
| **delimiter** (common) | The delimiter which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **forcePathStyle** (common) | Set whether the S3 client should use path-style URL instead of virtual-hosted-style. | false | boolean |
| **ignoreBody** (common) | If it is true, the S3 Object Body will be ignored completely if it is set to false, the S3 Object will be put in the body. Setting this to true will override any behavior defined by includeBody option. | false | boolean |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **policy** (common) | The policy for this queue to set in the com.amazonaws.services.s3.AmazonS3#setBucketPolicy() method. |  | String |
| **prefix** (common) | The prefix which is used in the com.amazonaws.services.s3.model.ListObjectsRequest to only consume objects we are interested in. |  | String |
| **region** (common) | 
The region in which the S3 client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **customerAlgorithm** (common (advanced)) | Define the customer algorithm to use in case CustomerKey is enabled. |  | String |
| **customerKeyId** (common (advanced)) | Define the id of the Customer key to use in case CustomerKey is enabled. |  | String |
| **customerKeyMD5** (common (advanced)) | Define the MD5 of Customer key to use in case CustomerKey is enabled. |  | String |
| **deleteAfterRead** (consumer) | Delete objects from S3 after they have been retrieved. The deleting is only performed if the Exchange is committed. If a rollback occurs, the object is not deleted. If this option is false, then the same objects will be retrieved over and over again in the polls. Therefore, you need to use the Idempotent Consumer EIP in the route to filter out duplicates. You can filter using the AWS2S3Constants#BUCKET\_NAME and AWS2S3Constants#KEY headers, or only the AWS2S3Constants#KEY header. | true | boolean |
| **destinationBucket** (consumer) | Define the destination bucket where an object must be moved when moveAfterRead is set to true. |  | String |
| **destinationBucketPrefix** (consumer) | Define the destination bucket prefix to use when an object must be moved, and moveAfterRead is set to true. |  | String |
| **destinationBucketSuffix** (consumer) | Define the destination bucket suffix to use when an object must be moved, and moveAfterRead is set to true. |  | String |
| **doneFileName** (consumer) | If provided, Camel will only consume files if a done file exists. |  | String |
| **fileName** (consumer) | To get the object from the bucket with the given file name. |  | String |
| **includeBody** (consumer) | If it is true, the S3Object exchange will be consumed and put into the body and closed. If false, the S3Object stream will be put raw into the body and the headers will be set with the S3 object metadata. This option is strongly related to the autocloseBody option. In case of setting includeBody to true because the S3Object stream will be consumed then it will also be closed, while in case of includeBody false then it will be up to the caller to close the S3Object stream. However, setting autocloseBody to true when includeBody is false it will schedule to close the S3Object stream automatically on exchange completion. | true | boolean |
| **includeFolders** (consumer) | If it is true, the folders/directories will be consumed. If it is false, they will be ignored, and Exchanges will not be created for those. | true | boolean |
| **maxConnections** (consumer) | **Deprecated** Set the maxConnections parameter in the S3 client configuration. This option is deprecated and has no effect. Use the httpClientBuilder option on the S3 client configuration to customize the HTTP client connection pool. | 60 | int |
| **maxMessagesPerPoll** (consumer) | Gets the maximum number of messages as a limit to poll at each polling. Gets the maximum number of messages as a limit to poll at each polling. The default value is 10. Use 0 or a negative number to set it as unlimited. | 10 | int |
| **moveAfterRead** (consumer) | Move objects from S3 bucket to a different bucket after they have been retrieved. To accomplish the operation, the destinationBucket option must be set. The copy bucket operation is only performed if the Exchange is committed. If a rollback occurs, the object is not moved. | false | boolean |
| **removePrefixOnMove** (consumer) | Remove the contents of the prefix configuration string from the new S3Object key before copying. For example, if prefix is set to 'demo/notify' and the destinationBucketPrefix is set to 'demo/archive', an S3Object with a key of 'demo/notify/example.txt' will be copied to 'demo/archive/example.txt', rather than the default behavior where the new key is 'demo/archive/demo/notify/example.txt'. Only applicable when moveAfterRead is true. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **autocloseBody** (consumer (advanced)) | If this option is true and includeBody is false, then the S3Object.close() method will be called on exchange completion. This option is strongly related to includeBody option. In case of setting includeBody to false and autocloseBody to false, it will be up to the caller to close the S3Object stream. Setting autocloseBody to true, will close the S3Object stream automatically. | true | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **inProgressRepository** (consumer (advanced)) | A pluggable in-progress repository org.apache.camel.spi.IdempotentRepository. The in-progress repository is used to account the current in progress files being consumed. By default a memory based repository is used. |  | IdempotentRepository |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **batchMessageNumber** (producer) | The number of messages composing a batch in streaming upload mode. | 10 | int |
| **batchSize** (producer) | The batch size (in bytes) in streaming upload mode. | 1000000 | int |
| **bufferSize** (producer) | The buffer size (in bytes) in streaming upload mode. | 1000000 | int |
| **deleteAfterWrite** (producer) | Delete file object after the S3 file has been uploaded. | false | boolean |
| **keyName** (producer) | Setting the key name for an element in the bucket through endpoint parameter. |  | String |
| **multiPartUpload** (producer) | If it is true, camel will upload the file with multipart format. The part size is decided by the partSize option. Camel will only do multipart uploads for files that are larger than the part-size thresholds. Files that are smaller will be uploaded in a single operation. | false | boolean |
| **namingStrategy** (producer) | 

The naming strategy to use in streaming upload mode.

Enum values:

-   progressive
    
-   random
    
-   timestamp
    





 | progressive | AWSS3NamingStrategyEnum |
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
    
-   headBucket
    
-   headObject
    
-   restoreObject
    
-   getObjectTagging
    
-   putObjectTagging
    
-   deleteObjectTagging
    
-   getObjectAcl
    
-   putObjectAcl
    
-   createBucket
    
-   getBucketTagging
    
-   putBucketTagging
    
-   deleteBucketTagging
    
-   getBucketVersioning
    
-   putBucketVersioning
    
-   getBucketPolicy
    
-   putBucketPolicy
    
-   deleteBucketPolicy
    





 |  | AWS2S3Operations |
| **partSize** (producer) | Set up the partSize which is used in multipart upload, the default size is 25 MB. The minimum size in AWS is 5 MB. Camel will only do multipart uploads for files that are larger than the part-size thresholds. Files that are smaller will be uploaded in a single operation. | 26214400 | long |
| **restartingPolicy** (producer) | 

The restarting policy to use in streaming upload mode.

Enum values:

-   override
    
-   lastPart
    





 | override | AWSS3RestartingPolicyEnum |
| **storageClass** (producer) | The storage class to set in the com.amazonaws.services.s3.model.PutObjectRequest request. |  | String |
| **streamingUploadMode** (producer) | When stream mode is true, the upload to bucket will be done in streaming. | false | boolean |
| **streamingUploadTimeout** (producer) | While streaming upload mode is true, this option set the timeout to complete upload. |  | long |
| **timestampGroupingEnabled** (producer) | Enable timestamp-based grouping of messages into time windows for file creation. When enabled, messages are grouped by their timestamp header into time windows. | false | boolean |
| **timestampHeaderName** (producer) | The name of the message header containing the timestamp for grouping. Default is CamelMessageTimestamp. | CamelMessageTimestamp | String |
| **timestampWindowSizeMillis** (producer) | The size of the time window in milliseconds for timestamp-based grouping. Messages within the same time window will be written to the same file. Default is 300000 (5 minutes). | 300000 | long |
| **awsKMSKeyId** (producer (advanced)) | Define the id of KMS key to use in case KMS is enabled. |  | String |
| **conditionalWritesEnabled** (producer (advanced)) | Uploads the object only if the object key name does not already exist in the bucket specified. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **useAwsKMS** (producer (advanced)) | Define if KMS must be used or not. | false | boolean |
| **useCustomerKey** (producer (advanced)) | Define if Customer Key must be used or not. | false | boolean |
| **useSSES3** (producer (advanced)) | Define if SSE S3 must be used or not. | false | boolean |
| **amazonS3Client** (advanced) | **Autowired** Reference to a com.amazonaws.services.s3.AmazonS3 in the registry. |  | S3Client |
| **amazonS3Presigner** (advanced) | **Autowired** An S3 Presigner for Request, used mainly in createDownloadLink operation. |  | S3Presigner |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SQS client. |  | String |
| **proxyPort** (proxy) | Specify a proxy port to be used inside the client definition. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the S3 client.

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
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the S3 client should expect to load credentials through a default credentials provider. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the S3 client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the S3 client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in S3. | false | boolean |

## Message Headers

The AWS S3 Storage Service component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsS3BucketName** (common) Constant: [`BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#BUCKET_NAME) | The bucket Name (can be dynamic using the simple language in the producer) which this object will be stored or which will be used for the current operation or in which this object is contained. |  | String |
| **CamelAwsS3ProducedBucketName** (producer) Constant: [`PRODUCED_BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#PRODUCED_BUCKET_NAME) | The computed bucket name that was used by the producer such as to get or put an s3 object. |  | String |
| **CamelAwsS3BucketDestinationName** (producer) Constant: [`BUCKET_DESTINATION_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#BUCKET_DESTINATION_NAME) | The bucket Destination Name which will be used for the current operation. |  | String |
| **CamelAwsS3BucketExists** (common) Constant: [`BUCKET_EXISTS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#BUCKET_EXISTS) | Whether the bucket exists when using the headBucket operation. |  | boolean |
| **CamelAwsS3ContentControl** (common) Constant: [`CACHE_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CACHE_CONTROL) | The optional Cache-Control HTTP header which allows the user to specify caching behavior along the HTTP request/reply chain. |  | String |
| **CamelAwsS3ContentDisposition** (common) Constant: [`CONTENT_DISPOSITION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_DISPOSITION) | The optional Content-Disposition HTTP header, which specifies presentational information such as the recommended filename for the object to be saved as. |  | String |
| **CamelAwsS3ContentEncoding** (common) Constant: [`CONTENT_ENCODING`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_ENCODING) | The optional Content-Encoding HTTP header specifying what content encodings have been applied to the object and what decoding mechanisms must be applied in order to obtain the media-type referenced by the Content-Type field. |  | String |
| **CamelAwsS3ContentLength** (common) Constant: [`CONTENT_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_LENGTH) | The Content-Length HTTP header indicating the size of the associated object in bytes. |  | Long |
| **CamelAwsS3ContentMD5** (common) Constant: [`CONTENT_MD5`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_MD5) | The base64 encoded 128-bit MD5 digest of the associated object (content - not including headers) according to RFC 1864. This data is used as a message integrity check to verify that the data received by Amazon S3 is the same data that the caller sent. |  | String |
| **CamelAwsS3ContentType** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#CONTENT_TYPE) | The Content-Type HTTP header, which indicates the type of content stored in the associated object. The value of this header is a standard MIME type. |  | String |
| **CamelAwsS3ETag** (common) Constant: [`E_TAG`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#E_TAG) | (producer) The ETag value for the newly uploaded object. (consumer) The hex encoded 128-bit MD5 digest of the associated object according to RFC 1864. This data is used as an integrity check to verify that the data received by the caller is the same data that was sent by Amazon S3. |  | String |
| **CamelAwsS3Key** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#KEY) | The key (can be dynamic using the simple language in the producer) under which this object is stored or will be stored or which will be used for the current operation. |  | String |
| **CamelAwsS3ProducedKey** (producer) Constant: [`PRODUCED_KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#PRODUCED_KEY) | The computed key that was used for retrieving this object. |  | String |
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
| **CamelAwsS3GrantFullControl** (producer) Constant: [`GRANT_FULL_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#GRANT_FULL_CONTROL) | Gives the grantee READ, READ\_ACP, and WRITE\_ACP permissions on the object. The value is a grantee expression such as id=, emailAddress= or uri=. |  | String |
| **CamelAwsS3GrantRead** (producer) Constant: [`GRANT_READ`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#GRANT_READ) | Allows the grantee to read the object data and its metadata. The value is a grantee expression such as id=, emailAddress= or uri=. |  | String |
| **CamelAwsS3GrantReadACP** (producer) Constant: [`GRANT_READ_ACP`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#GRANT_READ_ACP) | Allows the grantee to read the object ACL. The value is a grantee expression such as id=, emailAddress= or uri=. |  | String |
| **CamelAwsS3GrantWriteACP** (producer) Constant: [`GRANT_WRITE_ACP`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#GRANT_WRITE_ACP) | Allows the grantee to write the ACL for the object. The value is a grantee expression such as id=, emailAddress= or uri=. |  | String |
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
    
-   COMPLETED
    
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
| **CamelAwsS3IfMatchCondition** (common) Constant: [`IF_MATCH_CONDITION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#IF_MATCH_CONDITION) | Return/copy the object only if its entity tag (ETag) is the same as the one specified in this header. |  | String |
| **CamelAwsS3IfModifiedSinceCondition** (common) Constant: [`IF_MODIFIED_SINCE_CONDITION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#IF_MODIFIED_SINCE_CONDITION) | Return/copy the object only if it has been modified since the specified time; otherwise, return a 304 Not Modified error. |  | String |
| **CamelAwsS3IfNoneMatchCondition** (common) Constant: [`IF_NONE_MATCH_CONDITION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#IF_NONE_MATCH_CONDITION) | Return/copy the object only if its entity tag (ETag) is different from the one specified in this header. |  | String |
| **CamelAwsS3IfUnmodifiedSinceCondition** (common) Constant: [`IF_UNMODIFIED_SINCE_CONDITION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#IF_UNMODIFIED_SINCE_CONDITION) | Return/copy the object only if it has not been modified since the specified time. |  | String |
| **CamelAwsS3OverrideBucketName** (common) Constant: [`OVERRIDE_BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#OVERRIDE_BUCKET_NAME) | The bucket Name to override (can be dynamic using the simple language in the producer) which this object will be stored or which will be used for the current operation or in which this object is contained. |  | String |
| **CamelAwsS3KeysToDelete** (producer) Constant: [`KEYS_TO_DELETE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#KEYS_TO_DELETE) | A list of keys to delete when using deleteObjects operation. |  | List |
| **CamelAwsS3RestoreDays** (producer) Constant: [`RESTORE_DAYS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#RESTORE_DAYS) | The number of days for which the restore request will remain active when using restoreObject operation. |  | Integer |
| **CamelAwsS3RestoreTier** (producer) Constant: [`RESTORE_TIER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#RESTORE_TIER) | The tier at which the restore will be processed when using restoreObject operation (e.g., Standard, Bulk, Expedited). |  | String |
| **CamelAwsS3ObjectTags** (producer) Constant: [`OBJECT_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#OBJECT_TAGS) | The object tags to set when using putObjectTagging operation. |  | Map |
| **CamelAwsS3BucketTags** (producer) Constant: [`BUCKET_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#BUCKET_TAGS) | The bucket tags to set when using putBucketTagging operation. |  | Map |
| **CamelAwsS3BucketPolicy** (producer) Constant: [`BUCKET_POLICY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#BUCKET_POLICY) | The bucket policy as JSON string when using putBucketPolicy operation. |  | String |
| **CamelAwsS3VersioningStatus** (producer) Constant: [`VERSIONING_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#VERSIONING_STATUS) | The versioning status (Enabled or Suspended) when using putBucketVersioning operation. |  | String |
| **CamelAwsS3MfaDelete** (producer) Constant: [`MFA_DELETE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#MFA_DELETE) | Whether to enable MFA delete when using putBucketVersioning operation. |  | String |
| **CamelAwsS3UploadLinkExpirationTime** (producer) Constant: [`UPLOAD_LINK_EXPIRATION_TIME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#UPLOAD_LINK_EXPIRATION_TIME) | The expiration time of the upload link in milliseconds. |  | Long |
| **CamelAwsS3UploadLinkBrowserCompatible** (producer) Constant: [`UPLOAD_LINK_BROWSER_COMPATIBLE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#UPLOAD_LINK_BROWSER_COMPATIBLE) | Whether the upload link is browser compatible. |  | boolean |
| **CamelAwsS3UploadLinkHttpRequestHeaders** (producer) Constant: [`UPLOAD_LINK_HTTP_REQUEST_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#UPLOAD_LINK_HTTP_REQUEST_HEADERS) | The headers that are needed by the service for upload (not needed when BrowserCompatible is true). |  | Map |
| **CamelAwsS3UploadLinkSignedPayload** (producer) Constant: [`UPLOAD_LINK_SIGNED_PAYLOAD`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3/latest/org/apache/camel/component/aws2/s3/AWS2S3Constants.html#UPLOAD_LINK_SIGNED_PAYLOAD) | The request payload that is needed by the service for upload (not needed when BrowserCompatible is true). |  | String |

Required S3 component options

You have to provide the amazonS3Client in the Registry or your accessKey and secretKey to access the [Amazon’s S3](https://aws.amazon.com/s3).

## Usage

### Batch Consumer

This component implements the Batch Consumer.

This allows you, for instance, to know how many messages exist in this batch and for instance, let the Aggregator aggregate this number of messages.

### S3 Producer operations

Camel-AWS2-S3 component provides the following operation on the producer side:

-   copyObject
    
-   deleteObject
    
-   deleteObjects
    
-   listBuckets
    
-   deleteBucket
    
-   listObjects
    
-   getObject (this will return an S3Object instance)
    
-   getObjectRange (this will return an S3Object instance)
    
-   createDownloadLink
    
-   createUploadLink
    
-   headBucket
    
-   headObject
    
-   restoreObject
    
-   getObjectTagging
    
-   putObjectTagging
    
-   deleteObjectTagging
    
-   getObjectAcl
    
-   putObjectAcl
    
-   createBucket
    
-   getBucketTagging
    
-   putBucketTagging
    
-   deleteBucketTagging
    
-   getBucketVersioning
    
-   putBucketVersioning
    
-   getBucketPolicy
    
-   putBucketPolicy
    
-   deleteBucketPolicy
    

If you don’t specify an operation, explicitly the producer will do:

-   a single file upload
    
-   a multipart upload if multiPartUpload option is enabled
    

## Examples

For example, to read file `hello.txt` from bucket `helloBucket`, use the following snippet:

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws2-s3://helloBucket?accessKey=yourAccessKey&secretKey=yourSecretKey&prefix=hello.txt")
    .to("file:/var/downloaded");
```

```xml
<route>
  <from uri="aws2-s3://helloBucket?accessKey=yourAccessKey&amp;secretKey=yourSecretKey&amp;prefix=hello.txt"/>
  <to uri="file:/var/downloaded"/>
</route>
```

```yaml
- route:
    from:
      uri: aws2-s3://helloBucket
      parameters:
        accessKey: yourAccessKey
        secretKey: yourSecretKey
        prefix: hello.txt
      steps:
        - to:
            uri: file:/var/downloaded
```

### Advanced AmazonS3 configuration

If your Camel Application is running behind a firewall or if you need to have more control over the `S3Client` instance configuration, you can create your own instance and refer to it in your Camel aws2-s3 component configuration:

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws2-s3://MyBucket?amazonS3Client=#client&delay=5000&maxMessagesPerPoll=5")
    .to("mock:result");
```

```xml
<route>
  <from uri="aws2-s3://MyBucket?amazonS3Client=#client&amp;delay=5000&amp;maxMessagesPerPoll=5"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: aws2-s3://MyBucket
      parameters:
        amazonS3Client: "#client"
        delay: 5000
        maxMessagesPerPoll: 5
      steps:
        - to:
            uri: mock:result
```

### Use KMS with the S3 component

To use AWS KMS to encrypt/decrypt data by using AWS infrastructure, you can use the options introduced in 2.21.x like in the following example

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:tmp/test?fileName=test.txt")
    .setHeader("CamelAwsS3Key", constant("testFile"))
    .to("aws2-s3://mybucket?amazonS3Client=#client&useAwsKMS=true&awsKMSKeyId=3f0637ad-296a-3dfe-a796-e60654fb128c");
```

```xml
<route>
  <from uri="file:tmp/test?fileName=test.txt"/>
  <setHeader name="CamelAwsS3Key">
    <constant>testFile</constant>
  </setHeader>
  <to uri="aws2-s3://mybucket?amazonS3Client=#client&amp;useAwsKMS=true&amp;awsKMSKeyId=3f0637ad-296a-3dfe-a796-e60654fb128c"/>
</route>
```

```yaml
- route:
    from:
      uri: file:tmp/test
      parameters:
        fileName: test.txt
      steps:
        - setHeader:
            name: CamelAwsS3Key
            constant: testFile
        - to:
            uri: aws2-s3://mybucket
            parameters:
              amazonS3Client: "#client"
              useAwsKMS: true
              awsKMSKeyId: "3f0637ad-296a-3dfe-a796-e60654fb128c"
```

> **Tip**
> The Java example uses the string value `"CamelAwsS3Key"` directly. You can also use the Java constant `AWS2S3Constants.KEY`.

In this way, you’ll ask S3 to use the KMS key 3f0637ad-296a-3dfe-a796-e60654fb128c, to encrypt the file test.txt. When you ask to download this file, the decryption will be done directly before the download.

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

### Bucket Auto-creation

With the option `autoCreateBucket` users are able to avoid the auto-creation of an S3 Bucket in case it doesn’t exist. The default for this option is `false`. If set to false, any operation on a not-existent bucket in AWS won’t be successful and an error will be returned.

### Moving stuff between a bucket and another bucket

Some users like to consume stuff from a bucket and move the content in a different one without using the copyObject feature of this component. If this is case for you, remember to remove the bucketName header from the incoming exchange of the consumer, otherwise the file will always be overwritten on the same original bucket.

### Using the customer key as encryption

We introduced also the customer key support (an alternative of using KMS). The following code shows an example.

_Java-only: programmatic customer key encryption setup_

```java
String key = UUID.randomUUID().toString();
byte[] secretKey = generateSecretKey();
String b64Key = Base64.getEncoder().encodeToString(secretKey);
String b64KeyMd5 = Md5Utils.md5AsBase64(secretKey);

String awsEndpoint = "aws2-s3://mycamel?autoCreateBucket=false&useCustomerKey=true&customerKeyId=RAW(" + b64Key + ")&customerKeyMD5=RAW(" + b64KeyMd5 + ")&customerAlgorithm=" + AES256.name();

from("direct:putObject")
    .setHeader("CamelAwsS3Key", constant("test.txt"))
    .setBody(constant("Test"))
    .to(awsEndpoint);
```

### Using a POJO as body

Sometimes building an AWS Request can be complex because of multiple options. We introduce the possibility to use a POJO as the body. In AWS S3 there are multiple operations you can submit, as an example for List objects request, you can do something like:

_Java-only: POJO request requires building AWS SDK request objects_

```java
from("direct:aws2-s3")
    .setBody(ListObjectsV2Request.builder().bucket(bucketName).build())
    .to("aws2-s3://test?amazonS3Client=#amazonS3Client&operation=listObjects&pojoRequest=true");
```

In this way, you’ll pass the request directly without the need of passing headers and options specifically related to this operation.

### Create S3 client and add component to registry

Sometimes you would want to perform some advanced configuration using AWS2S3Configuration, which also allows to set the S3 client. You can create and set the S3 client in the component configuration as shown in the following example

_Java-only: programmatic S3 client creation_

```java
String awsBucketAccessKey = "your_access_key";
String awsBucketSecretKey = "your_secret_key";

S3Client s3Client = S3Client.builder()
        .credentialsProvider(StaticCredentialsProvider.create(
                AwsBasicCredentials.create(awsBucketAccessKey, awsBucketSecretKey)))
        .region(Region.US_EAST_1).build();

AWS2S3Configuration configuration = new AWS2S3Configuration();
configuration.setAmazonS3Client(s3Client);
configuration.setAutoDiscoverClient(true);
configuration.setBucketName("s3bucket2020");
configuration.setRegion("us-east-1");
```

Now you can configure the S3 component (using the configuration object created above) and add it to the registry in the configure method before initialization of routes.

_Java-only: programmatic component registration_

```java
AWS2S3Component s3Component = new AWS2S3Component(getContext());
s3Component.setConfiguration(configuration);
s3Component.setLazyStartProducer(true);
camelContext.addComponent("aws2-s3", s3Component);
```

Now your component will be used for all the operations implemented in camel routes.

### Note about using this component for storing and retrieving objects from/to Dell ECS (Elastic Cloud Solutions)

For storing and retrieving objects from/to Dell ECS, both of the `forcePathStyle` and `overrideEndpoint` options need to be set to `true` and using the `uriEndpointOverride` you need to provide your own ECS endpoint.

_Java-only: programmatic Dell ECS configuration_

```java
String awsBucketAccessKey = "your_access_key";
String awsBucketSecretKey = "your_secret_key";

S3Client s3Client = S3Client.builder()
        .credentialsProvider(StaticCredentialsProvider.create(
                AwsBasicCredentials.create(awsBucketAccessKey, awsBucketSecretKey)))
        .region(Region.US_EAST_1).build();

AWS2S3Configuration configuration = new AWS2S3Configuration();
configuration.setForcePathStyle(true);
configuration.setOverrideEndpoint(true);
configuration.setUriEndpointOverride("http://ecs1.emc.com:9020");
```

For more details see [their documentation](https://www.dell.com/support/manuals/en-us/ecs-appliance-/ecs_pub_data_access_guide_3_3_to_3_6/using-the-java-amazon-sdk?guid=guid-149be134-6938-4cd7-9503-cf3ca9d23261&lang=en-us).

## Sub-Pages

For more details on specific features, see:

-   [Producer Operations](others/aws2-s3-producer-operations.md) - All producer operation examples with minimum IAM permissions
    
-   [Streaming Upload](others/aws2-s3-streaming.md) - Streaming upload mode, naming strategies, and timestamp grouping
    
-   [Consumer Examples](others/aws2-s3-consumer-examples.md) - Consumer patterns including prefix filtering, polling strategies, and done files
    

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