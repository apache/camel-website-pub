# Simple

**Since Camel 1.1**

The Simple Expression Language was a really simple language when it was created, but has since grown more powerful. It is primarily intended for being a very small and simple language for evaluating `Expression` or `Predicate` without requiring any new dependencies or knowledge of other scripting languages such as Groovy.

The simple language is designed with intent to cover almost all the common use cases when little need for scripting in your Camel routes.

However, for much more complex use cases, then a more powerful language is recommended such as:

-   [Groovy](groovy-language.md)
    
-   [MVEL](mvel-language.md)
    
-   [OGNL](ognl-language.md)
    

> **Note**
> The simple language requires `camel-bean` JAR as classpath dependency if the simple language uses OGNL expressions, such as calling a method named `myMethod` on the message body: `${body.myMethod()}`. At runtime the simple language will then us its built-in OGNL support which requires the `camel-bean` component.

The simple language uses `${body}` placeholders for complex expressions or functions.

> **Note**
> See also the [CSimple](csimple-language.md) language which is **compiled**.

> **Tip**
> **Alternative syntax**
>
> You can also use the alternative syntax which uses `$simple{ }` as placeholders. This can be used in situations to avoid clashes when using, for example, Spring property placeholder together with Camel.

## Simple Language options

The Simple language supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **resultType** (common) |  | `String` | Sets the class of the result type (type from output). |
| **trim** (advanced) | `true` | `Boolean` | Whether to trim the value to remove leading and trailing whitespaces and line breaks. |

## Variables

  
| Variable | Type | Description |
| --- | --- | --- |
| camelId | String | the CamelContext name |
| camelContext.**OGNL** | Object | the CamelContext invoked using a Camel OGNL expression. |
| exchange | Exchange | the Exchange |
| exchange.**OGNL** | Object | the Exchange invoked using a Camel OGNL expression. |
| exchangeId | String | the exchange id |
| id | String | the message id |
| logExchange | String | Dumps the exchange for logging purpose (uses `ExchangeFormatter` to format the output). |
| messageTimestamp | long | the message timestamp (millis since epoc) that this message originates from. Some systems like JMS, Kafka, AWS have a timestamp on the event/message that Camel received. This method returns the timestamp if a timestamp exists. The message timestamp and exchange created are different. An exchange always has a created timestamp which is the local timestamp when Camel created the exchange. The message timestamp is only available in some Camel components when the consumer is able to extract the timestamp from the source event. If the message has no timestamp, then 0 is returned. |
| body | Object | the body |
| body.**OGNL** | Object | the body invoked using a Camel OGNL expression. |
| bodyAs(_type_) | Type | Converts the body to the given type determined by its classname. The converted body can be null. |
| bodyAs(_type_).**OGNL** | Object | Converts the body to the given type determined by its classname and then invoke methods using a Camel OGNL expression. The converted body can be null. |
| bodyOneLine | String | Converts the body to a String and removes all line-breaks, so the string is in one line. |
| prettyBody | String | Converts the body to a String, and attempts to pretty print if JSon or XML; otherwise the body is returned as the String value. |
| originalBody | Object | The original incoming body (only available if allowUseOriginalMessage=true). |
| mandatoryBodyAs(_type_) | Type | Converts the body to the given type determined by its classname, and expects the body to be not null. |
| mandatoryBodyAs(_type_).**OGNL** | Object | Converts the body to the given type determined by its classname and then invoke methods using a Camel OGNL expression. |
| header.foo | Object | refer to the foo header |
| header\[foo\] | Object | refer to the foo header |
| headers.foo | Object | refer to the foo header |
| headers:foo | Object | refer to the foo header |
| headers\[foo\] | Object | refer to the foo header |
| header.foo\[bar\] | Object | regard foo header as a map and perform lookup on the map with bar as the key |
| header.foo.**OGNL** | Object | refer to the foo header and invoke its value using a Camel OGNL expression. |
| headerAs(_key_,_type_) | Type | converts the header to the given type determined by its classname |
| headers | Map | refer to the headers |
| headers.size | int | The number of headers |
| variable.foo | Object | refer to the foo variable |
| variable\[foo\] | Object | refer to the foo variable |
| variable.foo.**OGNL** | Object | refer to the foo variable and invoke its value using a Camel OGNL expression. |
| variableAs(_key_,_type_) | Type | converts the variable to the given type determined by its classname |
| variables | Map | refer to the variables |
| variables.size | int | The number of variables |
| exchangeProperty.foo | Object | refer to the foo property on the exchange |
| exchangeProperty\[foo\] | Object | refer to the foo property on the exchange |
| exchangeProperty.foo.**OGNL** | Object | refer to the foo property on the exchange and invoke its value using a Camel OGNL expression. |
| messageAs(_type_) | Type | Converts the message to the given type determined by its classname. The converted message can be null. |
| messageAs(_type_).**OGNL** | Object | Converts the message to the given type determined by its classname and then invoke methods using a Camel OGNL expression. The converted message can be null. |
| sys.foo | String | refer to the JVM system property |
| sysenv.foo | String | refer to the system environment variable |
| env.foo | String | refer to the system environment variable |
| exception | Object | refer to the exception object on the exchange, is **null** if no exception set on exchange. Will fall back and grab caught exceptions (`Exchange.EXCEPTION_CAUGHT`) if the Exchange has any. |
| exception.**OGNL** | Object | refer to the exchange exception invoked using a Camel OGNL expression object |
| exception.message | String | refer to the `exception.message` on the exchange, is **null** if no exception set on exchange. Will fall back and grab caught exceptions (`Exchange.EXCEPTION_CAUGHT`) if the Exchange has any. |
| exception.stacktrace | String | refer to the exception.stracktrace on the exchange, is **null** if no exception set on exchange. Will fall back and grab caught exceptions (`Exchange.EXCEPTION_CAUGHT`) if the Exchange has any. |
| date:\_command\_ | Date | evaluates to a Date object. Supported commands are: `now` for current timestamp, `exchangeCreated` for the timestamp when the current exchange was created, `header.xxx` to use the Long/Date object in the header with the key xxx. `variable.xxx` to use the Long/Date in the variable with the key xxx. `exchangeProperty.xxx` to use the Long/Date object in the exchange property with the key xxx. `file` for the last modified timestamp of the file (available with a File consumer). Command accepts offsets such as: `now-24h` or `header.xxx+1h` or even `now+1h30m-100`. |
| date:\_command:pattern\_ | String | Date formatting using `java.text.SimpleDateFormat` patterns. |
| date-with-timezone:\_command:timezone:pattern\_ | String | Date formatting using `java.text.SimpleDateFormat` timezones and patterns. |
| bean:\_bean expression\_ | Object | Invoking a bean expression using the [Bean](../../4.18.x/bean-component.md) language. Specifying a method name, you must use dot as the separator. We also support the ?method=methodname syntax that is used by the [Bean](../../4.18.x/bean-component.md) component. Camel will by default lookup a bean by the given name. However, if you need to refer to a bean class (such as calling a static method), then you can prefix with the type, such as `bean:type:fqnClassName`. |
| properties:key:default | String | Lookup a property with the given key. If the key does not exist nor has a value, then an optional default value can be specified. |
| propertiesExist:key | boolean | Checks whether a property placeholder with the given key exists or not. The result can be negated by prefixing the key with `!`. |
| fromRouteId | String | Returns the original route id where this exchange was created. |
| routeId | String | Returns the route id of the current route the Exchange is being routed. |
| routeGroup | String | Returns the route group of the current route the Exchange is being routed. Not all routes have a group assigned, so this may be null. |
| stepId | String | Returns the id of the current step the Exchange is being routed. |
| threadId | String | Returns the id of the current thread. Can be used for logging. |
| threadName | String | Returns the name of the current thread. Can be used for logging. |
| hostname | String | Returns the local hostname (may be empty if not possible to resolve). |
| ref:xxx | Object | To look up a bean from the Registry with the given id. |
| type:name.field | Object | To refer to a type or field by its FQN name. To refer to a field, you can append .FIELD\_NAME. For example, you can refer to the constant field from Exchange as: `org.apache.camel.Exchange.FILE_NAME` |
| empty(type) | depends on parameter | Creates a new empty object of the type given as parameter. The type-parameter-Strings are case-insensitive.  
`string` → empty String  
`list` → empty ArrayList  
`map` → empty LinkedHashMap  
 |
| list(val1,val2,…​) | java.util.ArrayList | The list function creates an ArrayList with the given set of values. |
| map(key1,value1,…​) | java.util.LinkedHashMap | The map function creates a LinkedHashMap with the given set of pairs. |
| null | null | represents a **null** |
| random(value) | Integer | returns a random Integer between 0 (included) and _value_ (excluded) |
| random(min,max) | Integer | returns a random Integer between _min_ (included) and _max_ (excluded) |
| replace(from,to) | String | replace all the string values in the message body. To make it easier to replace single and double quotes, then you can use XML escaped values `&quot;` as double quote, `&apos;` as single quote, and `&empty;` as empty value. |
| replace(from,to,exp) | String | replace all the string values in the given expression. To make it easier to replace single and double quotes, then you can use XML escaped values `&quot;` as double quote, `&apos;` as single quote, and `&empty;` as empty value. |
| substring(num1) | String | returns a substring of the message body. If the number is positive, then the returned string is clipped from the beginning. If the number is negative, then the returned string is clipped from the ending. |
| substring(num1,num2) | String | returns a substring of the message body. If the number is positive, then the returned string is clipped from the beginning. If the number is negative, then the returned string is clipped from the ending. |
| substring(num1,num2,exp) | String | returns a substring of the given expression. If the number is positive, then the returned string is clipped from the beginning. If the number is negative, then the returned string is clipped from the ending. |
| collate(group) | List | The collate function iterates the message body and groups the data into sub lists of specified size. This can be used with the Splitter EIP to split a message body and group/batch the split sub message into a group of N sub lists. This method works similar to the collate method in Groovy. |
| skip(number) | Iterator | The skip function iterates the message body and skips the first number of items. This can be used with the Splitter EIP to split a message body and skip the first N number of items. |
| join(separator,prefix,exp) | String | The join function iterates the message body (by default) and joins the data into a string. The separator is by default a comma. The prefix is optional. The join uses the message body as source by default. It is possible to refer to another source (simple language) such as a header via the exp parameter. For example `join('&','id=','$\{header.ids}')`. |
| messageHistory | String | The message history of the current exchange - how it has been routed. This is similar to the route stack-trace message history the error handler logs in case of an unhandled exception. |
| messageHistory(false) | String | As messageHistory but without the exchange details (only includes the route stack-trace). This can be used if you do not want to log sensitive data from the message itself. |
| uuid(type) | String | Returns a UUID using the Camel `UuidGenerator`. You can choose between `default`, `classic`, `short`, `simple` and `random` as the type. If no type is given, the default is used. It is also possible to use a custom `UuidGenerator` and bind the bean to the [Registry](../../../manual/registry.md) with an id. For example `${uuid(myGenerator)}` where the ID is _myGenerator_. |
| hash(exp,algorithm) | String | Returns a hashed value (string in hex decimal) using JDK MessageDigest. The algorithm can be SHA-256 (default) or SHA3-256. |
| jsonpath(exp) | Object | When working with JSon data, then this allows using the JsonPath language, for example, to extract data from the message body (in JSon format). This requires having camel-jsonpath JAR on the classpath. |
| jsonpath(input,exp) | Object | When working with JSon data, then this allows using the JsonPath language, for example, to extract data from the message body (in JSon format). This requires having camel-jsonpath JAR on the classpath. For _input_, you can choose `header:key`, `exchangeProperty:key` or `variable:key` to use as input for the JSon payload instead of the message body. |
| jq(exp) | Object | When working with JSon data, then this allows using the JQ language, for example, to extract data from the message body (in JSon format). This requires having camel-jq JAR on the classpath. |
| jq(input,exp) | Object | When working with JSon data, then this allows using the JQ language, for example, to extract data from the message body (in JSon format). This requires having camel-jq JAR on the classpath. For _input_, you can choose `header:key`, `exchangeProperty:key` or `variable:key` to use as input for the JSon payload instead of the message body. |
| xpath(exp) | Object | When working with XML data, then this allows using the XPath language, for example, to extract data from the message body (in XML format). This requires having camel-xpath JAR on the classpath. |
| xpath(input,exp) | Object | When working with XML data, then this allows using the XPath language, for example, to extract data from the message body (in XML format). This requires having camel-xpath JAR on the classpath. For _input_ you can choose `header:key`, `exchangeProperty:key` or `variable:key` to use as input for the JSon payload instead of the message body. |
| pretty(exp) | String | Converts the inlined expression to a String, and attempts to pretty print if JSon or XML, otherwise the expression is returned as the String value. |
| iif(predicate, trueExp, falseExp) | Object | Evaluates the `predicate` expression and returns the value of `trueExp` if the predicate is true, otherwise the value of `falseExp` is returned. This function is similar to the ternary operator in Java. |

## Attachment functions

From **Camel 4.10** onwards then Camel has built-in attachment functions making it easy to obtain details from attachments stored on the Camel Message such as from HTTP file uploads, email with file attachments etc.

This requires having `camel-attachments` JAR on the classpath.

  
| Function | Type | Description |
| --- | --- | --- |
| attachments | Map | All the attachments as a `Map<String,DataHandler>`. |
| attachments.size | int | The number of attachments. Is 0 if there are no attachments. |
| attachmentContentAsText(key) | String | The content of the attachment as text (ie `String`). |
| attachmentContent(key) | Object | The content of the attachment. |
| attachmentContentAs(key,_type_) | Object | The content of the attachment, converted to the given type. |
| attachmentHeader(key,name) | Object | The attachment header with the given name. |
| attachmentHeaderAs(key,name,_type_) | Object | The attachment header with the given name, converted to the given type. |
| attachment\[key\] | DataHandler | The `DataHandler` for the given attachment. |
| attachment.**OGNL** | Object | refer to the foo attachment on the exchange and invoke its value using a Camel OGNL expression. |

## OGNL expression support

The [Simple](#) and [Bean](#) languages support a Camel [OGNL](ognl-language.md) notation for invoking beans in a chain like fashion.

[OGNL](https://en.wikipedia.org/wiki/OGNL) (Object-Graph Navigation Language) is a powerful expression language used in Java. In Camel you can use OGNL dot notation to invoke methods. If you for instance have a body that contains a POJO that has a `getFamilyName` method then you can construct the Simple syntax as follows:

```java
simple("${body.familyName}")
```

Or use similar syntax as in Java:

```java
simple("${body.getFamilyName()}")
```

Camel’s OGNL support is for invoking methods only. You cannot access fields. Camel support accessing the length field of Java arrays.

> **Note**
> When using **OGNL** then `camel-bean` JAR is required to be on the classpath.

### OGNL Variables

The following variables support OGNL:

| Variable |
| --- |
| camelContext |
| exchange |
| exception |
| body |
| bodyAs(type) |
| messageAs(type) |
| header.foo |
| exchangeProperty.foo |
| variable.foo |

### Basic OGNL examples

Suppose the Message IN body contains a POJO which has a `getAddress()` method. Then you can use Camel OGNL notation to access the address object:

```java
simple("${body.address}")
simple("${body.address.street}")
simple("${body.address.zip}")
```

Camel understands the shorthand names for getters, but you can invoke any method or use the real name such as:

```java
simple("${body.address}")
simple("${body.getAddress.getStreet}")
simple("${body.address.getZip}")
simple("${body.doSomething}")
```

You can also use the null safe operator (`?.`) to avoid NPE if, for example, the body does NOT have an address

```java
simple("${body?.address?.street}")
```

### Advanced OGNL examples

It is also possible to index in `Map` or `List` types, so you can do:

```java
simple("${body[foo].name}")
```

To assume the body is `Map` based and look up the value with `foo` as key, and invoke the `getName` method on that value.

If the key has space, then you **must** enclose the key with quotes, for example, 'foo bar':

```java
simple("${body['foo bar'].name}")
```

You can access the `Map` or `List` objects directly using their key name (with or without dots) :

```java
simple("${body[foo]}")
simple("${body[this.is.foo]}")
```

Suppose there was no value with the key `foo` then you can use the null safe operator to avoid the NPE as shown:

```java
simple("${body[foo]?.name}")
```

You can also access `List` types, for example, to get lines from the address you can do:

```java
simple("${body.address.lines[0]}")
simple("${body.address.lines[1]}")
simple("${body.address.lines[2]}")
```

There is a special `last` keyword which can be used to get the last value from a list.

```java
simple("${body.address.lines[last]}")
```

And to get the 2nd last you can subtract a number, so we can use `last-1` to indicate this:

```java
simple("${body.address.lines[last-1]}")
```

And the third last is, of course:

```java
simple("${body.address.lines[last-2]}")
```

And you can call the size method on the list with

```java
simple("${body.address.lines.size}")
```

Camel supports the length field for Java arrays as well, e.g.:

```java
String[] lines = new String[]{"foo", "bar", "cat"};
exchange.getIn().setBody(lines);

simple("There are ${body.length} lines")
```

And yes, you can combine this with the operator support as shown below:

```java
simple("${body.address.zip} > 1000")
```

## Operator support

The parser is limited to only support a single operator.

To enable it, the left value must be enclosed in `${ }`. The syntax is:

${leftValue} OP rightValue

Where the `rightValue` can be a String literal enclosed in `' '`, `null`, a constant value or another expression enclosed in `${ }`.

> **Important**
> There **must** be spaces around the operator.

Camel will automatically type convert the rightValue type to the leftValue type, so it is able to e.g., convert a string into a numeric, so you can use `>` comparison for numeric values.

The following operators are supported:

 
| Operator | Description |
| --- | --- |
| \== | equals |
| \=~ | equals ignore case (will ignore case when comparing String values) |
| \> | greater than |
| \>= | greater than or equals |
| < | less than |
| <= | less than or equals |
| != | not equals |
| !=~ | not equals ignore case (will ignore case when comparing String values) |
| contains | For testing if contains in a string-based value |
| !contains | For testing if it does not contain in a string-based value |
| ~~ | For testing if contains by ignoring case sensitivity in a string-based value |
| !~~ | For testing if it does not contain by ignoring case sensitivity in a string-based value |
| regex | For matching against a given regular expression pattern defined as a String value |
| !regex | For not matching against a given regular expression pattern defined as a String value |
| in | For matching if in a set of values, each element must be separated by comma. If you want to include an empty value, then it must be defined using double comma, e.g. `',, bronze,silver,gold'`, which is a set of four values with an empty value and then the three medals. |
| !in | For matching if not in a set of values, each element must be separated by comma. If you want to include an empty value, then it must be defined using double comma, e.g. `',,bronze,silver,gold'`, which is a set of four values with an empty value and then the three medals. |
| is | For matching if the left-hand side type is an instance of the value. |
| !is | For matching if the left-hand side type is not an instance of the value. |
| range | For matching if the left-hand side is within a range of values defined as numbers: `from..to`.. |
| !range | For matching if the left-hand side is not within a range of values defined as numbers: `from..to`. . |
| startsWith | For testing if the left-hand side string starts with the right-hand string. |
| starts with | Same as the startsWith operator. |
| endsWith | For testing if the left-hand side string ends with the right-hand string. |
| ends with | Same as the endsWith operator. |

And the following unary operators can be used:

 
| Operator | Description |
| --- | --- |
| ++ | To increment a number by one. The left-hand side must be a function, otherwise parsed as literal. |
|  —  | To decrement a number by one. The left-hand side must be a function, otherwise parsed as literal. |
| \\n | To use newline character. |
| \\t | To use tab character. |
| \\r | To use carriage return character. |
| \\} | To use the `}` character as text. This may be needed when building a JSon structure with the simple language. |

And the following logical operators can be used to group expressions:

 
| Operator | Description |
| --- | --- |
| && | The logical and operator is used to group two expressions. |
| || | The logical or operator is used to group two expressions. |

The syntax for AND is:

```text
${leftValue} OP rightValue && ${leftValue} OP rightValue
```

And the syntax for OR is:

```text
${leftValue} OP rightValue || ${leftValue} OP rightValue
```

Some examples:

```java
// exact equals match
simple("${header.foo} == 'foo'")

// ignore case when comparing, so if the header has value FOO, this will match
simple("${header.foo} =~ 'foo'")

// here Camel will type convert '100' into the type of header.bar and if it is an Integer '100' will also be converter to an Integer
simple("${header.bar} == '100'")

simple("${header.bar} == 100")

// 100 will be converter to the type of header.bar, so we can do > comparison
simple("${header.bar} > 100")

// if the value of header.bar was 100, value returned will be 101. header.bar itself will not be changed.
simple("${header.bar}++")
```

### Comparing with different types

When you compare with different types such as String and int, then you have to take a bit of care. Camel will use the type from the left-hand side as first priority. And fallback to the right-hand side type if both values couldn’t be compared based on that type.  
This means you can flip the values to enforce a specific type. Suppose the bar value above is a String. Then you can flip the equation:

```java
simple("100 < ${header.bar}")
```

which then ensures the int type is used as first priority.

This may change in the future if the Camel team improves the binary comparison operations to prefer numeric types to String-based. It’s most often the String type which causes problems when comparing with numbers.

```java
// testing for null
simple("${header.baz} == null")

// testing for not null
simple("${header.baz} != null")
```

And a bit more advanced example where the right value is another expression

```java
simple("${header.date} == ${date:now:yyyyMMdd}")

simple("${header.type} == ${bean:orderService?method=getOrderType}")
```

And an example with `contains`, testing if the title contains the word Camel

```java
simple("${header.title} contains 'Camel'")
```

And an example with regex, testing if the number header is a 4-digit value:

```java
simple("${header.number} regex '\\d{4}'")
```

And finally an example if the header equals any of the values in the list. Each element must be separated by comma, and no space around.  
This also works for numbers etc., as Camel will convert each element into the type of the left-hand side.

```java
simple("${header.type} in 'gold,silver'")
```

And for all the last 3, we also support the negate test using not:

```java
simple("${header.type} !in 'gold,silver'")
```

And you can test if the type is a certain instance, e.g., for instance a String

```java
simple("${header.type} is 'java.lang.String'")
```

We have added a shorthand for all `java.lang` types, so you can write it as:

```java
simple("${header.type} is 'String'")
```

Ranges are also supported. The range interval requires numbers and both from and end are inclusive. For instance, to test whether a value is between 100 and 199:

```java
simple("${header.number} range 100..199")
```

Notice we use `..` in the range without spaces. It is based on the same syntax as Groovy.

```java
simple("${header.number} range '100..199'")
```

As the XML DSL does not have all the power as the Java DSL with all its various builder methods, you have to resort to using some other languages for testing with simple operators. Now you can do this with the simple language. In the sample below, we want to test it if the header is a widget order:

```xml
<from uri="seda:orders">
   <filter>
       <simple>${header.type} == 'widget'</simple>
       <to uri="bean:orderService?method=handleWidget"/>
   </filter>
</from>
```

### Using and / or

If you have two expressions you can combine them with the `&&` or `||` operator.

For instance:

```java
simple("${header.title} contains 'Camel' && ${header.type'} == 'gold'")
```

And of course the `||` is also supported. The sample would be:

```java
simple("${header.title} contains 'Camel' || ${header.type'} == 'gold'")
```

## Examples

In the XML DSL sample below, we filter based on a header value:

```xml
<from uri="seda:orders">
   <filter>
       <simple>${header.foo}</simple>
       <to uri="mock:fooOrders"/>
   </filter>
</from>
```

The Simple language can be used for the predicate test above in the Message Filter pattern, where we test if the in message has a `foo` header (a header with the key `foo` exists). If the expression evaluates to `**true**`, then the message is routed to the `mock:fooOrders` endpoint, otherwise the message is dropped.

The same example in Java DSL:

```java
from("seda:orders")
    .filter().simple("${header.foo}")
        .to("seda:fooOrders");
```

You can also use the simple language for simple text concatenations such as:

```java
from("direct:hello")
    .transform().simple("Hello ${header.user} how are you?")
    .to("mock:reply");
```

Notice that we must use `${ }` placeholders in the expression now to allow Camel to parse it correctly.

And this sample uses the date command to output current date.

```java
from("direct:hello")
    .transform().simple("The today is ${date:now:yyyyMMdd} and it is a great day.")
    .to("mock:reply");
```

And in the sample below, we invoke the bean language to invoke a method on a bean to be included in the returned string:

```java
from("direct:order")
    .transform().simple("OrderId: ${bean:orderIdGenerator}")
    .to("mock:reply");
```

Where `orderIdGenerator` is the id of the bean registered in the Registry. If using Spring, then it is the Spring bean id.

If we want to declare which method to invoke on the order id generator bean we must prepend `.method name` such as below where we invoke the `generateId` method.

```java
from("direct:order")
    .transform().simple("OrderId: ${bean:orderIdGenerator.generateId}")
    .to("mock:reply");
```

We can use the `?method=methodname` option that we are familiar with the [Bean](../../4.18.x/bean-component.md) component itself:

```java
from("direct:order")
    .transform().simple("OrderId: ${bean:orderIdGenerator?method=generateId}")
    .to("mock:reply");
```

You can also convert the body to a given type, for example, to ensure that it is a String you can do:

```xml
<transform>
  <simple>Hello ${bodyAs(String)} how are you?</simple>
</transform>
```

There are a few types which have a shorthand notation, so we can use `String` instead of `java.lang.String`. These are: `byte[], String, Integer, Long`. All other types must use their FQN name, e.g. `org.w3c.dom.Document`.

It is also possible to look up a value from a header `Map`:

```xml
<transform>
  <simple>The gold value is ${header.type[gold]}</simple>
</transform>
```

In the code above we look up the header with name `type` and regard it as a `java.util.Map` and we then look up with the key `gold` and return the value. If the header is not convertible to Map, an exception is thrown. If the header with name `type` does not exist `null` is returned.

You can nest functions, such as shown below:

```xml
<setHeader name="myHeader">
  <simple>${properties:${header.someKey}}</simple>
</setHeader>
```

### Substring

You can use the `substring` function to more easily clip the message body. For example if the message body contains the following 10 letters `ABCDEFGHIJ` then:

```xml
<setBody>
  <simple>${substring(3)}</simple>
</setBody>
```

Then the message body after the substring will be `DEFGHIJ`. If you want to clip from the end instead, then use negative values such as `substring(-3)`.

You can also clip from both ends at the same time such as `substring(1,-1)` that will clip the first and last character in the String.

If the number is higher than the length of the message body, then an empty string is returned, for example `substring(99)`.

Instead of the message body then a simple expression can be nested as input, for example, using a variable, as shown below:

```xml
<setBody>
  <simple>${substring(1,-1,${variable.foo})}</simple>
</setBody>
```

### Replacing double and single quotes

You can use the `replace` function to more easily replace all single or double quotes in the message body, using the XML escape syntax. This avoids to fiddle with enclosing a double quote or single quotes with outer quotes, that can get confusing to be correct as you may need to escape the quotes as well. So instead you can use the XML escape syntax where double quote is `&quot;` and single quote is `&apos;` (yeah that is the name).

For example, to replace all double quotes with single quotes:

```java
from("direct:order")
  .transform().simple("${replace(&quot; , &apos;)}")
  .to("mock:reply");
```

And to replace all single quotes with double quotes:

```xml
<setBody>
  <simple>${replace(&apos; , &quot;)}</simple>
</setBody>
```

Or to remove all double quotes:

```xml
<setBody>
  <simple>${replace(&quot; , &empty;)}</simple>
</setBody>
```

## Setting the result type

You can now provide a result type to the [Simple](#) expression, which means the result of the evaluation will be converted to the desired type. This is most usable to define types such as booleans, integers, etc.

For example, to set a header as a boolean type, you can do:

```java
.setHeader("cool", simple("true", Boolean.class))
```

And in XML DSL

```xml
<setHeader name="cool">
  <!-- use resultType to indicate that the type should be a java.lang.Boolean -->
  <simple resultType="java.lang.Boolean">true</simple>
</setHeader>
```

## Using new lines or tabs in XML DSLs

It is easier to specify new lines or tabs in XML DSLs as you can escape the value now

```xml
<transform>
  <simple>The following text\nis on a new line</simple>
</transform>
```

## Leading and trailing whitespace handling

The trim attribute of the expression can be used to control whether the leading and trailing whitespace characters are removed or preserved. The default value is true, which removes the whitespace characters.

```xml
<setBody>
  <simple trim="false">You get some trailing whitespace characters.     </simple>
</setBody>
```

## Loading script from external resource

You can externalize the script and have Camel load it from a resource such as `"classpath:"`, `"file:"`, or `"http:"`. This is done using the following syntax: `"resource:scheme:location"`, e.g., to refer to a file on the classpath you can do:

```java
.setHeader("myHeader").simple("resource:classpath:mysimple.txt")
```

## Spring Boot Auto-Configuration

When using simple with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-core-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 114 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.cloud.consul.service-discovery.acl-token** | Sets the ACL token to be used with Consul. |  | String |
| **camel.cloud.consul.service-discovery.block-seconds** | The seconds to wait for a watch event, default 10 seconds. | 10 | Integer |
| **camel.cloud.consul.service-discovery.configurations** | Define additional configuration definitions. |  | Map |
| **camel.cloud.consul.service-discovery.connect-timeout-millis** | Connect timeout for OkHttpClient. |  | Long |
| **camel.cloud.consul.service-discovery.datacenter** | The data center. |  | String |
| **camel.cloud.consul.service-discovery.enabled** | Enable the component. | true | Boolean |
| **camel.cloud.consul.service-discovery.password** | Sets the password to be used for basic authentication. |  | String |
| **camel.cloud.consul.service-discovery.properties** | Set client properties to use. These properties are specific to what service call implementation are in use. For example if using a different one, then the client properties are defined according to the specific service in use. |  | Map |
| **camel.cloud.consul.service-discovery.read-timeout-millis** | Read timeout for OkHttpClient. |  | Long |
| **camel.cloud.consul.service-discovery.url** | The Consul agent URL. |  | String |
| **camel.cloud.consul.service-discovery.user-name** | Sets the username to be used for basic authentication. |  | String |
| **camel.cloud.consul.service-discovery.write-timeout-millis** | Write timeout for OkHttpClient. |  | Long |
| **camel.cloud.dns.service-discovery.configurations** | Define additional configuration definitions. |  | Map |
| **camel.cloud.dns.service-discovery.domain** | The domain name;. |  | String |
| **camel.cloud.dns.service-discovery.enabled** | Enable the component. | true | Boolean |
| **camel.cloud.dns.service-discovery.properties** | Set client properties to use. These properties are specific to what service call implementation are in use. For example if using a different one, then the client properties are defined according to the specific service in use. |  | Map |
| **camel.cloud.dns.service-discovery.proto** | The transport protocol of the desired service. | \_tcp | String |
| **camel.cloud.kubernetes.service-discovery.api-version** | Sets the API version when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.ca-cert-data** | Sets the Certificate Authority data when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.ca-cert-file** | Sets the Certificate Authority data that are loaded from the file when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-cert-data** | Sets the Client Certificate data when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-cert-file** | Sets the Client Certificate data that are loaded from the file when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-key-algo** | Sets the Client Keystore algorithm, such as RSA when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-key-data** | Sets the Client Keystore data when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-key-file** | Sets the Client Keystore data that are loaded from the file when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.client-key-passphrase** | Sets the Client Keystore passphrase when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.configurations** | Define additional configuration definitions. |  | Map |
| **camel.cloud.kubernetes.service-discovery.dns-domain** | Sets the DNS domain to use for DNS lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.enabled** | Enable the component. | true | Boolean |
| **camel.cloud.kubernetes.service-discovery.lookup** | How to perform service lookup. Possible values: client, dns, environment. When using client, then the client queries the kubernetes master to obtain a list of active pods that provides the service, and then random (or round robin) select a pod. When using dns the service name is resolved as name.namespace.svc.dnsDomain. When using dnssrv the service name is resolved with SRV query for _._…​svc…​ When using environment then environment variables are used to lookup the service. By default environment is used. | environment | String |
| **camel.cloud.kubernetes.service-discovery.master-url** | Sets the URL to the master when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.namespace** | Sets the namespace to use. Will by default use namespace from the ENV variable KUBERNETES\_MASTER. |  | String |
| **camel.cloud.kubernetes.service-discovery.oauth-token** | Sets the OAUTH token for authentication (instead of username/password) when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.password** | Sets the password for authentication when using client lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.port-name** | Sets the Port Name to use for DNS/DNSSRV lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.port-protocol** | Sets the Port Protocol to use for DNS/DNSSRV lookup. |  | String |
| **camel.cloud.kubernetes.service-discovery.properties** | Set client properties to use. These properties are specific to what service call implementation are in use. For example if using a different one, then the client properties are defined according to the specific service in use. |  | Map |
| **camel.cloud.kubernetes.service-discovery.trust-certs** | Sets whether to turn on trust certificate check when using client lookup. | false | Boolean |
| **camel.cloud.kubernetes.service-discovery.username** | Sets the username for authentication when using client lookup. |  | String |
| **camel.language.constant.enabled** | Whether to enable auto configuration of the constant language. This is enabled by default. |  | Boolean |
| **camel.language.constant.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.csimple.enabled** | Whether to enable auto configuration of the csimple language. This is enabled by default. |  | Boolean |
| **camel.language.csimple.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.exchange-property.enabled** | Whether to enable auto configuration of the exchangeProperty language. This is enabled by default. |  | Boolean |
| **camel.language.exchange-property.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.file.enabled** | Whether to enable auto configuration of the file language. This is enabled by default. |  | Boolean |
| **camel.language.file.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.header.enabled** | Whether to enable auto configuration of the header language. This is enabled by default. |  | Boolean |
| **camel.language.header.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.ref.enabled** | Whether to enable auto configuration of the ref language. This is enabled by default. |  | Boolean |
| **camel.language.ref.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.simple.enabled** | Whether to enable auto configuration of the simple language. This is enabled by default. |  | Boolean |
| **camel.language.simple.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.tokenize.enabled** | Whether to enable auto configuration of the tokenize language. This is enabled by default. |  | Boolean |
| **camel.language.tokenize.group-delimiter** | Sets the delimiter to use when grouping. If this has not been set then token will be used as the delimiter. |  | String |
| **camel.language.tokenize.source** | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| **camel.language.tokenize.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.language.variable.enabled** | Whether to enable auto configuration of the variable language. This is enabled by default. |  | Boolean |
| **camel.language.variable.trim** | Whether to trim the value to remove leading and trailing whitespaces and line breaks. | true | Boolean |
| **camel.resilience4j.automatic-transition-from-open-to-half-open-enabled** | Enables automatic transition from OPEN to HALF\_OPEN state once the waitDurationInOpenState has passed. | false | Boolean |
| **camel.resilience4j.bulkhead-enabled** | Whether bulkhead is enabled or not on the circuit breaker. Default is false. | false | Boolean |
| **camel.resilience4j.bulkhead-max-concurrent-calls** | Configures the max amount of concurrent calls the bulkhead will support. | 25 | Integer |
| **camel.resilience4j.bulkhead-max-wait-duration** | Configures a maximum amount of time which the calling thread will wait to enter the bulkhead. If bulkhead has space available, entry is guaranteed and immediate. If bulkhead is full, calling threads will contest for space, if it becomes available. maxWaitDuration can be set to 0. Note: for threads running on an event-loop or equivalent (rx computation pool, etc), setting maxWaitDuration to 0 is highly recommended. Blocking an event-loop thread will most likely have a negative effect on application throughput. | 0 | Integer |
| **camel.resilience4j.circuit-breaker** | Refers to an existing io.github.resilience4j.circuitbreaker.CircuitBreaker instance to lookup and use from the registry. When using this, then any other circuit breaker options are not in use. |  | String |
| **camel.resilience4j.config** | Refers to an existing io.github.resilience4j.circuitbreaker.CircuitBreakerConfig instance to lookup and use from the registry. |  | String |
| **camel.resilience4j.configurations** | Define additional configuration definitions. |  | Map |
| **camel.resilience4j.enabled** | Enable the component. | true | Boolean |
| **camel.resilience4j.failure-rate-threshold** | Configures the failure rate threshold in percentage. If the failure rate is equal or greater than the threshold the CircuitBreaker transitions to open and starts short-circuiting calls. The threshold must be greater than 0 and not greater than 100. Default value is 50 percentage. |  | Float |
| **camel.resilience4j.ignore-exception** | Configure a list of exceptions that are ignored and neither count as a failure nor success. Any exception matching or inheriting from one of the list will not count as a failure nor success, even if the exceptions is part of recordExceptions. |  | List |
| **camel.resilience4j.minimum-number-of-calls** | Configures the minimum number of calls which are required (per sliding window period) before the CircuitBreaker can calculate the error rate. For example, if minimumNumberOfCalls is 10, then at least 10 calls must be recorded, before the failure rate can be calculated. If only 9 calls have been recorded the CircuitBreaker will not transition to open even if all 9 calls have failed. Default minimumNumberOfCalls is 100. | 100 | Integer |
| **camel.resilience4j.permitted-number-of-calls-in-half-open-state** | Configures the number of permitted calls when the CircuitBreaker is half open. The size must be greater than 0. Default size is 10. | 10 | Integer |
| **camel.resilience4j.record-exception** | Configure a list of exceptions that are recorded as a failure and thus increase the failure rate. Any exception matching or inheriting from one of the list counts as a failure, unless explicitly ignored via ignoreExceptions. |  | List |
| **camel.resilience4j.sliding-window-size** | Configures the size of the sliding window which is used to record the outcome of calls when the CircuitBreaker is closed. slidingWindowSize configures the size of the sliding window. Sliding window can either be count-based or time-based. If slidingWindowType is COUNT\_BASED, the last slidingWindowSize calls are recorded and aggregated. If slidingWindowType is TIME\_BASED, the calls of the last slidingWindowSize seconds are recorded and aggregated. The slidingWindowSize must be greater than 0. The minimumNumberOfCalls must be greater than 0. If the slidingWindowType is COUNT\_BASED, the minimumNumberOfCalls cannot be greater than slidingWindowSize . If the slidingWindowType is TIME\_BASED, you can pick whatever you want. Default slidingWindowSize is 100. | 100 | Integer |
| **camel.resilience4j.sliding-window-type** | Configures the type of the sliding window which is used to record the outcome of calls when the CircuitBreaker is closed. Sliding window can either be count-based or time-based. If slidingWindowType is COUNT\_BASED, the last slidingWindowSize calls are recorded and aggregated. If slidingWindowType is TIME\_BASED, the calls of the last slidingWindowSize seconds are recorded and aggregated. Default slidingWindowType is COUNT\_BASED. | COUNT\_BASED | String |
| **camel.resilience4j.slow-call-duration-threshold** | Configures the duration threshold (seconds) above which calls are considered as slow and increase the slow calls percentage. Default value is 60 seconds. | 60 | Integer |
| **camel.resilience4j.slow-call-rate-threshold** | Configures a threshold in percentage. The CircuitBreaker considers a call as slow when the call duration is greater than slowCallDurationThreshold Duration. When the percentage of slow calls is equal or greater the threshold, the CircuitBreaker transitions to open and starts short-circuiting calls. The threshold must be greater than 0 and not greater than 100. Default value is 100 percentage which means that all recorded calls must be slower than slowCallDurationThreshold. |  | Float |
| **camel.resilience4j.throw-exception-when-half-open-or-open-state** | Whether to throw io.github.resilience4j.circuitbreaker.CallNotPermittedException when the call is rejected due circuit breaker is half open (and was not attempted but rejected immediately) or open (always rejected). This option is only in use when there is NOT a fallback configured on the circuit breaker. When there is a fallback then the fallback is always executed and CallNotPermittedException is not thrown. | false | Boolean |
| **camel.resilience4j.timeout-cancel-running-future** | Configures whether cancel is called on the running future. Defaults to true. | true | Boolean |
| **camel.resilience4j.timeout-duration** | Configures the thread execution timeout. Default value is 1 second. | 1000 | Integer |
| **camel.resilience4j.timeout-enabled** | Whether timeout is enabled or not on the circuit breaker. Default is false. | false | Boolean |
| **camel.resilience4j.timeout-executor-service** | References to a custom thread pool to use when timeout is enabled (uses ForkJoinPool#commonPool() by default). |  | ExecutorService |
| **camel.resilience4j.wait-duration-in-open-state** | Configures the wait duration (in seconds) which specifies how long the CircuitBreaker should stay open, before it switches to half open. Default value is 60 seconds. | 60 | Integer |
| **camel.resilience4j.writable-stack-trace-enabled** | Enables writable stack traces. When set to false, Exception.getStackTrace returns a zero length array. This may be used to reduce log spam when the circuit breaker is open as the cause of the exceptions is already known (the circuit breaker is short-circuiting calls). | true | Boolean |
| **camel.rest.api-component** | The name of the Camel component to use as the REST API. If no API Component has been explicit configured, then Camel will lookup if there is a Camel component responsible for servicing and generating the REST API documentation, or if a org.apache.camel.spi.RestApiProcessorFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **camel.rest.api-context-path** | Sets a leading context-path the REST API will be using. This can be used when using components such as camel-servlet where the deployed web application is deployed using a context-path. |  | String |
| **camel.rest.api-context-route-id** | Sets the route id to use for the route that services the REST API. The route will by default use an auto assigned route id. |  | String |
| **camel.rest.api-host** | To use a specific hostname for the API documentation (such as swagger or openapi) This can be used to override the generated host with this configured hostname. |  | String |
| **camel.rest.api-property** | Allows to configure as many additional properties for the api documentation. For example set property api.title to my cool stuff. |  | Map |
| **camel.rest.api-vendor-extension** | Whether vendor extension is enabled in the Rest APIs. If enabled then Camel will include additional information as vendor extension (eg keys starting with x-) such as route ids, class names etc. Not all 3rd party API gateways and tools supports vendor-extensions when importing your API docs. | false | Boolean |
| **camel.rest.binding-mode** | Sets the binding mode to use. The default value is off. | off | RestBindingMode |
| **camel.rest.binding-package-scan** | Package name to use as base (offset) for classpath scanning of POJO classes are located when using binding mode is enabled for JSon or XML. Multiple package names can be separated by comma. |  | String |
| **camel.rest.client-request-validation** | Whether to enable validation of the client request to check: 1) Content-Type header matches what the Rest DSL consumes; returns HTTP Status 415 if validation error. 2) Accept header matches what the Rest DSL produces; returns HTTP Status 406 if validation error. 3) Missing required data (query parameters, HTTP headers, body); returns HTTP Status 400 if validation error. 4) Parsing error of the message body (JSon, XML or Auto binding mode must be enabled); returns HTTP Status 400 if validation error. | false | Boolean |
| **camel.rest.client-response-validation** | Whether to check what Camel is returning as response to the client: 1) Status-code and Content-Type matches Rest DSL response messages. 2) Check whether expected headers is included according to the Rest DSL repose message headers. 3) If the response body is JSon then check whether its valid JSon. Returns 500 if validation error detected. | false | Boolean |
| **camel.rest.component** | The Camel Rest component to use for the REST transport (consumer), such as netty-http, jetty, servlet, undertow. If no component has been explicit configured, then Camel will lookup if there is a Camel component that integrates with the Rest DSL, or if a org.apache.camel.spi.RestConsumerFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **camel.rest.component-property** | Allows to configure as many additional properties for the rest component in use. |  | Map |
| **camel.rest.consumer-property** | Allows to configure as many additional properties for the rest consumer in use. |  | Map |
| **camel.rest.context-path** | Sets a leading context-path the REST services will be using. This can be used when using components such as camel-servlet where the deployed web application is deployed using a context-path. Or for components such as camel-jetty or camel-netty-http that includes a HTTP server. |  | String |
| **camel.rest.cors-headers** | Allows to configure custom CORS headers. |  | Map |
| **camel.rest.data-format-property** | Allows to configure as many additional properties for the data formats in use. For example set property prettyPrint to true to have json outputted in pretty mode. The properties can be prefixed to denote the option is only for either JSON or XML and for either the IN or the OUT. The prefixes are: json.in. json.out. xml.in. xml.out. For example a key with value xml.out.mustBeJAXBElement is only for the XML data format for the outgoing. A key without a prefix is a common key for all situations. |  | Map |
| **camel.rest.enable-cors** | Whether to enable CORS headers in the HTTP response. The default value is false. | false | Boolean |
| **camel.rest.enable-no-content-response** | Whether to return HTTP 204 with an empty body when a response contains an empty JSON object or XML root object. The default value is false. | false | Boolean |
| **camel.rest.endpoint-property** | Allows to configure as many additional properties for the rest endpoint in use. |  | Map |
| **camel.rest.host** | The hostname to use for exposing the REST service. |  | String |
| **camel.rest.host-name-resolver** | If no hostname has been explicit configured, then this resolver is used to compute the hostname the REST service will be using. | alllocalip | RestHostNameResolver |
| **camel.rest.inline-routes** | Inline routes in rest-dsl which are linked using direct endpoints. Each service in Rest DSL is an individual route, meaning that you would have at least two routes per service (rest-dsl, and the route linked from rest-dsl). By inlining (default) allows Camel to optimize and inline this as a single route, however this requires to use direct endpoints, which must be unique per service. If a route is not using direct endpoint then the rest-dsl is not inlined, and will become an individual route. This option is default true. | true | Boolean |
| **camel.rest.json-data-format** | Name of specific json data format to use. By default jackson will be used. Important: This option is only for setting a custom name of the data format, not to refer to an existing data format instance. |  | String |
| **camel.rest.port** | The port number to use for exposing the REST service. Notice if you use servlet component then the port number configured here does not apply, as the port number in use is the actual port number the servlet component is using. eg if using Apache Tomcat its the tomcat http port, if using Apache Karaf its the HTTP service in Karaf that uses port 8181 by default etc. Though in those situations setting the port number here, allows tooling and JMX to know the port number, so its recommended to set the port number to the number that the servlet engine uses. |  | String |
| **camel.rest.producer-api-doc** | Sets the location of the api document the REST producer will use to validate the REST uri and query parameters are valid accordingly to the api document. The location of the api document is loaded from classpath by default, but you can use file: or http: to refer to resources to load from file or http url. |  | String |
| **camel.rest.producer-component** | Sets the name of the Camel component to use as the REST producer. |  | String |
| **camel.rest.scheme** | The scheme to use for exposing the REST service. Usually http or https is supported. The default value is http. |  | String |
| **camel.rest.skip-binding-on-error-code** | Whether to skip binding on output if there is a custom HTTP error code header. This allows to build custom error messages that do not bind to json / xml etc, as success messages otherwise will do. | false | Boolean |
| **camel.rest.use-x-forward-headers** | Whether to use X-Forward headers to set host etc. for OpenApi. This may be needed in special cases involving reverse-proxy and networking going from HTTP to HTTPS etc. Then the proxy can send X-Forward headers (X-Forwarded-Proto) that influences the host names in the OpenAPI schema that camel-openapi-java generates from Rest DSL routes. | false | Boolean |
| **camel.rest.validation-levels** | Allows to configure custom validation levels when using camel-openapi-validator with client request/response validator. |  | Map |
| **camel.rest.xml-data-format** | Name of specific XML data format to use. By default jaxb will be used. Important: This option is only for setting a custom name of the data format, not to refer to an existing data format instance. |  | String |