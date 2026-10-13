# SWIFT MT

**Since Camel 3.20**

The SWIFT MT data format is used to encode and decode SWIFT MT messages. The data format leverages the library [Prowide Core](https://github.com/prowide/prowide-core) to encode and decode SWIFT MT messages.

## Options

The SWIFT MT dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **writeInJson** (common) | `false` | `Boolean` | Whether to marshal messages in JSON format. |

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
     <marshal>
       <custom ref="swiftInJson" />
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
            custom:
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

## Translating between MT and MX

The SWIFT MT and [SWIFT MX](swiftMx-dataformat.md) data formats read and write messages, but they do not translate one format into the other. They also do not validate messages against SWIFT network rules or usage guidelines such as CBPR+ or SEPA.

To convert a message, such as an MT103 into a pacs.008, unmarshal it with SWIFT MT, map the fields to an ISO 20022 model class such as `MxPacs00800108` in your own bean or processor, and marshal the result with SWIFT MX. The other direction works the same way, starting with SWIFT MX.

Translation that follows the official SWIFT mapping rules is outside the scope of Camel. Use a dedicated translation product or service for that.

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