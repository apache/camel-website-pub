# Google Calendar Stream

**Since Camel 2.23**

**Only consumer is supported**

The Google Calendar Stream component provides access to [Calendar](https://calendar.google.com) via the [Google Calendar Web APIs](https://developers.google.com/calendar/overview). This component provides the streaming feature for Calendar events.

Google Calendar uses the [OAuth 2.0 protocol](https://developers.google.com/accounts/docs/OAuth2) for authenticating a Google account and authorizing access to user data. Before you can use this component, you will need to [create an account and generate OAuth credentials](https://developers.google.com/calendar/auth). Credentials comprise of a clientId, clientSecret, and a refreshToken. A handy resource for generating a long-lived refreshToken is the [OAuth playground](https://developers.google.com/oauthplayground).

In the case of a [service account](https://developers.google.com/identity/protocols/oauth2#serviceaccount), credentials comprise of a JSON-file (serviceAccountKey). You can also use [delegation domain-wide authority](https://developers.google.com/identity/protocols/oauth2/service-account#delegatingauthority) (delegate) and one, several, or all possible [Calendar API Auth Scopes](https://developers.google.com/calendar/api/guides/auth) (scopes).

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

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Google Calendar Stream component supports 21 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (consumer) | Google Calendar application name. Example would be camel-google-calendar/1.0. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **calendarId** (consumer) | The calendarId to be used. | primary | String |
| **clientId** (consumer) | Client ID of the calendar application. |  | String |
| **configuration** (consumer) | The configuration. |  | GoogleCalendarStreamConfiguration |
| **considerLastUpdate** (consumer) | Take into account the lastUpdate of the last event polled as start date for the next poll. | false | boolean |
| **consumeFromNow** (consumer) | Consume events in the selected calendar from now on. | true | boolean |
| **delegate** (consumer) | Delegate for wide-domain service account. |  | String |
| **maxResults** (consumer) | Max results to be returned. | 10 | int |
| **query** (consumer) | The query to execute on calendar. |  | String |
| **scopes** (consumer) | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/calendar/auth](https://developers.google.com/calendar/auth) for more info. |  | List |
| **syncFlow** (consumer) | Sync events, see [https://developers.google.com/calendar/v3/sync](https://developers.google.com/calendar/v3/sync) Note: not compatible with: 'query' and 'considerLastUpdate' parameters. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientFactory** (advanced) | The client Factory. |  | GoogleCalendarClientFactory |
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

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **index** (consumer) | **Required** Specifies an index for the endpoint. |  | String |

### Query Parameters (36 parameters)

   
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
| **scopes** (consumer) | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/calendar/auth](https://developers.google.com/calendar/auth) for more info. |  | List |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **syncFlow** (consumer) | Sync events, see [https://developers.google.com/calendar/v3/sync](https://developers.google.com/calendar/v3/sync) Note: not compatible with: 'query' and 'considerLastUpdate' parameters. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





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
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. |  | Map |
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

The Google Calendar Stream component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleCalendarEventId** (consumer) Constant: [`EVENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-calendar/latest/org/apache/camel/component/google/calendar/stream/GoogleCalendarStreamConstants.html#EVENT_ID) | The calendar event id. |  | String |

## Spring Boot Auto-Configuration

When using google-calendar-stream with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-calendar-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 39 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-calendar-stream.access-token** | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **camel.component.google-calendar-stream.application-name** | Google Calendar application name. Example would be camel-google-calendar/1.0. |  | String |
| **camel.component.google-calendar-stream.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-calendar-stream.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-calendar-stream.calendar-id** | The calendarId to be used. | primary | String |
| **camel.component.google-calendar-stream.client-factory** | The client Factory. The option is a org.apache.camel.component.google.calendar.GoogleCalendarClientFactory type. |  | GoogleCalendarClientFactory |
| **camel.component.google-calendar-stream.client-id** | Client ID of the calendar application. |  | String |
| **camel.component.google-calendar-stream.client-secret** | Client secret of the calendar application. |  | String |
| **camel.component.google-calendar-stream.configuration** | The configuration. The option is a org.apache.camel.component.google.calendar.stream.GoogleCalendarStreamConfiguration type. |  | GoogleCalendarStreamConfiguration |
| **camel.component.google-calendar-stream.consider-last-update** | Take into account the lastUpdate of the last event polled as start date for the next poll. | false | Boolean |
| **camel.component.google-calendar-stream.consume-from-now** | Consume events in the selected calendar from now on. | true | Boolean |
| **camel.component.google-calendar-stream.delegate** | Delegate for wide-domain service account. |  | String |
| **camel.component.google-calendar-stream.email-address** | The emailAddress of the Google Service Account. |  | String |
| **camel.component.google-calendar-stream.enabled** | Whether to enable auto configuration of the google-calendar-stream component. This is enabled by default. |  | Boolean |
| **camel.component.google-calendar-stream.max-results** | Max results to be returned. | 10 | Integer |
| **camel.component.google-calendar-stream.p12-file-name** | The name of the p12 file which has the private key to use with the Google Service Account. |  | String |
| **camel.component.google-calendar-stream.query** | The query to execute on calendar. |  | String |
| **camel.component.google-calendar-stream.refresh-token** | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **camel.component.google-calendar-stream.scopes** | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/calendar/auth](https://developers.google.com/calendar/auth) for more info. |  | List |
| **camel.component.google-calendar-stream.service-account-key** | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |
| **camel.component.google-calendar-stream.sync-flow** | Sync events, see [https://developers.google.com/calendar/v3/sync](https://developers.google.com/calendar/v3/sync) Note: not compatible with: 'query' and 'considerLastUpdate' parameters. | false | Boolean |
| **camel.component.google-calendar-stream.user** | The email address of the user the application is trying to impersonate in the service account flow. |  | String |
| **camel.component.google-calendar.access-token** | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **camel.component.google-calendar.application-name** | Google calendar application name. Example would be camel-google-calendar/1.0. |  | String |
| **camel.component.google-calendar.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-calendar.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-calendar.client-factory** | To use the GoogleCalendarClientFactory as factory for creating the client. Will by default use BatchGoogleCalendarClientFactory. The option is a org.apache.camel.component.google.calendar.GoogleCalendarClientFactory type. |  | GoogleCalendarClientFactory |
| **camel.component.google-calendar.client-id** | Client ID of the calendar application. |  | String |
| **camel.component.google-calendar.client-secret** | Client secret of the calendar application. |  | String |
| **camel.component.google-calendar.configuration** | To use the shared configuration. The option is a org.apache.camel.component.google.calendar.GoogleCalendarConfiguration type. |  | GoogleCalendarConfiguration |
| **camel.component.google-calendar.delegate** | Delegate for wide-domain service account. |  | String |
| **camel.component.google-calendar.email-address** | The emailAddress of the Google Service Account. |  | String |
| **camel.component.google-calendar.enabled** | Whether to enable auto configuration of the google-calendar component. This is enabled by default. |  | Boolean |
| **camel.component.google-calendar.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-calendar.p12-file-name** | The name of the p12 file which has the private key to use with the Google Service Account. |  | String |
| **camel.component.google-calendar.refresh-token** | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **camel.component.google-calendar.scopes** | Specifies the level of permissions you want a calendar application to have to a user account. You can separate multiple scopes by comma. See [https://developers.google.com/google-apps/calendar/auth](https://developers.google.com/google-apps/calendar/auth) for more info. |  | List |
| **camel.component.google-calendar.service-account-key** | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |
| **camel.component.google-calendar.user** | The email address of the user the application is trying to impersonate in the service account flow. |  | String |