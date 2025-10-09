# Google Drive

**Since Camel 2.14**

**Both producer and consumer are supported**

The Google Drive component provides access to the [Google Drive file storage service](http://drive.google.com) via the [Google Drive Web APIs](https://developers.google.com/drive/v2/reference).

Google Drive uses the [OAuth 2.0 protocol](https://developers.google.com/accounts/docs/OAuth2) for authenticating a Google account and authorizing access to user data. Before you can use this component, you will need to [create an account and generate OAuth credentials](https://developers.google.com/drive/web/auth/web-server). Credentials comprise of a clientId, clientSecret, and a refreshToken. A handy resource for generating a long-lived refreshToken is the [OAuth playground](https://developers.google.com/oauthplayground).

In the case of a [service account](https://developers.google.com/identity/protocols/oauth2#serviceaccount), credentials comprise of a JSON-file (serviceAccountKey). You can also use [delegation domain-wide authority](https://developers.google.com/identity/protocols/oauth2/service-account#delegatingauthority) (delegate) and one, several, or all possible [Drive API (V2) Auth Scopes](https://developers.google.com/drive/api/v2/about-auth) (scopes).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
        <groupId>org.apache.camel</groupId>
        <artifactId>camel-google-drive</artifactId>
        <!-- use the same version as your Camel core version -->
        <version>x.x.x</version>
</dependency>
```

## URI Format

The GoogleDrive Component uses the following URI format:

google-drive://endpoint-prefix/endpoint?\[options\]

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

The Google Drive component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | Google drive application name. Example would be camel-google-drive/1.0. |  | String |
| **clientId** (common) | Client ID of the drive application. |  | String |
| **configuration** (common) | To use the shared configuration. |  | GoogleDriveConfiguration |
| **delegate** (common) | Delegate for wide-domain service account. |  | String |
| **scopes** (common) | Specifies the level of permissions you want a drive application to have to a user account. See [https://developers.google.com/drive/web/scopes](https://developers.google.com/drive/web/scopes) for more info. |  | List |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientFactory** (advanced) | To use the GoogleCalendarClientFactory as factory for creating the client. Will by default use BatchGoogleDriveClientFactory. |  | GoogleDriveClientFactory |
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the drive application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |

## Endpoint Options

The Google Drive endpoint is configured using URI syntax:

google-drive:apiName/methodName

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   DRIVE\_ABOUT
    
-   DRIVE\_APPS
    
-   DRIVE\_CHANGES
    
-   DRIVE\_CHANNELS
    
-   DRIVE\_CHILDREN
    
-   DRIVE\_COMMENTS
    
-   DRIVE\_FILES
    
-   DRIVE\_PARENTS
    
-   DRIVE\_PERMISSIONS
    
-   DRIVE\_PROPERTIES
    
-   DRIVE\_DRIVES
    
-   DRIVE\_TEAMDRIVES
    
-   DRIVE\_REPLIES
    
-   DRIVE\_REVISIONS
    





 |  | GoogleDriveApiName |
| **methodName** (common) | 

**Required** What sub operation to use for the selected operation.

Enum values:

-   copy
    
-   delete
    
-   get
    
-   getIdForEmail
    
-   insert
    
-   list
    
-   patch
    
-   stop
    
-   touch
    
-   trash
    
-   untrash
    
-   update
    
-   watch
    





 |  | String |

### Query Parameters (30 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | Google drive application name. Example would be camel-google-drive/1.0. |  | String |
| **clientFactory** (common) | To use the GoogleCalendarClientFactory as factory for creating the client. Will by default use BatchGoogleDriveClientFactory. |  | GoogleDriveClientFactory |
| **clientId** (common) | Client ID of the drive application. |  | String |
| **delegate** (common) | Delegate for wide-domain service account. |  | String |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **scopes** (common) | Specifies the level of permissions you want a drive application to have to a user account. See [https://developers.google.com/drive/web/scopes](https://developers.google.com/drive/web/scopes) for more info. |  | List |
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
| **clientSecret** (security) | Client secret of the drive application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |

## API Parameters (13 APIs)

The Google Drive endpoint is an API based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

google-drive:apiName/methodName

There are 13 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**drive-apps**](#_api_drive-apps) | Both | The apps collection of methods |
| [**drive-changes**](#_api_drive-changes) | Both | The changes collection of methods |
| [**drive-channels**](#_api_drive-channels) | Both | The channels collection of methods |
| [**drive-children**](#_api_drive-children) | Both | The children collection of methods |
| [**drive-comments**](#_api_drive-comments) | Both | The comments collection of methods |
| [**drive-drives**](#_api_drive-drives) | Both | The drives collection of methods |
| [**drive-files**](#_api_drive-files) | Both | The files collection of methods |
| [**drive-parents**](#_api_drive-parents) | Both | The parents collection of methods |
| [**drive-permissions**](#_api_drive-permissions) | Both | The permissions collection of methods |
| [**drive-properties**](#_api_drive-properties) | Both | The properties collection of methods |
| [**drive-replies**](#_api_drive-replies) | Both | The replies collection of methods |
| [**drive-revisions**](#_api_drive-revisions) | Both | The revisions collection of methods |
| [**drive-teamdrives**](#_api_drive-teamdrives) | Both | The teamdrives collection of methods |

Each API is documented in the following sections to come.

### API: drive-apps

**Both producer and consumer are supported**

The drive-apps API is defined in the syntax as follows:

```none
google-drive:drive-apps/methodName?[parameters]
```

The 1 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**get**](#_api_drive-apps_method_get) |  | Gets a specific app |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Apps.Get get(String appId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **appId** | The ID of the app | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-changes

**Both producer and consumer are supported**

The drive-changes API is defined in the syntax as follows:

```none
google-drive:drive-changes/methodName?[parameters]
```

The 2 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**get**](#_api_drive-changes_method_get) |  | Deprecated - Use changes |
| [**watch**](#_api_drive-changes_method_watch) |  | Subscribe to changes for a user |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Changes.Get get(String changeId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **changeId** | The ID of the change | String |

#### Method watch

Signatures:

-   com.google.api.services.drive.Drive.Changes.Watch watch(com.google.api.services.drive.model.Channel content);
    

The google-drive/watch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentChannel** | The com.google.api.services.drive.model.Channel | Channel |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-channels

**Both producer and consumer are supported**

The drive-channels API is defined in the syntax as follows:

```none
google-drive:drive-channels/methodName?[parameters]
```

The 1 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**stop**](#_api_drive-channels_method_stop) |  | Stop watching resources through this channel |

#### Method stop

Signatures:

-   com.google.api.services.drive.Drive.Channels.Stop stop(com.google.api.services.drive.model.Channel content);
    

The google-drive/stop API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentChannel** | The com.google.api.services.drive.model.Channel | Channel |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-children

**Both producer and consumer are supported**

The drive-children API is defined in the syntax as follows:

```none
google-drive:drive-children/methodName?[parameters]
```

The 4 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-children_method_delete) |  | Removes a child from a folder |
| [**get**](#_api_drive-children_method_get) |  | Gets a specific child reference |
| [**insert**](#_api_drive-children_method_insert) |  | Inserts a file into a folder |
| [**list**](#_api_drive-children_method_list) |  | Lists a folder’s children |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Children.Delete delete(String folderId, String childId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **childId** | The ID of the child | String |
| **folderId** | The ID of the folder | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Children.Get get(String folderId, String childId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **childId** | The ID of the child | String |
| **folderId** | The ID of the folder | String |

#### Method insert

Signatures:

-   com.google.api.services.drive.Drive.Children.Insert insert(String folderId, com.google.api.services.drive.model.ChildReference content);
    

The google-drive/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.ChildReference | ChildReference |
| **folderId** | The ID of the folder | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Children.List list(String folderId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **folderId** | The ID of the folder | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-comments

**Both producer and consumer are supported**

The drive-comments API is defined in the syntax as follows:

```none
google-drive:drive-comments/methodName?[parameters]
```

The 6 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-comments_method_delete) |  | Deletes a comment |
| [**get**](#_api_drive-comments_method_get) |  | Gets a comment by ID |
| [**insert**](#_api_drive-comments_method_insert) |  | Creates a new comment on the given file |
| [**list**](#_api_drive-comments_method_list) |  | Lists a file’s comments |
| [**patch**](#_api_drive-comments_method_patch) |  | Updates an existing comment |
| [**update**](#_api_drive-comments_method_update) |  | Updates an existing comment |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Comments.Delete delete(String fileId, String commentId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **fileId** | The ID of the file | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Comments.Get get(String fileId, String commentId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **fileId** | The ID of the file | String |

#### Method insert

Signatures:

-   com.google.api.services.drive.Drive.Comments.Insert insert(String fileId, com.google.api.services.drive.model.Comment content);
    

The google-drive/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Comment | Comment |
| **fileId** | The ID of the file | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Comments.List list(String fileId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |

#### Method patch

Signatures:

-   com.google.api.services.drive.Drive.Comments.Patch patch(String fileId, String commentId, com.google.api.services.drive.model.Comment content);
    

The google-drive/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **content** | The com.google.api.services.drive.model.Comment | Comment |
| **fileId** | The ID of the file | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Comments.Update update(String fileId, String commentId, com.google.api.services.drive.model.Comment content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **content** | The com.google.api.services.drive.model.Comment | Comment |
| **fileId** | The ID of the file | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-drives

**Both producer and consumer are supported**

The drive-drives API is defined in the syntax as follows:

```none
google-drive:drive-drives/methodName?[parameters]
```

The 6 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-drives_method_delete) |  | Permanently deletes a shared drive for which the user is an organizer |
| [**get**](#_api_drive-drives_method_get) |  | Gets a shared drive’s metadata by ID |
| [**hide**](#_api_drive-drives_method_hide) |  | Hides a shared drive from the default view |
| [**insert**](#_api_drive-drives_method_insert) |  | Creates a new shared drive |
| [**unhide**](#_api_drive-drives_method_unhide) |  | Restores a shared drive to the default view |
| [**update**](#_api_drive-drives_method_update) |  | Updates the metadata for a shared drive |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Drives.Delete delete(String driveId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **driveId** | The ID of the shared drive | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Drives.Get get(String driveId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **driveId** | The ID of the shared drive | String |

#### Method hide

Signatures:

-   com.google.api.services.drive.Drive.Drives.Hide hide(String driveId);
    

The google-drive/hide API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **driveId** | The ID of the shared drive | String |

#### Method insert

Signatures:

-   com.google.api.services.drive.Drive.Drives.Insert insert(String requestId, com.google.api.services.drive.model.Drive content);
    

The google-drive/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Drive | Drive |
| **requestId** | An ID, such as a random UUID, which uniquely identifies this user’s request for idempotent creation of a shared drive. A repeated request by the same user and with the same request ID will avoid creating duplicates by attempting to create the same shared drive. If the shared drive already exists a 409 error will be returned. | String |

#### Method unhide

Signatures:

-   com.google.api.services.drive.Drive.Drives.Unhide unhide(String driveId);
    

The google-drive/unhide API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **driveId** | The ID of the shared drive | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Drives.Update update(String driveId, com.google.api.services.drive.model.Drive content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Drive | Drive |
| **driveId** | The ID of the shared drive | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-files

**Both producer and consumer are supported**

The drive-files API is defined in the syntax as follows:

```none
google-drive:drive-files/methodName?[parameters]
```

The 11 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**copy**](#_api_drive-files_method_copy) |  | Creates a copy of the specified file |
| [**delete**](#_api_drive-files_method_delete) |  | Permanently deletes a file by ID |
| [**export**](#_api_drive-files_method_export) |  | Exports a Google Workspace document to the requested MIME type and returns exported byte content |
| [**get**](#_api_drive-files_method_get) |  | Gets a file’s metadata or content by ID |
| [**insert**](#_api_drive-files_method_insert) |  | Insert a new file |
| [**patch**](#_api_drive-files_method_patch) |  | Updates a file’s metadata and/or content |
| [**touch**](#_api_drive-files_method_touch) |  | Set the file’s updated time to the current server time |
| [**trash**](#_api_drive-files_method_trash) |  | Moves a file to the trash |
| [**untrash**](#_api_drive-files_method_untrash) |  | Restores a file from the trash |
| [**update**](#_api_drive-files_method_update) |  | Updates a file’s metadata and/or content |
| [**watch**](#_api_drive-files_method_watch) |  | Subscribe to changes on a file |

#### Method copy

Signatures:

-   com.google.api.services.drive.Drive.Files.Copy copy(String fileId, com.google.api.services.drive.model.File content);
    

The google-drive/copy API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.File | File |
| **fileId** | The ID of the file to copy | String |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Files.Delete delete(String fileId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file to delete | String |

#### Method export

Signatures:

-   com.google.api.services.drive.Drive.Files.Export export(String fileId, String mimeType);
    

The google-drive/export API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **mimeType** | The MIME type of the format requested for this export | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Files.Get get(String fileId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID for the file in question | String |

#### Method insert

Signatures:

-   com.google.api.services.drive.Drive.Files.Insert insert(com.google.api.services.drive.model.File content);
    
-   com.google.api.services.drive.Drive.Files.Insert insert(com.google.api.services.drive.model.File content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-drive/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.File media metadata or null if none | File |
| **mediaContent** | The media HTTP content or null if none | AbstractInputStreamContent |

#### Method patch

Signatures:

-   com.google.api.services.drive.Drive.Files.Patch patch(String fileId, com.google.api.services.drive.model.File content);
    

The google-drive/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.File | File |
| **fileId** | The ID of the file to update | String |

#### Method touch

Signatures:

-   com.google.api.services.drive.Drive.Files.Touch touch(String fileId);
    

The google-drive/touch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file to update | String |

#### Method trash

Signatures:

-   com.google.api.services.drive.Drive.Files.Trash trash(String fileId);
    

The google-drive/trash API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file to trash | String |

#### Method untrash

Signatures:

-   com.google.api.services.drive.Drive.Files.Untrash untrash(String fileId);
    

The google-drive/untrash API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file to untrash | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Files.Update update(String fileId, com.google.api.services.drive.model.File content);
    
-   com.google.api.services.drive.Drive.Files.Update update(String fileId, com.google.api.services.drive.model.File content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.File media metadata or null if none | File |
| **fileId** | The ID of the file to update | String |
| **mediaContent** | The media HTTP content or null if none | AbstractInputStreamContent |

#### Method watch

Signatures:

-   com.google.api.services.drive.Drive.Files.Watch watch(String fileId, com.google.api.services.drive.model.Channel content);
    

The google-drive/watch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentChannel** | The com.google.api.services.drive.model.Channel | Channel |
| **fileId** | The ID for the file in question | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-parents

**Both producer and consumer are supported**

The drive-parents API is defined in the syntax as follows:

```none
google-drive:drive-parents/methodName?[parameters]
```

The 4 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-parents_method_delete) |  | Removes a parent from a file |
| [**get**](#_api_drive-parents_method_get) |  | Gets a specific parent reference |
| [**insert**](#_api_drive-parents_method_insert) |  | Adds a parent folder for a file |
| [**list**](#_api_drive-parents_method_list) |  | Lists a file’s parents |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Parents.Delete delete(String fileId, String parentId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **parentId** | The ID of the parent | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Parents.Get get(String fileId, String parentId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **parentId** | The ID of the parent | String |

#### Method insert

Signatures:

-   com.google.api.services.drive.Drive.Parents.Insert insert(String fileId, com.google.api.services.drive.model.ParentReference content);
    

The google-drive/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.ParentReference | ParentReference |
| **fileId** | The ID of the file | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Parents.List list(String fileId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-permissions

**Both producer and consumer are supported**

The drive-permissions API is defined in the syntax as follows:

```none
google-drive:drive-permissions/methodName?[parameters]
```

The 7 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-permissions_method_delete) |  | Deletes a permission from a file or shared drive |
| [**get**](#_api_drive-permissions_method_get) |  | Gets a permission by ID |
| [**getIdForEmail**](#_api_drive-permissions_method_getIdForEmail) |  | Returns the permission ID for an email address |
| [**insert**](#_api_drive-permissions_method_insert) |  | Inserts a permission for a file or shared drive |
| [**list**](#_api_drive-permissions_method_list) |  | Lists a file’s or shared drive’s permissions |
| [**patch**](#_api_drive-permissions_method_patch) |  | Updates a permission using patch semantics |
| [**update**](#_api_drive-permissions_method_update) |  | Updates a permission |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Permissions.Delete delete(String fileId, String permissionId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID for the file or shared drive | String |
| **permissionId** | The ID for the permission | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Permissions.Get get(String fileId, String permissionId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID for the file or shared drive | String |
| **permissionId** | The ID for the permission | String |

#### Method getIdForEmail

Signatures:

-   com.google.api.services.drive.Drive.Permissions.GetIdForEmail getIdForEmail(String email);
    

The google-drive/getIdForEmail API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **email** | The email address for which to return a permission ID | String |

#### Method insert

Signatures:

-   com.google.api.services.drive.Drive.Permissions.Insert insert(String fileId, com.google.api.services.drive.model.Permission content);
    

The google-drive/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Permission | Permission |
| **fileId** | The ID for the file or shared drive | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Permissions.List list(String fileId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID for the file or shared drive | String |

#### Method patch

Signatures:

-   com.google.api.services.drive.Drive.Permissions.Patch patch(String fileId, String permissionId, com.google.api.services.drive.model.Permission content);
    

The google-drive/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Permission | Permission |
| **fileId** | The ID for the file or shared drive | String |
| **permissionId** | The ID for the permission | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Permissions.Update update(String fileId, String permissionId, com.google.api.services.drive.model.Permission content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Permission | Permission |
| **fileId** | The ID for the file or shared drive | String |
| **permissionId** | The ID for the permission | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-properties

**Both producer and consumer are supported**

The drive-properties API is defined in the syntax as follows:

```none
google-drive:drive-properties/methodName?[parameters]
```

The 6 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-properties_method_delete) |  | Deletes a property |
| [**get**](#_api_drive-properties_method_get) |  | Gets a property by its key |
| [**insert**](#_api_drive-properties_method_insert) |  | Adds a property to a file, or updates it if it already exists |
| [**list**](#_api_drive-properties_method_list) |  | Lists a file’s properties |
| [**patch**](#_api_drive-properties_method_patch) |  | Updates a property |
| [**update**](#_api_drive-properties_method_update) |  | Updates a property |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Properties.Delete delete(String fileId, String propertyKey);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **propertyKey** | The key of the property | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Properties.Get get(String fileId, String propertyKey);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **propertyKey** | The key of the property | String |

#### Method insert

Signatures:

-   com.google.api.services.drive.Drive.Properties.Insert insert(String fileId, com.google.api.services.drive.model.Property content);
    

The google-drive/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Property | Property |
| **fileId** | The ID of the file | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Properties.List list(String fileId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |

#### Method patch

Signatures:

-   com.google.api.services.drive.Drive.Properties.Patch patch(String fileId, String propertyKey, com.google.api.services.drive.model.Property content);
    

The google-drive/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Property | Property |
| **fileId** | The ID of the file | String |
| **propertyKey** | The key of the property | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Properties.Update update(String fileId, String propertyKey, com.google.api.services.drive.model.Property content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Property | Property |
| **fileId** | The ID of the file | String |
| **propertyKey** | The key of the property | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-replies

**Both producer and consumer are supported**

The drive-replies API is defined in the syntax as follows:

```none
google-drive:drive-replies/methodName?[parameters]
```

The 6 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-replies_method_delete) |  | Deletes a reply |
| [**get**](#_api_drive-replies_method_get) |  | Gets a reply |
| [**insert**](#_api_drive-replies_method_insert) |  | Creates a new reply to the given comment |
| [**list**](#_api_drive-replies_method_list) |  | Lists all of the replies to a comment |
| [**patch**](#_api_drive-replies_method_patch) |  | Updates an existing reply |
| [**update**](#_api_drive-replies_method_update) |  | Updates an existing reply |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Replies.Delete delete(String fileId, String commentId, String replyId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **fileId** | The ID of the file | String |
| **replyId** | The ID of the reply | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Replies.Get get(String fileId, String commentId, String replyId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **fileId** | The ID of the file | String |
| **replyId** | The ID of the reply | String |

#### Method insert

Signatures:

-   com.google.api.services.drive.Drive.Replies.Insert insert(String fileId, String commentId, com.google.api.services.drive.model.CommentReply content);
    

The google-drive/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **content** | The com.google.api.services.drive.model.CommentReply | CommentReply |
| **fileId** | The ID of the file | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Replies.List list(String fileId, String commentId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **fileId** | The ID of the file | String |

#### Method patch

Signatures:

-   com.google.api.services.drive.Drive.Replies.Patch patch(String fileId, String commentId, String replyId, com.google.api.services.drive.model.CommentReply content);
    

The google-drive/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **content** | The com.google.api.services.drive.model.CommentReply | CommentReply |
| **fileId** | The ID of the file | String |
| **replyId** | The ID of the reply | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Replies.Update update(String fileId, String commentId, String replyId, com.google.api.services.drive.model.CommentReply content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **content** | The com.google.api.services.drive.model.CommentReply | CommentReply |
| **fileId** | The ID of the file | String |
| **replyId** | The ID of the reply | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-revisions

**Both producer and consumer are supported**

The drive-revisions API is defined in the syntax as follows:

```none
google-drive:drive-revisions/methodName?[parameters]
```

The 5 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-revisions_method_delete) |  | Permanently deletes a file version |
| [**get**](#_api_drive-revisions_method_get) |  | Gets a specific revision |
| [**list**](#_api_drive-revisions_method_list) |  | Lists a file’s revisions |
| [**patch**](#_api_drive-revisions_method_patch) |  | Updates a revision |
| [**update**](#_api_drive-revisions_method_update) |  | Updates a revision |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Revisions.Delete delete(String fileId, String revisionId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **revisionId** | The ID of the revision | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Revisions.Get get(String fileId, String revisionId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **revisionId** | The ID of the revision | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Revisions.List list(String fileId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |

#### Method patch

Signatures:

-   com.google.api.services.drive.Drive.Revisions.Patch patch(String fileId, String revisionId, com.google.api.services.drive.model.Revision content);
    

The google-drive/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Revision | Revision |
| **fileId** | The ID for the file | String |
| **revisionId** | The ID for the revision | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Revisions.Update update(String fileId, String revisionId, com.google.api.services.drive.model.Revision content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Revision | Revision |
| **fileId** | The ID for the file | String |
| **revisionId** | The ID for the revision | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-teamdrives

**Both producer and consumer are supported**

The drive-teamdrives API is defined in the syntax as follows:

```none
google-drive:drive-teamdrives/methodName?[parameters]
```

The 4 method(s) is listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand alias name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-teamdrives_method_delete) |  | Deprecated use drives |
| [**get**](#_api_drive-teamdrives_method_get) |  | Deprecated use drives |
| [**insert**](#_api_drive-teamdrives_method_insert) |  | Deprecated use drives |
| [**update**](#_api_drive-teamdrives_method_update) |  | Deprecated use drives |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Teamdrives.Delete delete(String teamDriveId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **teamDriveId** | The ID of the Team Drive | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Teamdrives.Get get(String teamDriveId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **teamDriveId** | The ID of the Team Drive | String |

#### Method insert

Signatures:

-   com.google.api.services.drive.Drive.Teamdrives.Insert insert(String requestId, com.google.api.services.drive.model.TeamDrive content);
    

The google-drive/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.TeamDrive | TeamDrive |
| **requestId** | An ID, such as a random UUID, which uniquely identifies this user’s request for idempotent creation of a Team Drive. A repeated request by the same user and with the same request ID will avoid creating duplicates by attempting to create the same Team Drive. If the Team Drive already exists a 409 error will be returned. | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Teamdrives.Update update(String teamDriveId, com.google.api.services.drive.model.TeamDrive content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.TeamDrive | TeamDrive |
| **teamDriveId** | The ID of the Team Drive | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e. the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

## More Information

For more information on the endpoints and options see API documentation at: [https://developers.google.com/drive/v2/reference/](https://developers.google.com/drive/v2/reference/)

## Spring Boot Auto-Configuration

When using google-drive with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-drive-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-drive.access-token** | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **camel.component.google-drive.application-name** | Google drive application name. Example would be camel-google-drive/1.0. |  | String |
| **camel.component.google-drive.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-drive.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-drive.client-factory** | To use the GoogleCalendarClientFactory as factory for creating the client. Will by default use BatchGoogleDriveClientFactory. The option is a org.apache.camel.component.google.drive.GoogleDriveClientFactory type. |  | GoogleDriveClientFactory |
| **camel.component.google-drive.client-id** | Client ID of the drive application. |  | String |
| **camel.component.google-drive.client-secret** | Client secret of the drive application. |  | String |
| **camel.component.google-drive.configuration** | To use the shared configuration. The option is a org.apache.camel.component.google.drive.GoogleDriveConfiguration type. |  | GoogleDriveConfiguration |
| **camel.component.google-drive.delegate** | Delegate for wide-domain service account. |  | String |
| **camel.component.google-drive.enabled** | Whether to enable auto configuration of the google-drive component. This is enabled by default. |  | Boolean |
| **camel.component.google-drive.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-drive.refresh-token** | OAuth 2 refresh token. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **camel.component.google-drive.scopes** | Specifies the level of permissions you want a drive application to have to a user account. See [https://developers.google.com/drive/web/scopes](https://developers.google.com/drive/web/scopes) for more info. |  | List |
| **camel.component.google-drive.service-account-key** | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |