# HDFS

**Since Camel 2.14**

**Both producer and consumer are supported**

The HDFS component enables you to read and write messages from/to an HDFS file system using Hadoop 2.x. HDFS is the distributed file system at the heart of [Hadoop](http://hadoop.apache.org).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-hdfs</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

hdfs://hostname\[:port\]\[/path\]\[?options\]

The path is treated in the following way:

1.  as a consumer, if it’s a file, it just reads the file, otherwise if it represents a directory it scans all the file under the path satisfying the configured pattern. All the files under that directory must be of the same type.
    
2.  as a producer, if at least one split strategy is defined, the path is considered a directory and under that directory the producer creates a different file per split named using the configured UuidGenerator.
    

When consuming from hdfs then in normal mode, a file is split into chunks, producing a message per chunk. You can configure the size of the chunk using the chunkSize option. If you want to read from hdfs and write to a regular file using the file component, then you can use the fileMode=Append to append each of the chunks together.

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

The HDFS component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **jAASConfiguration** (security) | To use the given configuration for security with JAAS. |  | Configuration |
| **kerberosConfigFile** (security) | To use kerberos authentication, set the value of the 'java.security.krb5.conf' environment variable to an existing file. If the environment variable is already set, warn if different than the specified parameter. |  | String |

## Endpoint Options

The HDFS endpoint is configured using URI syntax:

hdfs:hostName:port/path

with the following path and query parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **hostName** (common) | **Required** HDFS host to use. |  | String |
| **port** (common) | HDFS port to use. | 8020 | int |
| **path** (common) | **Required** The directory path to use. |  | String |

### Query Parameters (45 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectOnStartup** (common) | Whether to connect to the HDFS file system on starting the producer/consumer. If false then the connection is created on-demand. Notice that HDFS may take up till 15 minutes to establish a connection, as it has hardcoded 45 x 20 sec redelivery. By setting this option to false allows your application to startup, and not block for up till 15 minutes. | true | boolean |
| **fileSystemType** (common) | 
Set to LOCAL to not use HDFS but local java.io.File instead.

Enum values:

-   LOCAL
    
-   HDFS
    





 | HDFS | HdfsFileSystemType |
| **fileType** (common) | 

The file type to use. For more details see Hadoop HDFS documentation about the various files types.

Enum values:

-   NORMAL\_FILE
    
-   SEQUENCE\_FILE
    
-   MAP\_FILE
    
-   BLOOMMAP\_FILE
    
-   ARRAY\_FILE
    





 | NORMAL\_FILE | HdfsFileType |
| **keyType** (common) | 

The type for the key in case of sequence or map files.

Enum values:

-   NULL
    
-   BOOLEAN
    
-   BYTE
    
-   SHORT
    
-   INT
    
-   FLOAT
    
-   LONG
    
-   DOUBLE
    
-   TEXT
    
-   BYTES
    





 | NULL | WritableType |
| **namedNodes** (common) | A comma separated list of named nodes (e.g. srv11.example.com:8020,srv12.example.com:8020). |  | String |
| **owner** (common) | The file owner must match this owner for the consumer to pickup the file. Otherwise the file is skipped. |  | String |
| **valueType** (common) | 

The type for the key in case of sequence or map files.

Enum values:

-   NULL
    
-   BOOLEAN
    
-   BYTE
    
-   SHORT
    
-   INT
    
-   FLOAT
    
-   LONG
    
-   DOUBLE
    
-   TEXT
    
-   BYTES
    





 | BYTES | WritableType |
| **pattern** (consumer) | The pattern used for scanning the directory. | \* | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **streamDownload** (consumer) | Sets the download method to use when not using a local working directory. If set to true, the remote files are streamed to the route as they are read. When set to false, the remote files are loaded into memory before being sent into the route. | false | boolean |
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
| **append** (producer) | Append to existing file. Notice that not all HDFS file systems support the append option. | false | boolean |
| **overwrite** (producer) | Whether to overwrite existing files with the same name. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **blockSize** (advanced) | The size of the HDFS blocks. | 67108864 | long |
| **bufferSize** (advanced) | The buffer size used by HDFS. | 4096 | int |
| **checkIdleInterval** (advanced) | How often (time in millis) in to run the idle checker background task. This option is only in use if the splitter strategy is IDLE. | 500 | int |
| **chunkSize** (advanced) | When reading a normal file, this is split into chunks producing a message per chunk. | 4096 | int |
| **compressionCodec** (advanced) | 

The compression codec to use.

Enum values:

-   DEFAULT
    
-   GZIP
    
-   BZIP2
    
-   SNAPPY
    
-   LZ4
    
-   ZSTANDARD
    





 | DEFAULT | HdfsCompressionCodec |
| **compressionType** (advanced) | 

The compression type to use (is default not in use).

Enum values:

-   NONE
    
-   RECORD
    
-   BLOCK
    





 | NONE | CompressionType |
| **openedSuffix** (advanced) | When a file is opened for reading/writing the file is renamed with this suffix to avoid to read it during the writing phase. | opened | String |
| **readSuffix** (advanced) | Once the file has been read is renamed with this suffix to avoid to read it again. | read | String |
| **replication** (advanced) | The HDFS replication factor. | 3 | short |
| **splitStrategy** (advanced) | In the current version of Hadoop opening a file in append mode is disabled since it’s not very reliable. So, for the moment, it’s only possible to create new files. The Camel HDFS endpoint tries to solve this problem in this way: If the split strategy option has been defined, the hdfs path will be used as a directory and files will be created using the configured UuidGenerator. Every time a splitting condition is met, a new file is created. The splitStrategy option is defined as a string with the following syntax: splitStrategy=ST:value,ST:value,…​ where ST can be: BYTES a new file is created, and the old is closed when the number of written bytes is more than value MESSAGES a new file is created, and the old is closed when the number of written messages is more than value IDLE a new file is created, and the old is closed when no writing happened in the last value milliseconds. |  | String |
| **maxMessagesPerPoll** (filter) | To define a maximum messages to gather per poll. By default a limit of 100 is set. Can be used to set a limit of e.g. 1000 to avoid when starting up the server that there are thousands of files. Values can only be greater than 0. Notice: If this option is in use then the limit will be applied on the valid files. For example if you have 100000 files and use maxMessagesPerPoll=500, then only the first 500 files will be picked up. | 100 | int |
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
| **kerberosConfigFileLocation** (security) | The location of the kerb5.conf file ([https://web.mit.edu/kerberos/krb5-1.12/doc/admin/conf\_files/krb5\_conf.html](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/conf_files/krb5_conf.md)). |  | String |
| **kerberosKeytabLocation** (security) | The location of the keytab file used to authenticate with the kerberos nodes (contains pairs of kerberos principals and encrypted keys (which are derived from the Kerberos password)). |  | String |
| **kerberosUsername** (security) | The username used to authenticate with the kerberos nodes. |  | String |

## Message Headers

The HDFS component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHdfsClose** (producer) Constant: [`HDFS_CLOSE`](https://javadoc.io/doc/org.apache.camel/camel-hdfs/latest/org/apache/camel/component/hdfs/HdfsConstants.html#HDFS_CLOSE) | Indicates to close the stream. |  | Boolean |
| **CamelFileName** (common) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-hdfs/latest/org/apache/camel/component/hdfs/HdfsConstants.html#FILE_NAME) | (producer) Specifies the name of the file to write (relative to the endpoint path). The name can be a String or an Expression object. Only relevant when not using a split strategy. (consumer) Specifies the name of the file to read. |  | String |
| **CamelFileNameConsumed** (consumer) Constant: [`FILE_NAME_CONSUMED`](https://javadoc.io/doc/org.apache.camel/camel-hdfs/latest/org/apache/camel/component/hdfs/HdfsConstants.html#FILE_NAME_CONSUMED) | The name of the file consumed. |  | String |
| **CamelFileAbsolutePath** (consumer) Constant: [`FILE_ABSOLUTE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-hdfs/latest/org/apache/camel/component/hdfs/HdfsConstants.html#FILE_ABSOLUTE_PATH) | The absolute path of the file. |  | String |
| **KEY** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-hdfs/latest/org/apache/camel/component/hdfs/HdfsConstants.html#KEY) | The HDFS key. |  | Object |
| **CamelFileLength** (consumer) Constant: [`FILE_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-hdfs/latest/org/apache/camel/component/hdfs/HdfsConstants.html#FILE_LENGTH) | The size of the file. |  | Long |

## KeyType and ValueType

-   NULL it means that the key or the value is absent
    
-   BYTE for writing a byte, the java Byte class is mapped into a BYTE
    
-   BYTES for writing a sequence of bytes. It maps the java ByteBuffer class
    
-   SHORT for writing java short
    
-   INT for writing java integer
    
-   FLOAT for writing java float
    
-   LONG for writing java long
    
-   DOUBLE for writing java double
    
-   TEXT for writing java strings
    

BYTES is also used with everything else, for example, in Camel a file is sent around as an InputStream, int this case is written in a sequence file or a map file as a sequence of bytes.

## Splitting Strategy

In the current version of Hadoop opening a file in append mode is disabled since it’s not very reliable. So, for the moment, it’s only possible to create new files. The Camel HDFS endpoint tries to solve this problem in this way:

-   If the split strategy option has been defined, the hdfs path will be used as a directory and files will be created using the configured UuidGenerator
    
-   Every time a splitting condition is met, a new file is created.  
    The splitStrategy option is defined as a string with the following syntax: splitStrategy=<ST>:<value>,<ST>:<value>,\*
    

where <ST> can be:

-   BYTES a new file is created, and the old is closed when the number of written bytes is more than <value>
    
-   MESSAGES a new file is created, and the old is closed when the number of written messages is more than <value>
    
-   IDLE a new file is created, and the old is closed when no writing happened in the last <value> milliseconds
    

note that this strategy currently requires either setting an IDLE value or setting the HdfsConstants.HDFS\_CLOSE header to false to use the BYTES/MESSAGES configuration…​otherwise, the file will be closed with each message

for example:

hdfs://localhost/tmp/simple-file?splitStrategy=IDLE:1000,BYTES:5

it means: a new file is created either when it has been idle for more than 1 second or if more than 5 bytes have been written. So, running `hadoop fs -ls /tmp/simple-file` you’ll see that multiple files have been created.

## Controlling to close file stream

When using the [HDFS](#) producer **without** a split strategy, then the file output stream is by default closed after the write. However you may want to keep the stream open, and only explicitly close the stream later. For that you can use the header `HdfsConstants.HDFS_CLOSE` (value = `"CamelHdfsClose"`) to control this. Setting this value to a boolean allows you to explicit control whether the stream should be closed or not.

Notice this does not apply if you use a split strategy, as there are various strategies that can control when the stream is closed.

## Using this component in OSGi

There are some quirks when running this component in an OSGi environment related to the mechanism Hadoop 2.x uses to discover different `org.apache.hadoop.fs.FileSystem` implementations. Hadoop 2.x uses `java.util.ServiceLoader` which looks for `/META-INF/services/org.apache.hadoop.fs.FileSystem` files defining available filesystem types and implementations. These resources are not available when running inside OSGi.

As with `camel-hdfs` component, the default configuration files need to be visible from the bundle class loader. A typical way to deal with it is to keep a copy of `core-default.xml` (and e.g., `hdfs-default.xml`) in your bundle root.

### Using this component with manually defined routes

There are two options:

1.  Package `/META-INF/services/org.apache.hadoop.fs.FileSystem` resource with bundle that defines the routes. This resource should list all the required Hadoop 2.x filesystem implementations.
    
2.  Provide boilerplate initialization code which populates internal, static cache inside `org.apache.hadoop.fs.FileSystem` class:
    

```java
org.apache.hadoop.conf.Configuration conf = new org.apache.hadoop.conf.Configuration();
conf.setClass("fs.file.impl", org.apache.hadoop.fs.LocalFileSystem.class, FileSystem.class);
conf.setClass("fs.hdfs.impl", org.apache.hadoop.hdfs.DistributedFileSystem.class, FileSystem.class);
...
FileSystem.get("file:///", conf);
FileSystem.get("hdfs://localhost:9000/", conf);
...
```

### Using this component with Blueprint container

Two options:

1.  Package `/META-INF/services/org.apache.hadoop.fs.FileSystem` resource with bundle that contains blueprint definition.
    
2.  Add the following to the blueprint definition file:
    

```xml
<bean id="hdfsOsgiHelper" class="org.apache.camel.component.hdfs.HdfsOsgiHelper">
   <argument>
      <map>
         <entry key="file:///" value="org.apache.hadoop.fs.LocalFileSystem"  />
         <entry key="hdfs://localhost:9000/" value="org.apache.hadoop.hdfs.DistributedFileSystem" />
         ...
      </map>
   </argument>
</bean>

<bean id="hdfs" class="org.apache.camel.component.hdfs.HdfsComponent" depends-on="hdfsOsgiHelper" />
```

This way Hadoop 2.x will have correct mapping of URI schemes to filesystem implementations.

### Using this component with a HighAvailability configuration

In a HA setup, there will be multiple nodes (_configured through the **namedNodes** parameter_). The "hostname" and "port" portion of the endpoint uri will no longer have a _"host"_ meaning, but it will represent the name given to the cluster.

You can choose whatever name you want for the cluster (_the name should follow the \[a-zA-Z0-9\] convention_). This name will be sanitized by replacing the _dirty_ characters with underscore. This is done so that a host name or ip could pottentialy be used, if it makes sense to you.

The cluster name will be mapped to the HA filesystem with a coresponding proxy, with failover, and the _works_.

```java
from("hdfs://node1_and_2_cluster/dir1/dir2?namedNodes=node1.exemple.org:8020,node2.exemple.org:8020").routeId(...)
...
```

### Using this component with Kerberos authentication

The kerberos config file is read when the camel component is created, not when the endpoint is created. Because of this, the config file must be set at startup, with a call like:

```java
static {
  HdfsComponent.setKerberosConfigFile("/etc/security/kerb5.conf");
}
```

## Spring Boot Auto-Configuration

When using hdfs with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-hdfs-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.hdfs.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hdfs.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hdfs.enabled** | Whether to enable auto configuration of the hdfs component. This is enabled by default. |  | Boolean |
| **camel.component.hdfs.j-a-a-s-configuration** | To use the given configuration for security with JAAS. The option is a javax.security.auth.login.Configuration type. |  | Configuration |
| **camel.component.hdfs.kerberos-config-file** | To use kerberos authentication, set the value of the 'java.security.krb5.conf' environment variable to an existing file. If the environment variable is already set, warn if different than the specified parameter. |  | String |
| **camel.component.hdfs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |