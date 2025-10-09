# SCP

**Since Camel 2.10**

**Only producer is supported**

The Camel Jsch component supports the [SCP protocol](http://en.wikipedia.org/wiki/Secure_copy) using the Client API of the [Jsch](http://www.jcraft.com/jsch/) project. Jsch is already used in camel by the [FTP](ftp-component.md) component for the **sftp:** protocol.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jsch</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

scp://host\[:port\]/destination\[?options\]

The file name can be specified either in the <path> part of the URI or as a "CamelFileName" header on the message (`Exchange.FILE_NAME` if used in code).

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

The SCP component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **verboseLogging** (producer) | JSCH is verbose logging out of the box. Therefore we turn the logging down to DEBUG logging by default. But setting this option to true turns on the verbose logging again. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The SCP endpoint is configured using URI syntax:

scp:host:port/directoryName

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (producer) | **Required** Hostname of the FTP server. |  | String |
| **port** (producer) | Port of the FTP server. |  | int |
| **directoryName** (producer) | The starting directory. |  | String |

### Query Parameters (24 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **checksumFileAlgorithm** (producer) | 
If provided, then Camel will write a checksum file when the original file has been written. The checksum file will contain the checksum created with the provided algorithm for the original file. The checksum file will always be written in the same folder as the original file.

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
| **chmod** (producer) | Allows you to set chmod on the stored file. For example chmod=664. | 664 | String |
| **disconnect** (common) | Whether or not to disconnect from remote FTP server right after use. Disconnect will only disconnect the current connection to the FTP server. If you have a consumer which you want to stop, then you need to stop the consumer/route instead. | false | boolean |
| **fileName** (producer) | Use Expression such as File Language to dynamically set the filename. For consumers, it’s used as a filename filter. For producers, it’s used to evaluate the filename to write. If an expression is set, it take precedence over the CamelFileName header. (Note: The header itself can also be an Expression). The expression options support both String and Expression types. If the expression is a String type, it is always evaluated using the File Language. If the expression is an Expression type, the specified Expression type is used - this allows you, for instance, to use OGNL expressions. For the consumer, you can use it to filter filenames, so you can for instance consume today’s file using the File Language syntax: mydata-$\\{date:now:yyyyMMdd}.txt. The producers support the CamelOverruleFileName header which takes precedence over any existing CamelFileName header; the CamelOverruleFileName is a header that is used only once, and makes it easier as this avoids to temporary store CamelFileName and have to restore it afterwards. |  | String |
| **flatten** (producer) | Flatten is used to flatten the file name path to strip any leading paths, so it’s just the file name. This allows you to consume recursively into sub-directories, but when you eg write the files to another directory they will be written in a single directory. Setting this to true on the producer enforces that any file name in CamelFileName header will be stripped for any leading paths. | false | boolean |
| **jailStartingDirectory** (producer) | Used for jailing (restricting) writing files to the starting directory (and sub) only. This is enabled by default to not allow Camel to write files to outside directories (to be more secured out of the box). You can turn this off to allow writing files to directories outside the starting directory, such as parent or root folders. | true | boolean |
| **strictHostKeyChecking** (producer) | 

Sets whether to use strict host key checking. Possible values are: no, yes.

Enum values:

-   no
    
-   yes
    





 | no | String |
| **allowNullBody** (producer (advanced)) | Used to specify if a null body is allowed during file writing. If set to true then an empty file will be created, when set to false, and attempting to send a null body to the file component, a GenericFileWriteException of 'Cannot write null body to file.' will be thrown. If the fileExist option is set to 'Override', then the file will be truncated, and if set to append the file will remain unchanged. | false | boolean |
| **disconnectOnBatchComplete** (producer (advanced)) | Whether or not to disconnect from remote FTP server right after a Batch upload is complete. disconnectOnBatchComplete will only disconnect the current connection to the FTP server. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **moveExistingFileStrategy** (producer (advanced)) | Strategy (Custom Strategy) used to move file with special naming token to use when fileExist=Move is configured. By default, there is an implementation used if no custom strategy is provided. |  | FileMoveExistingStrategy |
| **browseLimit** (advanced) | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | int |
| **connectTimeout** (advanced) | Sets the connect timeout for waiting for a connection to be established Used by both FTPClient and JSCH. | 10000 | int |
| **soTimeout** (advanced) | Sets the so timeout FTP and FTPS Is the SocketOptions.SO\_TIMEOUT value in millis. Recommended option is to set this to 300000 so as not have a hanged connection. On SFTP this option is set as timeout on the JSCH Session instance. | 300000 | int |
| **timeout** (advanced) | Sets the data timeout for waiting for reply Used only by FTPClient. | 30000 | int |
| **knownHostsFile** (security) | Sets the known\_hosts file, so that the jsch endpoint can do host key verification. You can prefix with classpath: to load the file from classpath instead of file system. |  | String |
| **password** (security) | Password to use for login. |  | String |
| **preferredAuthentications** (security) | Set a comma separated list of authentications that will be used in order of preference. Possible authentication methods are defined by JCraft JSCH. Some examples include: gssapi-with-mic,publickey,keyboard-interactive,password If not specified the JSCH and/or system defaults will be used. |  | String |
| **privateKeyBytes** (security) | Set the private key bytes to that the endpoint can do private key verification. This must be used only if privateKeyFile wasn’t set. Otherwise the file will have the priority. |  | byte\[\] |
| **privateKeyFile** (security) | Set the private key file to that the endpoint can do private key verification. You can prefix with classpath: to load the file from classpath instead of file system. |  | String |
| **privateKeyFilePassphrase** (security) | Set the private key file passphrase to that the endpoint can do private key verification. |  | String |
| **username** (security) | Username to use for login. |  | String |
| **useUserKnownHostsFile** (security) | If knownHostFile has not been explicit configured, then use the host file from System.getProperty(user.home) /.ssh/known\_hosts. | true | boolean |
| **ciphers** (security (advanced)) | Set a comma separated list of ciphers that will be used in order of preference. Possible cipher names are defined by JCraft JSCH. Some examples include: aes128-ctr,aes128-cbc,3des-ctr,3des-cbc,blowfish-cbc,aes192-cbc,aes256-cbc. If not specified the default list from JSCH will be used. |  | String |

## Limitations

Currently, camel-jsch only supports a [Producer](https://www.javadoc.io/doc/org.apache.camel/camel-api/current/org/apache/camel/Producer.md) (i.e., copy files to another host).

## Spring Boot Auto-Configuration

When using scp with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jsch-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.scp.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.scp.enabled** | Whether to enable auto configuration of the scp component. This is enabled by default. |  | Boolean |
| **camel.component.scp.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.scp.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.scp.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.scp.verbose-logging** | JSCH is verbose logging out of the box. Therefore we turn the logging down to DEBUG logging by default. But setting this option to true turns on the verbose logging again. | false | Boolean |