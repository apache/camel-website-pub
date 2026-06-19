# Weather

**Since Camel 2.12**

**Both producer and consumer are supported**

The Weather component is used for polling weather information from [Open Weather Map](http://openweathermap.org) - a site that provides free global weather and forecast information. The information is returned as a json String object.

Camel will poll for updates to the current weather and forecasts once per hour by default. It can also be used to query the weather api based on the parameters defined on the endpoint which is used as producer.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-weather</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

weather://<unused name>\[?options\]

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

The Weather component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Weather endpoint is configured using URI syntax:

weather:name

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** The name value is not used. |  | String |

### Query Parameters (40 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **appid** (common) | **Required** APPID ID used to authenticate the user connected to the API Server. |  | String |
| **headerName** (common) | To store the weather result in this header instead of the message body. This is useable if you want to keep current message body as-is. |  | String |
| **language** (common) | 
Language of the response.

Enum values:

-   en
    
-   ru
    
-   it
    
-   es
    
-   sp
    
-   uk
    
-   ua
    
-   de
    
-   pt
    
-   ro
    
-   pl
    
-   fi
    
-   nl
    
-   fr
    
-   bg
    
-   sv
    
-   se
    
-   zh\_tw
    
-   zh
    
-   zh\_cn
    
-   tr
    
-   hr
    
-   ca
    





 | en | WeatherLanguage |
| **mode** (common) | 

The output format of the weather data.

Enum values:

-   HTML
    
-   JSON
    
-   XML
    





 | JSON | WeatherMode |
| **period** (common) | If null, the current weather will be returned, else use values of 5, 7, 14 days. Only the numeric value for the forecast period is actually parsed, so spelling, capitalisation of the time period is up to you (its ignored). |  | String |
| **units** (common) | 

The units for temperature measurement.

Enum values:

-   IMPERIAL
    
-   METRIC
    





 |  | WeatherUnits |
| **weatherApi** (common) | 

The API to use (current, forecast/3 hour, forecast daily, station).

Enum values:

-   Current
    
-   Station
    
-   Hourly
    
-   Daily
    





 |  | WeatherApi |
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
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **geoLocationProvider** (advanced) | A custum geolocation provider to determine the longitude and latitude to use when no location information is set. The default implementaion uses the ipstack API and requires geolocationAccessKey and geolocationRequestHostIP. |  | GeoLocationProvider |
| **httpClient** (advanced) | To use an existing configured http client (for example with http proxy). |  | CloseableHttpClient |
| **cnt** (filter) | Number of results to be found. |  | Integer |
| **ids** (filter) | List of id’s of city/stations. You can separate multiple ids by comma. |  | String |
| **lat** (filter) | Latitude of location. You can use lat and lon options instead of location. For boxed queries this is the bottom latitude. |  | String |
| **location** (filter) | If null Camel will try and determine your current location using the geolocation of your ip address, else specify the city,country. For well known city names, Open Weather Map will determine the best fit, but multiple results may be returned. Hence specifying and country as well will return more accurate data. If you specify current as the location then the component will try to get the current latitude and longitude and use that to get the weather details. You can use lat and lon options instead of location. |  | String |
| **lon** (filter) | Longitude of location. You can use lat and lon options instead of location. For boxed queries this is the left longtitude. |  | String |
| **rightLon** (filter) | For boxed queries this is the right longtitude. Needs to be used in combination with topLat and zoom. |  | String |
| **topLat** (filter) | For boxed queries this is the top latitude. Needs to be used in combination with rightLon and zoom. |  | String |
| **zip** (filter) | Zip-code, e.g. 94040,us. |  | String |
| **zoom** (filter) | For boxed queries this is the zoom. Needs to be used in combination with rightLon and topLat. |  | Integer |
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
| **geolocationAccessKey** (security) | **Required** The geolocation service now needs an accessKey to be used. |  | String |
| **geolocationRequestHostIP** (security) | **Required** The geolocation service now needs to specify the IP associated to the accessKey you’re using. |  | String |

## Message Headers

The Weather component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelWeatherLocation** (producer) Constant: [`WEATHER_LOCATION`](https://javadoc.io/doc/org.apache.camel/camel-weather/latest/org/apache/camel/component/weather/WeatherConstants.html#WEATHER_LOCATION) | Used by the producer to override the endpoint location and use the location from this header instead. |  | String |
| **CamelWeatherQuery** (common) Constant: [`WEATHER_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-weather/latest/org/apache/camel/component/weather/WeatherConstants.html#WEATHER_QUERY) | The original query URL sent to the Open Weather Map site. |  | String |

## Usage

### Exchange data format

Camel will deliver the body as a json formatted `java.lang.String` (see the `mode` option above).

## Examples

In this sample we find the 7-day weather forecast for Madrid, Spain:

-   Java
    
-   XML
    
-   YAML
    

```java
from("weather:foo?location=Madrid,Spain&period=7 days&appid=APIKEY&geolocationAccessKey=IPSTACK_ACCESS_KEY&geolocationRequestHostIP=LOCAL_IP")
    .to("jms:queue:weather");
```

```xml
<route>
  <from uri="weather:foo?location=Madrid,Spain&amp;period=7 days&amp;appid=APIKEY&amp;geolocationAccessKey=IPSTACK_ACCESS_KEY&amp;geolocationRequestHostIP=LOCAL_IP"/>
  <to uri="jms:queue:weather"/>
</route>
```

```yaml
- route:
    from:
      uri: weather:foo
      parameters:
        location: "Madrid,Spain"
        period: "7 days"
        appid: APIKEY
        geolocationAccessKey: IPSTACK_ACCESS_KEY
        geolocationRequestHostIP: LOCAL_IP
      steps:
        - to:
            uri: jms:queue:weather
```

To just find the current weather for your current location, you can use this:

-   Java
    
-   XML
    
-   YAML
    

```java
from("weather:foo?appid=APIKEY&geolocationAccessKey=IPSTACK_ACCESS_KEY&geolocationRequestHostIP=LOCAL_IP")
    .to("jms:queue:weather");
```

```xml
<route>
  <from uri="weather:foo?appid=APIKEY&amp;geolocationAccessKey=IPSTACK_ACCESS_KEY&amp;geolocationRequestHostIP=LOCAL_IP"/>
  <to uri="jms:queue:weather"/>
</route>
```

```yaml
- route:
    from:
      uri: weather:foo
      parameters:
        appid: APIKEY
        geolocationAccessKey: IPSTACK_ACCESS_KEY
        geolocationRequestHostIP: LOCAL_IP
      steps:
        - to:
            uri: jms:queue:weather
```

And to find the weather using the producer, we do:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("weather:foo?location=Madrid,Spain&appid=APIKEY&geolocationAccessKey=IPSTACK_ACCESS_KEY&geolocationRequestHostIP=LOCAL_IP");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="weather:foo?location=Madrid,Spain&amp;appid=APIKEY&amp;geolocationAccessKey=IPSTACK_ACCESS_KEY&amp;geolocationRequestHostIP=LOCAL_IP"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: weather:foo
            parameters:
              location: "Madrid,Spain"
              appid: APIKEY
              geolocationAccessKey: IPSTACK_ACCESS_KEY
              geolocationRequestHostIP: LOCAL_IP
```

And we can send in a message with a header to get the weather for any location as shown:

_Java-only: ProducerTemplate API usage_

```java
String json = template.requestBodyAndHeader("direct:start", "", "CamelWeatherLocation", "Paris,France&appid=APIKEY", String.class);
```

And to get the weather at the current location, then:

_Java-only: ProducerTemplate API usage_

```java
String json = template.requestBodyAndHeader("direct:start", "", "CamelWeatherLocation", "current&appid=APIKEY", String.class);
```