# Tar File

**Since Camel 2.16**

The Tar File Data Format is a message archiving format. Messages can be marshalled to Tar Files containing a single entry, and Tar Files containing a single entry can be unmarshalled to the original file contents. The Tar File is not compressed: for a `.tar.gz`, marshal it with the [gzipDeflater](gzipDeflater-dataformat.md) data format as well.

There is also an aggregation strategy that can aggregate multiple messages into a single Tar File.

## TarFile Options

The Tar File dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **usingIterator** (common) | `false` | `Boolean` | Whether to use an iterator to split tar entries when the tar file has more than one entry, for use with the splitter EIP in streaming mode. |
| **allowEmptyDirectory** (common) | `false` | `Boolean` | Whether to allow getting the iterator even if the directory is empty, when the tar file has more than one entry. |
| **preservePathElements** (common) | `false` | `Boolean` | Whether to preserve path elements when the file name contains path elements in the tar file. |
| **maxDecompressedSize** (advanced) | `1073741824` | `Integer` | The maximum decompressed size of a tar file (in bytes). An IOException is thrown if the decompressed size exceeds this amount. Set to -1 to disable. |

## Message Body

The message body at each side of the Tar File data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `text`, `bytes`, `stream` or `file` | The content of the one entry: text, bytes, a stream or a file. The entry size is taken from the content, not from the CamelFileLength header. |
| **Marshal output** | `stream`, as binary | The tar file, not compressed, in the stream cache, or a byte array when stream caching is off. The CamelFileName header is the entry name with .tar. |
| **Unmarshal input** | `bytes`, `stream` or `file`, as binary | A tar file with one entry, or with several when usingIterator. A .tar.gz is unmarshalled with gzipDeflater first. |
| **Unmarshal output** | `stream` | 
The content of the one file in the stream cache, or a byte array when stream caching is off; folder entries are skipped, and a tar with more files fails. With usingIterator, an Iterator for the split EIP: of messages with the content of one file each, in a stream cache.

-   With `usingIterator=true`: `iterator` (`org.apache.camel.dataformat.tarfile.TarIterator`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Marshal

In this example, we marshal a regular text/XML payload to a Tar File payload, and send it to an ActiveMQ queue called MY\_QUEUE.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .marshal().tarFile()
    .to("activemq:queue:MY_QUEUE");
```

```xml
<route>
    <from uri="direct:start"/>
    <marshal>
        <tarFile/>
    </marshal>
    <to uri="activemq:queue:MY_QUEUE"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            tarFile: {}
        - to:
            uri: activemq:queue:MY_QUEUE
```

The name of the Tar entry inside the created Tar File is based on the incoming `CamelFileName` message header, which is the standard message header used by the file component. Additionally, the outgoing `CamelFileName` message header is automatically set to the file name of the incoming `CamelFileName` message header, without its path, with the ".tar" suffix. So, for example, if the following route finds a file named "test.txt" in the input directory, the output will be a Tar File named "test.txt.tar" containing a single Tar entry named "test.txt":

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:input/directory?antInclude=*/.txt")
    .marshal().tarFile()
    .to("file:output/directory");
```

```xml
<route>
    <from uri="file:input/directory?antInclude=*/.txt"/>
    <marshal>
        <tarFile/>
    </marshal>
    <to uri="file:output/directory"/>
</route>
```

```yaml
- route:
    from:
      uri: file:input/directory
      parameters:
        antInclude: "*/.txt"
      steps:
        - marshal:
            tarFile: {}
        - to:
            uri: file:output/directory
```

If there is no incoming `CamelFileName` message header (for example, if the file component is not the consumer), then the message ID is used by default, and since the message ID is normally a unique generated ID, you will end up with filenames like `ID-MACHINENAME-2443-1211718892437-1-0.tar`. If you want to override this behavior, then you can set the value of the `CamelFileName` header explicitly in your route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader(Exchange.FILE_NAME, constant("report.txt"))
    .marshal().tarFile()
    .to("file:output/directory");
```

```xml
<route>
    <from uri="direct:start"/>
    <setHeader name="CamelFileName">
        <constant>report.txt</constant>
    </setHeader>
    <marshal>
        <tarFile/>
    </marshal>
    <to uri="file:output/directory"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelFileName
            constant: report.txt
        - marshal:
            tarFile: {}
        - to:
            uri: file:output/directory
```

This route would result in a Tar File named "report.txt.tar" in the output directory, containing a single Tar entry named "report.txt".

## Unmarshal

In this example we unmarshal a Tar File payload from an ActiveMQ queue called MY\_QUEUE to its original format, and forward it for processing to the `UnTarpedMessageProcessor`.

_Java-only: inline Processor class_

```java
from("activemq:queue:MY_QUEUE").unmarshal().tarFile().process(new UnTarpedMessageProcessor());
```

If the Tar File has more than one entry, the usingIterator option of TarFileDataFormat to be true, and you can use splitter to do the further work.

_Java-only: Java programmatic data format configuration_

```java
  TarFileDataFormat tarFile = new TarFileDataFormat();
  tarFile.setUsingIterator(true);
  from("file:src/test/resources/org/apache/camel/dataformat/tarfile/?delay=1000&noop=true")
    .unmarshal(tarFile)
    .split(bodyAs(Iterator.class))
        .streaming()
          .process(new UnTarpedMessageProcessor())
    .end();
```

Or you can use the TarSplitter as an expression for splitter directly like this

_Java-only: Java TarSplitter class_

```java
   from("file:src/test/resources/org/apache/camel/dataformat/tarfile?delay=1000&noop=true")
     .split(new TarSplitter())
        .streaming()
        .process(new UnTarpedMessageProcessor())
     .end();
```

> **Important**
> You cannot use TarSplitter in _parallel_ mode with the splitter.

## Aggregate

> **Note**
> Please note that this aggregation strategy requires eager completion check to work properly.

In this example, we aggregate all text files found in the input directory into a single Tar File that is stored in the output directory.

_Java-only: Java TarAggregationStrategy class_

```java
   from("file:input/directory?antInclude=*/.txt")
     .aggregate(new TarAggregationStrategy())
       .constant(true)
       .completionFromBatchConsumer()
       .eagerCheckCompletion()
   .to("file:output/directory");
```

The outgoing `CamelFileName` message header is created using java.io.File.createTempFile, with the ".tar" suffix. If you want to override this behavior, then you can set the value of the `CamelFileName` header explicitly in your route:

_Java-only: Java TarAggregationStrategy class_

```java
   from("file:input/directory?antInclude=*/.txt")
     .aggregate(new TarAggregationStrategy())
       .constant(true)
       .completionFromBatchConsumer()
       .eagerCheckCompletion()
     .setHeader(Exchange.FILE_NAME, constant("reports.tar"))
   .to("file:output/directory");
```

## Dependencies

To use Tar Files in your camel routes, you need to add a dependency on **camel-tarfile**, which implements this data format.

If you use Maven you can add the following to your `pom.xml`, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-tarfile</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```