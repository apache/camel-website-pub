# Avro

**Since Camel 2.14**

This component provides a dataformat for avro, which allows serialization and deserialization of messages using Apache Avro’s binary dataformat. Since Camel 3.2 rpc functionality was moved into separate `camel-avro-rpc` component.

> **Tip**
> There is also `camel-jackson-avro` which is a more powerful Camel dataformat for using Avro.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-avro</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

You can easily generate classes from a schema, using maven, ant etc. More details can be found at the [Apache Avro documentation](http://avro.apache.org/docs/current/).

## Avro Dataformat Options

The Avro dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **instanceClassName** (common) |  | `String` | Class name to use for marshal and unmarshalling. |
| **serializablePackages** (security) |  | `String` | Comma-separated list of additional packages that contain trusted Avro model classes. Avro 1.12 validates classes resolved from schemas; Camel automatically trusts packages derived from the configured schema or instance class. |

## Message Body

The message body at each side of the Avro data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `pojo` | An Avro record: an object of a class the Avro compiler generated, or a GenericRecord of the schema of instanceClassName. Without instanceClassName the schema comes from the class of the body, so a GenericRecord fails. A Map is not converted. |
| **Marshal output** | `stream`, as binary | The record in Avro binary encoding, without the schema (not an Avro container file), in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `bytes`, `stream` or `file`, as binary | One record in Avro binary encoding, as marshal writes it: unmarshal fails without instanceClassName (or a schema set in Java). |
| **Unmarshal output** | `pojo` | An object of the class instanceClassName names; a GenericRecord when a schema set in Java has no class on the classpath.
With `instanceClassName` set: an object of the class it names, or null.

 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).

## Examples

### Avro Data Format usage

Using the avro data format is as easy as specifying that the class that you want to marshal or unmarshal in your route.

_Java-only: programmatic AvroDataFormat with schema_

```java
AvroDataFormat format = new AvroDataFormat(Value.SCHEMA$);

from("direct:in").marshal(format).to("direct:marshal");
from("direct:back").unmarshal(format).to("direct:unmarshal");
```

Where Value is an Avro Maven Plugin Generated class.

The same route can be expressed in XML or YAML:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .marshal().avro("org.apache.camel.dataformat.avro.Message")
    .to("log:out");
```

```xml
<route>
    <from uri="direct:in"/>
    <marshal>
        <avro instanceClassName="org.apache.camel.dataformat.avro.Message" library="ApacheAvro"/>
    </marshal>
    <to uri="log:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - marshal:
            avro:
              instanceClassName: org.apache.camel.dataformat.avro.Message
              library: ApacheAvro
        - to:
            uri: log:out
```

An alternative can be to specify the dataformat inside the context and reference it from your route.

_XML-only: Spring XML data format configuration_

```xml
<camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
     <dataFormats>
        <avro id="avro" instanceClassName="org.apache.camel.dataformat.avro.Message" library="ApacheAvro"/>
    </dataFormats>
    <route>
        <from uri="direct:in"/>
        <marshal><custom ref="avro"/></marshal>
        <to uri="log:out"/>
    </route>
</camelContext>
```

In the same manner, you can unmarshal using the avro data format.