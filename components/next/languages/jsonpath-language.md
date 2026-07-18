# JSONPath

**Since Camel 2.13**

Camel supports [JSONPath](https://github.com/json-path/JsonPath/) to allow using [Expression](../../../manual/expression.md) or [Predicate](../../../manual/predicate.md) on JSON messages.

## JSONPath Options

The JSONPath language supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **suppressExceptions** (common) | `false` | `Boolean` | Whether to suppress exceptions such as PathNotFoundException. |
| **allowSimple** (advanced) | `true` | `Boolean` | Whether to allow in inlined Simple exceptions in the JSONPath expression. |
| **allowEasyPredicate** (advanced) | `true` | `Boolean` | Whether to allow using the easy predicate parser to pre-parse predicates. |
| **writeAsString** (common) | `false` | `Boolean` | Whether to write the output of each row/element as a JSON String value instead of a Map/POJO value. |
| **unpackArray** (common) | `false` | `Boolean` | Whether to unpack a single element json-array into an object. |
| **option** (advanced) |  | `Enum` | 
To configure additional options on JSONPath. Multiple values can be separated by comma.

Enum values:

-   DEFAULT\_PATH\_LEAF\_TO\_NULL
    
-   ALWAYS\_RETURN\_LIST
    
-   AS\_PATH\_LIST
    
-   SUPPRESS\_EXCEPTIONS
    
-   REQUIRE\_PROPERTIES
    





 |
| **source** (common) |  | `String` | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |
| **resultType** (common) |  | `String` | The class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. |

## Usage

### JSONPath Syntax

Using the JSONPath syntax takes some time to learn, even for basic predicates. So for example, to find out all the cheap books you have to do:

```text
$.store.book[?(@.price < 20)]
```

### Easy JSONPath Syntax

However, what if you could just write it as:

```text
store.book.price < 20
```

And you can omit the path if you just want to look at nodes with a price key:

```text
price < 20
```

To support this there is a `EasyPredicateParser` which kicks-in if you have defined the predicate using a basic style. That means the predicate must not start with the `$` sign, and only include one operator.

The easy syntax is:

```text
left OP right
```

You can use Camel simple language in the right operator, eg:

```text
store.book.price < ${header.limit}
```

See the [JSONPath](https://github.com/json-path/JsonPath) project page for more syntax examples.

## Examples

For example, you can use JSONPath in a [Predicate](../../../manual/predicate.md) with the [Content-Based Router](../eips/choice-eip.md) EIP.

-   Java
    
-   XML DSL
    

```java
from("queue:books.new")
  .choice()
    .when().jsonpath("$.store.book[?(@.price < 10)]")
      .to("jms:queue:book.cheap")
    .when().jsonpath("$.store.book[?(@.price < 30)]")
      .to("jms:queue:book.average")
    .otherwise()
      .to("jms:queue:book.expensive");
```

```xml
<route>
  <from uri="direct:start"/>
  <choice>
    <when>
      <jsonpath>$.store.book[?(@.price &lt; 10)]</jsonpath>
      <to uri="mock:cheap"/>
    </when>
    <when>
      <jsonpath>$.store.book[?(@.price &lt; 30)]</jsonpath>
      <to uri="mock:average"/>
    </when>
    <otherwise>
      <to uri="mock:expensive"/>
    </otherwise>
  </choice>
</route>
```

### Supported message body types

Camel JSONPath supports message body using the following types:

 
| Type | Comment |
| --- | --- |
| `File` | Reading from files |
| `String` | Plain strings |
| `Map` | Message bodies as `java.util.Map` types |
| `List` | Message bodies as `java.util.List` types |
| `POJO` | **Optional** If Jackson is on the classpath, then camel-jsonpath is able to use Jackson to read the message body as POJO and convert to `java.util.Map` which is supported by JSONPath. For example, you can add `camel-jackson` as dependency to include Jackson. |
| `InputStream` | If none of the above types matches, then Camel will attempt to read the message body as a `java.io.InputStream`. |

If a message body is of unsupported type, then an exception is thrown by default. However, you can configure JSONPath to suppress exceptions (see below)

### Suppressing exceptions

By default, jsonpath will throw an exception if the json payload does not have a valid path accordingly to the configured jsonpath expression. In some use-cases, you may want to ignore this in case the json payload contains optional data. Therefore, you can set the option `suppressExceptions` to `true` to ignore this as shown:

-   Java
    
-   XML DSL
    

```java
from("direct:start")
    .choice()
        // use true to suppress exceptions
        .when().jsonpath("person.middlename", true)
            .to("mock:middle")
        .otherwise()
            .to("mock:other");
```

```xml
<route>
  <from uri="direct:start"/>
  <choice>
    <when>
      <jsonpath suppressExceptions="true">person.middlename</jsonpath>
      <to uri="mock:middle"/>
    </when>
    <otherwise>
      <to uri="mock:other"/>
    </otherwise>
  </choice>
</route>
```

This option is also available on the `@JsonPath` annotation.

### Inline Simple expressions

It’s possible to inlined [Simple](simple-language.md) language in the JSONPath expression using the simple syntax `${xxx}`.

An example is shown below:

-   Java
    
-   XML DSL
    

```java
from("direct:start")
  .choice()
    .when().jsonpath("$.store.book[?(@.price < ${header.cheap})]")
      .to("mock:cheap")
    .when().jsonpath("$.store.book[?(@.price < ${header.average})]")
      .to("mock:average")
    .otherwise()
      .to("mock:expensive");
```

```xml
<route>
  <from uri="direct:start"/>
  <choice>
    <when>
      <jsonpath>$.store.book[?(@.price &lt; ${header.cheap})]</jsonpath>
      <to uri="mock:cheap"/>
    </when>
    <when>
      <jsonpath>$.store.book[?(@.price &lt; ${header.average})]</jsonpath>
      <to uri="mock:average"/>
    </when>
    <otherwise>
      <to uri="mock:expensive"/>
    </otherwise>
  </choice>
</route>
```

You can turn off support for inlined Simple expression by setting the option `allowSimple` to `false` as shown:

-   Java
    
-   XML DSL
    

```java
.when().jsonpath("$.store.book[?(@.price < 10)]", false, false)
```

```xml
<jsonpath allowSimple="false">$.store.book[?(@.price &lt; 10)]</jsonpath>
```

### Using variables as source

By default, the message body is the source for the jsonpath evaluation. However, if you need to refer to a variable or message header instead as the body, then this is easy as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setVariable("cars", constant("[\"Ford\", \"BMW\", \"Fiat\"]"))
    .setBody(simple("${jsonpath(variable:cars , $.length())}"))
    .to("mock:cars");
```

```xml
<route>
  <from uri="direct:start"/>
  <setVariable name="cars">
    <constant>["Ford", "BMW", "Fiat"]</constant>
  </setVariable>
  <setBody>
    <simple>${jsonpath(variable:cars , $.length())}</simple>
  </setBody>
  <to uri="mock:cars"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setVariable:
            name: cars
            constant: '["Ford", "BMW", "Fiat"]'
        - setBody:
            simple: "${jsonpath(variable:cars , $.length())}"
        - to:
            uri: mock:cars
```

Here we set a variable named _cars_ with a json array of 3 cars. Then we want to count the length of the array using jsonpath length function. Notice how we use the inlined simple language, and can easily refer to the variable as the source using `variable:cars`.

### JSONPath injection

You can use [Bean Integration](../../../manual/bean-integration.md) to invoke a method on a bean and use various languages such as JSONPath (via the `@JsonPath` annotation) to extract a value from the message and bind it to a method parameter, as shown below:

_Java-only: Java annotation bean integration_

```java
public class Foo {

    @Consume("activemq:queue:books.new")
    public void doSomething(@JsonPath("$.store.book[*].author") String author, @Body String json) {
      // process the inbound message here
    }
}
```

### Encoding Detection

The encoding of the JSON document is detected automatically, if the document is encoded in unicode (UTF-8, UTF-16LE, UTF-16BE, UTF-32LE, UTF-32BE) as specified in RFC-4627. If the encoding is a non-unicode encoding, you can either make sure that you enter the document in String format to JSONPath, or you can specify the encoding in the header `CamelJsonPathJsonEncoding`.

### Split JSON data into sub rows as JSON

You can use JSONPath to split a JSON document, such as:

_Java-only: Java DSL with class literal parameter_

```java
from("direct:start")
    .split().jsonpath("$.store.book[*]", List.class)
    .to("log:book");
```

> **Important**
> Notice how we specify `List.class` as the result-type. This is because if there is only a single element (only 1 book), then jsonpath will return the single entity as a `Map` instead of `List<Map>`. Therefore, we tell Camel that the result should always be a `List`, and Camel will then automatic wrap the single element into a new `List` object.

Then each book is logged, however the message body is a `Map` instance. Sometimes you may want to output this as plain String JSON value instead, which can be done with the `writeAsString` option as shown:

_Java-only: Java DSL with class literal parameter_

```java
from("direct:start")
    .split().jsonpathWriteAsString("$.store.book[*]", List.class)
    .to("log:book");
```

Then each book is logged as a String JSON value.

### Unpack a single-element array into an object

It is possible to unpack a single-element array into an object:

_Java-only: Java DSL with class literal parameter_

```java
from("direct:start")
    .setBody().jsonpathUnpack("$.store.book", Book.class)
    .to("log:book");
```

If a book array contains only one book, it will be converted into a Book object.

### Using header as input

By default, JSONPath uses the message body as the input source. However, you can also use a header as input by specifying the `source` option.

For example, to count the number of books from a JSON document that was stored in a header named `books` you can do:

_Java-only: Java fluent expression builder API_

```java
var jp = expression().jsonpath("$..store.book.length()").resultType(int.class)
        .source("header:books").end();

from("direct:start")
    .setHeader("numberOfBooks", jp)
    .to("mock:result");
```

And you can also inline the expression:

_Java-only: Java fluent expression builder API_

```java
from("direct:start")
    .setHeader("numberOfBooks", expression().jsonpath("$..store.book.length()").resultType(int.class)
            .source("header:books").end())
    .to("mock:result");
```

In the `jsonpath` expression above we specify the name of the header as `books`, and we also told that we wanted the result to be converted as an integer by `int.class`.

> **Tip**
> You can also use `variable:` as source prefix to refer to an Exchange variable instead of a header.

The same example in XML DSL would be easier to do:

_XML-only:_

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="numberOfBooks">
    <jsonpath source="header:books" resultType="int">$..store.book.length()</jsonpath>
  </setHeader>
  <to uri="mock:result"/>
</route>
```

### Transforming a JSon message

For basic JSon transformation where you have a fixed structure, you can represent with a combination of using Camel simple and JSonPath language as:

```json
{
  "company": "${jsonpath($.customer.name)}",
  "location": "${jsonpath($.customer.address.country)}",
  "gold": ${jsonpath($.customer.orders.length() > 5)}
}
```

Here we use the simple language to define the structure and use JSonPath as inlined functions via the `${jsonpath(exp)}` syntax.

This makes it possible to use simple as a template language to define a basic structure and then JSonPath to grab the data from an incoming JSon message. The output of the transformation is also JSon, but with simple you could also make it XML or plain text based:

```xml
<customer gold="${jsonpath($.customer.orders.length() > 5)}">
    <company>${jsonpath($.customer.name)}</company>
    <location>${jsonpath($.customer.address.country)}</location>
</customer>
```