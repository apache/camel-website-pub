# Set Variables

The SetVariables EIP is used for setting multiple [Exchange](../../../manual/exchange.md) variables at the same time.

## Options

The Set Variables eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **variables** | **Required** Contains the variables to be set. |  | List |

## Exchange properties

The Set Variables eip has no exchange properties.

## Using Set Variables

The following example shows how to set multiple variables in a Camel route using Java, XML or YAML. Note that the syntax is slightly different in each case.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setVariables("myVar", constant("test"), "otherVar", constant("other"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setVariables>
        <setVariable name="myVar">
            <constant>test</constant>
        </setVariable>
        <setVariable name="otherVar">
            <constant>other</constant>
        </setVariable>
    </setVariables>
    <to uri="direct:b"/>
</route>
```

```yaml
- from:
    uri: direct:a
    steps:
      - setVariables:
          variables:
            - name: myVar
              constant: test
            - name: otherVar
              constant: other
      - to:
          uri: direct:b
```

For example, the variables values are [constants](../../4.18.x/languages/constant-language.md).

Any of the Camel languages can be used, such as [Simple](../../4.18.x/languages/simple-language.md).

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setVariables("randomNumber", simple("${random(1,100)}"), "body", simple("${body}"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setVariables>
        <setVariable name="randomNumber">
            <simple>${random(1,100)}</simple>
        </setVariable>
        <setVariable name="body">
            <simple>${body}</simple>
        </setVariable>
    </setVariables>
    <to uri="direct:b"/>
</route>
```

```yaml
- from:
    uri: direct:a
    steps:
      - setVariables:
          variables:
            - name: randomNumber
              simple: "${random(1,100)}"
            - name: body
              simple: "${body}"
      - to:
          uri:direct:b
```

### Setting a variable from another variable

You can also set several variables where later ones depend on earlier ones.

In the example, we first set the variable foo to the body and then set bar based on comparing foo with a value.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setVariables("foo", simple("${body}"), "bar", simple("${variable.foo} > 10", Boolean.class))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setVariables>
	    <setVariable name="foo">
			<simple>${body}</simple>
		</setVariable>
		<setVariable name="bar">
			<simple resultType="java.lang.Boolean">${variable.foo} > 10</simple>
		</setVariable>
	</setVariables>
    <to uri="direct:b"/>
</route>
```

```yaml
- from:
    uri: direct:a
    steps:
      - setVariables:
          variables:
            - name: foo
              simple: "${body}"
            - name: bar
              simple:
                expression: "${variable.foo} > 10"
                resultType: "boolean"
      - to:
          uri:direct:b
```

### Using a Map with Java DSL

It’s also possible to build a Map and pass it as the single argument to `setVariables().` If the order in which the variables should be set is important, use a `LinkedHashMap`.

Java

```java
private Map<String, Expression> variableMap = new java.util.LinkedHashMap<>();
variableMap.put("foo", ConstantLanguage.constant("ABC"));
variableMap.put("bar", ConstantLanguage.constant("XYZ"));

from("direct:startMap")
    .setVariables(variableMap)
    .to("direct:b");
```

If the ordering is not critical, then `Map.of(name1, expr1, name2, expr2…​)` can be used.

Java

```java
from("direct:startMap")
    .setVariables(Map.of("foo", "ABC", "bar", "XYZ"))
    .to("direct:b");
```