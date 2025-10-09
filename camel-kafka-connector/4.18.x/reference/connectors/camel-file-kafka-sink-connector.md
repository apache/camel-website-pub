# camel-file-kafka-connector sink configuration

Connector Description: Read and write files.

When using camel-file-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-file-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.file.CamelFileSinkConnector
```

The camel-file sink connector supports 32 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.sink.path.directoryName** | **Required** The starting directory. |  | HIGH |
| **camel.sink.endpoint.charset** | This option is used to specify the encoding of the file. You can use this on the consumer, to specify the encodings of the files, which allow Camel to know the charset it should load the file content in case the file content is being accessed. Likewise when writing a file, you can use this option to specify which charset to write the file as well. Do mind that when writing the file Camel may have to read the message content into memory to be able to convert the data into the configured charset, so do not use this if you have big messages. |  | MEDIUM |
| **camel.sink.endpoint.doneFileName** | Producer: If provided, then Camel will write a 2nd done file when the original file has been written. The done file will be empty. This option configures what file name to use. Either you can specify a fixed name. Or you can use dynamic placeholders. The done file will always be written in the same folder as the original file. Consumer: If provided, Camel will only consume files if a done file exists. This option configures what file name to use. Either you can specify a fixed name. Or you can use dynamic placeholders.The done file is always expected in the same folder as the original file. Only $\\{file.name} and $\\{file.name.next} is supported as dynamic placeholders. |  | MEDIUM |
| **camel.sink.endpoint.fileName** | Use Expression such as File Language to dynamically set the filename. For consumers, it’s used as a filename filter. For producers, it’s used to evaluate the filename to write. If an expression is set, it take precedence over the CamelFileName header. (Note: The header itself can also be an Expression). The expression options support both String and Expression types. If the expression is a String type, it is always evaluated using the File Language. If the expression is an Expression type, the specified Expression type is used - this allows you, for instance, to use OGNL expressions. For the consumer, you can use it to filter filenames, so you can for instance consume today’s file using the File Language syntax: mydata-$\\{date:now:yyyyMMdd}.txt. The producers support the CamelOverruleFileName header which takes precedence over any existing CamelFileName header; the CamelOverruleFileName is a header that is used only once, and makes it easier as this avoids to temporary store CamelFileName and have to restore it afterwards. |  | MEDIUM |
| **camel.sink.endpoint.appendChars** | Used to append characters (text) after writing files. This can for example be used to add new lines or other separators when writing and appending new files or existing files. To specify new-line (slash-n or slash-r) or tab (slash-t) characters then escape with an extra slash, eg slash-slash-n. |  | MEDIUM |
| **camel.sink.endpoint.checksumFileAlgorithm** | 
If provided, then Camel will calculate a checksum from the file that has been written, and store the result in the CamelFileChecksum header. One of: \[MD2\] \[MD5\] \[SHA\_1\] \[SHA\_224\] \[SHA\_256\] \[SHA\_384\] \[SHA\_512\] \[SHA\_512\_224\] \[SHA\_512\_256\] \[SHA3\_224\] \[SHA3\_256\] \[SHA3\_384\] \[SHA3\_512\].

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
    





 |  | MEDIUM |
| **camel.sink.endpoint.checksumWriteFile** | If checksumFileAlgorithm has been configured then this option controls whether to write a checksum file as well or not. The checksum file will always be written in the same folder as the original file. | true | MEDIUM |
| **camel.sink.endpoint.fileExist** | 

What to do if a file already exists with the same name. Override, which is the default, replaces the existing file. - Append - adds content to the existing file. - Fail - throws a GenericFileOperationException, indicating that there is already an existing file. - Ignore - silently ignores the problem and does not override the existing file, but assumes everything is okay. - Move - option requires to use the moveExisting option to be configured as well. The option eagerDeleteTargetFile can be used to control what to do if an moving the file, and there exists already an existing file, otherwise causing the move operation to fail. The Move option will move any existing files, before writing the target file. - TryRename is only applicable if tempFileName option is in use. This allows to try renaming the file from the temporary name to the actual name, without doing any exists check. This check may be faster on some file systems and especially FTP servers. One of: \[Override\] \[Append\] \[Fail\] \[Ignore\] \[Move\] \[TryRename\].

Enum values:

-   Override
    
-   Append
    
-   Fail
    
-   Ignore
    
-   Move
    
-   TryRename
    





 | "Override" | MEDIUM |
| **camel.sink.endpoint.flatten** | Flatten is used to flatten the file name path to strip any leading paths, so it’s just the file name. This allows you to consume recursively into sub-directories, but when you eg write the files to another directory they will be written in a single directory. Setting this to true on the producer enforces that any file name in CamelFileName header will be stripped for any leading paths. | false | MEDIUM |
| **camel.sink.endpoint.jailStartingDirectory** | Used for jailing (restricting) writing files to the starting directory (and sub) only. This is enabled by default to not allow Camel to write files to outside directories (to be more secured out of the box). You can turn this off to allow writing files to directories outside the starting directory, such as parent or root folders. | true | MEDIUM |
| **camel.sink.endpoint.moveExisting** | Expression (such as File Language) used to compute file name to use when fileExist=Move is configured. To move files into a backup subdirectory just enter backup. This option only supports the following File Language tokens: file:name, file:name.ext, file:name.noext, file:onlyname, file:onlyname.noext, file:ext, and file:parent. Notice the file:parent is not supported by the FTP component, as the FTP component can only move any existing files to a relative directory based on current dir as base. |  | MEDIUM |
| **camel.sink.endpoint.tempFileName** | The same as tempPrefix option but offering a more fine grained control on the naming of the temporary filename as it uses the File Language. The location for tempFilename is relative to the final file location in the option 'fileName', not the target directory in the base uri. For example if option fileName includes a directory prefix: dir/finalFilename then tempFileName is relative to that subdirectory dir. |  | MEDIUM |
| **camel.sink.endpoint.tempPrefix** | This option is used to write the file using a temporary name and then, after the write is complete, rename it to the real name. Can be used to identify files being written and also avoid consumers (not using exclusive read locks) reading in progress files. Is often used by FTP when uploading big files. |  | MEDIUM |
| **camel.sink.endpoint.allowNullBody** | Used to specify if a null body is allowed during file writing. If set to true then an empty file will be created, when set to false, and attempting to send a null body to the file component, a GenericFileWriteException of 'Cannot write null body to file.' will be thrown. If the fileExist option is set to 'Override', then the file will be truncated, and if set to append the file will remain unchanged. | false | MEDIUM |
| **camel.sink.endpoint.chmod** | Specify the file permissions that are sent by the producer, the chmod value must be between 000 and 777; If there is a leading digit like in 0755, we will ignore it. |  | MEDIUM |
| **camel.sink.endpoint.chmodDirectory** | Specify the directory permissions used when the producer creates missing directories, the chmod value must be between 000 and 777; If there is a leading digit like in 0755, we will ignore it. |  | MEDIUM |
| **camel.sink.endpoint.eagerDeleteTargetFile** | Whether or not to eagerly delete any existing target file. This option only applies when you use fileExists=Override and the tempFileName option as well. You can use this to disable (set it to false) deleting the target file before the temp file is written. For example you may write big files and want the target file to exists during the temp file is being written. This ensure the target file is only deleted until the very last moment, just before the temp file is being renamed to the target filename. This option is also used to control whether to delete any existing files when fileExist=Move is enabled, and an existing file exists. If this option copyAndDeleteOnRenameFails false, then an exception will be thrown if an existing file existed, if its true, then the existing file is deleted before the move operation. | true | MEDIUM |
| **camel.sink.endpoint.forceWrites** | Whether to force syncing, writes to the file system. You can turn this off if you do not want this level of guarantee, for example, if writing to logs / audit logs etc.; this would yield better performance. | true | MEDIUM |
| **camel.sink.endpoint.keepLastModified** | Will keep the last modified timestamp from the source file (if any). Will use the FileConstants.FILE\_LAST\_MODIFIED header to located the timestamp. This header can contain either a java.util.Date or long with the timestamp. If the timestamp exists and the option is enabled it will set this timestamp on the written file. Note: This option only applies to the file producer. You cannot use this option with any of the ftp producers. | false | MEDIUM |
| **camel.sink.endpoint.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.sink.endpoint.moveExistingFileStrategy** | Strategy (Custom Strategy) used to move file with special naming token to use when fileExist=Move is configured. By default, there is an implementation used if no custom strategy is provided. |  | MEDIUM |
| **camel.sink.endpoint.autoCreate** | Automatically create missing directories in the file’s pathname. For the file consumer, that means creating the starting directory. For the file producer, it means the directory the files should be written to. | true | MEDIUM |
| **camel.sink.endpoint.autoCreateStepwise** | When auto-creating directories should each subdirectory be created one at a time. This may be needed due to security issues on some file-shares. | false | MEDIUM |
| **camel.sink.endpoint.browseLimit** | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | MEDIUM |
| **camel.sink.endpoint.bufferSize** | Buffer size in bytes used for writing files (or in case of FTP for downloading and uploading files). | 131072 | MEDIUM |
| **camel.sink.endpoint.copyAndDeleteOnRenameFail** | Whether to fall back and do a copy and delete file, in case the file could not be renamed directly. This option is not available for the FTP component. | true | MEDIUM |
| **camel.sink.endpoint.renameUsingCopy** | Perform rename operations using a copy and delete strategy. This is primarily used in environments where the regular rename operation is unreliable (e.g., across different file systems or networks). This option takes precedence over the copyAndDeleteOnRenameFail parameter that will automatically fall back to the copy and delete strategy, but only after additional delays. | false | MEDIUM |
| **camel.sink.endpoint.synchronous** | Sets whether synchronous processing should be strictly used. | false | MEDIUM |
| **camel.component.file.lazyStartProducer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | MEDIUM |
| **camel.component.file.autowiredEnabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | MEDIUM |
| **camel.component.file.healthCheckConsumerEnabled** | Used for enabling or disabling all consumer based health checks from this component. | true | MEDIUM |
| **camel.component.file.healthCheckProducerEnabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | MEDIUM |

The camel-file sink connector has no converters out of the box.

The camel-file sink connector supports 1 transforms out of the box, which are listed below.

-   org.apache.camel.kafkaconnector.file.transformers.FileTransforms
    

The camel-file sink connector has no aggregation strategies out of the box.