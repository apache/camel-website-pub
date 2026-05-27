# AWS S3 Vectors

**Since Camel 4.17**

**Both producer and consumer are supported**

The AWS S3 Vectors component stores and queries vector embeddings using [Amazon S3 Vectors](https://aws.amazon.com/s3/features/vectors/).

Prerequisites

You need an AWS account with access to S3 Vectors. See [Amazon S3 Vectors](https://aws.amazon.com/s3/features/vectors/).

## URI Format

aws2-s3-vectors://vectorBucketName\[?options\]

You can append query options to the URI:

`?option1=value&option2=value&…​`

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

The AWS S3 Vectors component supports 33 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | The component configuration. |  | AWS2S3VectorsConfiguration |
| **dataType** (common) | 
The data type of the vector. Options: float32, float16.

Enum values:

-   float32
    
-   float16
    





 | float32 | String |
| **distanceMetric** (common) | 

The distance metric to use for similarity search. Options: cosine, euclidean, dot-product.

Enum values:

-   cosine
    
-   euclidean
    
-   dot-product
    





 | cosine | String |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **region** (common) | 

The region in which S3 Vectors client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1).

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
| **similarityThreshold** (common) | The minimum similarity threshold for results. |  | Float |
| **topK** (common) | The number of top similar vectors to return in a query. | 10 | Integer |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **vectorDimensions** (common) | The dimensions of the vector embeddings (default: 1536, which is the dimension for OpenAI text-embedding-3-small). | 1536 | Integer |
| **vectorIndexName** (common) | The name of the vector index. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerMetadataFilter** (consumer) | Optional metadata filter for the consumer to filter vectors during polling. |  | String |
| **consumerQueryVector** (consumer) | The query vector to use for the consumer to poll for similar vectors. Specified as comma-separated float values (e.g., 0.1,0.2,0.3). If not specified, the consumer will not poll. |  | String |
| **delay** (consumer) | Milliseconds before the next poll for the consumer. | 500 | long |
| **deleteAfterRead** (consumer) | Delete vectors after they have been consumed. | false | boolean |
| **maxMessagesPerPoll** (consumer) | The maximum number of messages to consume per poll for the consumer. | 10 | int |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 

The operation to perform.

Enum values:

-   putVectors
    
-   queryVectors
    
-   deleteVectors
    
-   getVectors
    
-   createVectorBucket
    
-   deleteVectorBucket
    
-   listVectorBuckets
    
-   describeVectorBucket
    
-   createVectorIndex
    
-   deleteVectorIndex
    
-   listVectorIndexes
    
-   describeVectorIndex
    





 |  | AWS2S3VectorsOperations |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **s3VectorsClient** (advanced) | **Autowired** Reference to a software.amazon.awssdk.services.s3vectors.S3VectorsClient in the registry. |  | S3VectorsClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the S3 Vectors client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the S3 Vectors client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the S3 Vectors client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the S3 Vectors client should expect to load credentials through a default credentials provider. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the S3 Vectors client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the S3 Vectors client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in S3 Vectors. | false | boolean |

## Endpoint Options

The AWS S3 Vectors endpoint is configured using URI syntax:

aws2-s3-vectors://vectorBucketName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **vectorBucketName** (common) | **Required** Vector bucket name or ARN. |  | String |

### Query Parameters (46 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataType** (common) | 
The data type of the vector. Options: float32, float16.

Enum values:

-   float32
    
-   float16
    





 | float32 | String |
| **distanceMetric** (common) | 

The distance metric to use for similarity search. Options: cosine, euclidean, dot-product.

Enum values:

-   cosine
    
-   euclidean
    
-   dot-product
    





 | cosine | String |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **region** (common) | 

The region in which S3 Vectors client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1).

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
| **similarityThreshold** (common) | The minimum similarity threshold for results. |  | Float |
| **topK** (common) | The number of top similar vectors to return in a query. | 10 | Integer |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **vectorDimensions** (common) | The dimensions of the vector embeddings (default: 1536, which is the dimension for OpenAI text-embedding-3-small). | 1536 | Integer |
| **vectorIndexName** (common) | The name of the vector index. |  | String |
| **consumerMetadataFilter** (consumer) | Optional metadata filter for the consumer to filter vectors during polling. |  | String |
| **consumerQueryVector** (consumer) | The query vector to use for the consumer to poll for similar vectors. Specified as comma-separated float values (e.g., 0.1,0.2,0.3). If not specified, the consumer will not poll. |  | String |
| **delay** (consumer) | Milliseconds before the next poll for the consumer. | 500 | long |
| **deleteAfterRead** (consumer) | Delete vectors after they have been consumed. | false | boolean |
| **maxMessagesPerPoll** (consumer) | The maximum number of messages to consume per poll for the consumer. | 10 | int |
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

The operation to perform.

Enum values:

-   putVectors
    
-   queryVectors
    
-   deleteVectors
    
-   getVectors
    
-   createVectorBucket
    
-   deleteVectorBucket
    
-   listVectorBuckets
    
-   describeVectorBucket
    
-   createVectorIndex
    
-   deleteVectorIndex
    
-   listVectorIndexes
    
-   describeVectorIndex
    





 |  | AWS2S3VectorsOperations |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **s3VectorsClient** (advanced) | **Autowired** Reference to a software.amazon.awssdk.services.s3vectors.S3VectorsClient in the registry. |  | S3VectorsClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the S3 Vectors client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the S3 Vectors client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the S3 Vectors client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
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
| **useDefaultCredentialsProvider** (security) | Set whether the S3 Vectors client should expect to load credentials through a default credentials provider. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the S3 Vectors client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the S3 Vectors client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in S3 Vectors. | false | boolean |

## Message Headers

The AWS S3 Vectors component supports 17 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsS3VectorsOperation** (common) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelAwsS3VectorsVectorBucketName** (common) Constant: [`VECTOR_BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#VECTOR_BUCKET_NAME) | The name of the vector bucket which will be used for the current operation. |  | String |
| **CamelAwsS3VectorsVectorIndexName** (common) Constant: [`VECTOR_INDEX_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#VECTOR_INDEX_NAME) | The name of the vector index which will be used for the current operation. |  | String |
| **CamelAwsS3VectorsVectorId** (producer) Constant: [`VECTOR_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#VECTOR_ID) | The unique identifier for a vector. |  | String |
| **CamelAwsS3VectorsVectorData** (producer) Constant: [`VECTOR_DATA`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#VECTOR_DATA) | The vector embedding data as a list of floats or float array. |  | List or float\[\] |
| **CamelAwsS3VectorsVectorDimensions** (producer) Constant: [`VECTOR_DIMENSIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#VECTOR_DIMENSIONS) | The dimensions of the vector. |  | Integer |
| **CamelAwsS3VectorsDataType** (producer) Constant: [`DATA_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#DATA_TYPE) | The data type of the vector (float32 or float16). |  | String |
| **CamelAwsS3VectorsVectorMetadata** (producer) Constant: [`VECTOR_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#VECTOR_METADATA) | Additional metadata for the vector as a map. |  | Map |
| **CamelAwsS3VectorsQueryVector** (producer) Constant: [`QUERY_VECTOR`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#QUERY_VECTOR) | The query vector for similarity search as a list of floats or float array. |  | List or float\[\] |
| **CamelAwsS3VectorsTopK** (producer) Constant: [`TOP_K`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#TOP_K) | The number of top similar vectors to return. |  | Integer |
| **CamelAwsS3VectorsDistanceMetric** (producer) Constant: [`DISTANCE_METRIC`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#DISTANCE_METRIC) | The distance metric to use for similarity search (cosine, euclidean, dot-product). |  | String |
| **CamelAwsS3VectorsSimilarityThreshold** (producer) Constant: [`SIMILARITY_THRESHOLD`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#SIMILARITY_THRESHOLD) | The minimum similarity threshold for results. |  | Float |
| **CamelAwsS3VectorsMetadataFilter** (producer) Constant: [`METADATA_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#METADATA_FILTER) | Optional filter expression for metadata filtering during vector search. |  | String |
| **CamelAwsS3VectorsSimilarityScore** (consumer) Constant: [`SIMILARITY_SCORE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#SIMILARITY_SCORE) | The similarity score of the returned vector. |  | Float |
| **CamelAwsS3VectorsResultCount** (consumer) Constant: [`RESULT_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#RESULT_COUNT) | The number of vectors returned in the result. |  | Integer |
| **CamelAwsS3VectorsIndexStatus** (consumer) Constant: [`INDEX_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#INDEX_STATUS) | The status of the vector index. |  | String |
| **CamelAwsS3VectorsVectorBucketArn** (consumer) Constant: [`VECTOR_BUCKET_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-s3-vectors/latest/org/apache/camel/component/aws2/s3vectors/AWS2S3VectorsConstants.html#VECTOR_BUCKET_ARN) | The ARN of the vector bucket. |  | String |

## Usage

### Producer Operations

-   `putVectors` - Insert vectors
    
-   `queryVectors` - Search similar vectors
    
-   `deleteVectors` - Delete vectors
    
-   `getVectors` - Retrieve vectors by ID
    
-   `createVectorBucket` - Create bucket
    
-   `deleteVectorBucket` - Delete bucket
    
-   `listVectorBuckets` - List buckets
    
-   `describeVectorBucket` - Get bucket info
    
-   `createVectorIndex` - Create index
    
-   `deleteVectorIndex` - Delete index
    
-   `listVectorIndexes` - List indexes
    
-   `describeVectorIndex` - Get index info
    

### Consumer

The consumer polls for vectors using similarity search. It tracks processed vector IDs to avoid duplicates.

## Examples

### Insert Vectors

-   Java
    
-   YAML
    

```java
from("direct:insert")
    .setHeader(AWS2S3VectorsConstants.VECTOR_ID, constant("doc-001"))
    .setBody(constant(Arrays.asList(0.1f, 0.2f, 0.3f)))
    .to("aws2-s3-vectors://my-bucket?operation=putVectors&vectorIndexName=my-index");
```

```yaml
- route:
    from:
      uri: direct:insert
      steps:
        - setHeader:
            name: CamelAwsS3VectorsVectorId
            constant: doc-001
        - setBody:
            constant:
              - 0.1
              - 0.2
              - 0.3
        - to:
            uri: aws2-s3-vectors://my-bucket
            parameters:
              operation: putVectors
              vectorIndexName: my-index
```

### Query Similar Vectors

-   Java
    
-   YAML
    

```java
from("direct:search")
    .setBody(constant(Arrays.asList(0.15f, 0.25f, 0.35f)))
    .setHeader(AWS2S3VectorsConstants.TOP_K, constant(5))
    .to("aws2-s3-vectors://my-bucket?operation=queryVectors&vectorIndexName=my-index")
    .log("Found ${body.size} similar vectors");
```

```yaml
- route:
    from:
      uri: direct:search
      steps:
        - setBody:
            constant:
              - 0.15
              - 0.25
              - 0.35
        - setHeader:
            name: CamelAwsS3VectorsTopK
            constant: 5
        - to:
            uri: aws2-s3-vectors://my-bucket
            parameters:
              operation: queryVectors
              vectorIndexName: my-index
        - log:
            message: "Found ${body.size} similar vectors"
```

### Consumer Polling

-   Java
    
-   YAML
    

```java
from("aws2-s3-vectors://my-bucket?"
    + "vectorIndexName=my-index"
    + "&consumerQueryVector=0.1,0.2,0.3"
    + "&delay=5000"
    + "&maxMessagesPerPoll=10")
    .log("Vector ID: ${header.CamelAwsS3VectorsVectorId}")
    .to("direct:process");
```

```yaml
- route:
    from:
      uri: aws2-s3-vectors://my-bucket
      parameters:
        vectorIndexName: my-index
        consumerQueryVector: "0.1,0.2,0.3"
        delay: 5000
        maxMessagesPerPoll: 10
      steps:
        - log:
            message: "Vector ID: ${header.CamelAwsS3VectorsVectorId}"
        - to:
            uri: direct:process
```

### Create Index

-   Java
    
-   YAML
    

```java
from("direct:createIndex")
    .setHeader(AWS2S3VectorsConstants.VECTOR_DIMENSIONS, constant(1536))
    .setHeader(AWS2S3VectorsConstants.DATA_TYPE, constant("float32"))
    .setHeader(AWS2S3VectorsConstants.DISTANCE_METRIC, constant("cosine"))
    .to("aws2-s3-vectors://my-bucket?operation=createVectorIndex&vectorIndexName=my-index");
```

```yaml
- route:
    from:
      uri: direct:createIndex
      steps:
        - setHeader:
            name: CamelAwsS3VectorsVectorDimensions
            constant: 1536
        - setHeader:
            name: CamelAwsS3VectorsDataType
            constant: float32
        - setHeader:
            name: CamelAwsS3VectorsDistanceMetric
            constant: cosine
        - to:
            uri: aws2-s3-vectors://my-bucket
            parameters:
              operation: createVectorIndex
              vectorIndexName: my-index
```

## Dependencies

Maven users will need to add the following dependency to their `pom.xml`.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-s3-vectors</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

where `x.x.x` is the version number of the latest Camel release.

## Spring Boot Auto-Configuration

When using aws2-s3-vectors with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-s3-vectors-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 34 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-s3-vectors.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-s3-vectors.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-s3-vectors.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws2-s3-vectors.configuration** | The component configuration. The option is a org.apache.camel.component.aws2.s3vectors.AWS2S3VectorsConfiguration type. |  | AWS2S3VectorsConfiguration |
| **camel.component.aws2-s3-vectors.consumer-metadata-filter** | Optional metadata filter for the consumer to filter vectors during polling. |  | String |
| **camel.component.aws2-s3-vectors.consumer-query-vector** | The query vector to use for the consumer to poll for similar vectors. Specified as comma-separated float values (e.g., 0.1,0.2,0.3). If not specified, the consumer will not poll. |  | String |
| **camel.component.aws2-s3-vectors.data-type** | The data type of the vector. Options: float32, float16. | float32 | String |
| **camel.component.aws2-s3-vectors.delay** | Milliseconds before the next poll for the consumer. | 500 | Long |
| **camel.component.aws2-s3-vectors.delete-after-read** | Delete vectors after they have been consumed. | false | Boolean |
| **camel.component.aws2-s3-vectors.distance-metric** | The distance metric to use for similarity search. Options: cosine, euclidean, dot-product. | cosine | String |
| **camel.component.aws2-s3-vectors.enabled** | Whether to enable auto configuration of the aws2-s3-vectors component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-s3-vectors.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws2-s3-vectors.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws2-s3-vectors.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-s3-vectors.max-messages-per-poll** | The maximum number of messages to consume per poll for the consumer. | 10 | Integer |
| **camel.component.aws2-s3-vectors.operation** | The operation to perform. |  | AWS2S3VectorsOperations |
| **camel.component.aws2-s3-vectors.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-s3-vectors.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **camel.component.aws2-s3-vectors.proxy-host** | To define a proxy host when instantiating the S3 Vectors client. |  | String |
| **camel.component.aws2-s3-vectors.proxy-port** | To define a proxy port when instantiating the S3 Vectors client. |  | Integer |
| **camel.component.aws2-s3-vectors.proxy-protocol** | To define a proxy protocol when instantiating the S3 Vectors client. | https | Protocol |
| **camel.component.aws2-s3-vectors.region** | The region in which S3 Vectors client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1). |  | String |
| **camel.component.aws2-s3-vectors.s3-vectors-client** | Reference to a software.amazon.awssdk.services.s3vectors.S3VectorsClient in the registry. The option is a software.amazon.awssdk.services.s3vectors.S3VectorsClient type. |  | S3VectorsClient |
| **camel.component.aws2-s3-vectors.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-s3-vectors.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws2-s3-vectors.similarity-threshold** | The minimum similarity threshold for results. |  | Float |
| **camel.component.aws2-s3-vectors.top-k** | The number of top similar vectors to return in a query. | 10 | Integer |
| **camel.component.aws2-s3-vectors.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-s3-vectors.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-s3-vectors.use-default-credentials-provider** | Set whether the S3 Vectors client should expect to load credentials through a default credentials provider. | false | Boolean |
| **camel.component.aws2-s3-vectors.use-profile-credentials-provider** | Set whether the S3 Vectors client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-s3-vectors.use-session-credentials** | Set whether the S3 Vectors client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in S3 Vectors. | false | Boolean |
| **camel.component.aws2-s3-vectors.vector-dimensions** | The dimensions of the vector embeddings (default: 1536, which is the dimension for OpenAI text-embedding-3-small). | 1536 | Integer |
| **camel.component.aws2-s3-vectors.vector-index-name** | The name of the vector index. |  | String |