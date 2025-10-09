# JQ

**Since Camel 3.18**

Camel supports [JQ](https://stedolan.github.io/jq) to allow using [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) on JSON messages.

## JQ Options

The JQ language supports 4 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **headerName** |  | `String` | Name of header to use as input, instead of the message body It has as higher precedent than the propertyName if both are set. |
| **propertyName** |  | `String` | Name of property to use as input, instead of the message body. It has a lower precedent than the headerName if both are set. |
| **resultType** |  | `String` | Sets the class of the result type (type from output). |
| **trim** | `true` | `Boolean` | Whether to trim the value to remove leading and trailing whitespaces and line breaks. |

## Examples

For example, you can use JQ in a [Predicate](../../../manual/predicate.md) with the [Content Based Router](../eips/choice-eip.md) EIP.

```java
from("queue:books.new")
  .choice()
    .when().jq(".store.book.price < 10)")
      .to("jms:queue:book.cheap")
    .when().jq(".store.book.price < 30)")
      .to("jms:queue:book.average")
    .otherwise()
      .to("jms:queue:book.expensive");
```

## Message body types

Camel JQ leverages `camel-jackson` for type conversion. To enable camel-jackson POJO type conversion, refer to the Camel Jackson documentation.

## Using header as input

By default, JQ uses the message body as the input source. However, you can also use a header as input by specifying the `headerName` option.

For example to count the number of books from a JSON document that was stored in a header named `books` you can do:

```java
from("direct:start")
    .setHeader("numberOfBooks")
        .jq(".store.books | length", int.class, "books")
    .to("mock:result");
```

## Camel supplied JQ Functions

The camel-jq adds the following functions:

-   `header` - Allow to access the Message header in a JQ expression.
    

For example, to set the property foo with the value from the Message header \`MyHeader':

```java
from("direct:start")
    .transform()
        .jq(".foo = header(\"MyHeader\")")
    .to("mock:result");
```

## Dependencies

If you use Maven you could just add the following to your `pom.xml`, substituting the version number for the latest and greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jq</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using jq with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jq-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.language.jq.enabled** | Whether to enable auto configuration of the jq language. This is enabled by default. |  | Boolean |
| **camel.language.jq.header-name** | Name of header to use as input, instead of the message body It has as higher precedent than the propertyName if both are set. |  | String |
| **camel.language.jq.property-name** | Name of property to use as input, instead of the message body. It has a lower precedent than the headerName if both are set. |  | String |
| **camel.language.jq.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |