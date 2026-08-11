# Set Headers

The SetHeaders EIP is used for setting multiple [message](message.md) headers at the same time.

## Options

The Set Headers eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **headers** | **Required** Contains the headers to be set. |  | List |

## Exchange properties

The Set Headers eip has no exchange properties.

## Using Set Headers

The following example shows how to set multiple headers in a Camel route using Java, XML or YAML. Note that the syntax is slightly different in each case.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setHeaders("myHeader", constant("test"), "otherHeader", constant("other"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setHeaders>
        <setHeader name="myHeader">
            <constant>test</constant>
        </setHeader>
        <setHeader name="otherHeader">
            <constant>other</constant>
        </setHeader>
    </setHeaders>
    <to uri="direct:b"/>
</route>
```

```yaml
- from:
    uri: direct:a
    steps:
      - setHeaders:
          headers:
            - name: myHeader
              constant: test
            - name: otherHeader
              constant: other
      - to:
          uri:direct:b
```

For example, the header values are [constants](../../4.22.x/languages/constant-language.md).

Any of the Camel languages can be used, such as [Simple](../../4.22.x/languages/simple-language.md).

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setHeaders("randomNumber", simple("${random(1,100)}"), "body", simple("${body}"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setHeaders>
        <setHeader name="randomNumber">
            <simple>${random(1,100)}</simple>
        </setHeader>
        <setHeader name="body">
            <simple>${body}</simple>
        </setHeader>
    </setHeaders>
    <to uri="direct:b"/>
</route>
```

```yaml
- from:
    uri: direct:a
    steps:
      - setHeaders:
          headers:
            - name: randomNumber
              simple: "${random(1,100)}"
            - name: body
              simple: "${body}"
      - to:
          uri:direct:b
```

### Setting a header from another header

You can also set several headers where later ones depend on earlier ones.

In the example, we first set the header foo to the body and then set bar based on comparing foo with a value.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setHeaders("foo", simple("${body}"), "bar", simple("${header.foo} > 10", Boolean.class))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setHeaders>
	    <setHeader name="foo">
			<simple>${body}</simple>
		</setHeader>
		<setHeader name="bar">
			<simple resultType="java.lang.Boolean">${header.foo} > 10</simple>
		</setHeader>
	</setHeaders>
    <to uri="direct:b"/>
</route>
```

```yaml
- from:
    uri: direct:a
    steps:
      - setHeaders:
          headers:
            - name: foo
              simple: "${body}"
            - name: bar
              simple:
                expression: "${header.foo} > 10"
                resultType: "boolean"
      - to:
          uri:direct:b
```

### Using a Map with Java DSL

It’s also possible to build a Map and pass it as the single argument to `setHeaders().` If the order in which the headers should be set is important, use a `LinkedHashMap`.

Java

```java
private Map<String, Expression> headerMap = new java.util.LinkedHashMap<>();
headerMap.put("foo", ConstantLanguage.constant("ABC"));
headerMap.put("bar", ConstantLanguage.constant("XYZ"));

from("direct:startMap")
    .setHeaders(headerMap)
    .to("direct:b");
```

If the ordering is not critical, then `Map.of(name1, expr1, name2, expr2…​)` can be used.

Java

```java
from("direct:startMap")
    .setHeaders(Map.of("foo", "ABC", "bar", "XYZ"))
    .to("direct:b");
```