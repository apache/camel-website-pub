# Google Calendar Stream

**Since Camel 2.23**

**Only consumer is supported**

The Google Calendar Stream component provides access to [Calendar](https://calendar.google.com) via the [Google Calendar Web APIs](https://developers.google.com/calendar/overview). This component provides the streaming feature for Calendar events.

Google Calendar uses the [OAuth 2.0 protocol](https://developers.google.com/accounts/docs/OAuth2) for authenticating a Google account and authorizing access to user data. Before you can use this component, you will need to [create an account and generate OAuth credentials](https://developers.google.com/calendar/auth). Credentials consist of a `clientId`, `clientSecret`, and a `refreshToken`. A handy resource for generating a long-lived `refreshToken` is the [OAuth playground](https://developers.google.com/oauthplayground).

In the case of a [service account](https://developers.google.com/identity/protocols/oauth2#serviceaccount), credentials consist of a JSON-file (serviceAccountKey). You can also use [delegation domain-wide authority](https://developers.google.com/identity/protocols/oauth2/service-account#delegatingauthority) (delegate) and one, several, or all possible [Calendar API Auth Scopes](https://developers.google.com/calendar/api/guides/auth).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
        <groupId>org.apache.camel</groupId>
        <artifactId>camel-google-calendar</artifactId>
        <!-- use the same version as your Camel core version -->
        <version>x.x.x</version>
</dependency>
```

## URI Format

The Google Calendar Component uses the following URI format:

google-calendar-stream://index?\[options\]

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

The Google Calendar Stream component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (consumer) | Google Calendar application name. Example would be camel-google-calendar/1.0. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **calendarId** (consumer) | The calendarId to be used. | primary | String |
| **clientId** (consumer) | Client ID of the calendar application. |  | String |
| **configuration** (consumer) | The configuration. |  | GoogleCalendarStreamConfiguration |
| **considerLastUpdate** (consumer) | Take into account the lastUpdate of the last event polled as start date for the next poll. | false | boolean |
| **consumeFromNow** (consumer) | Consume events in the selected calendar from now on. | true | boolean |
| **delegate** (consumer) | Delegate for wide-domain service account. |  | String |
| **maxResults** (consumer) | Max results to be returned. | 10 | int |
| **query** (consumer) | The query to execute on calendar. |  | String |
| **scopes** (consumer) | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **syncFlow** (consumer) | Sync events, see [https://developers.google.com/calendar/v3/sync](https://developers.google.com/calendar/v3/sync) Note: not compatible with: 'query' and 'considerLastUpdate' parameters. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientFactory** (advanced) | The client Factory. |  | GoogleCalendarClientFactory |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the calendar application. |  | String |
| **emailAddress** (security) | The emailAddress of the Google Service Account. |  | String |
| **p12FileName** (security) | The name of the p12 file which has the private key to use with the Google Service Account. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |
| **user** (security) | The email address of the user the application is trying to impersonate in the service account flow. |  | String |

## Endpoint Options

The Google Calendar Stream endpoint is configured using URI syntax:

google-calendar-stream:index

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **index** (consumer) | **Required** Specifies an index for the endpoint. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (consumer) | Google Calendar application name. Example would be camel-google-calendar/1.0. |  | String |
| **calendarId** (consumer) | The calendarId to be used. | primary | String |
| **clientId** (consumer) | Client ID of the calendar application. |  | String |
| **considerLastUpdate** (consumer) | Take into account the lastUpdate of the last event polled as start date for the next poll. | false | boolean |
| **consumeFromNow** (consumer) | Consume events in the selected calendar from now on. | true | boolean |
| **delegate** (consumer) | Delegate for wide-domain service account. |  | String |
| **maxResults** (consumer) | Max results to be returned. | 10 | int |
| **query** (consumer) | The query to execute on calendar. |  | String |
| **scopes** (consumer) | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **syncFlow** (consumer) | Sync events, see [https://developers.google.com/calendar/v3/sync](https://developers.google.com/calendar/v3/sync) Note: not compatible with: 'query' and 'considerLastUpdate' parameters. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
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
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the calendar application. |  | String |
| **emailAddress** (security) | The emailAddress of the Google Service Account. |  | String |
| **p12FileName** (security) | The name of the p12 file which has the private key to use with the Google Service Account. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |
| **user** (security) | The email address of the user the application is trying to impersonate in the service account flow. |  | String |

## Message Headers

The Google Calendar Stream component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleCalendarEventId** (consumer) Constant: [`EVENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-calendar/latest/org/apache/camel/component/google/calendar/stream/GoogleCalendarStreamConstants.html#EVENT_ID) | The calendar event id. |  | String |