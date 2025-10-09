# DataSonnet

**Since Camel 3.7**

Camel supports [DataSonnet](https://datasonnet.com/) transformations to allow an [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) to be used in the [DSL](../../../manual/dsl.md).

For example, you could use DataSonnet to create a Predicate in a [Message Filter](../eips/filter-eip.md) or as an Expression for a [Recipient List](../eips/recipientList-eip.md).

To use a DataSonnet expression, use the following Java code:

```java
datasonnet("someDSExpression");
```

## DataSonnet Options

The DataSonnet language supports 5 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **bodyMediaType** (common) |  | `String` | The String representation of the message’s body MediaType. |
| **outputMediaType** (common) |  | `String` | The String representation of the MediaType to output. |
| **source** (common) |  | `String` | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the value to remove leading and trailing whitespaces and line breaks. |

## Usage

### Setting a result type

The [DataSonnet](#) expression will return a `com.datasonnet.document.Document` by default. The document preserves the content type metadata along with the contents of the transformation result. In predicates, however, the Document will be automatically unwrapped and the boolean content will be returned. Similarly, any time you want the content in a specific result type like a String. To do this, you have to instruct the [DataSonnet](#) which result type to return.

-   Java
    
-   XML
    

```java
datasonnet("body.foo", String.class);
```

```xml
<datasonnet resultType="java.lang.String">body.foo</datasonnet>
```

> **Note**
> In XML DSL you use the `resultType` attribute to provide a fully qualified class name.

If the expression results in an array, or an object, you can instruct the expression to return you `List.class` or `Map.class`, respectively. However, you must also set the output media type to `application/x-java-object`.

> **Note**
> The default `Document` object is useful in situations where there are intermediate transformation steps, and so retaining the content metadata through a route execution is valuable.

### Specifying Media Types

Traditionally, the input and output media types are specified through the [DataSonnet Header](https://datasonnet.s3-us-west-2.amazonaws.com/docs-ci/primary/master/datasonnet/1.0-SNAPSHOT/headers.md). The [DataSonnet](#) expression provides convenience options for specifying the body and output media types without the need for a Header, this is useful if the transformation is a one-liner, for example.

The DataSonnet expression will look for a body media type in the following order:

1.  If the body is a `Document` it will use the metadata in the object
    
2.  If the bodyMediaType parameter was provided in the DSL, it will use its value
    
3.  A `CamelDatasonnetBodyMediaType` exchange property
    
4.  A `Content-Type` message header
    
5.  The DataSonnet Header payload media type directive
    
6.  `application/x-java-object`
    

And for output media type:

1.  If the outputMediaType parameter was provided in the DSL, it will use its value
    
2.  A "CamelDatasonnetOutputMediaType" exchange property
    
3.  A "CamelDatasonnetOutputMediaType" message header
    
4.  The DataSonnet Header output media type directive
    
5.  `application/x-java-object`
    

### Functions

Camel adds the following DataSonnet functions that can be used to access the exchange:

   
| Function | Argument | Type | Description |
| --- | --- | --- | --- |
| cml.properties | key for property | String | To look up a property using the [Properties](../properties-component.md) component (property placeholders). |
| cml.header | the header name | String | Will return the message header. |
| cml.exchangeProperty | key for property | String | Will return the exchange property. |
| cml.variable | the variable name | String | Will return the exchange variable. |

Here’s an example showing some of these functions in use:

-   Java
    
-   XML
    

```java
from("direct:in")
    .setBody(datasonnet("'hello, ' + cml.properties('toGreet')", String.class))
    .to("mock:camel");
```

```xml
<route>
    <from uri="direct:in"/>
    <setBody>
        <datasonnet resultTypeName="java.lang.String">'hello, ' + cml.properties('toGreet')</datasonnet>
    </setBody>
    <to uri="mock:camel"/>
</route>
```

### Loading script from external resource

You can externalize the script and have Apache Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`.  
This is done using the following syntax: `"resource:scheme:location"`, e.g., to refer to a file on the classpath you can do:

```java
.setHeader("myHeader").datasonnet("resource:classpath:mydatasonnet.ds");
```

## Examples

Here is a simple example using a DataSonnet expression as a predicate in a Message Filter:

-   Java
    
-   XML
    

```java
// let's route if a line item is over $100
from("queue:foo")
    .filter(datasonnet("ds.arrays.firstWith(body.lineItems, function(item) item > 100) != null"))
    .to("queue:bar");
```

```xml
<route>
    <from uri="queue:foo"/>
    <filter>
        <datasonnet>ds.arrays.firstWith(body.lineItems, function(item) item > 100) != null</datasonnet>
        <to uri="queue:bar"/>
    </filter>
</route>
```

Here is an example of a simple DataSonnet expression as a transformation EIP. This example will transform an XML body with `lineItems` into JSON while filtering out lines that are under 100.

-   Java
    
-   XML
    

```java
from("queue:foo")
    .transform(datasonnet("ds.filter(body.lineItems, function(item) item > 100)", String.class, "application/xml", "application/json"))
    .to("queue:bar");
```

```xml
<route>
    <from uri="queue:foo"/>
    <filter>
        <datasonnet bodyMediaType="application/xml" outputMediaType="application/json" resultTypeName="java.lang.String" >
            ds.filter(body.lineItems, function(item) item > 100)
        </datasonnet>
        <to uri="queue:bar"/>
    </filter>
</route>
```

## Dependencies

To use scripting languages in your camel routes, you need to add a dependency on **camel-datasonnet**.

If you use Maven you could just add the following to your `pom.xml`, substituting the version number for the latest and greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-datasonnet</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using datasonnet with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-datasonnet-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.language.datasonnet.body-media-type** | The String representation of the message’s body MediaType. |  | String |
| **camel.language.datasonnet.enabled** | Whether to enable auto configuration of the datasonnet language. This is enabled by default. |  | Boolean |
| **camel.language.datasonnet.output-media-type** | The String representation of the MediaType to output. |  | String |
| **camel.language.datasonnet.source** | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| **camel.language.datasonnet.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |