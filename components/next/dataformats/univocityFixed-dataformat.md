# uniVocity Fixed Length

**Since Camel 2.15**

This [Data Format](../../../manual/data-format.md) uses [uniVocity-parsers](https://www.univocity.com/pages/univocity_parsers_tutorial.md) for reading and writing three kinds of tabular data text files:

-   CSV (Comma Separated Values), where the values are separated by a symbol (usually a comma)
    
-   fixed-width, where the values have known sizes
    
-   TSV (Tabular Separated Values), where the fields are separated by a tabulation
    

Thus, there are three data formats based on uniVocity-parsers.

If you use Maven, you can add the following to your `pom.xml`, substituting the version number for the latest release.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-univocity-parsers</artifactId>
    <version>x.x.x</version>
</dependency>
```

## Options

Most configuration options of the uniVocity-parsers are available in the data formats. If you want more information about a particular option, please refer to their [documentation page](https://www.univocity.com/pages/univocity_parsers_tutorial#settings).

The three data formats share common options and have dedicated ones, this section presents them all.

## Options

The uniVocity Fixed Length dataformat supports 16 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **padding** (common) |  | `String` | The padding character. The default value is a space. |
| **skipTrailingCharsUntilNewline** (common) | `false` | `Boolean` | Whether or not the trailing characters until new line must be ignored. The default value is false. |
| **recordEndsOnNewline** (common) | `false` | `Boolean` | Whether or not the record ends on new line. The default value is false. |
| **nullValue** (advanced) |  | `String` | The string representation of a null value. The default value is null. |
| **skipEmptyLines** (common) | `true` | `Boolean` | Whether or not the empty lines must be ignored. The default value is true. |
| **ignoreTrailingWhitespaces** (common) | `true` | `Boolean` | Whether or not the trailing white spaces must be ignored. The default value is true. |
| **ignoreLeadingWhitespaces** (common) | `true` | `Boolean` | Whether or not the leading white spaces must be ignored. The default value is true. |
| **headersDisabled** (common) | `false` | `Boolean` | Whether or not the headers are disabled. When defined, this option explicitly sets the headers as null which indicates that there is no header. The default value is false. |
| **headerExtractionEnabled** (common) | `false` | `Boolean` | Whether or not the header must be read in the first line of the test document. The default value is false. |
| **numberOfRecordsToRead** (advanced) |  | `Integer` | The maximum number of record to read. |
| **emptyValue** (advanced) |  | `String` | The String representation of an empty value. |
| **lineSeparator** (advanced) |  | `String` | The line separator of the files. The default value is to use the JVM platform line separator. |
| **normalizedLineSeparator** (advanced) |  | `String` | The normalized line separator of the files. The default value is a new line character. |
| **comment** (advanced) | `#` | `String` | The comment symbol. The default value is #. |
| **lazyLoad** (common) | `false` | `Boolean` | Whether the unmarshalling should produce an iterator that reads the lines on the fly or if all the lines must be read at once. The default value is false. |
| **asMap** (common) | `false` | `Boolean` | Whether the unmarshalling should produce maps for the lines values instead of lists. It requires to have header (either defined or collected). The default value is false. |

## Marshalling usages

The marshalling accepts either:

-   A list of maps (`List<Map<String, ?>>`), one for each line
    
-   A single map (`Map<String, ?>`), for a single line
    

Any other body will throws an exception.

### Usage example: marshalling a Map into CSV format

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:input")
    .marshal().univocityCsv()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:input"/>
    <marshal>
        <univocity-csv/>
    </marshal>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:input
      steps:
        - marshal:
            univocityCsv: {}
        - to:
            uri: mock:result
```

### Usage example: marshalling a Map into fixed-width format

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:input")
    .marshal().univocityFixed()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:input"/>
    <marshal>
        <univocity-fixed padding="_">
            <univocity-header length="5"/>
            <univocity-header length="5"/>
            <univocity-header length="5"/>
        </univocity-fixed>
    </marshal>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:input
      steps:
        - marshal:
            univocityFixed:
              padding: "_"
        - to:
            uri: mock:result
```

### Usage example: marshalling a Map into TSV format

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:input")
    .marshal().univocityTsv()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:input"/>
    <marshal>
        <univocity-tsv/>
    </marshal>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:input
      steps:
        - marshal:
            univocityTsv: {}
        - to:
            uri: mock:result
```

## Unmarshalling usages

The unmarshalling uses an `InputStream` in order to read the data.

Each row produces either:

-   a list with all the values in it (`asMap` option with `false`);
    
-   A map with all the values indexed by the headers (`asMap` option with `true`).
    

All the rows can either:

-   be collected at once into a list (`lazyLoad` option with `false`);
    
-   be read on the fly using an iterator (`lazyLoad` option with `true`).
    

### Usage example: unmarshalling a CSV format into maps with automatic headers

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:input")
    .unmarshal().univocityCsv()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:input"/>
    <unmarshal>
        <univocity-csv headerExtractionEnabled="true" asMap="true"/>
    </unmarshal>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:input
      steps:
        - unmarshal:
            univocityCsv:
              headerExtractionEnabled: true
              asMap: true
        - to:
            uri: mock:result
```

### Usage example: unmarshalling a fixed-width format into lists

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:input")
    .unmarshal().univocityFixed()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:input"/>
    <unmarshal>
        <univocity-fixed>
            <univocity-header length="5"/>
            <univocity-header length="5"/>
            <univocity-header length="5"/>
        </univocity-fixed>
    </unmarshal>
    <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:input
      steps:
        - unmarshal:
            univocityFixed: {}
        - to:
            uri: mock:result
```