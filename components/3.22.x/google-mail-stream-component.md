# Google Mail Stream

**Since Camel 2.22**

**Only consumer is supported**

The Google Mail component provides access to [Gmail](http://gmail.com/) via the [Google Mail Web APIs](https://developers.google.com/gmail/api/v1/reference/). This component provides the streaming feature for Messages.

Google Mail uses the [OAuth 2.0 protocol](https://developers.google.com/accounts/docs/OAuth2) for authenticating a Google account and authorizing access to user data. Before you can use this component, you will need to [create an account and generate OAuth credentials](https://developers.google.com/gmail/api/auth/web-server). Credentials comprise of a clientId, clientSecret, and a refreshToken. A handy resource for generating a long-lived refreshToken is the [OAuth playground](https://developers.google.com/oauthplayground).

In the case of a [service account](https://developers.google.com/identity/protocols/oauth2#serviceaccount), credentials comprise of a JSON-file (serviceAccountKey). You can also use [delegation domain-wide authority](https://developers.google.com/identity/protocols/oauth2/service-account#delegatingauthority) (delegate) and one, several, or all possible [GMail API Auth Scopes](https://developers.google.com/gmail/api/auth/scopes) (scopes).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-mail</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.y.z</version>
</dependency>
```

## URI Format

The GoogleMail Component uses the following URI format:

google-mail-stream://index?\[options\]

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

The Google Mail Stream component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (consumer) | Google mail application name. Example would be camel-google-mail/1.0. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **clientId** (consumer) | Client ID of the mail application. |  | String |
| **delegate** (consumer) | Delegate for wide-domain service account. |  | String |
| **labels** (consumer) | Comma separated list of labels to take into account. |  | String |
| **markAsRead** (consumer) | Mark the message as read once it has been consumed. | true | boolean |
| **maxResults** (consumer) | Max results to be returned. | 10 | long |
| **query** (consumer) | The query to execute on gmail box. | is:unread | String |
| **scopes** (consumer) | GMail scopes. |  | List |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientFactory** (advanced) | The client Factory. |  | GoogleMailClientFactory |
| **configuration** (advanced) | The configuration. |  | GoogleMailStreamConfiguration |
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the mail application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Sets .json file with credentials for Service account. |  | String |

## Endpoint Options

The Google Mail Stream endpoint is configured using URI syntax:

google-mail-stream:index

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **index** (consumer) | **Required** Currently not in use. |  | String |

### Query Parameters (31 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (consumer) | Google mail application name. Example would be camel-google-mail/1.0. |  | String |
| **clientId** (consumer) | Client ID of the mail application. |  | String |
| **delegate** (consumer) | Delegate for wide-domain service account. |  | String |
| **labels** (consumer) | Comma separated list of labels to take into account. |  | String |
| **markAsRead** (consumer) | Mark the message as read once it has been consumed. | true | boolean |
| **maxResults** (consumer) | Max results to be returned. | 10 | long |
| **query** (consumer) | The query to execute on gmail box. | is:unread | String |
| **scopes** (consumer) | GMail scopes. |  | List |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
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
| **clientSecret** (security) | Client secret of the mail application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Sets .json file with credentials for Service account. |  | String |

## Message Headers

The Google Mail Stream component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleMailStreamTo** (consumer) Constant: [`MAIL_TO`](https://javadoc.io/doc/org.apache.camel/camel-google-mail/latest/org/apache/camel/component/google/mail/stream/GoogleMailStreamConstants.html#MAIL_TO) | The recipient of the message. |  | String |
| **CamelGoogleMailStreamFrom** (consumer) Constant: [`MAIL_FROM`](https://javadoc.io/doc/org.apache.camel/camel-google-mail/latest/org/apache/camel/component/google/mail/stream/GoogleMailStreamConstants.html#MAIL_FROM) | The emitter of the message. |  | String |
| **CamelGoogleMailStreamCc** (consumer) Constant: [`MAIL_CC`](https://javadoc.io/doc/org.apache.camel/camel-google-mail/latest/org/apache/camel/component/google/mail/stream/GoogleMailStreamConstants.html#MAIL_CC) | The carbon copy of the message. |  | String |
| **CamelGoogleMailStreamBcc** (consumer) Constant: [`MAIL_BCC`](https://javadoc.io/doc/org.apache.camel/camel-google-mail/latest/org/apache/camel/component/google/mail/stream/GoogleMailStreamConstants.html#MAIL_BCC) | The blind carbon cpoy of the message. |  | String |
| **CamelGoogleMailStreamSubject** (consumer) Constant: [`MAIL_SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-google-mail/latest/org/apache/camel/component/google/mail/stream/GoogleMailStreamConstants.html#MAIL_SUBJECT) | The subject of the message. |  | String |
| **CamelGoogleMailId** (consumer) Constant: [`MAIL_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-mail/latest/org/apache/camel/component/google/mail/stream/GoogleMailStreamConstants.html#MAIL_ID) | The ID of the message. |  | String |

## Spring Boot Auto-Configuration

When using google-mail-stream with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-mail-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 31 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-mail-stream.access-token** | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **camel.component.google-mail-stream.application-name** | Google mail application name. Example would be camel-google-mail/1.0. |  | String |
| **camel.component.google-mail-stream.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-mail-stream.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-mail-stream.client-factory** | The client Factory. The option is a org.apache.camel.component.google.mail.GoogleMailClientFactory type. |  | GoogleMailClientFactory |
| **camel.component.google-mail-stream.client-id** | Client ID of the mail application. |  | String |
| **camel.component.google-mail-stream.client-secret** | Client secret of the mail application. |  | String |
| **camel.component.google-mail-stream.configuration** | The configuration. The option is a org.apache.camel.component.google.mail.stream.GoogleMailStreamConfiguration type. |  | GoogleMailStreamConfiguration |
| **camel.component.google-mail-stream.delegate** | Delegate for wide-domain service account. |  | String |
| **camel.component.google-mail-stream.enabled** | Whether to enable auto configuration of the google-mail-stream component. This is enabled by default. |  | Boolean |
| **camel.component.google-mail-stream.labels** | Comma separated list of labels to take into account. |  | String |
| **camel.component.google-mail-stream.mark-as-read** | Mark the message as read once it has been consumed. | true | Boolean |
| **camel.component.google-mail-stream.max-results** | Max results to be returned. | 10 | Long |
| **camel.component.google-mail-stream.query** | The query to execute on gmail box. | is:unread | String |
| **camel.component.google-mail-stream.refresh-token** | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **camel.component.google-mail-stream.scopes** | GMail scopes. |  | List |
| **camel.component.google-mail-stream.service-account-key** | Sets .json file with credentials for Service account. |  | String |
| **camel.component.google-mail.access-token** | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **camel.component.google-mail.application-name** | Google mail application name. Example would be camel-google-mail/1.0. |  | String |
| **camel.component.google-mail.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-mail.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-mail.client-factory** | To use the GoogleCalendarClientFactory as factory for creating the client. Will by default use BatchGoogleMailClientFactory. The option is a org.apache.camel.component.google.mail.GoogleMailClientFactory type. |  | GoogleMailClientFactory |
| **camel.component.google-mail.client-id** | Client ID of the mail application. |  | String |
| **camel.component.google-mail.client-secret** | Client secret of the mail application. |  | String |
| **camel.component.google-mail.configuration** | To use the shared configuration. The option is a org.apache.camel.component.google.mail.GoogleMailConfiguration type. |  | GoogleMailConfiguration |
| **camel.component.google-mail.delegate** | Delegate for wide-domain service account. |  | String |
| **camel.component.google-mail.enabled** | Whether to enable auto configuration of the google-mail component. This is enabled by default. |  | Boolean |
| **camel.component.google-mail.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-mail.refresh-token** | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **camel.component.google-mail.scopes** | GMail scopes. |  | Collection |
| **camel.component.google-mail.service-account-key** | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |