# Zip File

**Since Camel 2.11**

The Zip File Data Format is a message compression and decompression format. Messages can be marshaled (compressed) to Zip files containing a single entry, and Zip files containing a single entry can be unmarshalled (decompressed) to the original file contents. This data format supports ZIP64, as long as Java 7 or later is being used.

## ZipFile Options

The Zip File dataformat supports 4 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **usingIterator** (common) | `false` | `Boolean` | If the zip file has more than one entry, the setting this option to true, allows working with the splitter EIP, to split the data using an iterator in a streaming mode. |
| **allowEmptyDirectory** (common) | `false` | `Boolean` | If the zip file has more than one entry, setting this option to true, allows to get the iterator even if the directory is empty. |
| **preservePathElements** (common) | `false` | `Boolean` | If the file name contains path elements, setting this option to true, allows the path to be maintained in the zip file. |
| **maxDecompressedSize** (advanced) | `1073741824` | `Integer` | Set the maximum decompressed size of a zip file (in bytes). The default value if not specified corresponds to 1 gigabyte. An IOException will be thrown if the decompressed size exceeds this amount. Set to -1 to disable setting a maximum decompressed size. |

## Marshal

In this example, we marshal a regular text/XML payload to a compressed payload using Zip file compression, and send it to an ActiveMQ queue called MY\_QUEUE.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .marshal().zipFile()
    .to("activemq:queue:MY_QUEUE");
```

```xml
<route>
    <from uri="direct:start"/>
    <marshal>
        <zipFile/>
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
          zipFile: {}
      - to:
          uri: activemq:queue:MY_QUEUE
```

The name of the Zip entry inside the created Zip file is based on the incoming `CamelFileName` message header, which is the standard message header used by the file component. Additionally, the outgoing `CamelFileName` message header is automatically set to the value of the incoming `CamelFileName` message header, with the ".zip" suffix. So, for example, if the following route finds a file named "test.txt" in the input directory, the output will be a Zip file named "test.txt.zip" containing a single Zip entry named "test.txt":

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:input/directory?antInclude=*/.txt")
    .marshal().zipFile()
    .to("file:output/directory");
```

```xml
<route>
    <from uri="file:input/directory?antInclude=*/.txt"/>
    <marshal>
        <zipFile/>
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
          zipFile: {}
      - to:
          uri: file:output/directory
```

If there is no incoming `CamelFileName` message header, (for example, if the file component is not the consumer), then the message ID is used by default. Since the message ID is normally a unique generated ID, you will end up with filenames like `ID-MACHINENAME-2443-1211718892437-1-0.zip`. If you want to override this behavior, then you can set the value of the `CamelFileName` header explicitly in your route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader(Exchange.FILE_NAME, constant("report.txt"))
    .marshal().zipFile()
    .to("file:output/directory");
```

```xml
<route>
    <from uri="direct:start"/>
    <setHeader name="CamelFileName">
        <constant>report.txt</constant>
    </setHeader>
    <marshal>
        <zipFile/>
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
          zipFile: {}
      - to:
          uri: file:output/directory
```

This route would result in a Zip file named "report.txt.zip" in the output directory, containing a single Zip entry named "report.txt".

## Unmarshal

In this example we unmarshal a Zip file payload from an ActiveMQ queue called MY\_QUEUE to its original format, and forward it for processing to the `UnZippedMessageProcessor`.

_Java-only: inline Processor class_

```java
from("activemq:queue:MY_QUEUE")
    .unmarshal().zipFile()
    .process(new UnZippedMessageProcessor());
```

If the zip file has more than one entry, the usingIterator option of ZipFileDataFormat to be true, and you can use splitter to do the further work.

_Java-only: Java programmatic data format configuration_

```java
ZipFileDataFormat zipFile = new ZipFileDataFormat();
zipFile.setUsingIterator(true);

from("file:src/test/resources/org/apache/camel/dataformat/zipfile/?delay=1000&noop=true")
    .unmarshal(zipFile)
    .split(bodyAs(Iterator.class)).streaming()
        .process(new UnZippedMessageProcessor())
    .end();
```

Or you can use the ZipSplitter as an expression for splitter directly like this:

_Java-only: Java ZipSplitter class_

```java
from("file:src/test/resources/org/apache/camel/dataformat/zipfile?delay=1000&noop=true")
    .split(new ZipSplitter()).streaming()
        .process(new UnZippedMessageProcessor())
    .end();
```

> **Important**
> You **cannot** use ZipSplitter in _parallel_ mode with the splitter.

## Aggregate

> **Note**
> Please note that this aggregation strategy requires eager completion check to work properly.

In this example, we aggregate all text files found in the input directory into a single Zip file that is stored in the output directory.

_Java-only: Java ZipAggregationStrategy class_

```java
from("file:input/directory?antInclude=*/.txt")
    .aggregate(constant(true), new ZipAggregationStrategy())
        .completionFromBatchConsumer().eagerCheckCompletion()
        .to("file:output/directory");
```

The outgoing `CamelFileName` message header is created using java.io.File.createTempFile, with the ".zip" suffix. If you want to override this behavior, then you can set the value of the `CamelFileName` header explicitly in your route:

_Java-only: Java ZipAggregationStrategy class_

```java
from("file:input/directory?antInclude=*/.txt")
    .aggregate(constant(true), new ZipAggregationStrategy())
        .completionFromBatchConsumer().eagerCheckCompletion()
        .setHeader(Exchange.FILE_NAME, constant("reports.zip"))
        .to("file:output/directory");
```

## Dependencies

To use Zip files in your camel routes, you need to add a dependency on **camel-zipfile** which implements this data format.

If you use Maven you can add the following to your `pom.xml`, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-zipfile</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```