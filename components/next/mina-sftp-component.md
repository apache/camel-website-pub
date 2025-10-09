# MINA SFTP

**Since Camel 4.18**

**Both producer and consumer are supported**

The MINA SFTP component provides access to remote file systems over the SFTP protocol using Apache MINA SSHD library.

This component is designed as a near drop-in replacement for the JSch-based `sftp` component, requiring only a URI scheme change from `sftp://` to `mina-sftp://`. Most configuration options remain the same for supported features.

## URI format

mina-sftp://\[username@\]host\[:port\]/directoryName\[?options\]

Where **directoryName** represents the underlying directory. The directory name is a relative path.

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

The MINA SFTP component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The MINA SFTP endpoint is configured using URI syntax:

mina-sftp:host:port/directoryName

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | **Required** Hostname of the FTP server. |  | String |
| **port** (common) | Port of the FTP server. |  | int |
| **directoryName** (common) | The starting directory. |  | String |

### Query Parameters (137 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **binary** (common) | Specifies the file transfer mode, BINARY or ASCII. Default is ASCII (false). | false | boolean |
| **charset** (common) | This option is used to specify the encoding of the file. You can use this on the consumer, to specify the encodings of the files, which allow Camel to know the charset it should load the file content in case the file content is being accessed. Likewise when writing a file, you can use this option to specify which charset to write the file as well. Do mind that when writing the file Camel may have to read the message content into memory to be able to convert the data into the configured charset, so do not use this if you have big messages. |  | String |
| **disconnect** (common) | Whether or not to disconnect from remote FTP server right after use. Disconnect will only disconnect the current connection to the FTP server. If you have a consumer which you want to stop, then you need to stop the consumer/route instead. | false | boolean |
| **doneFileName** (common) | Producer: If provided, then Camel will write a 2nd done file when the original file has been written. The done file will be empty. This option configures what file name to use. Either you can specify a fixed name. Or you can use dynamic placeholders. The done file will always be written in the same folder as the original file. Consumer: If provided, Camel will only consume files if a done file exists. This option configures what file name to use. Either you can specify a fixed name. Or you can use dynamic placeholders.The done file is always expected in the same folder as the original file. Only $\\{file.name} and $\\{file.name.next} is supported as dynamic placeholders. |  | String |
| **fileName** (common) | Use Expression such as File Language to dynamically set the filename. For consumers, it’s used as a filename filter. For producers, it’s used to evaluate the filename to write. If an expression is set, it take precedence over the CamelFileName header. (Note: The header itself can also be an Expression). The expression options support both String and Expression types. If the expression is a String type, it is always evaluated using the File Language. If the expression is an Expression type, the specified Expression type is used - this allows you, for instance, to use OGNL expressions. For the consumer, you can use it to filter filenames, so you can for instance consume today’s file using the File Language syntax: mydata-$\\{date:now:yyyyMMdd}.txt. The producers support the CamelOverruleFileName header which takes precedence over any existing CamelFileName header; the CamelOverruleFileName is a header that is used only once, and makes it easier as this avoids to temporary store CamelFileName and have to restore it afterwards. |  | String |
| **passiveMode** (common) | Sets passive mode connections. Default is active mode connections. | false | boolean |
| **separator** (common) | 
Sets the path separator to be used. UNIX = Uses unix style path separator Windows = Uses windows style path separator Auto = (is default) Use existing path separator in file name.

Enum values:

-   UNIX
    
-   Windows
    
-   Auto
    





 | UNIX | PathSeparator |
| **fastExistsCheck** (common (advanced)) | If set this option to be true, camel-ftp will use the list file directly to check if the file exists. Since some FTP server may not support to list the file directly, if the option is false, camel-ftp will use the old way to list the directory and check if the file exists. This option also influences readLock=changed to control whether it performs a fast check to update file information or not. This can be used to speed up the process if the FTP server has a lot of files. | false | boolean |
| **delete** (consumer) | If true, the file will be deleted after it is processed successfully. | false | boolean |
| **moveFailed** (consumer) | Sets the move failure expression based on Simple language. For example, to move files into a .error subdirectory use: .error. Note: When moving the files to the fail location Camel will handle the error and will not pick up the file again. |  | String |
| **noop** (consumer) | If true, the file is not moved or deleted in any way. This option is good for readonly data, or for ETL type requirements. If noop=true, Camel will set idempotent=true as well, to avoid consuming the same files over and over again. | false | boolean |
| **preMove** (consumer) | Expression (such as File Language) used to dynamically set the filename when moving it before processing. For example to move in-progress files into the order directory set this value to order. |  | String |
| **preSort** (consumer) | When pre-sort is enabled then the consumer will sort the file and directory names during polling, that was retrieved from the file system. You may want to do this in case you need to operate on the files in a sorted order. The pre-sort is executed before the consumer starts to filter, and accept files to process by Camel. This option is default=false meaning disabled. | false | boolean |
| **recursive** (consumer) | If a directory, will look for files in all the sub-directories as well. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **streamDownload** (consumer) | Sets the download method to use when not using a local working directory. If set to true, the remote files are streamed to the route as they are read. When set to false, the remote files are loaded into memory before being sent into the route. If enabling this option then you must set stepwise=false as both cannot be enabled at the same time. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **download** (consumer (advanced)) | Whether the FTP consumer should download the file. If this option is set to false, then the message body will be null, but the consumer will still trigger a Camel Exchange that has details about the file such as file name, file size, etc. It’s just that the file will not be downloaded. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **ignoreFileNotFoundOrPermissionError** (consumer (advanced)) | Whether to ignore when (trying to list files in directories or when downloading a file), which does not exist or due to permission error. By default when a directory or file does not exist or insufficient permission, then an exception is thrown. Setting this option to true allows to ignore that instead. | false | boolean |
| **inProgressRepository** (consumer (advanced)) | A pluggable in-progress repository org.apache.camel.spi.IdempotentRepository. The in-progress repository is used to account the current in progress files being consumed. By default a memory based repository is used. |  | IdempotentRepository |
| **localWorkDirectory** (consumer (advanced)) | When consuming, a local work directory can be used to store the remote file content directly in local files, to avoid loading the content into memory. This is beneficial, if you consume a very big remote file and thus can conserve memory. |  | String |
| **onCompletionExceptionHandler** (consumer (advanced)) | To use a custom org.apache.camel.spi.ExceptionHandler to handle any thrown exceptions that happens during the file on completion process where the consumer does either a commit or rollback. The default implementation will log any exception at WARN level and ignore. |  | ExceptionHandler |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **processStrategy** (consumer (advanced)) | A pluggable org.apache.camel.component.file.GenericFileProcessStrategy allowing you to implement your own readLock option or similar. Can also be used when special conditions must be met before a file can be consumed, such as a special ready file exists. If this option is set then the readLock option does not apply. |  | GenericFileProcessStrategy |
| **throwExceptionOnConnectFailed** (consumer (advanced)) | Should an exception be thrown if connection failed (exhausted)By default exception is not thrown and a WARN is logged. You can use this to enable exception being thrown and handle the thrown exception from the org.apache.camel.spi.PollingConsumerPollStrategy rollback method. | false | boolean |
| **useList** (consumer (advanced)) | Whether to allow using LIST command when downloading a file. Default is true. In some use cases you may want to download a specific file and are not allowed to use the LIST command, and therefore you can set this option to false. Notice when using this option, then the specific file to download does not include meta-data information such as file size, timestamp, permissions etc, because those information is only possible to retrieve when LIST command is in use. | true | boolean |
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
| **jailStartingDirectory** (producer) | Used for jailing (restricting) writing files to the starting directory (and sub) only. This is enabled by default to not allow Camel to write files to outside directories (to be more secured out of the box). You can turn this off to allow writing files to directories outside the starting directory, such as parent or root folders. | true | boolean |
| **moveExisting** (producer) | Expression (such as File Language) used to compute file name to use when fileExist=Move is configured. To move files into a backup subdirectory just enter backup. This option only supports the following File Language tokens: file:name, file:name.ext, file:name.noext, file:onlyname, file:onlyname.noext, file:ext, and file:parent. Notice the file:parent is not supported by the FTP component, as the FTP component can only move any existing files to a relative directory based on current dir as base. |  | String |
| **tempFileName** (producer) | The same as tempPrefix option but offering a more fine grained control on the naming of the temporary filename as it uses the File Language. The location for tempFilename is relative to the final file location in the option 'fileName', not the target directory in the base uri. For example if option fileName includes a directory prefix: dir/finalFilename then tempFileName is relative to that subdirectory dir. |  | String |
| **tempPrefix** (producer) | This option is used to write the file using a temporary name and then, after the write is complete, rename it to the real name. Can be used to identify files being written and also avoid consumers (not using exclusive read locks) reading in progress files. Is often used by FTP when uploading big files. |  | String |
| **allowNullBody** (producer (advanced)) | Used to specify if a null body is allowed during file writing. If set to true then an empty file will be created, when set to false, and attempting to send a null body to the file component, a GenericFileWriteException of 'Cannot write null body to file.' will be thrown. If the fileExist option is set to 'Override', then the file will be truncated, and if set to append the file will remain unchanged. | false | boolean |
| **chmod** (producer (advanced)) | Allows you to set chmod on the stored file. For example chmod=640. |  | String |
| **chmodDirectory** (producer (advanced)) | Allows you to set chmod during path creation. For example chmod=640. |  | String |
| **disconnectOnBatchComplete** (producer (advanced)) | Whether or not to disconnect from remote FTP server right after a Batch upload is complete. disconnectOnBatchComplete will only disconnect the current connection to the FTP server. | false | boolean |
| **eagerDeleteTargetFile** (producer (advanced)) | Whether or not to eagerly delete any existing target file. This option only applies when you use fileExists=Override and the tempFileName option as well. You can use this to disable (set it to false) deleting the target file before the temp file is written. For example you may write big files and want the target file to exists during the temp file is being written. This ensure the target file is only deleted until the very last moment, just before the temp file is being renamed to the target filename. This option is also used to control whether to delete any existing files when fileExist=Move is enabled, and an existing file exists. If this option copyAndDeleteOnRenameFails false, then an exception will be thrown if an existing file existed, if its true, then the existing file is deleted before the move operation. | true | boolean |
| **keepLastModified** (producer (advanced)) | Will keep the last modified timestamp from the source file (if any). Will use the FileConstants.FILE\_LAST\_MODIFIED header to located the timestamp. This header can contain either a java.util.Date or long with the timestamp. If the timestamp exists and the option is enabled it will set this timestamp on the written file. Note: This option only applies to the file producer. You cannot use this option with any of the ftp producers. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **moveExistingFileStrategy** (producer (advanced)) | Strategy (Custom Strategy) used to move file with special naming token to use when fileExist=Move is configured. By default, there is an implementation used if no custom strategy is provided. |  | FileMoveExistingStrategy |
| **sendNoop** (producer (advanced)) | Whether to send a noop command as a pre-write check before uploading files to the FTP server. This is enabled by default as a validation of the connection is still valid, which allows to silently re-connect to be able to upload the file. However if this causes problems, you can turn this option off. | true | boolean |
| **autoCreate** (advanced) | Automatically create missing directories in the file’s pathname. For the file consumer, that means creating the starting directory. For the file producer, it means the directory the files should be written to. | true | boolean |
| **bindAddress** (advanced) | Specifies the address of the local interface against which the connection should bind. |  | String |
| **browseLimit** (advanced) | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | int |
| **bulkRequests** (advanced) | Specifies how many requests may be outstanding at any one time. Increasing this value may slightly improve file transfer speed but will increase memory usage. |  | Integer |
| **compression** (advanced) | To use compression. Specify a level from 1 to 10. |  | int |
| **connectTimeout** (advanced) | Sets the connect timeout for waiting for a connection to be established Used by both FTPClient and JSCH. | 10000 | int |
| **existDirCheckUsingLs** (advanced) | **Deprecated** Deprecated: JSch-specific parameter, ignored by mina-sftp. MINA SSHD uses stat() for directory existence checks. | false | Boolean |
| **filenameEncoding** (advanced) | Encoding to use for FTP client when parsing filenames. By default, UTF-8 is used. |  | String |
| **jschLoggingLevel** (advanced) | **Deprecated** Deprecated: JSch-specific parameter, ignored by mina-sftp. Configure logging via your logging framework instead. |  | String |
| **maximumReconnectAttempts** (advanced) | Specifies the maximum reconnect attempts Camel performs when it tries to connect to the remote FTP server. Use 0 to disable this behavior. |  | int |
| **readBufferSize** (advanced) | Sets the buffer size in bytes used for reading data from SFTP connections. If not specified, the MINA SSHD default buffer size is used. Larger values may improve transfer speed for large files but will increase memory usage. Maximum recommended value is 126976 bytes (124KB) to avoid data corruption issues. This parameter maps directly to Apache MINA SSHD’s READ\_BUFFER\_SIZE property. |  | Integer |
| **reconnectDelay** (advanced) | Delay in millis Camel will wait before performing a reconnect attempt. | 1000 | long |
| **serverAliveCountMax** (advanced) | Sets the number of keep-alive messages which may be sent without receiving any messages back from the server. If this threshold is reached while keep-alive messages are being sent, the connection will be disconnected. The default value is one. | 1 | int |
| **serverAliveInterval** (advanced) | Sets the interval (millis) to send a keep-alive message. If zero is specified, any keep-alive message must not be sent. The default interval is zero. |  | int |
| **serverMessageLoggingLevel** (advanced) | **Deprecated** Deprecated: JSch-specific parameter, ignored by mina-sftp. Configure logging via your logging framework instead. |  | String |
| **soTimeout** (advanced) | Sets the so timeout FTP and FTPS Is the SocketOptions.SO\_TIMEOUT value in millis. Recommended option is to set this to 300000 so as not have a hanged connection. On SFTP this option is set as timeout on the JSCH Session instance. | 300000 | int |
| **stepwise** (advanced) | Sets whether we should stepwise change directories while traversing file structures when downloading files, or as well when uploading a file to a directory. You can disable this if you for example are in a situation where you cannot change directory on the FTP server due security reasons. Stepwise cannot be used together with streamDownload. | true | boolean |
| **timeout** (advanced) | Sets the data timeout for waiting for reply Used only by FTPClient. | 30000 | int |
| **writeBufferSize** (advanced) | Sets the buffer size in bytes used for writing data to SFTP connections. If not specified, the MINA SSHD default buffer size is used. Larger values may improve transfer speed for large files but will increase memory usage. Maximum recommended value is 126976 bytes (124KB) to avoid data corruption issues. This parameter maps directly to Apache MINA SSHD’s WRITE\_BUFFER\_SIZE property. |  | Integer |
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
| **readLockIdempotentReleaseAsync** (lock) | Whether the delayed release task should be synchronous or asynchronous. See more details at the readLockIdempotentReleaseDelay option. | false | boolean |
| **readLockIdempotentReleaseAsyncPoolSize** (lock) | The number of threads in the scheduled thread pool when using asynchronous release tasks. Using a default of 1 core threads should be sufficient in almost all use-cases, only set this to a higher value if either updating the idempotent repository is slow, or there are a lot of files to process. This option is not in-use if you use a shared thread pool by configuring the readLockIdempotentReleaseExecutorService option. See more details at the readLockIdempotentReleaseDelay option. |  | int |
| **readLockIdempotentReleaseDelay** (lock) | Whether to delay the release task for a period of millis. This can be used to delay the release tasks to expand the window when a file is regarded as read-locked, in an active/active cluster scenario with a shared idempotent repository, to ensure other nodes cannot potentially scan and acquire the same file, due to race-conditions. By expanding the time-window of the release tasks helps prevents these situations. Note delaying is only needed if you have configured readLockRemoveOnCommit to true. |  | int |
| **readLockIdempotentReleaseExecutorService** (lock) | To use a custom and shared thread pool for asynchronous release tasks. See more details at the readLockIdempotentReleaseDelay option. |  | ScheduledExecutorService |
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
| **autoCreateKnownHostsFile** (security) | If knownHostFile does not exist, then attempt to auto-create the path and file (beware that the file will be created by the current user of the running Java process, which may not have file permission). | false | boolean |
| **certBytes** (security) | Set the OpenSSH certificate as a byte array for certificate-based authentication. |  | byte\[\] |
| **certFile** (security) | Set the OpenSSH certificate file path for certificate-based authentication. |  | String |
| **certUri** (security) | Set the OpenSSH certificate (loaded from classpath by default) for certificate-based authentication. |  | String |
| **ciphers** (security) | Set the list of ciphers that will be used in order of preference. Possible cipher names are defined by Apache MINA SSHD. Some examples include: aes128-ctr,aes128-cbc,3des-ctr,3des-cbc,blowfish-cbc,aes192-cbc,aes256-cbc. If not specified the default list from MINA SSHD will be used. |  | String |
| **keyExchangeProtocols** (security) | Set the list of key exchange protocols that will be used in order of preference. If not specified the default list from MINA SSHD will be used. |  | String |
| **keyPair** (security) | Sets a key pair of the public and private key so to that the SFTP endpoint can do public/private key verification. |  | KeyPair |
| **knownHosts** (security) | Sets the known\_hosts from the byte array, so that the SFTP endpoint can do host key verification. |  | byte\[\] |
| **knownHostsFile** (security) | Sets the known\_hosts file, so that the SFTP endpoint can do host key verification. |  | String |
| **knownHostsUri** (security) | Sets the known\_hosts file (loaded from classpath by default), so that the SFTP endpoint can do host key verification. |  | String |
| **password** (security) | Password to use for login. |  | String |
| **preferredAuthentications** (security) | Set the preferred authentications which SFTP endpoint will used. Some example include: password,publickey. If not specified the default list will be used. |  | String |
| **privateKey** (security) | Set the private key as byte so that the SFTP endpoint can do private key verification. |  | byte\[\] |
| **privateKeyFile** (security) | Set the private key file so that the SFTP endpoint can do private key verification. |  | String |
| **privateKeyPassphrase** (security) | Set the private key file passphrase so that the SFTP endpoint can do private key verification. |  | String |
| **privateKeyUri** (security) | Set the private key file (loaded from classpath by default) so that the SFTP endpoint can do private key verification. |  | String |
| **publicKeyAcceptedAlgorithms** (security) | Set a comma separated list of public key accepted algorithms. If not specified the default list will be used. |  | String |
| **serverHostKeys** (security) | Set the list of algorithms supported for the server host key. Some examples include: ssh-dss,ssh-rsa,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521. If not specified the default list from MINA SSHD will be used. |  | String |
| **serverKeyVerifier** (security) | Custom ServerKeyVerifier for host key verification. When provided, this verifier is used exclusively, ignoring strictHostKeyChecking, knownHostsFile, and other host key options. |  | ServerKeyVerifier |
| **strictHostKeyChecking** (security) | 

Sets whether to use strict host key checking.

Enum values:

-   no
    
-   yes
    





 | no | String |
| **username** (security) | Username to use for login. |  | String |
| **useUserKnownHostsFile** (security) | If knownHostFile has not been explicit configured then use the host file from System.getProperty(user.home)/.ssh/known\_hosts. | true | boolean |
| **shuffle** (sort) | To shuffle the list of files (sort in random order). | false | boolean |
| **sortBy** (sort) | Built-in sort by using the File Language. Supports nested sorts, so you can have a sort by file name and as a 2nd group sort by modified date. |  | String |
| **sorter** (sort) | Pluggable sorter as a java.util.Comparator class. |  | Comparator |

## Message Headers

The MINA SFTP component supports 17 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelFileLength** (consumer) Constant: [`FILE_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_LENGTH) | A long value containing the file size. |  | long |
| **CamelFileLastModified** (consumer) Constant: [`FILE_LAST_MODIFIED`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_LAST_MODIFIED) | A Long value containing the last modified timestamp of the file. |  | long |
| **CamelFileNameOnly** (consumer) Constant: [`FILE_NAME_ONLY`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_NAME_ONLY) | Only the file name (the name with no leading paths). |  | String |
| **CamelFileName** (common) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_NAME) | (producer) Specifies the name of the file to write (relative to the endpoint directory). This name can be a String; a String with a file or simple Language expression; or an Expression object. If it’s null then Camel will auto-generate a filename based on the message unique ID. (consumer) Name of the consumed file as a relative file path with offset from the starting directory configured on the endpoint. |  | String |
| **CamelFileNameConsumed** (consumer) Constant: [`FILE_NAME_CONSUMED`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_NAME_CONSUMED) | The name of the file that has been consumed. |  | String |
| **CamelFileAbsolute** (consumer) Constant: [`FILE_ABSOLUTE`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_ABSOLUTE) | A boolean option specifying whether the consumed file denotes an absolute path or not. Should normally be false for relative paths. Absolute paths should normally not be used but we added to the move option to allow moving files to absolute paths. But can be used elsewhere as well. |  | Boolean |
| **CamelFileAbsolutePath** (consumer) Constant: [`FILE_ABSOLUTE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_ABSOLUTE_PATH) | The absolute path to the file. For relative files this path holds the relative path instead. |  | String |
| **CamelFilePath** (consumer) Constant: [`FILE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_PATH) | The file path. For relative files this is the starting directory. For absolute files this is the absolute path. |  | String |
| **CamelFileRelativePath** (consumer) Constant: [`FILE_RELATIVE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_RELATIVE_PATH) | The relative path. |  | String |
| **CamelFileParent** (common) Constant: [`FILE_PARENT`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_PARENT) | The parent path. |  | String |
| **CamelFileNameProduced** (producer) Constant: [`FILE_NAME_PRODUCED`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_NAME_PRODUCED) | The actual absolute filepath (path name) for the output file that was written. This header is set by Camel and its purpose is providing end-users with the name of the file that was written. |  | String |
| **CamelOverruleFileName** (producer) Constant: [`OVERRULE_FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#OVERRULE_FILE_NAME) | Is used for overruling CamelFileName header and use the value instead (but only once, as the producer will remove this header after writing the file). The value can be only be a String. Notice that if the option fileName has been configured, then this is still being evaluated. |  | Object |
| **CamelFileLocalWorkPath** (consumer) Constant: [`FILE_LOCAL_WORK_PATH`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_LOCAL_WORK_PATH) | Path to the local work file, if local work directory is used. |  | String |
| **CamelRemoteFileInputStream** (consumer) Constant: [`REMOTE_FILE_INPUT_STREAM`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#REMOTE_FILE_INPUT_STREAM) | The remote file input stream. |  | InputStream |
| **CamelFileHost** (consumer) Constant: [`FILE_HOST`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FILE_HOST) | The remote hostname. |  | String |
| **CamelFtpReplyCode** (common) Constant: [`FTP_REPLY_CODE`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FTP_REPLY_CODE) | The FTP client reply code. |  | int |
| **CamelFtpReplyString** (common) Constant: [`FTP_REPLY_STRING`](https://javadoc.io/doc/org.apache.camel/camel-mina-sftp/latest/org/apache/camel/component/file/remote/FtpConstants.html#FTP_REPLY_STRING) | The FTP client reply string. |  | String |

## Username Resolution

When no username is specified in the URI, the mina-sftp component follows the same username resolution order as the JSch-based camel-sftp component, matching standard SSH client behavior.

### Resolution Priority Order

  
| Priority | Source | Description |
| --- | --- | --- |
| 1 (highest) | URI parameter | Username specified directly in URI: `mina-sftp://myuser@host/path` |
| 2 | SSH config file | `User` directive in `~/.ssh/config` for the target host |
| 3 (lowest) | OS username | `System.getProperty("user.name")` - current operating system user |

### SSH Config Resolution

The component reads the user’s `~/.ssh/config` file (if it exists) and applies matching `Host` entries. For example:

```none
# ~/.ssh/config
Host myserver.example.com
    User deployuser

Host *.internal.example.com
    User admin

Host *
    User defaultuser
```

With this configuration: \* `mina-sftp://myserver.example.com/path` uses username `deployuser` \* `mina-sftp://app.internal.example.com/path` uses username `admin` \* `mina-sftp://other.example.com/path` uses username `defaultuser`

### OS Username Fallback

If the SSH config file exists but does not contain a `User` directive for the target host, the component falls back to the operating system username (`System.getProperty("user.name")`).

> **Important**
> The OS username fallback only occurs when the SSH config file exists. If no `~/.ssh/config` file exists at all, the connection will fail with "No username specified when the session was created".

### Explicit Username Recommended

For production deployments, always specify the username explicitly in the URI to ensure predictable behavior across different environments:

```java
// Recommended: explicit username
from("mina-sftp://deployuser@host/path?password=secret")
    .to("file:local");

// Not recommended: relies on SSH config or OS username
from("mina-sftp://host/path?password=secret")
    .to("file:local");
```

### Compatibility with camel-sftp

This username resolution behavior is identical to the JSch-based camel-sftp component, ensuring seamless migration. Both components:

-   Check the URI for an explicit username first
    
-   Fall back to `~/.ssh/config` if no username in URI
    
-   Fall back to OS username if SSH config exists but has no `User` directive
    

## Authentication

The MINA SFTP component supports multiple authentication methods:

### Password Authentication

```java
from("mina-sftp://admin@host/path?password=secret")
    .to("file:local");
```

### Public Key Authentication

#### Using Private Key File

```java
from("mina-sftp://user@host/path?privateKeyFile=/home/user/.ssh/id_rsa")
    .to("file:local");
```

#### Using Private Key from Classpath

```java
from("mina-sftp://user@host/path?privateKeyUri=classpath:keys/id_rsa")
    .to("file:local");
```

#### Using Encrypted Private Key

```java
from("mina-sftp://user@host/path?privateKeyFile=/path/to/encrypted_key&privateKeyPassphrase=mypassphrase")
    .to("file:local");
```

#### Using Direct KeyPair Object

```java
KeyPairGenerator keyGen = KeyPairGenerator.getInstance("RSA");
keyGen.initialize(2048);
KeyPair keyPair = keyGen.generateKeyPair();

MinaSftpEndpoint endpoint = context.getEndpoint(
    "mina-sftp://user@host/path", MinaSftpEndpoint.class);
MinaSftpConfiguration config = (MinaSftpConfiguration) endpoint.getConfiguration();
config.setKeyPair(keyPair);
```

### Authentication Priority

When both password and public key authentication are configured, the component will:

1.  Try public key authentication first
    
2.  Fall back to password authentication if public key fails
    

This behavior matches the JSch-based sftp component.

### Preferred Authentication Methods

You can customize the authentication order using the `preferredAuthentications` option:

```java
from("mina-sftp://user@host/path?password=secret&privateKeyFile=/path/to/key&preferredAuthentications=password,publickey")
    .to("file:local");
```

#### Available Authentication Methods

 
| Method | Description |
| --- | --- |
| `publickey` | Public key or certificate-based authentication |
| `password` | Password-based authentication |
| `keyboard-interactive` | Keyboard-interactive authentication (multi-factor scenarios) |

If `preferredAuthentications` is not specified, the default order from Apache MINA SSHD is used: publickey, keyboard-interactive, password.

### Public Key Accepted Algorithms

You can restrict which public key algorithms are accepted for authentication using the `publicKeyAcceptedAlgorithms` option:

```java
from("mina-sftp://user@host/path?privateKeyFile=/path/to/key&publicKeyAcceptedAlgorithms=ssh-ed25519,rsa-sha2-256,rsa-sha2-512")
    .to("file:local");
```

#### Available Public Key Algorithms

 
| Algorithm | Description |
| --- | --- |
| `ssh-ed25519` | Ed25519 algorithm (modern, recommended) |
| `rsa-sha2-256` | RSA with SHA-256 signature (recommended) |
| `rsa-sha2-512` | RSA with SHA-512 signature (recommended) |
| `ecdsa-sha2-nistp256` | ECDSA with NIST P-256 curve |
| `ecdsa-sha2-nistp384` | ECDSA with NIST P-384 curve |
| `ecdsa-sha2-nistp521` | ECDSA with NIST P-521 curve |
| `ssh-rsa` | Legacy RSA with SHA-1 (avoid if possible) |
| `ssh-dss` | DSA algorithm (deprecated) |

#### Example: Modern Algorithms Only

For security-conscious deployments, restrict to modern algorithms only:

```java
from("mina-sftp://user@host/path?privateKeyFile=/path/to/key&publicKeyAcceptedAlgorithms=ssh-ed25519,rsa-sha2-256,rsa-sha2-512,ecdsa-sha2-nistp256")
    .to("file:local");
```

If `publicKeyAcceptedAlgorithms` is not specified, the default list from Apache MINA SSHD is used.

### Supported Key Formats

The component supports all key formats natively supported by Apache MINA SSHD:

-   **PEM formats**: PKCS#1, PKCS#8, OpenSSH format
    
-   **OpenSSH native format**
    
-   **Encrypted keys**: Supported (PKCS#8 encrypted requires BouncyCastle)
    

### Supported Key Algorithms

-   RSA (all key sizes)
    
-   ECDSA (P-256, P-384, P-521)
    
-   Ed25519
    
-   DSA
    

### Client Certificate Authentication

The mina-sftp component supports OpenSSH certificate-based authentication, which provides centralized key management through a Certificate Authority (CA). This is a MINA SSHD-specific feature not available in the JSch-based sftp component.

OpenSSH certificates bind a public key to identity information and are signed by a trusted CA. They provide:

-   Centralized key revocation
    
-   Time-limited access without key rotation
    
-   Principal-based authorization
    

#### Certificate Options

  
| Option | Description | Priority |
| --- | --- | --- |
| `certBytes` | Certificate content as byte array (for programmatic loading from secret managers) | 1 (highest) |
| `certUri` | URI to certificate file (classpath:, file:, etc.) | 2 |
| `certFile` | Path to certificate file on filesystem | 3 (lowest) |

#### Option Priority Order

When multiple certificate options are configured, the component uses this priority order:

1.  `certBytes` - checked first (highest priority)
    
2.  `certUri` - checked second
    
3.  `certFile` - checked last (lowest priority)
    

The first non-empty option wins. This matches the priority order used for private key options (`privateKey` > `privateKeyUri` > `privateKeyFile`).

#### Certificate Format Requirements

-   Certificates must be in OpenSSH format (as generated by `ssh-keygen -s`)
    
-   Only USER type certificates are supported (for client authentication)
    
-   The certificate must correspond to the configured private key
    
-   Certificate file typically has a `-cert.pub` suffix (e.g., `id_rsa-cert.pub`)
    

#### Example: Certificate from File

```java
from("direct:start")
    .to("mina-sftp://user@host/path"
        + "?privateKeyFile=/path/to/id_rsa"
        + "&certFile=/path/to/id_rsa-cert.pub");
```

#### Example: Certificate from Classpath

```java
from("direct:start")
    .to("mina-sftp://user@host/path"
        + "?privateKeyUri=classpath:keys/id_rsa"
        + "&certUri=classpath:keys/id_rsa-cert.pub");
```

#### Example: Certificate from Byte Array

```java
// Load certificate from external secret manager
byte[] certBytes = secretManager.getCertificate("sftp-cert");
byte[] keyBytes = secretManager.getPrivateKey("sftp-key");

MinaSftpEndpoint endpoint = context.getEndpoint(
    "mina-sftp://user@host/path", MinaSftpEndpoint.class);
MinaSftpConfiguration config = (MinaSftpConfiguration) endpoint.getConfiguration();
config.setCertBytes(certBytes);
config.setPrivateKey(keyBytes);
```

#### Certificate Validation

The component validates certificates before use:

-   **Type check**: Only USER certificates are accepted (not HOST certificates)
    
-   **Validity period**: Certificate must be currently valid (not expired, not before valid-from date)
    
-   **Private key requirement**: A corresponding private key must be configured
    

Invalid certificates result in clear error messages indicating the issue.

## Examples

### Upload Files

```java
from("file:inbox")
    .to("mina-sftp://user@sftp.example.com/upload?password=secret");
```

### Download Files

```java
from("mina-sftp://user@sftp.example.com/download?password=secret&delete=true")
    .to("file:outbox");
```

### Poll and Move

```java
from("mina-sftp://user@host/inbox?password=secret&move=.done")
    .to("file:local");
```

### Filter by Extension

```java
from("mina-sftp://user@host/data?password=secret&antInclude=*.csv")
    .to("direct:process-csv");
```

## Migration from JSch SFTP

Users migrating from the JSch-based `sftp` component can switch by changing only the URI scheme:

Before (JSch)

```java
from("sftp://user@host/path?password=secret")
    .to("file:local");
```

After (MINA SSHD)

```java
from("mina-sftp://user@host/path?password=secret")
    .to("file:local");
```

All standard configuration options remain the same for supported features.

### Features Not Supported

The following features from the JSch component are **not** supported by mina-sftp:

-   **Proxy support**: HTTP proxy, SOCKS4, SOCKS5 proxy connections
    
-   **GSSAPI/Kerberos authentication**
    

If you require these features, continue using the JSch-based `sftp` component.

If you configure an unsupported feature, the component will throw a clear error message indicating the feature is not supported.

### Behavioral Differences

While the mina-sftp component aims for compatibility with the sftp component, there are some behavioral differences due to the underlying SSH libraries.

#### Comparison Table

  
| Feature | mina-sftp (Apache MINA SSHD) | sftp (JSch) |
| --- | --- | --- |
| **License** | Apache License 2.0 | BSD-style license |
| **Compression** | Built-in support, no extra JARs needed | Requires manually adding jsch-zlib JAR to classpath |
| **Ciphers** | Modern algorithms (ChaCha20-Poly1305, AES-GCM); validates cipher names before connection | Limited algorithms; errors at connection time for invalid ciphers |
| **Key Exchange Protocols** | Modern algorithms (Curve25519, ECDH, post-quantum ready); validates protocol names before connection | Limited algorithms; uses JSch.setConfig("kex", …​) |
| **Server Host Keys** | Modern algorithms (Ed25519, RSA-SHA2, ECDSA); validates algorithm names before connection | Limited algorithms; uses session.setConfig("server\_host\_key", …​) |
| **Known Hosts Port Matching** | Strict OpenSSH semantics: `hostname` matches port 22 only; `[hostname]:port` required for non-standard ports | Lenient: `hostname` matches any port |
| **serverAliveCountMax=0** | Fire-and-forget mode: heartbeats sent with `wantReply=false`, connection never terminated | Keep-alive disabled, no heartbeats sent |
| **serverAliveCountMax < 0** | Same as `0` (fire-and-forget mode) | Keep-alive disabled |
| **Host Key Verification** | Apache MINA SSHD ServerKeyVerifier with certificate support | JSch-specific HostKeyRepository |
| **Algorithm Support** | Modern algorithms including Ed25519, ECDSA (all curves), ChaCha20-Poly1305 | Limited algorithm support, requires workarounds for modern algorithms |
| **Proxy Support** | Not supported | HTTP, SOCKS4, SOCKS5 proxy support |
| **GSSAPI/Kerberos** | Not supported | Supported |
| **Logging Configuration** | Uses SLF4J natively; `loggingLevel` and `serverMessageLoggingLevel` parameters not supported - use standard logging framework configuration instead | Requires `loggingLevel` parameter to bridge JSch internal logging to SLF4J; `serverMessageLoggingLevel` for server messages |

#### Known Hosts Port Matching

The mina-sftp component follows **strict OpenSSH semantics** for known\_hosts port matching, while the sftp component is more lenient.

**OpenSSH known\_hosts format:**

-   `hostname` - matches the hostname on **port 22 only**
    
-   `[hostname]:port` - matches the hostname on the specified non-standard port
    

**Example:** If your known\_hosts file contains:

```none
myserver.example.com ssh-rsa AAAAB3NzaC1yc2E...
```

-   **sftp component**: This entry matches connections to `myserver.example.com` on **any port**
    
-   **mina-sftp component**: This entry matches connections to `myserver.example.com` on **port 22 only**
    

**For non-standard ports with mina-sftp**, you must use the bracketed format:

```none
[myserver.example.com]:2222 ssh-rsa AAAAB3NzaC1yc2E...
```

This difference is important when migrating from the sftp component and using `strictHostKeyChecking=yes` with servers running on non-standard ports.

### Migration Checklist

When migrating from `sftp` to `mina-sftp`, verify the following:

1.  **URI Scheme**: Change `sftp://` to `mina-sftp://`
    
2.  **Proxy Usage**: If using proxy (HTTP, SOCKS4, SOCKS5), stay with `sftp` - proxy is not supported in mina-sftp
    
3.  **Kerberos/GSSAPI**: If using GSSAPI authentication, stay with `sftp`
    
4.  **Known Hosts on Non-Standard Ports**: Update known\_hosts entries to use `[hostname]:port` format for non-standard ports
    
5.  **serverAliveCountMax**: If using `serverAliveCountMax=0`, note the behavioral difference (fire-and-forget vs disabled)
    
6.  **Compression**: Remove any manual zlib JAR additions - mina-sftp has built-in compression support
    
7.  **Deprecated Parameters**: Remove JSch-specific parameters (`loggingLevel`, `serverMessageLoggingLevel`, `existDirCheckUsingLs`) - they are accepted but log warnings (see [Deprecated JSch Parameters (Migration from sftp)](#_deprecated_jsch_parameters_migration_from_sftp))
    
8.  **Logging Configuration**: Configure logging via log4j/logback instead of URI parameters (see [Logging Configuration](#_logging_configuration))
    
9.  **Test Authentication**: Verify public key and password authentication work correctly
    
10.  **Test Host Key Verification**: If using `strictHostKeyChecking=yes`, verify known\_hosts entries match
     

## Error Handling

### Connection Retry

```java
from("mina-sftp://user@host/path?password=secret&maximumReconnectAttempts=5&reconnectDelay=2000")
    .to("file:local");
```

### Error Messages

The component provides clear error messages for common failure scenarios:

#### Connection Errors

-   **Host unreachable**: `Cannot connect to {host}:{port}`
    
-   **Connection timeout**: `Connection timed out after {timeout}ms`
    

#### Authentication Errors

-   **Authentication failure**: `Authentication failed: {reason}`
    
-   **Authentication timeout**: `Authentication timed out after {timeout}ms`
    

#### Configuration Errors

-   **Invalid chmod**: `Invalid chmod value: '999'. Must be a valid octal number (e.g., 644, 755)`
    
-   **Invalid cipher**: `Unknown or unsupported cipher: xxx. Available ciphers: [aes128-ctr, aes256-ctr, …​]`
    
-   **Invalid key exchange**: `Unknown or unsupported key exchange protocol: xxx. Available protocols: [curve25519-sha256, …​]`
    
-   **Invalid host key algorithm**: `Unknown or unsupported server host key algorithm: xxx. Available algorithms: [ssh-ed25519, …​]`
    

#### Host Key Verification Errors

-   **Unknown host**: `Host key verification failed: server 'hostname:port' is not in the known_hosts file`
    
-   **Key mismatch**: `Host key verification failed: the host key for 'hostname:port' has changed!`
    
-   **Expired certificate**: `Host certificate has expired. Valid until <date>, current time: <date>`
    

#### Unsupported Features

-   **Proxy**: `Proxy not supported in mina-sftp, use sftp component`
    

The error messages include available options where applicable, making it easier to correct configuration issues.

## Compression

The mina-sftp component supports SSH data compression to reduce bandwidth usage for large file transfers over slow or metered connections.

### Enabling Compression

To enable compression, set the `compression` option to a value between 1 and 10:

```java
from("mina-sftp://user@host/path?password=secret&compression=5")
    .to("file:local");
```

The compression level is advisory; the actual compression behavior depends on the SSH library’s implementation. When compression is enabled, the component configures the following algorithms in order of preference:

1.  `zlib@openssh.com` (OpenSSH delayed compression - preferred for security)
    
2.  `zlib` (standard zlib compression)
    
3.  `none` (fallback if server doesn’t support compression)
    

### No Additional Dependencies Required

> **Note**
> Unlike the JSch-based `sftp` component which requires manually adding a zlib JAR to the classpath, Apache MINA SSHD includes built-in compression support. No additional dependencies are needed.

### Compression Fallback Behavior

If compression is enabled but the server does not support any compression algorithms, the connection automatically falls back to uncompressed transfer and logs a WARNING message:

```none
WARN  Compression was requested (level=5) but server does not support compression. Falling back to uncompressed transfer.
```

This allows the connection to proceed without manual intervention while alerting administrators to the configuration mismatch.

### Default Behavior

By default (`compression=0`), compression is disabled to minimize CPU overhead and maintain backward compatibility. Enable compression only when bandwidth savings outweigh the CPU cost of compression/decompression.

### Compression Algorithm Details

When compression is enabled, the component offers the following algorithms during SSH negotiation:

 
| Algorithm | Description |
| --- | --- |
| `zlib@openssh.com` | OpenSSH "delayed" compression. Compression starts only after authentication completes. This is preferred for security as it prevents potential compression-related attacks during the authentication phase. |
| `zlib` | Standard zlib compression. Compression is active immediately, including during authentication. Use only if the server doesn’t support delayed compression. |
| `none` | No compression (fallback). Used when the server doesn’t support any compression. |

The algorithm negotiation follows SSH protocol standards - the first mutually supported algorithm from the client’s preference list is selected.

## Cipher Configuration

The mina-sftp component allows you to specify which SSH cipher algorithms to use for encrypted data transfer.

### Configuring Ciphers

To specify a custom list of ciphers, use the `ciphers` option with a comma-separated list of cipher names:

```java
from("mina-sftp://user@host/path?password=secret&ciphers=aes256-ctr,aes256-gcm@openssh.com")
    .to("file:local");
```

Ciphers are offered to the server in the order specified. The first mutually supported cipher will be used.

### Available Ciphers

The following ciphers are supported by Apache MINA SSHD:

   
| Cipher Name | Algorithm | Mode | Notes |
| --- | --- | --- | --- |
| `aes128-ctr` | AES-128 | CTR | Standard, widely supported |
| `aes192-ctr` | AES-192 | CTR | Standard |
| `aes256-ctr` | AES-256 | CTR | Recommended for high security |
| `aes128-gcm@openssh.com` | AES-128 | GCM | Authenticated encryption |
| `aes256-gcm@openssh.com` | AES-256 | GCM | Recommended - authenticated encryption |
| `chacha20-poly1305@openssh.com` | ChaCha20 | AEAD | Modern, fast on CPUs without AES-NI |
| `aes128-cbc` | AES-128 | CBC | Legacy, avoid if possible |
| `aes192-cbc` | AES-192 | CBC | Legacy |
| `aes256-cbc` | AES-256 | CBC | Legacy, avoid if possible |
| `3des-cbc` | Triple DES | CBC | Deprecated, use only for compatibility |
| `blowfish-cbc` | Blowfish | CBC | Legacy |

### Cipher Security Recommendations

For security-hardened environments, use only modern authenticated encryption modes:

```java
// Recommended secure configuration
from("mina-sftp://user@host/path?password=secret&ciphers=aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-ctr")
    .to("file:local");
```

### Default Cipher Behavior

If `ciphers` is not specified, Apache MINA SSHD’s default cipher list is used, which includes a secure selection of modern algorithms.

> **Note**
> Unlike the JSch-based `sftp` component, Apache MINA SSHD supports modern algorithms like ChaCha20-Poly1305 and AES-GCM that are not available in JSch. Additionally, invalid cipher names are validated before attempting to connect, providing clearer error messages.

## Key Exchange Protocol Configuration

The mina-sftp component allows you to specify which SSH key exchange algorithms to use for deriving the shared session key.

### Configuring Key Exchange Protocols

To specify a custom list of key exchange protocols, use the `keyExchangeProtocols` option with a comma-separated list:

```java
from("mina-sftp://user@host/path?password=secret&keyExchangeProtocols=curve25519-sha256,ecdh-sha2-nistp256")
    .to("file:local");
```

Key exchange protocols are offered to the server in the order specified. The first mutually supported algorithm will be used.

### Available Key Exchange Protocols

The following key exchange protocols are supported by Apache MINA SSHD:

  
| Protocol Name | Description | Recommended |
| --- | --- | --- |
| `curve25519-sha256` | Modern Curve25519 elliptic curve with SHA-256 | Yes |
| `curve25519-sha256@libssh.org` | Curve25519 (libssh.org variant) | Yes |
| `curve448-sha512` | Curve448 with SHA-512 (stronger) | Yes |
| `ecdh-sha2-nistp256` | ECDH with NIST P-256 curve | Yes |
| `ecdh-sha2-nistp384` | ECDH with NIST P-384 curve | Yes |
| `ecdh-sha2-nistp521` | ECDH with NIST P-521 curve | Yes |
| `diffie-hellman-group14-sha256` | DH Group14 (2048-bit) with SHA-256 | Yes |
| `diffie-hellman-group15-sha512` | DH Group15 (3072-bit) with SHA-512 | Yes |
| `diffie-hellman-group16-sha512` | DH Group16 (4096-bit) with SHA-512 | Yes |
| `diffie-hellman-group17-sha512` | DH Group17 (6144-bit) with SHA-512 | Yes |
| `diffie-hellman-group18-sha512` | DH Group18 (8192-bit) with SHA-512 | Yes |
| `diffie-hellman-group-exchange-sha256` | DH Group Exchange with SHA-256 | Yes |
| `diffie-hellman-group14-sha1` | DH Group14 with SHA-1 | Deprecated |
| `diffie-hellman-group1-sha1` | DH Group1 (1024-bit) with SHA-1 | Deprecated |
| `diffie-hellman-group-exchange-sha1` | DH Group Exchange with SHA-1 | Deprecated |

### Default Key Exchange Behavior

If `keyExchangeProtocols` is not specified, Apache MINA SSHD’s default list is used, which prioritizes modern, secure algorithms.

## Server Host Key Configuration

The mina-sftp component allows you to specify which server host key algorithms are accepted for verifying the identity of the SSH server.

### Configuring Server Host Keys

To specify a custom list of server host key algorithms, use the `serverHostKeys` option with a comma-separated list:

```java
from("mina-sftp://user@host/path?password=secret&serverHostKeys=ssh-ed25519,rsa-sha2-512")
    .to("file:local");
```

Server host key algorithms are offered to the server in the order specified. The first mutually supported algorithm will be used for server authentication.

### Available Server Host Key Algorithms

The following server host key algorithms are supported by Apache MINA SSHD:

  
| Algorithm Name | Description | Recommended |
| --- | --- | --- |
| `ssh-ed25519` | EdDSA Ed25519 (modern, fast) | Yes |
| `rsa-sha2-512` | RSA with SHA-512 (2048+ bit keys) | Yes |
| `rsa-sha2-256` | RSA with SHA-256 (2048+ bit keys) | Yes |
| `ecdsa-sha2-nistp256` | ECDSA with NIST P-256 curve | Yes |
| `ecdsa-sha2-nistp384` | ECDSA with NIST P-384 curve | Yes |
| `ecdsa-sha2-nistp521` | ECDSA with NIST P-521 curve | Yes |
| `ssh-rsa` | RSA with SHA-1 | Deprecated |
| `ssh-dss` | DSA | Deprecated |

### Certificate Variants

Apache MINA SSHD also supports OpenSSH certificate-based host key verification:

-   `ssh-ed25519-cert-v01@openssh.com`
    
-   `rsa-sha2-256-cert-v01@openssh.com`
    
-   `rsa-sha2-512-cert-v01@openssh.com`
    
-   `ecdsa-sha2-nistp256-cert-v01@openssh.com`
    
-   `ecdsa-sha2-nistp384-cert-v01@openssh.com`
    
-   `ecdsa-sha2-nistp521-cert-v01@openssh.com`
    

### Default Server Host Key Behavior

If `serverHostKeys` is not specified, Apache MINA SSHD’s default list is used, which includes all supported algorithms with modern ones prioritized.

## Algorithm Security Recommendations

For security-hardened environments, configure only modern, recommended algorithms:

### Recommended Configuration

```java
// Security-hardened SFTP connection
from("mina-sftp://user@host/path?password=secret"
    + "&keyExchangeProtocols=curve25519-sha256,ecdh-sha2-nistp256,diffie-hellman-group16-sha512"
    + "&serverHostKeys=ssh-ed25519,rsa-sha2-512,ecdsa-sha2-nistp256"
    + "&ciphers=aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-ctr")
    .to("file:local");
```

### Algorithms to Avoid

The following algorithms are deprecated and should be avoided for new deployments:

 
| Algorithm | Reason |
| --- | --- |
| `diffie-hellman-group1-sha1` | 1024-bit DH is too weak; SHA-1 is deprecated |
| `diffie-hellman-group14-sha1` | SHA-1 is deprecated |
| `diffie-hellman-group-exchange-sha1` | SHA-1 is deprecated |
| `ssh-rsa` | Uses SHA-1 for signatures (deprecated) |
| `ssh-dss` | DSA is deprecated |

### Compliance Considerations

For environments requiring compliance with security standards (e.g., FIPS, PCI-DSS):

-   Use only NIST-approved curves (P-256, P-384, P-521) for ECDH and ECDSA
    
-   Use RSA with SHA-256 or SHA-512 (rsa-sha2-256, rsa-sha2-512)
    
-   Use AES-128 or AES-256 in CTR or GCM mode
    
-   Avoid Curve25519/Ed25519 if strict FIPS compliance is required (not NIST-approved)
    

## Connection Keep-Alive

The component supports SSH keep-alive (heartbeat) functionality to prevent connections from being dropped during long idle periods and to detect unresponsive servers.

### Configuration Options

   
| Option | Default | Type | Description |
| --- | --- | --- | --- |
| `serverAliveInterval` | `0` | int (ms) | Interval in milliseconds between keep-alive messages. Set to `0` to disable (default). |
| `serverAliveCountMax` | `1` | int | Maximum number of consecutive unanswered keep-alive messages before the connection is terminated. |

These option names follow the standard OpenSSH client configuration naming (`ServerAliveInterval` and `ServerAliveCountMax`) and are identical to the JSch-based `sftp` component for seamless migration.

> **Note**
> Under the hood, these settings are mapped to Apache MINA SSHD’s `CoreModuleProperties.HEARTBEAT_INTERVAL` and `CoreModuleProperties.HEARTBEAT_NO_REPLY_MAX` properties.

### Preventing Connection Drops

For routes with long idle periods between file transfers, configure keep-alive to prevent firewalls or servers from terminating the connection:

```java
// Send keep-alive every 30 seconds
from("mina-sftp://user@host/path?password=secret&serverAliveInterval=30000")
    .to("file:local");
```

### Detecting Unresponsive Servers

Configure `serverAliveCountMax` to control how quickly the component detects an unresponsive server:

```java
// Terminate connection after 3 unanswered keep-alives (90 seconds max)
from("mina-sftp://user@host/path?password=secret&serverAliveInterval=30000&serverAliveCountMax=3")
    .to("file:local");
```

With this configuration:

-   Keep-alive messages are sent every 30 seconds
    
-   If 3 consecutive messages go unanswered, the connection is terminated
    
-   Maximum detection time: 90 seconds (30s × 3)
    

### Default Behavior

By default (`serverAliveInterval=0`), no keep-alive messages are sent. This matches the JSch-based `sftp` component behavior.

> **Note**
> Negative values for `serverAliveInterval` are treated the same as `0` (keep-alive disabled). This behavior is consistent between `mina-sftp` and `sftp` components.

### Behavioral Difference: serverAliveCountMax with Zero or Negative Values

> **Important**
> There is a behavioral difference between `mina-sftp` and `sftp` components when `serverAliveCountMax` is set to `0` or a negative value.

  
| Value | mina-sftp (MINA SSHD) | sftp (JSch) |
| --- | --- | --- |
| `> 0` | Terminate connection after N unanswered heartbeats | Terminate connection after N unanswered heartbeats |
| `= 0` | **Fire-and-forget mode**: heartbeats are sent but no reply is expected, connection is never terminated due to unanswered heartbeats | No keep-alive messages are sent |
| `< 0` | **Fire-and-forget mode**: same as `0` | No keep-alive messages are sent |

This difference stems from the underlying libraries:

-   **Apache MINA SSHD**: When `HEARTBEAT_NO_REPLY_MAX ⇐ 0`, heartbeats are sent with `wantReply=false` (fire-and-forget mode)
    
-   **JSch**: When `serverAliveCountMax ⇐ 0`, keep-alive functionality is effectively disabled
    

#### Recommendation

To ensure consistent behavior when migrating from `sftp` to `mina-sftp`:

-   Always use positive values for `serverAliveCountMax` (default is `1`)
    
-   If you want to disable connection termination on unresponsive servers but still send heartbeats, `mina-sftp` with `serverAliveCountMax=0` provides this capability (not available in `sftp`)
    

## Host Key Verification

The MINA SFTP component supports comprehensive host key verification to protect against Man-in-the-Middle (MITM) attacks.

### Strict Host Key Checking

When `strictHostKeyChecking=yes`, the server’s host key must match an entry in the known hosts source. If the key is unknown or mismatches, the connection is rejected.

```java
from("mina-sftp://user@host/path?password=secret&strictHostKeyChecking=yes")
    .to("file:local");
```

### Known Hosts Sources (Priority Order)

The component checks for known hosts in this priority order:

1.  **Byte array** (`knownHosts`): Directly configured as byte array
    
2.  **URI/Classpath** (`knownHostsUri`): Loaded from classpath or file URI
    
3.  **File path** (`knownHostsFile`): Loaded from filesystem
    
4.  **User default** (`useUserKnownHostsFile=true`): Uses `~/.ssh/known_hosts`
    

#### Using Custom Known Hosts File

```java
from("mina-sftp://user@host/path?password=secret&strictHostKeyChecking=yes&knownHostsFile=/path/to/known_hosts")
    .to("file:local");
```

#### Using Known Hosts from Classpath

```java
from("mina-sftp://user@host/path?password=secret&strictHostKeyChecking=yes&knownHostsUri=classpath:ssh/known_hosts")
    .to("file:local");
```

#### Using User’s Default Known Hosts

By default, `useUserKnownHostsFile=true` which uses `~/.ssh/known_hosts`:

```java
from("mina-sftp://user@host/path?password=secret&strictHostKeyChecking=yes")
    .to("file:local");
```

### Auto-Create Known Hosts File (Development Only)

For development environments, you can enable automatic trust-on-first-use:

```java
from("mina-sftp://user@host/path?password=secret&autoCreateKnownHostsFile=true&knownHostsFile=/tmp/dev_known_hosts")
    .to("file:local");
```

> **Caution**
> Auto-create is only recommended for development environments. It weakens security by automatically trusting new hosts.

### Disable Host Key Checking (Testing Only)

```java
from("mina-sftp://user@localhost/test?password=secret&strictHostKeyChecking=no&useUserKnownHostsFile=false")
    .to("mock:result");
```

> **Caution**
> Disabling host key checking is insecure and should only be used for testing.

### Certificate-Based Host Verification

For enterprise environments using OpenSSH host certificates, you can use `@cert-authority` entries in your known\_hosts file to verify server certificates instead of maintaining individual host keys.

#### Using @cert-authority Entries

The standard OpenSSH known\_hosts format supports `@cert-authority` entries that define trusted CA public keys for certificate verification:

```none
# Trust this CA for all hosts in example.com domain
@cert-authority *.example.com ssh-rsa AAAAB3NzaC1yc2E... Production CA

# Trust this CA for a specific host
@cert-authority server.example.com ssh-ed25519 AAAAC3NzaC1lZDI1NTE5... Specific CA
```

#### Example Configuration

```java
from("mina-sftp://user@host.example.com/path?password=secret&strictHostKeyChecking=yes&knownHostsFile=/path/to/known_hosts")
    .to("file:local");
```

Where the known\_hosts file contains:

```none
# Regular host key entry
server1.example.com ssh-rsa AAAAB3NzaC1yc2E...

# CA for certificate-based verification
@cert-authority *.example.com ssh-rsa AAAAB3NzaC1yc2E... Enterprise CA
```

#### Certificate vs Known Hosts Priority

When both `@cert-authority` entries and regular host key entries are present:

-   If the server presents a certificate AND a matching `@cert-authority` entry exists: Certificate verification takes precedence
    
-   If certificate verification fails: Connection is rejected (does NOT fall back to regular known\_hosts entries)
    
-   If server presents a plain public key (not certificate): Regular known hosts verification is used
    

This ensures that servers configured for certificate authentication maintain their security guarantees.

### Custom ServerKeyVerifier

For advanced use cases, you can provide a custom `ServerKeyVerifier` implementation to handle host key verification. This allows integration with enterprise key management systems or implementing custom verification logic.

#### Using Custom Verifier via Bean Reference

```java
// Register custom verifier in Camel registry
ServerKeyVerifier myVerifier = (session, remoteAddress, serverKey) -> {
    // Custom verification logic
    return verifyAgainstEnterpriseKeyStore(serverKey);
};
context.getRegistry().bind("myVerifier", myVerifier);

// Use in endpoint URI
from("mina-sftp://user@host/path?password=secret&serverKeyVerifier=#myVerifier")
    .to("file:local");
```

#### Using Custom Verifier Programmatically

```java
MinaSftpEndpoint endpoint = context.getEndpoint(
    "mina-sftp://user@host/path?password=secret", MinaSftpEndpoint.class);
MinaSftpConfiguration config = (MinaSftpConfiguration) endpoint.getConfiguration();

config.setServerKeyVerifier((session, remoteAddress, serverKey) -> {
    // Custom verification logic
    return true;
});
```

#### Custom Verifier Precedence

When a custom `ServerKeyVerifier` is provided:

-   The custom verifier is used **exclusively** for host key verification
    
-   All other host key options are ignored (`strictHostKeyChecking`, `knownHostsFile`, `knownHostsUri`, etc.)
    
-   The user takes full responsibility for security decisions
    

This precedence ensures predictable behavior - when you provide a custom verifier, only your verification logic runs.

### Host Key Verification Error Messages

The component provides clear error messages for different failure scenarios:

-   **Unknown host**: `Host key verification failed: server 'hostname:port' is not in the known_hosts file.`
    
-   **Key mismatch**: `Host key verification failed: the host key for 'hostname:port' has changed! This may indicate a man-in-the-middle attack.`
    
-   **Untrusted CA**: `Certificate is signed by untrusted CA. Add @cert-authority entry to known_hosts file.`
    
-   **Expired certificate**: `Host certificate has expired. Valid until <date>, current time: <date>.`
    
-   **Principal mismatch**: `Hostname '<hostname>' is not listed in certificate principals.`
    

## Local Interface Binding

In multi-homed environments (servers with multiple network interfaces), you may need to specify which local network interface the SFTP connection should use.

### Configuring Bind Address

Use the `bindAddress` option to specify the local IP address or hostname to bind the outgoing connection:

```java
from("mina-sftp://user@host/path?password=secret&bindAddress=192.168.1.100")
    .to("file:local");
```

### Bind Address Formats

The mina-sftp component supports multiple formats for `bindAddress`:

  
| Format | Example | Description |
| --- | --- | --- |
| IPv4 address | `192.168.1.100` | Bind to IP, ephemeral port |
| IPv4 with port | `192.168.1.100:5000` | Bind to IP and specific port |
| IPv6 address | `::1` | Bind to IPv6, ephemeral port |
| IPv6 with port | `[::1]:5000` | Bind to IPv6 and port (bracketed notation) |
| Hostname | `localhost` | Bind to hostname, ephemeral port |
| Hostname with port | `localhost:5000` | Bind to hostname and specific port |
> **Note**
> The ability to specify a local port is a **mina-sftp specific feature** not available in the JSch-based `sftp` component. See [Difference from JSch SFTP Component](#bindaddress-difference) for details.

### Use Cases

 
| Scenario | Configuration |
| --- | --- |
| Multi-homed server | `bindAddress=10.0.0.50` (use internal network interface) |
| Firewall compliance | `bindAddress=172.16.0.1` (use DMZ interface) |
| Fixed source port (strict firewall) | `bindAddress=10.0.0.50:5000` (specific interface and port) |
| Default routing | Omit `bindAddress` (OS decides based on routing table) |

### Default Behavior

When `bindAddress` is not specified (default), the operating system’s routing table determines which local interface is used for the connection. This is the standard behavior for most use cases.

When a port is not specified (e.g., `bindAddress=192.168.1.100`), an ephemeral port is automatically assigned by the operating system.

### Error Handling

If an invalid or unavailable bind address is specified, the connection will fail with a clear error message:

```none
Invalid bind address: 192.168.99.99. Supported formats: host, host:port, [ipv6], [ipv6]:port
```

### Difference from JSch SFTP Component

The mina-sftp component’s `bindAddress` parameter has an enhanced format compared to the JSch-based `sftp` component:

  
| Feature | mina-sftp | sftp (JSch) |
| --- | --- | --- |
| **IP/hostname binding** | Supported | Supported |
| **Port specification** | Supported (`host:port` format) | Not supported (always ephemeral) |
| **IPv6 with port** | Supported (`[ipv6]:port` format) | Not supported |
| **Implementation** | Native MINA SSHD API (`SshClient.connect()` with local address) | Custom SocketFactory workaround |

#### Migration Note

If you are migrating from the `sftp` component to `mina-sftp`, your existing `bindAddress` configurations will work without changes. The port specification is an optional enhancement.

```java
// Works in both sftp and mina-sftp
bindAddress=192.168.1.100

// Only works in mina-sftp (port specification)
bindAddress=192.168.1.100:5000
```

## SFTP Buffer Size Configuration

The mina-sftp component allows you to configure buffer sizes for SFTP read and write operations to optimize file transfer performance.

### Configuring Buffer Sizes

Use `readBufferSize` and `writeBufferSize` to control the buffer allocation for SFTP transfers:

```java
// Configure 64KB read buffer and 32KB write buffer
from("mina-sftp://user@host/path?password=secret&readBufferSize=65536&writeBufferSize=32768")
    .to("file:local");

// Configure symmetric buffer sizes for balanced transfers
from("mina-sftp://user@host/path?password=secret&readBufferSize=65536&writeBufferSize=65536")
    .to("file:local");
```

### Buffer Size Options

  
| Option | Default | Description |
| --- | --- | --- |
| `readBufferSize` | MINA default | Buffer size in bytes for reading data from SFTP connections |
| `writeBufferSize` | MINA default | Buffer size in bytes for writing data to SFTP connections |

### Performance Tuning Guidelines

  
| Buffer Size | Memory Usage | Use Case |
| --- | --- | --- |
| `32768` (32KB) | Low | Memory-constrained environments, slow connections |
| `65536` (64KB) | Medium | Balanced performance (recommended starting point) |
| `98304` (96KB) | Medium-High | High-throughput connections |
| `126976` (124KB) | High | Maximum recommended - higher values may cause issues |

### Important Considerations

> **Important**
> The maximum recommended buffer size is `126976` bytes (approximately 124KB). Buffer sizes larger than this may cause data corruption issues in Apache MINA SSHD due to server read request size limits.

### Default Behavior

When buffer sizes are not specified, Apache MINA SSHD uses its internal defaults, which are suitable for most use cases. Configure explicit buffer sizes only when you need to optimize for specific network conditions or memory constraints.

### Migration from bulkRequests (Deprecated)

If you are migrating from a configuration using the deprecated `bulkRequests` parameter, use the following conversion:

  
| bulkRequests | Equivalent Buffer Size | Configuration |
| --- | --- | --- |
| `1` | 32KB | `readBufferSize=32768&writeBufferSize=32768` |
| `2` | 64KB | `readBufferSize=65536&writeBufferSize=65536` |
| `4` | 128KB (capped to 124KB) | `readBufferSize=126976&writeBufferSize=126976` |
| `8+` | 124KB (maximum) | `readBufferSize=126976&writeBufferSize=126976` |

The `bulkRequests` parameter is still supported for backward compatibility but is deprecated. New configurations should use `readBufferSize` and `writeBufferSize` directly as they map directly to Apache MINA SSHD’s native buffer properties.

> **Note**
> In the original JSch-based `sftp` component, `bulkRequests` controlled how many 32KB packets could be in-flight simultaneously. In Apache MINA SSHD, there is no direct equivalent, so the mina-sftp component approximates this behavior using buffer sizes. For fine-grained control over transfer characteristics, use `readBufferSize` and `writeBufferSize`.

## File and Directory Permissions (chmod)

The mina-sftp component supports setting POSIX file permissions on uploaded files and created directories.

### Setting File Permissions

Use the `chmod` option to set permissions on files after they are uploaded:

```java
// Set file permissions to rw-r--r-- (644)
from("file:/data/outbound")
    .to("mina-sftp://user@host/uploads?password=secret&chmod=644");

// Set file permissions to rw------- (600) for sensitive files
from("file:/data/secrets")
    .to("mina-sftp://user@host/secure?password=secret&chmod=600");
```

### Setting Directory Permissions

Use the `chmodDirectory` option to set permissions on directories when they are created:

```java
// Set directory permissions to rwxr-xr-x (755)
from("file:/data/outbound")
    .to("mina-sftp://user@host/uploads?password=secret&chmodDirectory=755");

// Combine with chmod for complete control
from("file:/data/outbound")
    .to("mina-sftp://user@host/uploads?password=secret&chmod=644&chmodDirectory=755");
```

### Permission Format

Permissions are specified as octal strings, just like the Unix `chmod` command:

  
| Value | Permissions | Description |
| --- | --- | --- |
| `777` | `rwxrwxrwx` | Full access for everyone (not recommended) |
| `755` | `rwxr-xr-x` | Owner full, group/others read+execute |
| `750` | `rwxr-x---` | Owner full, group read+execute, others none |
| `700` | `rwx------` | Owner only |
| `644` | `rw-r—​r--` | Owner read+write, group/others read-only |
| `640` | `rw-r-----` | Owner read+write, group read-only, others none |
| `600` | `rw-------` | Owner read+write only |

### Platform Considerations

> **Important**
> The `chmod` and `chmodDirectory` options only work on POSIX-compatible SFTP servers (Linux, macOS, Unix). Windows SFTP servers that don’t support POSIX permissions may ignore these settings or return an error.

### Configuration Validation

The `chmod` and `chmodDirectory` values are validated at endpoint startup. Invalid values will cause the endpoint to fail during initialization with a clear error message:

```none
Invalid chmod value: '999'. Must be a valid octal number (e.g., 644, 755).
The value contains non-octal characters (valid: 0-7).

Invalid chmodDirectory value: '888'. Must be an octal number between 000 and 7777 (e.g., 644, 755).
```

This early validation helps catch configuration errors before any file operations are attempted.

## Symbolic Links

The mina-sftp component supports reading and writing through symbolic links on SFTP servers that support them.

### Consumer Behavior

When consuming files, the consumer follows symbolic links to their target files:

```java
// Will consume files through symlinks
from("mina-sftp://user@host/data?password=secret")
    .to("file:local");
```

### Producer Behavior

When producing files, you can write to paths that are symbolic links. The file will be written to the symlink’s target:

```java
// Can write to symlink targets
from("file:local")
    .to("mina-sftp://user@host/upload-link?password=secret");
```

### Symlink Limitations

> **Note**
> **Absolute symlinks in chroot environments**: If the SFTP server uses a chroot jail (common with OpenSSH `ChrootDirectory`), absolute symlinks may not resolve correctly because the absolute path gets prepended with the chroot directory. Use **relative symlinks** for maximum compatibility in chroot environments.

```bash
# Relative symlink (works in chroot) - RECOMMENDED
ln -s ../actual-data/file.txt data/link.txt

# Absolute symlink (may fail in chroot)
ln -s /home/user/actual-data/file.txt data/link.txt
```

## Thread Safety

The mina-sftp component handles thread safety internally. The underlying MINA SSHD session and SFTP client are not thread-safe, so the component uses internal locking to ensure safe concurrent access.

### Concurrent Access

Multiple Camel routes can safely share the same SFTP endpoint. The component serializes access to the underlying SFTP connection:

```java
// Safe: Multiple routes can use the same endpoint
from("timer:upload1?period=5000")
    .setBody(constant("data1"))
    .to("mina-sftp://user@host/uploads?password=secret");

from("timer:upload2?period=5000")
    .setBody(constant("data2"))
    .to("mina-sftp://user@host/uploads?password=secret");
```

### Connection Pooling

Each endpoint maintains its own connection. For high-throughput scenarios with many concurrent operations, consider using multiple endpoints or connection pooling strategies at the route level.

## Filename Encoding

The mina-sftp component allows you to specify the character encoding used for filenames when communicating with the SFTP server.

### When to Use

By default, MINA SSHD uses UTF-8 encoding for filenames, which is the standard for modern SFTP servers. However, some legacy servers may use different regional encodings:

-   **GBK** or **GB2312** - Chinese servers
    
-   **Shift-JIS** or **EUC-JP** - Japanese servers
    
-   **ISO-8859-1** - Western European legacy systems
    
-   **Windows-1252** - Windows legacy systems
    

### Configuration

Use the `filenameEncoding` option to specify the charset:

```java
// Connect to a legacy server using GBK encoding for Chinese filenames
from("mina-sftp://user@host/path?password=secret&filenameEncoding=GBK")
    .to("file:local");

// Connect to a Japanese server
from("mina-sftp://user@host/path?password=secret&filenameEncoding=Shift-JIS")
    .to("file:local");
```

### Default Behavior

When `filenameEncoding` is not specified, UTF-8 is used (the MINA SSHD default). This is correct for most modern SFTP servers.

## Deprecated JSch Parameters (Migration from sftp)

The following parameters from the JSch-based `sftp` component are accepted for **backward compatibility** but are ignored. When used, they log a deprecation warning to help you identify configurations that need updating.

### Accepted but Ignored Parameters

  
| Parameter | Description | Recommendation |
| --- | --- | --- |
| `existDirCheckUsingLs` | JSch-specific workaround for Windows compatibility. MINA SSHD uses `stat()` instead. | Remove from URI |
| `jschLoggingLevel` | Controlled JSch internal logging verbosity. | Configure via log4j/logback (see [Logging Configuration](#_logging_configuration)) |
| `serverMessageLoggingLevel` | Controlled SSH server message logging. | Configure via log4j/logback (see [Logging Configuration](#_logging_configuration)) |

### Example Warning Messages

When these deprecated parameters are used, warnings like the following are logged:

```none
WARN  The 'existDirCheckUsingLs' parameter is specific to the JSch-based sftp component
      and is ignored by mina-sftp. MINA SSHD uses stat() for directory existence checks
      which is more reliable.

WARN  The 'jschLoggingLevel' parameter is specific to the JSch-based sftp component
      and is ignored by mina-sftp. MINA SSHD uses SLF4J natively - configure logging
      via your logging framework (log4j, logback) instead.
```

### Migration Example

```java
// Before (sftp component with JSch-specific parameters)
from("sftp://user@host/path?existDirCheckUsingLs=false&jschLoggingLevel=WARN")

// After (mina-sftp component) - remove JSch-specific parameters
from("mina-sftp://user@host/path")
```

The deprecated parameters will continue to work (without effect) to ease migration, but you should remove them to avoid the warning messages.

## Logging Configuration

### Difference from JSch SFTP Component

The JSch-based `sftp` component provides two logging-related configuration options:

-   `loggingLevel` (also known as `jschLoggingLevel`) - Controls the verbosity of JSch library internal logging
    
-   `serverMessageLoggingLevel` - Controls the log level for SSH server messages (banners, interactive messages)
    

**These options are NOT available in the mina-sftp component** because Apache MINA SSHD handles logging differently:

  
| Aspect | sftp (JSch) | mina-sftp (Apache MINA SSHD) |
| --- | --- | --- |
| **Logging Framework** | JSch has its own `com.jcraft.jsch.Logger` interface that must be bridged to SLF4J | Uses SLF4J natively - no bridge needed |
| **Library Logging Control** | Requires `loggingLevel` parameter to control JSch verbosity | Controlled via standard SLF4J configuration (log4j.properties, logback.xml) |
| **Server Messages** | `serverMessageLoggingLevel` controls `showMessage()` callback output | Server messages (banners) are handled internally and logged via SLF4J |

### Configuring MINA SSHD Logging

To control the verbosity of Apache MINA SSHD logging, configure your logging framework directly.

#### Log4j Configuration

```properties
# log4j.properties

# Set MINA SSHD logging level (equivalent to loggingLevel in sftp component)
log4j.logger.org.apache.sshd=WARN

# For more verbose debugging during development
log4j.logger.org.apache.sshd=DEBUG

# Fine-grained control over specific MINA SSHD components
log4j.logger.org.apache.sshd.client=DEBUG
log4j.logger.org.apache.sshd.common.channel=WARN
log4j.logger.org.apache.sshd.sftp=DEBUG

# To see SSH channel window operations (very verbose)
log4j.logger.org.apache.sshd.common.channel.Window=TRACE

# To see key exchange details
log4j.logger.org.apache.sshd.common.kex=DEBUG

# To see authentication details
log4j.logger.org.apache.sshd.client.auth=DEBUG
```

#### Log4j2 Configuration

```xml
<!-- log4j2.xml -->
<Configuration>
    <Loggers>
        <!-- Set MINA SSHD logging level -->
        <Logger name="org.apache.sshd" level="WARN"/>

        <!-- For debugging SFTP operations -->
        <Logger name="org.apache.sshd.sftp" level="DEBUG"/>

        <!-- For debugging authentication -->
        <Logger name="org.apache.sshd.client.auth" level="DEBUG"/>

        <!-- For debugging key exchange -->
        <Logger name="org.apache.sshd.common.kex" level="DEBUG"/>
    </Loggers>
</Configuration>
```

#### Logback Configuration

```xml
<!-- logback.xml -->
<configuration>
    <!-- Set MINA SSHD logging level (equivalent to loggingLevel in sftp component) -->
    <logger name="org.apache.sshd" level="WARN"/>

    <!-- For debugging during development -->
    <logger name="org.apache.sshd" level="DEBUG"/>

    <!-- Fine-grained control -->
    <logger name="org.apache.sshd.client" level="DEBUG"/>
    <logger name="org.apache.sshd.sftp" level="DEBUG"/>
    <logger name="org.apache.sshd.client.auth" level="DEBUG"/>
    <logger name="org.apache.sshd.common.kex" level="DEBUG"/>

    <!-- Very verbose channel window logging -->
    <logger name="org.apache.sshd.common.channel.Window" level="TRACE"/>
</configuration>
```

### Common Logging Scenarios

 
| Scenario | Logger Configuration |
| --- | --- |
| **Reduce noise in production** | `org.apache.sshd=WARN` or `org.apache.sshd=ERROR` |
| **Debug connection issues** | `org.apache.sshd.client=DEBUG` |
| **Debug authentication failures** | `org.apache.sshd.client.auth=DEBUG` |
| **Debug file transfer issues** | `org.apache.sshd.sftp=DEBUG` |
| **Debug host key verification** | `org.apache.sshd.client.keyverifier=DEBUG` |
| **Full verbose debugging** | `org.apache.sshd=TRACE` (warning: very verbose) |

### Migration Note

If you are migrating from the `sftp` component and were using `loggingLevel` or `serverMessageLoggingLevel`:

1.  These parameters are accepted for backward compatibility but will log a deprecation warning
    
2.  Remove these parameters from your endpoint URI to avoid the warning messages
    
3.  Add the equivalent logging configuration to your `log4j.properties`, `log4j2.xml`, or `logback.xml`
    
4.  The standard SLF4J approach provides more flexibility and follows Java logging best practices
    

Before (JSch sftp component)

```java
from("sftp://user@host/path?password=secret&loggingLevel=DEBUG&serverMessageLoggingLevel=INFO")
    .to("file:local");
```

After (MINA SSHD mina-sftp component)

```java
// Remove logging parameters from URI
from("mina-sftp://user@host/path?password=secret")
    .to("file:local");
```

And add to your logging configuration:

```properties
# log4j.properties
log4j.logger.org.apache.sshd=DEBUG
```