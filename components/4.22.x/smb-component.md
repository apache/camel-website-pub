# SMB

**Since Camel 4.3**

**Both producer and consumer are supported**

The Server Message Block (SMB) component provides a way to connect natively to SMB file shares, such as those provided by Microsoft Windows or [Samba](https://www.samba.org/).

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-smb</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

smb:address\[:port\]/shareName\[?options\]

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

The SMB component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The SMB endpoint is configured using URI syntax:

smb:hostname:port/shareName/path

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **hostname** (common) | **Required** The share hostname or IP address. |  | String |
| **port** (common) | The share port number. | 445 | int |
| **shareName** (common) | **Required** The name of the share directory. |  | String |
| **path** (common) | The base directory within the share. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **charset** (common) | This option is used to specify the encoding of the file. You can use this on the consumer, to specify the encodings of the files, which allow Camel to know the charset it should load the file content in case the file content is being accessed. Likewise when writing a file, you can use this option to specify which charset to write the file as well. Do mind that when writing the file Camel may have to read the message content into memory to be able to convert the data into the configured charset, so do not use this if you have big messages. |  | String |
| **disconnect** (common) | Whether or not to disconnect from remote SMB share right after use. Disconnect will only disconnect the current connection to the SMB share. If you have a consumer which you want to stop, then you need to stop the consumer/route instead. | false | boolean |
| **doneFileName** (common) | Producer: If provided, then Camel will write a 2nd done file when the original file has been written. The done file will be empty. This option configures what file name to use. Either you can specify a fixed name. Or you can use dynamic placeholders. The done file will always be written in the same folder as the original file. Consumer: If provided, Camel will only consume files if a done file exists. This option configures what file name to use. Either you can specify a fixed name. Or you can use dynamic placeholders.The done file is always expected in the same folder as the original file. Only $\\{file.name} and $\\{file.name.next} is supported as dynamic placeholders. |  | String |
| **fileName** (common) | Use Expression such as File Language to dynamically set the filename. For consumers, it’s used as a filename filter. For producers, it’s used to evaluate the filename to write. If an expression is set, it take precedence over the CamelFileName header. (Note: The header itself can also be an Expression). The expression options support both String and Expression types. If the expression is a String type, it is always evaluated using the File Language. If the expression is an Expression type, the specified Expression type is used - this allows you, for instance, to use OGNL expressions. For the consumer, you can use it to filter filenames, so you can for instance consume today’s file using the File Language syntax: mydata-$\\{date:now:yyyyMMdd}.txt. The producers support the CamelOverruleFileName header which takes precedence over any existing CamelFileName header; the CamelOverruleFileName is a header that is used only once, and makes it easier as this avoids to temporary store CamelFileName and have to restore it afterwards. |  | String |
| **jailStartingDirectory** (common) | Used for jailing (restricting) writing files to the starting directory (and sub) only. This is enabled by default to not allow Camel to write files to outside directories (to be more secured out of the box). You can turn this off to allow writing files to directories outside the starting directory, such as parent or root folders. For consumers that use a localWorkDirectory, this also restricts the downloaded files to stay within the configured localWorkDirectory. | true | boolean |
| **delete** (consumer) | If true, the file will be deleted after it is processed successfully. | false | boolean |
| **moveFailed** (consumer) | Sets the move failure expression based on Simple language. For example, to move files into a .error subdirectory use: .error. Note: When moving the files to the fail location Camel will handle the error and will not pick up the file again. |  | String |
| **noop** (consumer) | If true, the file is not moved or deleted in any way. This option is good for readonly data, or for ETL type requirements. If noop=true, Camel will set idempotent=true as well, to avoid consuming the same files over and over again. | false | boolean |
| **preMove** (consumer) | Expression (such as File Language) used to dynamically set the filename when moving it before processing. For example to move in-progress files into the order directory set this value to order. |  | String |
| **preSort** (consumer) | 
When pre-sort is enabled then the consumer will sort the file and directory names during polling, that was retrieved from the file system. You may want to do this in case you need to operate on the files in a sorted order. The pre-sort is executed before the consumer starts to filter, and accept files to process by Camel. This option is default=false meaning disabled. The following values are supported: name (sort by file name), modified (sort by last-modified timestamp), size (sort by file size). To sort in descending (reverse) order, prefix the value with a minus sign (e.g., -modified to sort newest first). The value true is an alias for name (backward compatible).

Enum values:

-   true
    
-   false
    
-   name
    
-   \-name
    
-   modified
    
-   \-modified
    
-   size
    
-   \-size
    





 |  | String |
| **recursive** (consumer) | If a directory, will look for files in all the sub-directories as well. | false | boolean |
| **searchPattern** (consumer) | The search pattern used to list the files (server side on SMB). This parameter can contain the name of a file (or multiple files, if wildcards are used) within this directory. When it is null all files are included. Two wild card characters are supported in the search pattern. The (question mark) character matches a single character. If a search pattern contains one or more characters, then exactly that number of characters is matched by the wildcards. For example, the criterion x matches abx but not abcx or ax, because the two file names do not have enough characters preceding the literal. When a file name criterion has characters trailing a literal, then the match is made with specified number of characters or less. For example, the criterion x matches xab, xa, and x, but not xabc. If only characters are present in the file name selection criterion, then the match is made as if the criterion contained characters trailing a literal. The (asterisk) character matches an entire file name. A null or empty specification criterion also selects all file names. For example, .abc or .abc match any file with an extension of abc. ., , or empty string match all files in a directory. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **streamDownload** (consumer) | Sets the download method to use when not using a local working directory. If set to true, the remote files are streamed to the route as they are read. When set to false, the remote files are loaded into memory before being sent into the route. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **download** (consumer (advanced)) | Whether the SMB consumer should download the file. If this option is set to false, then the message body will be null, but the consumer will still trigger a Camel Exchange that has details about the file such as file name, file size, etc. It’s just that the file will not be downloaded. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **inProgressRepository** (consumer (advanced)) | A pluggable in-progress repository org.apache.camel.spi.IdempotentRepository. The in-progress repository is used to account the current in progress files being consumed. By default a memory based repository is used. |  | IdempotentRepository |
| **localWorkDirectory** (consumer (advanced)) | When consuming, a local work directory can be used to store the remote file content directly in local files, to avoid loading the content into memory. This is beneficial, if you consume a very big remote file and thus can conserve memory. |  | String |
| **onCompletionExceptionHandler** (consumer (advanced)) | To use a custom org.apache.camel.spi.ExceptionHandler to handle any thrown exceptions that happens during the file on completion process where the consumer does either a commit or rollback. The default implementation will log any exception at WARN level and ignore. |  | ExceptionHandler |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **processStrategy** (consumer (advanced)) | A pluggable org.apache.camel.component.file.GenericFileProcessStrategy allowing you to implement your own readLock option or similar. Can also be used when special conditions must be met before a file can be consumed, such as a special ready file exists. If this option is set then the readLock option does not apply. |  | GenericFileProcessStrategy |
| **startingDirectoryMustExist** (consumer (advanced)) | Whether the starting directory must exist. Mind that the autoCreate option is default enabled, which means the starting directory is normally auto created if it doesn’t exist. You can disable autoCreate and enable this to ensure the starting directory must exist. Will throw an exception if the directory doesn’t exist. | false | boolean |
| **throwExceptionOnConnectFailed** (consumer (advanced)) | Should an exception be thrown if connection failed (exhausted). By default exception is not thrown and a WARN is logged. You can use this to enable exception being thrown and handle the thrown exception from the PollingConsumerPollStrategy rollback method. | false | boolean |
| **checksumFileAlgorithm** (producer) | 

If provided, then Camel will calculate a checksum from the file that has been written, and store the result in the CamelFileChecksum header.

Enum values:

-   MD2
    
-   MD5
    
-   SHA\_1
    
-   SHA\_224
    
-   SHA\_256
    
-   SHA\_384
    
-   SHA\_512
    
-   SHA\_512\_224
    
-   SHA\_512\_256
    
-   SHA3\_224
    
-   SHA3\_256
    
-   SHA3\_384
    
-   SHA3\_512
    





 |  | String |
| **checksumWriteFile** (producer) | If checksumFileAlgorithm has been configured then this option controls whether to write a checksum file as well or not. The checksum file will always be written in the same folder as the original file. | true | boolean |
| **fileExist** (producer) | 

What to do if a file already exists with the same name. Override, which is the default, replaces the existing file. - Append - adds content to the existing file. - Fail - throws a GenericFileOperationException, indicating that there is already an existing file. - Ignore - silently ignores the problem and does not override the existing file, but assumes everything is okay. - Move - option requires to use the moveExisting option to be configured as well. The option eagerDeleteTargetFile can be used to control what to do if an moving the file, and there exists already an existing file, otherwise causing the move operation to fail. The Move option will move any existing files, before writing the target file. - TryRename is only applicable if tempFileName option is in use. This allows to try renaming the file from the temporary name to the actual name, without doing any exists check. This check may be faster on some file systems and especially FTP servers.

Enum values:

-   Override
    
-   Append
    
-   Fail
    
-   Ignore
    
-   Move
    
-   TryRename
    





 | Override | GenericFileExist |
| **flatten** (producer) | Flatten is used to flatten the file name path to strip any leading paths, so it’s just the file name. This allows you to consume recursively into sub-directories, but when you eg write the files to another directory they will be written in a single directory. Setting this to true on the producer enforces that any file name in CamelFileName header will be stripped for any leading paths. | false | boolean |
| **moveExisting** (producer) | Expression (such as File Language) used to compute file name to use when fileExist=Move is configured. To move files into a backup subdirectory just enter backup. This option only supports the following File Language tokens: file:name, file:name.ext, file:name.noext, file:onlyname, file:onlyname.noext, file:ext, and file:parent. Notice the file:parent is not supported by the FTP component, as the FTP component can only move any existing files to a relative directory based on current dir as base. |  | String |
| **tempFileName** (producer) | The same as tempPrefix option but offering a more fine grained control on the naming of the temporary filename as it uses the File Language. The location for tempFilename is relative to the final file location in the option 'fileName', not the target directory in the base uri. For example if option fileName includes a directory prefix: dir/finalFilename then tempFileName is relative to that subdirectory dir. |  | String |
| **tempPrefix** (producer) | This option is used to write the file using a temporary name and then, after the write is complete, rename it to the real name. Can be used to identify files being written and also avoid consumers (not using exclusive read locks) reading in progress files. Is often used by FTP when uploading big files. |  | String |
| **allowNullBody** (producer (advanced)) | Used to specify if a null body is allowed during file writing. If set to true then an empty file will be created, when set to false, and attempting to send a null body to the file component, a GenericFileWriteException of 'Cannot write null body to file.' will be thrown. If the fileExist option is set to 'Override', then the file will be truncated, and if set to append the file will remain unchanged. | false | boolean |
| **disconnectOnBatchComplete** (producer (advanced)) | Whether or not to disconnect from remote SMB share right after a Batch upload is complete. disconnectOnBatchComplete will only disconnect the current connection to the SMB share. | false | boolean |
| **eagerDeleteTargetFile** (producer (advanced)) | Whether or not to eagerly delete any existing target file. This option only applies when you use fileExists=Override and the tempFileName option as well. You can use this to disable (set it to false) deleting the target file before the temp file is written. For example you may write big files and want the target file to exists during the temp file is being written. This ensure the target file is only deleted until the very last moment, just before the temp file is being renamed to the target filename. This option is also used to control whether to delete any existing files when fileExist=Move is enabled, and an existing file exists. If this option copyAndDeleteOnRenameFails false, then an exception will be thrown if an existing file existed, if its true, then the existing file is deleted before the move operation. | true | boolean |
| **keepLastModified** (producer (advanced)) | Will keep the last modified timestamp from the source file (if any). Will use the FileConstants.FILE\_LAST\_MODIFIED header to located the timestamp. This header can contain either a java.util.Date or long with the timestamp. If the timestamp exists and the option is enabled it will set this timestamp on the written file. Note: This option only applies to the file producer. You cannot use this option with any of the ftp producers. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **moveExistingFileStrategy** (producer (advanced)) | Strategy (Custom Strategy) used to move file with special naming token to use when fileExist=Move is configured. By default, there is an implementation used if no custom strategy is provided. |  | FileMoveExistingStrategy |
| **renameUsingCopy** (producer (advanced)) | Perform rename operations using a copy and delete strategy. This option takes precedence over the copyAndDeleteOnRenameFail parameter that will automatically fall back to the copy and delete strategy, but only after additional delays. | false | boolean |
| **autoCreate** (advanced) | Automatically create missing directories in the file’s pathname. For the file consumer, that means creating the starting directory. For the file producer, it means the directory the files should be written to. | true | boolean |
| **browseLimit** (advanced) | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | int |
| **bufferSize** (advanced) | Buffer size in bytes used for writing files (or in case of FTP for downloading and uploading files). | 131072 | int |
| **copyAndDeleteOnRenameFail** (advanced) | Whether to fall back and do a copy and delete file, in case the file could not be renamed directly. | false | boolean |
| **smbConfig** (advanced) | **Autowired** An optional SMB client configuration, can be used to configure client specific configurations, like timeouts. |  | SmbConfig |
| **antExclude** (filter) | Ant style filter exclusion. If both antInclude and antExclude are used, antExclude takes precedence over antInclude. Multiple exclusions may be specified in comma-delimited format. |  | String |
| **antFilterCaseSensitive** (filter) | Sets case sensitive flag on ant filter. | true | boolean |
| **antInclude** (filter) | Ant style filter inclusion. Multiple inclusions may be specified in comma-delimited format. |  | String |
| **eagerMaxMessagesPerPoll** (filter) | Allows for controlling whether the limit from maxMessagesPerPoll is eager or not. If eager then the limit is during the scanning of files. Where as false would scan all files, and then perform sorting. Setting this option to false allows for sorting all files first, and then limit the poll. Mind that this requires a higher memory usage as all file details are in memory to perform the sorting. | true | boolean |
| **exclude** (filter) | Is used to exclude files, if filename matches the regex pattern (matching is case in-sensitive). Notice if you use symbols such as plus sign and others you would need to configure this using the RAW() syntax if configuring this as an endpoint uri. See more details at configuring endpoint uris. |  | String |
| **excludeExt** (filter) | Is used to exclude files matching file extension name (case insensitive). For example to exclude bak files, then use excludeExt=bak. Multiple extensions can be separated by comma, for example to exclude bak and dat files, use excludeExt=bak,dat. Note that the file extension includes all parts, for example having a file named mydata.tar.gz will have extension as tar.gz. For more flexibility then use the include/exclude options. |  | String |
| **filter** (filter) | Pluggable filter as a org.apache.camel.component.file.GenericFileFilter class. Will skip files if filter returns false in its accept() method. |  | GenericFileFilter |
| **filterDirectory** (filter) | Filters the directory based on Simple language. For example to filter on current date, you can use a simple date pattern such as $\\{date:now:yyyMMdd}. |  | String |
| **filterFile** (filter) | Filters the file based on Simple language. For example to filter on file size, you can use $\\{file:size} 5000. |  | String |
| **idempotent** (filter) | Option to use the Idempotent Consumer EIP pattern to let Camel skip already processed files. Will by default use a memory based LRUCache that holds 1000 entries. If noop=true then idempotent will be enabled as well to avoid consuming the same files over and over again. | false | Boolean |
| **idempotentEager** (filter) | Sets whether to eagerly add the filename to the idempotent repository or wait until the exchange is complete. | true | Boolean |
| **idempotentKey** (filter) | To use a custom idempotent key. By default the absolute path of the file is used. You can use the File Language, for example to use the file name and file size, you can do: idempotentKey=$\\{file:name}-$\\{file:size}. |  | String |
| **idempotentRepository** (filter) | A pluggable repository org.apache.camel.spi.IdempotentRepository which by default use MemoryIdempotentRepository if none is specified and idempotent is true. |  | IdempotentRepository |
| **include** (filter) | Is used to include files, if filename matches the regex pattern (matching is case in-sensitive). Notice if you use symbols such as plus sign and others you would need to configure this using the RAW() syntax if configuring this as an endpoint uri. See more details at configuring endpoint uris. |  | String |
| **includeExt** (filter) | Is used to include files matching file extension name (case insensitive). For example to include txt files, then use includeExt=txt. Multiple extensions can be separated by comma, for example to include txt and xml files, use includeExt=txt,xml. Note that the file extension includes all parts, for example having a file named mydata.tar.gz will have extension as tar.gz. For more flexibility then use the include/exclude options. |  | String |
| **maxDepth** (filter) | The maximum depth to traverse when recursively processing a directory. | 2147483647 | int |
| **maxMessagesPerPoll** (filter) | To define a maximum messages to gather per poll. By default no maximum is set. Can be used to set a limit of e.g. 1000 to avoid when starting up the server that there are thousands of files. Set a value of 0 or negative to disabled it. Notice: If this option is in use then the File and FTP components will limit before any sorting. For example if you have 100000 files and use maxMessagesPerPoll=500, then only the first 500 files will be picked up, and then sorted. You can use the eagerMaxMessagesPerPoll option and set this to false to allow to scan all files first and then sort afterwards. |  | int |
| **minDepth** (filter) | The minimum depth to start processing when recursively processing a directory. Using minDepth=1 means the base directory. Using minDepth=2 means the first sub directory. |  | int |
| **move** (filter) | Expression (such as Simple Language) used to dynamically set the filename when moving it after processing. To move files into a .done subdirectory just enter .done. |  | String |
| **exclusiveReadLockStrategy** (lock) | Pluggable read-lock as a org.apache.camel.component.file.GenericFileExclusiveReadLockStrategy implementation. |  | GenericFileExclusiveReadLockStrategy |
| **readLock** (lock) | 

Used by consumer, to only poll the files if it has exclusive read-lock on the file (i.e. the file is not in-progress or being written). Camel will wait until the file lock is granted. This option provides the build in strategies: - none - No read lock is in use - markerFile - Camel creates a marker file (fileName.camelLock) and then holds a lock on it. This option is not available for the FTP component - changed - Changed is using file length/modification timestamp to detect whether the file is currently being copied or not. Will at least use 1 sec to determine this, so this option cannot consume files as fast as the others, but can be more reliable as the JDK IO API cannot always determine whether a file is currently being used by another process. The option readLockCheckInterval can be used to set the check frequency. - fileLock - is for using java.nio.channels.FileLock. This option is not avail for Windows OS and the FTP component. This approach should be avoided when accessing a remote file system via a mount/share unless that file system supports distributed file locks. - rename - rename is for using a try to rename the file as a test if we can get exclusive read-lock. - idempotent - (only for file component) idempotent is for using a idempotentRepository as the read-lock. This allows to use read locks that supports clustering if the idempotent repository implementation supports that. - idempotent-changed - (only for file component) idempotent-changed is for using a idempotentRepository and changed as the combined read-lock. This allows to use read locks that supports clustering if the idempotent repository implementation supports that. - idempotent-rename - (only for file component) idempotent-rename is for using a idempotentRepository and rename as the combined read-lock. This allows to use read locks that supports clustering if the idempotent repository implementation supports that.Notice: The various read locks is not all suited to work in clustered mode, where concurrent consumers on different nodes is competing for the same files on a shared file system. The markerFile using a close to atomic operation to create the empty marker file, but its not guaranteed to work in a cluster. The fileLock may work better but then the file system need to support distributed file locks, and so on. Using the idempotent read lock can support clustering if the idempotent repository supports clustering, such as Hazelcast Component or Infinispan.

Enum values:

-   none
    
-   markerFile
    
-   fileLock
    
-   rename
    
-   changed
    
-   idempotent
    
-   idempotent-changed
    
-   idempotent-rename
    





 | none | String |
| **readLockCheckInterval** (lock) | Interval in millis for the read-lock, if supported by the read lock. This interval is used for sleeping between attempts to acquire the read lock. For example when using the changed read lock, you can set a higher interval period to cater for slow writes. The default of 1 sec. may be too fast if the producer is very slow writing the file. Notice: For FTP the default readLockCheckInterval is 5000. The readLockTimeout value must be higher than readLockCheckInterval, but a rule of thumb is to have a timeout that is at least 2 or more times higher than the readLockCheckInterval. This is needed to ensure that ample time is allowed for the read lock process to try to grab the lock before the timeout was hit. | 1000 | long |
| **readLockDeleteOrphanLockFiles** (lock) | Whether or not read lock with marker files should upon startup delete any orphan read lock files, which may have been left on the file system, if Camel was not properly shutdown (such as a JVM crash). If turning this option to false then any orphaned lock file will cause Camel to not attempt to pickup that file, this could also be due another node is concurrently reading files from the same shared directory. | true | boolean |
| **readLockLoggingLevel** (lock) | 

Logging level used when a read lock could not be acquired. By default a DEBUG is logged. You can change this level, for example to OFF to not have any logging. This option is only applicable for readLock of types: changed, fileLock, idempotent, idempotent-changed, idempotent-rename, rename.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | DEBUG | LoggingLevel |
| **readLockMarkerFile** (lock) | Whether to use marker file with the changed, rename, or exclusive read lock types. By default a marker file is used as well to guard against other processes picking up the same files. This behavior can be turned off by setting this option to false. For example if you do not want to write marker files to the file systems by the Camel application. | true | boolean |
| **readLockMinAge** (lock) | This option is applied only for readLock=changed. It allows to specify a minimum age the file must be before attempting to acquire the read lock. For example use readLockMinAge=300s to require the file is at last 5 minutes old. This can speedup the changed read lock as it will only attempt to acquire files which are at least that given age. | 0 | long |
| **readLockMinLength** (lock) | This option is applied only for readLock=changed. It allows you to configure a minimum file length. By default Camel expects the file to contain data, and thus the default value is 1. You can set this option to zero, to allow consuming zero-length files. | 1 | long |
| **readLockRemoveOnCommit** (lock) | This option is applied only for readLock=idempotent. It allows to specify whether to remove the file name entry from the idempotent repository when processing the file is succeeded and a commit happens. By default the file is not removed which ensures that any race-condition do not occur so another active node may attempt to grab the file. Instead the idempotent repository may support eviction strategies that you can configure to evict the file name entry after X minutes - this ensures no problems with race conditions. See more details at the readLockIdempotentReleaseDelay option. | false | boolean |
| **readLockRemoveOnRollback** (lock) | This option is applied only for readLock=idempotent. It allows to specify whether to remove the file name entry from the idempotent repository when processing the file failed and a rollback happens. If this option is false, then the file name entry is confirmed (as if the file did a commit). | true | boolean |
| **readLockTimeout** (lock) | Optional timeout in millis for the read-lock, if supported by the read-lock. If the read-lock could not be granted and the timeout triggered, then Camel will skip the file. At next poll Camel, will try the file again, and this time maybe the read-lock could be granted. Use a value of 0 or lower to indicate forever. Currently fileLock, changed and rename support the timeout. Notice: For FTP the default readLockTimeout value is 20000 instead of 10000. The readLockTimeout value must be higher than readLockCheckInterval, but a rule of thumb is to have a timeout that is at least 2 or more times higher than the readLockCheckInterval. This is needed to ensure that ample time is allowed for the read lock process to try to grab the lock before the timeout was hit. | 10000 | long |
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
| **domain** (security) | The user domain. |  | String |
| **password** (security) | The password to access the share. |  | String |
| **username** (security) | The username required to access the share. |  | String |
| **shuffle** (sort) | To shuffle the list of files (sort in random order). | false | boolean |
| **sortBy** (sort) | Built-in sort by using the File Language. Supports nested sorts, so you can have a sort by file name and as a 2nd group sort by modified date. |  | String |
| **sorter** (sort) | Pluggable sorter as a java.util.Comparator class. |  | Comparator |

## Message Headers

The SMB component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelFileLength** (consumer) Constant: [`FILE_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_LENGTH) | A long value containing the file size. |  | long |
| **CamelFileLastModified** (consumer) Constant: [`FILE_LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_LAST_MODIFIED) | A Long value containing the last modified timestamp of the file. |  | long |
| **CamelFileNameOnly** (consumer) Constant: [`FILE_NAME_ONLY`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_NAME_ONLY) | Only the file name (the name with no leading paths). |  | String |
| **CamelFileName** (common) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_NAME) | (producer) Specifies the name of the file to write (relative to the endpoint directory). This name can be a String; a String with a file or simple Language expression; or an Expression object. If it’s null then Camel will auto-generate a filename based on the message unique ID. (consumer) Name of the consumed file as a relative file path with offset from the starting directory configured on the endpoint. |  | String |
| **CamelFileNameConsumed** (consumer) Constant: [`FILE_NAME_CONSUMED`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_NAME_CONSUMED) | The name of the file that has been consumed. |  | String |
| **CamelFileAbsolute** (consumer) Constant: [`FILE_ABSOLUTE`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_ABSOLUTE) | A boolean option specifying whether the consumed file denotes an absolute path or not. Should normally be false for relative paths. Absolute paths should normally not be used but we added to the move option to allow moving files to absolute paths. But can be used elsewhere as well. |  | Boolean |
| **CamelFileAbsolutePath** (consumer) Constant: [`FILE_ABSOLUTE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_ABSOLUTE_PATH) | The absolute path to the file. For relative files this path holds the relative path instead. |  | String |
| **CamelFilePath** (consumer) Constant: [`FILE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_PATH) | The file path. For relative files this is the starting directory. For absolute files this is the absolute path. |  | String |
| **CamelFileRelativePath** (consumer) Constant: [`FILE_RELATIVE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_RELATIVE_PATH) | The relative path. |  | String |
| **CamelFileParent** (common) Constant: [`FILE_PARENT`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_PARENT) | The parent path. |  | String |
| **CamelFileNameProduced** (producer) Constant: [`FILE_NAME_PRODUCED`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_NAME_PRODUCED) | The actual absolute filepath (path name) for the output file that was written. This header is set by Camel and its purpose is providing end-users with the name of the file that was written. |  | String |
| **CamelOverruleFileName** (producer) Constant: [`OVERRULE_FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#OVERRULE_FILE_NAME) | Is used for overruling CamelFileName header and use the value instead (but only once, as the producer will remove this header after writing the file). The value can be only be a String. Notice that if the option fileName has been configured, then this is still being evaluated. |  | Object |
| **CamelFileHost** (consumer) Constant: [`FILE_HOST`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_HOST) | The remote hostname. |  | String |
| **CamelSmbFileInputStream** (consumer) Constant: [`SMB_FILE_INPUT_STREAM`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#SMB_FILE_INPUT_STREAM) | The remote file input stream. |  | InputStream |
| **CamelFileLocalWorkPath** (common) Constant: [`FILE_LOCAL_WORK_PATH`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#FILE_LOCAL_WORK_PATH) | Path to the local work file, if local work directory is used. |  | String |
| **CamelSmbFileExists** (producer) Constant: [`SMB_FILE_EXISTS`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#SMB_FILE_EXISTS) | 
**Deprecated** The expected behavior if the file already exists.

Enum values:

-   Override
    
-   Append
    
-   Fail
    
-   Ignore
    
-   Move
    
-   TryRename
    





 |  | GenericFileExist |
| **CamelSmbUncPath** (consumer) Constant: [`SMB_UNC_PATH`](https://javadoc.io/doc/org.apache.camel/camel-smb/latest/org/apache/camel/component/smb/SmbConstants.html#SMB_UNC_PATH) | UNC path to the retrieved file. |  | String |

## Producer

For the SMB producer to operate correctly, the header `Exchange.FILE_NAME` has to be included in the exchange.

## Examples

### Polling files

For instance, polling all the files from an SMB file share and reading their contents would look like this:

_Java-only: uses fromF with string formatting and method reference Processor_

```java
private void process(Exchange exchange) throws IOException {
    final byte[] data = exchange.getMessage().getBody(byte[].class);
    LOG.debug("Read exchange as bytes with contents: {}", new String(data));
}

public void configure() {
    fromF("smb:%s/%s?username=%s&password=%s", service.address(), service.shareName(), service.userName(), service.password())
        .process(this::process)
        .to("mock:result");
}
```

> **Note**
> you may also get the file contents as an InputStream using `exchange.getMessage().getBody(InputStream.class)`.

### Polling files (advanced)

You can also get access to the file using the underlying `File` implementation provided by Camel. In that case, polling all the files from an SMB file share and reading their contents would look like this:

_Java-only: uses SmbFile class, type casts, fromF with string formatting, and method reference Processor_

```java
private void process(Exchange exchange) throws IOException {
    final org.apache.camel.component.smb.SmbFile file = exchange.getMessage().getBody(org.apache.camel.component.smb.SmbFile.class);
    LOG.debug("Read exchange: {}, with contents: {}", file.getFile(), new String((byte[]) file.getBody()));
}

public void configure() {
    fromF("smb:%s/%s?username=%s&password=%s", service.address(), service.shareName(), service.userName(), service.password())
        .process(this::process)
        .to("mock:result");
}
```

> **Note**
> Beware that the File object provided is not a `java.io.File` instance, but, instead a `org.apache.camel.component.smb.SmbFile` instance that extends Camel’s `GenericFile`. Relying on the underlying implementation may make your code more susceptible to problems between version upgrades of the library used to implement this component.
>
> To maintain backward compatibility, a new Camel Header `CamelSmbUncPath` has been introduced that provides the full absolute path when a File is consumed from the SMB server.

## Permissions

The Camel SMB component requires the authenticated user to have appropriate permissions on the SMB share. The exact permissions depend on the operations being performed:

-   **Reading files**: requires `Read Data` permission on the file.
    
-   **Writing files**: requires `Write Data` permission on the file and `Create Files` on the parent directory.
    
-   **Deleting files** (e.g., when using `delete=true` on a consumer): requires `Delete` permission on the file.
    

### STATUS\_ACCESS\_DENIED (0xc0000022) when deleting files

If you receive a `STATUS_ACCESS_DENIED` error when the consumer attempts to delete a file after processing, the most common causes are:

1.  **The authenticated user lacks the DELETE permission** on the file or the parent directory. Ensure the SMB user has been granted the `Delete` and `Delete Child` permissions.
    
2.  **The server’s volume uses UNIX security style instead of NTFS**. Some storage systems (such as NetApp ONTAP, TrueNAS, or other unified NAS platforms) support multiple volume security styles. When a volume uses UNIX security style, the server ignores NTFS ACLs and evaluates only UNIX file ownership and mode bits (`chmod`/`chown`). In this case, even if the Windows "Effective Access" UI shows full permissions, the delete operation can still be denied because the NTFS ACLs shown are not the actual access control mechanism.
    

To resolve this, either:

-   Change the volume security style to NTFS so that NTFS ACLs are evaluated, or
    
-   Ensure the UNIX file ownership and mode bits grant the SMB user delete access on the files and their parent directory.