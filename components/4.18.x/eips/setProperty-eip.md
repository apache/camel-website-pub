# Set Property

The SetProperty EIP is used for setting an [Exchange](../../../manual/exchange.md) property.

> **Note**
> An `Exchange` property is a key/value set as a `Map` on the `org.apache.camel.Exchange` instance. This is **not** for setting [property placeholders](../../../manual/using-propertyplaceholder.md).

## Options

The Set Property eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **name** | **Required** Name of exchange property to set a new value. The simple language can be used to define a dynamic evaluated exchange property name to be used. Otherwise a constant name will be used. |  | String |
| **expression** | **Required** Expression to return the value of the message exchange property. |  | ExpressionDefinition |

## Exchange properties

The Set Property eip has no exchange properties.

## Example

The following example shows how to set a property on the exchange in a Camel route:

-   Java
    
-   XML
    

```java
from("direct:a")
    .setProperty("myProperty", constant("test"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setProperty name="myProperty">
        <constant>test</constant>
    </setProperty>
    <to uri="direct:b"/>
</route>
```

### Setting an exchange property from another exchange property

You can also set an exchange property with the value from another exchange property.

In the example, we set the exchange property foo with the value from an existing exchange property named bar.

-   Java
    
-   XML
    

```java
from("direct:a")
    .setProperty("foo", exchangeProperty("bar"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setProperty name="foo">
        <exchangeProperty>bar</exchangeProperty>
    </setProperty>
    <to uri="direct:b"/>
</route>
```

### Setting an exchange property with the current message body

It is also possible to set an exchange property with a value from anything on the `Exchange` such as the message body:

-   Java
    
-   XML
    

```java
from("direct:a")
    .setProperty("myBody", body())
    .to("direct:b");
```

We use the [Simple](../languages/simple-language.md) language to refer to the message body:

```xml
<route>
    <from uri="direct:a"/>
    <setProperty name="myBody">
        <simple>${body}</simple>
    </setProperty>
    <to uri="direct:b"/>
</route>
```