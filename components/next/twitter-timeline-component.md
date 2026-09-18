# Twitter Timeline

**Since Camel 2.10**

**Both producer and consumer are supported**

The Twitter Timeline component consumes twitter timeline or updates the status of specific user.

The `timelineType` can be one of:

-   `public`
    
-   `home`
    
-   `user`
    
-   `mentions`
    
-   `retweetsofme`
    

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

The Twitter Timeline component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **httpProxyHost** (proxy) | The http proxy host which can be used for the camel-twitter. |  | String |
| **httpProxyPassword** (proxy) | The http proxy password which can be used for the camel-twitter. |  | String |
| **httpProxyPort** (proxy) | The http proxy port which can be used for the camel-twitter. |  | int |
| **httpProxyUser** (proxy) | The http proxy user which can be used for the camel-twitter. |  | String |
| **accessToken** (security) | The access token. |  | String |
| **accessTokenSecret** (security) | The access token secret. |  | String |
| **consumerKey** (security) | The consumer key. |  | String |
| **consumerSecret** (security) | The consumer secret. |  | String |

## Endpoint Options

The Twitter Timeline endpoint is configured using URI syntax:

twitter-timeline:timelineType

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **timelineType** (common) | 
**Required** The timeline type to produce/consume.

Enum values:

-   PUBLIC
    
-   HOME
    
-   USER
    
-   MENTIONS
    
-   LIST
    
-   UNKNOWN
    





 |  | TimelineType |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **list** (common) | The list name when using timelineType=list. |  | String |
| **user** (common) | The username when using timelineType=user. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **type** (consumer) | 
Endpoint type to use.

Enum values:

-   polling
    
-   direct
    





 | polling | EndpointType |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **distanceMetric** (consumer (advanced)) | 

Used by the geography search, to search by radius using the configured metrics. The unit can either be mi for miles, or km for kilometers. You need to configure all the following options: longitude, latitude, radius, and distanceMetric.

Enum values:

-   km
    
-   mi
    





 | km | String |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **extendedMode** (consumer (advanced)) | Used for enabling full text from twitter (eg receive tweets that contains more than 140 characters). | true | boolean |
| **latitude** (consumer (advanced)) | Used by the geography search to search by latitude. You need to configure all the following options: longitude, latitude, radius, and distanceMetric. |  | Double |
| **locations** (consumer (advanced)) | Bounding boxes, created by pairs of lat/lons. Can be used for filter. A pair is defined as lat,lon. And multiple pairs can be separated by semicolon. |  | String |
| **longitude** (consumer (advanced)) | Used by the geography search to search by longitude. You need to configure all the following options: longitude, latitude, radius, and distanceMetric. |  | Double |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **radius** (consumer (advanced)) | Used by the geography search to search by radius. You need to configure all the following options: longitude, latitude, radius, and distanceMetric. |  | Double |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **count** (filter) | Limiting number of results per page. | 5 | Integer |
| **filterOld** (filter) | Filter out old tweets, that has previously been polled. This state is stored in memory only, and based on last tweet id. | true | boolean |
| **lang** (filter) | The lang string ISO\_639-1 which will be used for searching. |  | String |
| **numberOfPages** (filter) | The number of pages result which you want camel-twitter to consume. | 1 | Integer |
| **sinceId** (filter) | The last tweet id which will be used for pulling the tweets. It is useful when the camel route is restarted after a long running. | 1 | long |
| **userIds** (filter) | To filter by user ids for filter. Multiple values can be separated by comma. |  | String |
| **httpProxyHost** (proxy) | The http proxy host which can be used for the camel-twitter. Can also be configured on the TwitterComponent level instead. |  | String |
| **httpProxyPassword** (proxy) | The http proxy password which can be used for the camel-twitter. Can also be configured on the TwitterComponent level instead. |  | String |
| **httpProxyPort** (proxy) | The http proxy port which can be used for the camel-twitter. Can also be configured on the TwitterComponent level instead. |  | Integer |
| **httpProxyUser** (proxy) | The http proxy user which can be used for the camel-twitter. Can also be configured on the TwitterComponent level instead. |  | String |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 30000 | long |
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
| **accessToken** (security) | The access token. Can also be configured on the TwitterComponent level instead. |  | String |
| **accessTokenSecret** (security) | The access secret. Can also be configured on the TwitterComponent level instead. |  | String |
| **consumerKey** (security) | The consumer key. Can also be configured on the TwitterComponent level instead. |  | String |
| **consumerSecret** (security) | The consumer secret. Can also be configured on the TwitterComponent level instead. |  | String |
| **sortById** (sort) | Sorts by id, so the oldest are first, and newest last. | true | boolean |

## Message Headers

The Twitter Timeline component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelTwitterEventType** (common) Constant: [`TWITTER_EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-twitter/latest/org/apache/camel/component/twitter/TwitterConstants.html#TWITTER_EVENT_TYPE) | The type of event. The supported values are the values of the enum org.apache.camel.component.twitter.consumer.TwitterEventType. |  | String |