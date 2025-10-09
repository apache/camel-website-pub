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
| **definition** |  | `String` | The flatpack pzmap configuration file. Can be omitted in simpler situations, but its preferred to use the pzmap. |
| **fixed** | `false` | `Boolean` | Delimited or fixed. Is by default false = delimited. |
| **delimiter** | `,` | `String` | The delimiter char (could be ; , or similar). |
| **ignoreFirstRecord** | `true` | `Boolean` | Whether the first line is ignored for delimited files (for the column headers). Is by default true. |
| **allowShortLines** | `false` | `Boolean` | Allows for lines to be shorter than expected and ignores the extra characters. |
| **ignoreExtraColumns** | `false` | `Boolean` | Allows for lines to be longer than expected and ignores the extra characters. |
| **textQualifier** |  | `String` | If the text is qualified with a character. Uses quote character by default. |
| **parserFactoryRef** |  | `String` | References to a custom parser factory to lookup in the registry. |

## Usage

To use the data format, simply instantiate an instance and invoke the marshal or unmarshal operation in the route builder:

```java
  FlatpackDataFormat fp = new FlatpackDataFormat();
  fp.setDefinition(new ClassPathResource("INVENTORY-Delimited.pzmap.xml"));
  ...
  from("file:order/in").unmarshal(df).to("seda:queue:neworder");
```

The sample above will read files from the `order/in` folder and unmarshal the input using the Flatpack configuration file `INVENTORY-Delimited.pzmap.xml` that configures the structure of the files. The result is a `DataSetList` object we store on the SEDA queue.

```java
FlatpackDataFormat df = new FlatpackDataFormat();
df.setDefinition(new ClassPathResource("PEOPLE-FixedLength.pzmap.xml"));
df.setFixed(true);
df.setIgnoreFirstRecord(false);

from("seda:people").marshal(df).convertBodyTo(String.class).to("jms:queue:people");
```

In the code above we marshal the data from a Object representation as a `List` of rows as `Maps`. The rows as `Map` contains the column name as the key, and the corresponding value. This structure can be created in Java code from e.g. a processor. We marshal the data according to the Flatpack format and convert the result as a `String` object and store it on a JMS queue.

## Dependencies

To use Flatpack in your camel routes you need to add the a dependency on **camel-flatpack** which implements this data format.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```java
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-flatpack</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using flatpack with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-flatpack-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.flatpack.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.flatpack.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.flatpack.enabled** | Whether to enable auto configuration of the flatpack component. This is enabled by default. |  | Boolean |
| **camel.component.flatpack.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.dataformat.flatpack.allow-short-lines** | Allows for lines to be shorter than expected and ignores the extra characters. | false | Boolean |
| **camel.dataformat.flatpack.definition** | The flatpack pzmap configuration file. Can be omitted in simpler situations, but its preferred to use the pzmap. |  | String |
| **camel.dataformat.flatpack.delimiter** | The delimiter char (could be ; , or similar). | , | String |
| **camel.dataformat.flatpack.enabled** | Whether to enable auto configuration of the flatpack data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.flatpack.fixed** | Delimited or fixed. Is by default false = delimited. | false | Boolean |
| **camel.dataformat.flatpack.ignore-extra-columns** | Allows for lines to be longer than expected and ignores the extra characters. | false | Boolean |
| **camel.dataformat.flatpack.ignore-first-record** | Whether the first line is ignored for delimited files (for the column headers). Is by default true. | true | Boolean |
| **camel.dataformat.flatpack.parser-factory-ref** | References to a custom parser factory to lookup in the registry. |  | String |
| **camel.dataformat.flatpack.text-qualifier** | If the text is qualified with a character. Uses quote character by default. |  | String |