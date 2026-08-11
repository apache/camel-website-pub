# Protobuf

**Since Camel 2.2**

Protobuf - Protocol Buffers

"Protocol Buffers - Google’s data interchange format"

Camel provides a Data Format to serialize between Java and the Protocol Buffer protocol. The project’s site details why you may wish to [choose this format over xml](https://developers.google.com/protocol-buffers/docs/overview). Protocol Buffer is language-neutral and platform-neutral, so messages produced by your Camel routes may be consumed by other language implementations.

[API Site](https://developers.google.com/protocol-buffers/docs/reference/java/)  
[Protobuf Implementation](https://github.com/google/protobuf)  

[Protobuf Java Tutorial](https://developers.google.com/protocol-buffers/docs/javatutorial)

## Protobuf Options

The Protobuf dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **instanceClass** (common) |  | `String` | Name of class to use when unmarshalling. |
| **contentTypeFormat** (common) | `native` | `Enum` | 
Defines a content type format in which protobuf message will be serialized/deserialized from(to) the Java been. The format can either be native or json for either native protobuf or json fields representation.

Enum values:

-   native
    
-   json
    





 |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |

## Content type format

It’s possible to parse JSON message to convert it to the protobuf format and unparse it back using native util converter. To use this option, set contentTypeFormat value to `json` or call protobuf with second parameter. If the default instance is not specified, always use the native protobuf format. The sample code shows below:

_Java-only: programmatic protobuf configuration with content type format_

```java
from("direct:marshal")
    .unmarshal()
    .protobuf("org.apache.camel.dataformat.protobuf.generated.AddressBookProtos$Person", "json")
    .to("mock:reverse");
```

## Input data type

This dataformat supports marshaling input data either as protobuf `Message` type or `Map` data type. In case of input data as `Map` type, first it will try to retrieve the data as `Map` using built-in type converters, if it fails to do so, it will fall back to retrieve it as proto `Message`.

## Output data type

As mentioned above, you can define the content type format to choose from JSON or native to serialize/deserialize data from/to. In addition, you can also obtain the data as `Map` and let this component do the heavy lifting to parse the data from proto `Message` to `Map`, you will need to set the `contentTypeFormat` to `native` and explicitly define the data type `Map` when you get body of the exchange. For instance: `exchange.getMessage().getBody(Map.class)`.

## Protobuf overview

This quick overview of how to use Protobuf. For more detail, see the [complete tutorial](https://developers.google.com/protocol-buffers/docs/javatutorial)

## Defining the proto format

The first step is to define the format for the body of your exchange. This is defined in a .proto file as so:

**addressbook.proto**

```protobuf
syntax = "proto2";

package org.apache.camel.component.protobuf;

option java_package = "org.apache.camel.component.protobuf";
option java_outer_classname = "AddressBookProtos";

message Person {
  required string name = 1;
  required int32 id = 2;
  optional string email = 3;

  enum PhoneType {
    MOBILE = 0;
    HOME = 1;
    WORK = 2;
  }

  message PhoneNumber {
    required string number = 1;
    optional PhoneType type = 2 [default = HOME];
  }

  repeated PhoneNumber phone = 4;
}

message AddressBook {
  repeated Person person = 1;
}
```

## Generating Java classes

The Protobuf SDK provides a compiler which will generate the Java classes for the format we defined in our `.proto` file. If your operating system is supported by [Protobuf Java code generator maven plugin](https://www.xolstice.org/protobuf-maven-plugin), you can automate protobuf Java code generating by adding the following configurations to your `pom.xml`:

Insert operating system and CPU architecture detection extension inside `<build>` tag of the project `pom.xml` or set `${os.detected.classifier}` parameter manually

```xml
<extensions>
  <extension>
    <groupId>kr.motd.maven</groupId>
    <artifactId>os-maven-plugin</artifactId>
    <version>1.4.1.Final</version>
  </extension>
</extensions>
```

Insert gRPC and protobuf Java code generator plugin **<plugins>** tag of the project `pom.xml`

```xml
<plugin>
  <groupId>org.xolstice.maven.plugins</groupId>
  <artifactId>protobuf-maven-plugin</artifactId>
  <version>0.5.0</version>
  <extensions>true</extensions>
  <executions>
    <execution>
      <goals>
        <goal>test-compile</goal>
        <goal>compile</goal>
      </goals>
      <configuration>
        <protocArtifact>com.google.protobuf:protoc:${protobuf-version}:exe:${os.detected.classifier}</protocArtifact>
      </configuration>
    </execution>
  </executions>
</plugin>
```

You can also run the compiler for any additional supported languages you require manually.

`protoc --java_out=. ./proto/addressbook.proto`

This will generate a single Java class named AddressBookProtos which contains inner classes for Person and AddressBook. Builders are also implemented for you. The generated classes implement com.google.protobuf.Message which is required by the serialization mechanism. For this reason it is important that only these classes are used in the body of your exchanges. Camel will throw an exception on route creation if you attempt to tell the Data Format to use a class that does not implement com.google.protobuf.Message. Use the generated builders to translate the data from any of your existing domain classes.

## Examples

You can use create the ProtobufDataFormat instance and pass it to Camel DataFormat marshal and unmarshal API like this.

_Java-only: programmatic ProtobufDataFormat instantiation_

```java
   ProtobufDataFormat format = new ProtobufDataFormat(Person.getDefaultInstance());

   from("direct:in").marshal(format);
   from("direct:back").unmarshal(format).to("mock:reverse");
```

Or use the DSL `protobuf()` passing the unmarshal default instance or default instance class name like this. However, if you have input data as `Map` type, you will need to **specify** the ProtobufDataFormat otherwise it will throw an error.

_Java-only: DSL protobuf() with class name and default instance_

```java
   // You don't need to specify the default instance for protobuf marshaling, but you will need in case your input data is a Map type
   from("direct:marshal").marshal().protobuf();
   from("direct:unmarshalA").unmarshal()
       .protobuf("org.apache.camel.dataformat.protobuf.generated.AddressBookProtos$Person")
       .to("mock:reverse");

   from("direct:unmarshalB").unmarshal().protobuf(Person.getDefaultInstance()).to("mock:reverse");
```

The following example shows how to use Protobuf to unmarshal:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .unmarshal().protobuf("org.apache.camel.dataformat.protobuf.generated.AddressBookProtos$Person")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <unmarshal>
    <protobuf instanceClass="org.apache.camel.dataformat.protobuf.generated.AddressBookProtos$Person"/>
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
            protobuf:
              instanceClass: org.apache.camel.dataformat.protobuf.generated.AddressBookProtos$Person
        - to:
            uri: mock:result
```

## Dependencies

To use Protobuf in your Camel routes, you need to add the dependency on **camel-protobuf**, which implements this data format.

Example pom.xml for `camel-protobuf`

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-protobuf</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```