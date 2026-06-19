# SWIFT MT

**Since Camel 3.20**

The SWIFT MT data format is used to encode and decode SWIFT MT messages. The data format leverages the library [Prowide Core](https://github.com/prowide/prowide-core) to encode and decode SWIFT MT messages.

## Options

The SWIFT MT dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **writeInJson** (common) | `false` | `Boolean` | The flag indicating that messages must be marshalled in a JSON format. |

In Spring DSL, you configure the data format using this tag:

_XML-only: Spring XML data format configuration_

```xml
<camelContext>
    <dataFormats>
        <swiftMt id="swiftInJson" writeInJson="true"/>
    </dataFormats>
    ...
</camelContext>
```

Then you can use it later by its reference:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:startEncode")
    .marshal("swiftInJson")
    .to("mock:result");
```

```xml
<route>
     <from uri="direct:startEncode" />
     <marshal ref="swiftInJson" />
     <to uri="mock:result" />
</route>
```

```yaml
- route:
    from:
      uri: direct:startEncode
      steps:
        - marshal:
            ref: swiftInJson
        - to:
            uri: mock:result
```

Most of the time, you won’t need to declare the data format if you use the default options. In that case, you can declare the data format inline as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:startEncode")
    .marshal().swiftMt()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:startEncode" />
    <marshal>
        <swiftMt />
    </marshal>
    <to uri="mock:result" />
</route>
```

```yaml
- route:
    from:
      uri: direct:startEncode
      steps:
        - marshal:
            swiftMt: {}
        - to:
            uri: mock:result
```

## Marshal

In this example, we marshal the messages read from a JMS queue in SWIFT format before storing the result into a file.

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms://myqueue")
    .marshal().swiftMt()
    .to("file://data.bin");
```

```xml
<route>
  <from uri="jms://myqueue"/>
  <marshal>
    <swiftMt/>
  </marshal>
  <to uri="file://data.bin"/>
</route>
```

```yaml
- route:
    from:
      uri: jms://myqueue
      steps:
        - marshal:
            swiftMt: {}
        - to:
            uri: file://data.bin
```

## Unmarshal

The unmarshaller converts the input data into the concrete class of type `com.prowidesoftware.swift.model.mt.AbstractMT` that best matches with the content of the message.

In this example, we unmarshal the content of a file to get SWIFT MT objects before processing them with the `newOrder` processor.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://data.bin")
    .unmarshal().swiftMt()
    .process("newOrder");
```

```xml
<route>
  <from uri="file://data.bin"/>
  <unmarshal>
    <swiftMt/>
  </unmarshal>
  <to uri="bean:newOrder"/>
</route>
```

```yaml
- route:
    from:
      uri: file://data.bin
      steps:
        - unmarshal:
            swiftMt: {}
        - to:
            uri: bean:newOrder
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