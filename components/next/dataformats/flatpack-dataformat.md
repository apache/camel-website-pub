# Flatpack

**Since Camel 2.1**

The [Flatpack](../flatpack-component.md) component ships with the Flatpack data format that can be used to format between fixed width or delimited text messages to a `List` of rows as `Map`.

-   marshal = from `List<Map<String, Object>>`, or a single `Map<String, Object>` as one row, to `OutputStream` (can be converted to `String`). Any other body fails with an `InvalidPayloadException`.
    
-   unmarshal = from `java.io.InputStream` (such as a `File` or `String`) to a `java.util.List` as an `org.apache.camel.component.flatpack.DataSetList` instance.  
    The result of the operation will contain all the data. If you need to process each row one by one you can split the exchange, using Splitter.
    

**Notice:** The Flatpack library does currently not support header and trailers for the marshal operation.

## Options

The Flatpack dataformat supports the following options which are listed below.

   
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

## Message Body

The message body at each side of the Flatpack data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `list` or `map` | The rows as a List of Maps, such as the DataSetList unmarshal gives, or a single Map as one row. Other bodies fail. Without a definition, the keys of the first Map name the columns. |
| **Marshal output** | `stream`, as text | The records in the stream cache, or a byte array when stream caching is off. An empty List writes nothing. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as text | 
 |
| **Unmarshal output** | `list` (`org.apache.camel.component.flatpack.DataSetList`) | A DataSetList: a List of the rows, each a HashMap of the column names and the values, which does not keep the column order. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).

## Usage

To use the data format, set it on the marshal or unmarshal step of the route:

-   Java
    
-   YAML
    

```java
FlatpackDataFormat fp = new FlatpackDataFormat();
fp.setDefinition("INVENTORY-Delimited.pzmap.xml");

from("file:order/in").unmarshal(fp).to("seda:neworder");
```

```yaml
- route:
    from:
      uri: file:order/in
      steps:
        - unmarshal:
            flatpack:
              definition: INVENTORY-Delimited.pzmap.xml
        - to:
            uri: seda:neworder
```

The sample above will read files from the `order/in` folder and unmarshal the input using the Flatpack configuration file `INVENTORY-Delimited.pzmap.xml` that configures the structure of the files. The result is a `DataSetList` object we store on the SEDA queue.

-   Java
    
-   YAML
    

```java
FlatpackDataFormat df = new FlatpackDataFormat();
df.setDefinition("PEOPLE-FixedLength.pzmap.xml");
df.setFixed(true);
df.setIgnoreFirstRecord(false);

from("seda:people").marshal(df).convertBodyTo(String.class).to("jms:queue:people");
```

```yaml
- route:
    from:
      uri: seda:people
      steps:
        - marshal:
            flatpack:
              definition: PEOPLE-FixedLength.pzmap.xml
              fixed: true
              ignoreFirstRecord: false
        - convertBodyTo:
            type: java.lang.String
        - to:
            uri: jms:queue:people
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