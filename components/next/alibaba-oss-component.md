# Alibaba Object Storage Service (OSS)

**Since Camel 4.23**

**Both producer and consumer are supported**

The Alibaba Cloud Object Storage Service (OSS) component allows you to integrate with [Alibaba Cloud OSS](https://www.alibabacloud.com/product/object-storage-service).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-alibaba-oss</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

alibaba-oss:bucketName\[?options\]

The `operation` query parameter selects the OSS operation to perform (for example `putObject`, `getObject`, `listObjects`).

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

The Alibaba Object Storage Service (OSS) component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Alibaba Object Storage Service (OSS) endpoint is configured using URI syntax:

alibaba-oss:bucketName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bucketName** (common) | Name of bucket to perform operation on. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpoint** (common) | OSS endpoint URL. Carries higher precedence than region based client initialization. |  | String |
| **objectName** (common) | Name of object to perform operation with. |  | String |
| **region** (common) | **Required** OSS service region. |  | String |
| **deleteAfterRead** (consumer) | Determines if objects should be deleted after they have been retrieved. | false | boolean |
| **maxMessagesPerPoll** (consumer) | The maximum number of messages to poll at each polling. | 10 | int |
| **prefix** (consumer) | The object name prefix used for filtering objects to be listed. |  | String |
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
| **maxKeys** (producer) | The maximum number of keys returned when listing objects. |  | Integer |
| **operation** (producer) | 

Operation to be performed.

Enum values:

-   listBuckets
    
-   listObjects
    
-   putObject
    
-   getObject
    
-   deleteObject
    
-   copyObject
    
-   headObject
    





 |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **ossClient** (advanced) | **Autowired** An autowired OSS client. |  | OSSClient |
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
| **accessKey** (security) | **Required** Access key for the cloud user. |  | String |
| **secretKey** (security) | **Required** Secret key for the cloud user. |  | String |
| **serviceKeys** (security) | Configuration object for cloud service authentication. |  | ServiceKeys |

## Message Headers

The Alibaba Object Storage Service (OSS) component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAlibabaOssBucketName** (consumer) Constant: [`BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-oss/latest/org/apache/camel/component/alibaba/oss/constants/OSSHeaders.html#BUCKET_NAME) | Name of the bucket where object is contained. |  | String |
| **CamelAlibabaOssObjectKey** (consumer) Constant: [`OBJECT_KEY`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-oss/latest/org/apache/camel/component/alibaba/oss/constants/OSSHeaders.html#OBJECT_KEY) | The key that the object is stored under. |  | String |
| **CamelAlibabaOssLastModified** (consumer) Constant: [`LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-oss/latest/org/apache/camel/component/alibaba/oss/constants/OSSHeaders.html#LAST_MODIFIED) | The date and time that the object was last modified. |  | String |
| **CamelAlibabaOssETag** (consumer) Constant: [`ETAG`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-oss/latest/org/apache/camel/component/alibaba/oss/constants/OSSHeaders.html#ETAG) | The 128-bit MD5 digest of the object content. |  | String |
| **CamelAlibabaOssContentMD5** (consumer) Constant: [`CONTENT_MD5`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-oss/latest/org/apache/camel/component/alibaba/oss/constants/OSSHeaders.html#CONTENT_MD5) | The 128-bit Base64-encoded digest of the object. |  | String |
| **CamelAlibabaOssObjectType** (consumer) Constant: [`OBJECT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-oss/latest/org/apache/camel/component/alibaba/oss/constants/OSSHeaders.html#OBJECT_TYPE) | Shows whether the object is a file or a folder. |  | String |
| **CamelAlibabaOssContentLength** (consumer) Constant: [`CONTENT_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-oss/latest/org/apache/camel/component/alibaba/oss/constants/OSSHeaders.html#CONTENT_LENGTH) | The size of the object body in bytes. |  | Long |
| **CamelAlibabaOssContentType** (consumer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-oss/latest/org/apache/camel/component/alibaba/oss/constants/OSSHeaders.html#CONTENT_TYPE) | The type of content stored in the object. |  | String |
| **CamelFileName** (consumer) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-alibaba-oss/latest/org/apache/camel/component/alibaba/oss/constants/OSSHeaders.html#FILE_NAME) | Name of the object with which the operation is to be performed. |  | String |

## Usage

### Message headers evaluated by the OSS producer

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelAlibabaOssOperation` | `String` | Name of operation to invoke |
| `CamelAlibabaOssBucketName` | `String` | Bucket name to invoke operation on (overrides the URI path bucket name) |
| `CamelAlibabaOssObjectName` | `String` | Name of the object to be used in operation |
| `CamelAlibabaOssSourceBucketName` | `String` | Source bucket name for copy operations |
| `CamelAlibabaOssSourceObjectName` | `String` | Source object name for copy operations |
| `CamelAlibabaOssPrefix` | `String` | Prefix filter when listing objects |
| `CamelAlibabaOssMaxKeys` | `Integer` | Maximum number of keys returned when listing objects |

If any of the above headers are set, they will override their corresponding query parameter or URI path value.

### List of Supported OSS Operations

-   listBuckets
    
-   listObjects - `bucketName` parameter is **required**
    
-   putObject - `bucketName` and `objectName` parameters are **required** (unless uploading a `File`)
    
-   getObject - `bucketName` and `objectName` parameters are **required**
    
-   deleteObject - `bucketName` and `objectName` parameters are **required**
    
-   copyObject - source and destination bucket/object names are **required**
    
-   headObject - `bucketName` and `objectName` parameters are **required**
    

### Consumer

The consumer polls objects from a bucket using `listObjectsV2`, downloads each object body, and optionally deletes objects after they have been processed when `deleteAfterRead` is enabled.

## Examples

### Put an object

```java
from("direct:start")
  .setBody(constant("Hello OSS"))
  .setHeader("CamelAlibabaOssObjectName", constant("hello.txt"))
  .to("alibaba-oss:my-bucket?operation=putObject&region=cn-hangzhou&accessKey=xxx&secretKey=yyy");
```

Producer operations return structured response metadata in the message body (`Map` or `List<Map>` depending on the operation).

### Consume objects from a bucket

```java
from("alibaba-oss:my-bucket?region=cn-hangzhou&accessKey=xxx&secretKey=yyy&deleteAfterRead=true")
  .to("log:output");
```