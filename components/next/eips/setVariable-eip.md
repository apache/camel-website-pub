# Set Variable

The SetVariable EIP is used for setting an [Exchange](../../../manual/exchange.md) variable.

## Options

The Set Variable eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **name** | **Required** Name of variable to set a new value. The simple language can be used to define a dynamic evaluated variable name. Otherwise a constant name will be used. |  | String |
| **expression** | **Required** The expression whose result is used as the variable value. |  | ExpressionDefinition |

## Exchange properties

The Set Variable eip has no exchange properties.

## Example

The following example shows how to set a variable on the exchange in a Camel route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setVariable("myVar", constant("test"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setVariable name="myVar">
        <constant>test</constant>
    </setVariable>
    <to uri="direct:b"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:a
      steps:
        - setVariable:
            name: myVar
            expression:
              constant:
                expression: test
        - to:
            uri: direct:b
```

### Setting a variable from a message header

You can also set a variable with the value from a message header.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setVariable("foo", header("bar"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setVariable name="foo">
        <header>bar</header>
    </setVariable>
    <to uri="direct:b"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:a
      steps:
        - setVariable:
            name: foo
            expression:
              header:
                expression: bar
        - to:
            uri: direct:b
```

### Setting variable with the current message body

It is of course also possible to set a variable with a value from anything on the `Exchange` such as the message body, where we use the [Simple](../../4.18.x/languages/simple-language.md) language to refer to the message body:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setVariable("myBody", simple("${body}"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setVariable name="myBody">
        <simple>${body}</simple>
    </setVariable>
    <to uri="direct:b"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:a
      steps:
        - setVariable:
            name: myBody
            expression:
              simple:
                expression: "${body}"
        - to:
            uri: direct:b
```