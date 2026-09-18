# Splunk

**Since Camel 2.13**

**Both producer and consumer are supported**

The Splunk component provides access to [Splunk](http://docs.splunk.com/Documentation/Splunk/latest) using the Splunk provided [client](https://github.com/splunk/splunk-sdk-java) api, and it enables you to publish and search for events in Splunk.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-splunk</artifactId>
    <version>${camel-version}</version>
</dependency>
```

## URI format

splunk://\[endpoint\]?\[options\]

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

The Splunk component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **splunkConfigurationFactory** (advanced) | To use the SplunkConfigurationFactory. |  | SplunkConfigurationFactory |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Splunk endpoint is configured using URI syntax:

splunk:name

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Name has no purpose. |  | String |

### Query Parameters (46 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **app** (common) | Splunk app. |  | String |
| **connectionTimeout** (common) | Timeout in MS when connecting to Splunk server. | 5000 | int |
| **host** (common) | Splunk host. | localhost | String |
| **owner** (common) | Splunk owner. |  | String |
| **port** (common) | Splunk port. | 8089 | int |
| **scheme** (common) | Splunk scheme. | https | String |
| **count** (consumer) | A number that indicates the maximum number of entities to return. |  | int |
| **earliestTime** (consumer) | Earliest time of the search time window. |  | String |
| **initEarliestTime** (consumer) | Initial start offset of the first search. |  | String |
| **latestTime** (consumer) | Latest time of the search time window. |  | String |
| **savedSearch** (consumer) | The name of the query saved in Splunk to run. |  | String |
| **search** (consumer) | The Splunk query to run. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **streaming** (consumer) | Sets streaming mode. Streaming mode sends exchanges as they are received, rather than in a batch. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **eventHost** (producer) | Override the default Splunk event host field. |  | String |
| **index** (producer) | Splunk index to write to. |  | String |
| **raw** (producer) | Should the payload be inserted raw. | false | boolean |
| **source** (producer) | Splunk source argument. |  | String |
| **sourceType** (producer) | Splunk sourcetype argument. |  | String |
| **tcpReceiverLocalPort** (producer) | Splunk tcp receiver port defined locally on splunk server. (For example if splunk port 9997 is mapped to 12345, tcpReceiverLocalPort has to be 9997). |  | Integer |
| **tcpReceiverPort** (producer) | Splunk tcp receiver port. |  | int |
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
| **password** (security) | Password for Splunk. |  | String |
| **sslProtocol** (security) | 

Set the ssl protocol to use.

Enum values:

-   TLSv1.2
    
-   TLSv1.1
    
-   TLSv1
    
-   SSLv3
    





 | TLSv1.2 | SSLSecurityProtocol |
| **token** (security) | User’s token for Splunk. This takes precedence over password when both are set. |  | String |
| **username** (security) | Username for Splunk. |  | String |
| **useSunHttpsHandler** (security) | Use sun.net.www.protocol.https.Handler Https handler to establish the Splunk Connection. Can be useful when running in application servers to avoid app. server https handling. | false | boolean |
| **validateCertificates** (security) | Sets client’s certificate validation mode. Value false makes SSL vulnerable and is not recommended for the production environment. | true | boolean |

## Usage

### Producer Endpoints

 
| Endpoint | Description |
| --- | --- |
| `stream` | Streams data to a named index or the default if not specified. When using stream mode, be aware of that Splunk has some internal buffer (about 1MB or so) before events get to the index. If you need realtime, better use submit or tcp mode. |
| `submit` | submit mode. Uses Splunk rest api to publish events to a named index or the default if not specified. |
| `tcp` | tcp mode. Streams data to a tcp port, and requires an open receiver port in Splunk. |

When publishing events, the message body should contain a SplunkEvent. See comment under message body.

**Example**

```java
      from("direct:start").convertBodyTo(SplunkEvent.class)
          .to("splunk://submit?username=user&password=123&index=myindex&sourceType=someSourceType&source=mySource")...
```

In this example, a converter is required to convert to a SplunkEvent class.

### Consumer Endpoints

 
| Endpoint | Description |
| --- | --- |
| `normal` | Performs normal search and requires a search query in the search option. |
| `realtime` | Performs realtime search on live data and requires a search query in the search option. |
| `savedsearch` | Performs search based on a search query saved in splunk and requires the name of the query in the savedSearch option. |

**Example**

```java
      from("splunk://normal?delay=5000&username=user&password=123&initEarliestTime=-10s&search=search index=myindex sourcetype=someSourcetype")
          .to("direct:search-result");
```

Camel Splunk component creates a route exchange per search result with a SplunkEvent in the body.

### Message body

Splunk operates on data in key/value pairs. The `SplunkEvent` class is a placeholder for such data, and should be in the message body for the producer. Likewise, it will be returned in the body per search result for the consumer.

You can send raw data to Splunk by setting the raw option on the producer endpoint. This is useful for e.g., json/xml and other payloads where Splunk has built in support.

### Use Cases

Search Twitter for tweets with music and publish events to Splunk

```java
      from("twitter://search?type=polling&keywords=music&delay=10&consumerKey=abc&consumerSecret=def&accessToken=hij&accessTokenSecret=xxx")
          .convertBodyTo(SplunkEvent.class)
          .to("splunk://submit?username=foo&password=bar&index=camel-tweets&sourceType=twitter&source=music-tweets");
```

To convert a Tweet to a `SplunkEvent`, you could use a converter like:

```java
@Converter
public class Tweet2SplunkEvent {
    @Converter
    public static SplunkEvent convertTweet(Status status) {
        SplunkEvent data = new SplunkEvent("twitter-message", null);
        //data.addPair("source", status.getSource());
        data.addPair("from_user", status.getUser().getScreenName());
        data.addPair("in_reply_to", status.getInReplyToScreenName());
        data.addPair(SplunkEvent.COMMON_START_TIME, status.getCreatedAt());
        data.addPair(SplunkEvent.COMMON_EVENT_ID, status.getId());
        data.addPair("text", status.getText());
        data.addPair("retweet_count", status.getRetweetCount());
        if (status.getPlace() != null) {
            data.addPair("place_country", status.getPlace().getCountry());
            data.addPair("place_name", status.getPlace().getName());
            data.addPair("place_street", status.getPlace().getStreetAddress());
        }
        if (status.getGeoLocation() != null) {
            data.addPair("geo_latitude", status.getGeoLocation().getLatitude());
            data.addPair("geo_longitude", status.getGeoLocation().getLongitude());
        }
        return data;
    }
}
```

Search Splunk for tweets:

```java
      from("splunk://normal?username=foo&password=bar&initEarliestTime=-2m&search=search index=camel-tweets sourcetype=twitter")
          .log("${body}");
```

### Other comments

Splunk comes with a variety of options for leveraging machine generated data with prebuilt apps for analyzing and displaying this. For example, the jmx app could be used to publish jmx attributes, e.g., route and jvm metrics to Splunk, and display this on a dashboard.

## Spring Boot Auto-Configuration

When using splunk with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-splunk-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.splunk.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.splunk.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.splunk.enabled** | Whether to enable auto configuration of the splunk component. This is enabled by default. |  | Boolean |
| **camel.component.splunk.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.splunk.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.splunk.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.splunk.splunk-configuration-factory** | To use the SplunkConfigurationFactory. The option is a org.apache.camel.component.splunk.SplunkConfigurationFactory type. |  | SplunkConfigurationFactory |