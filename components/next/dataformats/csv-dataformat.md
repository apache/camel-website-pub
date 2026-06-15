# CSV

**Since Camel 1.3**

The CSV Data Format uses [Apache Commons CSV](http://commons.apache.org/proper/commons-csv/) to handle CSV payloads (Comma Separated Values) such as those exported/imported by Excel.

## Options

The CSV dataformat supports 28 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **format** (common) | `DEFAULT` | `Enum` | 
The format to use.

Enum values:

-   DEFAULT
    
-   EXCEL
    
-   INFORMIX\_UNLOAD
    
-   INFORMIX\_UNLOAD\_CSV
    
-   MONGODB\_CSV
    
-   MONGODB\_TSV
    
-   MYSQL
    
-   ORACLE
    
-   POSTGRESQL\_CSV
    
-   POSTGRESQL\_TEXT
    
-   RFC4180
    





 |
| **commentMarkerDisabled** (advanced) | `false` | `Boolean` | Disables the comment marker of the reference format. |
| **commentMarker** (advanced) |  | `String` | Sets the comment marker of the reference format. |
| **delimiter** (common) |  | `String` | Sets the delimiter to use. The default value is , (comma). |
| **escapeDisabled** (advanced) | `false` | `Boolean` | Use for disabling using escape character. |
| **escape** (advanced) |  | `String` | Sets the escape character to use. |
| **headerDisabled** (common) | `false` | `Boolean` | Use for disabling headers. |
| **header** (common) |  | `String` | To configure the CSV headers. Multiple headers can be separated by comma. |
| **allowMissingColumnNames** (common) | `false` | `Boolean` | Whether to allow missing column names. |
| **ignoreEmptyLines** (common) | `false` | `Boolean` | Whether to ignore empty lines. |
| **ignoreSurroundingSpaces** (common) | `false` | `Boolean` | Whether to ignore surrounding spaces. |
| **nullStringDisabled** (advanced) | `false` | `Boolean` | Used to disable null strings. |
| **nullString** (advanced) |  | `String` | Sets the null string. |
| **quoteDisabled** (common) | `false` | `Boolean` | Used to disable quotes. |
| **quote** (common) |  | `String` | Sets the quote to use which by default is double-quote character. |
| **recordSeparatorDisabled** (common) |  | `String` | Used for disabling record separator. |
| **recordSeparator** (common) |  | `String` | Sets the record separator (aka new line) which by default is new line characters (CRLF). |
| **skipHeaderRecord** (common) | `false` | `Boolean` | Whether to skip the header record in the output. |
| **quoteMode** (common) |  | `Enum` | 

Sets the quote mode.

Enum values:

-   ALL
    
-   ALL\_NON\_NULL
    
-   MINIMAL
    
-   NON\_NUMERIC
    
-   NONE
    





 |
| **ignoreHeaderCase** (common) | `false` | `Boolean` | Sets whether or not to ignore case when accessing header names. |
| **trim** (common) | `false` | `Boolean` | Sets whether or not to trim leading and trailing blanks. |
| **trailingDelimiter** (common) | `false` | `Boolean` | Sets whether or not to add a trailing delimiter. |
| **marshallerFactoryRef** (advanced) |  | `String` | Sets the implementation of the CsvMarshallerFactory interface which is able to customize marshalling/unmarshalling behavior by extending CsvMarshaller or creating it from scratch. |
| **lazyLoad** (advanced) | `false` | `Boolean` | Whether the unmarshalling should produce an iterator that reads the lines on the fly or if all the lines must be read at one. |
| **useMaps** (common) | `false` | `Boolean` | Whether the unmarshalling should produce maps (HashMap)for the lines values instead of lists. It requires to have header (either defined or collected). |
| **useOrderedMaps** (common) | `false` | `Boolean` | Whether the unmarshalling should produce ordered maps (LinkedHashMap) for the lines values instead of lists. It requires to have header (either defined or collected). |
| **recordConverterRef** (advanced) |  | `String` | Refers to a custom CsvRecordConverter to lookup from the registry to use. |
| **captureHeaderRecord** (advanced) | `false` | `Boolean` | Whether the unmarshalling should capture the header record and store it in the message header. |

## Message Headers

The following headers are supported by this component:

### Producer only

 
| Header | Description |
| --- | --- |
| `CamelCsvHeaderRecord` | The header record collected from the CSV when setCaptureHeaderRecord is true. |

## Examples

### Marshalling a Map to CSV

The component allows you to marshal a Java Map (or any other message type that can be converted in a Map) into a CSV payload.

Considering the following body:

```java
Map<String, Object> body = new LinkedHashMap<>();
body.put("foo", "abc");
body.put("bar", 123);
```

and this route definition:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .marshal().csv()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:start" />
    <marshal>
        <csv />
    </marshal>
    <to uri="mock:result" />
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            csv: {}
        - to:
            uri: mock:result
```

then it will produce

abc,123

### Unmarshalling a CSV message into a Java List

Unmarshalling will transform a CSV message into a Java List with CSV file lines (containing another List with all the field values).

An example: we have a CSV file with names of persons, their IQ and their current activity.

```text
Jack Dalton, 115, mad at Averell
Joe Dalton, 105, calming Joe
William Dalton, 105, keeping Joe from killing Averell
Averell Dalton, 80, playing with Rantanplan
Lucky Luke, 120, capturing the Daltons
```

We can now use the CSV component to unmarshal this file:

```java
from("file:src/test/resources/?fileName=daltons.csv&noop=true")
    .unmarshal().csv()
    .to("mock:daltons");
```

The resulting message will contain a `List<List<String>>` like…​

```java
List<List<String>> data = (List<List<String>>) exchange.getIn().getBody();
for (List<String> line : data) {
    LOG.debug(String.format("%s has an IQ of %s and is currently %s", line.get(0), line.get(1), line.get(2)));
}
```

### Marshalling a List<Map> to CSV

**Since Camel 2.1**

If you have multiple rows of data you want to be marshalled into CSV format, you can now store the message payload as a `List<Map<String, Object>>` object where the list contains a Map for each row.

### File Poller of CSV, then unmarshaling

Given a bean which can handle the incoming data…​

**MyCsvHandler.java**

```java
// Some comments here
public void doHandleCsvData(List<List<String>> csvData)
{
    // do magic here
}
```

1.  your route then looks as follows
    

```xml
<route>
        <!-- poll every 10 seconds -->
        <from uri="file:///some/path/to/pickup/csvfiles?delete=true&amp;delay=10000" />
        <unmarshal><csv /></unmarshal>
        <to uri="bean:myCsvHandler?method=doHandleCsvData" />
</route>
```

### Marshaling with a pipe as delimiter

Considering the following body:

```java
Map<String, Object> body = new LinkedHashMap<>();
body.put("foo", "abc");
body.put("bar", 123);
```

And this Java route definition:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .marshal(new CsvDataFormat().setDelimiter(&#39;|&#39;))
    .to("mock:result")
```

```xml
<route>
  <from uri="direct:start" />
  <marshal>
    <csv delimiter="|" />
  </marshal>
  <to uri="mock:result" />
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            csv:
              delimiter: "|"
        - to:
            uri: mock:result
```

Then it will produce:

abc|123

Using autogenColumns, configRef and strategyRef attributes inside XML == DSL

**Since Camel 2.9.2 / 2.10 and deleted for Camel 2.15**

You can customize the CSV Data Format to make use of your own `CSVConfig` and/or `CSVStrategy`. Also note that the default value of the `autogenColumns` option is true. The following example should illustrate this customization.

```xml
<route>
  <from uri="direct:start" />
  <marshal>
    <!-- make use of a strategy other than the default one which is 'org.apache.commons.csv.CSVStrategy.DEFAULT_STRATEGY' -->
    <csv autogenColumns="false" delimiter="|" configRef="csvConfig" strategyRef="excelStrategy" />
  </marshal>
  <convertBodyTo type="java.lang.String" />
  <to uri="mock:result" />
</route>

<bean id="csvConfig" class="org.apache.commons.csv.writer.CSVConfig">
  <property name="fields">
    <list>
      <bean class="org.apache.commons.csv.writer.CSVField">
        <property name="name" value="orderId" />
      </bean>
      <bean class="org.apache.commons.csv.writer.CSVField">
        <property name="name" value="amount" />
      </bean>
    </list>
  </property>
</bean>

<bean id="excelStrategy" class="org.springframework.beans.factory.config.FieldRetrievingFactoryBean">
  <property name="staticField" value="org.apache.commons.csv.CSVStrategy.EXCEL_STRATEGY" />
</bean>
```

### Collecting header record

You can instruct the CSV Data Format to collect the headers into a message header called CamelCsvHeaderRecord.

```java
CsvDataFormat csv = new CsvDataFormat();
csv.setCaptureHeaderRecord(true);

from("direct:start")
  .unmarshal(csv)
  .log("${header[CamelCsvHeaderRecord]}");
```

### Using skipFirstLine or skipHeaderRecord option while unmarshaling

\*For Camel >= 2.16.5 The instruction for CSV Data format to skip headers or first line is the following. Usign the Spring/XML DSL:

```xml
<route>
  <from uri="direct:start" />
  <unmarshal>
    <csv skipHeaderRecord="true" />
  </unmarshal>
  <to uri="bean:myCsvHandler?method=doHandleCsv" />
</route>
```

**Since Camel 2.10 and deleted for Camel 2.15**

You can instruct the CSV Data Format to skip the first line which contains the CSV headers. Using the Spring/XML DSL:

-   Java
    
-   XML
    
-   YAML
    

```java
CsvDataFormat csv = new CsvDataFormat();
csv.setSkipFirstLine(true);

from("direct:start")
  .unmarshal(csv)
.to("bean:myCsvHandler?method=doHandleCsv");
```

```xml
<route>
  <from uri="direct:start" />
  <unmarshal>
    <csv skipFirstLine="true" />
  </unmarshal>
  <to uri="bean:myCsvHandler?method=doHandleCsv" />
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - unmarshal:
            csv:
              skipFirstLine: true
        - to:
            uri: bean:myCsvHandler
            parameters:
              method: doHandleCsv
```

### Unmarshaling with a pipe as delimiter

-   Java
    
-   XML
    
-   YAML
    

```java
CsvDataFormat csv = new CsvDataFormat();
CSVStrategy strategy = CSVStrategy.DEFAULT_STRATEGY;
strategy.setDelimiter('|');
csv.setStrategy(strategy);

from("direct:start")
  .unmarshal(csv)
  .to("bean:myCsvHandler?method=doHandleCsv");
```

Or, possibly:

```java
CsvDataFormat csv = new CsvDataFormat();
csv.setDelimiter("|");

from("direct:start")
  .unmarshal(csv)
  .to("bean:myCsvHandler?method=doHandleCsv");
```

```xml
<route>
  <from uri="direct:start" />
  <unmarshal>
    <csv delimiter="|" />
  </unmarshal>
  <to uri="bean:myCsvHandler?method=doHandleCsv" />
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - unmarshal:
            csv:
              delimiter: "|"
        - to:
            uri: bean:myCsvHandler
            parameters:
              method: doHandleCsv
```

**Issue in CSVConfig**

It looks like that

```java
CSVConfig csvConfig = new CSVConfig();
csvConfig.setDelimiter(';');
```

This doesn’t work. You have to set the delimiter as a String!

## Dependencies

To use CSV in your Camel routes, you need to add a dependency on **camel-csv**, which implements this data format.

If you use Maven, you can add the following to your pom.xml, substituting the version number for the latest and greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-csv</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using csv with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-csv-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 29 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.csv.allow-missing-column-names** | Whether to allow missing column names. | false | Boolean |
| **camel.dataformat.csv.capture-header-record** | Whether the unmarshalling should capture the header record and store it in the message header. | false | Boolean |
| **camel.dataformat.csv.comment-marker** | Sets the comment marker of the reference format. |  | String |
| **camel.dataformat.csv.comment-marker-disabled** | Disables the comment marker of the reference format. | false | Boolean |
| **camel.dataformat.csv.delimiter** | Sets the delimiter to use. The default value is , (comma). |  | String |
| **camel.dataformat.csv.enabled** | Whether to enable auto configuration of the csv data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.csv.escape** | Sets the escape character to use. |  | String |
| **camel.dataformat.csv.escape-disabled** | Use for disabling using escape character. | false | Boolean |
| **camel.dataformat.csv.format** | The format to use. | DEFAULT | String |
| **camel.dataformat.csv.header** | To configure the CSV headers. Multiple headers can be separated by comma. |  | String |
| **camel.dataformat.csv.header-disabled** | Use for disabling headers. | false | Boolean |
| **camel.dataformat.csv.ignore-empty-lines** | Whether to ignore empty lines. | false | Boolean |
| **camel.dataformat.csv.ignore-header-case** | Sets whether or not to ignore case when accessing header names. | false | Boolean |
| **camel.dataformat.csv.ignore-surrounding-spaces** | Whether to ignore surrounding spaces. | false | Boolean |
| **camel.dataformat.csv.lazy-load** | Whether the unmarshalling should produce an iterator that reads the lines on the fly or if all the lines must be read at one. | false | Boolean |
| **camel.dataformat.csv.marshaller-factory-ref** | Sets the implementation of the CsvMarshallerFactory interface which is able to customize marshalling/unmarshalling behavior by extending CsvMarshaller or creating it from scratch. |  | String |
| **camel.dataformat.csv.null-string** | Sets the null string. |  | String |
| **camel.dataformat.csv.null-string-disabled** | Used to disable null strings. | false | Boolean |
| **camel.dataformat.csv.quote** | Sets the quote to use which by default is double-quote character. |  | String |
| **camel.dataformat.csv.quote-disabled** | Used to disable quotes. | false | Boolean |
| **camel.dataformat.csv.quote-mode** | Sets the quote mode. |  | String |
| **camel.dataformat.csv.record-converter-ref** | Refers to a custom CsvRecordConverter to lookup from the registry to use. |  | String |
| **camel.dataformat.csv.record-separator** | Sets the record separator (aka new line) which by default is new line characters (CRLF). |  | String |
| **camel.dataformat.csv.record-separator-disabled** | Used for disabling record separator. |  | String |
| **camel.dataformat.csv.skip-header-record** | Whether to skip the header record in the output. | false | Boolean |
| **camel.dataformat.csv.trailing-delimiter** | Sets whether or not to add a trailing delimiter. | false | Boolean |
| **camel.dataformat.csv.trim** | Sets whether or not to trim leading and trailing blanks. | false | Boolean |
| **camel.dataformat.csv.use-maps** | Whether the unmarshalling should produce maps (HashMap)for the lines values instead of lists. It requires to have header (either defined or collected). | false | Boolean |
| **camel.dataformat.csv.use-ordered-maps** | Whether the unmarshalling should produce ordered maps (LinkedHashMap) for the lines values instead of lists. It requires to have header (either defined or collected). | false | Boolean |