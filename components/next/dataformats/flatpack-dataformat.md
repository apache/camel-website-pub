# Flatpack

**Since Camel 2.1**

The [Flatpack](../flatpack-component.md) component ships with the Flatpack data format that can be used to format between fixed width or delimited text messages to a `List` of rows as `Map`.

-   marshal = from `List<Map<String, Object>>` to `OutputStream` (can be converted to `String`)
    
-   unmarshal = from `java.io.InputStream` (such as a `File` or `String`) to a `java.util.List` as an `org.apache.camel.component.flatpack.DataSetList` instance.  
    The result of the operation will contain all the data. If you need to process each row one by one you can split the exchange, using Splitter.
    

**Notice:** The Flatpack library does currently not support header and trailers for the marshal operation.

## Options

The Flatpack dataformat supports 8 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **definition** (common) |  | `String` | The flatpack pzmap configuration file. Can be omitted in simpler situations, but its preferred to use the pzmap. |
| **fixed** (common) | `false` | `Boolean` | Delimited or fixed. Is by default false = delimited. |
| **delimiter** (common) | `,` | `String` | The delimiter char (could be ; , or similar). |
| **ignoreFirstRecord** (common) | `true` | `Boolean` | Whether the first line is ignored for delimited files (for the column headers). Is by default true. |
| **allowShortLines** (common) | `false` | `Boolean` | Allows for lines to be shorter than expected and ignores the extra characters. |
| **ignoreExtraColumns** (common) | `false` | `Boolean` | Allows for lines to be longer than expected and ignores the extra characters. |
| **textQualifier** (advanced) |  | `String` | If the text is qualified with a character. Uses quote character by default. |
| **parserFactory** (advanced) |  | `Object` | References to a custom parser factory to lookup in the registry. |

## Usage

To use the data format, instantiate an instance and invoke the marshal or unmarshal operation in the route builder:

_Java-only: programmatic FlatpackDataFormat configuration and unmarshal_

```java
  FlatpackDataFormat fp = new FlatpackDataFormat();
  fp.setDefinition(new ClassPathResource("INVENTORY-Delimited.pzmap.xml"));
  ...
  from("file:order/in").unmarshal(df).to("seda:queue:neworder");
```

The sample above will read files from the `order/in` folder and unmarshal the input using the Flatpack configuration file `INVENTORY-Delimited.pzmap.xml` that configures the structure of the files. The result is a `DataSetList` object we store on the SEDA queue.

_Java-only: programmatic FlatpackDataFormat configuration and marshal_

```java
FlatpackDataFormat df = new FlatpackDataFormat();
df.setDefinition(new ClassPathResource("PEOPLE-FixedLength.pzmap.xml"));
df.setFixed(true);
df.setIgnoreFirstRecord(false);

from("seda:people").marshal(df).convertBodyTo(String.class).to("jms:queue:people");
```

In the code above we marshal the data from an Object representation as a `List` of rows as `Maps`. The rows as `Map` contains the column name as the key, and the corresponding value. This structure can be created in Java code from e.g., a processor. We marshal the data according to the Flatpack format and convert the result as a `String` object and store it on a JMS queue.

## Dependencies

To use Flatpack in your camel routes, you need to add a dependency on **camel-flatpack** which implements this data format.

If you use maven, you could add the following to your `pom.xml`, substituting the version number for the latest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-flatpack</artifactId>
  <version>x.x.x</version>
</dependency>
```