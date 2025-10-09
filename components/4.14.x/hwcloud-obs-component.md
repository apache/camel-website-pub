# Huawei Object Storage Service (OBS)

**Since Camel 3.12**

**Both producer and consumer are supported**

Huawei Cloud Object Storage Service (OBS) component allows you to integrate with [OBS](https://www.huaweicloud.com/intl/en-us/product/obs.md) provided by Huawei Cloud.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-huaweicloud-obs</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

hwcloud-obs:operation\[?options\]

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

The Huawei Object Storage Service (OBS) component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Huawei Object Storage Service (OBS) endpoint is configured using URI syntax:

hwcloud-obs:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | **Required** Operation to be performed. |  | String |

### Query Parameters (41 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bucketName** (common) | Name of bucket to perform operation on. |  | String |
| **endpoint** (common) | OBS url. Carries higher precedence than region parameter based client initialization. |  | String |
| **objectName** (common) | Name of object to perform operation with. |  | String |
| **region** (common) | **Required** OBS service region. This is lower precedence than endpoint based configuration. |  | String |
| **deleteAfterRead** (consumer) | Determines if objects should be deleted after it has been retrieved. | false | boolean |
| **delimiter** (consumer) | The character used for grouping object names. |  | String |
| **destinationBucket** (consumer) | Name of destination bucket where objects will be moved when moveAfterRead is set to true. |  | String |
| **fileName** (consumer) | Get the object from the bucket with the given file name. |  | String |
| **includeFolders** (consumer) | If true, objects in folders will be consumed. Otherwise, they will be ignored and no Exchanges will be created for them. | true | boolean |
| **maxMessagesPerPoll** (consumer) | The maximum number of messages to poll at each polling. | 10 | int |
| **moveAfterRead** (consumer) | Determines whether objects should be moved to a different bucket after they have been retrieved. The destinationBucket option must also be set for this option to work. | false | boolean |
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
| **bucketLocation** (producer) | Location of bucket when creating a new bucket. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **proxyHost** (proxy) | Proxy server ip/hostname. |  | String |
| **proxyPassword** (proxy) | Proxy authentication password. |  | String |
| **proxyPort** (proxy) | Proxy server port. |  | int |
| **proxyUser** (proxy) | Proxy authentication user. |  | String |
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
| **ignoreSslVerification** (security) | Ignore SSL verification. | false | boolean |
| **secretKey** (security) | **Required** Secret key for the cloud user. |  | String |
| **serviceKeys** (security) | Configuration object for cloud service authentication. |  | ServiceKeys |

## Usage

### Message properties evaluated by the OBS producer

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelHwCloudObsOperation` | `String` | Name of operation to invoke |
| `CamelHwCloudObsBucketName` | `String` | Bucket name to invoke operation on |
| `CamelHwCloudObsBucketLocation` | `String` | Bucket location when creating a new bucket |
| `CamelHwCloudObsObjectName` | `String` | Name of the object to be used in operation. You can also configure the name of the object using this property while performing putObject operation |

If any of the above properties are set, they will override their corresponding query parameter.

### Message properties set by the OBS producer

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelHwCloudObsBucketExists` | `boolean` | Return value when invoking the `checkBucketExists` operation |

## Message Headers

The Huawei Object Storage Service (OBS) component supports 9 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHwCloudObsBucketName** (consumer) Constant: [`BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-huaweicloud-obs/latest/org/apache/camel/component/huaweicloud/obs/constants/OBSHeaders.html#BUCKET_NAME) | Name of the bucket where object is contained. |  | String |
| **CamelHwCloudObsObjectKey** (consumer) Constant: [`OBJECT_KEY`](https://javadoc.io/doc/org.apache.camel/camel-huaweicloud-obs/latest/org/apache/camel/component/huaweicloud/obs/constants/OBSHeaders.html#OBJECT_KEY) | The key that the object is stored under. |  | String |
| **CamelHwCloudObsLastModified** (consumer) Constant: [`LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-huaweicloud-obs/latest/org/apache/camel/component/huaweicloud/obs/constants/OBSHeaders.html#LAST_MODIFIED) | The date and time that the object was last modified. |  | Date |
| **CamelHwCloudObsETag** (consumer) Constant: [`ETAG`](https://javadoc.io/doc/org.apache.camel/camel-huaweicloud-obs/latest/org/apache/camel/component/huaweicloud/obs/constants/OBSHeaders.html#ETAG) | The 128-bit MD5 digest of the Base64 code of the object. This data is the unique identifier of the object content. |  | String |
| **CamelHwCloudObsContentMD5** (consumer) Constant: [`CONTENT_MD5`](https://javadoc.io/doc/org.apache.camel/camel-huaweicloud-obs/latest/org/apache/camel/component/huaweicloud/obs/constants/OBSHeaders.html#CONTENT_MD5) | The 128-bit Base64-encoded digest used to decrypt the object. |  | String |
| **CamelHwCloudObsObjectType** (consumer) Constant: [`OBJECT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-huaweicloud-obs/latest/org/apache/camel/component/huaweicloud/obs/constants/OBSHeaders.html#OBJECT_TYPE) | Shows whether the object is a file or a folder. |  | String |
| **Content-Length** (consumer) Constant: [`CONTENT_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-huaweicloud-obs/latest/org/apache/camel/component/huaweicloud/obs/constants/OBSHeaders.html#CONTENT_LENGTH) | The size of the object body in bytes. |  | Long |
| **Content-Type** (consumer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-huaweicloud-obs/latest/org/apache/camel/component/huaweicloud/obs/constants/OBSHeaders.html#CONTENT_TYPE) | The type of content stored in the object. |  | String |
| **CamelFileName** (consumer) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-huaweicloud-obs/latest/org/apache/camel/component/huaweicloud/obs/constants/OBSHeaders.html#FILE_NAME) | Name of the object with which the operation is to be performed. |  | String |

### List of Supported OBS Operations

-   listBuckets
    
-   createBucket - `bucketName` parameter is **required**, `bucketLocation` parameter is optional
    
-   deleteBucket - `bucketName` parameter is **required**
    
-   checkBucketExists - `bucketName` parameter is **required**
    
-   getBucketMetadata - `bucketName` parameter is **required**
    
-   listObjects - `bucketName` parameter is **required**
    
-   getObject - `bucketName` and `objectName` parameters are **required**
    
-   putObject - `bucketName` parameter is **required**. If exchange body contains File, then file name is used as default object name unless over-ridden via exchange property CamelHwCloudObsObjectName
    

### Passing Options Through Exchange Body

There are many options that can be submitted to the `createBucket` and `listObjects` operations, so they can be passed through the exchange body.

If you would like to configure all the [parameters](https://support.huaweicloud.com/intl/en-us/api-obs/obs_04_0021.md) when creating a bucket, you can pass a [CreateBucketRequest](https://obssdk-intl.obs.ap-southeast-1.myhuaweicloud.com/apidoc/en/java/com/obs/services/model/CreateBucketRequest.md) object or a Json string into the exchange body. If the exchange body is empty, a new bucket will be created using the bucketName and bucketLocation (if provided) passed through the endpoint uri.

```java
from("direct:triggerRoute")
 .setBody(new CreateBucketRequest("Bucket name", "Bucket location"))
 .to("hwcloud-obs:createBucket?region=cn-north-4&accessKey=********&secretKey=********")
```

```java
from("direct:triggerRoute")
 .setBody("{\"bucketName\":\"Bucket name\",\"location\":\"Bucket location\"}")
 .to("hwcloud-obs:createBucket?region=cn-north-4&accessKey=********&secretKey=********")
```

If you would like to configure all the [parameters](https://support.huaweicloud.com/intl/en-us/api-obs/obs_04_0022.md) when listing objects, you can pass a [ListObjectsRequest](https://obssdk-intl.obs.ap-southeast-1.myhuaweicloud.com/apidoc/en/java/com/obs/services/model/ListObjectsRequest.md) object or a Json string into the exchange body. If the exchange body is empty, objects will be listed based on the bucketName passed through the endpoint uri.

```java
from("direct:triggerRoute")
 .setBody(new ListObjectsRequest("Bucket name", 1000))
 .to("hwcloud-obs:listObjects?region=cn-north-4&accessKey=********&secretKey=********")
```

```java
from("direct:triggerRoute")
 .setBody("{\"bucketName\":\"Bucket name\",\"maxKeys\":1000"}")
 .to("hwcloud-obs:listObjects?region=cn-north-4&accessKey=********&secretKey=********")
```

### Using ServiceKey Configuration Bean

Access key and secret keys are required to authenticate against the OBS cloud. You can avoid having them being exposed and scattered over in your endpoint uri by wrapping them inside a bean of class `org.apache.camel.component.huaweicloud.obs.models.ServiceKeys`. Add it to the registry and let Camel look it up by referring the object via endpoint query parameter `serviceKeys`.

Check the following code snippets:

```xml
<bean id="myServiceKeyConfig" class="org.apache.camel.component.huaweicloud.obs.models.ServiceKeys">
   <property name="accessKey" value="your_access_key" />
   <property name="secretKey" value="your_secret_key" />
</bean>
```

```java
from("direct:triggerRoute")
 .setProperty(OBSPropeties.OPERATION, constant("createBucket"))
 .setProperty(OBSPropeties.BUCKET_NAME ,constant("your_bucket_name"))
 .setProperty(OBSPropeties.BUCKET_LOCATION, constant("your_bucket_location"))
 .to("hwcloud-obs:createBucket?region=cn-north-4&serviceKeys=#myServiceKeyConfig")
```

## Spring Boot Auto-Configuration

When using hwcloud-obs with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-huaweicloud-obs-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.hwcloud-obs.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hwcloud-obs.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hwcloud-obs.enabled** | Whether to enable auto configuration of the hwcloud-obs component. This is enabled by default. |  | Boolean |
| **camel.component.hwcloud-obs.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.hwcloud-obs.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.hwcloud-obs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |