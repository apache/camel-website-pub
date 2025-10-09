# JQ

**Since Camel 3.18**

Camel supports [JQ](https://jqlang.github.io/jq/) to allow using [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) on JSON messages.

## JQ Options

The JQ language supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **source** (common) |  | `String` | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. |

## Usage

### Message body types

Camel JQ leverages `camel-jackson` for type conversion. To enable camel-jackson POJO type conversion, refer to the Camel Jackson documentation.

### Using header as input

By default, JQ uses the message body as the input source. However, you can also use a header as input by specifying the `headerName` option.

For example, to count the number of books from a JSON document that was stored in a header named `books` you can do:

```java
from("direct:start")
    .setHeader("numberOfBooks")
        .jq(".store.books | length", int.class, "books")
    .to("mock:result");
```

### Camel supplied JQ Functions

> **Note**
> JQ comes with about a hundred built-in functions, and you can see many examples from [JQ](https://jqlang.github.io/jq/) documentation.

The camel-jq adds the following functions:

-   `header`: allow accessing the Message header in a JQ expression.
    
-   `property`: allow accessing the Exchange property in a JQ expression.
    
-   `constant`: allow using a constant value as-is in a JQ expression.
    
-   `variable`: allow accessing the Exchange variable in a JQ expression.
    
-   `body`: the message body as a textual value.
    

For example, to set the property foo with the value from the Message header \`MyHeader':

```java
from("direct:start")
    .transform()
        .jq(".foo = header(\"MyHeader\")")
    .to("mock:result");
```

Or from the exchange property:

```java
from("direct:start")
    .transform()
        .jq(".foo = property(\"MyProperty\")")
    .to("mock:result");
```

And using a constant value

```java
from("direct:start")
    .transform()
        .jq(".foo = constant(\"Hello World\")")
    .to("mock:result");
```

Or using an exchange variable:

```java
from("direct:start")
    .transform()
        .jq(".foo = variable(\"MyVar\")")
    .to("mock:result");
```

The `header`, `property` and `variable` functions also support returning a default value in case the key does not exist, as shown in the following:

```java
from("direct:start")
    .transform()
        .jq(".foo = header(\"MyHeader\", \"MyDefaultValue\")")
    .to("mock:result");
```

### Transforming a JSon message

For basic JSon transformation where you have a fixed structure, you can represent with a combination of using Camel simple and JQ language as:

{
  "company": "${jq(.customer.name)}",
  "location": "${jq(.customer.address.country)}",
  "gold": ${jq(.customer.orders\[\] | length > 5)}
}

Here we use the simple language to define the structure and use JQ as inlined functions via the `${jq(exp)}` syntax.

This makes it possible to use simple as a template language to define a basic structure and then JQ to grab the data from an incoming JSon message. The output of the transformation is also JSon, but with simple you could also make it XML or plain text based:

```xml
<customer gold="${jq(.customer.orders[] | length > 5)}">
    <company>${jq(.customer.name)}</company>
    <location>${jq(.customer.address.country)}</location>
</customer>
```

## Examples

For example, you can use JQ in a [Predicate](../../../manual/predicate.md) with the [Content-Based Router](../eips/choice-eip.md) EIP.

```java
from("queue:books.new")
  .choice()
    .when().jq(".store.book.price < 10")
      .to("jms:queue:book.cheap")
    .when().jq(".store.book.price < 30")
      .to("jms:queue:book.average")
    .otherwise()
      .to("jms:queue:book.expensive");
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

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.language.jq.enabled** | Whether to enable auto configuration of the jq language. This is enabled by default. |  | Boolean |
| **camel.language.jq.source** | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| **camel.language.jq.trim** | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. | true | Boolean |