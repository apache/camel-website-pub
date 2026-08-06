# Set Property

The SetProperty EIP is used for setting an [Exchange](../../../manual/exchange.md) property.

> **Note**
> An `Exchange` property is a key/value set as a `Map` on the `org.apache.camel.Exchange` instance. This is **not** for setting [property placeholders](../../../manual/using-propertyplaceholder.md).

## Options

The Set Property eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **name** | **Required** Name of exchange property to set a new value. The simple language can be used to define a dynamic evaluated property name. Otherwise a constant name will be used. |  | String |
| **expression** | **Required** The expression whose result is used as the exchange property value. |  | ExpressionDefinition |

## Exchange properties

The Set Property eip has no exchange properties.

## Example

The following example shows how to set a property on the exchange in a Camel route:

-   Java
    
-   XML
    
-   YAML
    

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

```yaml
- route:
    from:
      uri: direct:a
      steps:
        - setProperty:
            name: myProperty
            expression:
              constant:
                expression: test
        - to:
            uri: direct:b
```

### Setting an exchange property from another exchange property

You can also set an exchange property with the value from another exchange property.

In the example, we set the exchange property foo with the value from an existing exchange property named bar.

-   Java
    
-   XML
    
-   YAML
    

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

```yaml
- route:
    from:
      uri: direct:a
      steps:
        - setProperty:
            name: foo
            expression:
              exchangeProperty:
                expression: bar
        - to:
            uri: direct:b
```

### Setting an exchange property with the current message body

It is also possible to set an exchange property with a value from anything on the `Exchange` such as the message body, where we use the [Simple](../../4.18.x/languages/simple-language.md) language to refer to the message body:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:a")
    .setProperty("myBody", simple("${body}"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setProperty name="myBody">
        <simple>${body}</simple>
    </setProperty>
    <to uri="direct:b"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:a
      steps:
        - setProperty:
            name: myBody
            expression:
              simple:
                expression: "${body}"
        - to:
            uri: direct:b
```