# Google Mail

**Since Camel 2.15**

**Both producer and consumer are supported**

The Google Mail component provides access to [Gmail](http://gmail.com/) via the [Google Mail Web APIs](https://developers.google.com/gmail/api/v1/reference/).

Google Mail uses the [OAuth 2.0 protocol](https://developers.google.com/accounts/docs/OAuth2) for authenticating a Google account and authorizing access to user data. Before you can use this component, you will need to [create an account and generate OAuth credentials](https://developers.google.com/gmail/api/auth/web-server). Credentials consist of a `clientId`, `clientSecret`, and a `refreshToken`. A handy resource for generating a long-lived `refreshToken` is the [OAuth playground](https://developers.google.com/oauthplayground).

In the case of a [service account](https://developers.google.com/identity/protocols/oauth2#serviceaccount), credentials consist of a JSON-file (serviceAccountKey). You can also use [delegation domain-wide authority](https://developers.google.com/identity/protocols/oauth2/service-account#delegatingauthority) (delegate) and one, several, or all possible [GMail API Auth Scopes](https://developers.google.com/gmail/api/auth/scopes).

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

google-mail://endpoint-prefix/endpoint?\[options\]

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

The Google Mail component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | Google mail application name. Example would be camel-google-mail/1.0. |  | String |
| **clientId** (common) | Client ID of the mail application. |  | String |
| **configuration** (common) | To use the shared configuration. |  | GoogleMailConfiguration |
| **delegate** (common) | Delegate for wide-domain service account. |  | String |
| **scopes** (common) | Specifies the level of permissions you want a calendar application to have to a user account. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes) for more info. Multiple scopes can be separated by comma. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **clientFactory** (advanced) | To use the GoogleCalendarClientFactory as factory for creating the client. Will by default use BatchGoogleMailClientFactory. |  | GoogleMailClientFactory |
| **accessToken** (security) | OAuth 2 access token. This typically expires after an hour so refreshToken is recommended for long term usage. |  | String |
| **clientSecret** (security) | Client secret of the mail application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Mail component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |

## Endpoint Options

The Google Mail endpoint is configured using URI syntax:

google-mail:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   THREADS
    
-   MESSAGES
    
-   ATTACHMENTS
    
-   LABELS
    
-   HISTORY
    
-   DRAFTS
    
-   USERS
    





 |  | GoogleMailApiName |
| **methodName** (common) | 

**Required** What sub operation to use for the selected operation.

Enum values:

-   attachments
    
-   create
    
-   delete
    
-   get
    
-   getProfile
    
-   gmailImport
    
-   insert
    
-   list
    
-   modify
    
-   patch
    
-   send
    
-   stop
    
-   trash
    
-   untrash
    
-   update
    
-   watch
    





 |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **applicationName** (common) | Google mail application name. Example would be camel-google-mail/1.0. |  | String |
| **clientId** (common) | Client ID of the mail application. |  | String |
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
| **clientSecret** (security) | Client secret of the mail application. |  | String |
| **refreshToken** (security) | OAuth 2 refresh token. Using this, the Google Mail component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | String |
| **serviceAccountKey** (security) | Service account key in json format to authenticate an application as a service account. Accept base64 adding the prefix base64:. |  | String |

## API Parameters (7 APIs)

The Google Mail endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

google-mail:apiName/methodName

There are 7 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**attachments**](#_api_attachments) | Both | The attachments collection of methods |
| [**drafts**](#_api_drafts) | Both | The drafts collection of methods |
| [**history**](#_api_history) | Both | The history collection of methods |
| [**labels**](#_api_labels) | Both | The labels collection of methods |
| [**messages**](#_api_messages) | Both | The messages collection of methods |
| [**threads**](#_api_threads) | Both | The threads collection of methods |
| [**users**](#_api_users) | Both | The users collection of methods |

Each API is documented in the following sections to come.

### API: attachments

**Both producer and consumer are supported**

The attachments API is defined in the syntax as follows:

```none
google-mail:attachments/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**get**](#_api_attachments_method_get) |  | Gets the specified message attachment |

#### Method get

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.Attachments.Get get(String userId, String messageId, String id);
    

The google-mail/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the attachment | String |
| **messageId** | The ID of the message containing the attachment | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

In addition to the parameters above, the google-mail API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleMail.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleMail.myParameterNameHere` header.

### API: drafts

**Both producer and consumer are supported**

The drafts API is defined in the syntax as follows:

```none
google-mail:drafts/methodName?[parameters]
```

The 6 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_drafts_method_create) |  | Creates a new draft with the DRAFT label |
| [**delete**](#_api_drafts_method_delete) |  | Immediately and permanently deletes the specified draft |
| [**get**](#_api_drafts_method_get) |  | Gets the specified draft |
| [**list**](#_api_drafts_method_list) |  | Lists the drafts in the user’s mailbox |
| [**send**](#_api_drafts_method_send) |  | Sends the specified, existing draft to the recipients in the To, Cc, and Bcc headers |
| [**update**](#_api_drafts_method_update) |  | Replaces a draft’s content |

#### Method create

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Drafts.Create create(String userId, com.google.api.services.gmail.model.Draft content);
    
-   com.google.api.services.gmail.Gmail.Users.Drafts.Create create(String userId, com.google.api.services.gmail.model.Draft content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-mail/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.Draft media metadata or null if none | Draft |
| **mediaContent** | The media HTTP content | AbstractInputStreamContent |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method delete

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Drafts.Delete delete(String userId, String id);
    

The google-mail/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the draft to delete | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method get

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Drafts.Get get(String userId, String id);
    

The google-mail/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **format** | The format to return the draft in | String |
| **id** | The ID of the draft to retrieve | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method list

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Drafts.List list(String userId);
    

The google-mail/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **includeSpamTrash** | Include drafts from SPAM and TRASH in the results | Boolean |
| **maxResults** | Maximum number of drafts to return | Long |
| **pageToken** | Page token to retrieve a specific page of results in the list | String |
| **q** | Only return draft messages matching the specified query | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method send

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Drafts.Send send(String userId, com.google.api.services.gmail.model.Draft content);
    
-   com.google.api.services.gmail.Gmail.Users.Drafts.Send send(String userId, com.google.api.services.gmail.model.Draft content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-mail/send API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.Draft media metadata or null if none | Draft |
| **mediaContent** | The media HTTP content | AbstractInputStreamContent |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method update

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Drafts.Update update(String userId, String id, com.google.api.services.gmail.model.Draft content);
    
-   com.google.api.services.gmail.Gmail.Users.Drafts.Update update(String userId, String id, com.google.api.services.gmail.model.Draft content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-mail/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.Draft media metadata or null if none | Draft |
| **id** | 
 | String |
| **mediaContent** | The media HTTP content | AbstractInputStreamContent |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

In addition to the parameters above, the google-mail API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleMail.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleMail.myParameterNameHere` header.

### API: history

**Both producer and consumer are supported**

The history API is defined in the syntax as follows:

```none
google-mail:history/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**list**](#_api_history_method_list) |  | Lists the history of all changes to the given mailbox |

#### Method list

Signatures:

-   com.google.api.services.gmail.Gmail.Users.History.List list(String userId);
    

The google-mail/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **historyTypes** | History types to be returned by the function | List |
| **labelId** | Only return messages with a label matching the ID | String |
| **maxResults** | Maximum number of history records to return | Long |
| **pageToken** | Page token to retrieve a specific page of results in the list | String |
| **startHistoryId** | Required | BigInteger |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

In addition to the parameters above, the google-mail API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleMail.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleMail.myParameterNameHere` header.

### API: labels

**Both producer and consumer are supported**

The labels API is defined in the syntax as follows:

```none
google-mail:labels/methodName?[parameters]
```

The 6 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**create**](#_api_labels_method_create) |  | Creates a new label |
| [**delete**](#_api_labels_method_delete) |  | Immediately and permanently deletes the specified label and removes it from any messages and threads that it is applied to |
| [**get**](#_api_labels_method_get) |  | Gets the specified label |
| [**list**](#_api_labels_method_list) |  | Lists all labels in the user’s mailbox |
| [**patch**](#_api_labels_method_patch) |  | Patch the specified label |
| [**update**](#_api_labels_method_update) |  | Updates the specified label |

#### Method create

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Labels.Create create(String userId, com.google.api.services.gmail.model.Label content);
    

The google-mail/create API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.Label | Label |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method delete

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Labels.Delete delete(String userId, String id);
    

The google-mail/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the label to delete | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method get

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Labels.Get get(String userId, String id);
    

The google-mail/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the label to retrieve | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method list

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Labels.List list(String userId);
    

The google-mail/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method patch

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Labels.Patch patch(String userId, String id, com.google.api.services.gmail.model.Label content);
    

The google-mail/patch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.Label | Label |
| **id** | The ID of the label to update | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method update

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Labels.Update update(String userId, String id, com.google.api.services.gmail.model.Label content);
    

The google-mail/update API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.Label | Label |
| **id** | The ID of the label to update | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

In addition to the parameters above, the google-mail API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleMail.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleMail.myParameterNameHere` header.

### API: messages

**Both producer and consumer are supported**

The messages API is defined in the syntax as follows:

```none
google-mail:messages/methodName?[parameters]
```

The 12 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**attachments**](#_api_messages_method_attachments) |  | An accessor for creating requests from the Attachments collection |
| [**batchDelete**](#_api_messages_method_batchDelete) |  | Deletes many messages by message ID |
| [**batchModify**](#_api_messages_method_batchModify) |  | Modifies the labels on the specified messages |
| [**delete**](#_api_messages_method_delete) |  | Immediately and permanently deletes the specified message |
| [**get**](#_api_messages_method_get) |  | Gets the specified message |
| [**gmailImport**](#_api_messages_method_gmailImport) |  | Imports a message into only this user’s mailbox, with standard email delivery scanning and classification similar to receiving via SMTP |
| [**insert**](#_api_messages_method_insert) |  | Directly inserts a message into only this user’s mailbox similar to IMAP APPEND, bypassing most scanning and classification |
| [**list**](#_api_messages_method_list) |  | Lists the messages in the user’s mailbox |
| [**modify**](#_api_messages_method_modify) |  | Modifies the labels on the specified message |
| [**send**](#_api_messages_method_send) |  | Sends the specified message to the recipients in the To, Cc, and Bcc headers |
| [**trash**](#_api_messages_method_trash) |  | Moves the specified message to the trash |
| [**untrash**](#_api_messages_method_untrash) |  | Removes the specified message from the trash |

#### Method attachments

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.Attachments attachments();
    

The google-mail/attachments API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method batchDelete

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.BatchDelete batchDelete(String userId, com.google.api.services.gmail.model.BatchDeleteMessagesRequest content);
    

The google-mail/batchDelete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **batchDeleteMessagesRequest** | The com.google.api.services.gmail.model.BatchDeleteMessagesRequest | BatchDeleteMessagesRequest |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method batchModify

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.BatchModify batchModify(String userId, com.google.api.services.gmail.model.BatchModifyMessagesRequest content);
    

The google-mail/batchModify API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **batchModifyMessagesRequest** | The com.google.api.services.gmail.model.BatchModifyMessagesRequest | BatchModifyMessagesRequest |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method delete

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.Delete delete(String userId, String id);
    

The google-mail/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the message to delete | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method get

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.Get get(String userId, String id);
    

The google-mail/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **format** | The format to return the message in | String |
| **id** | The ID of the message to retrieve. This ID is usually retrieved using messages.list. The ID is also contained in the result when a message is inserted (messages.insert) or imported (messages.import). | String |
| **metadataHeaders** | When given and format is METADATA, only include headers specified | List |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method gmailImport

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.GmailImport gmailImport(String userId, com.google.api.services.gmail.model.Message content);
    
-   com.google.api.services.gmail.Gmail.Users.Messages.GmailImport gmailImport(String userId, com.google.api.services.gmail.model.Message content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-mail/gmailImport API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.Message media metadata or null if none | Message |
| **deleted** | Mark the email as permanently deleted (not TRASH) and only visible in Google Vault to a Vault administrator | Boolean |
| **internalDateSource** | Source for Gmail’s internal date of the message | String |
| **mediaContent** | The media HTTP content | AbstractInputStreamContent |
| **neverMarkSpam** | Ignore the Gmail spam classifier decision and never mark this email as SPAM in the mailbox | Boolean |
| **processForCalendar** | Process calendar invites in the email and add any extracted meetings to the Google Calendar for this user | Boolean |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method insert

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.Insert insert(String userId, com.google.api.services.gmail.model.Message content);
    
-   com.google.api.services.gmail.Gmail.Users.Messages.Insert insert(String userId, com.google.api.services.gmail.model.Message content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-mail/insert API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.Message media metadata or null if none | Message |
| **deleted** | Mark the email as permanently deleted (not TRASH) and only visible in Google Vault to a Vault administrator | Boolean |
| **internalDateSource** | Source for Gmail’s internal date of the message | String |
| **mediaContent** | The media HTTP content | AbstractInputStreamContent |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method list

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.List list(String userId);
    

The google-mail/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **includeSpamTrash** | Include messages from SPAM and TRASH in the results | Boolean |
| **labelIds** | Only return messages with labels that match all of the specified label IDs | List |
| **maxResults** | Maximum number of messages to return | Long |
| **pageToken** | Page token to retrieve a specific page of results in the list | String |
| **q** | Only return messages matching the specified query | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method modify

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.Modify modify(String userId, String id, com.google.api.services.gmail.model.ModifyMessageRequest content);
    

The google-mail/modify API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the message to modify | String |
| **modifyMessageRequest** | The com.google.api.services.gmail.model.ModifyMessageRequest | ModifyMessageRequest |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method send

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.Send send(String userId, com.google.api.services.gmail.model.Message content);
    
-   com.google.api.services.gmail.Gmail.Users.Messages.Send send(String userId, com.google.api.services.gmail.model.Message content, com.google.api.client.http.AbstractInputStreamContent mediaContent);
    

The google-mail/send API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.Message media metadata or null if none | Message |
| **mediaContent** | The media HTTP content | AbstractInputStreamContent |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method trash

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.Trash trash(String userId, String id);
    

The google-mail/trash API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the message to Trash | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method untrash

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Messages.Untrash untrash(String userId, String id);
    

The google-mail/untrash API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the message to remove from Trash | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

In addition to the parameters above, the google-mail API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleMail.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleMail.myParameterNameHere` header.

### API: threads

**Both producer and consumer are supported**

The threads API is defined in the syntax as follows:

```none
google-mail:threads/methodName?[parameters]
```

The 6 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**delete**](#_api_threads_method_delete) |  | Immediately and permanently deletes the specified thread |
| [**get**](#_api_threads_method_get) |  | Gets the specified thread |
| [**list**](#_api_threads_method_list) |  | Lists the threads in the user’s mailbox |
| [**modify**](#_api_threads_method_modify) |  | Modifies the labels applied to the thread |
| [**trash**](#_api_threads_method_trash) |  | Moves the specified thread to the trash |
| [**untrash**](#_api_threads_method_untrash) |  | Removes the specified thread from the trash |

#### Method delete

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Threads.Delete delete(String userId, String id);
    

The google-mail/delete API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | ID of the Thread to delete | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method get

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Threads.Get get(String userId, String id);
    

The google-mail/get API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **format** | The format to return the messages in | String |
| **id** | The ID of the thread to retrieve | String |
| **metadataHeaders** | When given and format is METADATA, only include headers specified | List |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method list

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Threads.List list(String userId);
    

The google-mail/list API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **includeSpamTrash** | Include threads from SPAM and TRASH in the results | Boolean |
| **labelIds** | Only return threads with labels that match all of the specified label IDs | List |
| **maxResults** | Maximum number of threads to return | Long |
| **pageToken** | Page token to retrieve a specific page of results in the list | String |
| **q** | Only return threads matching the specified query | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method modify

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Threads.Modify modify(String userId, String id, com.google.api.services.gmail.model.ModifyThreadRequest content);
    

The google-mail/modify API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.ModifyThreadRequest | ModifyThreadRequest |
| **id** | The ID of the thread to modify | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method trash

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Threads.Trash trash(String userId, String id);
    

The google-mail/trash API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the thread to Trash | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method untrash

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Threads.Untrash untrash(String userId, String id);
    

The google-mail/untrash API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **id** | The ID of the thread to remove from Trash | String |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

In addition to the parameters above, the google-mail API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleMail.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleMail.myParameterNameHere` header.

### API: users

**Both producer and consumer are supported**

The users API is defined in the syntax as follows:

```none
google-mail:users/methodName?[parameters]
```

The 3 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**getProfile**](#_api_users_method_getProfile) |  | Gets the current user’s Gmail profile |
| [**stop**](#_api_users_method_stop) |  | Stop receiving push notifications for the given user mailbox |
| [**watch**](#_api_users_method_watch) |  | Set up or update a push notification watch on the given user mailbox |

#### Method getProfile

Signatures:

-   com.google.api.services.gmail.Gmail.Users.GetProfile getProfile(String userId);
    

The google-mail/getProfile API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method stop

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Stop stop(String userId);
    

The google-mail/stop API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

#### Method watch

Signatures:

-   com.google.api.services.gmail.Gmail.Users.Watch watch(String userId, com.google.api.services.gmail.model.WatchRequest content);
    

The google-mail/watch API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **content** | The com.google.api.services.gmail.model.WatchRequest | WatchRequest |
| **userId** | The user’s email address. The special value me can be used to indicate the authenticated user. default: me | String |

In addition to the parameters above, the google-mail API can also use any of the [Query Parameters](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelGoogleMail.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelGoogleMail.myParameterNameHere` header.

> **Note**
> This is an API-based component, so per-call parameters can be supplied through `Camel`\-prefixed exchange headers in addition to the endpoint options. If the route consumes messages from untrusted producers, strip these internal headers at the trust boundary — for example with `removeHeaders("Camel*")` — before the message reaches this component, so that a sender cannot override the API call. See [the Camel security model](../../manual/security-model.md) for details.

## Data Type Transformer: update-message-labels

The `google-mail:update-message-labels` data type transformer builds a `ModifyMessageRequest` from exchange variables, resolving label names to Gmail label IDs automatically.

This is useful for modifying Gmail message labels (categorizing, archiving, starring, moving, etc.) without manually calling the labels/list API.

### Exchange Variables

  
| Variable | Type | Description |
| --- | --- | --- |
| `addLabels` | `String` (comma-separated) or `List<String>` | Label names to add to the message. |
| `removeLabels` | `String` (comma-separated) or `List<String>` | Label names to remove from the message. |

At least one of the two variables must be set.

Both system labels (INBOX, UNREAD, STARRED, SPAM, TRASH, IMPORTANT, etc.) and custom user-defined labels are resolved via the Gmail labels/list API.

### Examples

-   Java
    
-   YAML
    
-   XML
    

```java
from("google-mail-stream:0")
    .setVariable("addLabels", constant("Work"))
    .setVariable("removeLabels", constant("INBOX,UNREAD"))
    .transformDataType(new DataType("google-mail:update-message-labels"))
    .to("google-mail:messages/modify");
```

```yaml
- route:
    from:
      uri: "google-mail-stream:0"
    steps:
      - setVariable:
          name: addLabels
          constant: "Work"
      - setVariable:
          name: removeLabels
          constant: "INBOX,UNREAD"
      - transformDataType:
          toType: "google-mail:update-message-labels"
      - to:
          uri: "google-mail:messages/modify"
```

```xml
<route>
    <from uri="google-mail-stream:0"/>
    <setVariable name="addLabels">
        <constant>Work</constant>
    </setVariable>
    <setVariable name="removeLabels">
        <constant>INBOX,UNREAD</constant>
    </setVariable>
    <transformDataType toType="google-mail:update-message-labels"/>
    <to uri="google-mail:messages/modify"/>
</route>
```

## Data Type Transformer: draft

The `google-mail:draft` transformer converts a String body into a Gmail `Draft` using mail headers from the exchange.

It works with `google-mail-stream`, which sets headers like `threadId`, `messageId`, `from`, `to`, `cc`, `bcc`, and `subject` automatically when consuming messages. You can also set these headers manually to create drafts from scratch.

### Headers

The transformer reads the following headers:

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelGoogleMailStreamThreadId` | `String` | Thread ID for the conversation (optional, used for replies) |
| `CamelGoogleMailStreamMessageId` | `String` | Message ID to reply to (optional, sets In-Reply-To and References headers) |
| `CamelGoogleMailStreamFrom` | `String` | From address (optional) |
| `CamelGoogleMailStreamTo` | `String` | To address (optional) |
| `CamelGoogleMailStreamCc` | `String` | CC address (optional) |
| `CamelGoogleMailStreamBcc` | `String` | BCC address (optional) |
| `CamelGoogleMailStreamSubject` | `String` | Email subject (optional) |

All headers are optional.

### Message Body

The message body is a `String` with the email content (plain text or HTML).

Content type defaults to `text/plain; charset=UTF-8`. For HTML, set `Exchange.CONTENT_TYPE` to `text/html; charset=UTF-8`.

The transformer:

-   Builds an RFC 2822 MIME message and encodes it as Base64 URL-safe (required by Gmail API)
    
-   Sets `In-Reply-To` and `References` headers when `messageId` is present
    
-   Associates the draft with the correct thread when `threadId` is present
    

### Examples

-   Java
    
-   YAML
    
-   XML
    

```java
// Create a draft reply from a received message
from("google-mail-stream:0")
    .setBody(constant("Thank you for your message. I will respond soon."))
    .transformDataType(new DataType("google-mail:draft"))
    .to("google-mail:drafts/create?inBody=content");

// Create a new draft (no threading)
from("direct:newDraft")
    .setBody(constant("This is a new draft message"))
    .setHeader("CamelGoogleMailStreamFrom", constant("sender@example.com"))
    .setHeader("CamelGoogleMailStreamTo", constant("recipient@example.com"))
    .setHeader("CamelGoogleMailStreamSubject", constant("New Draft"))
    .transformDataType(new DataType("google-mail:draft"))
    .to("google-mail:drafts/create?inBody=content");
```

```yaml
# Create a draft reply from a received message
- route:
    from:
      uri: "google-mail-stream:0"
    steps:
      - setBody:
          constant: "Thank you for your message. I will respond soon."
      - transformDataType:
          toType: "google-mail:draft"
      - to:
          uri: "google-mail:drafts/create"
          parameters:
            inBody: content

# Create a new draft (no threading)
- route:
    from:
      uri: "direct:newDraft"
    steps:
      - setBody:
          constant: "This is a new draft message"
      - setHeader:
          name: CamelGoogleMailStreamFrom
          constant: "sender@example.com"
      - setHeader:
          name: CamelGoogleMailStreamTo
          constant: "recipient@example.com"
      - setHeader:
          name: CamelGoogleMailStreamSubject
          constant: "New Draft"
      - transformDataType:
          toType: "google-mail:draft"
      - to:
          uri: "google-mail:drafts/create"
          parameters:
            inBody: content
```

```xml
<!-- Create a draft reply from a received message -->
<route>
    <from uri="google-mail-stream:0"/>
    <setBody>
        <constant>Thank you for your message. I will respond soon.</constant>
    </setBody>
    <transformDataType toType="google-mail:draft"/>
    <to uri="google-mail:drafts/create?inBody=content"/>
</route>

<!-- Create a new draft (no threading) -->
<route>
    <from uri="direct:newDraft"/>
    <setBody>
        <constant>This is a new draft message</constant>
    </setBody>
    <setHeader name="CamelGoogleMailStreamFrom">
        <constant>sender@example.com</constant>
    </setHeader>
    <setHeader name="CamelGoogleMailStreamTo">
        <constant>recipient@example.com</constant>
    </setHeader>
    <setHeader name="CamelGoogleMailStreamSubject">
        <constant>New Draft</constant>
    </setHeader>
    <transformDataType toType="google-mail:draft"/>
    <to uri="google-mail:drafts/create?inBody=content"/>
</route>
```

## More Information

For more information on the endpoints and options see API documentation at: [https://developers.google.com/gmail/api/v1/reference/](https://developers.google.com/gmail/api/v1/reference/)