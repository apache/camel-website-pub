# Google Drive

**Since Camel 2.14**

**Both producer and consumer are supported**

The Google Drive component provides access to the [Google Drive file storage service](http://drive.google.com) via the [Google Drive Web APIs](https://developers.google.com/drive/v2/reference).

Google Drive uses the [OAuth 2.0 protocol](https://developers.google.com/accounts/docs/OAuth2) for authenticating a Google account and authorizing access to user data. Before you can use this component, you will need to [create an account and generate OAuth credentials](https://developers.google.com/drive/web/auth/web-server). Credentials consist of a `clientId`, `clientSecret`, and a `refreshToken`. A handy resource for generating a long-lived `refreshToken` is the [OAuth playground](https://developers.google.com/oauthplayground).

In the case of a [service account](https://developers.google.com/identity/protocols/oauth2#serviceaccount), credentials consist of a JSON-file (serviceAccountKey). You can also use [delegation domain-wide authority](https://developers.google.com/identity/protocols/oauth2/service-account#delegatingauthority) (delegate) and one, several, or all possible [Drive API (V2) Auth Scopes](https://developers.google.com/drive/api/v2/about-auth).

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

The Google Drive component supports 15 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | Google drive application name. Example would be camel-google-drive/1.0. |  | String |
| **clientId** (common) | Client ID of the drive application. |  | String |
| **configuration** (common) | To use the shared configuration. |  | GoogleDriveConfiguration |
| **delegate** (common) | Delegate for wide-domain service account. |  | String |
| **scopes** (common) | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientFactory** (advanced) | To use the GoogleCalendarClientFactory as factory for creating the client. Will by default use BatchGoogleDriveClientFactory. |  | GoogleDriveClientFactory |
| **proxyHost** (proxy) | Proxy server host. |  | String |
| **proxyPort** (proxy) | Proxy server port. |  | Integer |
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the drive application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Drive component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |

## Endpoint Options

The Google Drive endpoint is configured using URI syntax:

google-drive:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   DRIVE\_ABOUT
    
-   DRIVE\_CHANGES
    
-   DRIVE\_CHANNELS
    
-   DRIVE\_COMMENTS
    
-   DRIVE\_DRIVES
    
-   DRIVE\_FILES
    
-   DRIVE\_PERMISSIONS
    
-   DRIVE\_REPLIES
    
-   DRIVE\_REVISIONS
    
-   DRIVE\_TEAMDRIVES
    





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
| **scopes** (common) | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
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
| **clientSecret** (security) | Client secret of the drive application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Drive component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |

## API Parameters (9 APIs)

The Google Drive endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

google-drive:apiName/methodName

There are 9 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**drive-changes**](#_api_drive-changes) | Both | The changes collection of methods |
| [**drive-channels**](#_api_drive-channels) | Both | The channels collection of methods |
| [**drive-comments**](#_api_drive-comments) | Both | The comments collection of methods |
| [**drive-drives**](#_api_drive-drives) | Both | The drives collection of methods |
| [**drive-files**](#_api_drive-files) | Both | The files collection of methods |
| [**drive-permissions**](#_api_drive-permissions) | Both | The permissions collection of methods |
| [**drive-replies**](#_api_drive-replies) | Both | The replies collection of methods |
| [**drive-revisions**](#_api_drive-revisions) | Both | The revisions collection of methods |
| [**drive-teamdrives**](#_api_drive-teamdrives) | Both | The teamdrives collection of methods |

Each API is documented in the following sections to come.

### API: drive-changes

**Both producer and consumer are supported**

The drive-changes API is defined in the syntax as follows:

```none
google-drive:drive-changes/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**getStartPageToken**](#_api_drive-changes_method_getStartPageToken) |  | Gets the starting pageToken for listing future changes |
| [**list**](#_api_drive-changes_method_list) |  | Lists the changes for a user or shared drive |
| [**watch**](#_api_drive-changes_method_watch) |  | Subscribes to changes for a user |

#### Method getStartPageToken

Signatures:

-   com.google.api.services.drive.Drive.Changes.GetStartPageToken getStartPageToken();
    

The google-drive/getStartPageToken API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **driveId** | The ID of the shared drive for which the starting pageToken for listing future changes from that shared drive will be returned | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **teamDriveId** | Deprecated: Use driveId instead | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Changes.List list(String pageToken);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **driveId** | The shared drive from which changes will be returned | String |
| **includeCorpusRemovals** | Whether changes should include the file resource if the file is still accessible by the user at the time of the request, even when a file was removed from the list of changes and there will be no further change entries for this file | Boolean |
| **includeItemsFromAllDrives** | Whether both My Drive and shared drive items should be included in results | Boolean |
| **includeLabels** | A comma-separated list of IDs of labels to include in the labelInfo part of the response | String |
| **includePermissionsForView** | Specifies which additional view’s permissions to include in the response | String |
| **includeRemoved** | Whether to include changes indicating that items have been removed from the list of changes, for example by deletion or loss of access | Boolean |
| **includeTeamDriveItems** | Deprecated: Use includeItemsFromAllDrives instead | Boolean |
| **pageSize** | The maximum number of changes to return per page | Integer |
| **pageToken** | The token for continuing a previous list request on the next page. This should be set to the value of 'nextPageToken' from the previous response or to the response from the getStartPageToken method. | String |
| **restrictToMyDrive** | Whether to restrict the results to changes inside the My Drive hierarchy | Boolean |
| **spaces** | A comma-separated list of spaces to query within the corpora | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **teamDriveId** | Deprecated: Use driveId instead | String |

#### Method watch

Signatures:

-   com.google.api.services.drive.Drive.Changes.Watch watch(String pageToken, com.google.api.services.drive.model.Channel content);
    

The google-drive/watch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentChannel** | The com.google.api.services.drive.model.Channel | Channel |
| **driveId** | The shared drive from which changes will be returned | String |
| **includeCorpusRemovals** | Whether changes should include the file resource if the file is still accessible by the user at the time of the request, even when a file was removed from the list of changes and there will be no further change entries for this file | Boolean |
| **includeItemsFromAllDrives** | Whether both My Drive and shared drive items should be included in results | Boolean |
| **includeLabels** | A comma-separated list of IDs of labels to include in the labelInfo part of the response | String |
| **includePermissionsForView** | Specifies which additional view’s permissions to include in the response | String |
| **includeRemoved** | Whether to include changes indicating that items have been removed from the list of changes, for example by deletion or loss of access | Boolean |
| **includeTeamDriveItems** | Deprecated: Use includeItemsFromAllDrives instead | Boolean |
| **pageSize** | The maximum number of changes to return per page | Integer |
| **pageToken** | The token for continuing a previous list request on the next page. This should be set to the value of 'nextPageToken' from the previous response or to the response from the getStartPageToken method. | String |
| **restrictToMyDrive** | Whether to restrict the results to changes inside the My Drive hierarchy | Boolean |
| **spaces** | A comma-separated list of spaces to query within the corpora | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **teamDriveId** | Deprecated: Use driveId instead | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-channels

**Both producer and consumer are supported**

The drive-channels API is defined in the syntax as follows:

```none
google-drive:drive-channels/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**stop**](#_api_drive-channels_method_stop) |  | Stops watching resources through this channel |

#### Method stop

Signatures:

-   com.google.api.services.drive.Drive.Channels.Stop stop(com.google.api.services.drive.model.Channel content);
    

The google-drive/stop API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **contentChannel** | The com.google.api.services.drive.model.Channel | Channel |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-comments

**Both producer and consumer are supported**

The drive-comments API is defined in the syntax as follows:

```none
google-drive:drive-comments/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_drive-comments_method_create) |  | Creates a comment on a file |
| [**delete**](#_api_drive-comments_method_delete) |  | Deletes a comment |
| [**get**](#_api_drive-comments_method_get) |  | Gets a comment by ID |
| [**list**](#_api_drive-comments_method_list) |  | Lists a file’s comments |
| [**update**](#_api_drive-comments_method_update) |  | Updates a comment with patch semantics |

#### Method create

Signatures:

-   com.google.api.services.drive.Drive.Comments.Create create(String fileId, com.google.api.services.drive.model.Comment content);
    

The google-drive/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Comment | Comment |
| **fileId** | The ID of the file | String |

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
| **includeDeleted** | Whether to return deleted comments | Boolean |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Comments.List list(String fileId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **includeDeleted** | Whether to include deleted comments | Boolean |
| **pageSize** | The maximum number of comments to return per page | Integer |
| **pageToken** | The token for continuing a previous list request on the next page | String |
| **startModifiedTime** | The minimum value of 'modifiedTime' for the result comments (RFC 3339 date-time) | String |

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

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-drives

**Both producer and consumer are supported**

The drive-drives API is defined in the syntax as follows:

```none
google-drive:drive-drives/methodName?[parameters]
```

The 7 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_drive-drives_method_create) |  | Creates a shared drive |
| [**delete**](#_api_drive-drives_method_delete) |  | Permanently deletes a shared drive for which the user is an organizer |
| [**get**](#_api_drive-drives_method_get) |  | Gets a shared drive’s metadata by ID |
| [**hide**](#_api_drive-drives_method_hide) |  | Hides a shared drive from the default view |
| [**list**](#_api_drive-drives_method_list) |  | Lists the user’s shared drives |
| [**unhide**](#_api_drive-drives_method_unhide) |  | Restores a shared drive to the default view |
| [**update**](#_api_drive-drives_method_update) |  | Updates the metadata for a shared drive |

#### Method create

Signatures:

-   com.google.api.services.drive.Drive.Drives.Create create(String requestId, com.google.api.services.drive.model.Drive content);
    

The google-drive/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Drive | Drive |
| **requestId** | Required. An ID, such as a random UUID, which uniquely identifies this user’s request for idempotent creation of a shared drive. A repeated request by the same user and with the same request ID will avoid creating duplicates by attempting to create the same shared drive. If the shared drive already exists a 409 error will be returned. | String |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Drives.Delete delete(String driveId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **allowItemDeletion** | Whether any items inside the shared drive should also be deleted | Boolean |
| **driveId** | The ID of the shared drive | String |
| **useDomainAdminAccess** | Issue the request as a domain administrator; if set to true, then the requester will be granted access if they are an administrator of the domain to which the shared drive belongs | Boolean |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Drives.Get get(String driveId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **driveId** | The ID of the shared drive | String |
| **useDomainAdminAccess** | Issue the request as a domain administrator; if set to true, then the requester will be granted access if they are an administrator of the domain to which the shared drive belongs | Boolean |

#### Method hide

Signatures:

-   com.google.api.services.drive.Drive.Drives.Hide hide(String driveId);
    

The google-drive/hide API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **driveId** | The ID of the shared drive | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Drives.List list();
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pageSize** | Maximum number of shared drives to return per page | Integer |
| **pageToken** | Page token for shared drives | String |
| **q** | Query string for searching shared drives | String |
| **useDomainAdminAccess** | Issue the request as a domain administrator; if set to true, then all shared drives of the domain in which the requester is an administrator are returned | Boolean |

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
| **useDomainAdminAccess** | Issue the request as a domain administrator; if set to true, then the requester will be granted access if they are an administrator of the domain to which the shared drive belongs | Boolean |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-files

**Both producer and consumer are supported**

The drive-files API is defined in the syntax as follows:

```none
google-drive:drive-files/methodName?[parameters]
```

The 13 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**copy**](#_api_drive-files_method_copy) |  | Creates a copy of a file and applies any requested updates with patch semantics |
| [**create**](#_api_drive-files_method_create) |  | Creates a file |
| [**delete**](#_api_drive-files_method_delete) |  | Permanently deletes a file owned by the user without moving it to the trash |
| [**download**](#_api_drive-files_method_download) |  | Downloads the content of a file |
| [**emptyTrash**](#_api_drive-files_method_emptyTrash) |  | Permanently deletes all of the user’s trashed files |
| [**export**](#_api_drive-files_method_export) |  | Exports a Google Workspace document to the requested MIME type and returns exported byte content |
| [**generateIds**](#_api_drive-files_method_generateIds) |  | Generates a set of file IDs which can be provided in create or copy requests |
| [**get**](#_api_drive-files_method_get) |  | Gets a file’s metadata or content by ID |
| [**list**](#_api_drive-files_method_list) |  | Lists the user’s files |
| [**listLabels**](#_api_drive-files_method_listLabels) |  | Lists the labels on a file |
| [**modifyLabels**](#_api_drive-files_method_modifyLabels) |  | Modifies the set of labels applied to a file |
| [**update**](#_api_drive-files_method_update) |  | Updates a file’s metadata, content, or both |
| [**watch**](#_api_drive-files_method_watch) |  | Subscribes to changes to a file |

#### Method copy

Signatures:

-   com.google.api.services.drive.Drive.Files.Copy copy(String fileId, com.google.api.services.drive.model.File content);
    

The google-drive/copy API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **enforceSingleParent** | Deprecated: Copying files into multiple folders is no longer supported | Boolean |
| **file** | The com.google.api.services.drive.model.File | File |
| **fileId** | The ID of the file | String |
| **ignoreDefaultVisibility** | Whether to ignore the domain’s default visibility settings for the created file | Boolean |
| **includeLabels** | A comma-separated list of IDs of labels to include in the labelInfo part of the response | String |
| **includePermissionsForView** | Specifies which additional view’s permissions to include in the response | String |
| **keepRevisionForever** | Whether to set the keepForever field in the new head revision | Boolean |
| **ocrLanguage** | A language hint for OCR processing during image import (ISO 639-1 code) | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |

#### Method create

Signatures:

-   com.google.api.services.drive.Drive.Files.Create create(com.google.api.services.drive.model.File content);
    
-   com.google.api.services.drive.Drive.Files.Create create(com.google.api.services.drive.model.File content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-drive/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.File media metadata or null if none | File |
| **enforceSingleParent** | Deprecated: Creating files in multiple folders is no longer supported | Boolean |
| **ignoreDefaultVisibility** | Whether to ignore the domain’s default visibility settings for the created file | Boolean |
| **includeLabels** | A comma-separated list of IDs of labels to include in the labelInfo part of the response | String |
| **includePermissionsForView** | Specifies which additional view’s permissions to include in the response | String |
| **keepRevisionForever** | Whether to set the keepForever field in the new head revision | Boolean |
| **mediaContent** | The media HTTP content | AbstractInputStreamContent |
| **ocrLanguage** | A language hint for OCR processing during image import (ISO 639-1 code) | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **useContentAsIndexableText** | Whether to use the uploaded content as indexable text | Boolean |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Files.Delete delete(String fileId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **enforceSingleParent** | Deprecated: If an item isn’t in a shared drive and its last parent is deleted but the item itself isn’t, the item will be placed under its owner’s root | Boolean |
| **fileId** | The ID of the file | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |

#### Method download

Signatures:

-   com.google.api.services.drive.Drive.Files.Download download(String fileId);
    

The google-drive/download API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | Required. The ID of the file to download. | String |
| **mimeType** | Optional | String |
| **revisionId** | Optional | String |

#### Method emptyTrash

Signatures:

-   com.google.api.services.drive.Drive.Files.EmptyTrash emptyTrash();
    

The google-drive/emptyTrash API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **driveId** | If set, empties the trash of the provided shared drive | String |
| **enforceSingleParent** | Deprecated: If an item isn’t in a shared drive and its last parent is deleted but the item itself isn’t, the item will be placed under its owner’s root | Boolean |

#### Method export

Signatures:

-   com.google.api.services.drive.Drive.Files.Export export(String fileId, String mimeType);
    

The google-drive/export API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **mimeType** | Required. The MIME type of the format requested for this export. For a list of supported MIME types, see Export MIME types for Google Workspace documents(/workspace/drive/api/guides/ref- export-formats). | String |

#### Method generateIds

Signatures:

-   com.google.api.services.drive.Drive.Files.GenerateIds generateIds();
    

The google-drive/generateIds API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **count** | The number of IDs to return | Integer |
| **space** | The space in which the IDs can be used to create files | String |
| **type** | The type of items which the IDs can be used for | String |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Files.Get get(String fileId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **acknowledgeAbuse** | Whether the user is acknowledging the risk of downloading known malware or other abusive files | Boolean |
| **fileId** | The ID of the file | String |
| **includeLabels** | A comma-separated list of IDs of labels to include in the labelInfo part of the response | String |
| **includePermissionsForView** | Specifies which additional view’s permissions to include in the response | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Files.List list();
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **corpora** | Bodies of items (files or documents) to which the query applies | String |
| **corpus** | Deprecated: The source of files to list | String |
| **driveId** | ID of the shared drive to search | String |
| **includeItemsFromAllDrives** | Whether both My Drive and shared drive items should be included in results | Boolean |
| **includeLabels** | A comma-separated list of IDs of labels to include in the labelInfo part of the response | String |
| **includePermissionsForView** | Specifies which additional view’s permissions to include in the response | String |
| **includeTeamDriveItems** | Deprecated: Use includeItemsFromAllDrives instead | Boolean |
| **orderBy** | A comma-separated list of sort keys | String |
| **pageSize** | The maximum number of files to return per page | Integer |
| **pageToken** | The token for continuing a previous list request on the next page | String |
| **q** | A query for filtering the file results | String |
| **spaces** | A comma-separated list of spaces to query within the corpora | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **teamDriveId** | Deprecated: Use driveId instead | String |

#### Method listLabels

Signatures:

-   com.google.api.services.drive.Drive.Files.ListLabels listLabels(String fileId);
    

The google-drive/listLabels API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID for the file | String |
| **maxResults** | The maximum number of labels to return per page | Integer |
| **pageToken** | The token for continuing a previous list request on the next page | String |

#### Method modifyLabels

Signatures:

-   com.google.api.services.drive.Drive.Files.ModifyLabels modifyLabels(String fileId, com.google.api.services.drive.model.ModifyLabelsRequest content);
    

The google-drive/modifyLabels API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file to which the labels belong | String |
| **modifyLabelsRequest** | The com.google.api.services.drive.model.ModifyLabelsRequest | ModifyLabelsRequest |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Files.Update update(String fileId, com.google.api.services.drive.model.File content);
    
-   com.google.api.services.drive.Drive.Files.Update update(String fileId, com.google.api.services.drive.model.File content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **addParents** | A comma-separated list of parent IDs to add | String |
| **enforceSingleParent** | Deprecated: Adding files to multiple folders is no longer supported | Boolean |
| **file** | The com.google.api.services.drive.model.File media metadata or null if none | File |
| **fileId** | The ID of the file | String |
| **includeLabels** | A comma-separated list of IDs of labels to include in the labelInfo part of the response | String |
| **includePermissionsForView** | Specifies which additional view’s permissions to include in the response | String |
| **keepRevisionForever** | Whether to set the keepForever field in the new head revision | Boolean |
| **mediaContent** | The media HTTP content | AbstractInputStreamContent |
| **ocrLanguage** | A language hint for OCR processing during image import (ISO 639-1 code) | String |
| **removeParents** | A comma-separated list of parent IDs to remove | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **useContentAsIndexableText** | Whether to use the uploaded content as indexable text | Boolean |

#### Method watch

Signatures:

-   com.google.api.services.drive.Drive.Files.Watch watch(String fileId, com.google.api.services.drive.model.Channel content);
    

The google-drive/watch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **acknowledgeAbuse** | Whether the user is acknowledging the risk of downloading known malware or other abusive files | Boolean |
| **channel** | The com.google.api.services.drive.model.Channel | Channel |
| **fileId** | The ID of the file | String |
| **includeLabels** | A comma-separated list of IDs of labels to include in the labelInfo part of the response | String |
| **includePermissionsForView** | Specifies which additional view’s permissions to include in the response | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-permissions

**Both producer and consumer are supported**

The drive-permissions API is defined in the syntax as follows:

```none
google-drive:drive-permissions/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_drive-permissions_method_create) |  | Creates a permission for a file or shared drive |
| [**delete**](#_api_drive-permissions_method_delete) |  | Deletes a permission |
| [**get**](#_api_drive-permissions_method_get) |  | Gets a permission by ID |
| [**list**](#_api_drive-permissions_method_list) |  | Lists a file’s or shared drive’s permissions |
| [**update**](#_api_drive-permissions_method_update) |  | Updates a permission with patch semantics |

#### Method create

Signatures:

-   com.google.api.services.drive.Drive.Permissions.Create create(String fileId, com.google.api.services.drive.model.Permission content);
    

The google-drive/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Permission | Permission |
| **emailMessage** | A plain text custom message to include in the notification email | String |
| **enforceExpansiveAccess** | Whether the request should enforce expansive access rules | Boolean |
| **enforceSingleParent** | Deprecated: See moveToNewOwnersRoot for details | Boolean |
| **fileId** | The ID of the file or shared drive | String |
| **moveToNewOwnersRoot** | This parameter only takes effect if the item isn’t in a shared drive and the request is attempting to transfer the ownership of the item | Boolean |
| **sendNotificationEmail** | Whether to send a notification email when sharing to users or groups | Boolean |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **transferOwnership** | Whether to transfer ownership to the specified user and downgrade the current owner to a writer | Boolean |
| **useDomainAdminAccess** | Issue the request as a domain administrator | Boolean |

#### Method delete

Signatures:

-   com.google.api.services.drive.Drive.Permissions.Delete delete(String fileId, String permissionId);
    

The google-drive/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **enforceExpansiveAccess** | Whether the request should enforce expansive access rules | Boolean |
| **fileId** | The ID of the file or shared drive | String |
| **permissionId** | The ID of the permission | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **useDomainAdminAccess** | Issue the request as a domain administrator | Boolean |

#### Method get

Signatures:

-   com.google.api.services.drive.Drive.Permissions.Get get(String fileId, String permissionId);
    

The google-drive/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **permissionId** | The ID of the permission | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **useDomainAdminAccess** | Issue the request as a domain administrator | Boolean |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Permissions.List list(String fileId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file or shared drive | String |
| **includePermissionsForView** | Specifies which additional view’s permissions to include in the response | String |
| **pageSize** | The maximum number of permissions to return per page | Integer |
| **pageToken** | The token for continuing a previous list request on the next page | String |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **useDomainAdminAccess** | Issue the request as a domain administrator | Boolean |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Permissions.Update update(String fileId, String permissionId, com.google.api.services.drive.model.Permission content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Permission | Permission |
| **enforceExpansiveAccess** | Whether the request should enforce expansive access rules | Boolean |
| **fileId** | The ID of the file or shared drive | String |
| **permissionId** | The ID of the permission | String |
| **removeExpiration** | Whether to remove the expiration date | Boolean |
| **supportsAllDrives** | Whether the requesting application supports both My Drives and shared drives | Boolean |
| **supportsTeamDrives** | Deprecated: Use supportsAllDrives instead | Boolean |
| **transferOwnership** | Whether to transfer ownership to the specified user and downgrade the current owner to a writer | Boolean |
| **useDomainAdminAccess** | Issue the request as a domain administrator | Boolean |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-replies

**Both producer and consumer are supported**

The drive-replies API is defined in the syntax as follows:

```none
google-drive:drive-replies/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_drive-replies_method_create) |  | Creates a reply to a comment |
| [**delete**](#_api_drive-replies_method_delete) |  | Deletes a reply |
| [**get**](#_api_drive-replies_method_get) |  | Gets a reply by ID |
| [**list**](#_api_drive-replies_method_list) |  | Lists a comment’s replies |
| [**update**](#_api_drive-replies_method_update) |  | Updates a reply with patch semantics |

#### Method create

Signatures:

-   com.google.api.services.drive.Drive.Replies.Create create(String fileId, String commentId, com.google.api.services.drive.model.Reply content);
    

The google-drive/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **content** | The com.google.api.services.drive.model.Reply | Reply |
| **fileId** | The ID of the file | String |

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
| **includeDeleted** | Whether to return deleted replies | Boolean |
| **replyId** | The ID of the reply | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Replies.List list(String fileId, String commentId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **fileId** | The ID of the file | String |
| **includeDeleted** | Whether to include deleted replies | Boolean |
| **pageSize** | The maximum number of replies to return per page | Integer |
| **pageToken** | The token for continuing a previous list request on the next page | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Replies.Update update(String fileId, String commentId, String replyId, com.google.api.services.drive.model.Reply content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The ID of the comment | String |
| **content** | The com.google.api.services.drive.model.Reply | Reply |
| **fileId** | The ID of the file | String |
| **replyId** | The ID of the reply | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-revisions

**Both producer and consumer are supported**

The drive-revisions API is defined in the syntax as follows:

```none
google-drive:drive-revisions/methodName?[parameters]
```

The 4 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_drive-revisions_method_delete) |  | Permanently deletes a file version |
| [**get**](#_api_drive-revisions_method_get) |  | Gets a revision’s metadata or content by ID |
| [**list**](#_api_drive-revisions_method_list) |  | Lists a file’s revisions |
| [**update**](#_api_drive-revisions_method_update) |  | Updates a revision with patch semantics |

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
| **acknowledgeAbuse** | Whether the user is acknowledging the risk of downloading known malware or other abusive files | Boolean |
| **fileId** | The ID of the file | String |
| **revisionId** | The ID of the revision | String |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Revisions.List list(String fileId);
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The ID of the file | String |
| **pageSize** | The maximum number of revisions to return per page | Integer |
| **pageToken** | The token for continuing a previous list request on the next page | String |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Revisions.Update update(String fileId, String revisionId, com.google.api.services.drive.model.Revision content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.Revision | Revision |
| **fileId** | The ID of the file | String |
| **revisionId** | The ID of the revision | String |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

### API: drive-teamdrives

**Both producer and consumer are supported**

The drive-teamdrives API is defined in the syntax as follows:

```none
google-drive:drive-teamdrives/methodName?[parameters]
```

The 5 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_drive-teamdrives_method_create) |  | Deprecated: Use drives |
| [**delete**](#_api_drive-teamdrives_method_delete) |  | Deprecated: Use drives |
| [**get**](#_api_drive-teamdrives_method_get) |  | Deprecated: Use drives |
| [**list**](#_api_drive-teamdrives_method_list) |  | Deprecated: Use drives |
| [**update**](#_api_drive-teamdrives_method_update) |  | Deprecated: Use drives |

#### Method create

Signatures:

-   com.google.api.services.drive.Drive.Teamdrives.Create create(String requestId, com.google.api.services.drive.model.TeamDrive content);
    

The google-drive/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.TeamDrive | TeamDrive |
| **requestId** | Required. An ID, such as a random UUID, which uniquely identifies this user’s request for idempotent creation of a Team Drive. A repeated request by the same user and with the same request ID will avoid creating duplicates by attempting to create the same Team Drive. If the Team Drive already exists a 409 error will be returned. | String |

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
| **useDomainAdminAccess** | Issue the request as a domain administrator; if set to true, then the requester will be granted access if they are an administrator of the domain to which the Team Drive belongs | Boolean |

#### Method list

Signatures:

-   com.google.api.services.drive.Drive.Teamdrives.List list();
    

The google-drive/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **pageSize** | Maximum number of Team Drives to return | Integer |
| **pageToken** | Page token for Team Drives | String |
| **q** | Query string for searching Team Drives | String |
| **useDomainAdminAccess** | Issue the request as a domain administrator; if set to true, then all Team Drives of the domain in which the requester is an administrator are returned | Boolean |

#### Method update

Signatures:

-   com.google.api.services.drive.Drive.Teamdrives.Update update(String teamDriveId, com.google.api.services.drive.model.TeamDrive content);
    

The google-drive/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.drive.model.TeamDrive | TeamDrive |
| **teamDriveId** | The ID of the Team Drive | String |
| **useDomainAdminAccess** | Issue the request as a domain administrator; if set to true, then the requester will be granted access if they are an administrator of the domain to which the Team Drive belongs | Boolean |

In addition to the parameters above, the google-drive API can also use any of the [Query Parameters (30 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleDrive.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleDrive.myParameterNameHere` header.

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

The component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-drive.access-token** | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **camel.component.google-drive.application-name** | Google drive application name. Example would be camel-google-drive/1.0. |  | String |
| **camel.component.google-drive.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-drive.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-drive.client-factory** | To use the GoogleCalendarClientFactory as factory for creating the client. Will by default use BatchGoogleDriveClientFactory. The option is a org.apache.camel.component.google.drive.GoogleDriveClientFactory type. |  | GoogleDriveClientFactory |
| **camel.component.google-drive.client-id** | Client ID of the drive application. |  | String |
| **camel.component.google-drive.client-secret** | Client secret of the drive application. |  | String |
| **camel.component.google-drive.configuration** | To use the shared configuration. The option is a org.apache.camel.component.google.drive.GoogleDriveConfiguration type. |  | GoogleDriveConfiguration |
| **camel.component.google-drive.delegate** | Delegate for wide-domain service account. |  | String |
| **camel.component.google-drive.enabled** | Whether to enable auto configuration of the google-drive component. This is enabled by default. |  | Boolean |
| **camel.component.google-drive.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-drive.proxy-host** | Proxy server host. |  | String |
| **camel.component.google-drive.proxy-port** | Proxy server port. |  | Integer |
| **camel.component.google-drive.refresh-token** | OAuth 2 refresh token. Using this, the Google Drive component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **camel.component.google-drive.scopes** | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **camel.component.google-drive.service-account-key** | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |