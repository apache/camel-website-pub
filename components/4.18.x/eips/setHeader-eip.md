# Set Header

The SetHeader EIP is used for setting a [message](message.md) header.

## Options

The Set Header eip supports 0 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | Sets the note of this node. |  | String |
| **description** | Sets the description of this node. |  | String |
| **disabled** | Disables this EIP from the route. | false | Boolean |
| **name** | **Required** Name of message header to set a new value The simple language can be used to define a dynamic evaluated header name to be used. Otherwise a constant name will be used. |  | String |
| **expression** | **Required** Expression to return the value of the header. |  | ExpressionDefinition |

## Exchange properties

The Set Header eip has no exchange properties.

## Using Set Header

The following example shows how to set a header in a Camel route:

-   Java
    
-   XML
    

```java
from("direct:a")
    .setHeader("myHeader", constant("test"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setHeader name="myHeader">
        <constant>test</constant>
    </setHeader>
    <to uri="direct:b"/>
</route>
```

In the example, the header value is a [constant](../languages/constant-language.md).

Any of the Camel languages can be used, such as [Simple](../languages/simple-language.md).

-   Java
    
-   XML
    

```java
from("direct:a")
    .setHeader("randomNumber", simple("${random(1,100)}"))
    .to("direct:b");
```

Header can be set using fluent syntax.

```java
from("direct:a")
    .setHeader("randomNumber").simple("${random(1,100)}")
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setHeader name="randomNumber">
        <simple>${random(1,100)}</simple>
    </setHeader>
    <to uri="direct:b"/>
</route>
```

See [JSONPath](../languages/jsonpath-language.html#_using_header_as_input) for another example.

### Setting a header from another header

You can also set a header with the value from another header.

In the example, we set the header foo with the value from an existing header named bar.

-   Java
    
-   XML
    

```java
from("direct:a")
    .setHeader("foo", header("bar"))
    .to("direct:b");
```

```xml
<route>
    <from uri="direct:a"/>
    <setHeader name="foo">
        <header>bar</header>
    </setHeader>
    <to uri="direct:b"/>
</route>
```

If you need to set several headers on the message, see [Set Headers](setHeaders-eip.md).