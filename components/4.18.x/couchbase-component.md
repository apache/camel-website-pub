# Couchbase

**Since Camel 2.19**

**Both producer and consumer are supported**

The **couchbase:** component allows you to treat [Couchbase](https://www.couchbase.com/) instances as a producer or consumer of messages.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-couchbase</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

couchbase:url

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

The Couchbase component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Couchbase endpoint is configured using URI syntax:

couchbase:protocol://hostname:port

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **protocol** (common) | **Required** The protocol to use. |  | String |
| **hostname** (common) | **Required** The hostname to use. |  | String |
| **port** (common) | The port number to use. | 8091 | int |

### Query Parameters (46 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bucket** (common) | **Required** The bucket to use. |  | String |
| **collection** (common) | The collection to use. |  | String |
| **key** (common) | The key to use. |  | String |
| **scope** (common) | The scope to use. |  | String |
| **consumerProcessedStrategy** (consumer) | Define the consumer Processed strategy to use. | none | String |
| **consumerRetryPause** (consumer) | Define the consumer retry pause between different attempts. | 5000 | int |
| **descending** (consumer) | Define if this operation is descending or not. | false | boolean |
| **designDocumentName** (consumer) | The design document name to use. | beer | String |
| **fullDocument** (consumer) | If true consumer will return complete document instead data defined in view. | false | boolean |
| **limit** (consumer) | The output limit to use. | \-1 | int |
| **rangeEndKey** (consumer) | Define a range for the end key. |  | String |
| **rangeStartKey** (consumer) | Define a range for the start key. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **skip** (consumer) | Define the skip to use. | \-1 | int |
| **viewName** (consumer) | The view name to use. | brewery\_beers | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **autoStartIdForInserts** (producer) | Define if we want an autostart Id when we are doing an insert operation. | false | boolean |
| **operation** (producer) | The operation to do. | CCB\_PUT | String |
| **persistTo** (producer) | Where to persist the data. | 0 | int |
| **producerRetryAttempts** (producer) | Define the number of retry attempts. | 2 | int |
| **producerRetryPause** (producer) | Define the producer retry pause between different attempts. | 5000 | int |
| **replicateTo** (producer) | Where to replicate the data. | 0 | int |
| **startingIdForInsertsFrom** (producer) | Define the starting Id where we are doing an insert operation. |  | long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **additionalHosts** (advanced) | The additional hosts. |  | String |
| **connectTimeout** (advanced) | Define the timeoutconnect in milliseconds. | 30000 | long |
| **queryTimeout** (advanced) | Define the operation timeout in milliseconds. | 2500 | long |
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
| **password** (security) | The password to use. |  | String |
| **username** (security) | The username to use. |  | String |

## Message Headers

The Couchbase component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelCouchbaseKey** (consumer) Constant: [`HEADER_KEY`](https://javadoc.io/doc/org.apache.camel/camel-couchbase/latest/org/apache/camel/component/couchbase/CouchbaseConstants.html#HEADER_KEY) | The key. |  | String |
| **CamelCouchbaseId** (common) Constant: [`HEADER_ID`](https://javadoc.io/doc/org.apache.camel/camel-couchbase/latest/org/apache/camel/component/couchbase/CouchbaseConstants.html#HEADER_ID) | The document id. |  | String |
| **CamelCouchbaseTtl** (producer) Constant: [`HEADER_TTL`](https://javadoc.io/doc/org.apache.camel/camel-couchbase/latest/org/apache/camel/component/couchbase/CouchbaseConstants.html#HEADER_TTL) | The expiry for the document in seconds. |  | String |
| **CamelCouchbaseDesignDocumentName** (consumer) Constant: [`HEADER_DESIGN_DOCUMENT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-couchbase/latest/org/apache/camel/component/couchbase/CouchbaseConstants.html#HEADER_DESIGN_DOCUMENT_NAME) | The design document name. |  | String |
| **CamelCouchbaseViewName** (consumer) Constant: [`HEADER_VIEWNAME`](https://javadoc.io/doc/org.apache.camel/camel-couchbase/latest/org/apache/camel/component/couchbase/CouchbaseConstants.html#HEADER_VIEWNAME) | The view name. |  | String |
| **CamelCqlResumeQuery** (consumer) Constant: [`COUCHBASE_RESUME_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-couchbase/latest/org/apache/camel/component/couchbase/CouchbaseConstants.html#COUCHBASE_RESUME_ACTION) | The resume action to execute when resuming. |  | String |

## Couchbase SDK compatibility

Using collections and scopes is supported only for Couchbase Server 7.0 and later.

This component is currently using Java SDK 3.x, so it might be not compatible with older Couchbase servers anymore. Check the compatibility [page](https://docs.couchbase.com/java-sdk/current/project-docs/compatibility.md) for details.

-   The value formerly interpreted as a bucket-name is now interpreted as a username. The username must correspond to a user defined on the cluster that is being accessed.
    
-   The value formerly interpreted as a bucket-password is now interpreted as the password of the defined user.
    

## Spring Boot Auto-Configuration

When using couchbase with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-couchbase-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.couchbase.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.couchbase.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.couchbase.enabled** | Whether to enable auto configuration of the couchbase component. This is enabled by default. |  | Boolean |
| **camel.component.couchbase.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.couchbase.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.couchbase.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |