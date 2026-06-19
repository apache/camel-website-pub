# SWIFT MX

**Since Camel 3.20**

The SWIFT MX data format is used to encode and decode SWIFT MX messages. The data format leverages the library [Prowide ISO 20022](https://github.com/prowide/prowide-iso20022) to encode and decode SWIFT MX messages.

## Options

The SWIFT MX dataformat supports 4 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **writeInJson** (common) | `false` | `Boolean` | The flag indicating that messages must be marshalled in a JSON format. |
| **readMessageId** (advanced) |  | `Object` | The type of MX message to produce when unmarshalling an input stream. If not set, it will be automatically detected from the namespace used. |
| **readConfig** (advanced) |  | `Object` | Refers to a specific configuration to use when unmarshalling an input stream to lookup from the registry. |
| **writeConfig** (advanced) |  | `Object` | Refers to a specific configuration to use when marshalling a message to lookup from the registry. |

In Spring DSL, you configure the data format using this tag:

_XML-only: Spring XML data format configuration_

```xml
<camelContext>
    <dataFormats>
        <swiftMx id="swiftInJson" writeInJson="true"/>
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
    .marshal().swiftMx()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:startEncode" />
    <marshal>
        <swiftMx />
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
            swiftMx: {}
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
    .marshal().swiftMx()
    .to("file://data.bin");
```

```xml
<route>
  <from uri="jms://myqueue"/>
  <marshal>
    <swiftMx/>
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
            swiftMx: {}
        - to:
            uri: file://data.bin
```

## Unmarshal

The unmarshaller converts the input data into the concrete class of type `com.prowidesoftware.swift.model.mx.AbstractMX` that best matches with the content of the message.

In this example, we unmarshal the content of a file to get SWIFT MX objects before processing them with the `newOrder` processor.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://data.bin")
    .unmarshal().swiftMx()
    .process("newOrder");
```

```xml
<route>
  <from uri="file://data.bin"/>
  <unmarshal>
    <swiftMx/>
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
            swiftMx: {}
        - to:
            uri: bean:newOrder
```

## Dependencies

To use SWIFT MX in your Camel routes, you need to add a dependency on **camel-swift** which implements this data format.

If you use Maven, you can add the following to your pom.xml:

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-swift</artifactId>
  <version>x.x.x</version>  <!-- use the same version as your Camel core version -->
</dependency>
```