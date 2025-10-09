# Stream

**Since Camel 1.3**

**Both producer and consumer are supported**

The Stream component provides access to the `System.in`, `System.out` and `System.err` streams as well as allowing streaming of file.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-stream</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

stream:in\[?options\]
stream:out\[?options\]
stream:err\[?options\]
stream:header\[?options\]
stream:file?fileName=/foo/bar.txt
stream:http?httpUrl=http:myserver:8080/data

If the `stream:header` URI is specified, the `stream` header is used to find the stream to write to. This option is available only for stream producers (that is, it cannot appear in `from()`).

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

The Stream component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Stream endpoint is configured using URI syntax:

stream:kind

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **kind** (common) | 
**Required** Kind of stream to use such as System.in, System.out, a file, or a http url.

Enum values:

-   in
    
-   out
    
-   err
    
-   header
    
-   file
    
-   http
    





 |  | String |

### Query Parameters (23 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **encoding** (common) | You can configure the encoding (is a charset name) to use text-based streams (for example, message body is a String object). If not provided, Camel uses the JVM default Charset. |  | String |
| **fileName** (common) | When using the stream:file URI format, this option specifies the filename to stream to/from. |  | String |
| **fileWatcher** (consumer) | To use JVM file watcher to listen for file change events to support re-loading files that may be overwritten, somewhat like tail --retry. | false | boolean |
| **groupLines** (consumer) | To group X number of lines in the consumer. For example to group 10 lines and therefore only spit out an Exchange with 10 lines, instead of 1 Exchange per line. |  | int |
| **groupStrategy** (consumer) | Allows to use a custom GroupStrategy to control how to group lines. |  | GroupStrategy |
| **httpHeaders** (consumer) | When using stream:http format, this option specifies optional http headers, such as Accept: application/json. Multiple headers can be separated by comma. |  | String |
| **httpUrl** (consumer) | When using stream:http format, this option specifies the http url to stream from. |  | String |
| **initialPromptDelay** (consumer) | Initial delay in milliseconds before showing the message prompt. This delay occurs only once. Can be used during system startup to avoid message prompts being written while other logging is done to the system out. | 2000 | long |
| **promptDelay** (consumer) | Optional delay in milliseconds before showing the message prompt. |  | long |
| **promptMessage** (consumer) | Message prompt to use when reading from stream:in; for example, you could set this to Enter a command:. |  | String |
| **readLine** (consumer) | Whether to read the input stream in line mode (terminate by line breaks). Setting this to false, will instead read the entire stream until EOL. | true | boolean |
| **retry** (consumer) | Will retry opening the stream if it’s overwritten, somewhat like tail --retry If reading from files then you should also enable the fileWatcher option, to make it work reliable. | false | boolean |
| **scanStream** (consumer) | To be used for continuously reading a stream such as the unix tail command. | false | boolean |
| **scanStreamDelay** (consumer) | Delay in milliseconds between read attempts when using scanStream. |  | long |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **appendNewLine** (producer) | Whether to append a new line character at end of output. | true | boolean |
| **autoCloseCount** (producer) | Number of messages to process before closing stream on Producer side. Never close stream by default (only when Producer is stopped). If more messages are sent, the stream is reopened for another autoCloseCount batch. |  | int |
| **closeOnDone** (producer) | This option is used in combination with Splitter and streaming to the same file. The idea is to keep the stream open and only close when the Splitter is done, to improve performance. Mind this requires that you only stream to the same file, and not 2 or more files. | false | boolean |
| **delay** (producer) | Initial delay in milliseconds before producing the stream. |  | long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **readTimeout** (advanced) | Sets the read timeout to a specified timeout, in milliseconds. A non-zero value specifies the timeout when reading from Input stream when a connection is established to a resource. If the timeout expires before there is data available for read, a java.net.SocketTimeoutException is raised. A timeout of zero is interpreted as an infinite timeout. |  | int |

## Message Headers

The Stream component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelStreamIndex** (consumer) Constant: [`STREAM_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-stream/latest/org/apache/camel/component/stream/StreamConstants.html#STREAM_INDEX) | The index. |  | long |
| **CamelStreamComplete** (consumer) Constant: [`STREAM_COMPLETE`](https://javadoc.io/doc/org.apache.camel/camel-stream/latest/org/apache/camel/component/stream/StreamConstants.html#STREAM_COMPLETE) | Is complete. |  | boolean |

## Message content

The Stream component supports either `String` or `byte[]` for writing to streams. Just add either `String` or `byte[]` content to the `message.in.body`. Messages sent to the **stream:** producer in binary mode are not followed by the newline character (as opposed to the `String` messages). Message with `null` body will not be appended to the output stream.  
The special `stream:header` URI is used for custom output streams. Just add a `java.io.OutputStream` object to `message.in.header` in the key `header`.  
See samples for an example.

## Samples

In the following sample we route messages from the `direct:in` endpoint to the `System.out` stream:

```java
// Route messages to the standard output.
from("direct:in").to("stream:out");

// Send String payload to the standard output.
// Message will be followed by the newline.
template.sendBody("direct:in", "Hello Text World");

// Send byte[] payload to the standard output.
// No newline will be added after the message.
template.sendBody("direct:in", "Hello Bytes World".getBytes());
```

The following sample demonstrates how the header type can be used to determine which stream to use. In the sample we use our own output stream, `MyOutputStream`.

The following sample demonstrates how to continuously read a file stream (analogous to the UNIX `tail` command):

```java
from("stream:file?fileName=/server/logs/server.log&scanStream=true&scanStreamDelay=1000")
  .to("bean:logService?method=parseLogLine");
```

If you want to re-load the file if it rollover/rewritten then you should also turn on the `fileWatcher` and `retry` options.

```java
from("stream:file?fileName=/server/logs/server.log&scanStream=true&scanStreamDelay=1000&retry=true&fileWatcher=true")
  .to("bean:logService?method=parseLogLine");
```

## Reading HTTP server side streaming

The camel-stream component has basic support for connecting to a remote HTTP server and read streaming data (chunk of data separated by new-line).

```java
from("stream:http?scanStream=true&httpUrl=http://localhost:8500")
  .to("log:input");
```

## Spring Boot Auto-Configuration

When using stream with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-stream-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.stream.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.stream.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.stream.enabled** | Whether to enable auto configuration of the stream component. This is enabled by default. |  | Boolean |
| **camel.component.stream.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |