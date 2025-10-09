# Dropbox

**Since Camel 2.14**

**Both producer and consumer are supported**

The Dropbox component allows you to treat [Dropbox](https://www.dropbox.com) remote folders as a producer or consumer of messages. Using the [Dropbox Java Core API](https://github.com/dropbox/dropbox-sdk-java), this camel component has the following features:

-   As a consumer, download files and search files by queries
    
-   As a producer, download files, move files between remote directories, delete files/dir, upload files and search files by queries
    

In order to work with Dropbox API you need to obtain an **accessToken**, **expireIn**, **refreshToken**, **apiKey**, **apiSecret** and a **clientIdentifier.**  
You can refer to the [Dropbox documentation](https://dropbox.tech/developers/migrating-app-permissions-and-access-tokens) that explains how to get them.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-dropbox</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

dropbox://\[operation\]?\[options\]

Where **operation** is the specific action (typically is a CRUD action) to perform on Dropbox remote folder.

## Operations

 
| Operation | Description |
| --- | --- |
| `del` | deletes files or directories on Dropbox |
| `get` | download files from Dropbox |
| `move` | move files from folders on Dropbox |
| `put` | upload files on Dropbox |
| `search` | search files on Dropbox based on string queries |

**Operations** require additional options to work, some are mandatory for the specific operation.

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

The Dropbox component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Dropbox endpoint is configured using URI syntax:

dropbox:operation

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (common) | 
**Required** The specific action (typically is a CRUD action) to perform on Dropbox remote folder.

Enum values:

-   put
    
-   del
    
-   search
    
-   get
    
-   move
    





 |  | DropboxOperation |

### Query Parameters (16 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clientIdentifier** (common) | Name of the app registered to make API requests. |  | String |
| **query** (common) | A space-separated list of sub-strings to search for. A file matches only if it contains all the sub-strings. If this option is not set, all files will be matched. |  | String |
| **remotePath** (common) | Original file or folder to move. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **localPath** (producer) | Optional folder or file to upload on Dropbox from the local filesystem. If this option has not been configured then the message body is used as the content to upload. |  | String |
| **newRemotePath** (producer) | Destination file or folder. |  | String |
| **uploadMode** (producer) | 

Which mode to upload. in case of add the new file will be renamed if a file with the same name already exists on dropbox. in case of force if a file with the same name already exists on dropbox, this will be overwritten.

Enum values:

-   add
    
-   force
    





 |  | DropboxUploadMode |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (advanced) | To use an existing DbxClient instance as Dropbox client. |  | DbxClientV2 |
| **accessToken** (security) | **Required** The access token to make API requests for a specific Dropbox user. |  | String |
| **apiKey** (security) | **Required** The apiKey to make API requests for a specific Dropbox user. |  | String |
| **apiSecret** (security) | **Required** The apiSecret to make API requests for a specific Dropbox user. |  | String |
| **expireIn** (security) | **Required** The expire time to access token for a specific Dropbox user. |  | Long |
| **refreshToken** (security) | **Required** The refresh token to refresh the access token for a specific Dropbox user. |  | String |

## Message Headers

The Dropbox component supports 13 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDropboxRemotePath** (all) Constant: [`HEADER_REMOTE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#HEADER_REMOTE_PATH) | The remote path. |  | String |
| **CamelDropboxNewRemotePath** (move) Constant: [`HEADER_NEW_REMOTE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#HEADER_NEW_REMOTE_PATH) | The new remote path. |  | String |
| **CamelDropboxLocalPath** (put) Constant: [`HEADER_LOCAL_PATH`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#HEADER_LOCAL_PATH) | The local path. |  | String |
| **CamelDropboxUploadMode** (put) Constant: [`HEADER_UPLOAD_MODE`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#HEADER_UPLOAD_MODE) | The upload mode. |  | String |
| **CamelDropboxQuery** (search) Constant: [`HEADER_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#HEADER_QUERY) | The query. |  | String |
| **CamelDropboxPutFileName** (put) Constant: [`HEADER_PUT_FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#HEADER_PUT_FILE_NAME) | The name of the file to upload. |  | String |
| **DOWNLOADED\_FILE** (get) Constant: [`DOWNLOADED_FILE`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#DOWNLOADED_FILE) | In case of single file download, path of the remote file downloaded. |  | String |
| **DOWNLOADED\_FILES** (get) Constant: [`DOWNLOADED_FILES`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#DOWNLOADED_FILES) | In case of multiple files download, path of the remote files downloaded. |  | String |
| **UPLOADED\_FILE** (put) Constant: [`UPLOADED_FILE`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#UPLOADED_FILE) | In case of single file upload, path of the remote path uploaded. |  | String |
| **UPLOADED\_FILES** (put) Constant: [`UPLOADED_FILES`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#UPLOADED_FILES) | In case of multiple files upload, string with the remote paths uploaded. |  | String |
| **FOUND\_FILES** (search) Constant: [`FOUND_FILES`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#FOUND_FILES) | List of file path founded. |  | String |
| **DELETED\_PATH** (del) Constant: [`DELETED_PATH`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#DELETED_PATH) | Name of the path deleted on dropbox. |  | String |
| **MOVED\_PATH** (move) Constant: [`MOVED_PATH`](https://javadoc.io/doc/org.apache.camel/camel-dropbox/latest/org/apache/camel/component/dropbox/util/DropboxConstants.html#MOVED_PATH) | Name of the path moved on dropbox. |  | String |

## Del operation

Delete files on Dropbox.

Works only as Camel producer.

Below are listed the options for this operation:

  
| Property | Mandatory | Description |
| --- | --- | --- |
| `remotePath` | `true` | Folder or file to delete on Dropbox |

### Samples

```java
from("direct:start")
  .to("dropbox://del?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&remotePath=/root/folder1")
  .to("mock:result");

from("direct:start")
  .to("dropbox://del?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&remotePath=/root/folder1/file1.tar.gz")
  .to("mock:result");
```

### Result Message Body

The following objects are set on message body result:

 
| Object type | Description |
| --- | --- |
| `String` | name of the path deleted on dropbox |

## Get (download) operation

Download files from Dropbox.

Works as Camel producer or Camel consumer.

Below are listed the options for this operation:

  
| Property | Mandatory | Description |
| --- | --- | --- |
| `remotePath` | `true` | Folder or file to download from Dropbox |

### Samples

```java
from("direct:start")
  .to("dropbox://get?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&remotePath=/root/folder1/file1.tar.gz")
  .to("file:///home/kermit/?fileName=file1.tar.gz");

from("direct:start")
  .to("dropbox://get?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&remotePath=/root/folder1")
  .to("mock:result");

from("dropbox://get?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&remotePath=/root/folder1")
  .to("file:///home/kermit/");
```

### Result Message Body

The following objects are set on message body result:

 
| Object type | Description |
| --- | --- |
| `byte[]` or `CachedOutputStream` if stream caching is enabled | in case of single file download, stream representing the file downloaded |
| `Map<String, byte[]>` or `Map<String, CachedOutputStream>` if stream caching is enabled | in case of multiple files download, a map with as key the path of the remote file downloaded and as value the stream representing the file downloaded |

## Move operation

Move files on Dropbox between one folder to another.

Works only as Camel producer.

Below are listed the options for this operation:

  
| Property | Mandatory | Description |
| --- | --- | --- |
| `remotePath` | `true` | Original file or folder to move |
| `newRemotePath` | `true` | Destination file or folder |

### Samples

```java
from("direct:start")
  .to("dropbox://move?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&remotePath=/root/folder1&newRemotePath=/root/folder2")
  .to("mock:result");
```

### Result Message Body

The following objects are set on message body result:

 
| Object type | Description |
| --- | --- |
| `String` | name of the path moved on dropbox |

## Put (upload) operation

Upload files on Dropbox.

Works as Camel producer.

Below are listed the options for this operation:

  
| Property | Mandatory | Description |
| --- | --- | --- |
| `uploadMode` | `true` | add or force this option specifies how a file should be saved on dropbox: in case of "add" the new file will be renamed if a file with the same name already exists on dropbox. In case of "force" if a file with the same name already exists on dropbox, this will be overwritten. |
| `localPath` | `false` | Folder or file to upload on Dropbox from the local filesystem. If this option has been configured then it takes precedence over uploading as a single file with content from the Camel message body (message body is converted into a byte array). |
| `remotePath` | `false` | Folder destination on Dropbox. If the property is not set, the component will upload the file on a remote path equal to the local path. With Windows or without an absolute localPath you may run into an exception like the following: Caused by: java.lang.IllegalArgumentException: 'path': bad path: must start with "/": "C:/My/File"  
OR  
Caused by: java.lang.IllegalArgumentException: 'path': bad path: must start with "/": "MyFile"  
 |

### Samples

```java
from("direct:start").to("dropbox://put?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&uploadMode=add&localPath=/root/folder1")
  .to("mock:result");

from("direct:start").to("dropbox://put?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&uploadMode=add&localPath=/root/folder1&remotePath=/root/folder2")
  .to("mock:result");
```

And to upload a single file with content from the message body

```java
from("direct:start")
   .setHeader(DropboxConstants.HEADER_PUT_FILE_NAME, constant("myfile.txt"))
   .to("dropbox://put?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&uploadMode=add&remotePath=/root/folder2")
   .to("mock:result");
```

The name of the file can be provided in the header `DropboxConstants.HEADER_PUT_FILE_NAME` or `Exchange.FILE_NAME` in that order of precedence. If no header has been provided then the message id (uuid) is used as the file name.

### Result Message Body

The following objects are set on message body result:

 
| Object type | Description |
| --- | --- |
| `String` | in case of single file upload, result of the upload operation, OK or KO |
| `Map<String, DropboxResultCode>` | in case of multiple files upload, a map with as key the path of the remote file uploaded and as value the result of the upload operation, OK or KO |

## Search operation

Search inside a remote Dropbox folder including its sub directories.

Works as Camel producer and as Camel consumer.

Below are listed the options for this operation:

  
| Property | Mandatory | Description |
| --- | --- | --- |
| `remotePath` | `true` | Folder on Dropbox where to search in. |
| `query` | `true` | A space-separated list of sub-strings to search for. A file matches only if it contains all the sub-strings. If this option is not set, all files will be matched. The query is required to be provided in either the endpoint configuration or as a header `CamelDropboxQuery` on the Camel message. |

### Samples

```java
from("dropbox://search?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&remotePath=/XXX&query=XXX")
  .to("mock:result");

from("direct:start")
  .setHeader("CamelDropboxQuery", constant("XXX"))
  .to("dropbox://search?accessToken=XXX&clientIdentifier=XXX&expireIn=1000&refreshToken=XXXX"
      +"&apiKey=XXXXX&apiSecret=XXXXXX&remotePath=/XXX")
  .to("mock:result");
```

### Result Message Body

The following objects are set on message body result:

 
| Object type | Description |
| --- | --- |
| `List<com.dropbox.core.v2.files.SearchMatchV2>` | list of file path founded. For more information on this object refer to [Dropbox documentation](https://javadoc.io/doc/com.dropbox.core/dropbox-core-sdk/latest/com/dropbox/core/v2/files/SearchMatchV2.md). |

## Spring Boot Auto-Configuration

When using dropbox with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-dropbox-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.dropbox.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.dropbox.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.dropbox.enabled** | Whether to enable auto configuration of the dropbox component. This is enabled by default. |  | Boolean |
| **camel.component.dropbox.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |