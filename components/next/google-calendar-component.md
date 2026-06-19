# Google Calendar

**Since Camel 2.15**

**Both producer and consumer are supported**

The Google Calendar component provides access to [Google Calendar](http://google.com/calendar) via the [Google Calendar Web APIs](https://developers.google.com/google-apps/calendar/v3/reference/).

Google Calendar uses the [OAuth 2.0 protocol](https://developers.google.com/accounts/docs/OAuth2) for authenticating a Google account and authorizing access to user data. Before you can use this component, you will need to [create an account and generate OAuth credentials](https://developers.google.com/google-apps/calendar/auth). Credentials consist of a `clientId`, `clientSecret`, and a `refreshToken`. A handy resource for generating a long-lived `refreshToken` is the [OAuth playground](https://developers.google.com/oauthplayground).

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

The Google Calendar component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | Google calendar application name. Example would be camel-google-calendar/1.0. |  | String |
| **clientId** (common) | Client ID of the calendar application. |  | String |
| **configuration** (common) | To use the shared configuration. |  | GoogleCalendarConfiguration |
| **delegate** (common) | Delegate for wide-domain service account. |  | String |
| **scopes** (common) | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. | [https://www.googleapis.com/auth/calendar](https://www.googleapis.com/auth/calendar) | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientFactory** (advanced) | To use the GoogleCalendarClientFactory as factory for creating the client. Will by default use BatchGoogleCalendarClientFactory. |  | GoogleCalendarClientFactory |
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the calendar application. |  | String |
| **emailAddress** (security) | The emailAddress of the Google Service Account. |  | String |
| **p12FileName** (security) | The name of the p12 file which has the private key to use with the Google Service Account. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |
| **user** (security) | The email address of the user the application is trying to impersonate in the service account flow. |  | String |

## Endpoint Options

The Google Calendar endpoint is configured using URI syntax:

google-calendar:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   ACL
    
-   LIST
    
-   CALENDARS
    
-   CHANNELS
    
-   COLORS
    
-   FREEBUSY
    
-   EVENTS
    
-   SETTINGS
    





 |  | GoogleCalendarApiName |
| **methodName** (common) | 

**Required** What sub operation to use for the selected operation.

Enum values:

-   calendarImport
    
-   clear
    
-   delete
    
-   get
    
-   insert
    
-   instances
    
-   list
    
-   move
    
-   patch
    
-   query
    
-   quickAdd
    
-   stop
    
-   update
    
-   watch
    





 |  | String |

### Query Parameters (32 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | Google calendar application name. Example would be camel-google-calendar/1.0. |  | String |
| **clientId** (common) | Client ID of the calendar application. |  | String |
| **delegate** (common) | Delegate for wide-domain service account. |  | String |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **scopes** (common) | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. | [https://www.googleapis.com/auth/calendar](https://www.googleapis.com/auth/calendar) | String |
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

## API Parameters (7 APIs)

The Google Calendar endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

google-calendar:apiName/methodName

There are 7 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**acl**](#_api_acl) | Both | The acl collection of methods |
| [**calendars**](#_api_calendars) | Both | The calendars collection of methods |
| [**channels**](#_api_channels) | Both | The channels collection of methods |
| [**events**](#_api_events) | Both | The events collection of methods |
| [**freebusy**](#_api_freebusy) | Both | The freebusy collection of methods |
| [**list**](#_api_list) | Both | The calendarList collection of methods |
| [**settings**](#_api_settings) | Both | The settings collection of methods |

Each API is documented in the following sections to come.

### API: acl

**Both producer and consumer are supported**

The acl API is defined in the syntax as follows:

```none
google-calendar:acl/methodName?[parameters]
```

The 7 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_acl_method_delete) |  | Deletes an access control rule |
| [**get**](#_api_acl_method_get) |  | Returns an access control rule |
| [**insert**](#_api_acl_method_insert) |  | Creates an access control rule |
| [**list**](#_api_acl_method_list) |  | Returns the rules in the access control list for the calendar |
| [**patch**](#_api_acl_method_patch) |  | Updates an access control rule |
| [**update**](#_api_acl_method_update) |  | Updates an access control rule |
| [**watch**](#_api_acl_method_watch) |  | Watch for changes to ACL resources |

#### Method delete

Signatures:

-   com.google.api.services.calendar.Calendar.Acl.Delete delete(String calendarId, String ruleId);
    

The google-calendar/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **ruleId** | ACL rule identifier | String |

#### Method get

Signatures:

-   com.google.api.services.calendar.Calendar.Acl.Get get(String calendarId, String ruleId);
    

The google-calendar/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **ruleId** | ACL rule identifier | String |

#### Method insert

Signatures:

-   com.google.api.services.calendar.Calendar.Acl.Insert insert(String calendarId, com.google.api.services.calendar.model.AclRule content);
    

The google-calendar/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **content** | The com.google.api.services.calendar.model.AclRule | AclRule |
| **sendNotifications** | Whether to send notifications about the calendar sharing change | Boolean |

#### Method list

Signatures:

-   com.google.api.services.calendar.Calendar.Acl.List list(String calendarId);
    

The google-calendar/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **maxResults** | Maximum number of entries returned on one result page | Integer |
| **pageToken** | Token specifying which result page to return | String |
| **showDeleted** | Whether to include deleted ACLs in the result | Boolean |
| **syncToken** | Token obtained from the nextSyncToken field returned on the last page of results from the previous list request | String |

#### Method patch

Signatures:

-   com.google.api.services.calendar.Calendar.Acl.Patch patch(String calendarId, String ruleId, com.google.api.services.calendar.model.AclRule content);
    

The google-calendar/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **content** | The com.google.api.services.calendar.model.AclRule | AclRule |
| **ruleId** | ACL rule identifier | String |
| **sendNotifications** | Whether to send notifications about the calendar sharing change | Boolean |

#### Method update

Signatures:

-   com.google.api.services.calendar.Calendar.Acl.Update update(String calendarId, String ruleId, com.google.api.services.calendar.model.AclRule content);
    

The google-calendar/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **content** | The com.google.api.services.calendar.model.AclRule | AclRule |
| **ruleId** | ACL rule identifier | String |
| **sendNotifications** | Whether to send notifications about the calendar sharing change | Boolean |

#### Method watch

Signatures:

-   com.google.api.services.calendar.Calendar.Acl.Watch watch(String calendarId, com.google.api.services.calendar.model.Channel content);
    

The google-calendar/watch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **contentChannel** | The com.google.api.services.calendar.model.Channel | Channel |
| **maxResults** | Maximum number of entries returned on one result page | Integer |
| **pageToken** | Token specifying which result page to return | String |
| **showDeleted** | Whether to include deleted ACLs in the result | Boolean |
| **syncToken** | Token obtained from the nextSyncToken field returned on the last page of results from the previous list request | String |

In addition to the parameters above, the google-calendar API can also use any of the [Query Parameters (32 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleCalendar.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleCalendar.myParameterNameHere` header.

### API: calendars

**Both producer and consumer are supported**

The calendars API is defined in the syntax as follows:

```none
google-calendar:calendars/methodName?[parameters]
```

The 6 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**clear**](#_api_calendars_method_clear) |  | Clears a primary calendar |
| [**delete**](#_api_calendars_method_delete) |  | Deletes a secondary calendar |
| [**get**](#_api_calendars_method_get) |  | Returns metadata for a calendar |
| [**insert**](#_api_calendars_method_insert) |  | Creates a secondary calendar |
| [**patch**](#_api_calendars_method_patch) |  | Updates metadata for a calendar |
| [**update**](#_api_calendars_method_update) |  | Updates metadata for a calendar |

#### Method clear

Signatures:

-   com.google.api.services.calendar.Calendar.Calendars.Clear clear(String calendarId);
    

The google-calendar/clear API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |

#### Method delete

Signatures:

-   com.google.api.services.calendar.Calendar.Calendars.Delete delete(String calendarId);
    

The google-calendar/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |

#### Method get

Signatures:

-   com.google.api.services.calendar.Calendar.Calendars.Get get(String calendarId);
    

The google-calendar/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |

#### Method insert

Signatures:

-   com.google.api.services.calendar.Calendar.Calendars.Insert insert(com.google.api.services.calendar.model.Calendar content);
    

The google-calendar/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.calendar.model.Calendar | Calendar |

#### Method patch

Signatures:

-   com.google.api.services.calendar.Calendar.Calendars.Patch patch(String calendarId, com.google.api.services.calendar.model.Calendar content);
    

The google-calendar/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **content** | The com.google.api.services.calendar.model.Calendar | Calendar |

#### Method update

Signatures:

-   com.google.api.services.calendar.Calendar.Calendars.Update update(String calendarId, com.google.api.services.calendar.model.Calendar content);
    

The google-calendar/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **content** | The com.google.api.services.calendar.model.Calendar | Calendar |

In addition to the parameters above, the google-calendar API can also use any of the [Query Parameters (32 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleCalendar.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleCalendar.myParameterNameHere` header.

### API: channels

**Both producer and consumer are supported**

The channels API is defined in the syntax as follows:

```none
google-calendar:channels/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**stop**](#_api_channels_method_stop) |  | Stop watching resources through this channel |

#### Method stop

Signatures:

-   com.google.api.services.calendar.Calendar.Channels.Stop stop(com.google.api.services.calendar.model.Channel content);
    

The google-calendar/stop API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentChannel** | The com.google.api.services.calendar.model.Channel | Channel |

In addition to the parameters above, the google-calendar API can also use any of the [Query Parameters (32 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleCalendar.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleCalendar.myParameterNameHere` header.

### API: events

**Both producer and consumer are supported**

The events API is defined in the syntax as follows:

```none
google-calendar:events/methodName?[parameters]
```

The 11 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**calendarImport**](#_api_events_method_calendarImport) |  | Imports an event |
| [**delete**](#_api_events_method_delete) |  | Deletes an event |
| [**get**](#_api_events_method_get) |  | Returns an event based on its Google Calendar ID |
| [**insert**](#_api_events_method_insert) |  | Creates an event |
| [**instances**](#_api_events_method_instances) |  | Returns instances of the specified recurring event |
| [**list**](#_api_events_method_list) |  | Returns events on the specified calendar |
| [**move**](#_api_events_method_move) |  | Moves an event to another calendar, i |
| [**patch**](#_api_events_method_patch) |  | Updates an event |
| [**quickAdd**](#_api_events_method_quickAdd) |  | Creates an event based on a simple text string |
| [**update**](#_api_events_method_update) |  | Updates an event |
| [**watch**](#_api_events_method_watch) |  | Watch for changes to Events resources |

#### Method calendarImport

Signatures:

-   com.google.api.services.calendar.Calendar.Events.CalendarImport calendarImport(String calendarId, com.google.api.services.calendar.model.Event content);
    

The google-calendar/calendarImport API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **conferenceDataVersion** | Version number of conference data supported by the API client | Integer |
| **content** | The com.google.api.services.calendar.model.Event | Event |
| **supportsAttachments** | Whether API client performing operation supports event attachments | Boolean |

#### Method delete

Signatures:

-   com.google.api.services.calendar.Calendar.Events.Delete delete(String calendarId, String eventId);
    

The google-calendar/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **eventId** | Event identifier | String |
| **sendNotifications** | Deprecated | Boolean |
| **sendUpdates** | Guests who should receive notifications about the deletion of the event | String |

#### Method get

Signatures:

-   com.google.api.services.calendar.Calendar.Events.Get get(String calendarId, String eventId);
    

The google-calendar/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **alwaysIncludeEmail** | Deprecated and ignored | Boolean |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **eventId** | Event identifier | String |
| **maxAttendees** | The maximum number of attendees to include in the response | Integer |
| **timeZone** | Time zone used in the response | String |

#### Method insert

Signatures:

-   com.google.api.services.calendar.Calendar.Events.Insert insert(String calendarId, com.google.api.services.calendar.model.Event content);
    

The google-calendar/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **conferenceDataVersion** | Version number of conference data supported by the API client | Integer |
| **content** | The com.google.api.services.calendar.model.Event | Event |
| **maxAttendees** | The maximum number of attendees to include in the response | Integer |
| **sendNotifications** | Deprecated | Boolean |
| **sendUpdates** | Whether to send notifications about the creation of the new event | String |
| **supportsAttachments** | Whether API client performing operation supports event attachments | Boolean |

#### Method instances

Signatures:

-   com.google.api.services.calendar.Calendar.Events.Instances instances(String calendarId, String eventId);
    

The google-calendar/instances API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **alwaysIncludeEmail** | Deprecated and ignored | Boolean |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **eventId** | Recurring event identifier | String |
| **maxAttendees** | The maximum number of attendees to include in the response | Integer |
| **maxResults** | Maximum number of events returned on one result page | Integer |
| **originalStart** | The original start time of the instance in the result | String |
| **pageToken** | Token specifying which result page to return | String |
| **showDeleted** | Whether to include deleted events (with status equals cancelled) in the result | Boolean |
| **timeMax** | Upper bound (exclusive) for an event’s start time to filter by | DateTime |
| **timeMin** | Lower bound (inclusive) for an event’s end time to filter by | DateTime |
| **timeZone** | Time zone used in the response | String |

#### Method list

Signatures:

-   com.google.api.services.calendar.Calendar.Events.List list(String calendarId);
    

The google-calendar/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **alwaysIncludeEmail** | Deprecated and ignored | Boolean |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **eventTypes** | Event types to return | List |
| **iCalUID** | Specifies an event ID in the iCalendar format to be provided in the response | String |
| **maxAttendees** | The maximum number of attendees to include in the response | Integer |
| **maxResults** | Maximum number of events returned on one result page | Integer |
| **orderBy** | The order of the events returned in the result | String |
| **pageToken** | Token specifying which result page to return | String |
| **privateExtendedProperty** | Extended properties constraint specified as propertyName=value | List |
| **q** | Free text search terms to find events that match these terms in the following fields: - summary - description - location - attendee’s displayName - attendee’s email - organizer’s displayName - organizer’s email - workingLocationProperties | String |
| **sharedExtendedProperty** | Extended properties constraint specified as propertyName=value | List |
| **showDeleted** | Whether to include deleted events (with status equals cancelled) in the result | Boolean |
| **showHiddenInvitations** | Whether to include hidden invitations in the result | Boolean |
| **singleEvents** | Whether to expand recurring events into instances and only return single one-off events and instances of recurring events, but not the underlying recurring events themselves | Boolean |
| **syncToken** | Token obtained from the nextSyncToken field returned on the last page of results from the previous list request | String |
| **timeMax** | Upper bound (exclusive) for an event’s start time to filter by | DateTime |
| **timeMin** | Lower bound (exclusive) for an event’s end time to filter by | DateTime |
| **timeZone** | Time zone used in the response | String |
| **updatedMin** | Lower bound for an event’s last modification time (as a RFC3339 timestamp) to filter by | DateTime |

#### Method move

Signatures:

-   com.google.api.services.calendar.Calendar.Events.Move move(String calendarId, String eventId, String destination);
    

The google-calendar/move API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier of the source calendar where the event currently is on | String |
| **destination** | Calendar identifier of the target calendar where the event is to be moved to | String |
| **eventId** | Event identifier | String |
| **sendNotifications** | Deprecated | Boolean |
| **sendUpdates** | Guests who should receive notifications about the change of the event’s organizer | String |

#### Method patch

Signatures:

-   com.google.api.services.calendar.Calendar.Events.Patch patch(String calendarId, String eventId, com.google.api.services.calendar.model.Event content);
    

The google-calendar/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **alwaysIncludeEmail** | Deprecated and ignored | Boolean |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **conferenceDataVersion** | Version number of conference data supported by the API client | Integer |
| **content** | The com.google.api.services.calendar.model.Event | Event |
| **eventId** | Event identifier | String |
| **maxAttendees** | The maximum number of attendees to include in the response | Integer |
| **sendNotifications** | Deprecated | Boolean |
| **sendUpdates** | Guests who should receive notifications about the event update (for example, title changes, etc | String |
| **supportsAttachments** | Whether API client performing operation supports event attachments | Boolean |

#### Method quickAdd

Signatures:

-   com.google.api.services.calendar.Calendar.Events.QuickAdd quickAdd(String calendarId, String text);
    

The google-calendar/quickAdd API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **sendNotifications** | Deprecated | Boolean |
| **sendUpdates** | Guests who should receive notifications about the creation of the new event | String |
| **text** | The text describing the event to be created | String |

#### Method update

Signatures:

-   com.google.api.services.calendar.Calendar.Events.Update update(String calendarId, String eventId, com.google.api.services.calendar.model.Event content);
    

The google-calendar/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **alwaysIncludeEmail** | Deprecated and ignored | Boolean |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **conferenceDataVersion** | Version number of conference data supported by the API client | Integer |
| **content** | The com.google.api.services.calendar.model.Event | Event |
| **eventId** | Event identifier | String |
| **maxAttendees** | The maximum number of attendees to include in the response | Integer |
| **sendNotifications** | Deprecated | Boolean |
| **sendUpdates** | Guests who should receive notifications about the event update (for example, title changes, etc | String |
| **supportsAttachments** | Whether API client performing operation supports event attachments | Boolean |

#### Method watch

Signatures:

-   com.google.api.services.calendar.Calendar.Events.Watch watch(String calendarId, com.google.api.services.calendar.model.Channel content);
    

The google-calendar/watch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **alwaysIncludeEmail** | Deprecated and ignored | Boolean |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **contentChannel** | The com.google.api.services.calendar.model.Channel | Channel |
| **eventTypes** | Event types to return | List |
| **iCalUID** | Specifies an event ID in the iCalendar format to be provided in the response | String |
| **maxAttendees** | The maximum number of attendees to include in the response | Integer |
| **maxResults** | Maximum number of events returned on one result page | Integer |
| **orderBy** | The order of the events returned in the result | String |
| **pageToken** | Token specifying which result page to return | String |
| **privateExtendedProperty** | Extended properties constraint specified as propertyName=value | List |
| **q** | Free text search terms to find events that match these terms in the following fields: - summary - description - location - attendee’s displayName - attendee’s email - organizer’s displayName - organizer’s email - workingLocationProperties | String |
| **sharedExtendedProperty** | Extended properties constraint specified as propertyName=value | List |
| **showDeleted** | Whether to include deleted events (with status equals cancelled) in the result | Boolean |
| **showHiddenInvitations** | Whether to include hidden invitations in the result | Boolean |
| **singleEvents** | Whether to expand recurring events into instances and only return single one-off events and instances of recurring events, but not the underlying recurring events themselves | Boolean |
| **syncToken** | Token obtained from the nextSyncToken field returned on the last page of results from the previous list request | String |
| **timeMax** | Upper bound (exclusive) for an event’s start time to filter by | DateTime |
| **timeMin** | Lower bound (exclusive) for an event’s end time to filter by | DateTime |
| **timeZone** | Time zone used in the response | String |
| **updatedMin** | Lower bound for an event’s last modification time (as a RFC3339 timestamp) to filter by | DateTime |

In addition to the parameters above, the google-calendar API can also use any of the [Query Parameters (32 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleCalendar.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleCalendar.myParameterNameHere` header.

### API: freebusy

**Both producer and consumer are supported**

The freebusy API is defined in the syntax as follows:

```none
google-calendar:freebusy/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**query**](#_api_freebusy_method_query) |  | Returns free/busy information for a set of calendars |

#### Method query

Signatures:

-   com.google.api.services.calendar.Calendar.Freebusy.Query query(com.google.api.services.calendar.model.FreeBusyRequest content);
    

The google-calendar/query API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.calendar.model.FreeBusyRequest | FreeBusyRequest |

In addition to the parameters above, the google-calendar API can also use any of the [Query Parameters (32 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleCalendar.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleCalendar.myParameterNameHere` header.

### API: list

**Both producer and consumer are supported**

The list API is defined in the syntax as follows:

```none
google-calendar:list/methodName?[parameters]
```

The 7 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_list_method_delete) |  | Removes a calendar from the user’s calendar list |
| [**get**](#_api_list_method_get) |  | Returns a calendar from the user’s calendar list |
| [**insert**](#_api_list_method_insert) |  | Inserts an existing calendar into the user’s calendar list |
| [**list**](#_api_list_method_list) |  | Returns the calendars on the user’s calendar list |
| [**patch**](#_api_list_method_patch) |  | Updates an existing calendar on the user’s calendar list |
| [**update**](#_api_list_method_update) |  | Updates an existing calendar on the user’s calendar list |
| [**watch**](#_api_list_method_watch) |  | Watch for changes to CalendarList resources |

#### Method delete

Signatures:

-   com.google.api.services.calendar.Calendar.CalendarList.Delete delete(String calendarId);
    

The google-calendar/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |

#### Method get

Signatures:

-   com.google.api.services.calendar.Calendar.CalendarList.Get get(String calendarId);
    

The google-calendar/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |

#### Method insert

Signatures:

-   com.google.api.services.calendar.Calendar.CalendarList.Insert insert(com.google.api.services.calendar.model.CalendarListEntry content);
    

The google-calendar/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **colorRgbFormat** | Whether to use the foregroundColor and backgroundColor fields to write the calendar colors (RGB) | Boolean |
| **content** | The com.google.api.services.calendar.model.CalendarListEntry | CalendarListEntry |

#### Method list

Signatures:

-   com.google.api.services.calendar.Calendar.CalendarList.List list();
    

The google-calendar/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **maxResults** | Maximum number of entries returned on one result page | Integer |
| **minAccessRole** | The minimum access role for the user in the returned entries | String |
| **pageToken** | Token specifying which result page to return | String |
| **showDeleted** | Whether to include deleted calendar list entries in the result | Boolean |
| **showHidden** | Whether to show hidden entries | Boolean |
| **syncToken** | Token obtained from the nextSyncToken field returned on the last page of results from the previous list request | String |

#### Method patch

Signatures:

-   com.google.api.services.calendar.Calendar.CalendarList.Patch patch(String calendarId, com.google.api.services.calendar.model.CalendarListEntry content);
    

The google-calendar/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **colorRgbFormat** | Whether to use the foregroundColor and backgroundColor fields to write the calendar colors (RGB) | Boolean |
| **content** | The com.google.api.services.calendar.model.CalendarListEntry | CalendarListEntry |

#### Method update

Signatures:

-   com.google.api.services.calendar.Calendar.CalendarList.Update update(String calendarId, com.google.api.services.calendar.model.CalendarListEntry content);
    

The google-calendar/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **calendarId** | Calendar identifier. To retrieve calendar IDs call the calendarList.list method. If you want to access the primary calendar of the currently logged in user, use the primary keyword. | String |
| **colorRgbFormat** | Whether to use the foregroundColor and backgroundColor fields to write the calendar colors (RGB) | Boolean |
| **content** | The com.google.api.services.calendar.model.CalendarListEntry | CalendarListEntry |

#### Method watch

Signatures:

-   com.google.api.services.calendar.Calendar.CalendarList.Watch watch(com.google.api.services.calendar.model.Channel content);
    

The google-calendar/watch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentChannel** | The com.google.api.services.calendar.model.Channel | Channel |
| **maxResults** | Maximum number of entries returned on one result page | Integer |
| **minAccessRole** | The minimum access role for the user in the returned entries | String |
| **pageToken** | Token specifying which result page to return | String |
| **showDeleted** | Whether to include deleted calendar list entries in the result | Boolean |
| **showHidden** | Whether to show hidden entries | Boolean |
| **syncToken** | Token obtained from the nextSyncToken field returned on the last page of results from the previous list request | String |

In addition to the parameters above, the google-calendar API can also use any of the [Query Parameters (32 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleCalendar.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleCalendar.myParameterNameHere` header.

### API: settings

**Both producer and consumer are supported**

The settings API is defined in the syntax as follows:

```none
google-calendar:settings/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**get**](#_api_settings_method_get) |  | Returns a single user setting |
| [**list**](#_api_settings_method_list) |  | Returns all user settings for the authenticated user |
| [**watch**](#_api_settings_method_watch) |  | Watch for changes to Settings resources |

#### Method get

Signatures:

-   com.google.api.services.calendar.Calendar.Settings.Get get(String setting);
    

The google-calendar/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **setting** | The id of the user setting | String |

#### Method list

Signatures:

-   com.google.api.services.calendar.Calendar.Settings.List list();
    

The google-calendar/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **maxResults** | Maximum number of entries returned on one result page | Integer |
| **pageToken** | Token specifying which result page to return | String |
| **syncToken** | Token obtained from the nextSyncToken field returned on the last page of results from the previous list request | String |

#### Method watch

Signatures:

-   com.google.api.services.calendar.Calendar.Settings.Watch watch(com.google.api.services.calendar.model.Channel content);
    

The google-calendar/watch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentChannel** | The com.google.api.services.calendar.model.Channel | Channel |
| **maxResults** | Maximum number of entries returned on one result page | Integer |
| **pageToken** | Token specifying which result page to return | String |
| **syncToken** | Token obtained from the nextSyncToken field returned on the last page of results from the previous list request | String |

In addition to the parameters above, the google-calendar API can also use any of the [Query Parameters (32 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleCalendar.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleCalendar.myParameterNameHere` header.

> **Note**
> This is an API-based component, so per-call parameters can be supplied through `Camel`\-prefixed exchange headers in addition to the endpoint options. If the route consumes messages from untrusted producers, strip these internal headers at the trust boundary — for example with `removeHeaders("Camel*")` — before the message reaches this component, so that a sender cannot override the API call. See [the Camel security model](../../manual/security-model.md) for details.