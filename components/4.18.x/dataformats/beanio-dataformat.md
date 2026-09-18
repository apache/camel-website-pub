# BeanIO

**Since Camel 2.10**

The BeanIO Data Format uses [BeanIO](https://beanio.github.io/) to handle flat payloads (such as XML, CSV, delimited, or fixed length formats).

BeanIO is configured using a mapping XML file where you define the mapping from the flat format to Objects (POJOs). This mapping file is mandatory to use.

## Options

The BeanIO dataformat supports 8 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **mapping** (common) |  | `String` | **Required** The BeanIO mapping file. Is by default loaded from the classpath. You can prefix with file:, http:, or classpath: to denote from where to load the mapping file. |
| **streamName** (common) |  | `String` | **Required** The name of the stream to use. |
| **ignoreUnidentifiedRecords** (common) | `false` | `Boolean` | Whether to ignore unidentified records. |
| **ignoreUnexpectedRecords** (common) | `false` | `Boolean` | Whether to ignore unexpected records. |
| **ignoreInvalidRecords** (common) | `false` | `Boolean` | Whether to ignore invalid records. |
| **encoding** (advanced) |  | `String` | The charset to use. Is by default the JVM platform default charset. |
| **beanReaderErrorHandlerType** (advanced) |  | `String` | To use a custom org.apache.camel.dataformat.beanio.BeanIOErrorHandler as error handler while parsing. Configure the fully qualified class name of the error handler. Notice the options ignoreUnidentifiedRecords, ignoreUnexpectedRecords, and ignoreInvalidRecords may not be in use when you use a custom error handler. |
| **unmarshalSingleObject** (advanced) | `false` | `Boolean` | This options controls whether to unmarshal as a list of objects or as a single object only. The former is the default mode, and the latter is only intended in special use-cases where beanio maps the Camel message to a single POJO bean. |

## Usage

An example of a [mapping file is here](https://github.com/apache/camel/blob/main/components/camel-beanio/src/test/resources/org/apache/camel/dataformat/beanio/mappings.xml).

To use the `BeanIODataFormat` you need to configure the data format with the mapping file, as well the name of the stream.

This can be done as shown below. The streamName is `employeeFile`.

-   Java
    
-   XML
    

```java
DataFormat format = new BeanIODataFormat(
        "org/apache/camel/dataformat/beanio/mappings.xml",
        "employeeFile");

// a route which uses the bean io data format to format the CSV data
// to java objects
from("direct:unmarshal")
        .unmarshal(format)
        // and then split the message body, so we get a message for each row
        .split(body())
        .to("mock:beanio-unmarshal");

// convert a list of java objects back to flat format
from("direct:marshal")
        .marshal(format)
        .to("mock:beanio-marshal");
```

```xml
<route>
    <from uri="direct:unmarshal"/>
    <unmarshal>
        <beanio mapping="org/apache/camel/dataformat/beanio/mappings.xml" streamName="employeeFile"/>
    </unmarshal>
    <split>
        <simple>${body}</simple>
        <to uri="mock:beanio-unmarshal"/>
    </split>
</route>

<route>
    <from uri="direct:marshal"/>
    <marshal>
        <beanio mapping="org/apache/camel/dataformat/beanio/mappings.xml" streamName="employeeFile"/>
    </marshal>
    <to uri="mock:beanio-marshal"/>
</route>
```

To use the BeanIO data format in XML, you need to configure it using the `<beanio>` XML tag as shown below. The routes are similar to the example above.

The first route is for transforming CSV data into a `List<Employee>` Java objects. Which we then split, so the mock endpoint receives a message for each row.

The second route is for the reverse operation, to transform a `List<Employee>` into a stream of CSV data.

The CSV data could, for example, be as below:

```text
Joe,Smith,Developer,75000,10012009
Jane,Doe,Architect,80000,01152008
Jon,Anderson,Manager,85000,03182007
```

## Configuring beanio

The beanio mapper can be configured in `beanio.properties` file which can be loaded in the root classpath (in `src/main/resources` in your source projects). See the [beanio documentation](https://beanio.github.io/docs/reference-guide#80-configuration) for what can be configured.

> **Note**
> This configuration is global for beanio

## Dependencies

To use BeanIO in your Camel routes, you need to add a dependency on **camel-beanio** which implements this data format.

If you use Maven, you can just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-beanio</artifactId>
  <version>4.4.0</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using beanio with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-beanio-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.beanio.bean-reader-error-handler-type** | To use a custom org.apache.camel.dataformat.beanio.BeanIOErrorHandler as error handler while parsing. Configure the fully qualified class name of the error handler. Notice the options ignoreUnidentifiedRecords, ignoreUnexpectedRecords, and ignoreInvalidRecords may not be in use when you use a custom error handler. |  | String |
| **camel.dataformat.beanio.enabled** | Whether to enable auto configuration of the beanio data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.beanio.encoding** | The charset to use. Is by default the JVM platform default charset. |  | String |
| **camel.dataformat.beanio.ignore-invalid-records** | Whether to ignore invalid records. | false | Boolean |
| **camel.dataformat.beanio.ignore-unexpected-records** | Whether to ignore unexpected records. | false | Boolean |
| **camel.dataformat.beanio.ignore-unidentified-records** | Whether to ignore unidentified records. | false | Boolean |
| **camel.dataformat.beanio.mapping** | The BeanIO mapping file. Is by default loaded from the classpath. You can prefix with file:, http:, or classpath: to denote from where to load the mapping file. |  | String |
| **camel.dataformat.beanio.stream-name** | The name of the stream to use. |  | String |
| **camel.dataformat.beanio.unmarshal-single-object** | This options controls whether to unmarshal as a list of objects or as a single object only. The former is the default mode, and the latter is only intended in special use-cases where beanio maps the Camel message to a single POJO bean. | false | Boolean |