# Box

**Since Camel 2.14**

**Both producer and consumer are supported**

The Box component provides access to all the Box.com APIs accessible using [Box Java SDK](https://github.com/box/box-java-sdk/). It allows producing messages to upload and download files, create, edit, and manage folders, etc. It also supports APIs that allow polling for updates to user accounts and even changes to enterprise accounts, etc.

Box.com requires the use of OAuth2.0 for all client application authentications. To use camel-box with your account, you’ll need to create a new application within Box.com at [https://developer.box.com](https://developer.box.com/). The Box application’s client id and secret will allow access to Box APIs which require a current user. A user access token is generated and managed by the API for an end user.

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-box</artifactId>
    <version>${camel-version}</version>
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

The Box component supports 19 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | Box application client ID. |  | String |
| **configuration** (common) | To use the shared configuration. |  | BoxConfiguration |
| **enterpriseId** (common) | The enterprise ID to use for an App Enterprise. |  | String |
| **userId** (common) | The user ID to use for an App User. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **httpParams** (advanced) | Custom HTTP params for settings like proxy host. |  | Map |
| **authenticationType** (authentication) | The type of authentication for connection. Types of Authentication: STANDARD\_AUTHENTICATION - OAuth 2.0 (3-legged) SERVER\_AUTHENTICATION - OAuth 2.0 with JSON Web Tokens. | APP\_USER\_AUTHENTICATION | String |
| **accessTokenCache** (security) | Custom Access Token Cache for storing and retrieving access tokens. |  | IAccessTokenCache |
| **clientSecret** (security) | Box application client secret. |  | String |
| **encryptionAlgorithm** (security) | 
The type of encryption algorithm for JWT. Supported Algorithms: RSA\_SHA\_256 RSA\_SHA\_384 RSA\_SHA\_512.

Enum values:

-   RSA\_SHA\_256
    
-   RSA\_SHA\_384
    
-   RSA\_SHA\_512
    





 | RSA\_SHA\_256 | EncryptionAlgorithm |
| **maxCacheEntries** (security) | The maximum number of access tokens in cache. | 100 | int |
| **privateKeyFile** (security) | The private key for generating the JWT signature. |  | String |
| **privateKeyPassword** (security) | The password for the private key. |  | String |
| **publicKeyId** (security) | The ID for public key for validating the JWT signature. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **userName** (security) | Box user name, MUST be provided. |  | String |
| **userPassword** (security) | Box user password, MUST be provided if authSecureStorage is not set, or returns null on first call. |  | String |

## Endpoint Options

The Box endpoint is configured using URI syntax:

box:apiName/methodName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiName** (common) | 
**Required** What kind of operation to perform.

Enum values:

-   COLLABORATIONS
    
-   COMMENTS
    
-   EVENT\_LOGS
    
-   FILES
    
-   FOLDERS
    
-   GROUPS
    
-   EVENTS
    
-   SEARCH
    
-   TASKS
    
-   USERS
    





 |  | BoxApiName |
| **methodName** (common) | **Required** What sub operation to use for the selected operation. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientId** (common) | Box application client ID. |  | String |
| **enterpriseId** (common) | The enterprise ID to use for an App Enterprise. |  | String |
| **inBody** (common) | Sets the name of a parameter to be passed in the exchange In Body. |  | String |
| **userId** (common) | The user ID to use for an App User. |  | String |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **httpParams** (advanced) | Custom HTTP params for settings like proxy host. |  | Map |
| **authenticationType** (authentication) | The type of authentication for connection. Types of Authentication: STANDARD\_AUTHENTICATION - OAuth 2.0 (3-legged) SERVER\_AUTHENTICATION - OAuth 2.0 with JSON Web Tokens. | APP\_USER\_AUTHENTICATION | String |
| **accessTokenCache** (security) | Custom Access Token Cache for storing and retrieving access tokens. |  | IAccessTokenCache |
| **clientSecret** (security) | Box application client secret. |  | String |
| **encryptionAlgorithm** (security) | 

The type of encryption algorithm for JWT. Supported Algorithms: RSA\_SHA\_256 RSA\_SHA\_384 RSA\_SHA\_512.

Enum values:

-   RSA\_SHA\_256
    
-   RSA\_SHA\_384
    
-   RSA\_SHA\_512
    





 | RSA\_SHA\_256 | EncryptionAlgorithm |
| **maxCacheEntries** (security) | The maximum number of access tokens in cache. | 100 | int |
| **privateKeyFile** (security) | The private key for generating the JWT signature. |  | String |
| **privateKeyPassword** (security) | The password for the private key. |  | String |
| **publicKeyId** (security) | The ID for public key for validating the JWT signature. |  | String |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |
| **userName** (security) | Box user name, MUST be provided. |  | String |
| **userPassword** (security) | Box user password, MUST be provided if authSecureStorage is not set, or returns null on first call. |  | String |

## API Parameters (10 APIs)

The Box endpoint is an API-based component and has additional parameters based on which API name and API method is used. The API name and API method is located in the endpoint URI as the `apiName/methodName` path parameters:

box:apiName/methodName

There are 10 API names as listed in the table below:

  
| API Name | Type | Description |
| --- | --- | --- |
| [**collaborations**](#_api_collaborations) | Producer | Provides operations to manage Box collaborations |
| [**comments**](#_api_comments) | Producer | Provides operations to manage Box comments |
| [**event-logs**](#_api_event-logs) | Producer | Provides operations to read Box enterprise (admin) event logs |
| [**events**](#_api_events) | Consumer | Provides operations to manage Box events |
| [**files**](#_api_files) | Producer | Provides operations to manage Box files |
| [**folders**](#_api_folders) | Producer | Provides operations to manage Box folders |
| [**groups**](#_api_groups) | Producer | Provides operations to manage Box groups |
| [**search**](#_api_search) | Producer | Provides operations to manage Box searches |
| [**tasks**](#_api_tasks) | Producer | Provides operations to manage Box tasks |
| [**users**](#_api_users) | Producer | Provides operations to manage Box users |

Each API is documented in the following sections to come.

### API: collaborations

**Only producer is supported**

The collaborations API is defined in the syntax as follows:

```none
box:collaborations/methodName?[parameters]
```

The 7 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**addFolderCollaboration**](#_api_collaborations_method_addFolderCollaboration) | add | Add a collaboration to this folder |
| [**addFolderCollaborationByEmail**](#_api_collaborations_method_addFolderCollaborationByEmail) | add | Add a collaboration to this folder |
| [**deleteCollaboration**](#_api_collaborations_method_deleteCollaboration) | delete | Delete collaboration |
| [**getCollaborationInfo**](#_api_collaborations_method_getCollaborationInfo) | info | Get collaboration information |
| [**getFolderCollaborations**](#_api_collaborations_method_getFolderCollaborations) | collaborations | Get information about all of the collaborations for folder |
| [**getPendingCollaborations**](#_api_collaborations_method_getPendingCollaborations) | pendingCollaborations | Get all pending collaboration invites for the current user |
| [**updateCollaborationInfo**](#_api_collaborations_method_updateCollaborationInfo) | updateInfo | Update collaboration information |

#### Method addFolderCollaboration

Signatures:

-   com.box.sdk.BoxCollaboration addFolderCollaboration(String folderId, com.box.sdk.BoxCollaborator collaborator, com.box.sdk.BoxCollaboration.Role role);
    

The box/addFolderCollaboration API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **collaborator** | The collaborator to add | BoxCollaborator |
| **folderId** | The id of folder to add collaboration to | String |
| **role** | The role of the collaborator | Role |

#### Method addFolderCollaborationByEmail

Signatures:

-   com.box.sdk.BoxCollaboration addFolderCollaborationByEmail(String folderId, String email, com.box.sdk.BoxCollaboration.Role role);
    

The box/addFolderCollaborationByEmail API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **email** | The email address of the collaborator to add | String |
| **folderId** | The id of folder to add collaboration to | String |
| **role** | The role of the collaborator | Role |

#### Method deleteCollaboration

Signatures:

-   void deleteCollaboration(String collaborationId);
    

The box/deleteCollaboration API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **collaborationId** | The id of comment to change | String |

#### Method getCollaborationInfo

Signatures:

-   com.box.sdk.BoxCollaboration.Info getCollaborationInfo(String collaborationId);
    

The box/getCollaborationInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **collaborationId** | The id of collaboration | String |

#### Method getFolderCollaborations

Signatures:

-   java.util.Collection<com.box.sdk.BoxCollaboration.Info> getFolderCollaborations(String folderId);
    

The box/getFolderCollaborations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **folderId** | The id of folder to get collaborations information on | String |

#### Method getPendingCollaborations

Signatures:

-   java.util.Collection<com.box.sdk.BoxCollaboration.Info> getPendingCollaborations();
    

The box/getPendingCollaborations API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method updateCollaborationInfo

Signatures:

-   com.box.sdk.BoxCollaboration updateCollaborationInfo(String collaborationId, com.box.sdk.BoxCollaboration.Info info);
    

The box/updateCollaborationInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **collaborationId** | The id of collaboration | String |
| **info** | Collaboration information to update | Info |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

### API: comments

**Only producer is supported**

The comments API is defined in the syntax as follows:

```none
box:comments/methodName?[parameters]
```

The 6 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**addFileComment**](#_api_comments_method_addFileComment) | add | Add comment to file |
| [**changeCommentMessage**](#_api_comments_method_changeCommentMessage) | updateMessage | Change comment message |
| [**deleteComment**](#_api_comments_method_deleteComment) | delete | Delete comment |
| [**getCommentInfo**](#_api_comments_method_getCommentInfo) | info | Get comment information |
| [**getFileComments**](#_api_comments_method_getFileComments) | comments | Get a list of any comments on this file |
| [**replyToComment**](#_api_comments_method_replyToComment) | reply | Reply to a comment |

#### Method addFileComment

Signatures:

-   com.box.sdk.BoxFile addFileComment(String fileId, String message);
    

The box/addFileComment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file | String |
| **message** | The comment’s message | String |

#### Method changeCommentMessage

Signatures:

-   com.box.sdk.BoxComment changeCommentMessage(String commentId, String message);
    

The box/changeCommentMessage API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The id of comment to change | String |
| **message** | The new message for the comment | String |

#### Method deleteComment

Signatures:

-   void deleteComment(String commentId);
    

The box/deleteComment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The id of comment to delete | String |

#### Method getCommentInfo

Signatures:

-   com.box.sdk.BoxComment.Info getCommentInfo(String commentId);
    

The box/getCommentInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The id of comment | String |

#### Method getFileComments

Signatures:

-   java.util.List<com.box.sdk.BoxComment.Info> getFileComments(String fileId);
    

The box/getFileComments API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file | String |

#### Method replyToComment

Signatures:

-   com.box.sdk.BoxComment replyToComment(String commentId, String message);
    

The box/replyToComment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **commentId** | The id of comment to reply to | String |
| **message** | The message for the reply | String |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

### API: event-logs

**Only producer is supported**

The event-logs API is defined in the syntax as follows:

```none
box:event-logs/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**getEnterpriseEvents**](#_api_event-logs_method_getEnterpriseEvents) | events | Create an event stream with optional starting initial position and add listener that will be notified when an event is received |

#### Method getEnterpriseEvents

Signatures:

-   java.util.List<com.box.sdk.BoxEvent> getEnterpriseEvents(String position, java.util.Date after, java.util.Date before, com.box.sdk.BoxEvent.EventType\[\] types);
    

The box/getEnterpriseEvents API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **after** | The lower bound on the timestamp of the events returned | Date |
| **before** | The upper bound on the timestamp of the events returned | Date |
| **position** | The starting position of the event stream. May be null in which case all events within bounds returned. | String |
| **types** | An optional list of event types to filter by | EventType\[\] |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

### API: events

**Only consumer is supported**

The events API is defined in the syntax as follows:

```none
box:events/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**listen**](#_api_events_method_listen) |  | Create an event stream with optional starting initial position and add listener that will be notified when an event is received |

#### Method listen

Signatures:

-   void listen(com.box.sdk.EventListener listener, Long startingPosition);
    

The box/listen API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **startingPosition** | The starting position of the event stream | Long |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

### API: files

**Only producer is supported**

The files API is defined in the syntax as follows:

```none
box:files/methodName?[parameters]
```

The 21 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**checkUpload**](#_api_files_method_checkUpload) | canUpload | Does a pre-verification before upload, to check if the filename already exists or if there is permission to upload |
| [**copyFile**](#_api_files_method_copyFile) | copy | Copy file to destination folder while optionally giving it a new name |
| [**createFileMetadata**](#_api_files_method_createFileMetadata) | createMetadata | Create metadata for file in either the global properties template or the specified template type |
| [**createFileSharedLink**](#_api_files_method_createFileSharedLink) | link | Create a shared link to file |
| [**deleteFile**](#_api_files_method_deleteFile) | delete | Delete the file |
| [**deleteFileMetadata**](#_api_files_method_deleteFileMetadata) | delete | Delete the file properties metadata |
| [**deleteFileVersion**](#_api_files_method_deleteFileVersion) | delete | Delete a file version |
| [**downloadFile**](#_api_files_method_downloadFile) | download | Download a file |
| [**downloadPreviousFileVersion**](#_api_files_method_downloadPreviousFileVersion) | downloadVersion | Download a previous version of file |
| [**getDownloadURL**](#_api_files_method_getDownloadURL) | url | Get an expiring URL for downloading a file directly from Box |
| [**getFileInfo**](#_api_files_method_getFileInfo) | info | Get file information |
| [**getFileMetadata**](#_api_files_method_getFileMetadata) | metadata | Gets the file properties metadata |
| [**getFilePreviewLink**](#_api_files_method_getFilePreviewLink) |  | Get an expiring URL for creating an embedded preview session |
| [**getFileVersions**](#_api_files_method_getFileVersions) | versions | Get any previous versions of file |
| [**moveFile**](#_api_files_method_moveFile) | move | Move file to destination folder while optionally giving it a new name |
| [**promoteFileVersion**](#_api_files_method_promoteFileVersion) | promoteVersion | Promote a previous version of file |
| [**renameFile**](#_api_files_method_renameFile) | rename | Rename file giving it the name newName |
| [**updateFileInfo**](#_api_files_method_updateFileInfo) | updateInfo | Update file information |
| [**updateFileMetadata**](#_api_files_method_updateFileMetadata) | updateMetadata | Update the file properties metadata |
| [**uploadFile**](#_api_files_method_uploadFile) | upload | Upload a new file to parent folder |
| [**uploadNewFileVersion**](#_api_files_method_uploadNewFileVersion) | uploadVersion | Upload a new version of file |

#### Method checkUpload

Signatures:

-   void checkUpload(String fileName, String parentFolderId, Long size);
    

The box/checkUpload API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileName** | The name to give the uploaded file | String |
| **parentFolderId** | The id of parent folder | String |
| **size** | The size of the file’s content used for monitoring the upload’s progress | Long |

#### Method copyFile

Signatures:

-   com.box.sdk.BoxFile copyFile(String fileId, String destinationFolderId, String newName);
    

The box/copyFile API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **destinationFolderId** | The id of the destination folder | String |
| **fileId** | The id of file to copy | String |
| **newName** | The new name for copied file; if newName is null, the copied file has same name as the original. | String |

#### Method createFileMetadata

Signatures:

-   com.box.sdk.Metadata createFileMetadata(String fileId, com.box.sdk.Metadata metadata, String typeName);
    

The box/createFileMetadata API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of the file to create metadata for | String |
| **metadata** | The new metadata values | Metadata |
| **typeName** | The metadata template type name; if null the global properties template type is used. | String |

#### Method createFileSharedLink

Signatures:

-   com.box.sdk.BoxSharedLink createFileSharedLink(String fileId, com.box.sdk.BoxSharedLink.Access access, java.util.Date unshareDate, com.box.sdk.BoxSharedLink.Permissions permissions);
    

The box/createFileSharedLink API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **access** | The access level of the shared link | Access |
| **fileId** | The id of the file to create shared link on | String |
| **permissions** | The permissions of the created link; if permissions is null then the created shared link is created with default permissions. | Permissions |
| **unshareDate** | The date and time at which time the created shared link will expire; if unsharedDate is null then a non-expiring link is created. | Date |

#### Method deleteFile

Signatures:

-   void deleteFile(String fileId);
    

The box/deleteFile API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file to delete | String |

#### Method deleteFileMetadata

Signatures:

-   void deleteFileMetadata(String fileId);
    

The box/deleteFileMetadata API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file to delete | String |

#### Method deleteFileVersion

Signatures:

-   void deleteFileVersion(String fileId, Integer version);
    

The box/deleteFileVersion API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file with version to delete | String |
| **version** | The version of file to delete; initial version of file has value of 0, second version of file is 1 and so on. | Integer |

#### Method downloadFile

Signatures:

-   java.io.OutputStream downloadFile(String fileId, java.io.OutputStream output, Long rangeStart, Long rangeEnd, com.box.sdk.ProgressListener listener);
    

The box/downloadFile API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file | String |
| **listener** | A listener for monitoring the download’s progress; if null the download’s progress will not be monitored. | ProgressListener |
| **output** | The stream to which the file contents will be written | OutputStream |
| **rangeEnd** | The byte offset in file at which to stop the download; if null the entire contents of file will be downloaded. | Long |
| **rangeStart** | The byte offset in file at which to start the download; if null the entire contents of file will be downloaded. | Long |

#### Method downloadPreviousFileVersion

Signatures:

-   java.io.OutputStream downloadPreviousFileVersion(String fileId, Integer version, java.io.OutputStream output, com.box.sdk.ProgressListener listener);
    

The box/downloadPreviousFileVersion API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file | String |
| **listener** | A listener for monitoring the download’s progress; if null the download’s progress will not be monitored. | ProgressListener |
| **output** | The stream to which the version contents will be written | OutputStream |
| **version** | The version of file to download; initial version of file has value of 0, second version of file is 1 and so on. | Integer |

#### Method getDownloadURL

Signatures:

-   java.net.URL getDownloadURL(String fileId);
    

The box/getDownloadURL API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file | String |

#### Method getFileInfo

Signatures:

-   com.box.sdk.BoxFile.Info getFileInfo(String fileId, String\[\] fields);
    

The box/getFileInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fields** | The information fields to retrieve; if null all information fields are retrieved. | String\[\] |
| **fileId** | The id of file | String |

#### Method getFileMetadata

Signatures:

-   com.box.sdk.Metadata getFileMetadata(String fileId, String typeName);
    

The box/getFileMetadata API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of the file to retrieve metadata for | String |
| **typeName** | The metadata template type name; if null the global properties template type is used. | String |

#### Method getFilePreviewLink

Signatures:

-   java.net.URL getFilePreviewLink(String fileId);
    

The box/getFilePreviewLink API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of the file to get preview link on | String |

#### Method getFileVersions

Signatures:

-   java.util.Collection<com.box.sdk.BoxFileVersion> getFileVersions(String fileId);
    

The box/getFileVersions API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file | String |

#### Method moveFile

Signatures:

-   com.box.sdk.BoxFile moveFile(String fileId, String destinationFolderId, String newName);
    

The box/moveFile API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **destinationFolderId** | The id of the destination folder | String |
| **fileId** | The id of file to move | String |
| **newName** | The new name of moved file; if newName is null, the moved file has same name as the original. | String |

#### Method promoteFileVersion

Signatures:

-   com.box.sdk.BoxFileVersion promoteFileVersion(String fileId, Integer version);
    

The box/promoteFileVersion API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file | String |
| **version** | The version of file to promote; initial version of file has value of 0, second version of file is 1 and so on. | Integer |

#### Method renameFile

Signatures:

-   com.box.sdk.BoxFile renameFile(String fileId, String newFileName);
    

The box/renameFile API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file to rename | String |
| **newFileName** | The new name of file | String |

#### Method updateFileInfo

Signatures:

-   com.box.sdk.BoxFile updateFileInfo(String fileId, com.box.sdk.BoxFile.Info info);
    

The box/updateFileInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file to update | String |
| **info** | The updated information | Info |

#### Method updateFileMetadata

Signatures:

-   com.box.sdk.Metadata updateFileMetadata(String fileId, com.box.sdk.Metadata metadata);
    

The box/updateFileMetadata API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file to delete | String |
| **metadata** | The new metadata values | Metadata |

#### Method uploadFile

Signatures:

-   com.box.sdk.BoxFile uploadFile(String parentFolderId, java.io.InputStream content, String fileName, java.util.Date created, java.util.Date modified, Long size, Boolean check, com.box.sdk.ProgressListener listener);
    

The box/uploadFile API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **check** | If the file name is already used, call the uploadNewVersion instead. | Boolean |
| **content** | A stream containing contents of the file to upload | InputStream |
| **created** | The content created date that will be given to the uploaded file | Date |
| **fileName** | The name to give the uploaded file | String |
| **listener** | A listener for monitoring the upload’s progress | ProgressListener |
| **modified** | The content modified date that will be given to the uploaded file | Date |
| **parentFolderId** | The id of parent folder | String |
| **size** | The size of the file’s content used for monitoring the upload’s progress | Long |

#### Method uploadNewFileVersion

Signatures:

-   com.box.sdk.BoxFile uploadNewFileVersion(String fileId, java.io.InputStream fileContent, java.util.Date modified, Long fileSize, com.box.sdk.ProgressListener listener);
    

The box/uploadNewFileVersion API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileContent** | A stream containing contents of the file to upload | InputStream |
| **fileId** | The id of file | String |
| **fileSize** | The size of the file’s content used for monitoring the upload’s progress | Long |
| **listener** | A listener for monitoring the upload’s progress | ProgressListener |
| **modified** | The content modified date that will be given to the uploaded file | Date |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

### API: folders

**Only producer is supported**

The folders API is defined in the syntax as follows:

```none
box:folders/methodName?[parameters]
```

The 11 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**copyFolder**](#_api_folders_method_copyFolder) | copy | Copy folder to destination folder while optionally giving it a new name |
| [**createFolder**](#_api_folders_method_createFolder) | create | Create a folder specified by path from parent folder with given parentFolderId, creating intermediate directories as required |
| [**createFolderSharedLink**](#_api_folders_method_createFolderSharedLink) | create | Create a shared link to folder |
| [**deleteFolder**](#_api_folders_method_deleteFolder) | delete | Delete folder |
| [**getFolder**](#_api_folders_method_getFolder) | folder | Return the Box folder referenced by path |
| [**getFolderInfo**](#_api_folders_method_getFolderInfo) | folder | Get folder information |
| [**getFolderItems**](#_api_folders_method_getFolderItems) | folder | Returns a specific range of child items in folder and specifies which fields of each item to retrieve |
| [**getRootFolder**](#_api_folders_method_getRootFolder) | root | Return the root folder of authenticated user |
| [**moveFolder**](#_api_folders_method_moveFolder) | move | Move folder to destination folder while optionally giving it a new name |
| [**renameFolder**](#_api_folders_method_renameFolder) | rename | Rename folder giving it the name newName |
| [**updateFolderInfo**](#_api_folders_method_updateFolderInfo) | updateInfo | Update folder information |

#### Method copyFolder

Signatures:

-   com.box.sdk.BoxFolder copyFolder(String folderId, String destinationFolderId, String newName);
    

The box/copyFolder API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **destinationFolderId** | The id of the destination folder | String |
| **folderId** | The id of folder to copy | String |
| **newName** | The new name for copied folder; if newName is null, the copied folder has same name as the original. | String |

#### Method createFolder

Signatures:

-   com.box.sdk.BoxFolder createFolder(String parentFolderId, String folderName);
    
-   com.box.sdk.BoxFolder createFolder(String parentFolderId, String\[\] path);
    

The box/createFolder API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **folderName** | The name of created folder | String |
| **parentFolderId** | The id of parent folder | String |
| **path** | Sequence of Box folder names from parent folder to returned folder | String\[\] |

#### Method createFolderSharedLink

Signatures:

-   com.box.sdk.BoxSharedLink createFolderSharedLink(String folderId, com.box.sdk.BoxSharedLink.Access access, java.util.Date unshareDate, com.box.sdk.BoxSharedLink.Permissions permissions);
    

The box/createFolderSharedLink API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **access** | The access level of the shared link | Access |
| **folderId** | The id of folder to create shared link on | String |
| **permissions** | The permissions of the created link; if permissions is null then the created shared link is create with default permissions. | Permissions |
| **unshareDate** | The date and time at which time the created shared link will expire; if unsharedDate is null then a non-expiring link is created. | Date |

#### Method deleteFolder

Signatures:

-   void deleteFolder(String folderId);
    

The box/deleteFolder API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **folderId** | The id of folder to delete | String |

#### Method getFolder

Signatures:

-   com.box.sdk.BoxFolder getFolder(String\[\] path);
    

The box/getFolder API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **path** | Sequence of Box folder names from root folder to returned folder | String\[\] |

#### Method getFolderInfo

Signatures:

-   com.box.sdk.BoxFolder.Info getFolderInfo(String folderId, String\[\] fields);
    

The box/getFolderInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fields** | The information fields to retrieve; if null all information fields are retrieved. | String\[\] |
| **folderId** | The id of folder | String |

#### Method getFolderItems

Signatures:

-   java.util.Collection<com.box.sdk.BoxItem.Info> getFolderItems(String folderId, Long offset, Long limit, String\[\] fields);
    

The box/getFolderItems API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fields** | The item fields to retrieve for each child item; if null all item fields are retrieved. | String\[\] |
| **folderId** | The id of folder | String |
| **limit** | The maximum number of children to retrieve after the offset; if null all child items are retrieved. | Long |
| **offset** | The index of first child item to retrieve; if null all child items are retrieved. | Long |

#### Method getRootFolder

Signatures:

-   com.box.sdk.BoxFolder getRootFolder();
    

The box/getRootFolder API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method moveFolder

Signatures:

-   com.box.sdk.BoxFolder moveFolder(String folderId, String destinationFolderId, String newName);
    

The box/moveFolder API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **destinationFolderId** | The id of the destination folder | String |
| **folderId** | The id of folder to move | String |
| **newName** | The new name of moved folder; if newName is null, the moved folder has same name as the original. | String |

#### Method renameFolder

Signatures:

-   com.box.sdk.BoxFolder renameFolder(String folderId, String newFolderName);
    

The box/renameFolder API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **folderId** | The id of folder to rename | String |
| **newFolderName** | The new name of folder | String |

#### Method updateFolderInfo

Signatures:

-   com.box.sdk.BoxFolder updateFolderInfo(String folderId, com.box.sdk.BoxFolder.Info info);
    

The box/updateFolderInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **folderId** | The id of folder to update | String |
| **info** | The updated information | Info |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

### API: groups

**Only producer is supported**

The groups API is defined in the syntax as follows:

```none
box:groups/methodName?[parameters]
```

The 10 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**addGroupMembership**](#_api_groups_method_addGroupMembership) | addMembership | Add a member to group with the specified role |
| [**createGroup**](#_api_groups_method_createGroup) | create | Create a new group with a specified name and optional additional parameters |
| [**deleteGroup**](#_api_groups_method_deleteGroup) | delete | Delete group |
| [**deleteGroupMembership**](#_api_groups_method_deleteGroupMembership) | delete | Delete group membership |
| [**getAllGroups**](#_api_groups_method_getAllGroups) | groups | Get all the groups in the enterprise |
| [**getGroupInfo**](#_api_groups_method_getGroupInfo) | info | Get group information |
| [**getGroupMembershipInfo**](#_api_groups_method_getGroupMembershipInfo) | membershipInfo | Get group membership information |
| [**getGroupMemberships**](#_api_groups_method_getGroupMemberships) | memberships | Get information about all of the group memberships for this group |
| [**updateGroupInfo**](#_api_groups_method_updateGroupInfo) |  | Update group information |
| [**updateGroupMembershipInfo**](#_api_groups_method_updateGroupMembershipInfo) | updateMembershipInfo | Update group membership information |

#### Method addGroupMembership

Signatures:

-   com.box.sdk.BoxGroupMembership addGroupMembership(String groupId, String userId, com.box.sdk.BoxGroupMembership.GroupRole role);
    

The box/addGroupMembership API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupId** | The id of group | String |
| **role** | The role of the user in this group. Can be null to assign the default role. | GroupRole |
| **userId** | The id of user to be added to group | String |

#### Method createGroup

Signatures:

-   com.box.sdk.BoxGroup createGroup(String name, String provenance, String externalSyncIdentifier, String description, String invitabilityLevel, String memberViewabilityLevel);
    

The box/createGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **description** | The description of the new group | String |
| **externalSyncIdentifier** | The external\_sync\_identifier of the new group | String |
| **invitabilityLevel** | The invitibility\_level of the new group | String |
| **memberViewabilityLevel** | The member\_viewability\_level of the new group | String |
| **name** | The name of the new group | String |
| **provenance** | The provenance of the new group | String |

#### Method deleteGroup

Signatures:

-   void deleteGroup(String groupId);
    

The box/deleteGroup API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupId** | The id of group to delete | String |

#### Method deleteGroupMembership

Signatures:

-   void deleteGroupMembership(String groupMembershipId);
    

The box/deleteGroupMembership API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupMembershipId** | The id of group membership to delete | String |

#### Method getAllGroups

Signatures:

-   java.util.Collection<com.box.sdk.BoxGroup> getAllGroups();
    

The box/getAllGroups API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getGroupInfo

Signatures:

-   com.box.sdk.BoxGroup.Info getGroupInfo(String groupId);
    

The box/getGroupInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupId** | The id of group | String |

#### Method getGroupMembershipInfo

Signatures:

-   com.box.sdk.BoxGroupMembership.Info getGroupMembershipInfo(String groupMembershipId);
    

The box/getGroupMembershipInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupMembershipId** | The id of group membership | String |

#### Method getGroupMemberships

Signatures:

-   java.util.Collection<com.box.sdk.BoxGroupMembership.Info> getGroupMemberships(String groupId);
    

The box/getGroupMemberships API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupId** | The id of group | String |

#### Method updateGroupInfo

Signatures:

-   com.box.sdk.BoxGroup updateGroupInfo(String groupId, com.box.sdk.BoxGroup.Info groupInfo);
    

The box/updateGroupInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupId** | The id of group to update | String |
| **groupInfo** | The updated information | Info |

#### Method updateGroupMembershipInfo

Signatures:

-   com.box.sdk.BoxGroupMembership updateGroupMembershipInfo(String groupMembershipId, com.box.sdk.BoxGroupMembership.Info info);
    

The box/updateGroupMembershipInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **groupMembershipId** | The id of group membership to update | String |
| **info** | The updated information | Info |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

### API: search

**Only producer is supported**

The search API is defined in the syntax as follows:

```none
box:search/methodName?[parameters]
```

The 1 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**searchFolder**](#_api_search_method_searchFolder) | search | Search folder and all descendant folders using the given query |

#### Method searchFolder

Signatures:

-   java.util.Collection<com.box.sdk.BoxItem> searchFolder(String folderId, String query);
    

The box/searchFolder API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **folderId** | The id of folder searched | String |
| **query** | The search query | String |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

### API: tasks

**Only producer is supported**

The tasks API is defined in the syntax as follows:

```none
box:tasks/methodName?[parameters]
```

The 9 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**addAssignmentToTask**](#_api_tasks_method_addAssignmentToTask) | addAssignment | Add assignment for task |
| [**addFileTask**](#_api_tasks_method_addFileTask) | add | Add task to file |
| [**deleteTask**](#_api_tasks_method_deleteTask) | delete | Delete task |
| [**deleteTaskAssignment**](#_api_tasks_method_deleteTaskAssignment) | delete | Delete task assignment |
| [**getFileTasks**](#_api_tasks_method_getFileTasks) | tasks | Get a list of any tasks on file |
| [**getTaskAssignmentInfo**](#_api_tasks_method_getTaskAssignmentInfo) | assignmentInfo | Get task assignment information |
| [**getTaskAssignments**](#_api_tasks_method_getTaskAssignments) | assignments | Get a list of any assignments for task |
| [**getTaskInfo**](#_api_tasks_method_getTaskInfo) | info | Get task information |
| [**updateTaskInfo**](#_api_tasks_method_updateTaskInfo) | updateInfo | Update task information |

#### Method addAssignmentToTask

Signatures:

-   com.box.sdk.BoxTask addAssignmentToTask(String taskId, com.box.sdk.BoxUser assignTo);
    

The box/addAssignmentToTask API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **assignTo** | The user to assign to task | BoxUser |
| **taskId** | The id of task to add assignment for | String |

#### Method addFileTask

Signatures:

-   com.box.sdk.BoxTask addFileTask(String fileId, com.box.sdk.BoxTask.Action action, java.util.Date dueAt, String message);
    

The box/addFileTask API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **action** | The action the task assignee will be prompted to do | Action |
| **dueAt** | The day at which this task is due | Date |
| **fileId** | The id of file to add task to | String |
| **message** | An optional message to include with the task | String |

#### Method deleteTask

Signatures:

-   void deleteTask(String taskId);
    

The box/deleteTask API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **taskId** | The id of task to delete | String |

#### Method deleteTaskAssignment

Signatures:

-   void deleteTaskAssignment(String taskAssignmentId);
    

The box/deleteTaskAssignment API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **taskAssignmentId** | The id of task assignment to delete | String |

#### Method getFileTasks

Signatures:

-   java.util.List<com.box.sdk.BoxTask.Info> getFileTasks(String fileId);
    

The box/getFileTasks API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fileId** | The id of file | String |

#### Method getTaskAssignmentInfo

Signatures:

-   com.box.sdk.BoxTaskAssignment.Info getTaskAssignmentInfo(String taskAssignmentId);
    

The box/getTaskAssignmentInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **taskAssignmentId** | The id of task assignment | String |

#### Method getTaskAssignments

Signatures:

-   java.util.List<com.box.sdk.BoxTaskAssignment.Info> getTaskAssignments(String taskId);
    

The box/getTaskAssignments API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **taskId** | The id of task | String |

#### Method getTaskInfo

Signatures:

-   com.box.sdk.BoxTask.Info getTaskInfo(String taskId);
    

The box/getTaskInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **taskId** | The id of task | String |

#### Method updateTaskInfo

Signatures:

-   com.box.sdk.BoxTask updateTaskInfo(String taskId, com.box.sdk.BoxTask.Info info);
    

The box/updateTaskInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **info** | The updated information | Info |
| **taskId** | The id of task | String |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

### API: users

**Only producer is supported**

The users API is defined in the syntax as follows:

```none
box:users/methodName?[parameters]
```

The 11 method(s) is(are) listed in the table below, followed by detailed syntax for each method. (API methods can have a shorthand _alias_ name which can be used in the syntax instead of the name)

  
| Method | Alias | Description |
| --- | --- | --- |
| [**addUserEmailAlias**](#_api_users_method_addUserEmailAlias) | addEmailAlias | Add a new email alias to user’s account |
| [**createAppUser**](#_api_users_method_createAppUser) | create | Provision a new app user in an enterprise with additional user information using Box Developer Edition |
| [**createEnterpriseUser**](#_api_users_method_createEnterpriseUser) | create | Provision a new user in an enterprise with additional user information |
| [**deleteUser**](#_api_users_method_deleteUser) | delete | Delete user from an enterprise account |
| [**deleteUserEmailAlias**](#_api_users_method_deleteUserEmailAlias) | delete | Delete an email alias from user’s account |
| [**getAllEnterpriseOrExternalUsers**](#_api_users_method_getAllEnterpriseOrExternalUsers) | users | Get any managed users that match the filter term as well as any external users that match the filter term |
| [**getCurrentUser**](#_api_users_method_getCurrentUser) | currentUser | Get current user |
| [**getUserEmailAlias**](#_api_users_method_getUserEmailAlias) | emailAlias | Get a collection of all the email aliases for user |
| [**getUserInfo**](#_api_users_method_getUserInfo) | info | Get user information |
| [**moveFolderToUser**](#_api_users_method_moveFolderToUser) |  | Move root folder for specified user to current user |
| [**updateUserInfo**](#_api_users_method_updateUserInfo) | updateInfo | Update user information |

#### Method addUserEmailAlias

Signatures:

-   com.box.sdk.EmailAlias addUserEmailAlias(String userId, String email);
    

The box/addUserEmailAlias API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **email** | The email address to add as an alias | String |
| **userId** | The id of user | String |

#### Method createAppUser

Signatures:

-   com.box.sdk.BoxUser createAppUser(String name, com.box.sdk.CreateUserParams params);
    

The box/createAppUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **name** | The name of the user | String |
| **params** | Additional user information | CreateUserParams |

#### Method createEnterpriseUser

Signatures:

-   com.box.sdk.BoxUser createEnterpriseUser(String login, String name, com.box.sdk.CreateUserParams params);
    

The box/createEnterpriseUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **login** | The email address the user will use to login | String |
| **name** | The name of the user | String |
| **params** | Additional user information | CreateUserParams |

#### Method deleteUser

Signatures:

-   void deleteUser(String userId, boolean notifyUser, boolean force);
    

The box/deleteUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **force** | Whether or not this user should be deleted even if they still own files | Boolean |
| **notifyUser** | Whether or not to send an email notification to the user that their account has been deleted | Boolean |
| **userId** | The id of user to delete | String |

#### Method deleteUserEmailAlias

Signatures:

-   void deleteUserEmailAlias(String userId, String emailAliasId);
    

The box/deleteUserEmailAlias API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **emailAliasId** | The id of the email alias to delete | String |
| **userId** | The id of user | String |

#### Method getAllEnterpriseOrExternalUsers

Signatures:

-   java.util.List<com.box.sdk.BoxUser.Info> getAllEnterpriseOrExternalUsers(String filterTerm, String\[\] fields);
    

The box/getAllEnterpriseOrExternalUsers API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **fields** | The fields to retrieve. Leave this out for the standard fields. | String\[\] |
| **filterTerm** | The filter term to lookup users by (login for external, login or name for managed); if null all managed users are returned. | String |

#### Method getCurrentUser

Signatures:

-   com.box.sdk.BoxUser getCurrentUser();
    

The box/getCurrentUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |

#### Method getUserEmailAlias

Signatures:

-   java.util.Collection<com.box.sdk.EmailAlias> getUserEmailAlias(String userId);
    

The box/getUserEmailAlias API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userId** | The id of user | String |

#### Method getUserInfo

Signatures:

-   com.box.sdk.BoxUser.Info getUserInfo(String userId);
    

The box/getUserInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **userId** | The id of user | String |

#### Method moveFolderToUser

Signatures:

-   com.box.sdk.BoxFolder.Info moveFolderToUser(String userId, String sourceUserId);
    

The box/moveFolderToUser API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **sourceUserId** | The user id of the user whose files will be the source for this operation | String |
| **userId** | The id of user | String |

#### Method updateUserInfo

Signatures:

-   com.box.sdk.BoxUser updateUserInfo(String userId, com.box.sdk.BoxUser.Info info);
    

The box/updateUserInfo API method has the parameters listed in the table below:

  
| Parameter | Description | Type |
| --- | --- | --- |
| **info** | The updated information | Info |
| **userId** | The id of user to update | String |

In addition to the parameters above, the box API can also use any of the [Query Parameters (19 parameters)](#_query_parameters).

Any of the parameters can be provided in either the endpoint URI, or dynamically in a message header. The message header name must be of the format `CamelBox.parameter`. The `inBody` parameter overrides message header, i.e., the endpoint parameter `inBody=myParameterNameHere` would override a `CamelBox.myParameterNameHere` header.

## Usage

### Connection Authentication Types

The Box component supports three different types of authenticated connections.

#### Standard Authentication

**Standard Authentication** uses the **OAuth 2.0 three-legged authentication process** to authenticate its connections with Box.com. This type of authentication enables Box **managed users** and **external users** to access, edit, and save their Box content through the Box component.

#### App Enterprise Authentication

**App Enterprise Authentication** uses the **OAuth 2.0 with JSON Web Tokens (JWT)** to authenticate its connections as a **Service Account** for a **Box Application**. This type of authentication enables a service account to access, edit, and save the Box content of its **Box Application** through the Box component.

#### App User Authentication

**App User Authentication** uses the **OAuth 2.0 with JSON Web Tokens (JWT)** to authenticate its connections as an **App User** for a **Box Application**. This type of authentication enables app users to access, edit, and save their Box content in its **Box Application** through the Box component.

## Examples

The following route uploads new files to the user’s root folder:

```java
from("file:...")
    .to("box://files/upload/inBody=fileUploadRequest");
```

The following route polls user’s account for updates:

```java
from("box://events/listen?startingPosition=-1")
    .to("bean:blah");
```

The following route uses a producer with dynamic header options. The **fileId** property has the Box file id and the **output** property has the output stream of the file contents, so they are assigned to the **CamelBox.fileId** header and **CamelBox.output** header respectively as follows:

```java
from("direct:foo")
    .setHeader("CamelBox.fileId", header("fileId"))
    .setHeader("CamelBox.output", header("output"))
    .to("box://files/download")
    .to("file://...");
```

### More information

See more details at the Box API reference: [https://developer.box.com/reference](https://developer.box.com/reference)

## Spring Boot Auto-Configuration

When using box with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-box-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 20 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.box.access-token-cache** | Custom Access Token Cache for storing and retrieving access tokens. The option is a com.box.sdk.IAccessTokenCache type. |  | IAccessTokenCache |
| **camel.component.box.authentication-type** | The type of authentication for connection. Types of Authentication: STANDARD\_AUTHENTICATION - OAuth 2.0 (3-legged) SERVER\_AUTHENTICATION - OAuth 2.0 with JSON Web Tokens. | APP\_USER\_AUTHENTICATION | String |
| **camel.component.box.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.box.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.box.client-id** | Box application client ID. |  | String |
| **camel.component.box.client-secret** | Box application client secret. |  | String |
| **camel.component.box.configuration** | To use the shared configuration. The option is a org.apache.camel.component.box.BoxConfiguration type. |  | BoxConfiguration |
| **camel.component.box.enabled** | Whether to enable auto configuration of the box component. This is enabled by default. |  | Boolean |
| **camel.component.box.encryption-algorithm** | The type of encryption algorithm for JWT. Supported Algorithms: RSA\_SHA\_256 RSA\_SHA\_384 RSA\_SHA\_512. | rsa-sha-256 | EncryptionAlgorithm |
| **camel.component.box.enterprise-id** | The enterprise ID to use for an App Enterprise. |  | String |
| **camel.component.box.http-params** | Custom HTTP params for settings like proxy host. |  | Map |
| **camel.component.box.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.box.max-cache-entries** | The maximum number of access tokens in cache. | 100 | Integer |
| **camel.component.box.private-key-file** | The private key for generating the JWT signature. |  | String |
| **camel.component.box.private-key-password** | The password for the private key. |  | String |
| **camel.component.box.public-key-id** | The ID for public key for validating the JWT signature. |  | String |
| **camel.component.box.ssl-context-parameters** | To configure security using SSLContextParameters. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.box.user-id** | The user ID to use for an App User. |  | String |
| **camel.component.box.user-name** | Box user name, MUST be provided. |  | String |
| **camel.component.box.user-password** | Box user password, MUST be provided if authSecureStorage is not set, or returns null on first call. |  | String |