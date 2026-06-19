# Thrift

**Since Camel 2.20**

Camel provides a Data Format to serialize between Java and the [Apache Thrift](https://thrift.apache.org/). Apache Thrift is language-neutral and platform-neutral, so messages produced by your Camel routes may be consumed by other language implementations.

> **Note**
> Check the [Apache Thrift Implementation](https://github.com/apache/thrift) for additional details.

## Thrift Options

The Thrift dataformat supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **instanceClass** (common) |  | `String` | Name of class to use when unmarshalling. |
| **contentTypeFormat** (common) | `binary` | `Enum` | 
Defines a content type format in which thrift message will be serialized/deserialized from(to) the Java been. The format can either be native or json for either native binary thrift, json or simple json fields representation. The default value is binary.

Enum values:

-   binary
    
-   json
    
-   sjson
    





 |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |

## Content type format

It’s possible to parse JSON message to convert it to the Thrift format and serialize it back using native util converter. To use this option, set contentTypeFormat value to 'json' or call thrift with second parameter. If the default instance is not specified, always use the native binary Thrift format. The simple JSON format is write-only (marshal) and produces a simple output format suitable for parsing by scripting languages. The sample code shows below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:marshal")
    .unmarshal()
    .thrift("org.apache.camel.dataformat.thrift.generated.Work", "json")
    .to("mock:reverse");
```

```xml
<route>
  <from uri="direct:marshal"/>
  <unmarshal>
    <thrift instanceClass="org.apache.camel.dataformat.thrift.generated.Work" contentTypeFormat="json"/>
  </unmarshal>
  <to uri="mock:reverse"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:marshal
      steps:
        - unmarshal:
            thrift:
              instanceClass: org.apache.camel.dataformat.thrift.generated.Work
              contentTypeFormat: json
        - to:
            uri: mock:reverse
```

## Thrift overview

This quick overview of how to use Thrift. For more details, see the [complete tutorial](https://thrift.apache.org/tutorial/)

## Defining the thrift format

The first step is to define the format for the body of your exchange. This is defined in a .thrift file as so:

**tutorial.thrift**

```text
namespace java org.apache.camel.dataformat.thrift.generated

enum Operation {
  ADD = 1,
  SUBTRACT = 2,
  MULTIPLY = 3,
  DIVIDE = 4
}

struct Work {
  1: i32 num1 = 0,
  2: i32 num2,
  3: Operation op,
  4: optional string comment,
}
```

## Generating Java classes

The Apache Thrift provides a compiler which will generate the Java classes for the format we defined in our .thrift file.

You can also run the compiler for any additional supported languages you require manually.

`thrift -r --gen java -out ../java/ ./tutorial-dataformat.thrift`

This will generate separate Java class for each type defined in .thrift file, i.e., struct or enum. The generated classes implement org.apache.thrift.TBase which is required by the serialization mechanism. For this reason, it is important that only these classes are used in the body of your exchanges. Camel will throw an exception on route creation if you attempt to tell the Data Format to use a class that does not implement org.apache.thrift.TBase.

## Examples

You can use create the ThriftDataFormat instance and pass it to Camel DataFormat marshal and unmarshal API like this.

_Java-only: programmatic ThriftDataFormat instance_

```java
ThriftDataFormat format = new ThriftDataFormat(new Work());

from("direct:in").marshal(format);
from("direct:back").unmarshal(format).to("mock:reverse");
```

Or use the DSL thrift() passing the unmarshal default instance or default instance class name like this.

_Java-only: DSL thrift() with class name and instance parameters_

```java
// You don't need to specify the default instance for the thrift marshaling
from("direct:marshal").marshal().thrift();
from("direct:unmarshalA").unmarshal()
    .thrift("org.apache.camel.dataformat.thrift.generated.Work")
    .to("mock:reverse");

from("direct:unmarshalB").unmarshal().thrift(new Work()).to("mock:reverse");
```

The following example shows how to use Thrift to unmarshal:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .unmarshal().thrift("org.apache.camel.dataformat.thrift.generated.Work")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <unmarshal>
    <thrift instanceClass="org.apache.camel.dataformat.thrift.generated.Work"/>
  </unmarshal>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - unmarshal:
            thrift:
              instanceClass: org.apache.camel.dataformat.thrift.generated.Work
        - to:
            uri: mock:result
```

## Dependencies

To use Thrift in your Camel routes, you need to add a dependency on **camel-thrift**, which implements this data format.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-thrift</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```