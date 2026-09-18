# Set Variable

The SetVariable EIP is used for setting an [Exchange](../../../manual/exchange.md) variable.

## Options

The Set Variable eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **name** | **Required** Name of variable to set a new value The simple language can be used to define a dynamic evaluated variable name to be used. Otherwise a constant name will be used. |  | String |
| **expression** | **Required** Expression to return the value of the variable. |  | ExpressionDefinition |

## Exchange properties

The Set Variable eip has no exchange properties.

## Example

The following example shows how to set a variable on the exchange in a Camel route:

-   Java
    
-   XML
    

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

### Setting an variable from a message header

You can also set a variable with the value from a message header.

-   Java
    
-   XML
    

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

### Setting variable with the current message body

It is of course also possible to set a variable with a value from anything on the `Exchange` such as the message body:

-   Java
    
-   XML
    

```java
from("direct:a")
    .setVariable("myBody", body())
    .to("direct:b");
```

We use the [Simple](../../4.22.x/languages/simple-language.md) language to refer to the message body:

```xml
<route>
    <from uri="direct:a"/>
    <setVariable name="myBody">
        <simple>${body}</simple>
    </setVariable>
    <to uri="direct:b"/>
</route>
```