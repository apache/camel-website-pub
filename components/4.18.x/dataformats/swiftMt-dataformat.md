# SWIFT MT

**Since Camel 3.20**

The SWIFT MT data format is used to encode and decode SWIFT MT messages. The data format leverages the library [Prowide Core](https://github.com/prowide/prowide-core) to encode and decode SWIFT MT messages.

## Options

The SWIFT MT dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **writeInJson** (common) | `false` | `Boolean` | The flag indicating that messages must be marshalled in a JSON format. |

In Spring DSL, you configure the data format using this tag:

```xml
<camelContext>
    <dataFormats>
        <swiftMt id="swiftInJson" writeInJson="true"/>
    </dataFormats>
    ...
</camelContext>
```

Then you can use it later by its reference:

```xml
<route>
     <from uri="direct:startEncode" />
     <marshal ref="swiftInJson" />
     <to uri="mock:result" />
</route>
```

Most of the time, you won’t need to declare the data format if you use the default options. In that case, you can declare the data format inline as shown below:

```xml
<route>
    <from uri="direct:startEncode" />
    <marshal>
        <swiftMt />
    </marshal>
    <to uri="mock:result" />
</route>
```

## Marshal

In this example, we marshal the messages read from a JMS queue in SWIFT format before storing the result into a file.

```java
from("jms://myqueue")
    .marshal().swiftMt()
    .to("file://data.bin");
```

In Spring DSL:

```xml
 <from uri="jms://myqueue">
 <marshal>
     <swiftMt/>
 </marshal>
 <to uri="file://data.bin"/>
```

## Unmarshal

The unmarshaller converts the input data into the concrete class of type `com.prowidesoftware.swift.model.mt.AbstractMT` that best matches with the content of the message.

In this example, we unmarshal the content of a file to get SWIFT MT objects before processing them with the `newOrder` processor.

SwiftMt example in Java

```java
from("file://data.bin")
    .unmarshal().swiftMt()
    .process("newOrder");
```

SwiftMt example in In Spring DSL

```xml
 <from uri="file://data.bin">
 <unmarshal>
     <swiftMt/>
 </unmarshal>
 <to uri="bean:newOrder"/>
```

## Dependencies

To use SWIFT MT in your Camel routes, you need to add a dependency on **camel-swift** which implements this data format.

If you use Maven, you can add the following to your `pom.xml`:

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-swift</artifactId>
  <version>x.x.x</version>  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using swiftMt with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-swift-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.swift-mt.enabled** | Whether to enable auto configuration of the swiftMt data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.swift-mt.write-in-json** | The flag indicating that messages must be marshalled in a JSON format. | false | Boolean |
| **camel.dataformat.swift-mx.enabled** | Whether to enable auto configuration of the swiftMx data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.swift-mx.read-config** | Refers to a specific configuration to use when unmarshalling an input stream to lookup from the registry. The option is a com.prowidesoftware.swift.model.mx.MxReadConfiguration type. |  | String |
| **camel.dataformat.swift-mx.read-message-id** | The type of MX message to produce when unmarshalling an input stream. If not set, it will be automatically detected from the namespace used. The option is a com.prowidesoftware.swift.model.MxId type. |  | String |
| **camel.dataformat.swift-mx.write-config** | Refers to a specific configuration to use when marshalling a message to lookup from the registry. The option is a com.prowidesoftware.swift.model.mx.MxWriteConfiguration type. |  | String |
| **camel.dataformat.swift-mx.write-in-json** | The flag indicating that messages must be marshalled in a JSON format. | false | Boolean |