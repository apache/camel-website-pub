# File Watch

**Since Camel 3.0**

**Only consumer is supported**

This component can be used to watch file modification events in the folder. It is based on the project [directory-watcher](https://github.com/gmethvin/directory-watcher).

## URI Options

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

The File Watch component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **useFileHashing** (consumer) | Enables or disables file hashing to detect duplicate events. If you disable this, you can get some events multiple times on some platforms and JDKs. Check java.nio.file.WatchService limitations for your target platform. | true | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **concurrentConsumers** (advanced) | The number of concurrent consumers. Increase this value, if your route is slow to prevent buffering in queue. | 1 | int |
| **fileHasher** (advanced) | Reference to io.methvin.watcher.hashing.FileHasher. This prevents emitting duplicate events on some platforms. For working with large files and if you dont need detect multiple modifications per second per file, use #lastModifiedTimeFileHasher. You can also provide custom implementation in registry. | #murmur3FFileHasher | FileHasher |
| **pollThreads** (advanced) | The number of threads polling WatchService. Increase this value, if you see OVERFLOW messages in log. | 1 | int |
| **queueSize** (advanced) | Maximum size of queue between WatchService and consumer. Unbounded by default. | 2147483647 | int |

## Endpoint Options

The File Watch endpoint is configured using URI syntax:

file-watch:path

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **path** (consumer) | **Required** Path of directory to consume events from. |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **antInclude** (consumer) | ANT style pattern to match files. The file is matched against path relative to endpoint path. Pattern must be also relative (not starting with slash). | \*\* | String |
| **autoCreate** (consumer) | Auto create directory if does not exist. | true | boolean |
| **events** (consumer) | Comma separated list of events to watch. Possible values: CREATE,MODIFY,DELETE. | CREATE,MODIFY,DELETE | String |
| **recursive** (consumer) | Watch recursive in current and child directories (including newly created directories). | true | boolean |
| **useFileHashing** (consumer) | Enables or disables file hashing to detect duplicate events. If you disable this, you can get some events multiple times on some platforms and JDKs. Check java.nio.file.WatchService limitations for your target platform. | true | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **concurrentConsumers** (advanced) | The number of concurrent consumers. Increase this value, if your route is slow to prevent buffering in queue. | 1 | int |
| **fileHasher** (advanced) | Reference to io.methvin.watcher.hashing.FileHasher. This prevents emitting duplicate events on some platforms. For working with large files and if you dont need detect multiple modifications per second per file, use #lastModifiedTimeFileHasher. You can also provide custom implementation in registry. | #murmur3FFileHasher | FileHasher |
| **pollThreads** (advanced) | The number of threads polling WatchService. Increase this value, if you see OVERFLOW messages in log. | 1 | int |
| **queueSize** (advanced) | Maximum size of queue between WatchService and consumer. Unbounded by default. | 2147483647 | int |

## Message Headers

The File Watch component supports 10 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelFileEventType** (consumer) Constant: [`EVENT_TYPE_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#EVENT_TYPE_HEADER) | Type of event. Possible values: CREATE, DELETE, MODIFY. |  | String |
| **CamelFileNameOnly** (consumer) Constant: [`FILE_NAME_ONLY`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#FILE_NAME_ONLY) | Only the file name (the name with no leading paths). |  | String |
| **CamelFileAbsolute** (consumer) Constant: [`FILE_ABSOLUTE`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#FILE_ABSOLUTE) | A boolean option specifying whether the consumed file denotes an absolute path or not. Should normally be false for relative paths. Absolute paths should normally not be used but we added to the move option to allow moving files to absolute paths. But can be used elsewhere as well. |  | Boolean |
| **CamelFileAbsolutePath** (consumer) Constant: [`FILE_ABSOLUTE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#FILE_ABSOLUTE_PATH) | The absolute path to the file. For relative files this path holds the relative path instead. |  | String |
| **CamelFilePath** (consumer) Constant: [`FILE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#FILE_PATH) | The file path. For relative files this is the starting directory the relative filename. For absolute files this is the absolute path. |  | String |
| **CamelFileName** (consumer) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#FILE_NAME) | Name of the consumed file as a relative file path with offset from the starting directory configured on the endpoint. |  | String |
| **CamelFileRelativePath** (consumer) Constant: [`FILE_RELATIVE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#FILE_RELATIVE_PATH) | The relative path. |  | String |
| **CamelFileNameConsumed** (consumer) Constant: [`FILE_NAME_CONSUMED`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#FILE_NAME_CONSUMED) | The name of the file that has been consumed. |  | String |
| **CamelFileParent** (consumer) Constant: [`FILE_PARENT`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#FILE_PARENT) | The parent path. |  | String |
| **CamelFileLastModified** (consumer) Constant: [`FILE_LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-file-watch/latest/org/apache/camel/component/file/watch/FileWatchConstants.html#FILE_LAST_MODIFIED) | A Long value containing the last modified timestamp of the file. |  | long |

## Examples

### Recursive watch all events (file creation, file deletion, file modification):

-   Java
    
-   XML
    
-   YAML
    

```java
from("file-watch://some-directory")
    .log("File event: ${header.CamelFileEventType} occurred on file ${header.CamelFileName} at ${header.CamelFileLastModified}");
```

```xml
<route>
  <from uri="file-watch://some-directory"/>
  <log message="File event: ${header.CamelFileEventType} occurred on file ${header.CamelFileName} at ${header.CamelFileLastModified}"/>
</route>
```

```yaml
- route:
    from:
      uri: file-watch://some-directory
      steps:
        - log:
            message: "File event: ${header.CamelFileEventType} occurred on file ${header.CamelFileName} at ${header.CamelFileLastModified}"
```

### Recursive watch for creation and deletion of txt files:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file-watch://some-directory?events=DELETE,CREATE&antInclude=**/*.txt")
    .log("File event: ${header.CamelFileEventType} occurred on file ${header.CamelFileName} at ${header.CamelFileLastModified}");
```

```xml
<route>
  <from uri="file-watch://some-directory?events=DELETE,CREATE&amp;antInclude=**/*.txt"/>
  <log message="File event: ${header.CamelFileEventType} occurred on file ${header.CamelFileName} at ${header.CamelFileLastModified}"/>
</route>
```

```yaml
- route:
    from:
      uri: file-watch://some-directory
      parameters:
        events: "DELETE,CREATE"
        antInclude: "**/*.txt"
      steps:
        - log:
            message: "File event: ${header.CamelFileEventType} occurred on file ${header.CamelFileName} at ${header.CamelFileLastModified}"
```

### Create a snapshot of file when modified:

-   Java
    
-   XML
    
-   YAML
    

```java
from("file-watch://some-directory?events=MODIFY&recursive=false")
    .setHeader(Exchange.FILE_NAME, simple("${header.CamelFileName}.${header.CamelFileLastModified}"))
    .to("file:some-directory/snapshots");
```

```xml
<route>
  <from uri="file-watch://some-directory?events=MODIFY&amp;recursive=false"/>
  <setHeader name="CamelFileName">
    <simple>${header.CamelFileName}.${header.CamelFileLastModified}</simple>
  </setHeader>
  <to uri="file:some-directory/snapshots"/>
</route>
```

```yaml
- route:
    from:
      uri: file-watch://some-directory
      parameters:
        events: MODIFY
        recursive: false
      steps:
        - setHeader:
            name: CamelFileName
            expression:
              simple:
                expression: "${header.CamelFileName}.${header.CamelFileLastModified}"
        - to:
            uri: file:some-directory/snapshots
```

## Spring Boot Auto-Configuration

When using file-watch with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-file-watch-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.file-watch.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.file-watch.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.file-watch.concurrent-consumers** | The number of concurrent consumers. Increase this value, if your route is slow to prevent buffering in queue. | 1 | Integer |
| **camel.component.file-watch.enabled** | Whether to enable auto configuration of the file-watch component. This is enabled by default. |  | Boolean |
| **camel.component.file-watch.file-hasher** | Reference to io.methvin.watcher.hashing.FileHasher. This prevents emitting duplicate events on some platforms. For working with large files and if you dont need detect multiple modifications per second per file, use #lastModifiedTimeFileHasher. You can also provide custom implementation in registry. The option is a io.methvin.watcher.hashing.FileHasher type. |  | FileHasher |
| **camel.component.file-watch.poll-threads** | The number of threads polling WatchService. Increase this value, if you see OVERFLOW messages in log. | 1 | Integer |
| **camel.component.file-watch.queue-size** | Maximum size of queue between WatchService and consumer. Unbounded by default. | 2147483647 | Integer |
| **camel.component.file-watch.use-file-hashing** | Enables or disables file hashing to detect duplicate events. If you disable this, you can get some events multiple times on some platforms and JDKs. Check java.nio.file.WatchService limitations for your target platform. | true | Boolean |