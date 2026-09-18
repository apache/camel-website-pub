# RSS

**Since Camel 2.0**

**Only consumer is supported**

The RSS component is used for polling RSS feeds. By default, Camel will poll the feed every 60th second.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-rss</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

> **Note**
> The component currently only supports consuming feeds.

## URI format

rss:rssUri

Where `rssUri` is the URI to the RSS feed to poll.

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

The RSS component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The RSS endpoint is configured using URI syntax:

rss:feedUri

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **feedUri** (consumer) | **Required** The URI to the feed to poll. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **sortEntries** (consumer) | Sets whether to sort entries by published date. Only works when splitEntries = true. | false | boolean |
| **splitEntries** (consumer) | Sets whether or not entries should be sent individually or whether the entire feed should be sent as a single message. | true | boolean |
| **throttleEntries** (consumer) | Sets whether all entries identified in a single feed poll should be delivered immediately. If true, only one entry is processed per delay. Only applicable when splitEntries = true. | true | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **feedHeader** (advanced) | Sets whether to add the feed object as a header. | true | boolean |
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

## Message Headers

The RSS component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelRssFeed** (consumer) Constant: [`RSS_FEED`](https://javadoc.io/doc/org.apache.camel/camel-rss/latest/org/apache/camel/component/rss/RssConstants.html#RSS_FEED) | The entire SyncFeed object. |  | Object |

## Usage

### Exchange data types

Camel initializes the In body on the Exchange with a ROME `SyndFeed`. Depending on the value of the `splitEntries` flag, Camel returns either a `SyndFeed` with one `SyndEntry` or a `java.util.List` of `SyndEntrys`.

  
| Option | Value | Behavior |
| --- | --- | --- |
| `splitEntries` | `true` | A single entry from the current feed is set in the exchange. |
| `splitEntries` | `false` | The entire list of entries from the current feed is set in the exchange. |

## Example

If the URL for the RSS feed uses query parameters, this component will resolve them. For example, if the feed uses `alt=rss`, then the following example will be resolved:

-   Java
    
-   XML
    
-   YAML
    

```java
from("rss:http://someserver.com/feeds/posts/default?alt=rss&splitEntries=false&delay=1000")
    .to("bean:rss");
```

```xml
<route>
  <from uri="rss:http://someserver.com/feeds/posts/default?alt=rss&amp;splitEntries=false&amp;delay=1000"/>
  <to uri="bean:rss"/>
</route>
```

```yaml
- route:
    from:
      uri: "rss:http://someserver.com/feeds/posts/default?alt=rss"
      parameters:
        splitEntries: false
        delay: 1000
      steps:
        - to:
            uri: bean:rss
```

### Filtering entries

You can filter out entries using XPath, as shown in the data format section above. You can also exploit Camel’s Bean Integration to implement your own conditions. For instance, a filter equivalent to the XPath example above would be:

-   Java
    
-   XML
    
-   YAML
    

```java
from("rss:file:src/test/data/rss20.xml?splitEntries=true&delay=100")
    .filter().method("myFilterBean", "titleContainsCamel")
        .to("mock:result");
```

```xml
<route>
  <from uri="rss:file:src/test/data/rss20.xml?splitEntries=true&amp;delay=100"/>
  <filter>
    <method ref="myFilterBean" method="titleContainsCamel"/>
    <to uri="mock:result"/>
  </filter>
</route>
```

```yaml
- route:
    from:
      uri: rss:file:src/test/data/rss20.xml
      parameters:
        splitEntries: true
        delay: 100
      steps:
        - filter:
            method:
              ref: myFilterBean
              method: titleContainsCamel
            steps:
              - to:
                  uri: mock:result
```

The custom bean for this would be:

_Java-only: bean class definition with annotations and type casts_

```java
public static class FilterBean {

    public boolean titleContainsCamel(@Body SyndFeed feed) {
        SyndEntry firstEntry = (SyndEntry) feed.getEntries().get(0);
        return firstEntry.getTitle().contains("Camel");
    }
}
```

## Proxy Support in Camel RSS Component

The Camel RSS component does not natively support proxy configuration. However, you can work around this limitation by using the Camel HTTP component with a proxy and then processing the raw RSS feed using RSS dataformat.

Alternative Approach: Using the HTTP Component with Proxy Instead of directly using `from("rss:…​")`, you can configure an HTTP client with proxy settings and fetch the RSS feed via the HTTP component. Then, zhe RSS dataformat can be used to parse the raw response into a structured RSS feed.

### Configuring Proxy for HTTP Component and Processing RSS

Below is an example that sets up an HTTP client with a proxy (including authentication support) and uses it to retrieve and process an RSS feed:

_Java-only: programmatic proxy configuration with HttpClientConfigurer, registry binding, and RouteBuilder class_

```java
protected RoutesBuilder createRouteBuilder() throws Exception {
    String proxyHost = "myProxyHost";
    Integer proxyPort = 8888;
    String proxyUserName = "username";
    String proxyPassword = "password";

    context().getRegistry().bind("myHttpClientConfigurer", new HttpClientConfigurer() {
        @Override
        public void configureHttpClient(HttpClientBuilder clientBuilder) {
            var routePlanner = new DefaultProxyRoutePlanner(new HttpHost(proxyHost, proxyPort)) {
                @Override
                protected HttpHost determineProxy(HttpHost host, HttpContext context) throws HttpException {
                    // Custom logic for filtering specific hosts
                    return super.determineProxy(host, context);
                }
            };
            clientBuilder.setRoutePlanner(routePlanner);
            clientBuilder.setProxyAuthenticationStrategy(new DefaultAuthenticationStrategy());

            var credentials = new UsernamePasswordCredentials(
                    proxyUserName,
                    proxyPassword.toCharArray()
            );

            var credentialsProvider = new BasicCredentialsProvider();
            credentialsProvider.setCredentials(
                    new AuthScope(proxyHost, proxyPort),
                    credentials
            );
            clientBuilder.setDefaultCredentialsProvider(credentialsProvider);
        }
    });

    from("timer://mytimer?fixedRate=false&period=60&synchronous=true")
        .to("http://feeds.aps.org/rss/recent/prstper.xml?httpClientConfigurer=myHttpClientConfigurer")
        .unmarshal(new RssDataFormat())
        .to("mock:result");
}
```